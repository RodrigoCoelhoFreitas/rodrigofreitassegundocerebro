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
