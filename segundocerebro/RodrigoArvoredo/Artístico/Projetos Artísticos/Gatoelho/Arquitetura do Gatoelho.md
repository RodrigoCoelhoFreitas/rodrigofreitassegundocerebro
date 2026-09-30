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
