---
name: motion-principles
description: Fundamento de motion design para interface - quando animar e quando nao, timing, curvas de easing, springs, padroes de entrada e saida, densidade de movimento, reduced-motion e performance. Carregue antes de qualquer trabalho de animacao, seja para criar, revisar ou decidir se deve existir movimento.
---

# Princípios de motion

Funde o vocabulário de cinco fontes que se contradiziam. Quando este documento e uma skill de implementação (`gsap-*`, `motion-web`) divergirem sobre *se* ou *quanto* animar, este vence; elas mandam no *como*.

## Quando animar

Motion existe por uma destas cinco razões. Nenhuma se aplica? Não anime.

1. **Continuidade** — mostrar que este elemento é aquele elemento, movido. Um item que vira detalhe; um card que abre em página.
2. **Causalidade** — ligar a ação da pessoa ao resultado. O painel que desliza do botão que o abriu.
3. **Orientação** — de onde veio, para onde volta. Uma gaveta que entra pela direita sai pela direita.
4. **Feedback** — confirmar que o sistema recebeu a entrada. É o mais barato e o mais esquecido.
5. **Caráter** — o momento autoral. Um por superfície.

"Ficaria legal" não está na lista.

## Quando não animar

- Ação que a pessoa repete dezenas de vezes por dia. Delight na centésima repetição é atrito.
- Conteúdo que ela veio buscar. Fazer o texto esperar para aparecer é cobrar pedágio na própria informação.
- Estado de erro. A pessoa precisa ler agora, não assistir a uma transição.
- Qualquer coisa no caminho crítico de uma tarefa sob pressão de tempo.

## Timing

Duração é função da distância e da importância, não uma constante.

| O quê | Duração |
|---|---|
| Feedback micro (hover, press, toggle) | 100–150ms |
| Transição pequena (tooltip, dropdown, toast) | 150–250ms |
| Média (modal, gaveta, painel lateral) | 250–400ms |
| Grande (transição de página, elemento compartilhado) | 400–600ms |
| Momento autoral | o que ele exigir, dentro do razoável |

Acima de 400ms sem razão, a interface parece lenta. Abaixo de 100ms, o olho não registra continuidade e o movimento vira piscada — pior que nenhum.

**Saída é mais rápida que entrada**, tipicamente 70–80% da duração. Entrar apresenta; sair só precisa sair do caminho.

## Curvas

Nunca `linear`. Nunca `ease-in-out` por omissão. Escolha a curva.

- **Ease-out** — o default para quase tudo. Rápido no começo, assentando no fim. É o que parece responsivo: reage imediatamente ao comando.
- **Ease-in** — só para saída de coisa que desaparece.
- **Ease-in-out** — movimento que começa e termina na tela, como reordenar. Raro.
- **Spring** — o que tem massa: gesto, arraste, elástico, qualquer coisa que a pessoa "pega". Não use spring em fade de opacidade; não há massa para simular.

Pontos de partida úteis: `cubic-bezier(0.32, 0.72, 0, 1)` para a maioria das transições de UI; `cubic-bezier(0.22, 1, 0.36, 1)` para entradas mais expressivas.

**Spring:** pense em rigidez e amortecimento, não em duração. Amortecimento baixo demais produz aquele balanço de brinquedo que envelhece em dois dias. Overshoot só onde há metáfora física.

## Densidade

Uma superfície comporta:

- **Um sistema de fundo** — a mesma curva, a mesma distância, aplicados com consistência. Não deve ser notado. Se alguém elogia sua animação de entrada, ela está alta demais.
- **Um momento autoral** — o que a pessoa lembra. Um. Dois competem e viram zero.

Toda seção com a mesma entrada dramática não é sistema, é tique. O olho aprende o padrão na segunda vez e passa a esperá-lo em vez de ler o conteúdo.

## Entrada e saída

- **Estado inicial visível.** Se o JavaScript falhar, o conteúdo está lá. `opacity: 0` sem garantia de reversão é uma página em branco esperando para acontecer.
- **Distância curta.** 8–24px basta. Deslocamentos de 100px parecem software de apresentação.
- **Stagger** entre 30 e 60ms por item, com teto. Doze itens a 80ms somam quase um segundo de espera.
- **Anime a partir da direção que faz sentido.** Um menu que abre da direita entra pela direita.

## Reduced-motion

`prefers-reduced-motion: reduce` é obrigatório, e a resposta **não** é remover tudo.

Remover toda a animação quebra a causalidade que a pessoa usa para entender o que aconteceu. A resposta certa é **preservar a mudança de estado, remover o deslocamento**: mantenha um fade de 100–150ms, elimine translate, scale, rotação, parallax e qualquer movimento contínuo.

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

Esse bloco é o piso de segurança, não a solução completa. Para movimento que carrega significado, escreva a alternativa reduzida à mão.

## Performance

Padrão: `transform` e `opacity` — compostas na GPU, sem layout nem paint.

As demais não são proibidas, são caras: `filter: blur`, `backdrop-filter`, `clip-path`, `mask`, `box-shadow`. Entram quando o efeito exige e permanecem suaves sob medição no dispositivo mais fraco que o produto suporta.

Nunca anime `top`, `left`, `width`, `height`, `margin` ou `padding`. Cada frame dispara layout na árvore inteira.

`will-change` só no elemento que anima agora, removido ao terminar. Aplicado amplamente, consome memória de GPU e piora tudo.

`backdrop-filter` só em elemento fixo ou sticky. Num container que rola, ele repinta a cada frame.

## Acabamento

O que separa motion competente de motion bom:

- **Interruptível.** A pessoa clica de novo no meio da transição: ela reverte a partir de onde está, não salta para o início.
- **Origem correta.** `transform-origin` no ponto que a metáfora exige. Um menu que abre do botão cresce a partir do botão.
- **Uma coisa se move por vez** na hierarquia. Container e conteúdo animando com curvas diferentes ao mesmo tempo parece quebrado.
- **Sem flash de conteúdo não estilizado** antes da animação assumir.
