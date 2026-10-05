---
tags: [projeto, jogo, código, arquitetura]
---

# Arquitetura do Gatoelho

Ramificação de [[Gatoelho]]. Decisões técnicas, organização do código e como rodar/testar. Contexto de design em [[Game Design do Gatoelho]].

## Stack (decidida em 2026-09-29)
- **TypeScript** — nativo do navegador, natural para a experiência do Rodrigo em Java/.NET/Node (ver [[Backend]]), tipagem ajuda em jogo, e é onde o Claude consegue ajudar em 100% (tudo é texto). Alternativa considerada: Godot/GDScript (bom editor visual, mas build web pesada e trabalho em editor que o Claude não enxerga).
- **PixiJS 8** (renderização) com **arquitetura própria** — escolhido em vez de Phaser porque o controlador de movimento e a câmera, que são a alma do jogo, seriam escritos à mão de qualquer jeito. Defold e Unity também foram avaliados (Unity descartado pelo peso do build web).
- **Vite 8** (dev server e build) · **TypeScript 7** (versão nativa; `tsc --noEmit` para checagem).
- **Electron 44 + electron-builder** — o jogo virou **aplicativo de PC com ícone** (pedido do Rodrigo), mantendo a versão de navegador do mesmo código. Electron escolhido em vez de Tauri (leve, mas depende do navegador do sistema, com diferenças de áudio/controle/desempenho) e NW.js (comunidade menor).
- Recomendações ainda não aplicadas: **LDtk** para editar fases (hoje as fases são ASCII) e **Spine** para animação por esqueleto (pago), com física nas orelhas e no rabo.

## Comandos
- `npm run dev` — navegador com recarga automática (http://localhost:5173).
- `npm run desktop` — gera o build e abre a janela do jogo; `npm run desktop:dev` — janela com recarga (precisa do `dev` rodando).
- `npm run dist:win` — gera instalador e `.exe` portátil em `release\` (~111 MB, quase tudo é o Electron; o jogo tem < 1 MB).
- `npm run typecheck` / `npm run build`.
- O `.exe` não é assinado: o Windows mostra "O Windows protegeu o computador" → Mais informações → Executar mesmo assim.

## Princípios da arquitetura
- **Simulação separada do render**: lógica a 60 passos fixos por segundo (`FixedStepLoop`), render interpola — igual em monitor de 60 Hz ou 144 Hz.
- **Input por ações** (`jump`, `left`, `confirm`…), nunca por tecla. Uma tecla pode disparar várias ações (↑ pula na fase e sobe no menu). Teclado + **controle de videogame** (Gamepad API, layout padrão Xbox/PlayStation) somados, sem configurar.
- **Movimento cinemático escrito à mão**, sem motor de física; colisão AABB contra tiles resolvida por eixo.
- **Todo número de "sensação" em `src/config/`** (movimento, regras de vida, resolução).
- **A lógica não sabe desenhar**: `Player` tem estado e física; `PlayerView`/`GatoelhoRig` desenham. Por isso dá para testar o jogo inteiro sem abrir janela.
- **Eventos em vez de acoplamento**: o `Player` anuncia `jump`, `doubleJump`, `glideStart`, `land` a cada passo; a cena da fase decide que som tocar.
- **Adicionar uma fase não exige reprogramar**: fase = entrada em `level/levels.ts` + ponto em `world/worlds.ts`.

## Organização do código (`src/`)
- `core/` — loop de passo fixo, input (teclado + controle), matemática/easing.
- `config/` — `display.ts` (960×540 lógicos, tile 32 px), `movement.ts` (pulo por altura + tempo até o ápice → gravidade calculada), `rules.ts` (energia, vidas, dano).
- `physics/` — colisão contra a grade de tiles.
- `level/` — `TileMap` (sólido, espinhos, partida `P`, chegada `G`), `levels.ts` (lista de fases; `map: null` = "em breve"), `testLevel.ts`.
- `player/` — `Player` (movimento, pulo duplo, planar, empurrão), `Health` (energia + invulnerabilidade), `abilities.ts` (habilidades ligáveis), `playerClips.ts` + `PlayerAnimation.ts` (animação).
- `animation/` — **genérico**: clipes como dados (canais + quadros-chave com suavização `smooth`/`linear`/`step`) e `Animator` em camadas (base + sobreposições que se somam + mistura na troca).
- `game/` — casco (`Game.ts`), `Session` (vidas da partida), `damage.ts`, `goal.ts`, `progress.ts` (salvo em localStorage), `settings.ts` (volumes, depuração, tela cheia), `format.ts`.
- `scenes/` — `SceneManager` (transições fade e **íris** estilo Super Mario World) e as telas: Splash (LUDOVIC STUDIO), Title, Settings, **WorldMap**, Gameplay (com pausa e resultado).
- `world/` — mapa do mundo: dados (pontos, caminhos, **condições `completed`/`flag`**, caminhos `secret`), regras (`graph.ts`: alcançáveis, rota, direção apertada) e desenho.
- `render/` — `GatoelhoRig` (boneco movido por pose, usado na fase, no título e no mapa), fase, bandeira.
- `ui/` — HUD (corações com preenchimento parcial), minimapa, menu reutilizável (teclado + mouse + controle, itens ajustáveis), confete, fundo de menus.
- `audio/` — `AudioEngine` (barramentos de música/efeitos, volume, "abaixar" na pausa), efeitos por nome (`sounds.ts`), músicas em notação de texto (`songs.ts`) tocadas por `MusicPlayer` com agendamento à frente.
- `electron/main.cjs` — só a janela; tela cheia (F11/Alt+Enter) é tratada pelo jogo, igual no navegador.

## Testes e verificação
- **Simulações sem janela** (via `vite.ssrLoadModule`): movimento (8 casos), pulo duplo/planar (10), vida (7), animação (10), chegada/eventos/músicas (8), mapa do mundo (10) — **53 verificações passando em 2026-09-29**. ⚠️ Esses scripts ficaram em pasta temporária da sessão (`%TEMP%`), **não estão no repositório** — pendência: transformá-los em testes de verdade no projeto.
- **Ponta a ponta no Electron**: script que abre o jogo, aperta teclas como um jogador, tira prints, **mede o áudio que sai** (AnalyserNode via preload) e **simula um controle** (sobrescrevendo `navigator.getGamepads`).
- Bugs reais achados pelos testes: plataforma na altura da cabeça virava parede; erro de integração no pulo (130 em vez de 136 px); orelhas abertas por um quadro ao pousar; passar planando por cima da bandeira sem terminar a fase.

## Armadilhas do ambiente (máquina Gamer)
- Nas sessões do Claude Code dentro do VS Code vem `ELECTRON_RUN_AS_NODE=1` — o Electron roda como Node puro. Rodar com `env -u ELECTRON_RUN_AS_NODE`.
- O observador de arquivos do Vite segurava `release\electron.exe` aberto e o electron-builder falhava com EPERM — resolvido ignorando `release/` no `vite.config.ts` (a primeira suspeita, o Defender, estava errada).
- Janela invisível do Electron roda a poucos quadros por segundo; e com o monitor desligado/bloqueado, `capturePage` falha ("display surface not available") — para prints de teste, usar `offscreen: true` + `setFrameRate(60)`.
- `vite.config.ts` usa `base: './'` para o mesmo build funcionar na web e aberto do disco pelo Electron; `pixi.js` fica em devDependencies para não ser copiado duas vezes para dentro do `.exe`.

## Atualização 2026-09-30

### Fases e objetos
- Formato ASCII da fase ganhou tiles e entidades (legenda em `TileMap.parse`): `=` galho, `c` cenoura, `C` Cenoura Dourada, `D` item de habilidade, `S` placa, `K` checkpoint, `W` flor de vento, `T` toca. Placas e Douradas são numeradas da esquerda para a direita.
- `level/bosque1.ts` — a Fase 1, gerada por um script de design e mantida como texto. `level/levels.ts` guarda também os textos das placas e a habilidade que a fase ensina.
- `game/LevelObjects.ts` (lógica: o que foi pego, checkpoint ativo, placa próxima → eventos) separado de `render/LevelObjectsView.ts` (desenho). `render/ForestBackdrop.ts` = fundo em camadas (parallax). `ui/AbilityBanner.ts` = anúncio de habilidade, reaproveitando o boneco e as animações.
- Física: `TileMap.windZones` + `inWind`; planar dentro do vento leva `vy` até `-windRiseSpeed`. Galhos só colidem quando os pés estavam acima do topo no passo anterior.
- Atalhos de desenvolvimento novos: `N` próximo checkpoint, `T` (no mapa) sala de testes.

### Saves
- `game/progress.ts` virou dados puros (`toData`/`fromData`), sem saber onde são guardados; `completeLevel` é o único ponto que grava o resultado de uma fase (habilidades, Douradas, recordes) de uma vez.
- `game/saves.ts` — `SaveManager`: 3 espaços, qual está em uso, gravação automática (toda `progress.save()` regrava o espaço), tempo de jogo e data, migração do progresso único antigo para o Espaço 1, arquivo corrompido tratado como espaço vazio.
- Armazenamento por interface (`SaveStorage`): no navegador, `localStorage`; no PC, **arquivos JSON** em `%APPDATA%\Gatoelho\saves\jogo-N.json`, gravados de forma atômica (arquivo temporário + troca).
- `electron/preload.cjs` expõe só `read/write/remove` por `contextBridge`; `electron/saves.cjs` valida o número do espaço antes de virar nome de arquivo — a página do jogo continua isolada do sistema.
- `scenes/SaveSelectScene.ts` (escolha do jogo) e `ui/SaveIndicator.ts` (aviso "Jogo salvo", por cima de qualquer tela).

### Testes
- As simulações agora moram no repositório: `tests/sim/*.mjs`, rodadas por `npm test` (`tests/run.mjs`). **96 verificações** em 2026-09-30: pulo (8), pulo duplo e planar (10), vida (7), animação (10), chegada e músicas (8), mapa do mundo (10), **robô da Fase 1 (28)**, saves (15).
- O robô da Fase 1 joga cada trecho com comandos programados e prova três coisas: o trecho é possível com o kit certo, os trechos de planar são impossíveis sem planar, e os segredos só abrem do jeito previsto.
- Os testes de ponta a ponta no Electron (prints, áudio, controle simulado, saves em arquivo) continuam como scripts avulsos, fora do repositório.

## Atualização 2026-09-30 (noite) — sistemas das fases v3
- **Mapa (TileMap)**: tile novo `R` (raízes, sólidas até `setGatesOpen`); entidades `L`/`F` (pólen), `1`–`4` (flores-sino), `Q` (mural), `q` (pedra antiga), `u` (Cenoura Roxa), `r` (cenoura fujona), `O` (Onda). Objetos debaixo d'água continuam dentro dela.
- **Player**: `scramble` (pólen ativo, com tempo) e `swimming`; pólen-pluma muda a gravidade, pólen-escama troca a física por nado. Parâmetros em `config/scramble.ts`.
- **Lógica nova, sem desenho** (testável): `game/nap.ts` (cochilo), pólen/sinos/Onda/Cenoura Roxa em `LevelObjects`, cenouras fujonas em `LevelActors`, `purpleCarrots` no progresso.
- **Desenho novo**: `SunspotView` (substitui `GoalView`), `pictograms.ts` (placas), `glyphs.ts` (gatoelhês), `palettes.ts` + `ForestBackdrop` com paleta, sol e antena, `ScrambleFx` (filtro de cor `ColorMatrixFilter` no fundo+mundo, ondas e pólen), barbatanas e pena no `GatoelhoRig`. O confete saiu.
- **Testes**: 238 verificações (`npm test`), com arquivos novos `embaralhamento-e-cochilo`, `fase-bosque1-camadas` e `fase-bosque2-camadas`. O robô-criança agora pula espinheiros como se fossem buracos.
- **Gancho de desenvolvimento**: só com `npm run dev`, a fase fica em `window.__fase` (para prints automáticos colocarem o Gatoelho em qualquer lugar e ativarem pólen). Não existe no build final. Script de prints (Electron offscreen contra o servidor do Vite) guardado fora do repo.
- Scripts de design atualizados: `tools/gerar-bosque1.mjs` e `gerar-bosque2.mjs` (Fase 1 agora 212×22; Fase 2 230×28).

## Atualização 2026-10-01 — banho de gráficos
- **Resolução real**: o jogo pensa em 960×540, mas o renderer desenha na resolução da tela (`fitResolution` em `game/Game.ts`, refeita ao redimensionar e em tela cheia; teto 3×). A arte é vetorial, então fica nítida em qualquer tamanho.
- **`src/art/`** (novo): `paint.ts` (degradês reaproveitáveis com `FillGradient`, mistura de cores, contorno "ink", caminhos suaves, `arcLine`), `textures.ts` (texturas geradas uma vez: brilho aditivo, sombra de contato, névoa, vinheta), `palettes.ts` (luz de cada fase: céu, névoa, camadas, grama, terra, água, partículas), `sprites.ts` (catálogo de 64 vagas de sprite).
- **Armadilha do Pixi 8 descoberta**: `arc()` sem `moveTo` liga o começo do arco ao último ponto com uma reta (riscos atravessando a tela). Usar sempre `arcLine`.
- **Câmera** (`camera/Camera.ts`): chão fino na tela (Gatoelho a ~74% da altura), segura a altura do último chão nos pulos e voos, desce ao cair rápido ou nadar, suavização vertical, pode subir acima do topo da fase (céu).
- **Fundo** (`render/ForestBackdrop.ts`): céu, halo do sol, nuvens, pássaros, montanhas e morros com fio de luz, ruínas, duas linhas de copas com cipós, névoa e partículas. Usado também pelos menus (`ui/Backdrop.ts`). `render/Foreground.ts` ficou só com a vinheta.
- **Lista de sprites**: `node tools/listar-sprites.mjs > docs/sprites.md`; o teste `catalogo-de-sprites` garante que cada vaga aponta para um desenho que existe.
- **Prints automáticos**: Electron offscreen contra o servidor do Vite, usando o gancho `window.__fase` (só em modo dev) para posicionar o Gatoelho e trocar de fase. Scripts guardados fora do repo.
- 241 verificações em `npm test`.

## Atualização 2026-10-01 (noite) — fases v4
- **TileMap**: `M` agora é o sapo-balão (`entities.frogs`); `J`/`j` é o galho-mola (raiz na borda esquerda/direita do tile, 4 tiles de comprimento; `entities.branches`); `m`/`v` (troncos flutuantes) foram removidos.
- **`game/LevelActors.ts`** reescrito: "carregadores" genéricos (galho-mola e concha de caracol) com `moveCarriers` antes do jogador e `resolveCarriers` depois; galho = mola amortecida (`sag`, `speed`, `lift` com memória curta para alargar a janela do arremesso; `branchBend` exportado); sapo-balão = cama elástica (`Player.fallHeight` × `frogKeep` + `frogPush` com o pulo apertado, teto `frogMaxHeight`); inimigos com `stun` (caracol na concha, passarato tonto) em vez de sumir. Eventos novos: `fling`, `creak`, `recover`, `bounce.high`.
- **Player**: `apexY`/`fallHeight` (de que altura vem caindo) e `catapult(extra)`.
- **Cochilo**: `game/nap.ts` com as fases `approach → sniff → knead → turning → lying → sleeping` (para ao lado do objeto e pula para o meio); `PlayerAnimation.nap(phase)`; clipes `sniff`, `knead`, `turn`, `lieDown`, `sleep`; canais novos `bodyTilt` e `mouth` no `GatoelhoRig`.
- **`render/NapSpotView.ts`** substitui o `SunspotView`: três camadas (luz atrás do terreno, objeto atrás do Gatoelho, frente do objeto na frente dele) e `bedLift` (quanto ele sobe ao deitar dentro do objeto).
- **`render/DreamView.ts`**: o sonho (quatro cenas) por cima da fase, por baixo do HUD/resultado; o resultado aparece quando o sonho termina ou é pulado. `SceneManager` ganhou `color` nas transições (o "acordar" azul-noite).
- **`LevelDef`**: `nap`, `secretNap` (objeto + sonho) e `clues` (pistas no fundo: `fumaca`, `lenco`, `engrenagem`, `constelacao`, `fenda`, `pegadas`), lidas por `ForestBackdrop` e `DecorView`.
- **Nitidez**: `GraphicsContextSystem.defaultOptions.bezierSmoothness = 0.85` (em `Game.create`) e câmera arredondando ao pixel da tela (`SceneContext.resolution`).
- **Testes**: 266 verificações. Novos: concha-degrau, sapo com embalo (Fase 1 e rio da Fase 2), galho-mola (janela do arremesso, galho + pulo duplo), ritual do cochilo. Os robôs procuram atores pela posição (a ordem das listas é a de leitura do mapa, linha por linha — o "primeiro caracol" pode não ser o da esquerda).
- Prints automáticos v4 e a folha de recortes (montagem de vários prints) ficaram na pasta temporária da sessão.
