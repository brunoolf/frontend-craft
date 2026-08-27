---
name: implementation
description: Traduzir design em codigo React/Next real - composicao de componentes, fronteira server e client, responsivo, estados, imagens e escolha de dependencia. Use ao construir UI a partir de uma direcao ou design definido, ou ao refinar codigo de interface existente.
---

# Implementação

Design que não vira código funcionando é opinião. Você fecha essa distância.

## Antes de escrever

1. **`DESIGN.md`** — tokens e direção. **Use os tokens.** Valor hard-coded onde existe token é onde a entropia começa.
2. **Os componentes existentes.** Reusar o padrão do projeto vale mais que trazer o seu. Um botão novo ao lado de três que já existem é dívida, não entrega.
3. **A stack real.** React ou Next, App Router ou Pages, Tailwind ou CSS-in-JS, biblioteca de componentes, gerenciamento de estado. Descubra lendo, não presumindo.

## Composição

- Um componente faz uma coisa. Quando o arquivo passa de umas 200 linhas, geralmente são dois componentes disputando espaço.
- Separe apresentação de busca de dados. Componente que renderiza e busca é difícil de reusar e de testar.
- Composição antes de configuração. `<Card><CardHeader/></Card>` envelhece melhor que `<Card variant="x" hasHeader showIcon/>`. Prop booleana em cascata é o sinal de que a API está errada.
- Estado no nível mais baixo que funciona. Estado alto demais re-renderiza a árvore inteira.

## Next: server e client

`"use client"` só onde há estado, efeito, ou handler de evento. Empurre a fronteira para **baixo** na árvore: marcar a página inteira como client desfaz o benefício do App Router.

O padrão que funciona: página é server component, busca os dados, e passa para uma ilha client pequena que cuida da interação. Server component pode renderizar client component; o contrário só via `children`.

## Estilo

- Tokens do sistema. Se falta um valor, é uma conversa com `fc-design-system`, não um valor solto.
- Container queries onde o componente precisa reagir ao próprio espaço, não ao viewport. É a ferramenta certa para componente reusável e quase ninguém usa.
- Layout intrínseco antes de media query: `min()`, `clamp()`, `grid auto-fit`. Veja `responsive` — media query é o último recurso, não o primeiro.
- `:has()`, `:focus-visible`, `text-wrap: balance` em headings, `text-wrap: pretty` em corpo. Baratos e muito visíveis.
- Ordem de classe consistente. Numa base Tailwind, deixe o formatador cuidar.

## Estados obrigatórios

Um componente sem estes está pela metade:

`default` · `hover` · `focus-visible` · `active` · `disabled` · `loading` · `error` · `empty`

Estado de foco **visível** não é opcional. `focus-visible` para não mostrar o anel em clique de mouse, mostrando em teclado.

## Conteúdo

**Conteúdo real, nunca lorem ipsum.** Placeholder esconde exatamente os problemas que importam: transbordo, quebra de linha, medida longa demais, nome que não cabe.

O que você não puder verificar — preço, prazo, nome de cliente, número de usuários — **marque como pendência do usuário**. Nunca preencha com plausível. Um número inventado numa landing page é o pior defeito que este plugin pode produzir.

## Imagens

- `next/image` em Next, com `width`/`height` ou `fill` + container com `aspect-ratio`. Dimensão reservada é o que evita layout shift.
- `priority` só no LCP. Em tudo é o mesmo que em nada.
- `sizes` correto em imagem responsiva, senão o navegador baixa a maior.
- `alt` significativo; `alt=""` em decorativa.

## Dependências

O padrão é **não adicionar**. Antes de instalar:

1. O projeto já tem algo que resolve?
2. A plataforma resolve? `<dialog>`, popover API, `:has()`, container queries, View Transitions cobrem hoje o que exigia biblioteca ontem.
3. O custo em bundle vale o que economiza?

Quando precisar mesmo, `pick-ui-library` tem a lista curada por problema.

## Acessibilidade no ato de escrever

Não é passe posterior:

- Semântica antes de ARIA. `<button>` antes de `<div role="button">`.
- Label associado a todo campo.
- Heading em ordem, sem pular nível.
- Contraste verificado nos pares reais.
- Alvo de toque ≥24×24px.

## Regras

**Complete.** Nada de `// resto igual`, nada de componente esboçado que "seguiria o mesmo padrão". Se não couber numa resposta, entregue arquivos completos em sequência e diga o que falta. A única exceção são assets que só o usuário pode fornecer — marque-os.

**Responsivo desde o início, não como passe posterior.** Carregue `responsive` ao construir layout. Verifique com conteúdo real em todo breakpoint.

**Se o sistema estiver errado, diga.** Se a implementação revelar que falta um token ou que uma escala não funciona, reporte — não contorne com valor solto. Contornar silenciosamente é como sistemas morrem.
