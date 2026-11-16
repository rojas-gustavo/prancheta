# Prancheta — Design System (contexto do projeto)

Toda alteração visual no jogo Prancheta segue este documento.

- Design system (fonte da verdade): https://claude.ai/artifact/D6i9cE4wQfr6VH3FVDGKSx
- Jogo publicado: https://claude.ai/artifact/XbKY3Jd56pxNqJb4ZFXCjy
- Decisões e pesquisa: https://claude.ai/artifact/DRZZgD9Guk1W8rtBzNsd8b

Se este documento e o design system divergirem, vale o design system: leia `project/README.md` e `project/tokens.json` dele antes de mexer no visual do jogo, e atualize este documento em seguida.

## Como testar um ajuste

1. **Pelo design system (mais rápido).** Abra o link do design system, edite o token (cor, tamanho, espaçamento) na própria página e veja os 13 componentes mudarem na hora, nos temas Noturno e Diurno. Nada muda no jogo até você pedir.
2. **Pelo chat.** Peça "testa `accent` = #valor" (ou qualquer token/regra). O ajuste deve ser mostrado primeiro em uma prévia dos componentes afetados, com o contraste recalculado, antes de ser aplicado.
3. **Ao aprovar.** Peça "aplica". A ordem é sempre: design system → este documento → jogo.

Regras para quem faz o ajuste:

- Mude valores só nos tokens (bloco abaixo); nunca cor ou tamanho fixo dentro de um componente.
- Depois de mudar uma cor, recalcule o contraste: texto ≥ 4,5:1 sobre `bg`, `surface` e `surface-2`; bordas de controle ≥ 3:1; nos dois temas.
- Um ajuste por vez, com antes e depois lado a lado.

## Tokens (bloco único para editar e testar)

```css
:root, [data-theme="dark"] {            /* Noturno — tema principal */
  --bg:#0b1210; --surface:#141d1a; --surface-2:#1d2925;
  --line:#2f3f39; --line-strong:#6a8077;
  --ink:#f4f6f1; --mut:#a7b6ae;
  --accent:#c6ff3d; --on-accent:#0b1210;
  --gold:#ffc93c;
  --danger:#ff6b4a; --on-danger:#0b1210;
  --info:#5cc8ff; --home:#5cc8ff; --away:#ffa23a;
  /* iguais nos dois temas */
  --pitch:#1f9d55; --pitch-alt:#1a8a4a; --chalk:#f4f6f1; --boot:#0b1210;
  --tier-bronze:#d1936a; --tier-silver:#cfd6da;
  --tier-gold:var(--gold); --tier-elite:var(--accent);
}
[data-theme="light"] {                  /* Diurno */
  --bg:#f1f4ec; --surface:#ffffff; --surface-2:#e4e9df;
  --line:#cdd5cc; --line-strong:#6d7c74;
  --ink:#0b1210; --mut:#4a5a52;
  --accent:#0b6b33; --on-accent:#ffffff;
  --danger:#b92d14; --on-danger:#ffffff;
  --info:#075f9c; --home:#075f9c; --away:#a14e00;
}
:root {
  --font-display:"Barlow Condensed","Arial Narrow",sans-serif;
  --font-body:Barlow,system-ui,sans-serif;
  --space-1:4px; --space-2:8px; --space-3:12px; --space-4:16px;
  --space-5:24px; --space-6:32px; --space-7:48px;
  --radius-0:0px; --radius-sm:2px; --radius-pill:999px;
  --slant:-10deg; --cut:10px; --cut-lg:16px;
  --stroke-1:1px; --stroke-2:2px; --stroke-3:3px;
  --lift:0 8px 24px #00000066;
}
```

Fontes: `Barlow Condensed` 600, 700 e itálicos 700, 800, 900; `Barlow` 400, 500, 600, 700. No jogo elas vão embutidas em base64 (woff2, subset latin), sem depender de internet.

## Regras de uso

**Cor**
- Três planos: `bg` → `surface` (cartões) → `surface-2` (opções dentro do cartão). Texto em `ink`, apoio em `mut`.
- `accent` é do jogador: botão que avança, aba ativa, linha do seu clube, vitória. No máximo um preenchimento `accent` grande por tela.
- `gold` é dinheiro e título, sempre preenchimento com texto `boot`. `danger` é risco e perda. `home` azul × `away` laranja para confrontos.
- Cor nunca vai sozinha: V/E/D, ▲/▼/●, "▼ CRÍTICO", losango para fora de posição. No Diurno, `accent` e `danger` têm a mesma luminosidade.
- Foco de teclado: contorno sólido de 3px em `ink`, afastado 3px.

**Tipografia**
- Títulos: Barlow Condensed itálica 800–900, caixa alta. Tamanhos 96 / 64 / 40 / 28px.
- Números (placar, nível, preço): mesma família, reta, peso 700, tabulares. Tamanhos 72 / 40 / 24 / 16px.
- Rótulo (overline): condensada reta 13px, caixa alta, espaçamento 0.12em.
- Texto: Barlow 16px/1.5; rótulos 14px; mínimo 12px. Nunca texto corrido em caixa alta.

**Forma**
- Ação e placar inclinam `--slant`; o texto dentro volta ao eixo.
- Cartões retos com canto superior esquerdo chanfrado (`--cut`, `--cut-lg`).
- Redondo só ficha de jogador e pips. Sem gradiente; sem sombra em cartões.

**Voz**
- "Você", português do Brasil, vocabulário de arquibancada. Títulos específicos com o nome do envolvido. Opções começam pelo verbo. Dinheiro como `€12M`. Sem emoji.

## Componentes (classes `pr-`, em `components/bundle.css` do design system)

| Componente | Classe base | Onde usar |
|---|---|---|
| Button | `pr-btn` (`--ghost`, `--danger`, `--sm`) | Ação que avança; um primário por tela |
| TabBar | `pr-tabs` | Navegação no celular (abaixo de 820px) |
| RatingBadge | `pr-ovr` (`data-tier`) | Nível do jogador com a faixa escrita |
| PlayerCard | `pr-player` | Ficha: nível, posição, idade, potencial, 6 atributos |
| Crest | `pr-crest` | Escudo gerado pelo nome do clube |
| Pitch | `pr-pitch`, `pr-line`, `pr-tok` | Prancheta tática com os onze |
| TacticPicker | `pr-tactic` | Escolha do esquema; anda junto com o Pitch |
| Scorebug | `pr-score` | Placar do jogo-chave e do resultado |
| FormGuide | `pr-form` | Últimos cinco jogos em V/E/D |
| LeagueTable | `pr-table` (`pr-me`, `data-zone`) | Classificação com zonas e seu clube |
| EventCard | `pr-event`, `pr-choice` | Imprevisto com opções, custo e risco |
| StatMeter | `pr-meter` | Elenco, moral, diretoria (crítico abaixo de 35) |
| TransferOffer | `pr-offer`, `pr-chance` | Negociação com chance de aceite |

## Estado atual

- 2026-11-16: design system criado.
- 2026-11-16: o jogo embute o `components/bundle.css` real do design system e as fontes Barlow/Barlow Condensed em base64 (funciona offline). Aplicados: Scorebug (placar casa/fora com relógio e minuto ao vivo), FormGuide (últimos 5 jogos), TacticPicker, EventCard/choice com risco e custo, TransferOffer, TabBar, StatMeter, RatingBadge e LeagueTable. Falta: seletor de tema (hoje segue o sistema).
