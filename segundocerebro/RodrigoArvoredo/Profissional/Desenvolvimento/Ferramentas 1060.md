---
tags: [desenvolvimento, ferramentas, sites]
---

# Ferramentas 1060

Ramificação de [[Infraestrutura de Sites 1060]]. Ferramentas internas construídas pelo [[Eduardo Porto Teixeira]], vivendo no repositório `1060` (`github.com/1060brand/1060`) — reutilizáveis em qualquer projeto do ecossistema. Snapshot 2026-07-09, pendente de acesso direto do Rodrigo ao repositório.

## bootstrap-site — orquestrador de site novo
`1060/scripts/bootstrap-site/` — colapsa os ~7 passos manuais de criar site novo (Postgres, R2, GitHub, Vercel, OAuth) em 1 comando idempotente/fail-safe com `--dry-run`:
```
npm run bootstrap -- --slug X --type dynamic --client-email cliente@x.com
npm run bootstrap:check        # valida credenciais reais do .env
npm run bootstrap:destroy -- --slug X --confirm X [--drop-db --empty-bucket]
```
Estado (2026-06-22): **completo e validado por execução real** nos dois tipos (estático e dinâmico) — o processo de validação achou e corrigiu bugs que só apareciam em run real (clone assíncrono do GitHub template ainda vazio no momento do clone, `repoId` numérico exigido pela API v13 da Vercel, URL `.vercel.app` sufixada quando o slug já está em uso por terceiro). Única ação manual restante no tipo dinâmico: colar 1 redirect URI no OAuth Client Google compartilhado (~30s, o próprio comando imprime a URL exata). O tipo estático é 100% automatizável até a URL no ar.

## DSX — Design System eXtractor
Repositório separado (`github.com/1060brand/dsx`, fora do monorepo `1060`). CLI em TypeScript + Playwright + Commander + SDK da Anthropic que **extrai o design system completo de um site existente** (tokens visuais, componentes, hover states, layout, responsividade multi-viewport) via headless browser, com exportação multi-formato (md/json/css/figma/tailwind) e reescrita polida via Claude API (flag `--rewrite`). Usado principalmente pra manter brochures fiéis ao site antigo do cliente em migrações (ex.: saída da HostGator). Potencial comercial avaliado como alto — não há ferramenta de mercado equivalente hoje.
```
npx tsx src/index.ts https://site.com -o ds-site.md --timeout 60000
npx tsx src/index.ts https://site.com -o ds-site --format md,json,css,figma,tailwind --rewrite --timeout 60000
```

## falgen — geração de imagem via fal.ai
`1060/scripts/falgen/` — CLI pra gerar (Nano Banana, texto→imagem ou modo edit com foto/logo real como referência) e fazer upscale (AuraSR 4x, fiel ao original; ou Clarity, mais criativo/diffusion) de imagens de marca e mockup. Chave `FAL_API_KEY` no `.env` do repositório `1060`.
```
npm run gen:img -- --jobs scripts/falgen/jobs/<arquivo>.ts
npm run upscale:img -- --model aura
```
Aprendizado central: texto embaralha no modelo generativo — evitar composição pesada em texto, um ícone sem wordmark sai bem mais fiel que um lockup com texto; passar o logo real como referência (`refs`) mantém a marca fiel em vez de redesenhada.

## tinify (tinycomp) — compressão de imagem
`1060/scripts/tinify/compress.ts`, rodado via `npm run min:img`. Engine: pacote oficial `tinify` (TinyPNG). Reduz JPG/PNG/WebP em ~70-90% sem perda perceptível. **Regra dura do Eduardo**: toda otimização de imagem que ELE (ou quem opera nesse fluxo) processa manualmente usa tinify, nunca sharp/squoosh — a única exceção é upload de CLIENTE via painel do próprio produto, que usa sharp (evita estourar a cota free do tinify, 500 compressões/mês). Ver "Regra de ouro" em [[Infraestrutura de Sites 1060]].
```
npm run min:img -- --dir <pasta> --out <destino> [--resize WxH --resize-method fit]
```

## Toolchain de arquivos (sem Python)
A máquina do Eduardo resolve `python`/`python3` pro stub da Windows Store (abre a loja, não executa nada) — **decisão dura registrada: nunca tentar Python** nesse ecossistema. Runtime é Node v24 + binários nativos instalados via winget:
- **Pandoc** — conversão entre md/docx/pptx/html.
- **Poppler** (`pdftotext`, `pdfimages`, `pdftoppm`, `pdfinfo`) — resolve PDFs grandes/com imagem e destrava a leitura nativa de PDF do Claude Code.
- **ImageMagick** — crop/resize/convert de imagem via linha de comando.
- Libs Node auxiliares no repo `1060`: `exceljs` (xlsx/csv), `mammoth` (docx→texto), `sharp` (imagem programática).

Empacotado numa skill `/fileops` (`1060/.claude/skills/fileops/`), com tabela de decisão e os comandos exatos por tipo de operação (conversão, PDF token-safe, imagem, planilha).

## Relacionamentos
- [[Infraestrutura de Sites 1060]] — onde essas ferramentas se encaixam no pipeline de site.
- [[Geração de Sites via IA]] — processo que consome bootstrap-site e DSX na prática.

*Fonte: snapshot da memória do Claude do Eduardo, recebido em 2026-07-09.*
