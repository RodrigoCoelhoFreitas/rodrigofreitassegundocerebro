---
tags: [desenvolvimento, sites, cliente, código]
---

# Mundo da Lua

Ramificação de [[Sites 1060]]. Site do Mundo da Lua Podcast (conversas sobre tecnologia, inovação e empreendedorismo; a 1060 é parceira), em **https://www.mundodaluapod.com**. Contato do cliente: Armim. Repo `1060brand/mundodalua`, clonado em `projetos\mundodalua` em 2026-11-10; 67 commits desde 2026-08-25, 13 episódios publicados (EP013 em 2026-10-06).

É o exemplo de **site cinemático** da 1060 ("vitrine máxima da 1060": provar em 10 s que a marca tem universo próprio). Padrão geral em [[Padrão de Sites 1060]].

## O que tem de diferente

- **Não nasceu dos templates**: `create-next-app` puro + GSAP, sem `lib/site.ts`/`schema.ts` do template (a camada de SEO veio depois, em 2026-09-15: robots, grafo de entidades na home, datas reais, redirect de aliases, OG). Tem `CLAUDE.md`/`AGENTS.md` gerados pelo `next dev` ("This is NOT the Next.js you know": ler `node_modules/next/dist/docs/` antes de escrever código).
- **SSG data-driven**: publicar episódio é escrever dados (`src/data/episodios.ts`, `convidados.ts`, `conteudo/ep0NN.ts`), nunca criar rota. Home, acervo, tripulação, páginas de pessoa, sitemap e JSON-LD derivam disso.
- Transcrições do YouTube versionadas em `conteudo/transcricoes/EP0NN.sbv`.
- Experiência: eclipse procedural em WebGL sob scroll (pin de 500svh), cockpit de nave como chrome global entre rotas, tripulação de astronautas com tubos de oxigênio em física Verlet, Lunar Lander jogável como easter egg, abdução na página de contato, som 100% procedural (WebAudio, desligado por padrão, só começa por gesto), holograma 1060 no rodapé. O `DESIGN.md` registra cada versão e cada reversão pedida pelo Eduardo.
- Paleta do manual (Pantone): preto azulado `#0a0e16` (nunca `#000`), azuis `#004d8c`/`#5cd5ff` como luz do mundo, magenta `#ef2297` como acento único só em display grande. Archivo variável com a largura como voz de display.

## A skill /mundodalua

`.claude/skills/mundodalua/` (no repo) publica um episódio de ponta a ponta em 15 passos: dados do YouTube por script → transcrição no repo → ler o episódio inteiro → capítulos ancorados em cues reais → copy do YouTube conferida por script (≤ 5.000 caracteres e bytes) → nota no vault do Eduardo → imagens pelo tinify → dados do site → transcrição revisada por 4 agentes em paralelo → conteúdo da página → build e conferência com screenshots → vault → commit `feat(episodios): EP0NN …` + push → playlists → mensagem pronta para o convidado. É o melhor modelo de **skill de operação recorrente de cliente** da 1060. Os caminhos (`C:\Users\eduar\...`, pasta Temporaria) são da máquina do Eduardo.

Checks que já pegaram erro de verdade: descrição contada, nunca estimada; capítulos tirados da legenda, nunca da lista da equipe; nome próprio confirmado em fonte escrita (a legenda automática erra); o script do YouTube testado contra episódios conhecidos depois de qualquer mudança.

## Relacionamentos

- [[Produto Sites]] — portfólio.
- [[Ferramentas 1060]] — falgen, BiRefNet (`bgremove.mjs`) e tinify nos astronautas.

*Leitura do código e da skill: 2026-11-10.*
