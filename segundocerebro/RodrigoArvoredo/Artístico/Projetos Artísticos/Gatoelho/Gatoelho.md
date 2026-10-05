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
- [[Pesquisa de Fases do Gatoelho]] — como outros jogos constroem fases e o método de fases proposto.
- [[História e Mundos do Gatoelho]] — bíblia da história em camadas, mundos no modelo Donkey Kong Country 3, finais e missão paralela (rascunho).
- [[Linha do Tempo do Gatoelho]] — o que foi feito, em ordem, desde a pré-produção.

## Repositório
- Pasta: `C:\Users\Gamer\Documents\projetos\gatoelho` (máquina nova).
- GitHub (**privado**): `RodrigoCoelhoFreitas/gatoelho`, branch `main` — primeiro commit `32b63a9` em 2026-09-29.
- Executáveis Windows gerados em `gatoelho\release\`: `Gatoelho-Setup-0.1.0.exe` (instalador) e `Gatoelho-0.1.0-portatil.exe`.
- Também roda no navegador (`npm run dev` → http://localhost:5173) a partir do mesmo código.

## Estado em 2026-09-29
Protótipo jogável de ponta a ponta: abertura "LUDOVIC STUDIO" → título → **mapa do mundo** (estilo Super Mario World) → fase de testes → bandeira de chegada → resultado → volta ao mapa com o caminho seguinte revelado. Movimento com pulo, pulo duplo e planar; energia em corações + vidas; espinhos; HUD e minimapa; animações de personalidade; som e música sintetizados; controle de videogame; progresso salvo. Toda a arte ainda é **provisória** (formas geométricas) e só a Fase 1 (sala de testes) tem conteúdo.

**Próximo passo combinado:** conversar sobre **quais mecânicas básicas vêm primeiro e em que ordem o Gatoelho as ganha** — isso define o que cada fase ensina e onde ficam os primeiros segredos (ver [[Game Design do Gatoelho]]).

## Estado em 2026-09-30
- **Fase 1 de verdade: "Saindo da Toca"** substituiu a sala de testes no mapa. O Gatoelho começa só andando e pulando e **ganha as Orelhas Planadoras no meio da fase**; dali em diante a fase exige planar. Detalhes em [[Game Design do Gatoelho]].
- **Save e load**: três espaços de save, gravação automática, arquivos em disco no PC. Detalhes em [[Arquitetura do Gatoelho]].
- **Testes no repositório**: `npm test` roda 96 verificações sem abrir janela (pendência de ontem resolvida).
- GitHub: commits `e6261c2` (Fase 1 + habilidades + saves) e `52dd444` (testes), em `main`.
- A sala de testes continua existindo, fora do mapa (tecla `T` no mapa do mundo), com todas as habilidades.

**Próximos passos possíveis:** Fase 2 (que habilidade ou conceito ela ensina), primeiro inimigo, escalar paredes (já prometido por um segredo da Fase 1), e a arte definitiva do personagem.

## Estado em 2026-10-01
- **Visão e história**: jogo em camadas (a criança joga sem ler; a lore é para quem lê), o Embaralhamento e o laço dos Gatoelhos, arco curto v1. Ver [[História e Mundos do Gatoelho]] e [[Game Design do Gatoelho]].
- **Fases 1 e 2, versão 3**: cochilo no cantinho de sol no fim da fase, placas só com desenho, pólen embaralhador (pluma e escama), a Onda e as cenouras fujonas, gatoelhês, flores-sino, raízes e Cenoura Roxa. Método de fases em [[Pesquisa de Fases do Gatoelho]].
- **Banho de gráficos**: resolução real da tela, fundo em camadas com névoa e ruínas, paletas por fase, terreno e objetos arredondados com volume, Gatoelho com acabamento novo (silhueta original), câmera com chão fino. Catálogo de 64 vagas de sprite pronto para virar lista de encomenda. Ver [[Direção de Arte e Som do Gatoelho]] e [[Arquitetura do Gatoelho]].
- 241 verificações automáticas passando.

**Próximos passos possíveis:** mapa do mundo, HUD e painéis no estilo novo; mundos e chefes a partir da história; jogar com a enteada e ajustar o cochilo e as cores do pólen.

## Estado em 2026-10-01 (noite) — fases v4, cochilo e sonhos
- **Obstáculos sem cara de Mario**: os troncos flutuantes (plataformas elevadoras) saíram; o cogumelo-mola virou o **sapo-balão**; entrou o **galho-mola**; inimigos **não morrem** (caracol vira degrau na concha, passarato fica tonto). Ver [[Game Design do Gatoelho]].
- **Fases maiores**: Fase 1 com o Pomar Velho (212 → 248 colunas), Fase 2 com o Pomar dos Galhos-Mola (230 → 262), Horta Escondida maior (80 → 98).
- **Fim de fase**: o cochilo acontece num **cantinho com um objeto doméstico curioso** (cesto com novelo, pantufa de orelhas, relógio de bolso, xícara com óculos), com ritual de gato e depois um **sonho sem texto** cheio de pistas. Ver [[Direção de Arte e Som do Gatoelho]] e [[História e Mundos do Gatoelho]].
- **Pistas no fundo** (fumaça na serra, engrenagem, lenço, constelação, fenda, pegadas grandes) e gráficos mais limpos e nítidos.
- 266 verificações automáticas passando. Ainda não commitado ao escrever isto.
