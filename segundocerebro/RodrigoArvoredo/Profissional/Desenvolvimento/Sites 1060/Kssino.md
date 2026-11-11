---
tags: [desenvolvimento, sites, cliente, código]
---

# Kssino

Ramificação de [[Sites 1060]]. Site do Kssino, boletim de surf da praia do Cassino (Rio Grande/RS) desde 2008: hub da comunidade com boletim das ondas, câmera ao vivo, picos, fotos, escola de surf, loja e parceiros. Cliente: Touguinha. Repo `1060brand/kssino`, clonado em `projetos\kssino` em 2026-11-10. No ar em **https://kssino.com** desde 2026-10-08, substituindo o WordPress de `surfkssino.com` na HostGator.

É o maior site da 1060 nesta máquina (50 commits, ~1.300 URLs) e o melhor exemplo de **site dinâmico com painel de verdade** e de **migração de WordPress**. Padrão geral em [[Padrão de Sites 1060]].

## O que tem

- Nasceu do `site-dinamico-template` ([[Templates de Site 1060]]; o README ainda é o do template).
- Público em `(site)/`: boletim (lista, paginação estática, arquivo por ano/mês, página por slug), fotos (ensaios com paginação), picos (mapa), câmera ao vivo, escola de surf, loja, parceiros, contato, privacidade, `/app` e `/offline`. Rota `[...legado]` e `/legado/p/[id]` atendem URLs do WordPress (`/?p=N`); `/ir/[id]` conta clique de anúncio.
- Painel mobile-first: boletins, fotos, parceiros (Gold e Verificado, peças, vigência, destino do clique, popup, resultados), push, loja, configurações.
- **PWA com push** (`web-push`, VAPID checado no `prebuild`): 1.508 inscritos migrados do plugin Perfecty do WordPress; as inscrições vivem na origem antiga, então os caminhos de push do host antigo nunca podem levar 301.
- **Anúncios**: Gold mora ao lado do conteúdo, nunca acima; Verificados numa faixa rotativa; páginas de parceiro sem anúncio. Métricas diárias de impressão e contato, com robôs e navegadores automatizados excluídos.
- Migração (2026-09-07): 1.199 boletins, 8.063 fotos e 1.508 inscritos, por scripts `npm run migrar:*` (variantes, R2, conteúdo, postmeta, push, picos, verificar, delta, resgate).

## Design ("Arrebentação", redesenho de 2026-09)

Mundo: a arrebentação do Cassino vista de cima. Recusa o sulco do surf (turquesa, pôr do sol, coqueiro, fonte pincel) e o lookbook preto e branco. Identidade mantida: Druk Wide Bold (display, caixa alta) + Inter, `#0075aa`, `#002d3d`, `#00a0d0`. Forma única: paralelogramo de 23° (a inclinação das letras do logo); sem raio no resto. Assinaturas: o slider da home troca de destino com uma "lavada" de espuma; na escola, a prancha atravessa a arrebentação com a rolagem. Divisas de seção são linhas de espuma vivas, nunca borda reta. Peças de movimento reaproveitáveis em `components/movimento/` (Espuma, GradienteMar, FaixaCorrida, Paralaxe, Revelador, `useQuadro`).

## Lições que viraram padrão

- **Economia na Vercel** (`docs/economia-vercel.md`, 2026-10-19): o Kssino era 83% do custo do time (US$ 4,17 de 5,04 por semana; 98% das invocações, 99% das ISR Writes). Correções: matcher do `proxy.ts` com uma entrada por responsabilidade; vigência de anúncio filtrada no navegador em vez de entrar na chave do cache; tag por boletim (a tag única refazia 1.199 páginas a cada publicação); rede de revalidação de 7 dias. Plano declarado: levar essas regras para os templates e para `1060/docs/sites/infraestrutura-sites.md`.
- **Cutover sem o host antigo** (`docs/cutover.md`): a HostGator venceu por volta de 07/10 e não foi renovada; o lançamento de 08/10 aconteceu sem congelar o WordPress, e ficaram de fora os boletins de 29/09 até a queda e os inscritos depois de 07/09. Lição: lançar antes do vencimento do host antigo.
- `AUTH_URL` apontando para outro host quebra o login do painel; com `AUTH_TRUST_HOST` o Auth.js usa o host da requisição.
- Backup diário do banco no Easypanel → R2 `1060-backups` (restauração testada em 28/09).
- Sem `next build` local: o `.env.local` aponta para o banco de produção.

## Relacionamentos

- [[Produto Sites]] — mais um site do portfólio.
- [[Infraestrutura de Sites 1060]] — Postgres compartilhado, R2 (`cdn.kssino.com`, mantido `cdn.surfkssino.com` pelos 8.063 redirects de mídia), região `gru1`.

*Leitura do código e dos docs: 2026-11-10. Estado vivo do cliente no vault do Eduardo (`1060 Brand/Clientes/Kssino/`), fora deste.*
