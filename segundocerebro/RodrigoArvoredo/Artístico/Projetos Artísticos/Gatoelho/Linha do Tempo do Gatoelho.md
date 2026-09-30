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
