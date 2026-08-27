---
name: motion-web
description: Implementacao de motion na web sem GSAP - CSS moderno (scroll-driven animations, View Transitions, @starting-style, transition-behavior), e Motion/Framer Motion (AnimatePresence, layout animations, gestos, motion values). Use quando o movimento cabe na plataforma ou no React sem precisar de uma engine de timeline.
---

# Motion na web

Carregue `motion-principles` antes. Ela decide *se* e *quanto*; esta decide *como*.

## Escolha da ferramenta

Suba um degrau só quando o anterior não resolver:

| Necessidade | Ferramenta |
|---|---|
| Hover, foco, toggle, mudança de estado simples | `transition` CSS |
| Loop, keyframes, entrada sem JS | `@keyframes` |
| Entrada e saída de elemento com estado (React) | Motion `AnimatePresence` |
| Elemento que muda de posição no layout | Motion `layout` |
| Arrastar, gesto, movimento contínuo ligado a input | Motion values |
| Ligado ao progresso do scroll, efeito simples | CSS scroll-driven |
| Transição entre páginas ou vistas | View Transitions API |
| Sequência complexa, pin de scroll, orquestração fina | GSAP (`gsap-*`) |

Cada degrau custa bundle e complexidade. A maioria dos pedidos para em CSS.

## CSS moderno

**`@starting-style`** resolve o problema antigo de animar a entrada de um elemento que acabou de existir — inclusive de `display: none` e de camada de topo:

```css
.popover {
  opacity: 1;
  transition: opacity 200ms ease-out, display 200ms allow-discrete;
}
@starting-style {
  .popover { opacity: 0; }
}
```

`transition-behavior: allow-discrete` (ou `allow-discrete` na shorthand) é o que permite `display` e `overlay` participarem da transição. Sem isso, a saída pisca.

**Scroll-driven animations** rodam fora da main thread — ganho real de suavidade:

```css
@keyframes reveal {
  from { opacity: 0; transform: translateY(16px); }
}
.card {
  animation: reveal linear both;
  animation-timeline: view();
  animation-range: entry 10% cover 35%;
}
```

`view()` acompanha o elemento cruzando o viewport; `scroll()` acompanha o progresso de um container. Cobre reveal e parallax sem uma linha de JavaScript. Verifique suporte e garanta que o estado sem suporte seja o estado final visível.

**View Transitions:**

```js
if (!document.startViewTransition) { update(); return }
document.startViewTransition(() => update())
```

Sempre com o caminho de fallback. Use `view-transition-name` em elementos que persistem entre as vistas para obter continuidade — é o que dá a transição de elemento compartilhado sem biblioteca.

## Motion (Framer Motion)

**Entrada e saída.** `AnimatePresence` exige `key` estável e o filho direto sendo `motion`:

```jsx
<AnimatePresence mode="wait">
  {open && (
    <motion.div
      key="panel"
      initial={{ opacity: 0, y: 8 }}
      animate={{ opacity: 1, y: 0 }}
      exit={{ opacity: 0, y: 8 }}
      transition={{ duration: 0.2, ease: [0.32, 0.72, 0, 1] }}
    />
  )}
</AnimatePresence>
```

`mode="wait"` quando a saída e a entrada não devem coexistir. Sem ele, os dois se sobrepõem — às vezes é o que se quer, às vezes é o defeito.

**`layout`** anima mudança de posição e tamanho automaticamente, usando a técnica FLIP: transform em vez de propriedades de layout. Use `layoutId` para continuidade entre componentes diferentes — item de lista que vira detalhe. É a ferramenta certa para continuidade e a errada para tudo mais: aplicada amplamente, custa caro.

**Spring** para gesto e arraste. Pense em rigidez e amortecimento, não duração. Não use spring em fade puro — não há massa para simular.

**`whileInView`** com `viewport={{ once: true }}` para revelação na entrada. Sem `once`, o elemento reanima toda vez que reentra, o que irrita rápido.

**`useReducedMotion()`** é o hook oficial. Use-o para trocar o preset de movimento, não para desligar tudo.

## React: o essencial

- Toda animação criada em componente é destruída no unmount.
- Não anime durante o render. Efeito ou callback de evento.
- Objeto de `transition` recriado a cada render vira prop nova toda vez. Extraia para constante fora do componente.
- Em Next com App Router, componente que anima é client component. Empurre a fronteira para baixo: marcar a página inteira como client desfaz o benefício do server rendering.

## Armadilhas

- Animar altura de `auto`. Use `grid-template-rows: 0fr → 1fr`, ou `max-height` com um teto conhecido, ou `layout` do Motion.
- `AnimatePresence` sem `key`, ou com o `motion` não sendo filho direto: a saída simplesmente não roda.
- Vários elementos com o mesmo `view-transition-name` na mesma vista quebram a transição inteira.
- `backdrop-filter` em container que rola.
- `will-change` deixado permanentemente no CSS.
