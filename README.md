# frontend-craft

Um plugin de design frontend para Claude Code. Sete agentes especializados, 40 skills curadas, e roteamento automático — você descreve o problema em português normal e o agente certo assume.

Curado a partir de [nove projetos de código aberto](NOTICE.md), com as contradições entre eles resolvidas.

## Instalação

```bash
/plugin marketplace add brunoolf/frontend-craft
```

Depois:

```bash
/plugin install frontend-craft
```

## Como funciona

Você não precisa saber os nomes dos agentes. Descreva o problema:

> "isso ficou estranho"
> "faz uma landing page pro meu produto"
> "parece feito por IA"
> "o scroll trava no celular"
> "faz isso funcionar em qualquer tamanho de tela"
> "quero uma cena 3D de fundo enquanto rola"

A skill roteadora dispara, lê o projeto e despacha. Pedidos vagos passam primeiro pelo crítico — diagnóstico antes de tratamento.

## Os sete agentes

| Agente | Dono de |
|---|---|
| `fc-art-director` | Que universo visual o produto habita: estilo, paleta, tipografia, identidade, imagens de referência |
| `fc-design-system` | Tokens, escalas, temas, dark mode. Gera e mantém o `DESIGN.md` |
| `fc-ux-architect` | Fluxo, hierarquia de informação, carga cognitiva, estados, UX copy |
| `fc-motion-engineer` | Todo movimento: micro-interações, GSAP, scroll-driven, 3D/WebGL |
| `fc-implementer` | Design vira React/Next real. Componentes, responsivo, mockup→código |
| `fc-design-critic` | *Read-only.* Crítica com scoring, caça a padrões genéricos de IA |
| `fc-a11y-perf-auditor` | *Read-only.* WCAG 2.2, contraste, teclado, CLS, bundle, jank |

Os dois agentes read-only nunca editam. Eles diagnosticam; os de escrita tratam. É o que impede um crítico de "consertar" e destruir a intenção do design no caminho.

Todo agente carrega `craft-floor` antes de produzir qualquer coisa — é o piso compartilhado que faz sete agentes soarem como um time, e não como sete repositórios colados.

## Comandos

Atalhos para quando você já sabe o que quer. O roteamento automático é o caminho principal.

| Comando | Faz |
|---|---|
| `/fc` | Menu contextual — lê o projeto e sugere |
| `/fc:new` | Pipeline completo de superfície nova |
| `/fc:redesign` | Redesign, auditando o incumbente antes de substituir |
| `/fc:critique` | Crítica read-only com scoring |
| `/fc:audit` | Acessibilidade, performance e responsivo |
| `/fc:refine <verbo>` | 15 verbos: bolder, quieter, distill, polish, harden, typeset… |
| `/fc:animate` | Motion, incluindo scroll e 3D |
| `/fc:slides` | Apresentação HTML animada |

## Memória entre sessões

Dois arquivos na raiz do **seu** projeto:

- **`PRODUCT.md`** — o que é o produto, quem usa, quais as restrições
- **`DESIGN.md`** — a direção, os tokens, e *as razões de cada decisão*

A seção de razões é o que mais importa. Sem ela, a próxima sessão reabre discussões já resolvidas e o projeto vira a média de três direções incompatíveis.

## As 40 skills

**Fundação** — `frontend-craft` (roteador), `craft-floor`

**Direção visual** — `art-direction` (com referências brutalista, minimalista, alta gama, editorial), `brandkit`, `imagegen-web`, `design-dna`

**Sistema** — `design-system`, `ui-ux-dataset` (84 estilos, 192 paletas, ~1900 fontes, 99 diretrizes de UX)

**UX** — `ux-patterns`, `surface-modes`

**Motion** — `motion-principles`, `motion-web`, `motion-audit`, `animation-vocabulary`, `scroll-experiences`, e as 7 skills oficiais `gsap-*`

**3D** — as 10 skills `threejs-*`

**Implementação** — `implementation`, `responsive`, `image-to-code`, `pick-ui-library`, `refine-verbs`

**Avaliação** — `critique-method`, `audit-method`

**Extra** — `frontend-slides`

## O que este plugin decide por você

As fontes originais se contradiziam. O `craft-floor` arbitra, e essas arbitragens são a espinha do plugin:

- **Nenhuma fonte é banida por nome.** Inter é um tipo competente. O problema nunca foi a fonte — foi tê-la escolhido por ser o default.
- **Aninhamento de conteúdo é sempre errado; aninhamento de material não.** Card dentro de card porque a informação foi empilhada sem hierarquia: achate. Casca com raio concêntrico porque o mundo visual pede materialidade: legítimo, e não é default.
- **Um momento autoral por superfície.** "Tudo anima na entrada" e "um momento memorável" se contradizem. O momento vence; a revelação de entrada é sistema de fundo e não deve ser notada.
- **Espaçamento vem do modo da superfície.** `py-40` numa landing é respiro; num dashboard é desperdício.

## Escopo

**Dentro:** web moderna (React, Next.js, Tailwind, shadcn), 3D/WebGL para experiências de scroll, apresentações HTML.

**Fora:** mobile e desktop nativos, Vue/Svelte/Angular como alvos primários, e qualquer código executável.

## Licença

MIT. Veja [NOTICE.md](NOTICE.md) para a atribuição dos nove projetos de origem.
