# Prancheta

Simulador de carreira de treinador de futebol. Você assume um clube, enfrenta imprevistos a cada temporada (lesão, jogador pedindo para sair, proposta de outro clube), mexe no mercado, nos patrocínios e na escalação, e tenta virar lenda do banco de reservas.

Arquivo único, sem build e sem dependências: HTML, CSS e JavaScript puros, com as fontes (Barlow e Barlow Condensed) embutidas. Funciona offline.

## Como rodar

Abra `index.html` no navegador. Para publicar, use o GitHub Pages (Settings > Pages > Deploy from a branch > `main` / root) ou a Vercel apontando para a pasta raiz.

## O que tem

- Três modos de jogo: Rápido, Intermediário e Pro.
- Imprevistos por temporada com custo, risco e consequências na moral, no caixa e na diretoria.
- Mercado com compra, venda, jogadores livres, pré-contrato e negociação com chance de aceite.
- Patrocínio master e fornecedor esportivo, folha salarial ligada ao caixa.
- Esquemas táticos (inclusive com três zagueiros), escalação por jogo, tabela de classificação e sala de troféus.
- Placar (Scorebug) e últimos 5 jogos (FormGuide). A forma atualiza a cada 5 jogos no Rápido, a cada 3 no Intermediário e a cada jogo no Pro; passe o mouse em V, E ou D para ver as estatísticas.
- Layout responsivo: no celular, abas Jogo e Time (com Escalação e Tabela).

## Design system

O visual segue o design system "Prancheta" (tema Noturno por padrão, Diurno conforme o sistema). Regras, tokens e componentes estão em [`docs/design-system-prancheta.md`](docs/design-system-prancheta.md). Ordem de mudança: design system, documento, jogo.

## Teclado

Nos imprevistos, as teclas 1 a 4 escolhem as opções.
