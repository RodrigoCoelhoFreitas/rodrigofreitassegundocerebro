---
tags: [projeto, jogo, arte, cor]
---

# Paleta do Gatoelho

Ramificação de [[Direção de Arte e Som do Gatoelho]]. **Revisão 1, 2026-10-16. Status: proposta do Claude, nada decidido.** Pedido do Rodrigo: continuar pensando na paleta de cores, numa das conversas paralelas sobre o Gatoelho. Versão visual, com prints do jogo e simulação de daltonismo: https://claude.ai/artifact/WYd2nDjGaon1ob61KYFKyz

**Como foi feito.** Leitura de `src/art/palettes.ts` e de todas as cores fixas do código; das notas de história, Camada Zero, Tecido Infinito, Personagens, Guarda-Roupa e [[Misturas do Gatoelho]]. Prints tirados do jogo (Electron sem janela contra o Vite), com as paletas novas trocadas em tempo de execução (nenhum arquivo do jogo foi alterado). Daltonismo simulado com as matrizes de Machado, Oliveira e Fernandes (2009), na forma mais forte; diferenças de cor medidas em ΔE (CIEDE2000).

---

## A proposta em cinco pontos
1. **Um dicionário de cores**: cada cor quer dizer a mesma coisa no jogo inteiro. A criança usa as cores para jogar; quem repara descobre que elas contam a história.
2. **O vermelho é a lã das Vós**: só é vermelho o que foi tricotado.
3. **Cada região tem uma cor dominante e um destaque**; os destaques das quatro antenas, somados como luz, dão o branco do Clarão.
4. **A cor acompanha o arco**: cheia, azul de chuva na noite escura, as quatro cores no Pico, misturadas no fim. Cinza só para a Traça.
5. **Consertos que os prints mostraram**, com um teste novo (o **robô daltônico**) para que não voltem.

---

## Parte 1 — O dicionário
### Para jogar (a criança aprende na Fase 1 e usa até o fim)
| Cor | Quer dizer | Onde | Estado |
|---|---|---|---|
| Vermelho-lã `#d62828` | Siga | Lenço, fio vermelho | no código |
| Laranja-cenoura `#f77f00` (folha `#52b788`) | Pegue | Cenouras. Proposta: halo claro suave atrás de tudo que se pega | no código |
| Dourado `#ffc93c` | Algo novo para você | Habilidade, Cenoura Dourada, painel de habilidade, fase aberta no mapa. Sempre com brilho. Luzes do cenário nunca neste dourado | no código |
| Roxo `#9d4edd` | Escondido, e verdadeiro | Cenoura Roxa, saída secreta, Horta Escondida, luz de lua do cochilo `#b48cff`, céu dos sonhos | no código |
| Pontas claras `#f1e3b8` | Machuca | Todo espinho tem ponta clara; o corpo do espinheiro passa a vir da sombra da região. Água sempre com brilho branco | muda (corpo) |
| Fio de luz na borda (`light` da paleta) | Dá para pisar | Linha de luz em cima de todo chão | no código |

### Para ler (ninguém precisa entender; quem repara junta as peças)
| Cor | O que é |
|---|---|
| Vermelho desbotado `#b5524f` (no código, igual em 3 arquivos) | O mesmo vermelho, cansado: lenço do Bigodes, novelo do cochilo, lenço no galho, sonhos |
| Latão `#d4a537` (no código: o relógio) | Tudo que é de corda, do Bigodes: relógio, Tic e Tac, engenhocas, carrinho da Cisnobra. Dourado fosco, sem brilho, nunca parece item |
| Porcelana `#f3eefc` + florzinha azul `#6c7fd8`, vime `#c8955a` (no código) | Coisas da casa, herança da Vó de Todas: xícaras, cesto, objetos dos cochilos |
| Luz das Máquinas `#c8f4ff` (nova) | O mundo de antes: lâmpada das antenas (eram mastros), terminais do `// oi ~`, fendas, Ecos, a lua dupla na água, o reflexo que pisca. **Não muda com a hora do dia**: numa tarde dourada, só ela continua fria |
| Sépia (nova) | O passado: dentro da Casinha da Serra, Mundo do Bigodes parado, Ecos Antigos |
| Cinza de feltro `#9a9aa2` (nova) | Onde a Traça comeu, a cor some. **Só a Traça usa cinza** |
| Azul-noite `#271c57` + lilás `#cdbdf5` (no código) | Os sonhos: o único lugar sem as cores de jogar |
| Iridescente (muda; hoje é rosa-choque `#ff5d8f`) | O Embaralhamento: a Onda não tem cor própria, passa por todas |

---

## Parte 2 — A regra do vermelho
- O Tecido Infinito sorteia a pelagem, então o laranja não identifica o Gatoelho: **o lenço é** (o Guarda-Roupa já diz que ele não sai). A Camada Zero diz por quê: a Vó de Todas tricotava lenços vermelhos, e a Vó de cada redoma herdou o gesto. **O vermelho é a única cor do jogo que veio das pessoas.**
- **Regra: só é vermelho o que foi tricotado por uma Vó.** Lenço, fio, novelo, blusa inacabada da Vó Tartagarça, lenço de lata do Robogato, e os corações do HUD virando **corações de tricô**. Céu, flores, frutas, inimigos e telhados: coral, rosa, malva ou barro apagado. A criança vê vermelho e segue; o adulto percebe que todo vermelho é lã.
- **O fio tem forma**: um nozinho a cada palmo, para quem não enxerga vermelho. Na Dimensão das Teias (fios de todas as cores), é o nozinho que acha o fio certo.
- Combina com o [[Fio da Meada do Gatoelho]] (remendos "com ponto vermelho à vista") e com a [[Misturas do Gatoelho]] (lenços de urucum, que desbota ao sol: se entrar, a cor vira "vermelho-urucum").
- **Fora da regra no código hoje:** corações do HUD `#e63946` (`ui/Hud.ts`); Onda e luz da antena `#ff5d8f` (`render/ScrambleFx.ts`, `render/ForestBackdrop.ts`); flores `#ef476f` (`render/DecorView.ts`, `world/WorldMapView.ts`); frutinhas vermelhas no espinheiro `#e63946` (`render/LevelView.ts`: vermelho num perigo diz "siga" no lugar errado; virar amoras escuras); perigo no minimapa `#ff5a5f` (`ui/Minimap.ts`). As placas desenham o lenço em `#d62828`: certo.

---

## Parte 3 — As regiões do jogo 1
Dominante = o clima do lugar; destaque = a cor do que ele tem de especial, que é também a cor do feixe da antena dele (Marco 8). Hora e clima variam dentro disso.

| Região | Dominante | Destaque | Por quê |
|---|---|---|---|
| **Bosque das Cenouras** (Ato I) | musgo | cenoura `#f77f00` | A horta da Vó. Manhã, tarde e noite secreta já existem e viram as três horas do Bosque |
| **Telhadópolis** (Marco 4) | hora azul + telha de barro apagada `#b98470` | azulejo `#2a80e8` | A cidade é o mais "de gente" que os bichos têm (fala, voto, jornal são herança humana). O azul e branco do azulejo é o das xícaras da Vó |
| **Tocópolis** (Marco 5) | umbra-violeta | vaga-lume `#90f0b8` | A única região em que a luz vem dos bichos: o fio de luz das bordas é verde de vaga-lume. Verde mais frio que o real para não confundir com o dourado em quem tem daltonismo. A antena inverte claro e escuro |
| **Casinha da Serra** (Marco 6) | azul-serra na neblina | âmbar de dentro | Fora frio, dentro sépia: a tentação é casa. Sem antena |
| **Monte Ronrom** (Marco 7) | turquesa, céu lavado | ipê-rosa `#ff9ec4` | O lugar mais claro do jogo. O rosa é a Araipê e o Borbopótamo; pétalas no ar |
| **Pico do Clarão** (Marcos 10–13) | noite metálica | os quatro feixes → branco | O Pico quase não tem cor própria; as cores chegam nos feixes |
| **Noite escura** (Marco 9) | **azul-chuva** (recomendado) ou cinza | só o lenço e o fio | Azul: é a mesma chuva do prólogo e do Mundo do Gatinho (as três cenas rimam), triste sem ser morta para uma criança de 5 anos, e deixa o cinza só para a Traça |

---

## Parte 4 — Os quatro feixes
- As quatro cores de destaque (cenoura, azulejo, vaga-lume, ipê) estão espalhadas pelo círculo de cores; **somadas como luz, dão um branco levemente rosado** (conferido nas contas: `#c5acb5`, ΔE ≈ 12 do cinza neutro). O Clarão é feito das cores do mundo.
- **Conciliação com o [[Fio da Meada do Gatoelho]]** (Nó 5, outra conversa de hoje: as antenas aprendem o cheiro do Gatoelho e os feixes sobem com as cores das fitas dele). Recomendo juntar: o feixe sai da antena **na cor da região** e, subindo, **vira as duas cores das fitas do Gatoelho**. A criança vê as cores dos lugares indo embora; quem repara vê a máquina mirando nele. O branco das quatro somadas fica para o instante do disparo.
- Ideia (Marco 13): os quatro pedaços da foto vêm tingidos com a cor da antena de onde saíram; juntos, a foto fica com as cores normais.

## Parte 5 — A cor acompanha o arco
Bosque cheio → Telhadópolis, Tocópolis, Monte Ronrom (a última cor cheia) → Marcos 8 e 9: azul de chuva, só o fio é vermelho → Pico: as quatro cores chegam → Final da Toca: as cores voltam **misturadas**, como a colcha com um retalho faltando. "Inteiro não é puro", sem uma palavra.

---

## Parte 6 — O que os prints mostraram (consertos)
Do mais sério ao mais leve. Abaixo de uns ΔE 20, um objeto pequeno se mexendo começa a sumir no fundo.
1. **A tarde dourada (Fase 2) some para quem não vê vermelho e verde.** Céu, névoa, árvores e chão puxam para laranja e oliva, como a cenoura e o Gatoelho. Cenoura × céu do meio: ΔE 15 (11,5 com deuteranopia). Proposta testada (`tardeFria`, abaixo): sol, horizonte e chão quentes, árvores e montanhas de fundo na sombra violeta (contraluz). Pior caso sobe para ΔE 28 (23). Fica mais "entardecer" e menos "dourado": **decisão de gosto do Rodrigo**.
2. **O caracol tem a cor da cenoura**: concha `#d08a3a` × cenoura, ΔE 9. A Caracouve (concha de couve) resolve: ΔE 48.
3. **Na Horta Escondida, o sapo-balão tem a cor da grama**: `#5cc7a3` × `#5fbf8e`, ΔE 4,6. Grama azul-lua `#57a0c8`: ΔE 29.
4. **O halo do sol é dourado**: a Cenoura Dourada passou na frente do sol da manhã; halo `#ffd89a` × dourado, ΔE 11. Halo `#fff2d6`: ΔE 21.
5. **O espinheiro tem cor fixa** (`#2f6b3a`): quase a cor das árvores de perto na manhã (ΔE 10) e verde num mundo violeta nas regiões novas. As pontas claras avisam em toda luz; o corpo deve vir da sombra da região.
6. **A Onda é rosa-choque** (`#ff5d8f`), quase o ipê de Monte Ronrom. Proposta: Onda iridescente; lâmpada da antena na luz das Máquinas.

**Critério do robô daltônico** (cenoura × cada camada de fundo ≥ 20 com visão normal e com deuteranopia; dourado × halo do sol ≥ 15):

| Paleta | Cenoura × pior fundo | com deuteranopia | Dourado × halo | Resultado |
|---|---|---|---|---|
| Bosque · manhã (hoje) | 26,9 | 23,1 | 11,4 | não passa (halo) |
| Bosque · tarde (hoje) | 15,2 | 11,5 | 19,3 (7,6 deut.) | não passa |
| Horta Escondida (hoje) | 48,2 | 53,1 | 63,6 | passa |
| Bosque · tarde (proposta) | 28,3 | 22,8 | 20,9 | passa |
| Telhadópolis | 32,9 | 28,1 | 25,5 | passa |
| Tocópolis | 49,7 | 51,4 | 33,5 | passa |
| Casinha da Serra | 30,8 | 26,6 | 16,1 | passa |
| Monte Ronrom | 39,3 | 28,2 | 33,2 | passa |
| Pico do Clarão | 41,2 | 43,0 | 45,0 | passa |
| Noite escura · azul | 42,7 | 47,2 | 43,9 | passa |

---

## Parte 7 — Dimensões e lugares do Ato IV
Transformação por cima da paleta (`ColorMatrixFilter`), **nunca nas cores de jogar**.

| Lugar | Cor | Por quê |
|---|---|---|
| Mundo do Bigodes (redoma 8, parada) | Sépia; nada se mexe, nem a névoa | Sépia = passado (a mesma de dentro da Casinha) |
| Dimensão Lenta (redoma 3) | Azul-gelo dessaturado, rastros | O relógio quebrou; a cor esfria |
| Dimensão dos Espelhos (redoma 5) | Matiz girado pela metade do círculo, imagem espelhada | O Bosque fica magenta, a água laranja |
| Dimensão do Reflexo | As duas cores do lenço do jogador viram a paleta | O mundo de quem ajuda tem as cores de quem ajuda |
| Dimensão das Teias (redoma 6) | Quase preto, fios de todas as cores | Achar o fio vermelho pelo nozinho |
| Dimensão Original (o lado de fora) | O lugar mais colorido, cores naturais e cheias | "Ninguém é de uma cor só" |
| Ilha das Nove Vidas | Retalhos, cada pedaço na paleta de uma redoma | A colcha em forma de lugar |
| Mundo do Gatinho / do Coelhinho | Azul-chuva com poste amarelo / rosado de toca, luz de vela | Rimam com o prólogo; um ninguém esperava, o outro alguém esperava |
| O Avesso e a Traça | Cinza de feltro, bordas comidas mostram a trama | Só aqui existe cinza |
| Fendas | Borda na luz das Máquinas | Rachaduras nas paredes das redomas |
| Sonhos | Azul-noite e lilás (já existe) | Sem cores de jogar |

---

## Parte 8 — Personagens
- **Mil pelagens, um lenço.** O sorteio do Tecido Infinito só usa pelagens de gato de verdade (laranja, preto, cinza, creme, frajola, siamês, tigrado), olhos verdes, âmbar ou azuis, e duas garantias: **fio de luz na borda** na cor da luz da região e **lenço como a cor mais forte do corpo**.
- **O Bigodes = a pelagem do jogador envelhecida**: mesma semente, cor puxada uns 45% para o cinza e um pouco para o claro, focinho e bigode brancos, lenço desbotado, mesma orelha torta. É uma conta, então vale para qualquer pelagem, e a poça fica pessoal.
- **Elenco:** ninguém usa vermelho saturado, salvo o que é lã. Dourado com brilho só em item. Tudo que é de corda é latão.
- **Tintas do Guarda-Roupa:** umas 12, testadas contra todas as pelagens. O vermelho-lã não é tinta (o lenço é a única peça vermelha). As cores vindas do Modo Reflexo entram ajustadas para caber no conjunto.

## Parte 9 — As fitas do Faro
**A cor da fita diz o que o bicho sabe fazer; um símbolo na fita diz qual bicho é** (para daltonismo e para colecionar). As flores de DNA da [[Misturas do Gatoelho]] usam a cor do bicho que guardam (a Flor-Pluma já é lilás e a Flor-Escama já é verde-água no código).

| Família | Cor | Símbolo | Exemplos |
|---|---|---|---|
| Voa | lilás-pluma `#d6b8ff` | pena | aves, insetos, morcego · Flor-Pluma |
| Nada | verde-água `#72efdd` | onda | peixe, sapo, baleia · Flor-Escama |
| Cava | ocre `#d9a45a` | grão | coelho, toupeira, tatu · Flor-Casca |
| Caça | azul-noite `#4a5ad0` | garra | gato, lobo, jacaré |
| Carrega a casa | musgo `#8fae5a` | casco | tartaruga, caracol |
| Brilha | vaga-lume `#90f0b8` | estrela | vaga-lume · Flor-Lume |

- O Gatoelho é **caça + cava**: azul-noite e ocre, um par de opostos. O Bigodes tem as mesmas duas (Final do Cochilo). O gato "puro" da Dimensão Original tem todas. Se as fitas tiverem de ser "do Gatoelho de cada jogador" (Fio da Meada), a família é a mesma e o tom sai da semente.
- Pares que se confundem com daltonismo: cava × casa, voa × nada; o símbolo resolve.
- Ideia: o lenço de duas cores do Fio Vermelho vem sugerido com as duas cores das fitas do Gatoelho. O jogador ainda escolhe.

---

## Parte 10 — No código
- **`src/art/colors.ts`**: o dicionário num lugar só. Hoje a tinta `#5a2d0c` está repetida em 6 arquivos, o dourado em 3, o vermelho desbotado em 3.
- **Região × hora no `palettes.ts`**: as três paletas viram Bosque·manhã, Bosque·tarde, Bosque·noite; a fase diz região e hora.
- **Cores fixas que passam a seguir a região**: corpo do espinheiro, flores do chão, árvores do mapa.
- **Dimensões e ondas**: filtro no fundo e no terreno; cenouras, espinhos, lenço e Gatoelho fora.
- **Robô daltônico** em `tests/sim`, irmão do robô-criança, com o critério da Parte 6.
- O script de prints (Electron sem janela, troca de paletas com o jogo rodando) ficou na pasta temporária da conversa; pode virar ferramenta do repo.

### Paletas propostas (testadas no motor)
Mesma estrutura de `Palette` em `src/art/palettes.ts`. `tardeFria` herda da `tarde` atual.
```ts
tardeFria: { ...tarde, sky: [0x34457e, 0xb48ab8, 0xffe6c0], sun: { color: 0xffefc0, glow: 0xffe8d0, x: 0.78, y: 0.44, radius: 54 },
  cloud: 0xffe0c8, cloudShade: 0xb08aa8, mountains: 0x7f72a6, hills: 0x9a80a8, treesFar: 0x5f6a8c, treesNear: 0x3e4a68,
  fog: 0xead6e2, fogAlpha: 0.45, foreground: 0x1f1a2a, veil: { color: 0xff9f43, alpha: 0.025 } },
telhado: { sky: [0x27305e, 0x6f6aa8, 0xf0c8d0], sun: { color: 0xfff0d8, glow: 0xffd6c8, x: 0.15, y: 0.58, radius: 40 },
  cloud: 0xe8c8d8, cloudShade: 0x8a7aae, cloudAlpha: 0.7, mountains: 0x8f8fc0, hills: 0x7f7aab, treesFar: 0x5e5c92, treesNear: 0x403f72,
  fog: 0xcdbfe0, fogAlpha: 0.42, foreground: 0x17152b, light: 0xffd2a8, grass: 0xb98470, grassLight: 0xf0c0a0, grassDark: 0x8a5c55,
  dirt: [0x8a7590, 0x6b5a78, 0x51445f, 0x372e45], water: { surface: 0x6f8fe0, deep: 0x26306e, light: 0xe2e6ff },
  motes: 0xffe2c0, veil: { color: 0x4a5ad0, alpha: 0.04 }, vignette: 0.55 },
toca: { sky: [0x0f0a14, 0x221826, 0x3e2c38], sun: { color: 0xe6fff2, glow: 0xa0f0c0, x: 0.72, y: 0.3, radius: 8 }, stars: true,
  cloud: 0x3a2836, cloudShade: 0x1f1520, cloudAlpha: 0.35, mountains: 0x3c2a3c, hills: 0x4a3446, treesFar: 0x3a2a38, treesNear: 0x281c28,
  fog: 0x5a4256, fogAlpha: 0.38, foreground: 0x0b080c, light: 0xb0f8d0, grass: 0x7a8a4c, grassLight: 0xc0d67a, grassDark: 0x4c5632,
  dirt: [0x6e4c3a, 0x56392b, 0x402a20, 0x2a1b15], water: { surface: 0x4c86b8, deep: 0x16284a, light: 0xcff6ff },
  motes: 0x90f0b8, veil: { color: 0x2a1240, alpha: 0.05 }, vignette: 0.75 },
casinha: { sky: [0x7b90ae, 0xc0ccd9, 0xece2d2], sun: { color: 0xfff6e6, glow: 0xffe2b8, x: 0.62, y: 0.32, radius: 28 },
  cloud: 0xf3f5f7, cloudShade: 0xb6c2d0, cloudAlpha: 0.92, mountains: 0xa9b6c6, hills: 0x93a3b3, treesFar: 0x6f8193, treesNear: 0x4b5b6b,
  fog: 0xe6ebf0, fogAlpha: 0.68, foreground: 0x1b232c, light: 0xfff1d8, grass: 0x93ad7c, grassLight: 0xd2e2ac, grassDark: 0x62805a,
  dirt: [0x8c7b68, 0x6f6052, 0x55493f, 0x3b332d], water: { surface: 0x7aa7cc, deep: 0x2d4b6c, light: 0xe8f3ff }, motes: 0xf8f2e6, vignette: 0.5 },
ronrom: { sky: [0x3e8fd8, 0xa8e4f0, 0xf4fff8], sun: { color: 0xffffff, glow: 0xdafff6, x: 0.28, y: 0.2, radius: 32 },
  cloud: 0xffffff, cloudShade: 0xcfeaf2, cloudAlpha: 0.95, mountains: 0xb4d9e6, hills: 0x9fd4ca, treesFar: 0x70baa8, treesNear: 0x3f8f82,
  fog: 0xeffbfa, fogAlpha: 0.55, foreground: 0x0f3d3a, light: 0xffffff, grass: 0x84cf78, grassLight: 0xd4f8a2, grassDark: 0x4b9a64,
  dirt: [0x8b7d70, 0x6d6157, 0x53483f, 0x3a322c], water: { surface: 0x4fc8da, deep: 0x186a8c, light: 0xeaffff }, motes: 0xffc6de, vignette: 0.4 },
pico: { sky: [0x151930, 0x484d78, 0xd6d0f0], sun: { color: 0xffffff, glow: 0xdcd8ff, x: 0.78, y: 0.28, radius: 24 }, stars: true,
  cloud: 0x9894c0, cloudShade: 0x48487a, cloudAlpha: 0.6, mountains: 0x6a6c94, hills: 0x585a80, treesFar: 0x42446a, treesNear: 0x2c2e50,
  fog: 0xb2aed8, fogAlpha: 0.4, foreground: 0x0b0c19, light: 0xffffff, grass: 0x9c9eba, grassLight: 0xe8eaff, grassDark: 0x6a6c8c,
  dirt: [0x5c5c76, 0x47475f, 0x35354a, 0x23232f], water: { surface: 0x8ca2f2, deep: 0x22285e, light: 0xf2f2ff },
  motes: 0xffffff, veil: { color: 0xb4acff, alpha: 0.04 }, vignette: 0.6 },
chuvaAzul: { sky: [0x1f2b47, 0x3c5274, 0x6f86a6], sun: { color: 0xe6eeff, glow: 0x9fb4d8, x: 0.8, y: 0.2, radius: 18 },
  cloud: 0x52688a, cloudShade: 0x33445f, cloudAlpha: 0.85, mountains: 0x4f6488, hills: 0x47597a, treesFar: 0x3a4a68, treesNear: 0x2a3650,
  fog: 0x6a7f9e, fogAlpha: 0.48, foreground: 0x0f1522, light: 0xc4d4ee, grass: 0x5a7a74, grassLight: 0x8fb0a8, grassDark: 0x3e5a58,
  dirt: [0x4a4c58, 0x3c3e4a, 0x2f303a, 0x22232b], water: { surface: 0x5a7aa8, deep: 0x1a2844, light: 0xd2e0f4 }, motes: 0xa8bad4, vignette: 0.68 },
chuvaCinza: { sky: [0x2a2f37, 0x4a5059, 0x6c727b], sun: { color: 0xd0d4da, glow: 0x8c929a, x: 0.8, y: 0.2, radius: 18 },
  cloud: 0x5c626b, cloudShade: 0x3b4048, cloudAlpha: 0.85, mountains: 0x5c626b, hills: 0x51575f, treesFar: 0x464b53, treesNear: 0x353940,
  fog: 0x6c7279, fogAlpha: 0.5, foreground: 0x131519, light: 0xbac0c8, grass: 0x606a63, grassLight: 0x8c958e, grassDark: 0x444c47,
  dirt: [0x504b47, 0x413d3a, 0x322f2d, 0x242221], water: { surface: 0x5c6c7c, deep: 0x202b37, light: 0xcad5e0 }, motes: 0x9ca6b2, vignette: 0.72 },
```

---

## Perguntas em aberto
1. A regra do vermelho (só o que foi tricotado por uma Vó), incluindo os corações de tricô no HUD?
2. Os destaques (azulejo, vaga-lume, ipê) e os feixes: cor da região, cores das fitas do Gatoelho (Fio da Meada) ou um virando o outro enquanto sobe (recomendado)?
3. A tarde com sombra violeta ainda é a "tarde dourada"?
4. Noite escura em azul-chuva (recomendado) ou cinza?
5. Onda iridescente no lugar do rosa-choque?
6. Fitas do Faro pelo que o bicho sabe fazer, com o Gatoelho em azul-noite e ocre?
7. Fazer os consertos pequenos no código (halo do sol, grama da Horta, corpo do espinheiro, vermelhos fora da regra, `colors.ts`, robô daltônico)?

## Decisões do Rodrigo
(Ainda nenhuma.)
