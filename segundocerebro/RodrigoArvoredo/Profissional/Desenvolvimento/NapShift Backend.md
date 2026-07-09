---
tags: [projeto, código]
---

# NapShift Backend

Ramificação de [[Rodrigo Coelho Freitas]]. Repositório: `c:\Users\Dell\Documents\projetos\napshift`.

## Conceito de negócio
NapShift é uma "agência de marketing IA-first": o nome vem de "Nap" (cochilo) + "Shift" (turno) — "enquanto você tira um cochilo, a gente está no turno". Vende gestão de redes sociais para clientes (pequenas/médias marcas), substituindo o trabalho humano de social media por um **pipeline de agentes de IA** (estrategista, copywriter, diretor de arte, produtor, publicador, avaliador) que cria conteúdo para Instagram/Facebook, envia para aprovação via WhatsApp (interna e do cliente), publica automaticamente e coleta métricas. Também há um agente **SDR conversacional ("Bia")** que atende leads via WhatsApp.

Multi-tenant: cada cliente é um **workspace**, com plano comercial e cobrança via Asaas.

## Stack técnica e deploy
TypeScript (ESM) + Fastify 5 + Postgres 17 + Drizzle ORM (schema introspectado via `drizzle-kit pull`, banco é a fonte de verdade) + `@anthropic-ai/sdk` (Claude, `claude-sonnet-4-6`) + fal.ai (Nano Banana 2/Gemini, imagem) + Puppeteer (templates HTML→PNG) + Cloudflare R2 (primário) + Supabase Storage (fallback hot-standby) + Evolution API (WhatsApp self-hosted) + node-cron + Pino + Asaas (pagamentos) + Groq/Whisper (transcrição SDR) + OpenAI (fallback + modelo do SDR: `gpt-4o-mini`) + SearXNG.

Deploy manual via Easypanel (produção `api.napshift.com` / homolog `homolog-api.napshift.com`). **Regra: trabalhar sempre na branch `homolog`.**

## Estrutura
`src/agents/` (os 7 agentes) · `src/approval/` (fluxo WhatsApp) · `src/pipeline/` (orquestrador + máquina de estados) · `src/routes/` (`adm.ts` e `cliente.ts` são os maiores) · `src/services/` (integrações externas) · `src/sdr/` (agente Bia) · `src/db/` (DAOs por domínio, schema.ts introspectado) · `collection/` (coleção Postman, documentação viva da API) · `templates/` (HTML→PNG via Puppeteer, com variantes por cliente).

## Modelo de dados (essência, prefixo `agencia_`/`sdr_`)
- `agencia_workspaces` — um cliente/conta, config de marca/estratégia/formatos/aprovação inline.
- `agencia_usuarios` + `agencia_usuario_workspaces` (N:N, papel OWNER/ADMIN/MEMBRO) — unifica MARVIN/ADM/GERENTE/CLIENTE/LEAD.
- `agencia_tarefas` — tabela mais rica: pipeline de conteúdo, status via CHECK, `campanha_id` opcional.
- `agencia_aprovacoes`, `agencia_feedbacks`, `agencia_metricas` — fluxo de revisão e resultado.
- `agencia_planos`/`agencia_assinaturas`/`agencia_pagamentos` — comercial (Asaas).
- `agencia_formatos` — capacidade técnica (o que o sistema sabe produzir), separado do limite comercial do plano.
- `sdr_agentes`/`sdr_leads`/`sdr_conversas`/`sdr_mensagens` — SDR.

Migração 046 (radical): eliminou `agencia_clientes`/`agencia_configuracoes`, fundiu tudo em usuarios/workspaces — código/doc antiga citando essas tabelas está obsoleta.

## Máquina de estados do pipeline
`COPY → ARTE → PRODUCAO → REVIEW_I/REVIEW_C → PUBLICAR → AVALIACAO → CONCLUIDO`, alternativa terminal `CANCELADO`. REVIEW_I = aprovação interna da agência, REVIEW_C = aprovação do cliente (depende de flags do workspace).

## Gotchas e convenções
- **camelCase interno (Drizzle) vs. snake_case no contrato HTTP** — fonte recorrente de bugs (JSONB com chaves não convertidas). Drizzle só remapeia nome de coluna, não chaves dentro de um JSONB.
- Nunca `JSON.stringify` antes de gravar em coluna `jsonb` — o driver `pg` já serializa.
- Migrations manuais (`drizzle/*.sql`) aplicadas via DBeaver, não automático — fica pendente com frequência.
- Telefones armazenados sem o 9º dígito (padrão BR antigo).
- Dois eixos ortogonais de formato: `agencia_formatos.ativo` (capacidade técnica) vs. `agencia_planos.limite_formatos` (regra comercial) — não confundir.
- Storage dual: R2 primário, Supabase fallback automático em erro Meta 9004/2207052.
- Nunca usar `placehold.co`/URLs externas para imagem de teste — Instagram rejeita; há placeholder fixo no R2.
- SDR usa GPT-4o-mini (não Claude) por custo/latência.
- `.claude/memory/projeto.md` tem seção "Estados recentes" cronológica — fonte mais confiável de "por que uma decisão foi tomada".

## Frentes ativas (2026-07-07)
App Review da Meta (ainda incompleto) · feature de Campanhas (trigger pontual do Estrategista) · correções pós-migração Drizzle (camelCase/snake_case em cascata) · estabilização da ativação de workspace · gate de capacidade técnica de formatos.

## Implementação em profundidade

**Não existe orquestrador central de pipeline.** `pipeline/runner.ts` só serve pra teste manual (chama os agentes em sequência fixa). Em produção, cada agente roda seu próprio `node-cron` **a cada 1 minuto** (`src/index.ts`) e faz sua própria query filtrando `tarefas` pelo `status` que lhe interessa (ex: Copywriter busca tarefas em `COPY`). O "roteamento" é implícito: um agente termina, grava o novo status, e no próximo tick (até 1 min) o agente dono daquele status pega a tarefa. `cronGuard` evita sobreposição se a execução anterior ainda estiver rodando. `status-machine.ts` só fornece as funções puras de decisão (`isValidTransition`, `getStatusPosProducao`, `getStatusPosAprovacaoInterna`, `getStatusDestinoFeedback`), chamadas pelos agentes/handlers — não é ela quem dispara nada.

**3 formas de uma tarefa nascer**, sempre via `runEstrategista`: (1) cron semanal (segunda 8h) pra todos workspaces ativos; (2) trigger pós-onboarding com `forceImmediateProduction`, que pula a regra normal de "2 dias úteis antes da publicação"; (3) campanha pontual disparada por `POST /adm/campanhas`, que pode rodar com `consomeCredito=false` (bypassa cota).

**Prompt do Estrategista** é montado em duas partes: system prompt fixo por workspace (identidade, estratégia, público, formatos ativos — que depois viram **hard filter** de saída) e user message dinâmica (histórico recente pra não repetir tema, banda semanal de posts, eventos da janela, referências filtradas por tipo). Saída é um array JSON parseado por `extract-json.ts`, que tenta 3 estratégias em cascata (`JSON.parse` direto → bloco ```json``` → regex genérica do primeiro `[`/`{` ao último `]`/`}`) e não faz reparo de JSON malformado — depende do LLM obedecer "responda só com JSON". Cada tarefa gerada passa por filtro de formato produzível, limite de plano, plataformas válidas e corte no teto antes de virar linha em `tarefas`.

**Classificação de feedback do WhatsApp é feita por LLM, não regra fixa** (`approval/handler.ts`): a Claude decompõe a mensagem livre em ações com `categoria` (copy/legenda/arte/copy_arte/estrategia) e `auto_corrigivel`. Por cima disso, uma camada determinística resolve o status final quando há múltiplas ações (`STATUS_PRIORIDADE`: COPY vence ARTE) e decide se some é auto-corrigível o suficiente pra não reprocessar o pipeline. Campos de config editáveis por feedback são restritos por whitelist. Trava dura: se a tarefa já bateu o limite de tentativas, o handler intercepta **antes** de chamar a Claude e só aceita "APROVAR/OK/SIM" ou "CANCELAR/NÃO" literal.

**Renderização (`services/renderer.ts`)**: Puppeteer com browser Chromium singleton, JS desabilitado na página (templates são estáticos), e — ponto de segurança relevante — **interceptação de requests bloqueando qualquer host fora de uma allowlist** (fonts do Google + o host configurado de R2/Supabase), proteção contra SSRF via template malicioso. Placeholders `{{variavel}}` viram texto vazio se ausentes (nunca aparece "undefined"), e `*texto*` vira destaque via regex, exceto chaves técnicas na blacklist (cores, URLs). PNG final é validado por tamanho mínimo (10KB) como heurística de página em branco.

**Hot-swap R2↔Supabase não é genérico** — é disparado só pelo publicador do Instagram (`services/instagram.ts`) detectando o código exato `9004`/subcode `2207052` que a Graph API retorna quando não consegue baixar a `image_url` fornecida (bloqueio de fingerprint do storage primário, observado desde 2026-04-22). Ao detectar, baixa o arquivo do provider atual e regrava no fallback **com o mesmo nome de objeto** (idempotente), com cap de 1 retry.

## Primeiro cliente real (via snapshot 2026-07-09)
**AEMJS** (Associação Equipe Mestre Julio Secco) — entidade de jiu-jitsu, 16 unidades no sul do Brasil, ~500 atletas; a 1060 já tinha feito marca e site dela antes (juliosecco.com, ver [[Produto Sites]] portfólio). Onboarding feito em 2026-05-26 pelo Eduardo, com uma skill dedicada (`/onboardnap`) que lê material bruto do cliente e gera a configuração NapShift pronta pra colar no portal. Escolhido como primeiro caso por ser cliente próximo/baixo risco, não por processo formal de vendas — a comissão/processo comercial do NapShift como produto ainda não existe (ver [[Vendas]]).

## Relacionamentos
- Consumido por [[NapShift Web]] (frontend) via REST puro, contrato em snake_case.
- Vendido como produto via [[1060crm]].

*Estudo de base: 2026-07-07. Aprofundado (pipeline, prompts, feedback, renderer, storage): 2026-07-07.*
