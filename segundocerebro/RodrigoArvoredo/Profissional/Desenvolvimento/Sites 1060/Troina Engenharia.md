---
tags: [desenvolvimento, sites, cliente, código]
---

# Troina Engenharia

Ramificação de [[Sites 1060]]. Site da Troina Engenharia e Consultoria (Simone Troina, engenheira civil e de segurança do trabalho, perita; Valença/BA), em **https://www.troinaengenharia.com** desde 2026-09-29. Repo `1060brand/troinaengenharia`, clonado em `projetos\troinaengenharia` em 2026-11-10; 19 commits, quase todos do dia do lançamento.

É **o modelo mais completo do processo documentado**: único repo com as três etapas em arquivo (`docs/briefing.md`, `docs/conceito.md`, `docs/presenca.md`) e um `DESIGN.md` com quality gate e medição no domínio final. Para começar um site institucional novo, copiar a estrutura deste. Padrão geral em [[Padrão de Sites 1060]].

## O que tem

- Nasceu do `site-estatico-template` ([[Templates de Site 1060]]); sem banco.
- 26 páginas: home, 18 páginas de serviço em conteúdo tipado (`src/content/areas/*.ts`) com um renderer por tipo de bloco, página da Simone (E-E-A-T), Sobre, blog, contato, privacidade. Uma URL por intenção de busca, com schema por página.
- **Ativo citável**: calculadora de dose de ruído (NR-15 e NHO-01) em `/ferramentas/dose-de-ruido/`.
- Dois formulários (contato e perícia com anexo até 4 MB) em `/api/contato` e `/api/pericia`.
- OG por rota em `app/og/[...caminho]` (a home em `/og/inicio/`; a Simone com retrato).

## Conceito

Eixo funcional com assinatura. A faixa de triângulos da marca (identidade de 2022, feita pela 1060) é exatamente uma **Treliça K** isostática; o site calcula a treliça de verdade (método da rigidez direta, Cholesky, código próprio < 10 KB) e a carga corre com o cursor, o dedo ou o teclado. Cada área de serviço tem a sua tipologia de treliça (Howe, Pratt, Warren, Fink, arco, tesoura). Chanfro de 45° do logotipo nos botões e retratos; raio zero; código normativo gigante (NR-01, CPC 465…) como fundo das páginas de serviço. Work Sans, carvão `#24282b`, marinho `#0e284b`, azul em três luminâncias travadas por superfície.

Decisão do Eduardo depois do lançamento: o hero do desktop trocou a treliça pelo retrato da Simone ("é mais clichê, mas converte"); a K virou simulador na página Sobre.

## Lições

- Retratos gerados por IA a partir de duas fotos reais do rosto, aprovados pela cliente; cena técnica só com foto real.
- `vector-effect: non-scaling-stroke` foi ignorado num celular real e virou bolhas sobre o texto; nós passaram a ser `<circle>` com raio explícito.
- Turnstile carregado sob demanda devolveu o LCP; `data-language="pt-br"` evita o widget em inglês.
- Telas 4K: composição limitada a 1920 px (120rem), centralizada.
- Pendências registradas no lançamento: revisão do texto pela Simone (`revisado: true` libera índice e sitemap), WhatsApp com 8 dígitos (não entra no JSON-LD até confirmar), teste humano dos formulários, Search Console/Bing/analytics.

## Relacionamentos

- [[Produto Sites]] — portfólio.
- [[Ferramentas 1060]] — AuraSR (`upscale:img`) e tinify nos retratos.

*Leitura do código e dos docs: 2026-11-10.*
