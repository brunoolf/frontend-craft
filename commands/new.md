---
description: Pipeline completo para uma superficie nova
argument-hint: "[o que construir]"
---

Invoque `Skill(frontend-craft)`. Rode o pipeline **Superfície nova** de `references/routing.md`:

1. `fc-art-director` — decide o mundo visual (pule se `DESIGN.md` existe e o usuário não pediu direção nova)
2. `fc-design-system` — converte em tokens, escreve `DESIGN.md`
3. `fc-implementer` ∥ `fc-ux-architect`
4. `fc-motion-engineer`
5. `fc-design-critic` ∥ `fc-a11y-perf-auditor`
6. `fc-implementer` aplica os achados

Antes do passo 1, confirme o **modo da superfície** (Persuadir / Operar / Ler / Experimentar). Se o pedido cobre várias superfícies, divida com o usuário e rode uma por vez.

Superfície a construir: $ARGUMENTS
