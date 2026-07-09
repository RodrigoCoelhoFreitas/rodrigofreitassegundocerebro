---
tags: [desenvolvimento, backend, java]
---

# Java (backend)

Ramificação de [[Backend]]. Um dos 3 stacks de backend na trajetória profissional de [[Rodrigo Coelho Freitas]] (6 anos de mercado antes de se dedicar aos próprios negócios).

## Estado do ecossistema (2026)
- **Spring Boot continua o padrão de facto** da maioria das vagas/projetos Java — não por ser o mais rápido/leve, mas pela profundidade do ecossistema e maturidade de tooling (reduz custo total, do scaffold ao patch de segurança em produção).
- Tríade essencial: **Spring Boot + Spring Security + Spring Data JPA**. O resto (cache, observabilidade, arquitetura em camadas) se apoia nesses três.
- **Virtual threads (Project Loom)** viraram padrão: por volta de meados de 2026, praticamente todo serviço Spring Boot novo já nasce com `spring.threads.virtual.enabled=true`. Isso reduziu bastante a necessidade de programação reativa (WebFlux) só para lidar com I/O-bound — dá pra escrever código bloqueante "simples" e ainda ter concorrência no nível do reativo.
- **Quarkus e Micronaut** são as escolhas líderes quando o objetivo é microserviço com startup rápido — usam injeção de dependência em tempo de compilação, eliminando o scan de classpath que deixa o boot do Spring mais lento.
- Java moderno (21-25) trouxe evolução de linguagem relevante para backend: records, pattern matching, virtual threads — vale relembrar ao retomar um projeto Java depois de um tempo fora do ecossistema.

## Quando isso importa
Nenhum dos 3 projetos atuais ([[1060crm]], [[NapShift Backend]], [[NapShift Web]]) usa Java — é conhecimento de base útil se surgir integração com sistema legado, ou se avaliar stack pra um projeto novo fora do ecossistema Node atual.

Essa experiência vem da **RCA Digital** (2018-2024, ver Carreira em [[Rodrigo Coelho Freitas]]), em projetos como o **Portal Banco RCI Renault** e o **Projeto SIGA** (monitoramento de máquinas elétricas).
