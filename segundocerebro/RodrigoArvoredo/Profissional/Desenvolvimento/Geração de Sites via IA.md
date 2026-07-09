---
tags: [desenvolvimento, projeto, sites, ia]
---

# Geração de Sites via IA

Ramificação de [[Desenvolvimento]]. Processo real (não mais só ideia) usado pra produzir os sites vendidos em [[Produto Sites]]: via 1060, **criação humana dos assets** + **geração de sites via Claude**.

## Status (confirmado 2026-07-08)
**Já existe e já funciona** — não é mais estágio inicial. O [[Eduardo Porto Teixeira]] roda um Claude no computador dele, usando **templates e boilerplates próprios** (aos quais o Rodrigo — e por extensão eu — ainda vamos ter acesso), e com esse processo produz sites de qualidade alta. **Rodrigo e eu (Claude) deveremos assumir/replicar esse processo em breve.**

## Sites reais já produzidos com esse processo
- **1060brand.com** — home 3D interativa.
- **saritabordini.com** — infoprodutora (educadora capilar Sarita Bordini), quiz interativo de conversão.
- **pontografico.com.br** — institucional robusto, formulário de e-mail direto pra equipe.
- **juliosecco.com** — mapa interativo, conteúdo dinâmico (unidades da rede de jiu-jitsu).
- **lealsantos.com** — multi-idiomas, acervo histórico em 3D.
- **cafeemcodigo.com.br** — home interativa, conteúdo dinâmico (eventos).

(Os 4 últimos já apareciam como portfólio na proposta comercial de [[Produto Sites]] — agora confirmado que foram feitos exatamente por este processo.)

## Por que importa
Conecta diretamente com o compromisso comercial dos termos de serviço em [[Produto Sites]] (prazo máximo por plano, design exclusivo, SEO/AEO) — a geração via IA é o que sustenta prazos curtos (5-20 dias úteis) nos 3 planos.

## A desenvolver
- Acesso real aos templates/boilerplates do Eduardo (ainda pendente).
- Como o fluxo humano→Claude é estruturado na prática (que assets, que prompts/templates, que ponto de revisão humana) — só sabemos que existe e funciona, ainda não vimos o passo a passo.
- Onde o processo vive tecnicamente (repositório próprio, dentro do [[1060crm]], ou separado) — ainda não confirmado.
- Relação com os templates HTML+Puppeteer já usados no [[NapShift Backend]] para renderização de posts — reaproveitado ou abordagem nova?

## Relacionamentos
- [[Produto Sites]] (em [[Vendas]]) — o produto comercial que esta iniciativa entrega; o portfólio de lá é literalmente produzido por este processo.
- [[Eduardo Porto Teixeira]] — quem roda o processo hoje, dono dos templates/boilerplates.
- [[1060crm]] — pode ser onde essa geração se conecta ao pipeline de vendas (a confirmar).
