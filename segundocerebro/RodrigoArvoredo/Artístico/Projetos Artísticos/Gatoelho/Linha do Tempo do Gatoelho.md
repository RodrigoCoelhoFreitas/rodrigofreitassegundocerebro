---
tags: [projeto, jogo, histórico]
---

# Linha do Tempo do Gatoelho

Ramificação de [[Gatoelho]]. O que foi feito, na ordem em que aconteceu. Detalhes de cada decisão em [[Game Design do Gatoelho]] e [[Arquitetura do Gatoelho]].

## 2026-09-29 — primeira sessão (pré-produção → protótipo completo)
Tudo abaixo foi feito numa única sessão longa com o Claude Code, na máquina nova.

1. **Pré-produção, sem código.** O Rodrigo apresentou o projeto inteiro (conceito, personagem, referências, mecânicas, mundos, inimigos, escopo, preocupações com assets) e pediu análise crítica antes de qualquer decisão. O Claude apontou pontos fortes (pergunta central gato+coelho, "terminar × 100%", cenários clean, comportamento antes da criatura, caixas), conflitos (Sonic × Mario × exploração; mobilidade demais mata o level design; Instinto Felino como botão; combate corpo a corpo × referências de tiro; arte cinematográfica × volume de animação), sugeriu cortes (colecionáveis, power-ups, natação) e propôs direções de design e de tecnologia.
2. **Metroidvania?** Rodrigo perguntou sobre migrar para metroidvania; discutido — o híbrido "fases com retorno" (Mega Man X) foi recomendado.
3. **Linguagem: TypeScript**; projeto criado em `projetos/gatoelho` com **PixiJS + Vite**. Primeiro código: um bloco que anda pela fase, com loop de passo fixo e colisão por tiles.
4. **Pulo** (altura variável, coyote time, jump buffer) e sala de testes redesenhada.
5. **Pulo duplo e planar** (o Rodrigo quis os dois), ligáveis para comparar; depois o planar passou a funcionar **já no primeiro pulo**, segurando o botão.
6. **App de PC com ícone**: Electron + instalador e `.exe` portátil, mantendo a versão web.
7. **Vida**: corações, vidas, espinhos, HUD e **minimapa** translúcido no canto inferior direito.
8. **Ajustes de vida pedidos pelo Rodrigo**: buraco tira todos os corações; energia não binária (corações parciais, espinhos tiram meio). **Sistema de animação reaproveitável** + animação de parado com manias de personalidade.
9. **Fluxo do jogo**: abertura **"LUDOVIC STUDIO"**, título animado com menu (Jogar, Configurações, Sair), configurações, pausa.
10. **Fim de fase** (bandeira, comemoração, confete, resultado), **som e música sintetizados**, **controle de videogame**.
11. **Mapa do mundo** estilo Super Mario World: transição em círculo, Mundo 1 com 5 pontos, caminhos que se revelam ao concluir fases, suporte a caminhos secretos, progresso salvo. O Rodrigo definiu a visão: o Gatoelho **ganha muitas mecânicas com o tempo** e volta às fases para achar segredos.
12. Registro de tudo neste segundo cérebro (esta pasta).
13. **Primeiro commit e push**: repositório privado `RodrigoCoelhoFreitas/gatoelho` criado no GitHub (commit `32b63a9`, branch `main`).

**Fim do dia:** repositório com ~4.400 linhas de TypeScript em 52 arquivos, versionado no GitHub; 53 verificações automáticas passando (em scripts temporários, fora do repo); executáveis gerados em `release\`.

## 2026-09-30 — segunda sessão
1. **Fase 1 "Saindo da Toca"** — desenho da fase, progressão de habilidades (começa sem planar e sem pulo duplo), Dente-de-leão Dourado, flores de vento, galhos, cenouras, três Cenouras Douradas, checkpoints, placas, fundo em camadas. Um robô de simulação encontrou e ajudou a corrigir três problemas de level design antes de qualquer pessoa jogar.
2. **Save e load** — o Rodrigo relatou que o Gatoelho "já nascia com a habilidade" na Fase 1; a causa era o progresso único gravando na hora do pickup. Solução: três espaços de save, gravação automática com aviso, arquivos em disco no PC, e a regra "só vale o que se conclui".
3. **Testes para dentro do repositório** (`npm test`, 96 verificações).
4. Commits `e6261c2` e `52dd444` enviados ao GitHub; vault atualizado.

## 2026-09-30 — terceira sessão (visão, história e fases v3)
1. **Visão em camadas**: a enteada ainda não lê → nenhuma camada da criança depende de texto; o texto é a porta para a lore. Ver [[Game Design do Gatoelho]].
2. **História**: o Embaralhamento, o laço dos Gatoelhos (Dr. Bigodes = Gatoelho velho de outra dimensão), o final verdadeiro como percepção de que não existe mundo "puro". Arco curto v1 escrito. Ver [[História e Mundos do Gatoelho]].
3. **Pesquisa de fases** (Mickey/Donald, Cuphead, Castlevania, Super Metroid, Blackthorne, Contra, Hollow Knight e outros). Ver [[Pesquisa de Fases do Gatoelho]].
4. **Fases 1 e 2 v3**: cochilo no lugar da bandeira, placas sem texto, pólen embaralhador (pluma e escama), a Onda e as cenouras fujonas, gatoelhês, flores-sino, raízes e Cenoura Roxa, luz própria de cada fase e a antena no horizonte. 238 verificações passando. Ainda não commitado ao escrever isto.

## 2026-10-01 — banho de gráficos
Resolução real da tela, base de arte (degradês, brilhos, sombras), fundo em camadas com névoa, ruínas e pássaros, paletas novas, terreno e objetos arredondados, Gatoelho com acabamento novo (silhueta original mantida), câmera com chão fino, título com o cenário novo e o catálogo de 64 vagas de sprite. Testados e descartados pelo Rodrigo: capim em primeiro plano, raios de sol e um Gatoelho redesenhado demais. 241 verificações passando. Detalhes em [[Direção de Arte e Som do Gatoelho]].

## 2026-10-01 (noite) — fases v4: obstáculos, cochilo e sonhos
Pedido do Rodrigo: gráficos mais limpos e nítidos, obstáculos melhores e sem clichês do Mario, fases um pouco maiores, fim de fase num canto com objeto doméstico curioso, sonho com pistas e animação melhor de deitar, pistas da história no fundo.
1. Física nova medida antes de desenhar as fases: sapo-balão (cama elástica com embalo) e galho-mola (arremesso no rebote).
2. Troncos flutuantes removidos; cogumelo-mola → sapo-balão; inimigos deixam de morrer (concha-degrau e passarato tonto).
3. Fase 1 ganha o Pomar Velho; Fase 2, o Pomar dos Galhos-Mola e um sapo no rio no lugar da rota dos troncos; Horta maior.
4. Cochilo em cantinhos com objetos domésticos (cesto, pantufa, relógio, xícara), ritual de gato e sonhos sem texto.
5. Fundo mais limpo, pistas da história no cenário, curvas mais finas e câmera no pixel da tela.
6. 266 verificações passando. Detalhes em [[Game Design do Gatoelho]], [[Direção de Arte e Som do Gatoelho]] e [[História e Mundos do Gatoelho]].

## 2026-10-05 e 06 — a bíblia da história (revisões 4 a 9)
Sessão longa só de história e universo, sem mexer no código. O Rodrigo pediu um arco "magnífico" e foi decidindo rodada a rodada; tudo ficou registrado em notas novas.
1. **Revisão 4**: dois modos (Ronrom, fácil, para crianças pequenas; Arrepio, difícil e profundo), os três Gatoelhos (o nosso, o Bigodes, o Reflexo que ajuda sem aparecer), guarda-roupa, fim de fase direto para o mapa com transições abstratas, terminais nas antenas (sandbox). Decidido: "inteiro não é puro", todos os finais ficam, o Reflexo nunca aparece de corpo.
2. **Revisão 5**: a tese ("não dá para voltar, dá para tecer"), a volta no tempo como mecânica central, o luto do Bigodes, o Pé de Feijão-de-Corda (fase secreta de subida) e o Heitor, o hamster preguiçoso. Decidido: o luto fica, a perda do relógio no final fica, o Heitor é a ajuda discreta.
3. **Revisão 6**: a premissa **"o jogo que você joga aos 5, ajuda alguém a jogar aos 15 e entende aos 30"** (decidida como o grande diferencial), o Modo Reflexo, a Cápsula do Tempo, doze finais.
4. **Revisão 7**: lições dos clássicos (O Senhor dos Anéis, Harry Potter, Star Wars, Breaking Bad); o plano do Bigodes e a profecia lida no reflexo (decididos); o Patatu companheiro; a Madame Cisnobra; a Traça; treze finais; a bíblia dividida em notas.
5. **Revisão 8**: a segunda premissa, **"cada pessoa joga um Gatoelho diferente"** (dimensões por semente), o Avesso infinito, as missões escondidas do Reflexo, os achados, o jornal satírico O Novelo, os pilares de jogabilidade. Decidido: manter fases ("um Hollow Knight de fases").
6. **Revisão 9, a Camada Zero**: o mundo do Gatoelho é a Terra depois da extinção humana; as Máquinas, antes de partir para o espaço (a linhagem do livro [[A Sonda]]), fizeram o embaralhamento genético dos animais que restavam; no fim da série, o Gatoelho pede ajuda e sai da Terra com os amigos. Decidido: nada da superfície muda; a humanidade já está extinta quando o jogo começa; a ponte com A Sonda é a inteira.
Notas: [[Arco Completo do Gatoelho]], [[Finais do Gatoelho]], [[Lendas do Gatoelho]], [[Sistemas da História do Gatoelho]], [[Guarda-Roupa do Gatoelho]], [[Personagens do Gatoelho]], [[Tecido Infinito do Gatoelho]], [[Jornal do Gatoelho]], [[Camada Zero do Gatoelho]].

## 2026-10-06 — a história contada de uma vez
Pedido do Rodrigo: juntar tudo numa história mais clara e precisa, com marcos claros na trama principal, **sem inventar**. Resultado: a nota [[A História do Gatoelho]].
1. **A saga em quatro frases** e **a história verdadeira em ordem** (a casa da Vó de Todas, a Arca, as Nove Vidas, a oitava vida, o Clarão, a porta da toca, os oito anos do Bigodes contados pelo diário de versões dos terminais).
2. **A trama do jogo 1 em 21 marcos** (0 a 20, do prólogo à Primeira Porta; o Ronrom termina no 13) e **a saga em seis marcos** (S1 a S6, dos quatro jogos aos livros e [[A Sonda]]).
3. **A espinha**: as quatro revelações (o mapa da Casinha, a poça, a pedra da profecia, o varal), as recusas do Bigodes, os três Gatoelhos, plantar e colher ligado aos marcos.
4. **Seis ajustes de coerência**, aguardando aprovação: as 4.096 tentativas vieram depois do Clarão (não antes); o Robogato foi feito antes do Clarão; o mundo já era misturado antes do Clarão; o Reflexo é o fim do caminho que começa no Fio Vermelho; o lenço do nosso Gatoelho foi tricotado pelo Bigodes; a "máquina de reversão inteira" ainda sem definição.
5. **Pontos soltos** levantados: os mundos de origem e a Dona Coelha inteira na Camada Zero; o Fio Vermelho (desembaralhar todos) contra o propósito da Arca; o tempo entre a Partida e o jogo; o que as 4.096 tentativas fizeram no nosso mundo.

## 2026-10-15 — leitura completa do código
Rodada de revisão de todos os projetos, sem código novo. O código confere com as notas; os achados (teclas de desenvolvimento no jogo final, "Fim de jogo" que não recomeça a fase, executáveis velhos, texto obrigatório na tela) estão em [[Arquitetura do Gatoelho]]. Os seis ajustes de coerência de [[A História do Gatoelho]] seguem esperando a aprovação do Rodrigo.

## 2026-10-16 — as misturas (proposta)
Pedido do Rodrigo, numa conversa só de personagens (em paralelo às outras frentes): continuar pensando nos personagens e nas misturas entre bichos e plantas. Resultado: a nota [[Misturas do Gatoelho]], proposta, nada decidido. Nenhum arquivo do jogo foi alterado.
1. **A frente:** as plantas já estavam no jogo sem história (o Dente-de-leão e o Trevo dão as habilidades, o pólen dá as transformações). Bicho vai, planta fica; o Clarão misturou à força, a abelha mistura por encontro; planta é tempo.
2. **Seis regras** para misturas com planta (entre elas: comida não tem rosto; perigo parado não ganha rosto; uma piada por bicho).
3. **As Douradas:** plantas de verdade com nome de bicho acordam a metade gato ou coelho (Unha-de-gato para escalar, Rabo-de-gato para andar em fios); o pólen só empresta.
4. **Dez moradores novos** com silhueta, mania, dor e uma linha do caderno do Bigodes: Seu Dente-de-Leão (as plumas ensinam o planar sem texto), Girafassol, Ratoneia, Caracouve (o caracol do jogo ganha par), Batatus, Cogumelebres, Araipê, Vitória-Rã, Jabuticabra, Pipoco.
5. **Os Ao-Pé-da-Letra:** bichos de fundo tirados ao pé da letra de nomes populares de plantas do Brasil, para o Gerador.
6. **A família:** mania e dor para os irmãos (o Ouriçapo como alfineteiro da colcha, a Coalhoca que abraça, a Orcabelha que poliniza); o Patatu como o único que pede ajuda; o **Carrapatu** para o Patatu re-embaralhado.
7. **A janela da Vó:** o chá é de camomila (de dormir, e a Traça não come quem dorme); o vermelho é de urucum, que desbota ao sol; o vaso de rabo-de-gato e orelha-de-coelho. Mais a **horta que cruza**, fatos reais para o caderno e o custo de cada ideia.
8. **Alertas de coerência:** o Fio Vermelho separava todo mundo sem perguntar (aqui: "a Agulha pergunta"; o [[Fio da Meada do Gatoelho]] depois propôs "a Agulha costura", que esta nota passou a recomendar); a Dona Coelha é inteira, não pura.
9. **Revisão 1.1**, no mesmo dia: conciliada com o Fio da Meada e com a regra do vermelho da [[Paleta do Gatoelho]]; ideias descartadas e guardadas registradas.

## 2026-10-16 — o fio da meada (Revisão 10, proposta)
Pedido do Rodrigo, numa conversa só de enredo (em paralelo a outras frentes do jogo): limpar os detalhes da história e solidificar o fio da meada, numa grande rodada de pensamento. Resultado: a nota [[Fio da Meada do Gatoelho]], proposta, nada decidido.
1. **O fio**: o coração da história (o velho que não bateu na porta, a velha que deixa chá na janela, o filhote que é o fio entre os dois), a tese inteira ("não dá para voltar, dá para tecer, e um fio sozinho não tece") e a imagem da saga, **fenda × porta** ("fenda é porta que ninguém bateu").
2. **Cinco regras de cânone**: uma Terra, nove redomas e o lado de fora (dimensões infinitas saem do cânone e ficam como jeito de contar); o cânone da série segue o Fio Vermelho; tecer nunca é separar; a Camada Zero nunca é dita; todo elemento novo responde à pergunta do jogo ou sai.
3. **Treze nós desatados**: o Fio Vermelho costura em vez de desembaralhar todo mundo; as Máquinas pouparam o gato e o coelho da Vó (por isso a Corrente existe); a "nona vida" era a nona redoma; a profecia gravada embaixo de uma pedra, lida pelo avesso (física do reflexo); as antenas calibram a máquina ("o caçador era a caça"); o Bigodes dispara sem perguntar e o Patatu leva a onda (vira o Carrapatu); a Dona Coelha e o gatinho eram desta redoma; uma Agulha só e a blusa nas patas da Traça; a recaída v4097 no lugar da segunda luta; o Reflexo pelo arquivo, sem iterações; os nomes dos pulsos; o Feijão do Heitor com semente da Arca; o cesto, as cartas e a carta.
4. **Sete ideias novas**, entre elas a foto como instantâneo (por que o Bigodes desliga a máquina), o desejo e o defeito do herói e a xícara cheia como ponte entre o Ronrom e o Arrepio.
5. **Pontos soltos com recomendação**: uns 150 anos entre a Partida e o jogo; a Vó Tartuja fica na Terra; a Sonda é outra linhagem.
6. Converge com [[Misturas do Gatoelho]] (força × encontro, o Patatu que pede ajuda, o Carrapatu); diverge no Fio Vermelho (lá: "a Agulha pergunta"). Os seis ajustes de 2026-10-06 entram nas treze decisões pedidas ao Rodrigo.

## 2026-10-16 — a paleta (proposta)
Pedido do Rodrigo, numa conversa só de cor (em paralelo às outras frentes): continuar pensando na paleta. Resultado: a nota [[Paleta do Gatoelho]] e uma página com prints do jogo e simulação de daltonismo, proposta, nada decidido. Nenhum arquivo do jogo foi alterado: as paletas novas foram testadas trocando as cores com o jogo rodando.
1. **Um dicionário de cores**, com as cores para jogar (laranja pega, dourado é novo, roxo é escondido e verdadeiro, pontas claras machucam, fio de luz é chão) e as cores para ler (latão do Bigodes, porcelana da casa, luz das Máquinas, sépia do passado, cinza só da Traça, sonho, Onda iridescente).
2. **A regra do vermelho**: só é vermelho o que foi tricotado por uma Vó (o vermelho é a única cor que veio das pessoas). Fio com nozinho para quem não enxerga vermelho; corações do HUD de tricô. Cinco lugares do código fogem da regra hoje.
3. **Regiões**: Bosque (cenoura), Telhadópolis (azulejo), Tocópolis (vaga-lume), Casinha (âmbar e sépia), Monte Ronrom (ipê-rosa), Pico (os quatro feixes somam branco); noite escura em azul-chuva. Os feixes foram conciliados com o Nó 5 do [[Fio da Meada do Gatoelho]]: saem na cor da região e viram as cores das fitas do Gatoelho.
4. **Consertos achados nos prints**: a tarde da Fase 2 some para quem tem daltonismo vermelho-verde (proposta de sombra violeta testada); caracol da cor da cenoura; sapo da cor da grama na Horta; halo do sol dourado; espinheiro de cor fixa; Onda rosa-choque.
5. **Robô daltônico** proposto para `tests/sim`, com critério em ΔE; as paletas atuais da manhã e da tarde não passam, as propostas passam.
6. Também: dimensões do Ato IV como transformações de cor, pelagens sorteadas com limites, o Bigodes como a pelagem do jogador envelhecida, fitas do Faro pelo que o bicho sabe fazer (o Gatoelho em azul-noite e ocre).

## 2026-10-16 — o planeta e os mundos (proposta)
Pedido do Rodrigo, numa conversa só de fases e mundos (em paralelo às outras frentes): o mundo por onde o Gatoelho anda entre as fases é redondo, é o planeta; movimentação entre mundos como no Donkey Kong Country 3; zonas de gelo e industriais; lugares históricos abandonados só como easter egg; 4 mundos para a criança e as 9 realidades para o adulto. Resultado: a nota [[Planeta e Mundos do Gatoelho]], proposta, nada decidido. Nenhum arquivo do jogo foi alterado.
1. **O planeta**: nove gomos (as nove realidades) que se encontram no polo norte, onde fica o Pico do Clarão (a luz no topo é a bússola de quem não lê); a Ilha das Nove Vidas debaixo do gelo do Pico; a Borda no equador, com o Feijão; o lado de fora no hemisfério de baixo. Andar para leste é andar a Corrente em ordem, e a primeira vida mora ao lado da nona.
2. **A criança joga o lado de cá**, entrando pelas fendas do velho: Bosque (nosso), Telhadópolis (o Relojoeiro, industrial, relógios parados às cinco), Planície Branca e Tocópolis (a Sem Rosto, gelo em cima e túneis embaixo), Monte Ronrom (a Navegante, o mar que subiu para o céu), e o Pico de gelo, subindo a serra atrás de casa. Os marcos do Fio da Meada ficam na mesma ordem.
3. **O adulto joga o lado de lá**, entrando batendo na porta: Horta Perfeita (Jardineira), Reino de Vidro (Rei dos Espelhos), As Teias (Fiandeira, industrial), Os Campos (Coelhato, o único mundo sem lei) e, secreto, o Mundo Parado do Bigodes, atrás da porta dos fundos da Casinha, que é a primeira fenda.
4. **A lei de cada mundo é a cicatriz do que aquela vida tentou desfazer.**
5. **O mapa à moda do DKC3**: os chefes acalmados dão carona no planeta (no lugar dos veículos), o correio do Pinguinguru (no lugar dos ursos), os insones que ensinam a cantiga (no lugar das Banana Birds), o Heitor no mapa. O mapa é desenhado como o globo de tricô da Vó; a Traça come buracos nele; o Fio Vermelho cerze.
6. **Fases mundo a mundo** com uma receita de cinco (passeio, vertical, carona, fuga ou ritmo, luz) inspirada na variedade do DKC3; ≈ 25 fases no Ronrom.
7. **Cutucos históricos** com cinco regras (sem nome, grandes demais, rimando com a vida do mundo, sem corpo humano, cuidado com direito de imagem), entre eles a esfinge sem rosto na neve, a caravela no fundo seco, o tear de cartões perfurados e a porta do cofre de sementes no gelo.
8. **A série vira geografia**: jogo 1 o norte, jogo 2 o sul (o lado de fora), jogo 3 para dentro, jogo 4 para cima. Mexe nas propostas da Camada Zero, das Lendas (troca a 2ª e a 3ª vida) e do Fio da Meada (as redomas dos Espelhos e das Teias voltam para o jogo 1).
9. **Ideias guardadas**, no mesmo dia: as outras formas de planeta pensadas (de lado, em camadas; gomos de polo a polo; cilindro), as outras distribuições dos mundos (a mais forte: Telhadópolis como o porto da Navegante, com marés que inundam as ruas) e quinze ideias soltas.
