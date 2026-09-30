---
tags: [meta, guia]
---

# Guia de Uso do Segundo Cérebro

Nota de orientação — **escrita pra mim mesmo (Claude)**, pra ter acesso e navegação mais fácil neste vault em sessões futuras. O Rodrigo pediu que este arquivo seja **alimentado ao longo do tempo**, conforme surgirem novas convenções ou decisões sobre como o vault funciona — não é estático.

## Onde tudo fica
Local canônico (git): `c:\Users\Dell\Documents\projetos\rodrigofreitassegundocerebro\segundocerebro\RodrigoArvoredo\` na máquina antiga; **desde 2026-09-29 também em `C:\Users\Gamer\Documents\projetos\rodrigofreitassegundocerebro\segundocerebro\RodrigoArvoredo\`** (máquina nova, onde o workspace tem napshift, napshift-web, este vault e, desde 2026-09-29, **gatoelho** — 1060crm e rodrigo-arvoredo-site não estão lá). Caminhos `C:\Users\Dell\...` citados nas notas antigas se referem à máquina anterior. Repo GitHub: `RodrigoCoelhoFreitas/rodrigofreitassegundocerebro`, branch `main`. Existe um local antigo (`Documents\segundocerebro\RodrigoArvoredo\`, sem git) — **congelado, não editar mais**, só histórico.

## Ponto de entrada
Tudo começa em **`Rodrigo Coelho Freitas.md`** (nó mestre, na raiz do vault) — ele linka as 6 ramificações de topo. Cada ramificação é uma pasta com uma **nota-tronco de mesmo nome** (padrão MOC — Map of Content), que por sua vez linka as notas/subpastas dela. Sempre que for procurar algo, começa pelo tronco da área provável, não por busca cega.

## As 6 ramificações
- **Pessoas** → Amigos/, Família/ (pessoas próximas do Rodrigo).
- **Profissional** → Desenvolvimento/ (os 3 repos de código + conhecimento técnico geral), Vendas/ (lado comercial da 1060 Brand).
- **Artístico** → música, bandas, escritas, projetos artísticos (nome artístico: Rodrigo Arvoredo).
- **Histórias** → memórias/marcos pessoais (ainda pouco preenchido).
- **Anotações** → registro corrente: Notas Soltas, Reuniões, Agenda, Diário, e **[[Atividades Claude Code]]** (log do que eu faço nos repositórios).
- **Conteúdos** → Referências (material consumido) e Marketing (produção 1060/NapShift) — ainda vazias.

## Convenções que valem pra qualquer nota nova
- **Frontmatter obrigatório**: `tags: [...]` sempre presente.
- **Acentuação correta** em nome de arquivo/pasta (`Família`, não `Familia`) — única exceção: `.NET` vira `DotNet.md`, porque o Obsidian esconde arquivo que começa com ponto (mesma lógica da pasta `.obsidian`).
- **Toda pasta tem nota-tronco de mesmo nome**, linkando pra dentro (filhos) e citando a ramificação-mãe (frase padrão: "Ramificação de" + link pra pasta-mãe).
- **Wikilink sempre que a informação já existe em outra nota** — não duplicar conteúdo, linkar. Zettelkasten: notas atômicas, bem conectadas.
- **Não duplicar na memória do Claude Code** o que é puramente pessoal/artístico (família, bandas, livros) — só o que afeta trabalho de código/negócio vai pra `.claude/memory/`. Ver `segundo_cerebro_localizacao.md` lá pra saber o que já foi sincronizado.

## Auditoria
Existe um script de checagem (link quebrado / nota órfã / frontmatter ausente / tronco incompleto), reescrito a cada sessão em `scratchpad` (pasta temporária por sessão, não persiste) — rodar depois de qualquer lote de edições estruturais. Critério de sucesso: zero em tudo.

## Git
Este vault é um repositório git como os outros do workspace (1060crm, napshift, napshift-web). **Mesma regra**: nunca commitar/dar push sem comando explícito do Rodrigo — só editar os arquivos e avisar que está pronto pra commit.

## Log de decisões estruturais
- 2026-07-08: reestruturação de 6 pastas orgânicas (Desenvolvimento/Vendas/Artes/Amigos/Família/Histórias) pra 6 categorias estáveis (Pessoas/Profissional/Artístico/Histórias/Anotações/Conteúdos) — detalhe completo em [[Reorganização do Segundo Cérebro]].
- 2026-07-08: migração pro repositório git `rodrigofreitassegundocerebro`, primeiro commit+push feito.
- 2026-07-08: removido README.md padrão do GitHub (sem conteúdo real); criados este guia e [[Atividades Claude Code]].
- 2026-09-29: atualização em lote das notas técnicas com o estado de setembro do NapShift, em seções datadas ("Estado em 2026-09-29", "Atualização 2026-09-29") em vez de reescrever o texto de julho — assim fica visível o que mudou e quando. Convenção pra próximas atualizações grandes: mesma forma.
- 2026-09-29: criada a primeira **subpasta dentro de Projetos Artísticos** — `Gatoelho/`, com nota-tronco [[Gatoelho]] e 4 notas atômicas (design, arquitetura, arte/som, linha do tempo). O jogo ficou em Artístico (é criação da Ludovic Studio) e não em Profissional/Desenvolvimento, mas [[Desenvolvimento]] linka pra ele por ser projeto de código. Padrão pra projetos grandes daqui pra frente: pasta própria + tronco + notas por assunto, em vez de uma nota gigante.
- 2026-07-09: Rodrigo passou um snapshot da memória do Claude do Eduardo (`C:\Users\Dell\Documents\referenciasclaudinho`) pra configurar minha operação e enriquecer o vault. Criadas [[Infraestrutura de Sites 1060]] e [[Ferramentas 1060]]; [[Geração de Sites via IA]] teve as pendências técnicas resolvidas; adendos em [[Produto Sites]] (migração HostGator), [[1060crm]] (commits recentes) e [[NapShift Backend]] (primeiro cliente real, AEMJS). Regras comportamentais do Eduardo (acentuação, design system próprio, tinify, self-hosted) foram pra `.claude/memory/` (feedback), não pro vault — são instrução de operação, não conhecimento factual.
