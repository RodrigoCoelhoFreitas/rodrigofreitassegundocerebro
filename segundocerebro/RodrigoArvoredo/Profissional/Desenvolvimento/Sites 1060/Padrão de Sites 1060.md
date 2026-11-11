---
tags: [desenvolvimento, sites, padrão, processo]
---

# Padrão de Sites 1060

Ramificação de [[Sites 1060]]. Como a 1060 constrói um site de cliente, tirado do código real em 2026-11-10: os dois templates ([[Templates de Site 1060]]) e os três sites no ar que estão nesta máquina ([[Kssino]], [[Mundo da Lua]], [[Troina Engenharia]]). É o roteiro para começar um projeto novo no mesmo padrão. Onde o código divergir desta nota, o código ganha (regra que os próprios repositórios seguem).

## As duas regras que mandam em tudo

1. **A infra se repete, a aparência nunca.** O template entrega só infra (auth, banco, R2, contato, SEO); o frontend público nasce do design system do próprio cliente. É o diferencial comercial de [[Produto Sites]] ("design exclusivo, sem cara de template"). Ver "Regra de ouro" em [[Infraestrutura de Sites 1060]].
2. **Nada inventado.** Dado que não veio do cliente fica marcado como PENDENTE e não vai para o site como fato. No código isso vira flag: telefone com `confirmado: false` não entra no JSON-LD; página com `revisado: false` fica `noindex` e fora do sitemap até o cliente validar o texto (Troina).

## O processo, em etapas

Os documentos do método vivem no repo `1060` (`docs/sites/`), que ainda não está nesta máquina. As etapas abaixo são as que aparecem nos repositórios dos sites (a numeração é a do método; 1, 2 e 5 a 8 não deixaram arquivo nos repos):

| Etapa | Arquivo no repo do site | O que é |
|---|---|---|
| 0 · Briefing | `docs/briefing.md` | Cruza o roteiro de entrevista enviado ao cliente com o que ele devolveu. Tabela **Dado · Valor · Origem**; pendências em negrito. Lista de fontes (arquivos recebidos, rodadas de WhatsApp). |
| 3 · Conceito | `docs/conceito.md` | Feito com a skill `/conceito` do Eduardo. Ver seção seguinte. |
| 4 · Presença | `docs/presenca.md` | Plano de SEO + AEO antes da copy e do código (método `1060/docs/sites/metodo-seo-aeo.md`). Ver seção "Presença". |
| Build | código + `DESIGN.md` | O `DESIGN.md` é escrito **depois** do build, a partir do código ("regra da casa"). |
| Quality gate | seção no `DESIGN.md` | Ver seção própria. |
| 9 · Medição | seção no `DESIGN.md` | Lighthouse e checagens no domínio final; a medida local não vale como aprovação. |

## Conceito (etapa 3)

Fases, como aparecem em `troinaengenharia/docs/conceito.md`:

- **Fase 0, negócio.** Uma frase: "Este site é uma ferramenta de X para Y, que precisam decidir Z; sustentado por…". Mais a lista **"o que faria um resultado bonito parecer errado"** (ex.: na Troina, cara de construtora, cara de escritório de advocacia, promessa de resultado).
- **Fase 1, eixo.** Um de três: *funcional* · *funcional com assinatura* · *cinemático*. Os sinais de funcional: telefone e formulário precisam ser achados, o visitante compara fornecedores, confiança pesa mais que surpresa, categoria regulada.
- **Fase 2, divergência.** Nomear o **sulco da categoria** (o clichê visual do setor) e o **oposto previsível**, e recusar os dois. Gerar ~7 mecanismos do mundo do cliente e um oitavo excessivo de propósito (dele se aproveita uma peça). O mundo pode vir da própria marca (na Troina, a treliça da identidade de 2022); o repo `1060` guarda `docs/sites/mundos-usados.md` para não repetir mundo entre clientes.
- **Fase 3, gestos.** 3 a 5 gestos concretos (escala extrema, matéria, sobreposição, pin com scrub…).
- **Fase 4, famílias da home.** Tabela seção · família · campo (cor de fundo) · densidade; famílias sem repetir vizinho. Proibidos: eyebrow (rótulo pequeno acima do título) e zigzag (imagem/texto alternando lado).
- **Fase 5, contrato de direção.** Vai para o layout raiz como comentário: `FUNÇÃO`, `EIXO`, `MUNDO` (com as recusas), `ASSINATURA`, `GESTOS`, `FAMÍLIAS`, `COR`, `TIPO` e regras específicas do cliente (no Kssino, `ANÚNCIO`). Formatos vistos: `<script type="text/x-contrato-de-direcao">` (Mundo da Lua), comentário JS no layout `(site)` (Kssino), comentário HTML no primeiro filho do `<body>` (Troina).

Eixos dos três sites: Troina = funcional com assinatura (um momento interativo por página, que não trava o scroll); Kssino = cinemático na casca, funcional no utilitário; Mundo da Lua = cinemático puro (sem transação, "o produto é a experiência").

## Presença: SEO + AEO (etapa 4 e template)

**No plano (`docs/presenca.md`):** situação de partida (site, domínio, perfil no Google, redes, menções, concorrência por citação em IA) → arquitetura com **uma URL por intenção** (tabela URL · intenção · schema) → buscas-alvo em duas linhas (como se digita no Google / como se pergunta a uma IA) → **ativo citável** (na Troina, a calculadora de dose de ruído) → baseline AEO antes do lançamento. Honestidade declarada: sem ferramenta de volume de busca, as buscas saem de intenção.

**No código (já vem no template):**
- `src/lib/site.ts` é a fonte única de NAP (`SITE` + `NEGOCIO`); endereço e telefone nunca são escritos à mão em página.
- `src/lib/schema.ts`: um `@graph` por página, um nó por entidade, tipo schema.org mais específico em `NEGOCIO.tipo` (nunca Organization + LocalBusiness separados); builders de FAQ, Service, Article, Breadcrumb, Evento. `BreadcrumbList` em toda página interna.
- `<Faq>` gera o visível e o FAQPage da mesma fonte; `<Datas>` mostra publicado/atualizado (frescor é sinal de AEO). Sitemap com `lastModified` real, nunca a data do build.
- `robots.ts` libera os robôs de IA (OAI-SearchBot, ChatGPT-User, Claude-SearchBot, Claude-User, PerplexityBot; treino liberado por padrão), comentado bot a bot.
- **Guard de domínio:** sem `NEXT_PUBLIC_SITE_URL` o build não emite canonical, og:url nem sitemap. Essa env só existe em produção, então previews ficam `noindex` sozinhos.
- Verificação Google **e Bing** (Bing indexado é pré-requisito do ChatGPT Search) e IndexNow pingado pelo painel a cada publicação.
- Fontes por `next/font` (self-hosted, LGPD) e Cloudflare Web Analytics (sem cookie, sem banner).

**Convenções que os sites acrescentaram:**
- `trailingSlash: true` é o padrão da casa (Troina, Kssino). Redirect com destino de barra explícita, para ser um salto só.
- Aliases `*.vercel.app` redirecionam por host para o domínio canônico (Mundo da Lua, `next.config.ts`); host não canônico recebe `X-Robots-Tag: noindex` (Kssino).
- Canonical da home na raiz (o Kssino declarava `/index/`, corrigido em 2026-11-04).
- **Imagem de compartilhamento (OG) obrigatória antes do lançamento** — em 2026-11-04 o Eduardo passou em todos os sites corrigindo isso. Regras aprendidas: JPEG leve (o WhatsApp descarta preview pesado; PNG de 400 KB falhou); arte nova = nome de arquivo novo (`og-v2.jpg`), porque WhatsApp e LinkedIn cacheiam pela URL; composição central (o WhatsApp recorta); página com `openGraph` próprio substitui o bloco inteiro e precisa repetir a imagem; com `trailingSlash` não usar o arquivo `opengraph-image` (responde 308), e sim uma rota `/og/[...caminho]` (Troina). O repo `1060` tem `npm run og:marca` para gerar.

## Estrutura do repositório

- `github.com/1060brand/<slug>`, privado, branch única `main`; **push na `main` = deploy de produção na Vercel** (time da 1060). Não há `homolog` nos sites (diferente do NapShift).
- `README.md` com tabela "Onde está cada coisa"; `DESIGN.md`; `docs/` com briefing, conceito, presença e runbooks de operação (Kssino: `cutover.md`, `economia-vercel.md`).
- `src/app/(site)/` = site público (o JSON-LD do negócio sai uma vez no layout desse grupo, nunca no painel); `src/app/painel/` = admin; `src/app/api/`.
- Conteúdo como código: `src/content/` tipado (Troina: 18 páginas de serviço em `content/areas/*.ts`) ou `src/data/` (Mundo da Lua). Um renderer por tipo de bloco em vez de página escrita à mão.
- Componentes por domínio (`site/`, `home/`, `painel/`, `ui/`, `marca/`, `movimento/`, `formularios/`…), nomes de arquivo em português, kebab-case.
- Marca: o logotipo sai **do vetor original**, separado por script, nunca redesenhado (`src/assets/marca/*.svg` + `scripts/gerar-marca.mjs` no `predev`/`prebuild` do Kssino; arquivo com cor inesperada falha o build).
- Código, comentários e identificadores em português (comentário geralmente sem acento); texto de interface com acento correto.

## Design: regras de craft visíveis no código

- O DS do cliente (manual de marca, Pantone) é lei. Tokens com **nome semântico estável** e valor do cliente (`globals.css` com `@theme`).
- Contraste **medido e anotado por token** no `DESIGN.md` (razão WCAG de cada par). Cor de marca que reprova como texto pequeno fica só em display grande, ou ganha uma variante "-texto" mais escura (Troina: `azul` 4,3:1 → `azul-texto` 5,4:1).
- Uma forma-assinatura tirada do logotipo e raio zero no resto: paralelogramo de 23° das letras do Kssino; chanfro de 45° do R e do N da Troina. O recorte vai num `::before` para o anel de foco não ser cortado.
- Movimento sempre com rede: sem JS ou com `prefers-reduced-motion`, o conteúdo aparece. Todo loop `requestAnimationFrame` só roda visível (IntersectionObserver, aba ativa); animação CSS só em `transform`/`opacity`.
- Orçamento de peso: código próprio no lugar de biblioteca (motor de treliça < 10 KB, corda Verlet, Lunar Lander em canvas, som WebAudio procedural). Script de terceiro carregado sob demanda (Turnstile só quando o formulário chega a 600 px da tela: o LCP da home caiu de 2,6 s para 2,3 s).
- Detector `impeccable detect`: achado real é corrigido; achado falso é refutado com medida; ignore justificado é registrado no `DESIGN.md`.
- Breakpoint do menu **medido pelo conteúdo**, não pelo padrão do Tailwind (Troina: variante `menu:` em 1200 px).
- Assinatura da 1060 no rodapé (crédito no footer do template; holograma no Mundo da Lua).
- Decisões e reversões do Eduardo ficam datadas no `DESIGN.md` ("revisão 2026-08-27, decisão do Eduardo: …"), inclusive o que foi testado e rejeitado.

## Imagens

- Tudo que a 1060 processa à mão passa pelo tinify (`npm run min:img` no repo `1060`); upload do cliente pelo painel usa sharp → webp. Site estático com poucas imagens pode servir de `public/` em vez do R2 (decisão do Eduardo na Troina).
- Fotos geradas por IA a partir de foto real: falgen (nano-banana edit) → AuraSR 4x → redução para ~0,4x (apaga a trama na pele) → tinify; recorte de fundo com BiRefNet. Sempre conferir rosto, insígnias e bandeiras (o primeiro traje do Mundo da Lua veio com bandeira americana). Precisa de aprovação do cliente; cena técnica só com foto real.
- Imagem lazy com largura e altura explícitas.

## Dados e cache (site dinâmico)

Lições do Kssino e do Café em Código, já incorporadas em parte ao template:
- Leitura pública em `unstable_cache` **por tag**, invalidada pelo painel (`updateTag`); rede de segurança longa (7 dias). Tag por item (`boletim:<slug>`), não só por coleção: com tag única, cada boletim publicado refazia 1.199 páginas.
- A função cacheada devolve DTO com datas em string ISO, nunca `Date` nem linha do Drizzle (volta como string no segundo acesso).
- Página que depende de "hoje" chama `await connection()`; o que muda sozinho com o tempo (vigência de anúncio) é filtrado no navegador. Layout nunca tem cache curto nem chave com data (puxa o site inteiro).
- `proxy.ts` (middleware do Next 16) com matcher restrito ao que precisa; Auth.js só em `/painel` (senão grava cookie em resposta pública).
- Funções na região `gru1` (`vercel.json`), perto do banco. Fuso de Brasília como UTC-3 fixo.
- Sem `next build` local quando o `.env.local` aponta para o banco de produção: localmente só `tsc` e `eslint`; o build é o da Vercel.

## Formulários

Backend `POST /api/contact` do template (Resend + Turnstile). Conta Resend por cliente, domínio verificado, em produção só a chave `sending_access` restrita ao domínio. Turnstile com `data-language="pt-br"`. Sem Resend configurado, o formulário cai na saída por WhatsApp.

## Quality gate

Antes de dar por pronto (lista da Troina): build de produção limpo · 0 erro de console · 0 scroll horizontal em 360, 390, 768, 1024, 1440 e 1920 (e 2560/3840 se houver composição larga) · 1 `h1` por página · JSON-LD válido · links internos íntegros · `og:title` próprio e `og:image` 200 em toda página · interações pelo teclado (Esc devolve o foco, foco preso no menu do celular) · Lighthouse **no domínio final** (cache quente).

## Lançamento

- Domínio **em nome do cliente**; DNS na Cloudflare da 1060, sem proxy; escolher apex ou www como canônico e redirecionar o outro com 308.
- `NEXT_PUBLIC_SITE_URL` só em produção. Depois: Search Console e Bing por DNS, sitemap, IndexNow, Cloudflare Web Analytics.
- Migração de site antigo (WordPress/HostGator): runbook em `docs/cutover.md`, scripts `migrar:*`, redirects do legado, plano de rollback. Ver [[Kssino]].
- Scripts de operação no repo `1060`: `scripts/sites/dns/vercel-cutover.mjs`, `restaurar-zona.mjs`, `scripts/sites/vercel-env.mjs`, `scripts/sites/r2/*`.

## Git e commits

- Conventional Commits **em inglês**, escopo curto: `feat(painel)`, `fix(og)`, `perf(cache)`, `docs(design)`, `chore(paths)`. Corpo explica o porquê. Trailer `Co-Authored-By` do Claude. (Os primeiros commits do Kssino, de 2026-09, eram em português.)
- `DESIGN.md` e `docs/` atualizados no mesmo ritmo do código, em commits `docs(...)`.

## Onde as coisas moram na máquina do Eduardo

Os repositórios citam caminhos relativos: `<raiz>/Sites/<slug>` (repos dos sites), `<raiz>/1060` (scripts e método), `<raiz>/1060 Acervo/<cliente>/` (mídia original, referências, backup do WordPress) e `<raiz>/1060 Clientes/<cliente>/site/` (entregáveis, backups de DNS) — reorganização de 2026-10-21. O estado vivo de cada cliente fica no vault do Eduardo (`Segundo Cérebro/1060 Brand/Clientes/<Cliente>/`), que não é este vault.

## O que falta para seguir o padrão completo

O repo `1060` (método SEO+AEO, `mundos-usados.md`, regras de craft, `metodo-vendas-ultra.md`, `sop-novo-site.md`, orquestrador `bootstrap-site`, `og:marca`, falgen, tinify), as skills `/conceito`, `/wrap` e o `impeccable`, e as contas (Vercel, Cloudflare, R2, Resend, OAuth Google `1060 Sites`). Sem eles, dá para seguir o padrão à mão a partir dos templates e desta nota.

## Checklist de projeto novo

1. Decidir o tipo: estático ou dinâmico ([[Templates de Site 1060]]). Criar `1060brand/<slug>` a partir do template ("Use this template" no GitHub; nesta máquina não há `gh`).
2. `docs/briefing.md` (etapa 0) com tudo que veio do cliente e as pendências.
3. `docs/conceito.md` (etapa 3) até o contrato de direção.
4. `docs/presenca.md` (etapa 4): URLs por intenção, buscas-alvo, ativo citável.
5. Preencher `src/lib/site.ts` (`SITE`, `NEGOCIO` com subtipo schema.org), tokens do DS em `globals.css`, fonte da marca, logo do vetor original.
6. Construir o frontend sobre o DS; contrato de direção no layout raiz.
7. OG por página, sitemap com datas reais, FAQ, breadcrumbs.
8. Escrever o `DESIGN.md` a partir do código; rodar o quality gate.
9. Domínio, DNS, envs de produção, verificações, analytics; Lighthouse no domínio final.
10. Commits em inglês no padrão; README com "Onde está cada coisa".

*Fonte: leitura dos repositórios `site-estatico-template`, `site-dinamico-template`, `kssino`, `mundodalua`, `troinaengenharia` e `1060crm` em 2026-11-10.*
