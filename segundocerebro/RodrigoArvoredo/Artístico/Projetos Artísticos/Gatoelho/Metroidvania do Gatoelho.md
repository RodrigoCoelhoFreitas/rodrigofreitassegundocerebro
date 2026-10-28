---
tags: [projeto, jogo, game-design, mapa]
---

# Metroidvania do Gatoelho

Ramificação de [[Gatoelho]]. **A virada para o Mapa Único (2026-10-28).** O Gatoelho deixa de ser um jogo de fases e vira um **metroidvania**: um mapa 2D só, enorme para cima, para baixo e para os lados, como os de Hollow Knight e Super Metroid. As nove realidades e a história ([[A História do Gatoelho]]) continuam; o que muda é o chão onde tudo acontece.

**O esboço do mapa:** página interativa em https://claude.ai/artifact/PJM5h6HF6pQUfjZYkmbR8J (esboço 6: abas para as nove camadas, modos de cor "quando abre" e "papel da sala", as fichas e o que tem em cada sala, as vitrines, o que cada região guarda, as peças do mundo e o bestiário). A fonte é o arquivo `docs/mapa-unico/mapa.js` no repositório do jogo, com salas, portas, trancas, camadas, caminhos e o verificador. A página só desenha esse arquivo.

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

**Números do esboço 4:** **225 salas** em todas as camadas (cerca de **2.400 telas** na camada 9), mais **23 salas que só existem numa camada**; o mundo mede 143 × 63 telas. Cada camada fica entre 199 e 227 salas, porque umas somem e outras aparecem.

### Esboço 6 — transições longas, o que tem em cada sala e as vitrines (2026-10-28)
Pedido do Rodrigo: aumentar o mapa sem aumentar o número de salas (algumas salas um pouco maiores e, sobretudo, transições e corredores mais longos), detalhar o que tem em cada sala, e usar o recurso das referências de passar por um lugar que ainda não se alcança, de propósito, para o jogador ficar curioso: "o jogo é metroidvania, mas tem uma breve condução de roteiro nesse sentido".
- **O esticão**: o mundo ganhou colunas nas dez fronteiras entre regiões e linhas entre as faixas de profundidade. Uma sala que atravessa um corte cresce; as vizinhanças não mudam. Ficaram 114 salas maiores (transições entre regiões, poços, corredores, a Ilha). O mundo passou de 143 × 63 para **166 × 69 telas**, e a camada 9 de cerca de 2.400 para **cerca de 2.950 telas**, com as mesmas 225 salas.
- **O que tem em cada sala**: um catálogo de 46 **peças do mundo** (coletáveis, serviços, peças de sala e perigos, cada uma dizendo com que habilidade conversa) e a lista do que tem dentro de cada uma das 248 salas. Na camada 9: 14 caixas do Pinguinguru (uma por região: a peça do mapa e a viagem rápida), 14 Cenouras Roxas (uma por região), 26 Cenouras Douradas, 13 broches, 5 Ecos Antigos, 14 achados, 4 pedaços da foto, 5 mastros e 21 pontos de save (os novelos).
- **As vitrines do caminho** (a condução): antes de cada habilidade, o fio vermelho passa por um lugar que ainda não se alcança. Duas paradas novas no fio, de roteiro: **o Pé da Serra, antes de sair de casa** (lá no alto, a Casinha com a luz acesa e um paredão de gelo que ninguém sobe: a vitrine do caracol) e **o espinheiro fechado no fim do Bosque**, logo depois do planar (do outro lado, branco e silêncio: a vitrine do Lobovelha). As outras: a flor de vento adormecida no quintal (planar), a beirada alta dentro da árvore (pulo duplo), o paredão de unhas do outro lado do riacho (escalar), a grade do tamanho da cabeça na fábrica (Gato Líquido), o varal alto entre chaminés (fio), o gelo fino com o buraco no meio (volta no tempo), os rastros de galinha na neve (Faro), a nevasca por cima do respiradouro (Patas de Almofada), o feno do pomar, as caixas de vime e a praia sob a cachoeira (Disparada).
- **Os Nós no Fio** ⟨proposta⟩: no mapa de pausa, cada vitrine vira um nozinho vermelho no fio; quando a habilidade chega, o nó brilha. A condução sem texto, com a cara do jogo (vermelho é o que a Vó tricotou).
- **Regras novas no verificador**, todas passando: toda sala tem o que tem dentro; save e novelo sempre juntos; toda região guarda uma caixa do Pinguinguru, uma Cenoura Roxa, ao menos duas Douradas e um broche; nenhuma peça que pede uma habilidade aparece antes dela, a não ser como vitrine; antes de cada habilidade há uma vitrine no caminho.

### Esboço 5 — as fichas das salas e a coesão (2026-10-28)
Pedido do Rodrigo: manter o mapa do tamanho que está e detalhar a coesão, os desafios de cada sala e o planejamento.
- **Toda sala tem ficha** (as 248): o **papel** no mapa (ensina, coração, desafio, passagem, poço, atalho, mirante, segredo, dourada, chefe, história, save, camada), a **ideia** no método da [[Pesquisa de Fases do Gatoelho]] (lugar + verbo + reviravolta), as **habilidades que o desafio usa** na primeira visita, os **bichos** e, quando houver, a **chave de uma volta depois**. Exemplos: "A ponte de galhos quebrou: o primeiro voo, sobre um rio raso, sem perigo"; "Os vaga-lumes acendem quando ele chega perto e apagam quando ele para"; "Sem lei nenhuma: depois de tantos mundos estranhos, o desafio é um mundo normal".
- **O bestiário**: os embaralhados da [[Personagens do Gatoelho]] espalhados pelas regiões, mais a Jabuticabra e o Pipoco do Monte Ronrom e dois novos (proposta): o **Focarneiro** (foca + carneiro: desliza de barriga no gelo e dá cabeçada; acalma-se enrolando-se na própria lã) e o **Mariposapo** (mariposa + sapo: gruda nos fios com a língua e vai atrás de luz). Ninguém morre: cada um se acalma de um jeito.
- **Regras novas no verificador**, todas passando: nenhum desafio pede habilidade que o Gatoelho ainda não tem quando chega; toda região ensina a sua lei num lugar seguro antes de cobrá-la e tem um coração e um segredo; toda habilidade nova é usada logo na sala que ela abre; cada Dourada e cada poder **chama de volta** a pelo menos duas regiões (a regra Mega Man X, agora nas voltas também).
- **Consertos de lógica que as regras acharam**: a Torre Parada era alcançável pelo porto antes da volta no tempo (agora a oficina de Tic e Tac dá só para o porto, e o alçapão do sino abre voltando no tempo); o sino virou segredo de volta; para fechar as voltas, segredos novos com cara de história (o novelo vermelho numa fresta debaixo da cama, um buraco de foca no chão do iglu, a prateleira alta do Ouriçapo, o poste do varal até o telhado da toca, um monte de feno no fundo do pomar, uma parede de caixas de vime na fábrica).
- **Retrato da camada 9 pelas fichas**: 57 desafios, 56 segredos, 34 passagens, 21 lugares que ensinam, 21 poços e torres, 17 corações, 13 de história, 11 mirantes, 9 atalhos, 9 chefes.

### Esboço 4 — mais alto, mais fundo e mais coeso (2026-10-28)
Pedido do Rodrigo: mais salas, mais na vertical, e melhorar a lógica dos desafios de acesso a cada sala e a coesão de tudo.
- **Mais céu**: sete telas acima do antigo topo. A Copa Mais Alta e o Topo da Árvore Grande (o mapa inteiro visto de cima); o Feijão acima das nuvens; Onde a Neve Começa e o Ninho de Gelo sobre a estátua; a Caixa-d'Água, o Varal entre as Torres e o sino da Torre Parada; o Mar Mais Alto; o Cume do Pico; o Fuso do Céu e a Teia do Céu; a Torre de Vidro; o Moinho Alto.
- **Mais fundo: o Rio de Baixo.** A água é onde as camadas se encostam, e debaixo do mundo inteiro corre um rio. Ele nasce debaixo da Serra de Trás, enche o lago da Ilha pela cascata, passa pelo Lago sem Fundo (o reflexo mostra a toca por baixo) e pela Caverna das Gotas, e esquenta nas Fontes Quentes do vulcão (a água quente que a Gativara procurava). Chega-se por poços longos: a Escotilha no Túnel ARCA 9, a Chaminé de Lava, o Poço da Nascente (dezenove telas de queda), a Chaminé de Gelo. Mais a Câmara de Magma, a Câmara do Eco, os nichos do Nó, a Mina de Sal, a Toca Mais Funda e as Raízes da Figueira, o Poço da Adega e a Raiz da Dona Tronca. Camadas: o Abismo da Maré (3) e as Cavernas Pintadas (1).
- **Todo acesso tem um desafio.** Cada chave tem a frase do que ela vence (um vão largo, uma fresta do tamanho da cabeça, um paredão de gelo liso, uma queda alta demais, uma porta redonda), e as portas especiais têm a própria: "a ponte de galhos quebrou: um vão largo por cima do rio", "dezenove telas de queda", "uma grade no chão do túnel, do tamanho da cabeça", "uma onda que já passou: voltando no tempo ela volta e leva para cima".
- **O planar volta a abrir o mundo na hora**, como na Fase 1 original: do mirante, planando até a outra margem do rio.
- **O verificador ganhou três regras de coesão**: a regra Mega Man X (cada Dourada e cada poder abre passagens em pelo menos duas regiões), nenhuma sala a mais de 6 portas de um ponto de save, e toda região com o seu save. Elas pediram três consertos, todos de história: o pulo duplo também abre as pedras em pé dos Campos e a guarita da Morcevaca; o Feijão ganhou uma folha larga como cama e a copa um ninho velho; a Estação, um banco de concreto.
- **Modo "quando abre"** na página: cada sala pintada pelo passo do kit em que fica alcançável (dourado perto de casa, roxo no fim). Na camada 9: 24 salas no começo, +6 com o planar, +26 com o Lobovelha, +30 com a volta no tempo, +20 no Final da Toca, +62 com o gesto de bater.

### Esboço 3 — o mapa maior (2026-10-28)
Pedido do Rodrigo: aumentar o número de salas de cada versão do mapa, tudo fazendo sentido na história, no mesmo estilo. O mapa dobrou, e cada sala nova vem de alguém ou de algo das notas da bíblia.
- **Cinco faixas de profundidade**: céu, superfície, subsolo, **as Fundações** (nova: o concreto de quem veio antes, nunca explicado) e o nó debaixo do gelo do Pico. A progressão desce e sobe mais.
- **Bosque**: o Varal da Coalhoca, a Hortinha da Orcabelha, o Quintal (a flor de vento adormecida), o Ninho da Copa, o Riacho com a Vacaré, o Pé de Feijão em três trechos até o Lado de Fora (o Heitor dorme numa folha; na ponta, pela luneta, a segunda lua com uma luzinha), o Pomar Velho, o orelhão.
- **Raízes de Casa**: a Gruta do Mural, o Esconderijo do Ouriçapo, o Corredor das Cobrinhocas, a Lagoa debaixo do Riacho, a antessala do Covil (lã nos espinhos), o Porão e as Raízes do Feijão, que passam por baixo do rio e do muro.
- **As Fundações**: a Estação Debaixo de Casa, a Sala dos Terminais (`// oi ~`), o Túnel ARCA 9 (a placa), a Estação dos Batatus, as estações do Relógio e do Vulcão, o Poço Velho e as Galerias Antigas (letras que nenhum bicho lê; um relógio de bolso de outra vida).
- **Planície e Tocópolis**: o Iglu das Toupeiras, a Cabeça da Estátua, o **Galinheiro na Neve** (a Raposinha dá o Pé-de-gato), Debaixo do Gelo; a praça, a **Casa da Tia Toupaca** (o Faro; ela fia a lã), a Fila das Formigas (Tamanduformiga e Formigante), a Guarita da Morcevaca, a Mina de Gelo, o Lago Escuro (duas luas na água), o Escuro Total antes do Rei Caracólio.
- **Telhadópolis**: o Telhado da Cigarriga, o Camarim da Madame Cisnobra, o rastro da Cavalesma, o Chafariz da Elefoca, a Praça do Relógio, **a Rotativa d'O Novelo** (a máquina de jornal que imprime sozinha), a Torre em dois trechos, a Oficina de Tic e Tac, o Porto, a Fábrica em três salas, o Esgoto dos Passaratos, a Casa de Máquinas.
- **Monte Ronrom**: o Farol da Caranguejirafa, o Mirante da Corujaguar, a Encosta das Jabuticabras, o Ofurô da Gativara, o Mar no Céu em três trechos, o Coração do Vulcão (ele ronrona), as Cavernas dos Pipocos.
- **Pico**: a subida em três trechos, o Resgate do Carrapatu, os Fundos da Casinha (a caixinha de música), o Porão do Navio, as Quatro Leis em dois trechos, o Gelo que Canta, a Geleira Funda, o Lago Congelado; na Ilha, a Pedra Debruçada, a Horta Roxa e a Porta de Concreto.
- **Lado de lá**: um **mastro enferrujado em cada região** (Serra, Campos, Teias, Vidro, Horta), que faz bip; com as quatro antenas, são os nove de `9 de 9. aguardando.` Mais a Borda do Sal (o fim do mundo), o Salão do Trono Vazio, os Carretéis no Céu, a Sala das Lançadeiras, o Riacho dos Campos, as Tocas Fundas, o Mirante de Trás (a Casinha vista de costas), os Moinhos, o Celeiro e a Adega de Sementes.
- **Salas que só existem numa camada**: a Oficina do Robogato e a Neve Parada no Ar (8); o Pomar dos Filhotes e a Ruína da Torre (7); o Casulo, a Ponte de Fio do Pico à Serra e o Fio que Desce (6); o Céu de Espelho e o Salão do Rei (5); a Estufa sobre o Bosque (4); o Bolsão de Ar, o Estaleiro e as Comportas das Marés (3); a Oficina e a Mesa do Chá do Relojoeiro (2); a Neve de Séculos, o Jardim de Pedra e a Casa Funda da Sem Rosto (1); o Ninho da Traça, o Arquivo e Tudo o que se Desfez (Avesso).
- **A regra das trancas** entrou no verificador: cada sala-chave (23 delas) só se alcança depois da chave que a história pede, por qualquer caminho e por qualquer camada. Junto com ela: nenhuma sala sobreposta, nenhuma sala isolada, e todas as salas de todas as camadas alcançáveis com o kit completo.
- **Ajustes de coerência**: o Coelhato mora na Ilha (como na História); na camada 7 a casa dele está cheia dos filhotes dos filhotes de quem ele deixou. A Agulha fica na cômoda do quarto da toca parada. Os buracos da Traça no Avesso ficam em salas sem saída, para não cortar o mundo.

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
1. **Escopo.** Cerca de 2.950 telas na camada 9, mais as variações e as 23 salas próprias das outras camadas, é muito para uma pessoa. As camadas só cabem se reaproveitarem as salas de verdade; o peso de cada uma tem que ficar na região dela.
2. **Camadas que confundem.** O jogador precisa saber sempre em que camada está (cor, luz, som e um sinal no mapa de pausa) e como voltar.
3. **Puxar de baixo** é o sistema mais caro: o estado de cada camada fica salvo e muda as outras. Entra no motor na Etapa 2.
4. **Segredos cedo demais.** A camada 8 se abre no começo do jogo (o riacho). É um mistério bom, mas nada lá pode dar uma chave que quebre a história.
5. **Planar forte demais** (alerta antigo) pesa mais num mapa aberto.

## Perguntas em aberto
- Combate e editor (Parte 6).
- O nome e o desenho dos pontos de save.
- Os sonhos sem o cochilo: outro gatilho ou saem?
- Os nomes das salas do esboço são provisórios.
