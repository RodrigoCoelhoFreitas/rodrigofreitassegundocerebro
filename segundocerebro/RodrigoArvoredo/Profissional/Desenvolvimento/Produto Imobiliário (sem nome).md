---
tags: [projeto, código, planejamento]
---

# Produto Imobiliário (sem nome)

Ramificação de [[Rodrigo Coelho Freitas]]. **Ainda sem repositório** — em 2026-07-16 (sessão iniciada no repo [[1060crm]]) foi concluída só a fase de análise/planejamento, nenhum código/pasta foi criado. Plano denso completo salvo em `C:\Users\Dell\.claude\plans\claudinho-agora-vamos-come-ar-lazy-crown.md` (arquivo local do Claude Code, fora do vault) — ler esse arquivo antes de continuar qualquer rodada futura.

Rodrigo e [[Eduardo Porto Teixeira]] são sócios "em projetos específicos dentro da 1060", não em todo o guarda-chuva 1060 Brand — este é um desses projetos específicos, junto com [[NapShift Backend|NapShift]] e a venda de sites via [[1060crm]].

## Conceito de negócio
SaaS voltado ao mercado imobiliário: **landing pages + classificados para imobiliárias** (venda e aluguel). Cada imobiliária é um cliente/tenant. Corretores cadastram imóveis, administram a landing/conteúdo institucional da própria imobiliária, e configuram um agente de atendimento por IA.

Inspirado no [[TCC SISNI (FURG, 2018)]] do próprio Rodrigo — mas só no conceito de negócio, não na implementação técnica (ver nota do TCC pra detalhe do que foi descartado).

**Proposta de valor (3 pilares do pitch comercial)**:
1. Ferramenta completa de administração do trabalho do corretor (imóveis, classificados, landing, carteira de aluguel).
2. Atendente 24h automático e inteligente (agente SDR por imobiliária).
3. Motor de sugestão de negócios — não só "achar comprador mais rápido", mas ajudar na **divisão de comissão** entre corretores/imobiliárias diferentes e melhorar a **vazão** (giro) do estoque de imóveis.

## O diferencial: motor de sugestão de negócio (só vendas)
Corretores cadastram **Ofertas** (imóveis à venda) e **Procuras** (o que um cliente comprador busca), com **opt-in por registro** — cadastrar o imóvel/procura e ativá-lo pra rede são ações separadas. O sistema cruza a rede inteira (entre corretores e imobiliárias diferentes) e gera sugestões de negócio, com:
- **Ranking com pesos globais por atributo**, atualizados periodicamente a partir do feedback de negócios bem-sucedidos — reimplementação do mecanismo de reputação do TCC, em Node/TypeScript, provavelmente recalculado em batch/cron (padrão dos agentes do NapShift).
- **Privacidade preservada**: cada corretor só vê o próprio registro até a sugestão avançar (herdado do TCC).
- **Chat de match dedicado**: abre quando o match acontece, fecha quando resolvido (negócio fechado ou não fechado) — confirmado como requisito, era só "trabalho futuro" no TCC original.
- Explicitamente **exclusivo para vendas**, não aluguel.
- Divisão de comissão entre os dois lados de um negócio via sugestão — ainda em aberto se é só regra sugerida ou processamento real do repasse.

Desenho técnico proposto: duas camadas — (1) determinística (filtro por atributo essencial + score ponderado, rápida e auditável, sem LLM) gerando candidatos; (2) camada de IA por cima (interpretação de texto livre sobre o cliente, redação da notificação preservando privacidade, re-ranking) — nos moldes do pipeline de agentes do NapShift, não um RBC monolítico como o TCC original.

## Classificados: por imobiliária e busca global agregada
Cada oferta tem três flags independentes: aparecer na landing da própria imobiliária, aparecer na busca/classificados **geral da plataforma** (marketplace agregando todas as imobiliárias participantes, padrão Zap/Viva Real), e participar da rede de sugestão de negócio. Meta de produto explícita: filtros sofisticados (mapa, raio de busca, faixas), boa usabilidade tanto pro corretor quanto pro usuário final pesquisando.

## Administração de aluguéis
Fora do motor de matching (que é só venda). Tela com uma tabela por imóvel locado: endereço, nome do locador (proprietário), nome do locatário (inquilino), valor do aluguel, IPTU, água, luz, condomínio, valor total, e outras flags (status do boleto, vencimento, reajuste, vigência). Mais **contratos e vistorias gerados a partir de modelos** (templates).

**Boleto automático + split proprietário/imobiliária via Asaas** — pesquisado em 2026-07-16, tecnicamente viável:
- Assinaturas Asaas (`POST /v3/subscriptions`) geram boleto/Pix mensal automático — a própria doc do Asaas cita "cobrança mensal de aluguéis" como exemplo de uso.
- Split de pagamento divide a cobrança automaticamente entre imobiliária e proprietário (fixo ou % sobre valor líquido), herdado por toda cobrança futura da assinatura.
- Subcontas via API (`POST /v3/accounts`) dão ao proprietário sua própria carteira Asaas pro split, sem cadastro manual longo.
- **Bloqueador real de timing**: toda conta nova que cria subcontas entra num período de avaliação regulatória do Bacen de até 60 dias, limitado a 10 subcontas/R$2.000 em cobranças por subconta — inviabiliza carteira grande sem negociar antes com o comercial do Asaas.
- Decisão em aberto: MVP já inclui split/subconta (mais valor, mais fricção) ou começa só com boleto simples sem repasse automático.

## Atendimento via WhatsApp
Botão "Fale conosco" em cada landing de imobiliária, abrindo WhatsApp pro agente SDR configurado daquele tenant — reaproveitamento direto do subsistema `src/sdr/` do [[NapShift Backend|NapShift]] (`sdr_agentes` por workspace, Evolution API, sessão/histórico com resumo automático), só trocando o "conhecimento" do agente (imóveis da imobiliária em vez de planos de marketing).

## Domínio e cross-sell com Produto Sites
Landings de cada imobiliária vivem dentro do domínio do próprio sistema por padrão. Pra quem quiser domínio próprio, cross-sell natural com [[Produto Sites]] (hoje R$5.900 no plano Profissional): o site institucional passa a vir com conteúdo já integrado ao ambiente do corretor/imobiliária neste sistema, em vez de ser um site institucional genérico.

## Stack técnica (planejada, herdada 1:1 do NapShift)
Backend Fastify + Drizzle + Postgres self-hosted (VPS Hostinger via Easypanel) + JWT próprio; frontend Next.js App Router + Tailwind + shadcn/ui; dois repositórios separados (backend/frontend); deploy Easypanel (backend, manual) + Vercel (frontend, auto-deploy). Ver [[NapShift Backend]] e [[NapShift Web]] pra detalhe de cada peça reaproveitada — praticamente toda a arquitetura de referência vem de lá, exceto o motor de matching e a administração de aluguel/Asaas com split, que são território novo.

## Integração futura com o NapShift
Bancos separados (sem banco compartilhado), mas visão de cruzamento de dados entre os dois sistemas pra marketing cruzado: cliente deste produto (imobiliária) também pode ser atendido pelo NapShift, usando dados de um pra melhorar o atendimento/marketing do outro. Enquadrado pelo Rodrigo como parte de um ecossistema de SaaS maior da 1060 — não é requisito do MVP, mas vale desenhar a API já pensando nisso.

## Estado (2026-07-16)
Só planejamento — nenhum nome definido, nenhum repositório criado. Próxima rodada sugerida no plano: modelo de dados.

## Relacionamentos
- [[TCC SISNI (FURG, 2018)]] — origem conceitual, não técnica.
- [[NapShift Backend]] / [[NapShift Web]] — referência de arquitetura, quase tudo reaproveitado.
- [[Produto Sites]] — cross-sell pra domínio próprio.
- [[1060crm]] — onde a conversa de planejamento começou; sem relação de código.
