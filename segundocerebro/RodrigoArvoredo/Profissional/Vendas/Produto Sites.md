---
tags: [vendas, produto, sites]
---

# Produto Sites

Ramificação de [[Vendas]]. Frente de **desenvolvimento e publicação de sites** da 1060 Brand — a única frente com pipeline de venda ativo hoje no [[1060crm]]. Baseado nos Termos de Prestação de Serviços v1.0 (julho/2026) e na Proposta Comercial correspondente.

## Dados da empresa
- **1060 BRAND** — CNPJ 26.067.767/0001-21.
- Sede: Rua Francisco Marques, nº 270, Centro, CEP 96200-150, Rio Grande/RS.
- Administrador: [[Eduardo Porto Teixeira]].
- Contato oficial: WhatsApp (53) 98164-1060 · 1060brand@gmail.com.
- Foro: Rio Grande/RS.

## Planos, preços e comissão do vendedor
Comissão do vendedor = **20% sobre o valor do plano**, liberada quando a **entrada (50%) cai** — sem estorno se o cliente sumir depois (o vendedor já embolsa ao confirmar a entrada, independente do resto do projeto).

| Plano | Papel na venda | Preço | Comissão (20%) | Prazo máximo | O que inclui de exclusivo |
|---|---|---|---|---|---|
| **Premium** | Ancoragem — mostrado primeiro | R$ 9.700 | R$ 1.940 | 20 dias úteis | Tudo do Profissional + até 50 páginas, ajustes de identidade visual, integrações com ferramentas de terceiros, multi-idiomas |
| **Profissional** | O alvo — o plano que se quer vender | R$ 5.900 | R$ 1.180 | 10 dias úteis | Até 25 páginas; seções dinâmicas que o cliente alimenta pelo painel (blog, eventos, portfólio, cardápio/catálogo — sem venda online); resto do site é fixo |
| **Essencial** | Budget curto | R$ 2.300 | R$ 460 | 5 dias úteis | Landing page/institucional de página única, conteúdo estático |

**Regra de apresentação**: sempre os 3, do mais caro pro mais barato (Premium → Profissional → Essencial) — técnica de ancoragem de preço. Na proposta comercial, o Profissional carrega o selo "MAIS ESCOLHIDO".

Prazos são **máximos** e contam a partir do último entre: confirmação do pagamento da entrada e recebimento completo dos materiais do cliente (logo, textos/tópicos, fotos, dados de contato, acesso ao domínio se já existir).

**Nota para [[Desenvolvimento]]**: esses valores são os mesmos hardcoded em `PLANO_VALORES` no código do [[1060crm]] (comentário no código cita vigência BR 2026-06-26; este documento formal é a versão 1.0, julho/2026 — checar se uma futura mudança de preço exige atualizar as duas pontas).

## O que todo plano inclui
Design exclusivo a partir da identidade visual do cliente, copywriting, SEO + AEO (otimização para Google e para respostas de IA), layout responsivo, alta performance, botão de WhatsApp + mapa do Google, domínio + e-mail profissional, hospedagem/infraestrutura, primeiro ano de manutenção incluso.

## O que NÃO está incluso (orçado à parte)
Criação de logotipo/identidade visual, loja virtual (e-commerce), pagamentos online/sistemas sob medida, produção fotográfica/audiovisual, gestão de redes sociais/tráfego pago, custos de ferramentas de terceiros, migração de conteúdo além dos materiais fornecidos, qualquer alteração pós-aprovação final.

## Manutenção anual
R$ 300/ano a partir do 2º ano (1º incluso no plano). Cobre: renovação de domínio (1, .com.br ou .com), hospedagem/infra, e-mail profissional (1 caixa até 10 GB compartilhada), suporte básico via WhatsApp/e-mail para **manter no ar o que já foi entregue**. NÃO cobre nenhuma alteração de conteúdo/design/páginas/funcionalidades — isso é sempre orçado à parte (exceto conteúdo dinâmico que o próprio cliente já alimenta pelo painel, sem custo).

Sem renovação: site despublicado e e-mail encerrado 30 dias após o vencimento. **Domínio continua do cliente**, que pode transferir e gerir por conta própria.

## Processo comercial (fluxo completo)
1. **Mensagem de contratação** (WhatsApp/e-mail): identificação do cliente, plano, valor, prazo máximo e versão dos termos.
2. **Aceite**: cliente responde "Li e concordo com os termos" (ou equivalente inequívoco) — **sempre antes do pagamento**. Mensagem + resposta = instrumento formal da contratação.
3. **Entrada (50%)**: Pix, boleto ou cartão (até 12x, com juros). Reserva a produção na fila e dispara a contagem do prazo. **Comissão do vendedor libera aqui.**
4. **Briefing**: logo, textos/tópicos, fotos, domínio.
5. **Produção**: prazo máximo do plano conta a partir daqui (entrada paga + materiais completos).
6. **Revisão**: 2 rodadas inclusas, cada uma uma lista única consolidada de ajustes, executada em até 3 dias úteis. Ajuste = refinamento do entregue (textos, imagens, cores, espaçamento); **não** inclui novas páginas/funcionalidades/mudança de direcionamento (orçado à parte). Sem retorno do cliente em 14 dias corridos = aprovação tácita.
7. **Aprovação final**: entra a segunda metade do pagamento.
8. **No ar**: publicação no domínio do cliente (registrado no nome dele, sempre — inclusive após o fim da relação).

## Cancelamento e falta de retorno
- **Cliente cancela antes de iniciar produção**: devolução da entrada, retendo a 1060 Brand 40% a título de custos comerciais/administrativos/reserva de agenda.
- **Cliente cancela depois de iniciar produção**: entrada não é reembolsável.
- **1060 Brand cancela** (impossibilidade não causada pelo cliente, exceto força maior): devolução integral do que não foi prestado.
- **Cliente some por 30 dias corridos** (após 2 tentativas de contato): projeto arquivado, sem devolução. Pode retomar em até 90 dias sem custo extra (sujeito à fila); depois disso vira contratação nova.

## Discurso de vendas (da proposta comercial)
**Pitch central**: "Seu site profissional, no ar em dias" — design exclusivo (nada de template pronto), textos que vendem, carregamento rápido, achável no Google **e nas respostas de IA** (AEO). "No ar em dias, não em meses."

**4 argumentos anti-objeção ("o risco é nosso, não seu")**:
1. Só paga a segunda metade depois de aprovar — se não ficar como combinado, não é entregue nem cobrado.
2. Nada vai ao ar sem aprovação do cliente.
3. Prazos máximos por escrito, nos termos.
4. Domínio é sempre do cliente.

**FAQ de vendas (objeções mais comuns)**:
- *"Não tenho textos nem fotos"* → a 1060 Brand escreve tudo a partir de conversa/tópicos; fotos podem ser banco de imagens.
- *"E se eu não gostar?"* → 2 rodadas de ajuste + só paga a 2ª metade após aprovar.
- *"Fica preso com vocês?"* → não, domínio no nome do cliente, conteúdo é do cliente.
- *"Quanto custa manter depois?"* → R$ 300/ano, 1º incluso.
- *"O prazo é real?"* → sim, máximo, por escrito, conta da entrada + materiais completos.
- *"Fazem loja virtual?"* → sim, projeto à parte com orçamento/prazo próprios.

**Validade da proposta comercial**: 15 dias a partir do recebimento.

## Portfólio citado na proposta
- **saritabordini.com** — educadora capilar Sarita Bordini: 15+ páginas, quiz interativo de conversão, integração com plataforma de cursos.
- **pontografico.com.br** — gráfica Ponto Gráfico: formulário de orçamento direto pro e-mail da equipe.
- **juliosecco.com** — rede de escolas de jiu-jitsu do mestre Julio Secco: mapa interativo com 16 unidades, geridas pela equipe via painel.
- **lealsantos.com** — Leal Santos, indústria de pescados fundada em 1889: acervo histórico da marca em 3D.

## Propriedade intelectual
Código-fonte, painel de gestão e infraestrutura são da 1060 Brand, licenciados pro cliente enquanto a manutenção estiver vigente. Conteúdo (textos finais, imagens fornecidas, dados inseridos) é do cliente. Cliente autoriza a 1060 Brand a exibir o projeto em portfólio/divulgação.

## Cláusulas gerais relevantes
- Sem garantia de resultado específico (posicionamento, tráfego, vendas) — SEO/AEO são boas práticas, não garantia.
- LGPD: tratamento de dados pessoais estritamente necessário à execução do serviço (art. 7º, V, Lei 13.709/2018).
- Sem vínculo trabalhista/societário entre as partes.

## Relacionamentos
- [[1060crm]] (em [[Desenvolvimento]]) — `PLANO_VALORES` no código espelha os preços deste documento. Criado especificamente para organizar a equipe de vendedores e viabilizar prospecção ativa (ver [[Vendas]]).
- [[Geração de Sites via IA]] (em [[Desenvolvimento]]) — como os sites vendidos aqui são efetivamente produzidos (assets criados por humanos via 1060, geração via Claude).
- [[Eduardo Porto Teixeira]] — administrador/representante legal da 1060 Brand.

*Fonte: Termos de Prestação de Serviços — Desenvolvimento de Sites v1.0 (julho/2026) e Proposta Comercial correspondente, recebidos em 2026-07-07.*
