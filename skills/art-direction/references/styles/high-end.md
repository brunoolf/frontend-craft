# Alta gama

Profundidade háptica, ritmo espacial cinematográfico, micro-interações obsessivas. O acabamento de estúdio que faz um produto parecer caro antes de a pessoa ler qualquer coisa.

**Serve:** SaaS de topo, produto de IA, lançamento, portfólio de agência.
**Não serve:** ferramenta interna, produto de alta densidade, qualquer coisa em modo Operar. Neste estilo o respiro é enorme — num dashboard isso é desperdício.

## Onde este estilo erra

Ele é o mais fácil de imitar mal, porque suas características são copiáveis: vidro, blur, orbe brilhante. Copiadas sem estrutura, produzem exatamente a estética de IA que se quer evitar.

O que faz o estilo funcionar não é o vidro — é **material consistente e ritmo espacial**. Um projeto com uma superfície de material bem resolvida bate um coberto de blur.

## Material

Escolha **um** e leve até o fim:

- **Vidro etéreo** — preto profundo (`#050505`), gradientes de malha radial sutis ao fundo, cards com backdrop-blur e hairline branca a 10%. Grotesca geométrica larga.
- **Luxo editorial** — cremes quentes, sálvia contida ou espresso. Serifada variável de alto contraste em headings grandes. Grão de filme a 2–3% de opacidade para peso físico.
- **Estruturalismo suave** — branco ou prata. Grotesca massiva. Componentes flutuando com sombra ambiente muito difusa.

Misturar os três é como se produz aquela interface que parece cara e não é nada.

## Aninhamento de material

Contêineres importantes podem ser construídos como objeto físico: casca externa com fundo sutil, hairline e padding pequeno, contendo um núcleo com raio concêntrico calculado (`calc(2rem - 0.375rem)`) e realce interno de 1px.

**Isto não é default.** É uma decisão de material para os contêineres que importam. Se cada container do projeto tem casca dupla, virou template — e o `craft-floor` recusa aninhamento de conteúdo pela mesma razão.

## Ritmo espacial

- Padding de seção entre 96px e 160px. A página respira pesado.
- Escala tipográfica ampla, com salto real entre display e corpo.
- A grade quebra a monotonia: bento assimétrico, split editorial ou cascata em profundidade. Toda quebra de simetria colapsa em coluna única abaixo de 768px, com rotações e sobreposições removidas.

## Motion

- Curvas customizadas sempre. `cubic-bezier(0.32, 0.72, 0, 1)` é um bom ponto de partida.
- Botão pressiona (`scale` para 0.98) — massa física, não troca de cor.
- Revelação na entrada com deslocamento curto e desfoque leve resolvendo. Um sistema, uma curva.
- Nav como pilha flutuante destacada do topo, não barra colada.

## Não confunda com

Caro não é o mesmo que escuro-com-brilho. Um produto de alta gama pode ser branco, quente e quieto. O sinal de valor é **acabamento consistente** — o mesmo cuidado no estado disabled e no de erro que no hero. É lá que a maioria dos projetos entrega o jogo.
