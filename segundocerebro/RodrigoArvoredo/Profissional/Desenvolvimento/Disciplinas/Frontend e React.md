---
tags: [desenvolvimento, frontend, react]
---

# Frontend e React

Ramificação de [[Disciplinas]]. Usado em [[NapShift Web]] (Next.js 16.2 App Router, dois portais /adm e /cliente) e também é a base do [[1060crm]] (Next.js 16, App Router).

## Estado do ecossistema (2026)
- **Next.js 16**: Turbopack saiu do beta e é GA (build/dev estável em Rust). **Cache Components** + diretiva `use cache` substituem o modelo antigo de `fetch` cache — controle explícito do que e por quanto tempo cachear, com PPR (Partial Prerendering) como base. Breaking change grande: `params` e `searchParams` em páginas agora são **Promises** (precisa `await`/`use()`), não mais objetos síncronos.
- **App Router / RSC**: todo componente em `app/` é Server Component por padrão — `"use client"` é a exceção, não a regra. Server Actions maduras (mutação direto com `"use server"`, sem precisar de API route redundante pra CRUD simples).
- **Suspense** virou obrigatório, não opcional: qualquer componente que chama `useSearchParams()` precisa estar envolvido em `<Suspense>`, senão o build falha (Next força isso desde a v15 e continua em 16).
- **React 19**: Actions (funções async em transições) + hooks novos `useActionState`, `useOptimistic`, `useFormStatus`; API `use()` pra ler promise/context direto no render; `ref` virou prop normal (adeus `forwardRef` na maioria dos casos); tags de metadata (`<title>`, `<meta>`) podem ser renderizadas direto em qualquer componente, sem `next/head`.
- **React Compiler 1.0** estável desde out/2025, integrado no Next 16 com uma linha de config — memoização automática, elimina boa parte do `useMemo`/`useCallback` manual. Maior atrito em 2026: libs de terceiros que quebram as Rules of React, agora enforced em build time.
- **Tailwind v4**: motor Oxide (Rust), builds 2-5x mais rápidos. Config saiu do JS (`tailwind.config.js`) e virou **CSS-first**: `@import "tailwindcss"` + `@theme` direto no CSS. Detecção de content automática (sem configurar `content: []` na maioria dos casos). Container queries nativas (sem plugin). Breaking changes de default: cor de borda e de ring agora é `currentColor` (era `gray-200`/azul), ring width padrão caiu pra 1px.
- **shadcn/ui → Base UI**: em julho/2026 o shadcn oficializou Base UI como padrão pra novos projetos, no lugar de Radix. Motivo real: Radix perdeu ritmo depois que a Modulz (time original) foi comprada pela WorkOS em 2022 — gaps de componentes e dívida técnica acumularam. Os próprios engenheiros originais da Radix fundaram a Base UI (dentro da MUI) com o aprendizado de 3 anos. Radix não foi descontinuado — projetos existentes não precisam migrar, mas componentes novos podem só sair em Base UI.

## Quando isso importa
- O `AGENTS.md` do napshift-web trava de cara: "This is NOT the Next.js you know" — Next 16.2 tem breaking changes que não batem com o conhecimento de treino de LLM, manda checar `node_modules/next/dist/docs/` antes de codar qualquer coisa. Isso é literal: `params`/`searchParams` como Promise e o modelo de cache mudaram o suficiente pra invalidar padrões antigos.
- Suspense boundary obrigatório pra `useSearchParams()` já mordeu de verdade: `/registro` e `/cliente/perfil` quebravam o build até envolver em `<Suspense>` — não é teoria, é regra aprendida na marra.
- O `WorkspaceSwitcher` migrou do Dropdown do base-ui pra um popover custom via `createPortal`, por causa de um bug de stacking context — sinal de que mesmo a lib "nova" (Base UI) ainda tem arestas em produção, então nem sempre dá pra confiar cegamente na primitiva pronta.
- O design system do napshift-web é bem prescritivo (documentado em `docs/design-system-dashboard.md`): sidebar sempre escura, paleta roxo (`#7C3AED`) + amarelo (`#F59E0B`), cards flat sem sombra — construído em cima de shadcn/ui ("base-nova") + Tailwind, então qualquer componente novo tem que respeitar esses tokens antes de improvisar estilo.
- O 1060crm usa Tailwind 4 e Recharts pros dashboards.
- Ambos os projetos (napshift-web e 1060crm) rodam TypeScript 5 e React 19.2.4 — então tudo dessa nota (Actions, `use()`, Compiler) já é aplicável hoje, não é aspiracional.
