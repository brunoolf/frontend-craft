---
name: responsive
description: Projetar interface responsiva desde o inicio - estrategia de breakpoints, layout intrinseco (clamp, min, max, auto-fit), container queries, tipografia fluida, colapso de grade, imagens responsivas, densidade por viewport e as unidades de viewport modernas (dvh, svh, lvh). Use ao construir qualquer layout, nao apenas quando algo ja quebrou no mobile.
---

# Responsivo

Carregue ao **construir**, não só ao consertar. Layout responsivo pensado no fim vira uma pilha de breakpoints remendando decisões que nasceram fixas.

Para *detectar* o que já quebrou, veja `audit-method`. Para *corrigir* uma superfície existente, o verbo `adapt` em `refine-verbs`. Esta skill é sobre nascer certo.

## A mudança de mentalidade

Media query é a ferramenta de **último** recurso, não a primeira. O CSS moderno resolve a maior parte da responsividade sem nenhum breakpoint — e um layout que se adapta sozinho não tem os saltos abruptos que denunciam design feito por régua.

A ordem de preferência:

1. **Layout intrínseco** — `min()`, `max()`, `clamp()`, `flex-wrap`, `grid auto-fit`. Adapta continuamente.
2. **Container queries** — o componente reage ao próprio espaço.
3. **Media queries** — só para mudanças de *estrutura* que nenhuma das anteriores resolve.

## Layout intrínseco

**Container sem breakpoint:**

```css
.container {
  width: min(100% - 2rem, 72rem);
  margin-inline: auto;
}
```

Uma linha substitui três media queries. Abaixo de 72rem ocupa a largura menos a margem; acima, trava e centraliza.

**Grade que se organiza sozinha:**

```css
.grid {
  display: grid;
  gap: 1.5rem;
  grid-template-columns: repeat(auto-fit, minmax(min(18rem, 100%), 1fr));
}
```

Quantas colunas couberem, com mínimo de 18rem. O `min(18rem, 100%)` é o detalhe que evita transbordo em telas muito estreitas — sem ele, `minmax(18rem, …)` estoura abaixo de 288px.

Use `auto-fit` quando quiser que poucos itens estiquem; `auto-fill` quando quiser preservar as colunas vazias.

**Sidebar que vira empilhamento sem media query:**

```css
.layout {
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
}
.sidebar { flex: 1 1 16rem; }
.main    { flex: 999 1 30rem; }
```

O `flex-grow` desproporcional faz o main dominar quando há espaço e quebrar quando não há.

## Tipografia fluida

```css
:root {
  --step-0: clamp(1rem, 0.95rem + 0.25vw, 1.125rem);
  --step-1: clamp(1.25rem, 1.15rem + 0.5vw, 1.5rem);
  --step-3: clamp(2rem, 1.5rem + 2.5vw, 3.5rem);
  --step-5: clamp(3rem, 2rem + 5vw, 6rem);
}
```

Cada degrau interpola entre um piso e um teto. Três regras:

- **Sempre um teto.** `font-size: 5vw` sem `clamp` produz texto absurdo em monitor ultrawide.
- **Nunca `vw` puro no corpo.** Quebra o zoom do navegador, que é uma ferramenta de acessibilidade. A parte `rem` da fórmula é o que preserva o zoom.
- **Quanto maior o degrau, mais agressiva a inclinação.** Display precisa variar muito; corpo quase nada — a medida ideal de leitura não muda com o tamanho da tela.

O espaçamento também se beneficia: `padding-block: clamp(3rem, 8vw, 10rem)` em seções elimina a maioria dos breakpoints de espaçamento.

## Container queries

A ferramenta certa para **componente reutilizável**. Um card não deveria se importar com a largura da janela — ele se importa com o espaço que recebeu.

```css
.card-area { container-type: inline-size; }

@container (min-width: 30rem) {
  .card { grid-template-columns: 12rem 1fr; }
}
```

O mesmo card funciona na sidebar estreita e na área principal larga, sem saber onde está. Media query não consegue isso — é por isso que componentes de biblioteca costumam ter aquele salto errado.

Unidades `cqi` / `cqb` dimensionam em relação ao container, não ao viewport.

## Breakpoints, quando forem necessários

**Derive do conteúdo, não do dispositivo.** O breakpoint certo é onde *o seu layout* quebra — redimensione até o texto ficar feio e coloque o breakpoint ali. A lista de larguras de iPhone envelhece; o seu conteúdo não.

Como ponto de partida, três costumam bastar: **~640px** (empilhado → duas colunas), **~1024px** (estrutura completa), **~1440px** (teto do container). Mais que cinco é sinal de que o layout devia ser intrínseco.

**Mobile-first.** Escreva o estado base para a tela estreita e adicione com `min-width`. É a ordem que gera menos CSS e falha melhor: um estilo esquecido deixa a página empilhada — feio mas usável. O contrário deixa quebrada.

## Colapso de grade

Toda composição assimétrica precisa dizer o que acontece quando não cabe. Isso não é detalhe de acabamento: é onde a maioria dos designs "premium" quebra.

- Sobreposições com margem negativa e rotações **saem** no mobile. Elementos girados criam conflito de área de toque.
- `col-span` explícito volta a uma coluna.
- Rolagem horizontal só quando é intencional e evidente (carrossel, tabela) — nunca no corpo da página.
- Ordem visual segue a ordem de leitura. Reordenar com `order` ou `grid-row` desconecta o DOM do visual e quebra a navegação por teclado.

## Unidades de viewport

`100vh` está quebrado no Safari iOS: a barra de endereço entra e sai e o valor não acompanha, o que produz o salto clássico.

| Unidade | Comportamento |
|---|---|
| `svh` | Viewport **pequeno** — barras visíveis. O mais seguro para "cabe sem rolar" |
| `lvh` | Viewport **grande** — barras escondidas |
| `dvh` | **Dinâmico** — acompanha. O default para altura de seção |

Use `min-height: 100dvh` em seção de altura total. `100vh` é achado de auditoria.

## Imagens

```html
<img
  src="foto-800.jpg"
  srcset="foto-400.jpg 400w, foto-800.jpg 800w, foto-1600.jpg 1600w"
  sizes="(min-width: 64rem) 50vw, 100vw"
  width="800" height="600"
  alt="…">
```

- **`width` e `height` sempre**, mesmo com CSS por cima. É o que reserva espaço e evita layout shift.
- **`sizes` correto.** Errado, o navegador baixa a maior imagem — o desperdício de banda mais comum na web.
- `aspect-ratio` no CSS quando a proporção é fixa.
- Em Next, `next/image` com `sizes`; `fill` exige container com posição e proporção definidas.

## Além da largura

Responsivo não é só quantos pixels cabem:

- **`prefers-reduced-motion`** — veja `motion-principles`.
- **`hover: hover` e `pointer: fine`** — teste a capacidade, não a largura. Laptops têm tela sensível ao toque; tablets têm mouse. Presumir toque por largura erra nos dois sentidos.
- **Área de toque** ≥24×24px (WCAG 2.2 SC 2.5.8), 44×44 como meta em superfície móvel.
- **Áreas seguras** — `env(safe-area-inset-*)` para notch e indicador de home.
- **Densidade por modo** — a escala de espaçamento muda entre Persuadir e Operar (`surface-modes`), e essa diferença também é responsiva: um dashboard denso no desktop precisa de mais respiro no toque, não menos.

## Verificar

Sempre com **conteúdo real**. A maioria dos defeitos aparece no texto de verdade, não no placeholder.

- 360px (o menor razoável), 768px, 1280px e um viewport muito largo.
- Zoom do navegador em 200% — requisito de acessibilidade, e onde `vw` puro entrega o jogo.
- Texto 30% mais longo, simulando tradução.
- O corpo da página nunca rola na horizontal.
- Nenhum alvo de toque colapsado ou sobreposto.
- Tabela e bloco de código dentro do próprio container com `overflow-x: auto`.
