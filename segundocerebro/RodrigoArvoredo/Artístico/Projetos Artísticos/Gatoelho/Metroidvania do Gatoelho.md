---
tags: [projeto, jogo, game-design, mapa]
---

# Metroidvania do Gatoelho

Ramificação de [[Gatoelho]]. **A virada para o Mapa Único (2026-10-28).** O Gatoelho deixa de ser um jogo de fases e vira um **metroidvania**: um mapa 2D só, enorme para cima, para baixo e para os lados, como os de Hollow Knight e Super Metroid. As nove realidades e a história ([[A História do Gatoelho]]) continuam; o que muda é o chão onde tudo acontece.

**O esboço do mapa:** página interativa em https://claude.ai/artifact/PJM5h6HF6pQUfjZYkmbR8J (esboço 2, com abas para as nove camadas). A fonte é o arquivo `docs/mapa-unico/mapa.js` no repositório do jogo, com salas, portas, trancas, camadas, caminhos e o verificador. A página só desenha esse arquivo.

---

## Decisões do Rodrigo (2026-10-28)
1. O jogo vira **metroidvania**, com um mapa único e gigante em 2D. **Fases deixam de existir.** O mundo tem superfície e subterrâneo, **em terra e em gelo**, e o Gatoelho anda por ele para desvendar, encontrar coisas e enfrentar os chefes.
2. O jogo **deixa de ser tão infantil** e **mira o público de metroidvania**. A meta é ser um clássico do gênero, digno de prêmio.
3. **A história é a mesma**, e as nove realidades continuam, dentro do mapa único.
4. Referências de mapa: os mapas completos de Hollow Knight (hallownest.net, guia de 112%) e de Super Metroid (Zebes).
5. **Um mundo só, que não dá a volta.** Ele é **como nove mapas sobrepostos**: o jogador mais simples joga só um; os outros encontram formas de ir para as outras dimensões, que **aproveitam o mesmo mapa** com segredos e detalhes diferentes.
6. **Pontos de save e um save automático inteligente.** O cochilo pode sumir.
7. **O jogo é contínuo, exatamente como Super Metroid e Hollow Knight**: salas emendadas, sem fases.
8. **As fases que existem são esquecidas**; o mapa é pensado do zero como nos jogos de referência.
9. **O globo de tricô e o mapa de fases saem.**
10. **Progressão vertical e horizontal**, como nos jogos de referência.
11. **Os chefes surgem em lugares e condições específicos**, como em Hollow Knight.
12. **Linha dos Batatus** (metrô) e **correio do Pinguinguru** como viagem rápida.

**Em aberto:** combate (a patada) e editor de mapa (LDtk). Recomendações na Parte 6.

O que segue é **proposta do Claude** para fazer as decisões funcionarem, vetável a qualquer momento.

---

## Parte 1 — O mapa
1. **Um mundo só, com bordas.** O Reino de Vidro é a borda oeste, no sal; a Horta Perfeita é a borda leste, depois do mar.
2. **O Pico do Clarão é o eixo.** No topo, o Bigodes e a máquina; embaixo, debaixo do gelo, a Ilha das Nove Vidas. O gelo racha depois do Final da Toca e abre o caminho para o lado de lá, a oeste do Pico.
3. **O lado de cá fica a leste de casa** (Bosque, Planície Branca, Tocópolis, Telhadópolis, Monte Ronrom) e **o lado de lá a oeste do Pico** (Serra de Trás, Campos, Teias, Reino de Vidro), mais a Horta na borda leste.
4. **A casa no meio de tudo.** As **Raízes de Casa**, debaixo da toca, são o cruzamento: Bosque, Tocópolis, a Linha dos Batatus (com a estação **ARCA 9** debaixo de casa) e o gelo do Pico. Todo atalho volta para a despensa da Vó.
5. **Gelo e terra, em cima e embaixo**: gelo na Planície (em cima), em Tocópolis (embaixo, com terra), no Pico inteiro e na Serra de Trás; terra no Bosque, nas Raízes, nos Campos e na Horta.
6. **Toda tranca tem cara** (o dicionário das trancas da [[Habilidades e Builds do Gatoelho]]): a cor de cada porta é a da chave que a abre.
7. **Contínuo como nas referências.** Super Metroid e Hollow Knight também são feitos de salas emendadas por portas, com a câmera presa à sala e transições curtas. É o modelo adotado: sem fases, sem tela de mapa entre lugares.

**Números do esboço 2:** 98 salas-mãe, cerca de **950 telas por camada** (mundo de 100 × 37 telas). As salas-mãe vão ser recortadas em salas de verdade quando cada região for desenhada.

---

## Parte 2 — Nove mapas sobrepostos ⟨proposta⟩
É a Revisão 11 levada ao pé da letra: as Máquinas **dobraram o mesmo mundo nove vezes, no mesmo lugar**. Cada camada tem **as mesmas salas**; a vida que mora nela deixou o mundo de um jeito. A geografia é a mesma; mudam os estados, as passagens, os segredos e os chefes.

| Camada | Quem | Como o mapa inteiro fica | Por onde se entra | Antes do final? |
|---|---|---|---|---|
| **9** · a nossa | o nosso Gatoelho | o mapa do jogo | é onde o jogo começa | — |
| **8** · o Mundo Parado | o Bigodes | o instante do Clarão em sépia; neve parada no ar; a água é sólida; voltar no tempo não funciona | ficar parado diante do riacho (o reflexo que não acompanha) · a porta dos fundos da Casinha | **sim, segredo** |
| **7** · o Coelhato | o Coelhato, velhinho | séculos depois: mato por cima de tudo, bichos misturados vivendo bem, nenhuma lei | bater na porta da casa vazia | não |
| **6** · a Fiandeira | a Fiandeira | fios amarrando tudo; mexer numa coisa puxa as outras | puxar o fio certo do tear | não |
| **5** · o Rei dos Espelhos | o Rei | só se vê metade de cada um; anda-se no reflexo, de cabeça para baixo | andar no reflexo do sal até o mundo virar | não |
| **4** · a Jardineira | a Jardineira | tudo em fileiras de uma cor; o misturado é empurrado para fora | a porta redonda no fim da fileira | não |
| **3** · a Navegante | a Navegante | o mar nunca subiu: cobre o mundo de baixo; o subsolo está inundado | a fenda debaixo da caravela (Disparada) | **sim, segredo** |
| **2** · o Relojoeiro | o Relojoeiro | a Dimensão Lenta: tudo devagar, menos o Gatoelho; relógios às cinco | voltar no tempo dentro da sala lenta da torre | **sim, segredo** |
| **1** · a Sem Rosto | a Sem Rosto | a mais velha: tudo gasto, soterrado, luz trocada; Telhadópolis nunca existiu | no alto da cabeça da estátua, pelo Faro | **sim, segredo** |
| **Avesso** | a Traça | o mapa pelo lado de dentro do pano: espelhado e comido de traça | pelo Nó, depois da v4097 | não |

**As regras:**
- **Quem joga reto conhece só a camada 9.** A história inteira até o Final da Toca acontece nela.
- **De cima, só se deixa cair.** Desce-se de camada deixando-se cair numa poça, fenda ou porta, sempre num lugar marcado. Volta-se pelo mesmo lugar ou pela **Ilha**, que existe igual nas nove e as amarra: com a **Agulha** (achada na camada 8, na cômoda da toca parada), troca-se de camada no lago.
- **De baixo, puxa-se.** O que se faz numa camada muda a de cima: girar o ponteiro na camada 2 gira a torre de Telhadópolis na 9.
- **Cada camada derruba ou cria caminhos**: na 8 o rio é sólido e leva à Dona Coelha antes do tempo; na 7 o espinheiro virou capim; na 6 um fio liga a copa ao Morro do Vento; na 3 o barco da Navegante sobe o rio; na 4 a Árvore Grande foi cortada.
- **Escopo:** é aqui que nove mapas cabem no orçamento de um. Cada camada reaproveita as salas e muda tiles, estados, cor, luz, bichos e algumas passagens. O peso maior fica na região onde cada vida é mais forte.

---

## Parte 3 — Os caminhos

### O fio vermelho (a história, camada 9): 19 paradas
1. **A Toca**, a manhã da onda. 2. **Mirante**: Dente-de-leão (planar). 3. **Trilha das Cenouras**: Trevo (pulo duplo). 4. **Copas Altas**: Unha-de-gato (escalar). 5. **Covil do Lobovelha**, debaixo do Bosque (antena 1); acalmado, ele abre o espinheiro. 6. Passando a Planície calada, **Telhadópolis**: Gato Líquido. 7. **A Roda**: Tubaramster vira barco. 8. **Os Varais**: Rabo-de-gato. 9. **Pega-Pega nos Telhados**: o Cucodrilo e a **volta no tempo** (antena 2). 10. O buraco da Planície desmorona ao contrário: **Tocópolis** e o Faro. 11. **A Raposinha**: Pé-de-gato. 12. **Rei Caracólio** (antena 3). 13. O vagão até **ARCA 9**, debaixo de casa. 14. O caracol sobe a serra: **a Casinha**. 15. De barco, **o Fundo Seco**: a Disparada. 16. **O Mar no Céu**: Borbopótamo, antena 4, a Virada. 17. **O Beco**, a noite escura. 18. **A Subida da Serra**: a cantiga e o Carrapatu-trenó. 19. **A Máquina**: o Final da Toca.

É o desenho clássico do gênero, nos dois eixos: passar pela Planície sem poder descer e voltar com a volta no tempo; descer do Bosque às Raízes e a Tocópolis, subir a torre, o vulcão e o Mar no Céu, e por fim o Pico; abrir o atalho que liga tudo à casa (ARCA 9).

### Para quem procura
A xícara cheia e o gesto de **bater** → o Mundo Parado e a Agulha (camada 8) → pelo gelo rachado, a oeste do Pico, a Serra de Trás e os Campos: o Coelhato (7) → as Teias e a Fiandeira (6) → o Reino de Vidro e o Rei (5) → a Horta e a Jardineira (4) → a Ilha e a profecia lida rente à água → a Dona Coelha e a carta → a v4097 e o Avesso.

---

## Parte 4 — Chefes: onde e quando aparecem ⟨proposta⟩
| Chefe | Camada | Onde | Quando aparece |
|---|---|---|---|
| Lobovelha | 9 | Covil do Lobovelha | O covil fica vazio até o Gatoelho ter a Unha-de-gato; na primeira noite depois disso, o uivo que termina em "béééé" chama do fundo. |
| Tubaramster | 9 | A Roda | Dorme no fundo; só acorda quando a Roda vira de cabeça para baixo. |
| Cucodrilo | 9 | Pega-Pega nos Telhados | Às cinco, a hora do chá, o velho passa correndo pelos telhados; quem o segue acha o Cucodrilo com o relógio na barriga. |
| Rei Caracólio | 9 | Concha do Rei | Com luz é só uma concha gigante; sai no escuro total, quando os vaga-lumes se apagam. |
| Borbopótamo | 9 | O Mar no Céu | Desce na maré alta, depois que a terceira antena cai. |
| o Bigodes | 9 | A Máquina | Depois das quatro antenas: a máquina liga e a tempestade abre a subida. |
| Robogato | 8 | quarto da toca parada | Abre a porta um quadro atrasado; só luta depois de o Gatoelho dar corda na caixinha de música. |
| Ararranha | 6 | Os Teares | Quando alguém puxa o fio errado. |
| Camaleão | 5 | Palácio dos Espelhos | Nunca de frente: só no reflexo, de cabeça para baixo no sal. |
| Dona Tronca | 4 | As Estufas | Só anda quando todas as plaquinhas da Horta foram arrancadas. |
| a Traça | Avesso | o Nó | v4097: quando o velho liga a máquina de novo; cresce a cada volta no tempo. |

---

## Parte 5 — Save, morte e viagem ⟨proposta⟩
- **Pontos de save** pelo mundo (no esboço, um novelo: lugares onde alguém tricotava). Salvar ali cura e é o único lugar para trocar broches ([[Habilidades e Builds do Gatoelho]]).
- **Save automático inteligente**: grava sozinho ao pegar uma Dourada ou poder, acalmar um chefe, abrir um atalho, trocar de camada e entrar numa região nova. Ao cair, volta-se ao último ponto de save, mas nada do que foi gravado se perde.
- **Viagem rápida**: a Linha dos Batatus liga ARCA 9, Tocópolis, Telhadópolis e o Monte Ronrom (cada estação abre do lado de dentro); o correio do Pinguinguru leva entre caixas de correio achadas no mapa.
- **Consequências nas outras notas**: os sonhos que vinham depois do cochilo ([[Cutscenes do Gatoelho]], [[Roteiros do Gatoelho]]) precisam de outro gatilho ou saem; o "fim de fase" some do vocabulário.

---

## Parte 6 — Recomendações para o que está em aberto
- **Combate**: recomendo a **patada** (metade gato) junto com o **pisão-quique** (metade coelho). Ela empurra e atordoa, quebra coisas e acalma chefes em vez de matá-los. Num metroidvania o jogador precisa de uma ação curta e confiável o tempo todo (como o ferrão em Hollow Knight); sem ela o mundo grande fica vazio de interação. Mantém a regra "ninguém morre".
- **Editor**: recomendo o **LDtk**, editor gratuito de mapas 2D feito pelo diretor de Dead Cells. Ele desenha o mundo inteiro numa grade de telas, como o mapa do Super Metroid, e exporta um arquivo que o jogo lê. O `mapa.js` entra nele como molde. A alternativa é um editor próprio, mais caro de fazer.

---

## Parte 7 — O plano em etapas ⟨proposta⟩
1. **Segundo cérebro**: [[Game Design do Gatoelho]] (estrutura, save, público), [[Planeta e Mundos do Gatoelho]] (aviso: o planeta e a estrutura de fases foram substituídos; mundos, leis e chefes continuam), [[A História do Gatoelho]] (as camadas como mapas sobrepostos; "fase" vira "sala"), [[Habilidades e Builds do Gatoelho]] (as trancas oficiais e as chaves de chefe), [[Cutscenes do Gatoelho]] e [[Roteiros do Gatoelho]] (sem cochilo), [[Pesquisa de Fases do Gatoelho]] (método de mapa), [[Arquitetura do Gatoelho]].
2. **Motor**: salas no lugar de fases (mapa de tiles com posição na grade do mundo e portas nas bordas), carregamento da sala e das vizinhas, câmera presa à sala, transição curta; **camada como dimensão do mundo** (a mesma sala, com variações por camada); save novo (salas visitadas, itens por id, marcas da história, o que foi puxado de baixo, camada atual); mapa de pausa; pontos de save e save automático; viagem rápida; o verificador no `npm test`. **Saem** o mapa de fases (`WorldMapScene`), o globo (`PlanetScene`), o fim de fase e as fases atuais.
3. **O corpo do Gatoelho**: Unha-de-gato, queda rápida, lamber a pata e o combate, afinados até andar ser bom por si só.
4. **Fatia vertical**: Bosque, Raízes de Casa e Planície Branca (cerca de 176 telas), três Douradas, o Lobovelha, mapa de pausa, e **uma** passagem para a camada 8 (o riacho), para provar o sistema das camadas cedo.
5. **Regiões na ordem do fio vermelho**: Telhadópolis, Tocópolis, Monte Ronrom, Pico. Depois o lado de lá e as camadas.
6. **Arte e som definitivos**, em paralelo desde a fatia vertical.

---

## Parte 8 — Riscos honestos
1. **Escopo.** Cerca de 950 telas na camada 9, mais as variações das outras oito, é muito para uma pessoa. As camadas só cabem se reaproveitarem as salas de verdade; o peso de cada uma tem que ficar na região dela.
2. **Camadas que confundem.** O jogador precisa saber sempre em que camada está (cor, luz, som e um sinal no mapa de pausa) e como voltar.
3. **Puxar de baixo** é o sistema mais caro: o estado de cada camada fica salvo e muda as outras. Entra no motor na Etapa 2.
4. **Segredos cedo demais.** A camada 8 se abre no começo do jogo (o riacho). É um mistério bom, mas nada lá pode dar uma chave que quebre a história.
5. **Planar forte demais** (alerta antigo) pesa mais num mapa aberto.

## Perguntas em aberto
- Combate e editor (Parte 6).
- O nome e o desenho dos pontos de save.
- Os sonhos sem o cochilo: outro gatilho ou saem?
- Os nomes das salas do esboço são provisórios.
