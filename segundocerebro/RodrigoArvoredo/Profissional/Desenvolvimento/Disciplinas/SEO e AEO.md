---
tags: [desenvolvimento, seo, aeo, marketing]
---

# SEO e AEO

Ramificação de [[Disciplinas]]. É item vendido em TODO plano de site da 1060 Brand — "SEO — otimização para o Google" e "AEO — otimização para respostas de IA" aparecem lado a lado na proposta comercial. Precisa virar prática real, não só promessa de venda.

## Estado do ecossistema (2026)

- **Core Web Vitals** trocou FID por **INP** (Interaction to Next Paint) como métrica oficial desde 2024 — os 3 pilares hoje são LCP (carregamento), INP (responsividade) e CLS (estabilidade visual). Em Next.js, boa parte vem de graça se o projeto usa os primitivos certos: `next/image` (dimensiona e faz lazy load, evita CLS), `next/font` (self-host, sem FOUT/FOIT), Server Components reduzindo JS no cliente.
- **Metadata API** (App Router) é a forma correta de gerar `<title>`, description, canonical, Open Graph — via export estático `metadata` ou `generateMetadata()` assíncrono para rotas dinâmicas; resolve hierarquicamente entre `layout.tsx` e `page.tsx` (filho sobrescreve pai, sem merge automático).
- **`sitemap.ts`/`robots.ts`** são file conventions tipadas (`MetadataRoute.Sitemap`/`Robots`), não XML/txt à mão — versionáveis em código, particionáveis com `generateSitemaps()` acima de 50k URLs.
- **JSON-LD (schema.org)** continua o formato universal, parseado por Google e por sistemas de IA — injetado via `<script type="application/ld+json">` num Server Component com `JSON.stringify()`. Para site institucional, o que importa é `Organization`/`LocalBusiness` (nome, logo, endereço, telefone, redes sociais), `FAQPage`, `Article`.
- Google **descontinuou o rich result visual** de FAQPage/HowTo (2023, mais restrito ainda em jun/2026 — só sobra pra sites institucionais/saúde/governo) — mas o schema segue sendo **parseado como contexto pelos modelos generativos**: engenheiro do Google confirmou publicamente que structured data alimenta o "fanout" de sub-queries do AI Overviews. Ou seja: FAQPage não dá mais o acordeão bonito no Google clássico, mas ainda ajuda a ser citado por IA.
- **AEO/GEO** ("Answer/Generative Engine Optimization") é o nome que o mercado deu (2024-2026) a otimizar conteúdo para ser **extraído e citado** por ChatGPT Search, Perplexity, AI Overviews e Gemini — não é ranking de link azul, é "ser a fonte que o modelo cita ou parafraseia". Grande overlap com SEO clássico (mesmos sinais de autoridade), com ênfases próprias: resposta direta nas 1-2 primeiras frases de cada seção (o extrator de IA lê o começo do bloco pra decidir se "responde"), dado concreto citável a cada ~150-200 palavras, clareza de entidade (nome, localização, o que a empresa faz, sem ambiguidade com concorrente homônimo), autor nomeado se há blog (E-E-A-T: experiência real, não algo que um LLM inventaria).
- **Freshness pesa mais em AEO que em SEO**: parcela relevante das citações de IA em queries comerciais vem de páginas atualizadas nos últimos 6-12 meses. Perplexity favorece conteúdo recente; ChatGPT favorece autoridade de long-form; Google AI Overviews majoritariamente puxa de quem já está no top 10 orgânico — AEO sem SEO de base não sustenta sozinho.
- **`llms.txt`** (markdown na raiz resumindo o site pra IA) virou moda de proposta em 2024-2025, mas em 2026 os dados mostram que **crawlers de IA de busca praticamente não o buscam** — GPTBot, ClaudeBot, PerplexityBot leem HTML direto, e Google confirmou publicamente que não usa nem pretende usar. Funciona de fato é como insumo pra agentes de código (Cursor, Claude Code, Copilot) apontados numa doc técnica — não pra citação em resposta de busca por IA. Custo zero de implementar, não vale vender como diferencial forte.
- Item técnico simples e recorrente em todo checklist de AEO 2026: permitir explicitamente os user-agents de IA no `robots.txt` (`GPTBot`, `PerplexityBot`, `ClaudeBot`, `Google-Extended`) — sem isso, o site pode estar bloqueado justamente dos motores que alimentam as respostas de IA, mesmo indexando bem no Google tradicional.

## Quando isso importa

Os Termos de Prestação de Serviços da 1060 Brand (v1.0, jul/2026) — ver [[Produto Sites]] — incluem SEO e AEO em todo plano (Essencial/Profissional/Premium), com cláusula explícita de não-garantia: "a Contratada não garante resultados específicos — como posicionamento em buscadores, volume de tráfego ou vendas. As otimizações de SEO e AEO seguem boas práticas e não constituem garantia de classificação." É entrega de **processo** (aplicar boas práticas), não de **resultado** — o que muda o que precisa existir de fato: uma lista fixa e auditável de práticas, não uma promessa de posição.

Isso não é código do [[1060crm]] (o CRM não constrói site nenhum, só vende e acompanha a deal) — é responsabilidade de qualquer que seja o repositório/processo real de produção de sites da 1060 Brand, hoje fora dos 3 projetos estudados. Ainda assim, vale fixar aqui a lista concreta que sustentaria o pitch comercial ("achável no Google e nas respostas de IA", lado a lado no discurso de vendas do [[Produto Sites]]) com prática real:

1. Metadata API preenchida por página (title/description únicos, sem duplicar entre as páginas do institucional).
2. `sitemap.ts` + `robots.ts` versionados, com `Allow` explícito para GPTBot/PerplexityBot/ClaudeBot/Google-Extended.
3. JSON-LD `LocalBusiness`/`Organization` em toda página — nome, endereço, telefone, redes sociais reais (dá pra auditar se já existe no portfólio citado na proposta: saritabordini.com, pontografico.com.br, juliosecco.com, lealsantos.com).
4. Core Web Vitals verdes via `next/image` + `next/font` por padrão, não como decisão manual por projeto.
5. Seção de perguntas frequentes por página de serviço, resposta direta nas 2 primeiras frases — `FAQPage` schema é bônus, o texto já responde sem ele.
6. `llms.txt` de baixo custo/baixo retorno: incluir se sobrar tempo, nunca vender como diferencial de peso.
