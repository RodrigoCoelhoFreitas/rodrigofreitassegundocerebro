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
