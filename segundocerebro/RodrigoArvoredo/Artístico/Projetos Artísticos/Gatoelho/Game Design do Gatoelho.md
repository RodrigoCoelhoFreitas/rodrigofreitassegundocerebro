---
tags: [projeto, jogo, game-design]
---

# Game Design do Gatoelho

Ramificação de [[Gatoelho]]. O que o jogo quer ser, o que já foi decidido e o que ainda está em aberto. Técnica em [[Arquitetura do Gatoelho]]; visual e som em [[Direção de Arte e Som do Gatoelho]].

## Como o Rodrigo quer trabalhar neste projeto
- Construir de forma **incremental e organizada**, decidindo antes de produzir. Começou pela pré-produção (sem código) e só depois partiu para protótipo.
- As ideias dele **não são ordens imutáveis**: o Claude deve apontar quando algo é ruim para game design, arquitetura ou performance, propor alternativas e **avisar quando o escopo cresce** — preservando a identidade do jogo.
- **"Uma fase excelente vale mais que vinte medianas."**

## Prioridades (na ordem do Rodrigo)
1. Gatoelho extremamente divertido de controlar.
2. Personalidade.
3. Animações que contribuem para a personalidade.
4. Fases legíveis e divertidas.
5. Exploração que recompensa curiosidade.
6. Direção artística consistente.
7. Crianças conseguem jogar.
8. Jogadores experientes encontram coisas interessantes.
9. Código organizado conforme cresce.
10. Quantidade de conteúdo depois da qualidade.

## Referências (o que observar, sem copiar)
- **Super Mario** — legibilidade das fases, exploração, segredos, precisão de plataforma. **Mapa do mundo do Super Mario World** virou o modelo de estrutura.
- **Sonic** — velocidade, momentum, momentos de fluxo.
- **Mega Man** — habilidades, inimigos, progressão, chefes. **Mega Man X** (voltar às fases antigas com habilidades novas para achar upgrades) é o modelo de revisita.
- **Metal Slug X** — personalidade das animações, humor visual, cenários vivos.

## O personagem
Pequeno aventureiro, muito ágil: curioso, alegre, energético, brincalhão, levemente arteiro, corajoso, **muito expressivo** — inclusive parado (orelhas e rabo como expressão corporal). Visual atual do conceito: pelo laranja com áreas claras, olhos verdes grandes, orelhas enormes de coelho, rabo felino grande, patas expressivas, garrinhas, **lenço vermelho** e **mochila verde**.

Gato + coelho deve virar **gameplay**, não só estética. Coelho: saltos altos, salto duplo, impulso das patas traseiras, velocidade, orelhas para planar. Gato: garras, ataques rápidos, escalar/agarrar parede, salto de parede, aterrissagens, entrar em lugares pequenos, esconder-se.

## Estrutura do jogo (decidida em 2026-09-29)
- **Mapa do mundo visto de cima, estilo Super Mario World**: o Gatoelho anda entre as fases pelos caminhos, entra numa fase ao confirmar/clicar, e **o próprio mapa também terá segredos** (caminhos escondidos).
- **O Gatoelho ganha muitas e muitas mecânicas com o tempo**; por isso começamos pelas mais básicas. Com mecânicas novas, ele **volta às fases antigas e encontra segredos e recursos secretos** (modelo Mega Man X).
- Visão inicial de escopo do jogo completo: **5 mundos × (4 fases + 1 chefe) ≈ 25 fases** — referência, não compromisso. Começar pelo contrário: um trecho pequeno com qualidade muito alta (vertical slice no Bosque das Cenouras).
- Dois níveis naturais em cada fase: **terminar** (acessível, uma criança consegue) e **completar 100%** (exploração, domínio das habilidades, segredos).
- Metroidvania puro foi discutido: combina com o personagem (habilidades como chaves, Instinto Felino), mas criança se perde fácil e o design fica interdependente. O caminho escolhido (mapa + fases + revisita) pega o melhor dos dois.

## Mecânicas já implementadas (protótipo)
- **Andar** com aceleração, freada e virada rápida (velocidade máx. 260 px/s).
- **Pulo** com altura variável (136 px segurando; ~53 px num toque), queda mais rápida que a subida, **coyote time** 0,1 s e **jump buffer** 0,12 s.
- **Pulo duplo** (+96 px) — pedido do Rodrigo, mesmo com o alerta de que pulo duplo e planar resolvem problemas parecidos.
- **Planar com as orelhas**: segurar o botão depois de qualquer pulo (inclusive o do chão — decisão do Rodrigo) abre as orelhas quando começa a cair. Pousar segurando e sair andando de uma beirada **não** plana.
- Pulo duplo e planar são **ligáveis/desligáveis** (teclas 1/2 em desenvolvimento) — base do futuro sistema de habilidades conquistadas.
- **Energia contínua**: 300 pontos = 3 corações (100 por coração); espinhos tiram 50 (meio coração) + empurrão + 1,2 s de invulnerabilidade piscando.
- **Vidas**: 3. Acabou a energia → perde uma vida e volta ao início da fase. **Buraco tira todos os corações** (decisão do Rodrigo; a proposta anterior era perder um pouco e voltar à beirada). Sem vidas → recomeça a fase com vidas cheias, **sem tela punitiva de game over**.
- **Bandeira de chegada**: a coluna inteira do mastro conta (senão dava para passar planando por cima sem terminar a fase). Resultado mostra tempo, vidas e recorde.
- **Mapa do Mundo 1** com 5 pontos; só a Fase 1 começa liberada; concluir uma fase revela o caminho seguinte.

## Ideias em estudo (não decididas)
- **Instinto Felino** — perceber pegadas, passagens, objetos enterrados, plataformas ocultas, inimigos camuflados. Proposta do Claude: em vez de botão (que vira obrigação de ficar ligando), **o Gatoelho percebe sozinho** — orelhas giram para o segredo, rabo arrepia, ele encara uma parede suspeita quando parado. Une personalidade e sistema.
- **Caixas** ("gato adora caixa") — a ideia de maior identidade depois do movimento: esconderijo, passagem, objeto empurrável, entrada secreta, transporte, piada recorrente.
- **Ataque**: proposta de o ataque principal ser **pisão com as patas traseiras** (coelho; acessível como o do Mario) e garras como secundário/ferramenta.
- **Agarrar parede + salto de parede** (a parede alta da sala de testes já está lá esperando). Escalada livre e **nadar/mergulhar** ficam fora por enquanto (caros e pouco divertidos na maioria dos jogos).
- **Colecionáveis** — proposta de reduzir para três: **cenouras** (comuns, guiam o caminho), **Cenoura Dourada** (3 por fase, o "100%") e **corações**. Novelos, estrelas, mapas e chaves só entram se um problema de design pedir.
- **Power-ups** — nenhum no vertical slice; depois decidir entre temporário (Mario) e habilidade permanente (Mega Man), sem misturar sem motivo.
- **Mundos** (provisórios): Bosque das Cenouras (primeiro), Telhadópolis (telhados, verticalidade felina), Tocópolis (subterrâneo, segredos), Monte Ronrom (vulcânico), Ilha das Nove Vidas (misteriosa, mitologia).
- **Inimigos** — projetar pela **função** primeiro ("que comportamento esta fase precisa?"), criatura depois. Nomes já brincados: Tatugo, Caracol, Ratenio, Passarato, Plantaruga, Cogumelo, Espinheto, Fantomau.
- **Chefes** (preliminares): Rei Caracólio, Dona Tronca, Robogato, Gatópora, Dr. Bigodes. Antagonista da primeira aventura ainda não definido.
- **Universo** de criaturas híbridas; spin-offs sonhados (Gatoelho Kart, Party, Nove Vidas) — só visão de longo prazo, sem contaminar o escopo atual.
- Nomes provisórios das fases do Mundo 1: 1 Sala de Testes, 2 Trilha das Cenouras, 3 Cachoeira Risonha, 4 Copas Altas, Toca do Chefe.

## Alertas de design registrados
- **Planar está forte demais**: anda 260 px/s caindo só 80 px/s (mais de 3 tiles para frente por tile de queda) — quase nenhum buraco vira desafio. Testar `glideFallSpeed` entre 120 e 150.
- Pulo duplo **e** planar no kit base reduzem os desafios possíveis; alternativa: planar como habilidade conquistada depois.
- **Buraco = uma vida** é punitivo para criança pequena — observar a enteada jogando.
- Na tela de título, as setas não funcionam enquanto o título ainda está caindo (só confirmar pula a animação) — pode confundir criança apertando tudo.
- A enteada deveria ser **testadora desde cedo**: "10 minutos numa sala cinza e se divertir" era o critério de sucesso do protótipo de movimento.

## Perguntas em aberto
- ~~Idade da enteada~~ — ainda não lê (2026-09-30). Falta saber se já joga algo (qual jogo, qual aparelho).
- **Dispositivo**: PC com teclado/controle ou tablet/celular com toque? (o alvo virou PC, mas toque mudaria o kit de movimentos).
- **Quem produz arte, animação e som**, e quanto tempo por semana o Rodrigo tem para o projeto.
- **Ordem das mecânicas** que o Gatoelho ganha e o que cada fase ensina — próxima conversa combinada.

## Atualização 2026-09-30 — a primeira fase e a progressão de habilidades

### Progressão de habilidades (decisão do Rodrigo)
O Gatoelho **começa só andando e pulando** e conquista as habilidades ao longo do jogo; elas ficam salvas e valem em todas as fases, inclusive nas já jogadas — é o que permite voltar e achar segredos. Primeira habilidade: **Orelhas Planadoras** (planar), ganha na Fase 1. O **pulo duplo saiu do kit inicial** e fica para uma fase futura. Escalar paredes já está prometido por um segredo da Fase 1.

### Fase 1 · "Saindo da Toca" (Bosque das Cenouras)
Pedido do Rodrigo: uma primeira fase com tema de saída de casa, intuitiva, que apresente conceitos do jogo e em que ele ganhe a habilidade de "voar com as orelhas" e precise dela. Desenhada no estilo "ensinar sem falar": cada ideia aparece num lugar seguro, depois é cobrada, depois combinada.
1. **A toca** — sai pela porta redonda de uma toca no morro; placa ensina a andar; cenouras mostram o caminho.
2. **Primeiros pulos** — tronco, degrau, vala rasa (cair não custa vida), galhos, um buraco pequeno, espinhos com espaço de sobra.
3. **Dente-de-leão Dourado** — no alto de um platô, com checkpoint antes; é impossível passar sem pegar. Anúncio "Nova habilidade: Orelhas Planadoras".
4. **Treino seguro** — vão impossível de pular; quem erra cai num chão seguro com degraus de volta.
5. **Buraco de verdade** — atravessado planando, com cenouras desenhando a trajetória; segundo checkpoint depois.
6. **Flores de vento** (a reviravolta) — planando sobre elas, o vento leva para cima; único jeito de subir o paredão; depois, longa descida planando até a bandeira.

### Mecânicas novas
- **Flor de vento**: coluna de ar de 11 tiles; só afeta quem está planando (orelhas abertas pegam o vento).
- **Galhos**: plataformas que se atravessam por baixo e seguram por cima.
- **Cenouras** (55 na fase, contador no HUD) e **Cenouras Douradas** (3 por fase, o "100%") — a proposta de colecionáveis virou decisão.
- **Checkpoints**: perder uma vida volta ao último.
- **Placas** com balão de dica ao chegar perto (5 na fase).

### Os três segredos da Fase 1 (a ideia de voltar às fases, já na primeira)
- Uma Dourada **visível**, que exige subir pelos galhos e pular do mais alto.
- Uma **flor de vento "adormecida" ao lado da toca**: na primeira passada não faz nada (ele ainda não plana); cenouras sobem pela coluna como pista. Quem volta planando sobe até uma ilha escondida.
- Uma no **topo de uma chaminé de pedra**, só alcançável escalando — a placa diz "volte quando souber escalar paredes". Ou seja: o 100% da Fase 1 só será possível quando essa habilidade existir.

### Regra de save (decidida em 2026-09-30)
**Só vale o que se conclui**, como em Super Mario World: habilidades e Cenouras Douradas pegas numa fase só entram no save ao chegar na bandeira; sair da fase descarta. Nasceu de um problema relatado pelo Rodrigo — na segunda partida o Gatoelho "já nascia com a habilidade", porque o progresso único gravava na hora do pickup. Alerta registrado: criança que pega uma Dourada difícil e sai da fase perde a cenoura; a alternativa "pegou, é seu" (só a habilidade presa à conclusão) é uma troca pequena.

### O que os testes ensinaram sobre level design
- Coluna de vento de 2 tiles é estreita demais: o embalo tira o personagem dela → 3 tiles.
- Galho de 4 tiles é curto demais: um pulo correndo passa por cima → 5–6 tiles.
- Posição de colecionável difícil se escolhe por **busca na física** (de onde alcança, de onde não alcança, onde o pulo termina), não no olho.
- Planar continua forte (alerta de ontem mantido); a fase foi desenhada em volta disso.

## Visão decidida em 2026-09-30 — um jogo em camadas
A enteada **ainda não lê**. Pedido do Rodrigo: o jogo tem que ser bonitinho, intuitivo e divertido para criança, com um **final possível dentro da inocência**, mas ter **camadas mais sérias, com conteúdo e lore para quem sabe ler**, a ponto de ser aclamado pela crítica adulta. Nas palavras dele: "um jogo histórico dentro da simplicidade".

Consequências:
- **Saber ler vira a chave da segunda camada.** A camada da criança não tem nenhum texto obrigatório; todo o texto é opcional e guarda a lore. O jogo "cresce junto com a criança": o que ela jogou aos 5 anos se revela aos 8.
- **Camadas**: 0 = criança sem ler (história contada só com imagens, final feliz completo); 1 = quem lê (cartas, descrições de itens, nomes com duplo sentido); 2 = quem investiga (segredos de conhecimento, idioma gatoelhês, final verdadeiro); 3 = comunidade (mistérios coletivos, estilo Fez/Animal Well — opcional, avaliar escopo).
- **Regra**: a camada adulta nunca estraga a infantil. Nada assustador visível para a criança; o sério mora no texto e em detalhes do cenário. O final da criança é verdadeiro, não um "final ruim"; o final verdadeiro dá um novo sentido a ele sem negá-lo.
- **As placas de texto das Fases 1 e 2 precisam virar pictogramas/demonstrações** (e o anúncio "Nova habilidade" precisa ser visual).
- Antes de espalhar pistas, escrever a **bíblia do mundo** (a verdade escondida), senão a lore fica incoerente.
- Referências da camada dupla: Kirby (lore cósmica escondida em texto de pausa), Pokémon (entradas da Pokédex), Pikmin (anotações sobre os tesouros), Tunic, Fez, Animal Well, Hollow Knight (lore contada pelo ambiente), Chicory, Ghibli, Bluey (camada para os pais).
- Candidatas a sacada (sessão de 2026-09-30, não decididas): **Nove Vidas** (fantasminhas das vidas perdidas viram ajuda/ponte; adulto usa de propósito), **jogo sem texto com o corpo do Gatoelho como interface** (virou praticamente obrigatório), **idioma gatoelhês**, co-op "de colo", cochilo (dia/noite).

## Decisões de 2026-09-30 — a assinatura do jogo
- **Fim de fase = cochilo**: a bandeira (herança do Mario) sai; o Gatoelho acha um lugar de sol e cochila, e o sonho faz a transição. Pesquisa em [[Pesquisa de Fases do Gatoelho]]. (Ainda não implementado.)
- **Re-embaralhamento temporário** adotado: pólens/ondas que mudam as regras da física, as cores e o comportamento dos objetos da fase.
- **Transformações por DNA** adotadas: o Gatoelho ganha por um tempo um pedaço de outro bicho (peixe nada, tatu rola, morcego pendura, vaga-lume ilumina).
- Arco principal em história curta: [[História e Mundos do Gatoelho]].

## Fases 1 e 2, versão 3 (2026-09-30) — identidade, camadas e o cochilo
Pedido do Rodrigo: implementar o cochilo e levar as duas fases "para outro nível de mecânica, beleza e conceito", com mais caminhos ocultos, vários níveis de enigma, pistas e símbolos escondidos. Método em [[Pesquisa de Fases do Gatoelho]].

### Sistemas novos
- **Cochilo no fim da fase**: a bandeira virou um **cantinho de sol** (raio de luz que desce do céu num tufo de musgo; dá para ver de longe). O Gatoelho anda sozinho até o meio, dá duas voltinhas e se enrola para dormir, com "z z z" e a tela esquentando; o resultado aparece depois. A saída secreta é um **raio de luar roxo**.
- **Placas sem texto**: cada placa mostra um desenho (Gatoelho em miniatura, setas, botão de pulo; anel em volta = segurar).
- **Re-embaralhamento temporário (pólen)**: flores de pólen misturam o Gatoelho com outro bicho por um tempo, com onda saindo dele, o mundo num véu de cor e grãos de pólen girando em volta (um grão a menos a cada oitavo do tempo; as cores piscam no fim).
  - **Flor-Pluma** (10 s): gravidade leve — pulos, quiques e cogumelos bem mais altos. Ganha uma pena na cabeça.
  - **Flor-Escama** (14 s): DNA de peixe — a água deixa de ser perigo e vira caminho; nada com braçadas (pulo), e o efeito não acaba enquanto ele está na água. Ganha barbatanas.
- **A Onda do Embaralhamento** (evento de história, sem texto): logo no primeiro passo da Fase 1 ela passa, o mundo pisca em outras cores e as cenouras da horta **ganham pernas e fogem** — correm pela trilha à frente dele (guiando a criança) e, encurraladas numa beirada, se encolhem tremendo e são pegas. Nunca se jogam em buraco, água ou espinho.
- **Gatoelhês**: quatro símbolos (1 pata, 2 orelha, 3 rabo, 4 bigode). Aparecem nas **flores-sino** (cada uma mostra o seu), no **mural** que dá a ordem delas, nas **pedras antigas** (lore sem função, por enquanto) e, bem apagada, uma orelha gravada perto de toda passagem secreta.
- **Flores-sino + raízes + Cenoura Roxa** (a camada mais funda): tocar as flores na ordem do mural abre as raízes de um morrinho; dentro, numa câmara escondida, está a **Cenoura Roxa** (uma por fase, salva ao concluir; aparece no resultado só depois de achada). Andando reto (1, 2, 3…) nunca se acerta; é preciso pular por cima das flores.
- **Luz de cada fase**: manhã (Fase 1), tarde dourada com a **antena do Embaralhamento** soltando ondas no horizonte (Fase 2), roxo (Horta Escondida). Grama, céu, sol e morros mudam juntos.

### Fase 1 "Saindo da Toca" — camadas
1. **Criança**: a Onda, as três fujonas guiando e sendo pegas, o caminho de sempre, as flores-sino tocadas de passagem, o cochilo.
2. **Quem sobe nos galhos**: a **Flor-Pluma** no galho baixo da Árvore Grande → galho do topo → **Ninho da Copa** (cenouras e pedra antiga). O pulo duplo (Fase 2) é a segunda chave da mesma porta.
3. **Quem explora**: a **gruta ao pé do paredão** (quem só cai do paredão, sem planar, pousa perto dela) guarda o **mural**: rabo, pata, orelha.
4. **Quem lê o mural**: as flores-sino da clareira, o **Morrinho das Raízes** e a **Cenoura Roxa**.
- Ajuste que o robô achou: quem saía correndo do alto do paredão caía em cima do espinheiral; ele foi afastado dois tiles.

### Fase 2 "Trilha das Cenouras" — camadas
1. **Criança**: pega a **Flor-Escama** no caminho sem querer (uma placa desenha "flor → nadar"), então cair no rio deixa de ser castigo por um tempo.
2. **Quem mergulha**: o rio agora é fundo e corre por baixo das pedras; uma trilha de cenouras no fundo aponta um **túnel alagado debaixo do Campo** que dá numa **gruta com ar**, com o mural: orelha, bigode, pata, rabo.
3. **Quem lê o mural**: quatro flores-sino na reta final, o morrinho das raízes e a Cenoura Roxa.

### Perguntas em aberto
- O cochilo agrada? (tempo até o resultado: ~1,6 s dormindo)
- Força das cores do pólen (foi suavizada depois do primeiro print: a primeira versão deixava o mundo rosa-choque).
- A pedra antiga do Ninho ainda não significa nada: decidir o que ela diz na bíblia da história.

## Fases v4 (2026-10-01, noite) — obstáculos com a cara do Gatoelho
Pedido do Rodrigo: melhorar os obstáculos e a lógica deles, **fugir de elementos clássicos do Mario** (plataformas elevadoras), deixar os "cogumelos saltitantes" mais lúdicos, aumentar um pouco as fases e melhorar a jogabilidade.

### O que saiu e o que entrou
- **Saíram os troncos flutuantes** (as plataformas que iam e vinham sozinhas).
- **Sapo-balão** (sapo + baiacu, um híbrido do Embaralhamento) no lugar do cogumelo-mola. Dorme fazendo bolha; acorda estufado quando o Gatoelho chega perto. Continua valendo a regra da criança — **encostou, voa** (7,5 tiles) —, mas agora é uma **cama elástica**: quem cai de mais alto sobe mais alto, e **segurar o pulo na hora do quique dá embalo** (9,7 → 11,8 → 13,7 tiles). Soltando o botão, o quique fica sempre igual. É um brinquedo: a criança quica sem parar; quem entende o embalo chega a lugares novos.
- **Galho-mola**: galho que brota de um mourão e **verga com o peso** (a ponta mais que a raiz). Pular na hora em que ele volta **arremessa** (até ~6,7 tiles, contra 4,25 do pulo normal); pular na hora errada é só um pulo comum. A janela é de uns 0,2 s, e o galho fica balançando, então dá para tentar de novo. Quem passa por baixo não percebe nada.
- **Ninguém morre**: pisado, o **caracol se esconde na concha**, que vira um **degrau** por 5 s (e não sai enquanto alguém está em cima dele); o **passarato fica tonto**, desce um pouco com estrelinhas girando e volta para o lugar. Mais gentil para a criança e gera quebra-cabeças (a concha alcança um galho 5 tiles acima do chão).

### Fase 1 "Saindo da Toca" (248 colunas)
- Ao lado do primeiro caracol, um galho a 5 tiles: só de cima da concha (ou quicando no caracol com o pulo apertado).
- O sapo-balão leva ao mirante do Dente-de-leão (como o cogumelo levava).
- **Pomar Velho** (novo, antes das flores-sino): um sapo-balão no caminho (a criança é lançada longe e cai em chão seguro) com uma coluna de cenouras pedindo "mais alto!" — **três quiques de embalo** chegam a um galho altíssimo com cenouras e a pedra antiga; e uma **cerca velha com galho-mola** que, no rebote, arremessa até um galho com cenouras.
- O cogumelo da Clareira do Tronco Oco saiu (com o embalo, ele permitiria alcançar a Dourada que exige escalar).

### Fase 2 "Trilha das Cenouras" (262 colunas)
- **Pedras do Rio**: um sapo-balão dorme na última pedra. Quem anda até ele é arremessado por cima do resto do rio até a margem; **dois quiques com embalo** alcançam o galho da Cenoura Dourada 1 (antes era a rota dos troncos).
- **Pomar dos Galhos-Mola** (novo, depois do Grande Voo): mourões baixos com galhos-mola e um sapo; o **arremesso do galho + o pulo duplo** juntos alcançam uma copa alta com cenouras e uma pedra antiga (nenhum dos dois sozinho chega). A criança só pula os mourões.

### Horta Escondida (98 colunas)
Os troncos que passeavam viraram mourões com galhos-mola, e entrou uma torre de cenouras sobre um sapo-balão (para quem aprendeu o embalo).

### O cochilo agora é um ritual
Chegar **ao lado** do objeto do cantinho → **farejar** → **pulinho para dentro** → **amassar o pãozinho** → **duas voltinhas** → **espreguiçar, bocejar e deitar** → dormir (orelha tremendo de vez em quando) → **sonho** → resultado por cima do sonho. Dá para pular o sonho com o botão de pulo. Ver [[Direção de Arte e Som do Gatoelho]].

### Alertas registrados
- O embalo do sapo-balão é poderoso: qualquer sapo novo precisa ser conferido pelo robô contra segredos próximos (foi assim que o cogumelo da Clareira caiu).
- A janela do galho-mola (~0,2 s) pode ser difícil para criança pequena; por isso nenhum galho-mola é obrigatório. Observar a enteada jogando.
- O ritual do cochilo + sonho leva uns 12 s até o resultado (pulável). Se cansar na repetição, encurtar o sonho em revisitas.
