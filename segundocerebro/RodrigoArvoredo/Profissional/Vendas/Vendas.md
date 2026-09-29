---
tags: [tronco, vendas]
---

# Vendas

Ramificação de [[Rodrigo Coelho Freitas]]. Lado de negócio/comercial da 1060 Brand — venda de sites, NapShift e outras frentes (branding, marketing, SDR).

O lado técnico dessa operação (CRM que sustenta o processo) fica em [[1060crm]], dentro de [[Desenvolvimento]]. Esta ramificação é sobre a **prática comercial em si**: playbook de vendas, planos/comissões, processo de prospecção, discurso de venda.

## Por que o 1060crm existe (confirmado pelo Rodrigo, 2026-07-08)
O [[1060crm]] e a venda de sites estão **extremamente interligados neste momento**: o CRM foi criado especificamente para viabilizar a organização de uma **equipe de vendedores** fazendo **prospecção ativa**. Público-alvo do produto Sites: empresas que **não têm site ou têm um site muito ruim**.

## Frentes de produto
- **[[Produto Sites]]** — a única frente com pipeline ativo hoje. Planos, preços, comissão do vendedor, termos jurídicos completos e discurso de vendas documentados ali (fonte: termos de serviço + proposta comercial oficiais, jul/2026). Ligado à nova iniciativa de [[Geração de Sites via IA]].
- **NapShift** — plano futuro: vender por **assinatura mensal**. Ainda sem comissão/processo comercial formalizado. *Estado em 2026-09-29:* tabela da landing fechada em 2026-08-04 — Starter R$ 397, Pro R$ 497, Escala R$ 897/mês; SDR só a partir do Pro. A cobrança ainda está em sandbox no Asaas, então os botões de contratar mandam pro WhatsApp comercial. Único cliente externo ativo: AEMJS. Custo de produção medido (~US$ 0,12–1,10 por peça, ver [[NapShift Backend]]) ficou ~2x o estimado e é a base pra revisar os planos; destino decidido pelo Eduardo é um teste grátis de 30 dias, que depende de o cliente conseguir se configurar sozinho no portal.
- **SDR** — plano futuro: vender **individualmente para empresas** (não só embutido em outro pacote). Ainda sem comissão/processo comercial formalizado.
- Branding, marketing — sem plano de comercialização formal definido ainda.

Fio condutor estratégico dado pelo Rodrigo: as futuras frentes (NapShift, SDR) vão abordar **as mesmas tecnologias já usadas no NapShift e no 1060crm** — esse padrão de stack é considerado confiável o bastante pra ser reaproveitado, o que reforça o valor de manter [[Disciplinas]] e [[Backend]] bem documentados (aplica pra produto futuro, não só pros 3 projetos atuais).

## O que já se sabe (via estudo do 1060crm)
- Processo: prospecção em massa por nicho/cidade (scraping) → importação no CRM → higienização → abordagem por vendedor → pipeline por produto (site é a frente com pipeline ativo hoje).
- O "playbook de vendas" embutido no CRM (modal de informações de negócio) reflete o mesmo conteúdo de [[Produto Sites]].

## Prospecção fora do CRM (planilhas)
Antes de virar lead no [[1060crm]], a prospecção por nicho/região é feita em planilhas Excel.

**Local canônico a partir de 2026-07-07**: `Documents\projetos\prospeccao\` — pasta dentro do workspace VS Code (irmã de [[1060crm]]/[[NapShift Backend|NapShift]]/[[NapShift Web]]/este vault), não é repo git. Toda planilha nova deve ser salva ali, de forma estruturada.

Pastas antigas (histórico, não usar para arquivos novos):
- `Documents\prospeccao\` (fora de `projetos` — atenção, nome de pasta igual, caminho diferente) — prospecção crua por nicho/cidade (ex: clínicas e advocacia em Rio Grande/RS), com `modelo.xlsx` de referência.
- `Documents\leads\` — versões consolidadas por nicho mais amplo.

Estrutura padrão de cada planilha: aba principal (nome, Instagram, "Possui site?", link do site, overview, referências visuais) + aba **Resumo** (totais) + aba **Fontes** (rastreabilidade — URL de cada dado) + aba **Notas** (critério, método, e o aviso de que "não localizado" ≠ "confirmado sem site").

Exemplo gerado em 2026-07-07: `Barbearias_RS_Amostra_sem_site.xlsx` — amostra manual (via busca web, sem Apify) de barbearias no RS sem site próprio localizado. Primeiro arquivo movido para o local canônico, como teste da nova convenção.

## Estado da equipe e meta de conversão (confirmado 2026-07-08)
Ainda em fase de **treinamento da equipe de vendedores** e de construção de **parcerias mais fortes**. Meta de curto prazo: garantir **3 leads convertidos por semana**, de forma consistente — mesmo que isso exija consumir 300-400 leads pra chegar lá (taxa de conversão aceita na faixa de ~0,75%-1% nesse estágio inicial).

## A desenvolver
- Documento comercial formal das outras frentes (NapShift assinatura, SDR individual, branding, marketing) — hoje só Sites tem termos/proposta recebidos, mesmo já tendo direção de venda definida pra NapShift e SDR.
- Métricas de conversão além da meta semanal (ciclo médio de venda, taxa por vendedor individual, etc.) — hoje só existe a meta agregada de 3/semana.

## Relacionamentos
- [[1060crm]] (em [[Desenvolvimento]]) — ferramenta que sustenta este processo.
- [[Geração de Sites via IA]] (em [[Desenvolvimento]]) — como o produto Sites efetivamente é construído.
