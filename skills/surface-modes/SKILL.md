---
name: surface-modes
description: Os quatro modos de superficie - Persuadir, Operar, Ler, Experimentar - que definem o que conta como sucesso numa tela antes de qualquer decisao visual. Carregue antes de julgar ou desenhar qualquer superficie. Impede o erro mais comum de UX: aplicar criterio de landing page num dashboard ou vice-versa.
---

# Modos de superfície

Antes de qualquer decisão de layout, densidade ou motion, estabeleça o modo. Ele define o que conta como sucesso — e critério errado produz trabalho errado com competência.

**O modo vem da superfície pedida, não do produto.** A landing page de uma ferramenta interna é Persuadir. A documentação de uma casa de moda é Ler. O índice de um site de docs é Ler, não Persuadir.

## Os quatro

### Persuadir

*O visitante decide e age. O design é o produto.*

Landing pages, páginas de marketing, campanhas, pricing, páginas de lançamento.

- Ganhar atenção é o trabalho, não um efeito colateral.
- Espaçamento macro generoso. Escala tipográfica ampla. Um momento visual que fica na memória.
- Uma ação primária por viewport. Duas CTAs concorrentes é nenhuma.
- Imagem real quando o brief pede — placeholder cinza mata conversão.
- **Falha típica:** parecer um template. Todo mundo tem o mesmo hero, a mesma grade de três features, o mesmo depoimento.

### Operar

*O visitante completa uma tarefa. A interface some no caminho.*

App, dashboard, editor, admin, configurações, ferramentas.

- Escaneabilidade, consistência e expectativa nativa superam expressão.
- Densidade é virtude. O respiro de landing page aqui é desperdício e obriga a rolar por informação que devia estar visível.
- Estado do sistema sempre legível: o que está salvo, carregando, com erro.
- Atalho de teclado e navegação por Tab importam mais do que em qualquer outro modo.
- A marca vive em detalhes precisos — o timing de um toast, o acabamento de um foco — não em decoração.
- **Falha típica:** designer trata como portfólio. Animação de entrada em painel que a pessoa abre quarenta vezes por dia é tortura.

### Ler

*O visitante entende algo.*

Docs, artigos, guias, ajuda, changelog.

- Estrutura para compreensão primeiro: hierarquia de heading, âncora, navegação previsível.
- Medida de linha entre 65 e 75 caracteres. Não negociável — é o que separa leitura de escaneamento penoso.
- Ritmo vertical consistente. Espaço acima do heading maior que abaixo.
- Código, tabela e nota com tratamento distinto e estável.
- **Falha típica:** decorar em vez de estruturar. Ilustração bonita que empurra o conteúdo para baixo da dobra.

### Experimentar

*O visitante está dentro da obra. A interface recua.*

Portfólio, galeria, showcase, peça imersiva.

- O artefato lidera desde o primeiro viewport. Navegação some ou fica mínima.
- É o único modo onde motion pesado e 3D se justificam como conteúdo, não como enfeite.
- Ainda precisa de saída: a pessoa precisa conseguir sair da experiência.
- **Falha típica:** confundir imersão com fricção. Se levar quatro segundos para entender o que se faz ali, você perdeu.

## Consequências por modo

| | Persuadir | Operar | Ler | Experimentar |
|---|---|---|---|---|
| Espaçamento de seção | 96–160px | 24–48px | 48–72px | varia |
| Densidade | baixa | alta | média | baixa |
| Momento autoral | sim, no hero | não | não | é o produto |
| Motion de entrada | sim, sutil | quase nunca | não | sim |
| Medida de linha | 45–65ch | livre | 65–75ch | livre |

## Superfície mista

Um produto tem superfícies de modos diferentes. O sistema de design precisa dizer **qual escala vale onde** — não forçar uma única escala de espaçamento sobre landing e dashboard. Registre isso em `DESIGN.md`.

Quando uma superfície genuinamente mistura modos (um dashboard com um bloco de upsell), o modo dominante manda no layout; o bloco divergente é a exceção contida, não o novo padrão.
