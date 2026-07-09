---
tags: [anotações, meta]
---

# Reorganização do Segundo Cérebro

Ramificação de [[Notas Soltas]]. Registro do processo de construção e reestruturação deste vault — a própria estrutura em que esta nota vive é o assunto dela.

## Linha do tempo

- **2026-07-07**: primeira estruturação real do vault. Nó mestre criado, ramificado em 6 pastas temáticas que foram nascendo conforme o assunto aparecia na conversa: `Desenvolvimento`, `Vendas`, `Artes`, `Amigos`, `Família`, `Histórias`. Convenção adotada desde o início: cada pasta tem uma nota-tronco do mesmo nome (padrão MOC — Map of Content), que linka pra dentro (as notas da área) e pra fora (nó mestre).
- **2026-07-08 (manhã)**: auditoria completa do vault (script próprio, checando links quebrados, notas órfãs, frontmatter ausente, completude de tronco) — vault já estava limpo, só com pequenas inconsistências de acentuação em nomes de pasta/arquivo corrigidas (`Familia`→`Família`, `Historias`→`Histórias`, `Projetos Artisticos`→`Projetos Artísticos`).
- **2026-07-08 (tarde)**: reestruturação de fundo pedida pelo Rodrigo — trocar as 6 pastas temáticas orgânicas por 6 categorias de alto nível mais estáveis e genéricas: **Pessoas, Profissional, Artístico, Histórias, Anotações, Conteúdos**. Mapeamento:
  - `Pessoas/` ← `Amigos/` + `Família/` (mantidas como subpastas, não fundidas).
  - `Profissional/` ← `Desenvolvimento/` + `Vendas/`.
  - `Artístico/` ← rename direto de `Artes/` (incluindo o arquivo-tronco `Artes.md`→`Artístico.md`).
  - `Histórias/` — sem mudança, só confirmada como irmã das outras 5.
  - `Anotações/` e `Conteúdos/` — **categorias novas**, sem conteúdo prévio pra migrar. Definidas em conversa com o Rodrigo: Anotações cobre notas soltas, reuniões, agenda e diário; Conteúdos cobre referência consumida (livros/artigos/vídeos) e material de marketing/produção da 1060/NapShift, em subpastas separadas.
- **2026-07-08 (mesma tarde)**: migração do vault inteiro pra um repositório git próprio — `rodrigofreitassegundocerebro` (GitHub, branch `main`), nesse caminho aqui dentro (`segundocerebro/RodrigoArvoredo/`). Local antigo (`Documents\segundocerebro\RodrigoArvoredo\`, sem git) congelado, mantido como histórico mas sem receber mais edições.
- **2026-07-08 (fim do dia)**: primeiro commit e push do vault pro GitHub, sob comando explícito do Rodrigo — precisou antes configurar a identidade git da máquina (`user.name`/`user.email`), que nunca tinha sido feita.

## Por que isso importa
A estrutura de um segundo cérebro não é neutra — ela molda onde informação nova vai parar e o quão fácil é achá-la depois. A mudança de "pastas que nascem conforme o assunto aparece" pra "categorias fixas de alto nível" é uma aposta em estabilidade de longo prazo sobre flexibilidade de curto prazo: qualquer nota nova, de qualquer assunto, já tem um lugar óbvio pra cair, em vez de potencialmente precisar de uma pasta nova toda vez.

## Relacionamentos
- [[Notas Soltas]] — esta é a primeira nota real dessa subpasta (as outras 3 de [[Anotações]] — Reuniões, Agenda, Diário — ainda estão vazias).
