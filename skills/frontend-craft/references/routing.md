# Tabela de despacho

Indexada por **como o usuário fala**, não por nome de agente. Ele nunca vai dizer "chame o art-director".

## Sintoma → dono

| O usuário diz | Dono | Por quê |
|---|---|---|
| "faz uma landing page / site / portfólio" | pipeline **Superfície nova** | Precisa de direção antes de código |
| "refaz esse site" / "moderniza isso" | pipeline **Redesign** | Auditar o incumbente antes de substituir |
| "melhora isso" / "ficou estranho" / "tá esquisito" | `fc-design-critic` → despacha | Diagnóstico antes de tratamento |
| "parece feito por IA" / "tá genérico" / "parece template" | `fc-design-critic` → `fc-art-director` | Crítico nomeia os padrões; diretor escolhe o mundo substituto |
| "deixa mais bonito" / "deixa premium" / "adiciona polish" | `fc-design-critic` → `fc-implementer` | Vago. Precisa virar lista de achados antes de virar edição |
| "deixa mais ousado" / "tá gritando demais" / "simplifica" | `fc-implementer` com `refine-verbs` | Verbo de refino claro: bolder / quieter / distill |
| "as cores tão erradas" / "escolhe uma paleta" | `fc-art-director` | Decisão de mundo visual |
| "que fonte usar" / "a tipografia tá ruim" | `fc-art-director` → `fc-design-system` | Diretor escolhe, sistema formaliza a escala |
| "cria uma identidade / brand kit / logo" | `fc-art-director` | Skill `brandkit` |
| "gera imagens de referência do design" | `fc-art-director` | Skill `imagegen-web` |
| "extrai o design system daqui" / "documenta os tokens" | `fc-design-system` | Produz `DESIGN.md` |
| "adiciona dark mode" / "os tokens tão bagunçados" | `fc-design-system` | |
| "esse fluxo tá confuso" / "o usuário se perde" | `fc-ux-architect` | Arquitetura de informação |
| "faz o onboarding" / "estado vazio" / "mensagem de erro" | `fc-ux-architect` | Estados e UX copy |
| "esse texto de botão tá ruim" | `fc-ux-architect` com `refine-verbs` (clarify) | |
| "anima isso" / "tá sem vida" / "adiciona micro-interações" | `fc-motion-engineer` | |
| "que animações eu poderia ter aqui" | `fc-motion-engineer` com `motion-audit` | Read-only: propõe, não implementa |
| "revisa as animações" / "o motion tá ruim" | `fc-motion-engineer` com `motion-audit` | |
| "como chama aquele efeito que..." | skill `animation-vocabulary` direto | Não precisa de agente |
| "scroll com 3D de fundo" / "efeito parallax" / "cena que reage ao scroll" | `fc-motion-engineer` com `scroll-experiences` | |
| "quero um modelo 3D" / "WebGL" / "shader" | `fc-motion-engineer` com `threejs-*` | |
| "implementa esse mockup" / "transforma essa imagem em código" | `fc-implementer` com `image-to-code` | |
| "que biblioteca usar pra X" | skill `pick-ui-library` direto | Não precisa de agente |
| "quebra no mobile" / "não fica responsivo" | `fc-a11y-perf-auditor` → `fc-implementer` | Medir, depois corrigir |
| "tá lento" / "trava" / "engasga no scroll" | `fc-a11y-perf-auditor` → `fc-motion-engineer` ou `fc-implementer` | |
| "isso é acessível?" / "contraste" / "leitor de tela" | `fc-a11y-perf-auditor` | |
| "revisa isso antes de eu subir" | `fc-design-critic` ∥ `fc-a11y-perf-auditor` | Único paralelismo permitido |
| "faz uma apresentação / deck / slides" | skill `frontend-slides` direto | Vertical própria |

## Pipelines

### Superfície nova

```
1. fc-art-director      → decide o mundo visual. Grava a decisão.
2. fc-design-system     → converte o mundo em tokens. Escreve DESIGN.md.
3. fc-implementer  ∥  fc-ux-architect
                        → constrói / define fluxo e estados
4. fc-motion-engineer   → um momento autoral + o sistema de fundo
5. fc-design-critic  ∥  fc-a11y-perf-auditor
6. fc-implementer       → aplica os achados
```

Pule o passo 1 se `DESIGN.md` já existir e o usuário não pediu direção nova. Pule o 4 se ele disse que não quer animação.

### Redesign

```
1. fc-design-critic     → audita o incumbente. O look atual é evidência e anti-referência.
2. fc-art-director      → escolhe o mundo substituto. Não meio-termo com o antigo.
3. fc-design-system     → reescreve DESIGN.md
4. fc-implementer       → aplica, preservando conteúdo, função e verdade do produto
5. fc-a11y-perf-auditor
```

**Refinamento preserva; redesign substitui.** Refinamento mantém identidade, comportamento e cópia. Redesign mantém a verdade do produto e trata o visual antigo como anti-referência. Nunca divida a diferença — polir um visual que foi descartado é o pior dos dois mundos. Se não estiver claro qual dos dois o usuário quer, pergunte uma vez.

### Diagnóstico

```
1. fc-design-critic     → lista de achados priorizada
2. despache por área:
   visual/estética   → fc-art-director
   tokens/escala     → fc-design-system
   fluxo/copy        → fc-ux-architect
   motion            → fc-motion-engineer
   código/responsivo → fc-implementer
```

## Casos ambíguos

**Dois agentes servem.** Pergunte uma vez, com a diferença concreta: *"Quer que eu mexa só na aparência disso, ou repensar o fluxo também?"* Não pergunte duas vezes.

**O pedido é grande demais para um agente** ("refaz o produto inteiro"). Não despache. Divida em superfícies com o usuário e rode o pipeline por superfície. Uma superfície = uma tela ou uma página.

**Nenhum agente serve.** Se o pedido é backend, dados ou infra, esta skill não se aplica. Saia do caminho.
