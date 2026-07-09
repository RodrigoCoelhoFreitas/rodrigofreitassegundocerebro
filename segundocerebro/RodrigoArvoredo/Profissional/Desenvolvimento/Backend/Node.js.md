---
tags: [desenvolvimento, backend, nodejs]
---

# Node.js (backend)

Ramificação de [[Backend]]. O stack **em uso ativo** nos 3 projetos atuais — [[1060crm]], [[NapShift Backend]] e [[NapShift Web]] são todos TypeScript/Node.js.

## Estado do ecossistema (2026)
- **TypeScript é o padrão de facto** para backend Node — segurança de tipo + flexibilidade do JS, o que bate com a escolha já feita nos 3 projetos.
- **Frameworks**: Express ainda lidera em adoção geral (40-55% dos devs Node), mas o ecossistema se diversificou — **Fastify** (o que [[NapShift Backend]] usa) é a escolha pra APIs de alta performance; **NestJS** domina em APIs enterprise mais estruturadas; **Hono** está em ascensão como alternativa edge-first, com benchmarks de 2-4x mais requisições/segundo que Express.
- **ESM como padrão**: frameworks/libs novas vêm ESM-only, CommonJS virou legado — coerente com `"type": "module"` já usado no [[NapShift Backend]].
- **Serverless/edge** continuam relevantes pro modelo de deploy, mas os 3 projetos atuais usam deploy tradicional (Vercel pro Next.js, Easypanel/container pro Fastify) em vez de function-per-request.
- Test runner nativo do Node amadureceu — [[NapShift Backend]] já usa `node --test` + tsx em vez de um framework de teste externo.

## Quando isso importa
É o conhecimento do dia a dia — qualquer decisão de arquitetura nos 3 projetos passa por aqui primeiro.

Assim como Java e .NET, a base dessa experiência também vem da **RCA Digital** (2018-2024, ver Carreira em [[Rodrigo Coelho Freitas]]) — mas aqui é o único dos 3 stacks que seguiu em uso ativo depois, agora nos projetos da 1060 Brand/NapShift.
