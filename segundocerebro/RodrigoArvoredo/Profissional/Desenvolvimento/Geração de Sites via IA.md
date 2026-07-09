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

## Como o fluxo funciona, agora confirmado (via snapshot 2026-07-09)
Recebido em 2026-07-09 um snapshot da memória do Claude do Eduardo (`C:\Users\Dell\Documents\referenciasclaudinho`) que responde as perguntas que ficaram em aberto abaixo. Resumo:
- **Onde o processo vive tecnicamente**: repositório próprio `1060` (`github.com/1060brand/1060`) — scripts, orquestrador e documentação de TODOS os sites de cliente, separado do [[1060crm]] (que é só o CRM de vendas) e do NapShift. Cada site de cliente nasce como um repo próprio em `github.com/1060brand/<slug>`.
- **Templates/boilerplates**: dois "Template repository" no GitHub, infra-only (sem frontend público) — `site-estatico-template` e `site-dinamico-template`. Ver detalhe completo em [[Infraestrutura de Sites 1060]].
- **O passo a passo do fluxo humano→Claude**: existe um orquestrador de linha de comando (`bootstrap-site`) que cria o site inteiro (banco, R2, repo, deploy, hint de OAuth) em 1 comando, e um runbook manual equivalente (`1060/docs/sop-novo-site.md`) como fallback — ver [[Ferramentas 1060]]. A partir daí o trabalho real é frontend + conteúdo, escrito com apoio de Claude Code em cima do design system próprio de cada cliente.
- **Relação com os templates HTML+Puppeteer do NapShift**: continua não confirmada — não apareceu no material recebido; são sistemas de renderização diferentes (Puppeteer gera imagem de post pra rede social; aqui é site completo em Next.js).

Pendente: acesso real do Rodrigo ao repositório `1060` e às credenciais/ferramentas (ainda não migrado — a confirmação acima é só documental).

## Relacionamentos
- [[Produto Sites]] (em [[Vendas]]) — o produto comercial que esta iniciativa entrega; o portfólio de lá é literalmente produzido por este processo.
- [[Infraestrutura de Sites 1060]] — decisões de stack/infra usadas por todo site gerado por este processo.
- [[Ferramentas 1060]] — orquestrador `bootstrap-site`, DSX, tinify, falgen: as ferramentas que o processo usa na prática.
- [[Eduardo Porto Teixeira]] — quem roda o processo hoje, dono do repositório `1060` e dos templates/boilerplates.
- [[1060crm]] — repositório separado (sem relação de código); a conexão é só de negócio, via [[Produto Sites]].
