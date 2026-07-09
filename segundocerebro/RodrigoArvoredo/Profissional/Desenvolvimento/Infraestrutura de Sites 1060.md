---
tags: [desenvolvimento, infra, sites]
---

# Infraestrutura de Sites 1060

Ramificação de [[Geração de Sites via IA]]. Decisões de infraestrutura consolidadas pelo [[Eduardo Porto Teixeira]] para todo site de cliente da 1060 Brand — recebidas via snapshot da memória do Claude dele em 2026-07-09 (`contexto/infra/infraestrutura-sites.md`, repositório `1060`). Documento vivo do lado dele; aqui é o resumo pra orientar o Rodrigo quando herdar essa frente (ver [[Geração de Sites via IA]]). Ainda não confirmado com acesso direto ao repositório `1060` — checar antes de agir sobre um detalhe específico.

## Princípios
Controle próprio > SaaS de terceiros · free tier sempre que possível (custo recorrente fica com o CLIENTE, não com a 1060) · a menor stack que resolve · tudo versionado, segredos fora do repo.

## Stack base (todo site)
Next.js (App Router) + React + Tailwind v4 + TypeScript · Framer Motion (animação) · Lucide (ícones) · Vercel (deploy, preview automático por branch) · repo próprio por cliente em `github.com/1060brand/<slug>`, nascido de um boilerplate (ver seção seguinte) · conteúdo content-as-code (MDX/TS) por padrão, CMS só quando o cliente edita.

## Dois patamares de site
| Tipo | Quando usar | Boilerplate (template repo) |
|---|---|---|
| **Estático** (institucional/marketing) | Conteúdo estável, só a 1060 edita | `1060brand/site-estatico-template` — referência viva: saritabordini, ponto-gráfico |
| **Dinâmico** (CRUD + auth) | Cliente edita dados (eventos, produtos, unidades) por painel | `1060brand/site-dinamico-template` — referência viva: `1060brand/cafe-em-codigo` |

Ambos são *Template repository* no GitHub, **infra-only** — sem frontend público. A estética nasce do design system de cada cliente, nunca reaproveitada entre sites (ver "Regra de ouro" abaixo).

## Banco de dados — Postgres próprio (Supabase aposentado, jun/2026)
Motivo da virada: o free do Supabase **pausa projeto inativo (~7 dias)** — fatal pra painel de cliente acessado esporadicamente. Modelo atual: **uma instância Postgres 17 self-hosted compartilhada, um DATABASE por site** (role própria dona do próprio DB — `CREATE ROLE x; CREATE DATABASE x OWNER x`). Sem coluna `site`, sem RLS: isolamento é o próprio database; autorização vive na app via Auth.js + tabela `admins`.
- Roda (provisório) no **Easypanel KVM1** do NapShift, projeto `1060-sites` — exceção consciente à regra "Easypanel = exclusivo NapShift"; instância isolada do banco do NapShift. Migra pra uma VPS de sites própria quando ela existir.
- Porta não-padrão (54329) + TLS obrigatório (`sslmode=require`, cert self-signed) — a conexão Vercel→Postgres é **externa** (diferente do NapShift, que tem backend e banco na mesma rede interna do VPS).
- Auth: **Auth.js v5 (login Google) + Drizzle ORM**, sessão JWT + adapter Drizzle, allowlist `admins`. **OAuth Google: um projeto único `1060 Sites`, publicado** (escopos básicos → sem verificação nem aviso do Google, sem "test user" — a tabela `admins` é o gate real de acesso). Site novo = só 1 OAuth client novo dentro desse projeto.
- **Admin mestre `1060brand@gmail.com`** é admin de todo site automaticamente (injetado pelo script de migração de banco).

## Imagens — Cloudflare R2
Um bucket por projeto. Compressão **na inserção**, não na entrega — evita custo de transformação on-the-fly e o limite de otimização de imagem do Vercel free: o pipeline redimensiona + converte (AVIF/WebP) + comprime e já grava otimizado. Upload de CLIENTE via painel do produto = **sharp** (1600px/webp); assets que a própria 1060 processa manualmente (mockups, aplicações de marca) = **tinify** (ver [[Ferramentas 1060]]).

## Conteúdo/CMS — a escada
MDX puro (conteúdo estável, só a 1060 edita) → **Keystatic** (git-based, cliente edita conteúdo simples, sem banco) → **CRUD próprio** (cliente edita dados dinâmicos com query/relação — boilerplate dinâmico acima). Keystatic permite branding básico mas não é white-label profundo; se a exigência visual for além disso, vai direto pro CRUD próprio.

## Domínio, e-mail, SEO
- **Domínio/DNS: Cloudflare** sempre que possível (SSL automático, CDN, Turnstile e Email Routing num lugar só). `.com.br` não transfere registro pra Cloudflare Registrar — só o DNS; o registro fica no registro.br.
- **E-mail**: 1 alias simples → Cloudflare Email Routing (grátis, só recebe — não envia). Caixa real/múltiplos aliases/uso pesado → **CraneMail** (pago, IMAP, wizard de import direto de servidores tipo HostGator/cPanel).
- **Formulário de contato**: Resend (1 conta por cliente, isola reputação) + Turnstile anti-spam.
- **SEO padrão em todo site**: `sitemap.ts`, `robots.ts`, metadata + Open Graph, JSON-LD, SSR/SSG. **Analytics**: Cloudflare Web Analytics (grátis, privacy-first, sem cookie → sem banner de analytics). **LGPD**: banner de consentimento + política de privacidade, obrigatório em site BR.

## Hospedagem — risco a conhecer
O plano Vercel free (Hobby) é, nos termos, **não-comercial** — sites de cliente pagante tecnicamente exigem o Pro (~US$20/mês). Decisão (jun/2026): manter o Hobby por ora, ciente do risco — concentrar muitos sites comerciais numa única conta free aumenta a chance de uma suspensão derrubar todos de uma vez. Plano B **documentado, não migração planejada**: Cloudflare Pages (free permite uso comercial e é coerente com a stack Cloudflare já usada, mas a experiência com Next.js dinâmico nele foi ruim).

## Onde rodam back-ends (separação de infra)
**Easypanel (KVM1) é exclusivo do NapShift**, com uma exceção consciente: a instância Postgres compartilhada dos sites roda lá por ora (seção Banco de dados). Sites institucionais não precisam de máquina dedicada própria (serverless Vercel + Postgres compartilhado + R2 já resolve). Um sistema de cliente que exija servidor próprio de verdade leva uma máquina dedicada separada — a 1060 ainda não tem essa VPS de sites; contrata quando o primeiro caso do tipo justificar o custo.

## Orçamento de referência (jun/2026)
GitHub: ilimitado. Vercel: 100GB bandwidth/mês grátis por conta (Pro US$20/mês). Cloudflare R2: 10GB grátis + US$0,015/GB excedente. Cloudflare Email Routing: grátis.

## Regra de ouro — design system próprio por cliente
Todo site nasce de um **design system PRÓPRIO daquele cliente**, nunca de um frontend de template pronto — é o diferencial comercial ("design premium + entrega rápida"). O que se automatiza/repete é a **infra** (auth, banco, R2, painel, deploy — os boilerplates acima), nunca a aparência. Reaproveitar visual entre clientes mataria esse diferencial. Junto disso, **leveza**: um site não pode carregar dependência/feature que não usa (o antipadrão citado é WordPress + Elementor) — auditar o `package.json` sempre que um template for extraído ou atualizado.

## Como replicar um site novo
Runbook manual completo + o orquestrador `bootstrap-site` (1 comando só, ver [[Ferramentas 1060]]) estão descritos em `1060/docs/sop-novo-site.md`, dentro do repositório `1060` (`github.com/1060brand/1060`) — pendente de acesso direto do Rodrigo a esse repo.

## GitHub e Vercel — organizações separadas
| Org GitHub | Conta Vercel | Projetos |
|---|---|---|
| `@napshift` | conta NapShift Team | napshift, napshift-web |
| `@1060brand` | conta 1060 Brand | repo `1060` (docs/scripts/orquestrador) + 1 repo por site de cliente + [[1060crm]] |

Regra: nunca misturar — repos do NapShift sempre em `@napshift`; todo o resto em `@1060brand`. Motivo: contas misturadas já causaram desconexão de deploy e confusão de bandwidth no Vercel Hobby (limite é por conta).

## Relacionamentos
- [[Geração de Sites via IA]] — o processo de produção que usa esta infra.
- [[Ferramentas 1060]] — orquestrador `bootstrap-site`, DSX, tinify, falgen.
- [[Produto Sites]] (em [[Vendas]]) — o que é vendido comercialmente em cima desta infra.
- [[1060crm]] — roda sobre essa mesma infra de site dinâmico (Postgres compartilhado + R2), como repositório isolado.

*Fonte: snapshot da memória do Claude do Eduardo, recebido pelo Rodrigo em 2026-07-09 (`C:\Users\Dell\Documents\referenciasclaudinho`). Confirmar com acesso direto ao repo `1060` antes de agir sobre uma decisão específica — o documento envelhece.*
