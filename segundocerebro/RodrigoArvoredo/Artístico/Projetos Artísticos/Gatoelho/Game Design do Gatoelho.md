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
- **Idade da enteada** e se ela já joga algo (qual jogo, qual aparelho).
- **Dispositivo**: PC com teclado/controle ou tablet/celular com toque? (o alvo virou PC, mas toque mudaria o kit de movimentos).
- **Quem produz arte, animação e som**, e quanto tempo por semana o Rodrigo tem para o projeto.
- **Ordem das mecânicas** que o Gatoelho ganha e o que cada fase ensina — próxima conversa combinada.
