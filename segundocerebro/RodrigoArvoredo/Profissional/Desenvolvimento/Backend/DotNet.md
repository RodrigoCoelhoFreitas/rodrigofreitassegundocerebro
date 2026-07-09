---
tags: [desenvolvimento, backend, dotnet]
---

# .NET (backend)

Ramificação de [[Backend]]. Um dos 3 stacks de backend na trajetória profissional de [[Rodrigo Coelho Freitas]] (6 anos de mercado antes de se dedicar aos próprios negócios).

## Estado do ecossistema (2026)
- **ASP.NET Core** amadureceu de framework enterprise tradicional para plataforma cloud-native API-first, competitiva do startup ao sistema grande.
- **Minimal APIs** ganharam tração forte — muito projeto novo usa Minimal APIs ou Razor Pages em vez do MVC clássico. Para a maioria dos projetos com frontend separado (React/Angular), o padrão recomendado ainda é API ASP.NET Core limpa + frontend à parte (mesmo modelo que [[NapShift Web]] usa com o backend Fastify).
- **EF Core 10**: melhorias em compiled queries e batching valem revisão se for mexer em performance de banco; `dotnet-trace` é a ferramenta pra achar se o gargalo é mesmo a camada de dados.
- **Cache**: in-memory pra caso simples, Redis/SQL Server distribuído pra escala — decisão parecida com a que aparece em qualquer backend (comparável ao uso de storage/cache nos projetos NapShift).
- **Segurança**: middleware de Identity nativo cobre bem autenticação, RBAC e audit log sem precisar reinventar.
- Tendência mais "hype" (AI-assisted coding, Native AOT) é relevante pra performance/DX mas não muda a arquitetura de fundo.

## Quando isso importa
Nenhum dos 3 projetos atuais usa .NET — conhecimento de base útil se aparecer integração com sistema legado ou proposta de stack alternativa.

Essa experiência vem da **RCA Digital** (2018-2024, ver Carreira em [[Rodrigo Coelho Freitas]]), incluindo o **Site SESC São Paulo**.
