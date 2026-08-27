---
name: ui-ux-dataset
description: Dataset consultavel de referencia de design - 84 estilos visuais, 192 paletas por tipo de produto, 74 pares tipograficos, 1900 fontes Google, 99 diretrizes de UX, presets de motion, escolha de grafico, icones e padroes de landing page, mais guias por stack (React, Next, Tailwind, shadcn, Astro, three.js). Consulte quando precisar de opcoes concretas em volume - paletas, pares de fonte, escolha de grafico, pattern de secao - em vez de inventar do zero.
---

# Dataset de UI/UX

Referência tabular consultável. Use quando precisar de **opções concretas em volume**; não substitui julgamento — o `craft-floor` e a direção registrada continuam mandando.

O CLI Python original não foi portado. Consulte os CSVs com `Grep` e `Read`, que resolvem o mesmo problema sem dependência de runtime.

## Como consultar

Os arquivos estão em `data/` relativo a esta skill. Use `Grep` com `output_mode: "content"` e `-i`.

```
Grep(pattern: "luxury|elegant", path: "data/typography.csv", output_mode: "content", -i: true)
Grep(pattern: "SaaS", path: "data/colors.csv", output_mode: "content", -i: true)
```

Arquivos pequenos (até ~200 linhas) podem ser lidos inteiros com `Read`. `google-fonts.csv` tem ~1900 linhas — sempre `Grep` nele.

## Os arquivos

| Arquivo | Linhas | O que traz | Busque por |
|---|---|---|---|
| `styles.csv` | 84 | Estilos visuais com paleta, efeitos, para que serve e para que **não** serve | nome do estilo, keyword de humor |
| `colors.csv` | 192 | Paletas completas por tipo de produto, com papéis (primary, surface, muted, border, destructive, ring) e notas de contraste | tipo de produto |
| `typography.csv` | 74 | Pares de fonte com humor, para que serve, URL do Google Fonts e config Tailwind | humor, categoria |
| `google-fonts.csv` | ~1900 | Catálogo com classificação, eixos variáveis, subsets e ranking | nome, keyword, classificação |
| `ux-guidelines.csv` | 99 | Diretrizes com Do, Don't, exemplo bom e ruim, e severidade | categoria, tema |
| `motion.csv` | 16 | Presets por tier de intensidade, com duração, easing e snippet GSAP | tipo de interação |
| `ui-reasoning.csv` | 161 | Padrão recomendado por categoria de UI, com regras de decisão e anti-patterns | categoria de produto |
| `landing.csv` | 34 | Padrões de landing: ordem de seção, posição de CTA, estratégia de cor | keyword de padrão |
| `charts.csv` | 25 | Escolha de gráfico por tipo de dado, com quando **não** usar e nota de acessibilidade | tipo de dado |
| `icons.csv` | 104 | Ícones por categoria com biblioteca, import e uso | função do ícone |
| `products.csv` | 192 | Recomendações por tipo de produto: estilo, padrão de landing, foco de paleta | tipo de produto |
| `react-performance.csv` | 44 | Armadilhas de performance em React/Next com correção | sintoma |
| `app-interface.csv` | 29 | Diretrizes de interface de app | categoria |
| `stacks/*.csv` | — | Guias por stack: react, nextjs, html-tailwind, shadcn, astro, threejs | tema |

Os stacks fora do alvo deste plugin (Flutter, WPF, SwiftUI, Compose, Angular, Vue) foram removidos.

## Como usar bem

**Como ponto de partida, não como resposta.** Uma paleta do dataset é um começo defensável, não a decisão. A direção registrada em `DESIGN.md` vence sempre.

**Duas ou três consultas, não dez.** O dataset é grande o bastante para virar procrastinação. Consulte o que resolve a decisão em aberto e siga.

**Cruze quando útil.** `products.csv` diz o estilo recomendado para o tipo de produto; `styles.csv` detalha esse estilo; `colors.csv` dá a paleta; `typography.csv` o par de fontes. É a sequência natural para uma direção nova.

**A coluna "Do Not Use For" é a mais valiosa** em `styles.csv` e `charts.csv`. Saber o que um estilo estraga vale mais que saber o que ele enfeita.

## Cuidados

- As paletas trazem notas de contraste, mas **verifique os pares que você de fato usar**. A nota cobre a combinação prevista, não a sua.
- `typography.csv` sugere Inter em vários pares. Isso é um default razoável, não uma escolha — se você não sabe dizer por que Inter serve este produto, veja `art-direction`.
- Os snippets de motion em `motion.csv` usam sintaxe GSAP. Para a decisão de *se* e *quanto* animar, `motion-principles` manda.
