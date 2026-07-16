---
tags: [projeto, académico, histórico]
---

# TCC SISNI (FURG, 2018)

Ramificação de [[Rodrigo Coelho Freitas]]. Trabalho de conclusão do curso de Engenharia de Computação na FURG, 2018, orientação da Profa. Dra. Diana Francisca Adamatti: **"Sistema Inteligente para Sugestão de Negócios Imobiliários" (SISNI)**.

## Conceito (o que ainda importa hoje)
Corretor de imóveis cadastra dois tipos de registro numa rede compartilhada entre corretores de imobiliárias diferentes: **Oferta** (imóvel à venda, com atributos objetivos — cidade, bairro, tipo, quartos, banheiros, vagas de garagem, valor) e **Procura** (o que um cliente comprador deseja, mesmos atributos, cada um com um **peso de relevância em 5 níveis**: Irrelevante → Essencial). O sistema cruza toda a rede e gera um **ranking de sugestões de negócio** por corretor.

**Algoritmo**: Raciocínio Baseado em Casos (RBC) + busca ponderada. Atributos "Essenciais" (peso máximo) funcionam como filtro obrigatório — se não bate, a sugestão nem é gerada. Os demais somam `peso × reputação_global_do_atributo` na pontuação final. A **reputação global por atributo** é o mecanismo de aprendizado: toda vez que um corretor marca um negócio como bem-sucedido, os atributos essenciais daquela procura ganham +0,01 de reputação, os demais perdem 0,01, e tudo é renormalizado entre 0 e 1 — o sistema aprende, com o uso, quais atributos realmente pesam nos negócios que se concretizam.

**Privacidade já resolvida em 2018**: ao abrir uma sugestão, cada corretor só vê os dados do registro que é dele — os dados do outro corretor ficam ocultos até a negociação avançar.

**Trabalhos futuros do próprio TCC** (nunca implementados, mas documentados): migrar de desktop pra portal web, ferramentas administrativas pra imobiliária, chat entre os dois corretores enquanto o match for válido, app mobile de notificação.

## Por que essa nota existe
Em 2026-07-16, o Rodrigo usou este TCC como ponto de partida conceitual para um novo produto SaaS real — ver [[Produto Imobiliário (sem nome)]]. Ele foi explícito: **nenhuma ideia técnica do TCC** (Java desktop, RBC codificado à mão, MySQL via socket) é levada adiante — só o conceito de negócio (rede oferta/procura com privacidade preservada) e o modelo de dados como ponto de partida a adaptar. A implementação nova é 100% Node/TypeScript, no padrão do [[NapShift Backend|NapShift]].

## Relacionamentos
- [[Produto Imobiliário (sem nome)]] — o produto real que nasce dessa ideia, arquitetura completamente diferente.
