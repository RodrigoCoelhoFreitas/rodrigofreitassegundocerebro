---
tags: [desenvolvimento, sites, template, código]
---

# Templates de Site 1060

Ramificação de [[Sites 1060]]. Os dois *Template repository* da 1060 no GitHub, clonados nesta máquina em 2026-11-10 (`projetos\site-estatico-template` e `projetos\site-dinamico-template`). Confirmam pelo código o que [[Infraestrutura de Sites 1060]] descrevia a partir do snapshot de julho. Como usá-los num projeto: [[Padrão de Sites 1060]].

Os dois são **infra-only**: a home e o 404 são placeholders, e os tokens de `globals.css` têm nomes semânticos estáveis com valores de exemplo (refatoração de 2026-06-27, "aesthetic-agnostic"). Toda feature opcional é ligada por variável de ambiente e degrada sem ela (contato sem Resend responde 501; Turnstile sem secret é pulado em dev; analytics sem token some).

## site-estatico-template

Extraído do dinâmico em 2026-06-22; 4 commits. Next 16.2 · React 19 · Tailwind v4 · TypeScript · resend · zod. Sem banco, sem auth.

- `POST /api/contact` (Resend + Turnstile, validação zod).
- Camada de presença completa (commit `cc2fc86`, 2026-08-03): `lib/site.ts`, `lib/schema.ts`, `robots.ts`, `sitemap.ts`, `<JsonLd>`, `<Faq>`, `<Datas>`, metadata com guard de domínio.
- `lib/format.ts`: datas em pt-BR no fuso de São Paulo ("qua, 25 jun · 19h").
- `next.config.ts` libera o host do R2 se `R2_PUBLIC_URL` existir (bootstrap `--assets`).
- Último commit (2026-11-04): comentário lembrando que falta a imagem OG (`npm run og:marca` no repo `1060`).

## site-dinamico-template

Extraído do Café em Código em 2026-06-22; 11 commits. Soma ao estático: Auth.js 5 (Google) · Drizzle + postgres-js · R2 (`@aws-sdk/client-s3`) · sharp · react-hook-form · lucide-react.

- **Modelo DB-por-site**: um database por site na instância Postgres compartilhada; sem coluna `site`, sem RLS. `npm run db:provision -- <slug>` cria role e database (precisa de `.env.provision` com `ADMIN_DATABASE_URL`); `db:migrate` cria as tabelas e o admin mestre `1060brand@gmail.com`.
- **Painel** em `/painel`, protegido por `src/proxy.ts` (middleware do Next 16, matcher só em `/painel`); a allowlist `admins` é aplicada no `signIn`. Sem tela de usuários por decisão (site institucional tem 2 ou 3 e-mails): `npm run admin:list | admin:add -- email | admin:rm -- email [--sim]`; o admin mestre não pode ser removido.
- **Recurso de exemplo `eventos`**, que é o molde de CRUD. Para adaptar, na ordem: `db/schema.ts` → `lib/eventos.ts` + `eventos-admin.ts` + `eventos-schema.ts` → `app/painel/*` → `components/painel/evento-form.tsx` → `npm run db:generate`.
- Server actions devolvem `{ ok, error?, fieldErrors? }`; violação de unique (Postgres `23505`) vira mensagem amigável; upload de capa até 8 MB, só imagem, sharp → webp → R2.
- Cada save chama `revalidarPublico`: `updateTag` + `revalidatePath` das rotas + sitemap + ping no IndexNow (best-effort, nunca falha o save).
- Leitura pública em `unstable_cache` com tag e rede de 1 h; sem `DATABASE_URL` devolve lista vazia em vez de quebrar. Página que depende de "hoje" precisa de `await connection()` (bug real do Café em Código em 2026-10: evento passado seguia como próximo).
- Correções que valem para qualquer projeto com sharp na Vercel: copiar a saída do sharp para um `ArrayBuffer` não compartilhado antes de assinar no S3 (`c58cd48`) e rastrear o libvips nas funções que importam sharp (`e8f2aa3`; o mesmo conserto entrou no [[1060crm]] e no [[Kssino]]).
- Login com a marca do cliente e rodapé padrão com crédito da 1060 (`cf6ee2e`).

## Variáveis de ambiente

`NEXT_PUBLIC_SITE_URL` / `_NAME` / `_DESCRIPTION` · `NEXT_PUBLIC_GOOGLE_SITE_VERIFICATION` / `_BING_` · `INDEXNOW_KEY` (+ `public/<chave>.txt`) · `DATABASE_URL` (`sslmode=require`) · `AUTH_SECRET`, `AUTH_GOOGLE_ID/SECRET` (client OAuth compartilhado da 1060), `AUTH_URL` só em dev · `R2_*` · `RESEND_API_KEY`, `CONTACT_TO_EMAIL`, `CONTACT_FROM_EMAIL`, `TURNSTILE_SECRET_KEY`, `NEXT_PUBLIC_TURNSTILE_SITE_KEY` · `NEXT_PUBLIC_CF_ANALYTICS_TOKEN`. O `.gitignore` ignora `.env*` e mantém só o `.env.example`.

## Relacionamentos

- [[Infraestrutura de Sites 1060]] — as decisões de infra que estes templates implementam.
- [[Ferramentas 1060]] — o `bootstrap-site` cria o repo a partir destes templates.
- Sites nascidos deles nesta máquina: [[Kssino]] (dinâmico; o README ainda é o do template) e [[Troina Engenharia]] (estático). [[Mundo da Lua]] não nasceu deles.

*Leitura do código: 2026-11-10.*
