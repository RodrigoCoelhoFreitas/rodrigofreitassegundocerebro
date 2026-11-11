---
tags: [tronco, desenvolvimento, sites]
---

# Sites 1060

Ramificação de [[Desenvolvimento]]. Os sites de cliente da 1060 Brand **lidos pelo código**: em 2026-11-10 o Rodrigo clonou nesta máquina tudo a que tinha acesso no GitHub da `1060brand` (os dois templates, três sites no ar e o [[1060crm]]). As notas mais antigas ([[Infraestrutura de Sites 1060]], [[Ferramentas 1060]], [[Geração de Sites via IA]]) vieram do snapshot da memória do Eduardo em julho; estas aqui vêm do código.

## Por onde começar

- **[[Padrão de Sites 1060]]** — o roteiro: processo em etapas, contrato de direção, SEO+AEO, regras de design, cache, quality gate, lançamento, commits e o checklist de projeto novo.
- **[[Templates de Site 1060]]** — `site-estatico-template` e `site-dinamico-template`, o ponto de partida de todo site.

## Sites no ar (na máquina)

| Site | Tipo | Eixo | Por que estudar |
|---|---|---|---|
| [[Troina Engenharia]] | estático | funcional com assinatura | o processo inteiro documentado (briefing, conceito, presença, quality gate) |
| [[Kssino]] | dinâmico | cinemático na casca, funcional no utilitário | painel grande, PWA com push, anúncios, migração de WordPress, economia na Vercel |
| [[Mundo da Lua]] | estático, data-driven | cinemático | experiência imersiva e uma skill de publicação recorrente |

Outros sites da 1060 citados no portfólio de [[Produto Sites]] (Sarita Bordini, Ponto Gráfico, Julio Secco, Leal Santos, Café em Código, 1060brand.com) não estão nesta máquina.

## Estado da máquina (2026-11-10)

Pastas em `C:\Users\Gamer\Documents\projetos\`: `site-estatico-template`, `site-dinamico-template`, `kssino`, `mundodalua`, `troinaengenharia`, `1060crm`. Todos na `main`, sincronizados com o GitHub, **sem `node_modules` e sem `.env.local`** (as envs de produção ficam na Vercel e no `.env` do repo `1060`). A máquina não tem identidade git global: configurar `user.name`/`user.email` por repo antes do primeiro commit. O repo `1060` (método, scripts, orquestrador) segue sem acesso.
