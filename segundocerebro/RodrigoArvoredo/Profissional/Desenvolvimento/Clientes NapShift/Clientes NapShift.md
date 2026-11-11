---
tags: [tronco, desenvolvimento, napshift, clientes]
---

# Clientes NapShift

Ramificação de [[Desenvolvimento]]. As marcas que o [[NapShift Backend]] opera, estudadas em 2026-11-11 a partir do repositório **`napshift/napshift-clientes`** (privado, `main` direto, criado pelo [[Eduardo Porto Teixeira]] em 2026-11-10). O objetivo do estudo: estar pronto para gerar arte, imagem e texto para qualquer cliente sem sair da identidade dele.

Cliente do NapShift e cliente da 1060 são relações independentes, mesmo quando a empresa é a mesma (a [[EMMV]] é as duas coisas). O onboarding do NapShift mora neste repositório e nunca vai para o `1060 Clientes`.

## Os workspaces

| Nota | Workspace | Ramo | Onboarding | Estado em 2026-11-11 |
|---|---|---|---|---|
| [[AEMJS no NapShift]] | Associação Equipe Mestre Julio Secco | jiu-jitsu, 16 academias no sul do RS | 2026-06-02 (piloto do `/onboardnap`) | primeiro cliente real; assinatura no cartão não saiu (cartão bloqueado no Asaas) |
| [[Casa ProVida no NapShift]] | Casa ProVida | clínica de longevidade, Rio Grande | 2026-08-11 | **encerrado pelo painel em 2026-10-01** |
| [[Carlson Gracie no NapShift]] | Carlson Gracie Hendersonville | jiu-jitsu, Tennessee (EUA) | 2026-10-01 | primeiro cliente fora do Brasil; conteúdo em inglês |
| [[D'Kids no NapShift]] | D'Kids | moda infantil, Rio Grande | 2026-10-16 | templates recusados para o dia a dia; teste de IA com as peças em aberto |
| [[EMMV no NapShift]] | Escola de Música Marcelo Vaz | escola de música, Rio Grande | 2026-10-16 | publicado; campanha do 3º Mentes MusiCaos (13 a 15/11) |
| [[Ten Sushi no NapShift]] | Ten Sushi | restaurante japonês, Rio Grande | 2026-10-19 | marca refeita do zero; 272 fotos em 47 álbuns |
| [[Marcas da Casa no NapShift]] | 1060 Brand e NapShift | as marcas próprias | 2026-04 e 2026-08 | só o estado exportado; onboarding a refazer |

## Onde está a verdade de cada marca

- **`<slug>/05-config/<cliente>-napshift-config.md`**: os 6 campos do workspace (`identidade_marca`, `identidade_visual`, `estilo_escrita`, `contexto`, `estrategia`, `publico`) mais a tabela de eventos. É o texto que entra **literal** no prompt dos agentes.
- **`<slug>/INVENTARIO.md`**: o que chegou, onde foi parar, pendências e decisões sobre fotos.
- **`<slug>/05-config/<cliente>-referencias.md`**: o manifesto dos assets (logos, fontes, fotos, templates) com a descrição que o sistema usa para escolher cada um.
- **`<slug>/05-config/_publicacao-log.jsonl`**: tudo o que foi publicado no portal, inclusive mudanças feitas depois do onboarding. Depois da publicação, **o portal é a cópia de referência**: o `.md` pode estar atrás dele (a Carlson teve `contexto` trocado em 2026-10-27; a EMMV, uma linha do `identidade_visual` em 2026-10-20).
- **Fotos e mídia ficam fora do git** (`03-fotos/`, `04-midia/`, `06-previews/`). Nesta máquina não há acervo de fotos: quem continua o trabalho de outro pede essas pastas por fora.

## Como a arte é feita no sistema

1. O **Estrategista** monta a pauta pela `estrategia` e pelos eventos; o **Copywriter** escreve pelo `estilo_escrita`.
2. O **Diretor de Arte** escolhe o template e separa as referências (fotos, ícones, fundos) pelas descrições cadastradas.
3. O **Produtor** (Claude Opus) trabalha **um slide por sessão**: parte do template, que é ponto de partida e não molde, edita o HTML, gera imagem quando falta, renderiza e olha. O `identidade_visual` inteiro entra no system prompt dele: é a especificação de design.
4. Imagem gerada: **Nano Banana 2 no fal.ai**, em 2K, prompt em inglês. Render: HTML para PNG com Puppeteer.

Dois papéis de foto que não se misturam: **`imagem`** é a foto real que entra inteira na peça; **`foto_expert`, `foto_produto` e `foto_espaco`** nunca entram na peça, servem só de semente para gerar rosto, produto ou lugar fiéis. Pessoa real cadastrada só aparece por foto real ou gerada **com** a `foto_expert` dela; cada marca decide se pode gerar pessoa inventada.

## Regras que valem para todos os clientes

- **Story nunca imita a interface do Instagram** (regra do Eduardo, 2026-10-06): nada de botão, pílula com seta, enquete, caixa de pergunta, slider, figurinha de link, "arraste para cima". O convite é texto corrido: link da bio, DM ou responder o story.
- **Template é HTML completo**, sem `{{placeholders}}`, com conteúdo de exemplo no tom da marca, cores travadas no `:root` e fontes pelos aliases `titulo-font` e `corpo-font`. Feed 1080×1440, story 1080×1920. Sem `<link>` nem Google Fonts (o sanitizer remove).
- **Logo na mesma altura e coordenada em todos os templates** da marca; margem única; CTA em pílula só no feed.
- **Fonte só TTF ou OTF** (woff2 quebra o nome da família). A descrição da fonte precisa ter `titulo` ou `corpo` sem acento; a da logo para fundo escuro precisa ter `escuro`, `branco` ou `negativ`.
- **Texto da config com acentuação correta**: sem acento ali, o conteúdo do cliente sai sem acento.

## Como renderizar templates nesta máquina

O `npm run gen:preview` do backend dá timeout no Puppeteer aqui (o PC lento, ver memória do Claude) e ainda exige as variáveis de ambiente (usar o `.env.test`). O que funcionou em 2026-11-11: injetar os `@font-face` da marca com os aliases e tirar o print direto com `chrome.exe --headless=new --screenshot`, cerca de 30 segundos por imagem.

## Como continuar

O método completo é a skill `/onboardnap`, que mora em `napshift/.claude/skills/onboardnap/` (diretrizes 01 a 09 e a convenção de descrição de referências). Para produzir peça de um cliente: ler a config e o inventário dele e conferir o log de publicação. Nunca buscar regra de marca fora da pasta do cliente.
