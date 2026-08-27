---
name: scroll-experiences
description: Composicao de experiencias dirigidas por scroll - cena fixa de fundo com conteudo rolando por cima, 3D ou canvas reagindo ao progresso do scroll, secoes pinadas, parallax e narrativa por scroll. Cobre a arquitetura que liga scroll, cena e conteudo, o carregamento progressivo do bundle WebGL, os fallbacks e o orcamento de performance. Use quando o pedido envolve "coisas acontecendo no fundo enquanto rola", cena 3D sincronizada com scroll, ou storytelling por scroll.
---

# Experiências dirigidas por scroll

As outras skills cobrem as peças: `gsap-scrolltrigger` a API, `threejs-*` a cena, `motion-web` o scroll-driven CSS. Esta cobre **a composição** — que é onde essas experiências quebram.

## Decida a categoria primeiro

Cada uma tem arquitetura diferente. Escolher errado significa reescrever.

| Categoria | O que é | Custo |
|---|---|---|
| **Reveal no scroll** | Elementos aparecem ao entrar no viewport | Trivial. CSS ou IntersectionObserver |
| **Parallax** | Camadas em velocidades diferentes | Baixo. CSS scroll-driven resolve |
| **Seção pinada** | A seção trava e o conteúdo interno avança com o scroll | Médio. ScrollTrigger com pin |
| **Cena de fundo persistente** | Canvas ou WebGL fixo atrás, conteúdo rolando por cima | Alto. É o que a maioria quer ao dizer "coisas acontecendo no fundo" |
| **Scrollytelling** | A narrativa *é* a cena; o texto legenda | Muito alto. Projeto próprio |

**Antes de subir de categoria, pergunte se o efeito não sai na de baixo.** A maioria dos pedidos de "cena 3D de fundo" fica melhor resolvida com parallax em CSS mais um gradiente animado — sem 3MB de bundle e sem a bateria do celular.

## A arquitetura da cena de fundo

A estrutura que funciona:

```
<div class="scene-root">          position: fixed; inset: 0; z-index: 0;
  <canvas>                        pointer-events: none (a menos que interativa)
</div>
<main>                            position: relative; z-index: 1;
  <section>…</section>            conteudo rola normalmente
</main>
```

Três regras que evitam os defeitos clássicos:

1. **A cena é `fixed`, não `sticky`.** Sticky dentro de um container que rola cria stacking context e a cena some atrás de conteúdo em pontos imprevisíveis.
2. **`pointer-events: none` no canvas**, a menos que a cena receba entrada. Senão ela come cliques e seleção de texto.
3. **O conteúdo tem `z-index` acima e fundo próprio** onde precisa de legibilidade. Texto direto sobre cena animada é ilegível em metade dos frames.

## Ligar scroll ao estado da cena

**Nunca leia `scrollY` dentro do loop de render.** Isso força reflow síncrono a cada frame.

O padrão é um único valor de progresso normalizado, atualizado por ScrollTrigger ou IntersectionObserver, lido pelo loop:

```js
const state = { progress: 0, target: 0 }

ScrollTrigger.create({
  trigger: '#scene-range',
  start: 'top top',
  end: 'bottom bottom',
  onUpdate: (self) => { state.target = self.progress },
})

function frame() {
  // amortece: o scroll do usuario e irregular, a camera nao deve ser
  state.progress += (state.target - state.progress) * 0.08
  camera.position.z = 5 - state.progress * 3
  renderer.render(scene, camera)
  requestAnimationFrame(frame)
}
```

O amortecimento (`lerp`) é o que separa uma cena que parece cara de uma que parece amadora. Scroll bruto produz movimento nervoso — especialmente em trackpad e em scroll por toque com inércia.

**Um único `requestAnimationFrame` para a página inteira.** Múltiplos loops competindo é a causa mais comum de jank nessas páginas.

## Carregamento

Um bundle WebGL não pode bloquear a primeira renderização.

1. **A página funciona e é legível sem a cena.** Renderize o conteúdo primeiro, sempre.
2. **Importe a cena dinamicamente**, depois do primeiro paint e só se ela for de fato ser vista.
3. **Estado de carregamento que não é um vazio.** Um gradiente estático ou um poster no lugar da cena. Um retângulo preto por dois segundos é pior que não ter cena.
4. **Não inicialize acima da dobra se a cena está abaixo dela.** Use IntersectionObserver na faixa da cena.

```js
useEffect(() => {
  if (!inView || reducedMotion || !supportsWebGL()) return
  let dispose
  import('./scene').then((m) => { dispose = m.init(canvasRef.current) })
  return () => dispose?.()
}, [inView, reducedMotion])
```

## Fallbacks obrigatórios

Quatro caminhos precisam existir. Faltando qualquer um, a experiência está incompleta:

| Situação | Comportamento |
|---|---|
| Sem WebGL | Imagem estática ou gradiente CSS na faixa da cena |
| `prefers-reduced-motion` | Cena estática num frame representativo, ou só o fundo. **Não** carregue o bundle |
| Dispositivo fraco / bateria fraca | Reduza `pixelRatio`, desative postprocessing, corte partículas |
| JavaScript falhou | O conteúdo está lá e legível. Sempre |

`prefers-reduced-motion` numa experiência que *é* movimento não significa página quebrada: significa a mesma narrativa, contada estaticamente. O conteúdo e a ordem permanecem; só o movimento sai.

## Orçamento de performance

- **60fps no dispositivo alvo mais fraco.** Meça lá, não no seu monitor.
- **`pixelRatio` limitado:** `Math.min(devicePixelRatio, 2)`. Em telas 3x, renderizar nativo triplica o custo por nada visível.
- **Pause fora da tela.** `IntersectionObserver` para parar o loop quando a cena sai do viewport, e `visibilitychange` para parar em aba de fundo. Loop rodando invisível é bateria queimada.
- **Redimensionamento com debounce.** Recriar o renderer a cada pixel de resize trava a página.
- **Limpe.** Geometrias, materiais, texturas e render targets têm `dispose()`. Cena não descartada em navegação SPA vaza memória de GPU até o crash.

## Mobile

- Barra de endereço que aparece e some dispara `resize` constantemente. Use `100dvh`, não `100vh`, e faça debounce do handler.
- Scroll por toque tem inércia própria — o amortecimento precisa ser mais forte que no desktop.
- Considere não carregar a cena em telas estreitas. Uma imagem bem escolhida costuma superar uma cena 3D degradada.
- Alvos de toque não podem cair sob o canvas. Verifique o `pointer-events`.

## Acessibilidade

- Movimento não pode ser a única forma de acessar a informação. Se a cena revela conteúdo, esse conteúdo existe no DOM.
- Sequestrar o scroll (`scroll-jacking`) quebra teclado, leitor de tela e a expectativa da pessoa. Se for inevitável, ofereça saída e navegação por teclado equivalente.
- Nada que pisque entre 3 e 55 Hz.
- Uma seção pinada ainda precisa ser alcançável por Tab, na ordem certa.

## Sinais de que passou do ponto

- A pessoa não consegue chegar ao conteúdo sem assistir a uma sequência.
- O scroll parece pesado ou "atrasado" em vez de amortecido.
- A cena diz a mesma coisa que o texto ao lado — redundância cara.
- O bundle da página passa de 1MB por causa de um efeito de fundo.
