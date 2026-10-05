---
tags: [projeto, jogo, arte, áudio]
---

# Direção de Arte e Som do Gatoelho

Ramificação de [[Gatoelho]]. Identidade visual e sonora — o que existe hoje (provisório) e o que falta decidir. Ver também [[Game Design do Gatoelho]] (personagem) e [[Arquitetura do Gatoelho]] (como animação e áudio estão no código).

## Direção visual desejada
**Cartoon 2D moderno, extremamente polido, expressivo e colorido**, com a sensação de grandes animações cinematográficas familiares, mas com identidade própria. Decisão importante já tomada pelo Rodrigo: **o Gatoelho pode ter bastante detalhe, mas os cenários devem ser clean** — personagem, inimigos, plataformas importantes, perigos e itens precisam ser identificados na hora. Trabalhar com silhuetas claras, formas arredondadas, cores agradáveis, separação de planos, iluminação, profundidade e parallax, sem ruído visual.

## Concept art × asset de jogo
Preocupação do Rodrigo desde o início: não transformar imagens bonitas diretamente em sprites. Antes de produzir centenas de sprites, definir: tamanho do personagem na tela, resolução, proporções, pivôs, hitboxes, número de quadros e frame rate das animações, nomenclatura, organização das spritesheets, transparência, escala, filtros e pipeline de exportação. **Ainda não definido** — hoje o jogo usa resolução lógica 960×540 e hitbox provisória 28×44 px.

## O que existe hoje (tudo provisório)
- **Boneco geométrico do Gatoelho** (`GatoelhoRig`): corpo laranja, barriguinha clara, lenço vermelho, olhos verdes, orelhas de coelho, rabo com ponta clara; vira para o lado em que anda. Usado na fase, na tela de título (em tamanho grande) e no mapa do mundo.
- **Ícone do executável**: rosto do Gatoelho desenhado por código.
- Fase: blocos verdes com faixa de grama, espinhos cinza, céu azul. Mapa do mundo: grama, rio com ponte, árvores, plantação de cenouras, flores, nuvens — o trecho visualmente mais acabado até agora.
- Abertura **"LUDOVIC STUDIO"** (letras entrando, linha dourada) — ver [[Ludovic Studio]].

## Animação
- Sistema **por canais** (corpo esticar/achatar, orelhas de trás e da frente, olhos, rabo), com clipes como dados e personalidade agendada por um controlador — **pensado para ser reaproveitado com a arte definitiva**: os mesmos canais podem mover ossos de um esqueleto (Spine) ou virar índice de quadro de spritesheet.
- Estados: parado, correndo, pulando, caindo, planando; sobreposições: piscar (a cada 2–5 s), achatada ao pousar, comemoração no fim da fase.
- **Manias de parado** (personalidade quando o jogador não faz nada, pedido do Rodrigo): depois de 2,5 s parado, a cada 4–7 s — tremer a orelha, olhar em volta, brincar com o rabo, espreguiçar — sem repetir a mesma em seguida.
- Ideia forte ainda não implementada: **orelhas e rabo com física procedural** (mola/corrente), dando expressividade "de graça" e barateando muito a produção de animação.

## Som (provisório, sintetizado)
- Não há arquivos de áudio: tudo é **sintetizado por código** (Web Audio) em estilo chiptune alegre. Cada som e música tem **um nome**; trocar por gravações depois não mexe no jogo.
- Efeitos: menus, brilho da abertura, pulo, pulo duplo, vento ao planar, pouso, dano, perda de vida, pausa, fanfarra de chegada, caminho revelado no mapa, passo no mapa.
- Músicas: **título** (tranquila, 100 bpm), **mapa** (passeio, 112 bpm), **fase** (animada, 132 bpm). A música abaixa na pausa.
- O Claude verificou que o som **sai** (medindo o sinal), mas não consegue ouvir — a avaliação de gosto é do Rodrigo.

## Em aberto
Quem desenha, anima e compõe; técnica de animação definitiva (quadro a quadro × esqueleto); pipeline de exportação de sprites; paleta e tipografia oficiais.

## Atualização 2026-09-30
- **Fase com cara de bosque**: fundo em camadas com profundidade (céu em degradê, nuvens, montes, duas linhas de árvores), em cores suaves para não competir com o primeiro plano; terreno com grama ondulada e terra com pedrinhas; galhos de madeira com folhinhas.
- **A toca do Gatoelho**: morrinho verde com porta redonda de madeira, janela acesa e chaminé — é de onde ele sai na Fase 1.
- Objetos novos (todos provisórios, desenhados por código): cenoura, Cenoura Dourada com brilho (e "fantasma" quando já foi pega antes), Dente-de-leão Dourado, flor de vento azul-clara com tracinhos subindo, placa de madeira com balão de fala, checkpoint com bandeirinha que sobe.
- **Anúncio de habilidade**: clarão, painel dourado "Nova habilidade!" e o boneco demonstrando de orelhas abertas.
- Sons novos: cenoura ("plim" discreto), Cenoura Dourada (arpejo brilhante), nova habilidade (fanfarra longa), checkpoint.

## Banho de gráficos (2026-10-01)
Pedido do Rodrigo: manter a vibe, mas com formas mais arredondadas e qualidade "padrão Disney", cores lindas e misteriosas como em Hollow Knight, e tudo pronto para depois levantar a lista de sprites.

**Princípios adotados**
- Formas arredondadas e cheias; volume por degradê (luz em cima, sombra embaixo); contorno colorido e escuro, nunca preto; fio de luz na borda do lado do sol.
- Profundidade pela névoa: cada camada do fundo mais distante é mais clara e se perde na cor da névoa. Luz quente contra sombra fria.
- Capricho no **fundo**, frente limpa: silhuetas de capim na frente da câmera foram testadas e **descartadas** pelo Rodrigo; raios de sol também foram testados e **removidos** ("luzes muito, muito mais suaves").
- **Chão fino na tela**: a câmera enquadra o Gatoelho baixo (bastante céu, pouca terra); nos pulos e voos ela segura a altura do último chão, para o chão continuar à vista nos sobrevoos, e desce quando ele cai ou mergulha.
- O Gatoelho mantém a **silhueta original** (corpo retangular arredondado, orelhas retas com interior creme, rabo reto com ponta creme, lenço em faixa). Um redesenho mais "Disney" (feijão, focinho, bigodes, mochila) foi testado e recusado por ficar diferente demais; o apelo entra no acabamento (pelagem em degradê, olhos com brilho, bochecha corada).

**O que mudou**
- O jogo desenha na resolução real da tela (antes era 960×540 esticado e borrado).
- Fundo novo: céu em degradê, sol/lua com halo, nuvens fofas, bandos de passarinhos, montanhas e morros com fio de luz, **ruínas de pedra com musgo** (arcos, colunas, uma cabeça de pedra de orelhas compridas — pista do "mundo de antes"), duas linhas de copas com cipós, névoa entre as camadas, pozinho de luz.
- Paletas por fase refeitas: manhã de neblina (Fase 1), tarde dourada com a antena (Fase 2), noite violeta com estrelas e cogumelinhos que brilham (Horta Escondida).
- Terreno: grama em almofada com borda ondulada, terra que escurece com a profundidade, quinas redondas, pedrinhas e raízes; galhos, troncos, espinheiros e água com volume e brilho.
- Objetos e seres: cenouras arredondadas, Douradas/Roxa/itens com brilho de verdade, placas e checkpoint de madeira, toca com janela acesa, caracol e passarato fofos, cogumelo brilhante, troncos com anéis, cenouras fujonas com olhinhos.
- Sombra de contato sob o Gatoelho (fica no chão quando ele pula). Título com o mesmo cenário deslizando.

**Catálogo de sprites**: `src/art/sprites.ts` lista 64 vagas (o que é, tamanho, âncora, animações, variações e onde está o desenho provisório). `node tools/listar-sprites.mjs > docs/sprites.md` gera a lista de encomenda (245 quadros de animação ao todo). Um teste garante que o catálogo continua batendo com o código.

**Ainda no estilo antigo**: o mapa do mundo, os painéis de pausa/resultado e o HUD (corações e ícones).

## Fases v4 (2026-10-01, noite) — limpeza, nitidez, cochilo e sonhos
Pedido do Rodrigo: gráficos **um pouco mais limpos**, **melhor qualidade de resolução**, fim de fase num **canto interessante com um objeto doméstico** curioso, transição de **sonho só com pistas** e uma **animação melhor de deitar**.

**Mais limpo**
- Fundo: a linha de copas de perto ficou rala e entra na névoa; os cipós saíram; menos partículas de luz, mais fracas.
- Chão: menos pedrinhas, riscos e raízes no terreno; menos tufos, flores e árvores de fundo espalhados; o cantinho do cochilo fica sem enfeites em volta.

**Mais nítido**
- Curvas desenhadas com mais pontos (bordas redondas grandes não ficam "facetadas" em 2× e 3×).
- A câmera para no pixel **da tela**, não no pixel do jogo: em tela cheia a rolagem era aos saltos de 2–3 pixels; agora é lisa.

**Os cantinhos do cochilo** (uma luz mansa que desce do céu num objeto de alguém que passou antes):
- Fase 1 — **cesto de vime** com almofada xadrez; ao lado, um **novelo vermelho desbotado** com agulhas de tricô, e o fio segue adiante pelo chão.
- Fase 2 — **pantufa velha** com cara de gato e **orelhas de coelho**, um remendo e pompom, grande demais para ele.
- Saída secreta da Fase 2 — **relógio de bolso** em pé, com os **ponteiros andando para trás** e, na tampa, um retratinho de alguém de orelhas compridas; a corrente enrolada no chão vira ninho.
- Horta Escondida — **xícara de porcelana** sobre o pires, com **óculos redondos dobrados** ao lado.
- O objeto tem frente e fundo: o Gatoelho deita **dentro** (a parede do cesto/xícara fica na frente dele).

**Animação de deitar** (canais novos `bodyTilt` e `mouth`): fareja inclinado com a orelha atenta → pulinho para dentro → amassa o pãozinho (olhinhos de satisfação) → duas voltinhas (o corpo "afina" de lado no meio do giro) → espreguiça, **boceja com a boca aberta**, desce devagar, orelhas deitam e o rabo dá a volta → dorme respirando, com a orelha tremendo de vez em quando.

**Sonhos** (tela azul-noite, bolinhas de luz desfocadas, silhuetas lilás, nenhuma palavra): dois mundos que viram um (Fase 1), o velho do lenço (Fase 2), reflexos (saída secreta), cenouras roxas (Horta). O que cada um quer dizer está em [[História e Mundos do Gatoelho]]. A volta para o mapa depois do sonho é um "acordar" macio (some no azul do sonho, em vez da íris).

**Bichos novos**: sapo-balão verde-água com barriga clara e pintinhas de baiacu; galho-mola com folhas e uma florzinha na ponta (o que o diferencia de um galho comum); caracol escondido na concha; passarato tonto com estrelinhas.

**Sons novos** (sintetizados): quique com embalo, arremesso do galho, rangido do galho, "plim" de quem volta ao normal, bocejo, entrada no sonho.

Catálogo de sprites: **77 vagas, 370 quadros** (`docs/sprites.md`).
