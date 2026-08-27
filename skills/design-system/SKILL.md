---
name: design-system
description: Construir, extrair e manter design systems - tokens com papeis, escala tipografica, escala de espacamento, cor, raio, sombra, dark mode e tokens de motion. Inclui o formato do DESIGN.md, o artefato de memoria que preserva as decisoes e suas razoes entre sessoes. Use ao criar tokens, consertar inconsistencia, adicionar tema escuro ou documentar o sistema de um codigo existente.
---

# Design system

Um sistema converte direção em decisões reutilizáveis. Se ele não reduz o número de escolhas que a próxima pessoa precisa fazer, não é sistema — é uma paleta com nomes.

## Extraia antes de inventar

Em código existente, o sistema já está lá: implícito, inconsistente e espalhado. O trabalho não é impor uma escala nova sobre tudo — é encontrar o padrão dominante, nomeá-lo e alinhar os desvios.

1. Inventarie os valores reais em uso: cores, tamanhos de fonte, espaçamentos, raios.
2. Conte a frequência. O valor mais usado costuma ser o certo.
3. Agrupe os quase-iguais (`14px`, `15px`, `0.9rem` são o mesmo degrau tentando existir).
4. Nomeie por papel e migre os desvios.

Um sistema que ignora o incumbente vira segunda fonte da verdade — e duas fontes da verdade é pior que nenhuma.

## Cor por papel

Nunca uma lista de hexes. Papéis, para que tema seja troca de valores e não reescrita.

```
surface            fundo da página
surface-raised     cartão, painel, popover
surface-sunken     poço, campo de entrada
text               corpo
text-muted         secundário — tinja do matiz do fundo, nunca cinza puro
text-inverted      sobre superfície de destaque
border             hairline estrutural
border-strong      divisor com peso
accent             a ação. Uma. Se aparece em nove lugares, não é destaque
accent-text        texto legível sobre accent
success / warning / danger  + as variantes de superfície e texto
focus              anel de foco. ≥3:1 contra tudo que ele toca
```

Cada papel precisa de contraste verificado nos pares que realmente ocorrem.

## Escalas

**Espaçamento** com base declarada (4px é comum) e degraus que crescem de forma não-linear: `4 8 12 16 24 32 48 64 96 128`. Todo valor do produto sai daí. Um `margin-top: 37px` é um bug de sistema.

**Tipografia** com degraus distinguíveis. Se dois vizinhos são difíceis de diferenciar, um sobra. Seis a oito degraus bastam para quase tudo. Cada degrau carrega tamanho **e** entrelinha — declarados juntos, sempre.

**Raio, sombra, borda** também são escalas. Ad hoc aqui é a origem mais comum de inconsistência visual.

**Motion como token:** durações (`fast` 150ms, `base` 250ms, `slow` 400ms) e curvas nomeadas. É o que impede cada componente de inventar o próprio timing.

## As escalas são fluidas, não fixas

Uma escala que só vale numa largura está pela metade. Cada degrau de tipografia e de espaçamento define um piso e um teto, e interpola entre eles:

```css
--step-0: clamp(1rem, 0.95rem + 0.25vw, 1.125rem);
--step-3: clamp(2rem, 1.5rem + 2.5vw, 3.5rem);
--space-section: clamp(3rem, 8vw, 10rem);
```

Isso elimina a maior parte dos breakpoints de tipografia e espaçamento, e é o que evita o salto abrupto entre larguras. Quanto maior o degrau, mais agressiva a inclinação — display varia muito, corpo quase nada, porque a medida ideal de leitura não muda com o tamanho da tela.

Sempre um teto, e nunca `vw` puro no corpo: a parte em `rem` da fórmula é o que preserva o zoom do navegador, que é ferramenta de acessibilidade. Veja `responsive` para a mecânica completa.

## Dark mode

Não é inversão.

- Defina a paleta clara **completa** nos tokens base; redefina só os **valores** no tema escuro. Nunca redeclare estrutura.
- Superfície escura separa por luminância, não por sombra. Sombras somem; eleve com superfície mais clara.
- Nada de `#000` puro com `#FFF` puro. O contraste extremo produz vibração e cansa.
- Cores saturadas parecem mais intensas no escuro. Reduza saturação, aumente luminosidade.
- Três estados, não dois: escolha explícita clara, escolha explícita escura, e o default do sistema. Uma cor definida só dentro de um bloco de media query some no terceiro estado.

## DESIGN.md

Na raiz do projeto do usuário. Quatro seções:

```markdown
# Design

## Direção
[Uma frase concreta, mais o porquê ligado ao usuário e à cena de uso]

## Tokens
[Valor e papel. Agrupados por tipo.]

## Decisões
[A parte que mais importa. Cada decisão não-óbvia com a razão.
 "Raio 2px porque o produto é ferramenta de precisão e canto macio contradiz isso."]

## Fora de escopo
[O que foi deliberadamente descartado, e por quê. Impede que volte por acidente.]
```

Ao atualizar, **preserve as razões existentes**. Se estiver contradizendo uma decisão registrada, diga isso e registre a nova razão. Apagar silenciosamente é como um projeto vira a média de três direções incompatíveis.

Sem a seção de decisões, o arquivo é só uma lista de variáveis e a próxima sessão reabre tudo.

## Regras

**Menos degraus.** Seis usados com disciplina batem catorze usados ao acaso.

**Nomeie por papel, não por aparência.** `--accent`, não `--blue-500`. A cor muda; o papel permanece.

**O sistema serve o produto.** Um dashboard e uma landing não compartilham escala de espaçamento. Se o projeto tem superfícies de modos diferentes (`surface-modes`), o sistema precisa dizer qual escala vale onde.

**Token não usado é dívida.** Se nada consome, remova.
