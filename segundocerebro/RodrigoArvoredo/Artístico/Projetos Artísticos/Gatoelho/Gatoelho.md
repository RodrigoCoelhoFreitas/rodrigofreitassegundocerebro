---
tags: [tronco, projeto, jogo, código]
---

# Gatoelho

Ramificação de [[Projetos Artísticos]]. **Gatoelho — Aventura em Patas e Orelhas**: jogo 2D de plataforma, ação e exploração criado por [[Rodrigo Coelho Freitas]], assinado pela [[Ludovic Studio]] (é a abertura do jogo). Também listado em [[Desenvolvimento]], por ser projeto de código.

Nasceu da vontade de fazer um jogo para a **enteada do Rodrigo** — mas sem ser "jogo infantil básico": acessível para criança, com qualidade de gameplay, animação e mundo que também agrade jogadores mais velhos. O personagem é o **Gatoelho**, mistura de gato com coelho, e a pergunta que guia tudo é: *"o que seria divertido fazer num videogame se o personagem fosse realmente meio gato, meio coelho?"*

## Notas do projeto
- [[Game Design do Gatoelho]] — conceito, princípios, mecânicas (feitas e em estudo), estrutura de mundo/fases, vida e vidas, decisões e perguntas em aberto.
- [[Arquitetura do Gatoelho]] — tecnologia escolhida e por quê, organização do código, sistemas, comandos, testes e armadilhas do ambiente.
- [[Direção de Arte e Som do Gatoelho]] — identidade visual, o boneco provisório, animação reaproveitável, áudio sintetizado provisório, pipeline de assets ainda por definir.
- [[Linha do Tempo do Gatoelho]] — o que foi feito, em ordem, desde a pré-produção.

## Repositório
- Pasta: `C:\Users\Gamer\Documents\projetos\gatoelho` (máquina nova). Git iniciado, **sem nenhum commit ainda** (em 2026-09-29).
- Executáveis Windows gerados em `gatoelho\release\`: `Gatoelho-Setup-0.1.0.exe` (instalador) e `Gatoelho-0.1.0-portatil.exe`.
- Também roda no navegador (`npm run dev` → http://localhost:5173) a partir do mesmo código.

## Estado em 2026-09-29
Protótipo jogável de ponta a ponta: abertura "LUDOVIC STUDIO" → título → **mapa do mundo** (estilo Super Mario World) → fase de testes → bandeira de chegada → resultado → volta ao mapa com o caminho seguinte revelado. Movimento com pulo, pulo duplo e planar; energia em corações + vidas; espinhos; HUD e minimapa; animações de personalidade; som e música sintetizados; controle de videogame; progresso salvo. Toda a arte ainda é **provisória** (formas geométricas) e só a Fase 1 (sala de testes) tem conteúdo.

**Próximo passo combinado:** conversar sobre **quais mecânicas básicas vêm primeiro e em que ordem o Gatoelho as ganha** — isso define o que cada fase ensina e onde ficam os primeiros segredos (ver [[Game Design do Gatoelho]]).
