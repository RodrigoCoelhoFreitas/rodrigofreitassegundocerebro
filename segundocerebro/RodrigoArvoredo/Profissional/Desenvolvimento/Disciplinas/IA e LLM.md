---
tags: [desenvolvimento, ia, llm, claude, prompt-engineering]
---

# IA e LLM

Ramificação de [[Disciplinas]]. O coração do produto NapShift — um pipeline inteiro de agentes de IA que produz conteúdo de social media automaticamente.

## Estado do ecossistema (2026)

- **Claude API/SDK**: linha atual é Sonnet 4.5 → 4.6 → 5, com Sonnet 4.6 marcado pela Anthropic como "full upgrade" em coding, computer use, raciocínio de contexto longo e planejamento de agentes; Sonnet 5 acrescenta controle fino de "thinking effort" via API. **Structured outputs** (JSON Schema nativo, validado do lado da API, não mais só instrução em texto) chegaram a GA para Sonnet 4.5/4.6/5 — reduzem a dependência de "responda só em JSON" como boa vontade do modelo. **Tool use avançado** (Tool Search Tool, Programmatic Tool Calling, Tool Use Examples) GA em Sonnet 4.6, pensado pra agentes com dezenas/centenas de tools sem estourar contexto.
- **Prompt caching**: cache efêmero via `cache_control: {type: "ephemeral"}` em blocos de system prompt/tools/documentos — TTL de 5 min (escrita a 1.25x do input) ou 1h (escrita a 2x), leitura cacheada a **0.1x** do preço normal (~90% de economia). Crítico pra agentes que repetem o mesmo bloco grande de identidade de marca a cada chamada.
- **fal.ai**: hub de inferência que hospeda os modelos de imagem do momento — hoje o par relevante é **Nano Banana 2** (Gemini 3.1 Flash Image, geração ~5-10s, ~US$0,08/imagem) e **Nano Banana Pro** (Gemini 3 Pro Image, raciocínio mais pesado, 4K, edição ~US$0,15), ambos com "reasoning-guided generation", validação de texto renderizado caractere a caractere e consistência de personagem entre imagens — resolve o problema clássico de geração de imagem de marca (logo/produto consistente entre posts).
- **Parsing de JSON de saída de LLM**: problema de produção real, não teórico — um levantamento de ~288 chamadas logadas (maio/2026) mapeou as formas recorrentes de quebra: aspas/backslash mal escapados, saída envolta em fence ```json```, truncamento por limite de token cortando o JSON no meio, coerção de tipo errada. Duas escolas convivem: (1) **tool use / structured output nativo**, que valida contra schema do lado da API antes de devolver texto solto; (2) **parser defensivo em cascata** (JSON.parse direto → strip de fence → extração de span por regex/bracket-matching) como rede de segurança, porque nem toda saída passa por tool use e um erro 500 em produção por causa de output malformado custa caro. Bibliotecas de "JSON repair" (reconstroem JSON quebrado em vez de só extrair) são a camada seguinte, ainda pouco adotada — a maioria dos pipelines em produção para no parser em cascata e confia na obediência do prompt.

## Quando isso importa

O [[NapShift Backend]] é onde isso vira código, não teoria. Usa `@anthropic-ai/sdk` com `claude-sonnet-4-6` — ainda não migrado pra structured outputs nativo — para 4 dos 5 agentes do pipeline: **estrategista** (plano de conteúdo semanal via cron toda segunda 8h, ou disparo pontual por campanha), **copywriter** (copy/legenda/hashtags a partir de um schema de saída JSON), **diretor de arte** e **produtor**; o **avaliador** existe mas hoje é mockado, sem métricas reais do Instagram Insights ainda plugadas.

Não existe orquestrador central — cada agente roda seu próprio `node-cron` de 1 minuto e descobre trabalho filtrando a tabela `tarefas` por status; o "roteamento" entre estrategista → copywriter → diretor de arte → produtor é implícito no status gravado, não uma fila ou event bus. É polling, não push — consequência direta de nunca ter sido adotado um framework de orquestração.

O prompt do Estrategista mistura um system prompt fixo por workspace (identidade de marca, estratégia, formatos ativos) com uma user message dinâmica (histórico recente pra não repetir tema, banda semanal de posts, eventos) — candidato natural a prompt caching, ainda não implementado. A saída esperada é um array JSON, e quem resolve isso é `extract-json.ts`: três estratégias em cascata (JSON.parse direto → bloco ```json``` → regex genérica do primeiro `[`/`{` ao último `]`/`}`), sem reparo de JSON malformado — exatamente o "parser defensivo em cascata sem repair" descrito acima, dependente de o LLM obedecer "responda só com JSON".

Geração de imagem passa por fal.ai (Nano Banana 2/Gemini) com fallback em cascata pra DALL-E 3 (OpenAI) se fal.ai falhar — redundância de provedor, não só de modelo. Classificação de feedback do WhatsApp também é feita por LLM (Claude, temperature 0.0): decompõe a mensagem livre do cliente em ações categorizadas (copy/legenda/arte/estratégia), com uma camada determinística de prioridade por cima decidindo o status final quando há múltiplas ações. E o SDR ("Bia") foge do padrão Claude do resto do sistema: usa **GPT-4o-mini** (OpenAI) por custo/latência, com **Groq/Whisper** pra transcrição de áudio — mistura de provedores deliberada, não indecisão.

*Pesquisado e escrito em 2026-07-07.*
