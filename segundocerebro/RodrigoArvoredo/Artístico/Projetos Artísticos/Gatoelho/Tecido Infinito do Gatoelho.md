---
tags: [projeto, jogo, game-design, arquitetura]
---

# Tecido Infinito do Gatoelho

Ramificação de [[Gatoelho]], parte da bíblia do [[Arco Completo do Gatoelho]]. **Revisões 8 e 9 (2026-10-05), proposta do Claude.** A Revisão 9 (Parte 9, no fim) refaz a trama infinita à luz da [[Camada Zero do Gatoelho]], sem mudar nada do que está antes dela. Pedidos do Rodrigo: um jogo para **jogar a vida inteira**, com **dimensões infinitas** (uma por Novo Jogo), **geração aleatória** de detalhes e de histórias paralelas, **camadas de fases secretas que pareçam infinitas**, **missões escondidas no Modo Reflexo**, uma **caça quase infinita de itens**, **recortes de jornal infinitos** (em [[Jornal do Gatoelho]]) e a segunda premissa: **cada pessoa joga um Gatoelho diferente**.

## A segunda premissa
> **Cada pessoa joga um Gatoelho diferente.**

Ela sai direto da história: **existem infinitas dimensões, e em cada uma existe um Gatoelho.** Então cada Novo Jogo **é uma dimensão** do Tecido, e cada jogador é a nona vida do seu próprio mundo. As duas premissas se completam:
- **"Joga aos 5, ajuda aos 15, entende aos 30"** é a premissa **do tempo**: o mesmo jogo atravessa uma vida.
- **"Cada pessoa joga um Gatoelho diferente"** é a premissa **do espaço**: o mesmo jogo é um mundo diferente para cada um.

---

## Parte 1 — A dimensão de cada jogador

### Uma dimensão = uma semente
- Ao criar um Novo Jogo, o jogo sorteia uma **semente** (um número). Tudo o que é variável naquela dimensão nasce dela, **sempre igual** para a mesma semente.
- **O nome da dimensão** é a semente escrita em **gatoelhês**: quatro ou cinco símbolos (pata, orelha, fio, lua...). Dá para falar em voz alta, anotar e compartilhar ("joga a dimensão Orelha-Lua-Fio-Pata, o Heitor dorme num lugar absurdo lá"), como as sementes de Minecraft.
- **Uma dimensão pesa o mesmo que um save:** a semente e a lista do que o jogador mudou nela. O resto é recalculado no próprio computador.

### O que é igual em todas as dimensões
**A história e as fases principais.** O arco, os personagens principais, as fases feitas à mão, os chefes, os finais. A qualidade de Hollow Knight está aqui, e ela não pode ser sorteada.

### O que muda de dimensão para dimensão
| O que | Como varia | Por que importa |
|---|---|---|
| **O Gatoelho** | Pelagem (tigrado, malhado, frajola, siamês, rajado, mil combinações de cor), cor dos olhos, **qual orelha é torta**, formato e mancha do rabo, tamanho das orelhas, o jeito de ficar parado (um lambe a pata, outro persegue o rabo, outro boceja) | **Cada pessoa joga um Gatoelho diferente.** |
| **O Bigodes** | **É a versão velha e desbotada do Gatoelho daquela dimensão**: mesmas manchas, mesma orelha torta | A revelação na poça é **pessoal**: o vilão de cada jogador é o próprio Gatoelho dele envelhecido |
| **O Reflexo** | As cores do lenço dele são as que o jogador vai escolher no Fio Vermelho | Fecha o laço: o ajudante sempre teve as suas cores |
| **A população embaralhada** | Os inimigos comuns e os bichos de fundo são montados pelo **Gerador de Híbridos** (Parte 2): cada dimensão tem a sua fauna | O bestiário de cada um é diferente |
| **Os detalhes do cenário** | Flores, cogumelos, ruínas de fundo, objetos nos cantinhos de cochilo, a estampa das xícaras da Vó, o desenho da colcha, a posição das estrelas da constelação | O mundo parece vivido, e não cópia |
| **O Heitor** | Onde ele dorme no mapa e nas fases | Ninguém acha o Heitor no mesmo lugar que o amigo |
| **As fases secretas** | As camadas do Avesso (Parte 3) | O infinito |
| **A história da dimensão** | O que aconteceu naquele mundo depois do Clarão, contado nos recortes de jornal | Cada dimensão tem a sua crônica |
| **Os achados** | Os itens que chegam pelas fendas (Parte 5) | A caça |
| **A cantiga** | A melodia é sempre a mesma; os enfeites e o instrumento mudam | A criança reconhece a cantiga em qualquer dimensão |

### O Novo Jogo na história
- Começar um Novo Jogo **não apaga** a dimensão antiga: ela continua existindo, na lista de saves, como mais um fio na urdidura.
- **O Final da Corrente** (ligar a máquina) faz o Clarão cair **numa outra dimensão do próprio jogador**, se ele tiver mais de uma: ele vê, de fora, o começo da outra aventura dele. Quem tem uma só vê uma dimensão sorteada.

---

## Parte 2 — O Gerador de Híbridos
**A tecnologia que mais combina com o jogo**: um mundo de bichos misturados pede um sistema que mistura bichos.
- **Um catálogo de "metades"** desenhadas à mão: cabeças, troncos, patas, rabos, asas, cascos, bicos de umas 60 a 100 espécies. Cada metade traz **um comportamento** (o casco protege, a asa plana, a tromba borrifa, a pata de canguru pula).
- **O gerador junta duas metades** e monta:
  - **o corpo** (a parte da frente de um, a de trás de outro, com pontos de encaixe padronizados);
  - **o comportamento** (os módulos das duas metades combinados);
  - **o nome**, por uma regra de juntar palavras em português ("lobo" + "ovelha" → Lobovelha; "pato" + "tatu" → Patatu), com uma lista de exceções feita à mão para os nomes que soam mal;
  - **a página do caderno**: o desenho do Gatoelho na frente e uma anotação do Bigodes no verso, montada com frases-modelo.
- **Os personagens principais são feitos à mão**, não gerados. O gerador cuida da **multidão**: inimigos comuns, bichos de fundo, guardiões das camadas do Avesso, a população de cada dimensão.
- **Com 80 metades, são mais de 6 mil combinações.** O bestiário de uma vida inteira.
- **Regra de qualidade:** nenhuma combinação entra no jogo sem passar por um filtro (encaixes que funcionam, comportamentos que não se anulam). O robô de simulação testa cada híbrido gerado.

---

## Parte 3 — O Avesso: as camadas infinitas de fases secretas

### O que é
**O avesso do Tecido**, o lado de baixo do mundo, onde vive a Traça. É ali que ficam as camadas de fases secretas, uma embaixo da outra, **sem fundo conhecido**.

### Como se entra
- A primeira porta para o Avesso fica escondida no próprio jogo (um buraco de Traça numa fase do Arrepio). Cada camada vencida abre a seguinte.
- Camadas mais fundas só se abrem com **Fios de Reflexo**, ganhos ajudando outros jogadores (Parte 4).

### Como as camadas são feitas (o infinito sem perder qualidade)
- Cada camada é **montada a partir de salas feitas à mão**, centenas delas, desenhadas no padrão das fases principais, como em Spelunky e Dead Cells.
- A semente da dimensão e o número da camada decidem **quais salas, em que ordem, com que lei da física trocada** (gravidade, água para cima, luz invertida, tempo lento) e com que **tema** (cada camada pega o mundo de uma das nove vidas: o mar da Navegante, as engrenagens do Relojoeiro, as hortas da Jardineira, os espelhos do Rei, as teias da Fiandeira...).
- Cada camada termina num **guardião**, um híbrido gerado (Parte 2) com padrão de luta montado a partir dos comportamentos das metades.
- A cada camada, a mistura fica mais estranha: no começo, híbridos de dois bichos; mais fundo, de três; muito fundo, coisas que ninguém sabe o que são.
- O robô de simulação verifica que toda camada gerada **tem saída**.

### O que se encontra no Avesso
- **Achados** raros (Parte 5) e **recortes de jornal** (ver [[Jornal do Gatoelho]]).
- **Pedaços de lenda** sobre as nove vidas.
- **Ninhos de mariposa**: quanto mais fundo, mais perto do ninho da Traça.
- **Marcos de profundidade** feitos à mão, nos números redondos, como o caule do Feijão:
  - **Camada 9:** uma estátua de cada uma das nove vidas.
  - **Camada 99:** a gaveta de onde a Traça saiu (ver [[Lendas do Gatoelho]]).
  - **Camada 999:** um banquinho com duas xícaras.
  - **Camada 4.096:** o número do Bigodes. Lá está **a estátua da Primeira Vida, a Sem Rosto**. Quem chega vê que o rosto dela é **um espelho**: o jogador vê o próprio Gatoelho. **A Corrente não tem começo, e cada um é a primeira vida de si mesmo.** É a meta de uma vida inteira, e uma conquista que quase ninguém vai ter.

---

## Parte 4 — O Modo Reflexo em rede e as missões escondidas

### Abrir a dimensão para a rede
- Uma dimensão nasce **sozinha**: pesa só o save, sem servidor nenhum.
- Quando o jogador quiser, **põe a xícara de chá na janela** e a dimensão fica **aberta para a rede**: Reflexos de outras pessoas podem entrar nela.
- Do outro lado, quem já chegou ao Final do Fio Vermelho atravessa a **porta para o outro lado do rio** e cai, aleatoriamente, numa dimensão aberta.

### As missões do Reflexo (escondidas)
**O sistema de missões não é anunciado.** O Reflexo entra no jogo de alguém para ajudar, como sempre. Mas quem presta atenção repara que, na dimensão do outro, há **nós vermelhos** amarrados em lugares estranhos: num galho, no rabo de um passarato, na antena de um terminal. **Desatar um nó é uma missão.** Ninguém explica isso: descobrir é a primeira missão.

**Tipos de nó (gerados a partir do estado da dimensão de quem está jogando):**
| Nó | A missão |
|---|---|
| **Nó do caminho** | O jogador está preso no mesmo trecho há muito tempo. Ajudá-lo a passar, sem aparecer |
| **Nó do Heitor** | Fazer o jogador achar o Heitor (cutucando-o para um lugar visível) |
| **Nó da Vó** | O jogador passou por um banquinho de chá sem sentar. Fazê-lo voltar e esperar |
| **Nó do segredo** | Há um segredo perto e o jogador nunca o achou. Levá-lo até lá |
| **Nó do recorte** | Um recorte de jornal voou para um lugar alto. Soprá-lo até o jogador |
| **Nó do medo** | O jogador caiu muitas vezes num lugar. Segurá-lo na próxima queda |
| **Nó do achado** | Deixar um achado da sua própria coleção na janela do outro (um presente) |

**O que o Reflexo ganha:** cada nó desatado vira um **Fio de Reflexo**, com as cores do lenço de quem foi ajudado.
- Os fios entram na **colcha** da toca do Reflexo (um retalho por pessoa ajudada).
- **Fios tecidos juntos viram Chaves do Avesso**, que abrem as camadas mais fundas na dimensão do próprio Reflexo.
- Certos padrões de fios (ajudar nove crianças diferentes, desatar um nó de cada tipo) abrem **fases secretas feitas à mão** que só existem para quem ajudou.

**O que quem foi ajudado ganha:** a xícara lavada, de boca para baixo; um lenço novo no varal com as cores do Reflexo; às vezes um achado na janela. **Nunca um nome.**

**A regra de ouro:** a ajuda **nunca** tira o mérito de quem joga. As missões recompensam ajudar alguém a conseguir, nunca conseguir por ele.

### Os dois lados da rede
| | **Quem joga (Gatoelho)** | **Quem ajuda (Reflexo)** |
|---|---|---|
| Precisa de | Abrir a xícara na janela (qualquer modo, qualquer idade) | Ter chegado ao Final do Fio Vermelho |
| Faz | Joga normalmente | Gestos limitados, missões de nó |
| Vê | O mundo um pouco mais gentil | A dimensão do outro, com a fauna e o Gatoelho dele |
| Ganha | Lenços, xícaras, achados | Fios, retalhos, Chaves do Avesso, fases secretas |
| Fala | Nada | Só o ronrom |

### Por que isso não pesa em servidor
- **O conteúdo nunca viaja**: quem entra recebe só a **semente** e a lista curta de mudanças da dimensão, e monta o mundo no próprio computador.
- **Durante a visita**, só viajam **as entradas** de cada um (os botões de quem joga, os gestos de quem ajuda). O jogo de quem está jogando manda: ele roda a simulação, e o Reflexo vê uma cópia.
- **A conexão pode passar pela Steam** (salas de jogo e o retransmissor de rede que a Steam oferece de graça aos jogos dela). Para o começo, nenhum servidor próprio.
- **Um servidor mínimo, opcional**, só para coisas globais: contar quantos nós foram desatados no mundo, a "fome" global da Traça (Parte 6), o jornal da semana.
- **O que a engenharia precisa garantir desde já:** a simulação **determinística** (a mesma semente e as mesmas entradas dão o mesmo resultado). É o mesmo requisito da volta no tempo. **Uma decisão de motor serve às duas coisas.**

---

## Parte 5 — Os achados (a caça quase infinita)

### O que são
Objetos que **chegam pelas fendas**, vindos de outras dimensões: perdidos por alguém em algum mundo, levados pela corrente do Tecido. Aparecem escondidos nas fases, no Avesso, nas missões do Reflexo e nas janelas.

### Como são montados
Cada achado é a soma de partes, e cada parte conta um pedaço de história:
- **Um objeto-base** (feito à mão, umas 150): xícara, botão, chave, dedal, carta, brinquedo, relógio, óculos, figurinha, concha, moeda, retrato, carretel...
- **Um material** (cerca de 30): de lã, de vidro de espelho, de casco, de engrenagem, de vagem, de luar...
- **Uma origem**: uma das nove vidas, uma dimensão de outro jogador, ou o próprio Avesso.
- **Uma marca**: rachado, remendado, com dentinhos de Traça, com iniciais em gatoelhês, ainda morno.
- **Uma frase**: uma linha de história montada com frases-modelo e pedaços escritos à mão, assinada pelo Bigodes no caderno: *"Dedal de casco da Jardineira, com dentinhos de Traça. Alguém costurou até o fim."*

São **dezenas de milhares** de achados possíveis, cada um com uma frase. Uns poucos, **feitos à mão e raríssimos**, contam pedaços importantes da lenda.

### Onde ficam
- No **Gabinete da Tia Toupaca**: um museu de curiosidades em Tocópolis, onde a Tia "vê" os achados pelo cheiro. Cada achado tem um lugar na prateleira, e as prateleiras não têm fim.
- Alguns viram **broches** (com efeito) ou **peças do guarda-roupa**.
- Podem ser **dados de presente** na janela de outro jogador, pelo Modo Reflexo. **Não há troca nem venda**: só presente. Uma economia de carinho, e não de mercado.

---

## Parte 6 — Uma vida inteira sem esteira

### O pedido e a crítica
O Rodrigo quer mundos que exijam um **farm infinito** para se abrir, de modo que uma pessoa tenha **uma conta a vida toda** para conseguir explorar o jogo.

**A crítica honesta:** repetição infinita é exatamente o pecado do vilão (4.096 tentativas, a roda do Tubaramster) e o contrário da lição do Heitor. Um jogo que pregue "não dá para voltar, dá para tecer" e obrigue o jogador a repetir a mesma coisa para avançar contradiz a si mesmo, e afasta a criança e o case. **Mas o desejo por trás é ótimo:** uma conta para a vida inteira, um mundo que nunca se esgota.

### A proposta: cultivar em vez de repetir
"Farm", no Gatoelho, é **fazenda de verdade**: horta, tempo, cuidado. Os mundos de longa vida se abrem com coisas que **crescem**, não com coisas que **se repetem**:
| Chave de longa vida | Como se ganha | Tempo típico |
|---|---|---|
| **A horta da toca** | Feijões do Heitor, sementes de cenoura roxa do Coelhato e sementes achadas crescem em **dias reais** e mudam de estação | Semanas a anos |
| **A mudinha do Heitor** | Cresce em dias reais até virar árvore. Uma árvore adulta abre um caminho | Meses |
| **A Cápsula do Tempo** | O save "acordado" depois de muito tempo abre coisas que um save novo não abre | Anos |
| **A colcha** | Cada pessoa ajudada no Modo Reflexo é um retalho. Colchas grandes abrem portas no Avesso | Uma vida de ajuda |
| **A profundidade do Avesso** | Cada camada é nova (gerada), nunca repetida | Infinito |
| **O jornal** | Uma edição nova por semana real | Para sempre |
| **As estações e datas reais** | Coisas que só acontecem num mês do ano | Anos |
| **O caderno** | Completar o bestiário de híbridos da dimensão | Uma vida |

**A regra:** **nenhuma porta se abre com repetir a mesma coisa.** Só com coisas novas, tempo real ou ajuda a outras pessoas. Quem tem pressa não vai ver tudo; quem tem paciência, sim. **É o Heitor como regra de design.**

### E a Traça como guarda dessa regra
Quem tenta "forçar" o jogo voltando no tempo para repetir e farmar alimenta a Traça. Ela aparece e come os achados mal ganhos. **O jogo inteiro desencoraja a esteira com a própria história.**

### A Traça do Tecido (evento global, futuro)
Com o servidor mínimo, a Traça pode ser **uma só para todas as dimensões**: cresce com as voltas no tempo de todos os jogadores do mundo e encolhe com cada nó desatado por um Reflexo. Uma vez por ano, se ela estiver grande demais, abre-se um evento: a **Noite da Traça**, em que todos os Reflexos do mundo são chamados para ajudar. **A comunidade inteira contra o passado que não larga.**

---

## Parte 7 — Histórias paralelas (os spin-offs)

### Dentro do jogo: a crônica de cada dimensão
- Cada dimensão gera uma **crônica**: quem é o prefeito de Telhadópolis naquela dimensão, que guerra boba aconteceu entre dois formigueiros, que híbrido ficou famoso, que invenção deu errado.
- Ela é contada aos pedaços, **pelos recortes de jornal** e por **pequenas missões de fundo** que só existem naquela dimensão (ajudar o prefeito Vacaré a achar o chapéu, desfazer a confusão das eleições do Formigueiro).
- Montada a partir de **arcos-modelo** escritos à mão (umas 50 histórias curtas com papéis vazios), que o gerador preenche com os híbridos e lugares da dimensão.

### Fora do jogo: os spin-offs de verdade
O universo é grande o bastante para jogos derivados, todos usando a **mesma conta e a mesma dimensão** (o seu Gatoelho, com a pelagem dele, em outro jogo):
- **Gatoelho Kart** (corridas com os chefes; o Cavalesma sempre perde, e ganha um prêmio de consolação);
- **Gatoelho Party** (os minigames do Quintal da Toca, para festa);
- **Nove Vidas** (um jogo sobre uma das vidas anteriores; a Navegante é a candidata natural).

Visão de longo prazo, **sem contaminar o escopo** do jogo principal.

---

## Parte 8 — Os pilares de jogabilidade
**Pedido do Rodrigo: a jogabilidade tem que ser incrível.** Tudo o que está nesta bíblia é inútil se não for gostoso apertar o botão. Os pilares:
1. **Dez minutos numa sala vazia têm que ser divertidos.** Só correr, pular, planar, quicar, rolar e voltar no tempo, sem objetivo. Se isso não diverte, nada diverte. (É o teste de Super Mario 64 e de Celeste.)
2. **Precisão de Hollow Knight:** resposta no mesmo quadro, pulo de altura variável, coyote time, buffer de pulo, gravidade de queda maior que a de subida, nenhum controle "escorregadio" sem querer. (Muito disso já existe no protótipo.)
3. **Gato + coelho no corpo:** o coelho dá os pulos, o impulso e o planar com as orelhas; o gato dá as garras, a escalada, o encolher-se em lugares pequenos, a aterrissagem perfeita. **Toda habilidade tem que parecer coisa de bicho, não de super-herói.**
4. **Luta sem morte, mas com profundidade:** pisão, garras como ferramenta, ronrom para acalmar, Ecos, Soneca. Cada chefe é um quebra-cabeça de movimento com personalidade, legível como os de Hollow Knight.
5. **Fácil de começar, sem teto para dominar:** a criança termina; o speedrunner acha atalhos com Ecos, quicadas e voltas no tempo que nem o Rodrigo previu.
6. **Sensação ("game feel"):** pequenas pausas no impacto, o boneco esticando e achatando, poeirinha, som para cada superfície, a câmera que antecipa o movimento, as orelhas e o rabo sempre reagindo.
7. **Fases de Hollow Knight, mas fases:** cada fase cheia de caminhos, atalhos que se abrem por dentro, segredos que pedem habilidades novas e saídas secretas, e cada mundo **interligado por dentro** (decisão do Rodrigo: manter fases).
8. **O robô de simulação mede a diversão possível:** além de testar se dá para passar, mede os "momentos": quantos pulos justos, quantas escolhas de caminho, quanto tempo sem nada para fazer.

---

## Parte 9 — A trama infinita revista pela Camada Zero (Revisão 9)
Com a [[Camada Zero do Gatoelho]] (a Terra depois do fim da humanidade, a Arca das Máquinas, as nove redomas, a casa da Vó de Todas), **nada do que está acima muda** (decisão do Rodrigo). Mas a trama infinita fica muito mais forte, porque agora **todo sistema infinito tem uma razão dentro do mundo**, e a razão gera mecânicas novas.

### 9.1 — Cada sistema infinito tem uma origem
| Sistema | O que o jogador vê | O que é, na Camada Zero | O que isso acrescenta |
|---|---|---|---|
| **A semente da dimensão** | Um nome em gatoelhês | Uma **execução da Arca** (uma das trilhões que as Máquinas simulam, ou a redoma física) | A pergunta "esta é a de verdade?" nunca se responde |
| **O Gerador de Híbridos** | Bichos novos em cada dimensão | **O Catálogo de Metades**, o banco genético da Arca | Vira um lugar: **o Fichário**, um arquivo de gavetas sem fim no subsolo de Tocópolis, com uma ficha para cada metade de bicho. O caderno do Bigodes copia as fichas |
| **O Avesso** | Camadas secretas infinitas | **O arquivo das Máquinas**: memória empilhada, cada camada mais antiga | As camadas ganham uma ordem com sentido (9.3) |
| **Os nós vermelhos** | Missões escondidas do Reflexo | **Chamados de manutenção**: as Máquinas, presas à regra de não interferir, abrem chamados que só os que já saíram podem atender | As missões ganham famílias novas (9.4) |
| **Os achados** | Objetos que chegam pelas fendas | Coisas de outras redomas, do arquivo e, raríssimas, **da casa e do tempo dos humanos** | Uma camada nova de achados (9.6) |
| **O jornal** | O Novelo | **A Rotativa**, a máquina de notícias humana que imprime sozinha | A sátira repete a história humana porque **é** a história humana |
| **A Traça** | O luto que ninguém terminou de tecer | Também **a corrupção do arquivo** (o *bug*) | A Traça global vira manutenção coletiva |
| **As dimensões dos outros** | O Modo Reflexo online | Outras execuções; quem ajuda é quem já saiu | Exatamente o que o Reflexo faz na história |

### 9.2 — O mundo continua vivo enquanto o jogador está fora: as gerações
**O motor mais forte para uma vida inteira.** A Arca foi feita para a vida **continuar se misturando sozinha**, e na dimensão de cada jogador ela continua:
- **Os bichos da dimensão têm filhotes**, em **semanas reais**. Cada filhote junta metades dos pais (o Gerador de Híbridos, agora com herança): um filho do Vacaré com a Raposinha pode nascer com focinho de jacaré e penas de galinha.
- **Novas espécies aparecem** na dimensão de cada jogador e em nenhuma outra. O caderno ganha **árvores genealógicas**.
- **Quem volta depois de um ano** encontra os **netos** dos bichos que conheceu: os filhotes do Lobovelha, um descendente do Tubaramster que nunca correu numa roda.
- **Nada disso pesa:** as gerações são calculadas pela **data** e pela **semente**, não simuladas o tempo todo. O jogo só calcula quando o jogador abre.
- **A tese em forma de sistema:** a mistura não é um acidente que se conserta; **é o que a vida faz, sozinha, para sempre.** O mundo do jogador vai ficando mais misturado e mais bonito a cada ano.
- Os **personagens principais não mudam** (a Vó, o Heitor, o Patatu continuam sendo eles). As gerações acontecem na multidão.

### 9.3 — O Avesso com ordem: as camadas são o passado empilhado
As camadas infinitas ganham uma ordem que conta a história de baixo para cima, **sem nunca dizer nada**:
| Camadas | O que são (Camada Zero) | O que o jogador sente |
|---|---|---|
| **1 a 99** | As **iterações anteriores da redoma 9**: o próprio mundo do jogador, antes | Lugares quase iguais aos dele, com pequenas diferenças. Às vezes, um Eco do próprio Gatoelho fazendo outra escolha. **Rastros do Reflexo**, um lenço de duas cores esquecido |
| **100 a 999** | **As outras redomas**: os mundos das nove vidas | O mar da Navegante, as engrenagens do Relojoeiro, a horta da Jardineira... e o jeito de cada vida ter recusado |
| **1.000 a 4.095** | **As execuções simuladas** | Mundos que poderiam ter sido: dimensões em que o Gatoelho é outra mistura, em que a Vó é outra coisa, em que o Clarão nunca veio |
| **4.096** | O marco | A estátua da Primeira Vida, com o espelho no lugar do rosto |
| **Além de 4.096** | **Cada vez mais perto do tempo dos humanos** | O jogo não acaba. As camadas ficam mais antigas, mais silenciosas, e as coisas vão ficando **grandes demais para bichos**: uma maçaneta do tamanho de uma porta, um botão do tamanho de uma roda. Ninguém explica |

**E, com amigos:** as camadas 1.000 a 4.095 podem puxar **as sementes das dimensões dos amigos** (pela lista de amigos da Steam, sem servidor). Descer no Avesso pode ser visitar, em ruínas, um mundo que o seu amigo está jogando agora.

### 9.4 — As missões do Reflexo ganham famílias novas
Além dos nós da Revisão 8, os chamados das Máquinas trazem:
| Família | A missão | Por que existe (Camada Zero) |
|---|---|---|
| **Nó do Arquivo** | Na dimensão de outra pessoa, consertar uma camada do Avesso corrompida (acalmar mariposinhas) | A Traça global é corrupção do arquivo; os Reflexos fazem a manutenção |
| **Nó da Saudade** | Fazer o jogador de outra dimensão assistir a um Eco Antigo que ele nunca viu | O arquivo quer ser lembrado |
| **Nó do Mastro** | Ajudar alguém a acalmar uma antena | Os mastros foram feitos para chamar. Cada um acalmado é um mastro a menos fazendo o trabalho errado |
| **Nó da Porta** | Fazer alguém que está sozinho há muito tempo achar o Heitor, o Patatu, a Vó | **Ninguém sai sozinho** |

**A frase da Vó (o mistério coletivo):**
- Sempre que a Vó Tartuja começa uma frase sobre "como era antes", dorme no meio. A frase tem **um número fixo de palavras**, igual para todo mundo.
- Cada **Nó da Saudade** desatado revela, **na colcha de quem ajudou**, bordada num retalho, **uma palavra** da frase, sorteada.
- Ninguém consegue todas sozinho. **A comunidade inteira**, juntando o que cada um bordou, monta a frase da Vó. É um mistério feito para ser resolvido junto, como os enigmas de Fez.
- A frase é a coisa mais próxima de uma revelação que o primeiro jogo tem. **Quem escreve é o Rodrigo**, e ela não pode dizer "humano" (regra da Camada Zero). Um exemplo do tom: *"Antes, eles cantavam para a gente dormir, e depois foram embora cantando."*

### 9.5 — As Noites de Contato (eventos sem servidor)
- Em **nove noites por ano**, em datas fixas do calendário real, **a Arca passa mais perto**. Em todas as dimensões ao mesmo tempo, sem servidor nenhum (basta a data):
  - a **lua dupla** aparece no céu, e não só na água;
  - os **mastros** acalmados zumbem baixinho;
  - os **terminais** recebem um comentário `~` novo, diferente a cada ano;
  - o **Heitor** fala dormindo (roncos em gatoelhês mais longos);
  - algumas portas do Avesso, que só existem nessas noites, se abrem.
- Para a criança: noites mágicas em que o céu fica diferente. Para quem sabe: uma estação passando em órbita.
- Para o case: **o dia em que todo mundo entra ao mesmo tempo para ver a lua dupla.**

### 9.6 — Os achados ganham fundo
| Camada | Quantos | O que são | Onde aparecem |
|---|---|---|---|
| **Comuns** | Dezenas de milhares (gerados) | Objetos de outras execuções | Fases, Avesso raso, janelas |
| **Das Nove Vidas** | Algumas centenas (gerados com base feita à mão) | Objetos das outras redomas: uma bússola da Navegante, uma engrenagem do Relojoeiro | Avesso 100 a 999, Ilha |
| **Relíquias da Casa** | Cerca de 99 (feitos à mão) | Objetos da **casa da Vó de Todas**, em tamanho de gente: um dedal enorme, um óculos, uma chave, uma foto de um gato e um coelho dormindo juntos numa almofada | Avesso fundo, Noites de Contato, nós raros |
| **Páginas do Diário** | Cerca de 40 (escritas pelo Rodrigo) | **O diário da Vó de Todas**, em português, letra tremida: o gato, o coelho, a tartaruga, o chá, a cantiga, a colcha, "os que vão partir". **Nunca diz "humano" nem "máquina".** Juntas, contam o fim de uma vida e o começo de outra | As mais fundas do Avesso; algumas só na comunidade |

### 9.7 — A horta é o banco de sementes da Arca
- As sementes que o jogador planta na horta (feijões do Heitor, cenouras roxas do Coelhato, sementes achadas) vêm, na Camada Zero, do **banco de sementes da Arca**: plantas guardadas para depois do fim.
- A horta ganha **sementes raras**, achadas no Avesso e nas Noites de Contato, que crescem em **meses reais** e viram plantas que só existem naquela dimensão.
- É a melhor resposta ao "farm infinito" do Rodrigo: **farm de verdade**, de plantar e esperar, com sentido na história (a Arca foi feita para a vida crescer de novo).

### 9.8 — O pedido de ajuda, plantado desde o primeiro jogo
O fim da série é o Gatoelho **pedir ajuda**. O primeiro jogo já planta isso, escondido:
- Na linguagem Novelo existe uma função que **ninguém ensina**: `chamar()`. Digitada em qualquer terminal, responde: `sem sinal`.
- Depois que os quatro mastros (as antenas) foram acalmados, no terminal do Pico ela responde outra coisa: `sinal fraco. aguardando.`
- Em cada Noite de Contato, se alguém chamar, a resposta muda um pouco: `recebido.`, `quem é?`, `bata de novo.`
- **Nada acontece no primeiro jogo.** Mas o save guarda quantas vezes o jogador chamou. **No último jogo da série, as Máquinas lembram.**
- **Com o servidor mínimo (futuro):** um contador global de quantas vezes **o mundo inteiro** chamou. A Porta do Céu, no último jogo, pode se abrir **quando a comunidade tiver chamado o bastante**: os jogadores pedindo ajuda juntos, como os bichos nunca fizeram.

### 9.9 — O correio entre dimensões
O **Pinguinguru** passa a levar coisas **entre dimensões de amigos**, sem nenhum texto:
- um **achado** embrulhado;
- uma **foto** do Gatoelho (com a roupa);
- uma **semente** da horta;
- um **retalho** da colcha.
Chega na janela do outro, com o selo da pata do Gatoelho de quem mandou. **Uma rede social sem palavras**, segura para crianças, em que só se pode dar.

### 9.10 — O save atravessa a série
- A dimensão do jogador (a semente, o Gatoelho dele, as gerações, a horta, a colcha, os achados, a Cápsula do Tempo, as chamadas) **continua nos próximos jogos**.
- O jogador de 5 anos que plantou um feijão no primeiro jogo vai encontrar, no último, aos 25, **a árvore**.

### 9.11 — Por que tudo isso continua leve
Nenhum item acima precisa de servidor para existir: **a semente, a data e o save** bastam para as gerações, as Noites de Contato, o Avesso, os achados e o jornal. A Steam cobre a rede entre amigos. Um servidor mínimo, só no futuro, serve para o que é **global de verdade**: a Traça do Tecido, a frase da Vó coletiva, o contador de chamados.

## Alertas de escopo
1. **Isto é visão de longo prazo.** O primeiro lançamento é o Ronrom (Atos I a III). O Tecido Infinito vem em camadas: primeiro **a semente** (o seu Gatoelho diferente, a fauna, os detalhes), depois **o Avesso**, depois **a rede**.
2. **O que precisa entrar no motor já:** simulação **determinística** e **sementes**. Servem à volta no tempo, aos Ecos, à geração e à rede. Adiar isso custa caro depois.
3. **Gerado não é igual a bom.** O infinito só funciona sobre peças feitas à mão com muito cuidado (salas, metades de bichos, objetos, frases). A regra: **a máquina combina, as pessoas criam.**
4. **Rede com crianças exige cuidado de segurança** acima de tudo: sem texto, sem nome, sem voz, gestos limitados, saída imediata. O desenho acima já parte disso.

## Decisões do Rodrigo (2026-10-05, sobre a Revisão 7)
1. **O plano de amor torto do Bigodes e a profecia lida no reflexo entram.**
2. **A Traça precisa ser mais desenvolvida** (feito em [[Lendas do Gatoelho]]).
3. **O Patatu re-embaralhado:** decidir depois.
4. **Manter as fases.** "Um Hollow Knight de fases, com possibilidades infinitas."
5. **Pedidos novos:** jogar a vida inteira; mundos que exigem um farm muito longo para se abrir; geração aleatória de detalhes de cenário e de histórias paralelas; missões escondidas no Modo Reflexo que liberam fases secretas; camadas de fases secretas que pareçam infinitas; **cada pessoa joga um Gatoelho diferente**; uma dimensão por Novo Jogo, pesando como um save, que pode ser aberta para a rede entre Gatoelho e Reflexo; caça quase infinita de itens; recortes de jornal infinitos com ironia sobre o pior da humanidade, de um ponto de vista filosófico, histórico e democrático, um pouco mais à esquerda; jogabilidade incrível.

## Perguntas em aberto
1. **Cultivar em vez de repetir:** a troca do "farm infinito" por tempo real, cultivo, ajuda e profundidade serve?
2. **A Camada 4.096** com o espelho da Primeira Vida, como a meta de uma vida inteira: entra?
3. **A Traça do Tecido** como evento global anual (futuro): entra?
4. **Achados sem troca nem venda**, só presente: de acordo?
