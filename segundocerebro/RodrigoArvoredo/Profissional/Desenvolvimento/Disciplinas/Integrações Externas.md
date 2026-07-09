---
tags: [desenvolvimento, integrações, whatsapp, pagamentos, asaas]
---

# Integrações Externas

Ramificação de [[Disciplinas]]. Duas integrações críticas de negócio no NapShift: WhatsApp (aprovação de conteúdo, SDR) e Asaas (cobrança dos clientes).

## Estado do ecossistema (2026)

- **Evolution API** é a solução open-source de integração WhatsApp mais popular do Brasil: self-hosted, gratuita, roda como middleware sobre o **Baileys** (implementação Node.js do protocolo WhatsApp Web) e expõe uma API REST — envia texto, imagem, áudio, documento, gerencia múltiplas instâncias isoladas (multi-tenant) e tem integrações nativas com Typebot, Chatwoot, N8N, Dify, OpenAI. Não é API oficial: ela emula o WhatsApp Web para dar acesso programático, sem verificação empresarial nem aprovação de template — o que também é a origem do risco.
- **Risco de ban piorou em 2026**: desde o fim de 2025 a detecção da Meta ficou mais agressiva — instâncias que rodavam meses começaram a cair em 24-48h, com a mensagem "Your account is currently restricted. It looks like you may be using tools that do not follow our Terms". O ban é permanente, sem aviso prévio e sem recurso; volume baixo (~20-30 msgs/dia) reduz o risco mas não zera. Mitigação de mercado: warm-up de número, rate limiting agressivo, evitar broadcast/spam-like patterns.
- **Alternativa oficial**: Meta Cloud API, cobrada por conversa (janela de 24h, não por mensagem), ~R$0,20–0,50/conversa em 2026, exige verificação de negócio (Meta Business) e aprovação prévia de templates para mensagens fora da janela de 24h iniciada pelo usuário — trade-off claro: zero risco de ban vs. custo por conversa + rigidez de template vs. liberdade total (e risco) da Evolution API.
- **Asaas** é gateway de pagamento brasileiro focado em PMEs/SaaS/serviços recorrentes: Pix, boleto e cartão de crédito tokenizado, cobrança recorrente nativa (assinaturas com lembretes automáticos por e-mail/SMS), split de pagamento com escrow (retenção e liberação por evento) e link de pagamento sem taxa de emissão. Modelo de taxa é "paga só o que recebe" (sem mensalidade fixa): cartão ~1,99–2,99% + R$0,49/cobrança, boleto ~R$0,99–1,99, Pix com faixa gratuita mensal.
- **Comparação rápida**: Stripe é referência global (docs, SDKs, developer experience) mas historicamente mais fraco em boleto/Pix nativos e liquidação BR; Pagar.me (Grupo Stone) é o mais forte em marketplace/split para e-commerce de grande volume com antifraude robusto; Asaas se destaca no meio-termo — API simples, cobrança recorrente e Pix/boleto de primeira classe, forte tração em SaaS B2B e prestadores de serviço que precisam de assinatura mensal/trimestral/anual sem montar infra de billing própria.

## Quando isso importa

- No **[[NapShift Backend]]**, a Evolution API (self-hosted) carrega dois fluxos de negócio inteiros. Primeiro, aprovação de conteúdo via WhatsApp: `approval/sender.ts` envia a peça pro cliente aprovar, `approval/handler.ts` processa a resposta (aprovado/reprovado/ajuste). Segundo, o agente SDR conversacional "Bia", que atende leads recebidos por WhatsApp — com visão (`sdr/media.ts` baixa a imagem e monta content part para GPT-4o-mini vision) e transcrição de áudio (Groq Whisper, com fallback OpenAI). Tudo isso depende de mensagens *recebidas*, que passam por `src/webhook/router.ts` e `src/webhook/evolution-parser.ts` — o parser/router que normaliza o payload da Evolution API e faz dedup antes de rotear pro fluxo certo (aprovação vs. SDR).
- O risco de ban da Evolution API é risco de negócio direto aqui, não só técnico: se o número usado pra aprovação de conteúdo ou pro SDR "Bia" cair, o fluxo de aprovação de clientes e a captação de leads param até reconectar/trocar de número — não existe fallback automático pra Cloud API oficial hoje.
- Telefones no NapShift Backend são normalizados por `normalizarTelefone()` (`src/utils/phone.ts`) para o formato que o WhatsApp/Evolution API usa: sem o 9º dígito — 13 dígitos (`55` + DDD 2d + `9` + número 8d) viram 12 (`55` + DDD + número 8d). Existe também `phoneVariant()` pra gerar a forma alternativa (com/sem o 9) em fluxos de login, já que usuário pode digitar o telefone dos dois jeitos.
- **Asaas** é usado para assinatura/cobrança recorrente dos clientes do NapShift: `services/payment/asaas.ts` implementa o `PaymentProvider` (fetch nativo, timeout 15s, retry 1x em 5xx, autenticação via header `access_token`, não Bearer). Ciclo mensal/trimestral/anual, com status vindos direto do Asaas — `db/pagamentos.ts` trata `PAID_STATUSES = [RECEIVED, CONFIRMED, RECEIVED_IN_CASH]` como pago e `OPEN_STATUSES = [PENDING, OVERDUE]` como em aberto. Webhooks do Asaas chegam em `routes/webhook.ts` e há um agente de sincronização (`agents/pagamento-sync.ts`) pra manter o status local em dia.
- No **[[NapShift Web]]**, o wizard de novo workspace (`/cliente/workspaces/novo`) tokeniza o cartão direto com o Asaas via `POST /cliente/asaas/tokenize-card` (rota implementada em `routes/cliente.ts` do backend, atrás de `clienteAuthHook`) — o customer no Asaas é amarrado ao usuário CLIENTE autenticado (criado on-the-fly com cpf/email/telefone se ainda não existir) e o número do cartão nunca chega ao backend próprio do NapShift, só o token retornado pelo Asaas.
- No **[[1060crm]]** (CRM de vendas), não há integração de pagamento nenhuma — nem Asaas, nem Stripe, nem Pagar.me. As vendas de site fechadas pelo CRM são cobradas via Pix/boleto/cartão, mas o pagamento em si é processado fora do sistema (link de pagamento manual, conversa no WhatsApp do vendedor), sem tocar o schema nem as rotas do 1060crm — reforça que o 1060crm é ferramenta de pipeline/fechamento, não de billing.

Sources:
- [Evolution API Caindo em 2026: O Que Está Acontecendo](https://agenciacafeonline.com.br/blog/evolution-api-whatsapp-caindo-2026-o-que-esta-acontecendo/)
- [How to Use Evolution API Without Getting Banned on WhatsApp (2026 Guide)](https://wasenderapi.com/blog/how-to-use-evolution-api-without-getting-banned-on-whatsapp-2026-guide)
- [API Oficial WhatsApp vs Não Oficial: Guia Completo 2026](https://www.agenciarollin.com/blog/api-oficial-whatsapp-vs-nao-oficial-guia-completo-2026)
- [GitHub - evolution-foundation/evolution-api](https://github.com/EvolutionAPI/evolution-api)
- [Evolution API - Documentação do Evolution Foundation](https://docs.evolutionfoundation.com.br/evolution-api)
- [Preços e taxas Asaas](https://www.asaas.com/precos-e-taxas)
- [Taxas Asaas: pague apenas por cobrança recebida](https://blog.asaas.com/taxas-asaas/)
- [Reduza a inadimplência e fidelize clientes com cobranças recorrentes](https://materiais.asaas.com/cobranca-recorrente)
- [Qual API oferece split de pagamentos? Melhores opções](https://blog.asaas.com/qual-api-oferece-split-de-pagamentos/)
- [Como Funciona o Split de Pagamento em Marketplace](https://mindconsulting.com.br/2026/03/como-funciona-split-pagamento-marketplace/)
