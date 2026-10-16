---
tags: [projeto, código]
---

# NapShift Web

Ramificação de [[Rodrigo Coelho Freitas]]. Repositório: `c:\Users\Dell\Documents\projetos\napshift-web`.

## Conceito de negócio
Frontend Next.js do mesmo sistema [[NapShift Backend|NapShift]] — não é standalone. A própria memória do projeto declara: "backend e Web são o MESMO sistema em repos separados". O backend é a fonte canônica de contrato HTTP/schema/infra; o frontend consome via REST puro (fetch), sem acesso direto a banco.

Dois portais segregados:
- **`/adm`** — painel interno da agência (clientes/workspaces, equipe, tarefas, planos, financeiro, relatórios, campanhas, agentes de IA, docs técnicos embutidos).
- **`/cliente`** — portal do cliente final (dashboard Kanban, aprovações, plano/assinatura, perfil, referências de marca, eventos, FAQ, bugs).

Mais uma landing page de marketing pública em `/` e fluxo de registro self-service em `/registro`.

## Stack técnica
Next.js 16.2 (App Router/RSC) + React 19.2 + TypeScript · Tailwind CSS v4 · shadcn/ui (estilo `base-nova`, `@base-ui/react` no lugar de Radix) · Recharts, embla-carousel, lottie-react, three.js (fundo da landing), imask, Cloudflare Turnstile · Playwright (58/58 testes E2E) · estado global via React Context (`AuthContext`), sem Redux/Zustand.

Deploy: Vercel, auto-deploy por branch (`main` → produção, `homolog` → homologação).

## Estrutura
`src/app/` (rotas, `_components/` da landing) · `src/components/admin/`, `src/components/cliente/`, `src/components/shared/`, `src/components/ui/` · `src/contexts/auth-context.tsx` (único contexto global) · `src/lib/api.ts` (client HTTP com `Authorization: Bearer` e header `X-Workspace-Id` automáticos) · `src/types/api.ts` (849 linhas, **snake_case deliberado**, espelha contrato HTTP real) · `src/middleware.ts` (proteção via cookie `napshift-token`/`napshift-portal`) · `public/docs/` (documentação HTML do sistema, servida via iframe em `/adm/docs`, sincronizada manualmente a cada mudança de contrato) · `docs/design-system-dashboard.md` (design system muito prescritivo).

## Funcionalidades
Pipeline de conteúdo (Kanban, 9 estados) · múltiplos formatos de post · multi-workspace com troca via `WorkspaceSwitcher` · financeiro/assinaturas (Asaas) · agentes de IA configuráveis (SDR com conexão WhatsApp) · sistema de bugs reportáveis · relatórios (aprovações, clientes, pipeline, produção) · **Campanhas** (feature mais recente) · referências de marca, eventos, notificações · OAuth Google · reset de senha · onboarding guiado.

## Gotchas e convenções
- Trabalhar sempre em `homolog`; push para `main` = deploy automático. *(Atualizado 2026-09-22: trabalho em branch `feat/`/`fix/` saindo de `homolog`; `main` só via `npm run release` — ver [[DevOps e Testes]].)*
- `.claude/memory/` própria de UI, aponta (não duplica) para a memória canônica do backend em `../../../NapShift/.claude/memory/` — evita expor dados sensíveis de infra se alguém receber só este repo.
- `src/types/api.ts` é snake_case por decisão consciente, mesmo o backend usando camelCase internamente após migração Drizzle.
- Skill `/wrapnap` (no repo 1060) faz verificação cruzada entre endpoints alterados no backend e a documentação HTML estática deste frontend, atualizando-a automaticamente.
- `WorkspaceSwitcher` migrado de `base-ui` `DropdownMenu` para popover custom via `createPortal` + `position: fixed` — bug de stacking context com `overflow-y-auto` aninhado na sidebar.
- **Next.js 16.2 é tratado como "não confiável" para conhecimento de treino de LLM** — regra hardcoded em `AGENTS.md`: sempre checar `node_modules/next/dist/docs/` antes de codar. Suspense boundary obrigatório em qualquer página com `useSearchParams`.
- Autenticação dual-portal via cookie `napshift-portal` (`adm`|`cliente`) + JWT.
- Design system prescritivo: sidebar sempre escura, cards flat sem sombra, paleta roxo+amarelo, tom de voz irreverente em empty states — checar `docs/design-system-dashboard.md` antes de qualquer trabalho visual novo.

## Frentes ativas (2026-07-07)
Módulo de Campanhas (novo) · correções de timezone/formatação de datas · hard delete de tarefas · refinamento do fluxo de ativação de workspace · rename "Gerentes" → "Equipe" · manutenção disciplinada da documentação HTML a cada mudança de contrato.

## Implementação em profundidade

**Auth dual-portal (`auth-context.tsx`)**: JWT vive só no cookie `napshift-token` (sem localStorage, sem refresh token); portal ativo em cookie separado `napshift-portal`. `isADM`/`isGerente`/`isCliente` são derivados só de `user.tipo` (vindo do backend), não do cookie de portal. No mount, busca `/me` (cliente) ou `/adm/me` (demais) e aplica via `applyMe`. **Troca de workspace** é o fluxo mais delicado: seta o workspace ativo localmente **antes** de chamar o backend (assim o próprio `POST /me/workspace-ativo` já sai com o header `X-Workspace-Id` novo), recebe de volta um **JWT reemitido**, e só faz `setToken()` — sem reload nem logout, porque todo request subsequente já lê o cookie atualizado. `switchWorkspace` não existe fora do portal cliente.

**Terceiro mecanismo de workspace** (`src/lib/workspace-active.ts`): além do JWT (claim `wsa`) e do cookie de portal, existe uma variável de módulo + espelho em `localStorage["napshift-workspace-ativo"]` — é o que `api.ts` lê pra montar o header `X-Workspace-Id` a cada request, permitindo trocar de workspace sem esperar o JWT novo chegar.

**Cliente HTTP (`api.ts`)**: injeta `Authorization` e `X-Workspace-Id` automaticamente (caller pode sobrescrever o segundo manualmente). No 401, exclui explicitamente requests para `/login` (senão uma tentativa de login errada já dispara redirect) e decide o portal de destino em cascata: cookie → prefixo da URL atual → default `"adm"`. É hard navigation (`window.location.href`), o que evita loop porque a tela de login não dispara chamada autenticada sozinha. Upload de arquivo tem um path paralelo (`uploadRequest`) que duplica essa lógica em vez de reusar `request()`.

**Middleware (`middleware.ts`) — gap conhecido**: só checa a **presença** do cookie `napshift-token` (não decodifica/valida o JWT) e redireciona pelo **prefixo do path acessado**, não pelo cookie de portal. Ou seja: um usuário logado como cliente que digitar `/adm/qualquercoisa` manualmente **não é barrado pelo middleware** — a proteção real fica a cargo do backend rejeitar o JWT errado (401 → interceptor do `api.ts`). Vale lembrar disso se for mexer em rotas sensíveis.

**Wizard de novo workspace** (`/cliente/workspaces/novo`): estado 100% local (`useState`, sem reducer/contexto), 3 passos sem chamada de API entre eles. Cartão é tokenizado direto no Asaas (`POST /cliente/asaas/tokenize-card`) — **o número do cartão nunca chega ao backend próprio**, só o token. Exige `cpf_cnpj` e endereço completos no perfil antes de liberar o passo final (senão redireciona para completar perfil).

**`WorkspaceSwitcher`**: popover custom com `createPortal(document.body)` + `position: fixed`, calculado via `getBoundingClientRect()` do trigger — contorna dois containers com `overflow-y-auto` aninhados na sidebar que quebravam o `DropdownMenu` do base-ui. Fecha em clique-fora (listener global) e Escape; nunca renderiza fora do portal cliente.

## Estado em 2026-09-29 (leitura completa do repositório)

Mudanças desde o estudo de julho — algumas corrigem o que está escrito acima:
- **`src/middleware.ts` virou `src/proxy.ts`** (2026-07-27): convenção do Next 16, função exportada `proxy`. O comportamento é o mesmo — só confere a presença do cookie `napshift-token`; a proteção real continua no backend.
- **Documentação HTML do sistema saiu de `public/docs/`** (2026-09-25): tudo em `public/` é servido sem login, e as páginas de API, banco e serviços ficaram abertas em `napshift.com/docs`. Hoje vivem em `docs/sistema/`, só no repositório. Regra: documentação interna nunca em `public/`.
- **Botões de contratar da landing apontam pro WhatsApp comercial** (constante `CTA_CONTRATAR_HREF` em `src/lib/constants.ts`) enquanto a cobrança do Asaas estiver em sandbox. Quando existir a conta de produção, a constante volta pra `/registro`.
- **401 só encerra a sessão quando o corpo é de auth** (2026-09-14): um 401 do Asaas vazado pelo backend chegou a deslogar o ADM.
- **Base UI `<Select>` precisa da prop `items`** pra mostrar o rótulo em vez do valor cru — bug que estava em 48 selects herdado da migração Radix → Base UI.
- Telas novas do período: fotos com envio em lote, visualizador de slides no ADM (versões, ressalvas, tokens), "Salvar como template", "Pedir ajuste" com ajuste pontual por slide, notificações com deep-link, seleção de conta Meta por canal, encerramento/reabertura de workspace (em `homolog`).
- **Versão:** 1.2.0, mesmo número do backend. Release do Web sai com `--sem-testes` porque o lint tem 191 erros antigos (o `tsc` passa).
- **Armadilha pra rodar local:** sem `NEXT_PUBLIC_API_URL`, o `src/lib/api.ts` aponta pra API de **produção**. Usar `.env.local` apontando pra `https://homolog-api.napshift.com`.
- **Vercel Hobby tem um membro só:** commit de outro autor (Rodrigo) pode ter o deploy bloqueado até a conta virar Pro.
- Tabela de preços da landing (fechada em 2026-08-04): Starter R$ 397, Pro R$ 497, Escala R$ 897; SDR só a partir do Pro. O banco (`agencia_planos`) é a fonte de verdade — ao mudar plano, conferir os dois lados.

## Estado em 2026-10-16 (leitura completa do repositório, homolog em `ba802ff`)

- **Agora se chama `napshift-app`** (renomeado em 2026-10-01). Produção em **app.napshift.com**; este deploy ainda serve a landing antiga em napshift.com e redireciona as rotas de portal (307) para o subdomínio. O site novo (`napshift-site`) já serve napshift.com desde 2026-10-05.
- Versão 1.4.0. ~30 mil linhas, 62 páginas. Next 16.2.0, React 19.2.4, Base UI, Tailwind 4. `tsc` limpo.
- **Corrige o que está acima:** o desenvolvimento local **não aponta mais para produção** — sem `NEXT_PUBLIC_API_URL`, o `npm run dev` fala com homolog por um proxy `/_api`, e apontar para produção exige `NEXT_PUBLIC_ALLOW_PROD=1` (2026-10-09, BACKLOG 10.13). Credenciais de teste por papel (ADM, GERENTE, CLIENTE) ficam no `.env.test` local (não existe nesta máquina).
- **Corrige o que está acima:** o lint tem hoje **37 erros** (30 `no-explicit-any`, 6 `set-state-in-effect`, 1 `immutability`) e 40 avisos, não 191. E a suíte Playwright **não serve de rede** (auditoria de 2026-10-09): a última execução registrada é de abril, contra outro projeto na porta 3000, com specs quebrados.
- **Cores reais da marca:** `#6D3CFA` e `#121423` (a paleta `#7C3AED` do design system antigo nunca bateu com o arquivo do logo).
- **Cobrança no portal (v1.3.0):** o estado vem pronto do backend e o front só lê (`src/lib/cobranca.ts`); modo leitura com `PagamentoBanner`/`EncerradoBanner` no layout; tela reage ao `motivo` do erro, nunca ao texto; assistente de assinatura virou componente usado em "novo workspace" e "reassinar".

### O redesenho do portal (branch `feat/redesign-portal`)
- Redesenho completo do painel ADM/GERENTE e do portal do cliente, na **identidade nova** (roxo `#6D3CFA`, fontes Instrument Sans/Serif e Fragment Mono, tema claro e escuro), numa branch longa com **release única**. Decisão do Eduardo (2026-10-09): troca só o front, contra o backend atual (congelado); o que falta de backend virou o G12 de [[NapShift Backend]].
- **Em 2026-10-16 ainda é só documento**, nenhuma tela nova: F0 (ambiente seguro) e F1 (inventário e regras de negócio) feitas. Próximo: **F2**, arquitetura e protótipo navegável, aprovado pelo Eduardo no "Gate A" antes de qualquer código de tela. Depois: F3 (fundação), F4 (ondas de telas W1–W6), F5 (release).
- **Já decidido:** portal do cliente com linguagem simples ("Tarefas" vira "Postagens", a URL não muda); `/adm` vira a fila "Hoje"; gerente remarca pelo calendário (com travas no front até o G12); aprovação do gerente pelo portal (botões ligam quando o 12.1 sair); TanStack Query.
- **10 decisões abertas para o Gate A**, entre elas: cliente aprovar pelo portal mesmo com canal WhatsApp; Fotos e Referências virarem "Sua marca"; kanban do cliente virar "esta semana" + calendário; o que "Cliente ativo" e "Ativo" fazem com a cobrança.
- **Material de estudo:** `docs/redesenho/01-regras-de-negocio.md` (na branch longa) explica, com arquivo e linha, como datas, aprovação, ativação e cobrança funcionam de verdade e onde o portal atual engana. Exemplo: desligar o "Ativo" de um workspace cancela a assinatura no Asaas, sem confirmação; o `PUT` de tarefa aceita data `null`, ignora fuso e não confere cota.

### Nesta máquina
Pasta `napshift-web`, remoto `napshift/napshift-web.git` (funciona pelo redirecionamento). `node_modules` instalado em 2026-10-15.

## Relacionamentos
- Consome [[NapShift Backend]] via REST puro (contrato snake_case).
- Parte do mesmo produto vendido via [[1060crm]].

*Estudo de base: 2026-07-07. Aprofundado (auth, HTTP client, middleware, wizard, switcher): 2026-07-07. Atualizado com leitura completa: 2026-09-29.*
