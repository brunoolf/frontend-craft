---
name: refine-verbs
description: Os quinze verbos de refino de interface - bolder, quieter, distill, polish, delight, overdrive, typeset, layout, colorize, harden, onboard, clarify, adapt, optimize, extract. Cada um define um escopo estrito do que muda e do que nao se toca. Use quando o pedido nomeia uma direcao de refino, incluindo em linguagem natural: "deixa mais ousado", "ta gritando demais", "simplifica", "poli isso antes de subir".
---

# Verbos de refino

Cada verbo define **o que muda e o que não se toca**. O escopo é o valor: um refino que mexe em tudo é um redesign disfarçado, e destrói trabalho que estava certo.

**Regra comum a todos:** refino **preserva** identidade, comportamento, cópia e tudo fora do escopo. Se o pedido exige substituir o mundo visual, isso não é refino — é redesign, e passa por `fc-art-director`. Nunca divida a diferença.

## Reconhecimento em linguagem natural

| O usuário diz | Verbo |
|---|---|
| "deixa mais ousado", "tá tímido", "tá sem graça" | bolder |
| "tá gritando", "muito agressivo", "tá cansativo" | quieter |
| "simplifica", "tá poluído", "tem coisa demais" | distill |
| "poli isso", "revisa antes de eu subir" | polish |
| "adiciona personalidade", "tá sem alma" | delight |
| "vai com tudo", "surpreende" | overdrive |
| "a tipografia tá ruim", "arruma as fontes" | typeset |
| "o espaçamento tá errado", "tá desalinhado" | layout |
| "tá monocromático demais", "falta cor" | colorize |
| "prepara pra produção", "e se der erro" | harden |
| "faz o onboarding", "primeira experiência" | onboard |
| "esses textos tão ruins", "melhora as mensagens" | clarify |
| "arruma no mobile", "não fica bom no celular" | adapt |
| "tá lento", "trava" | optimize |
| "transforma em componente", "extrai os tokens" | extract |

---

## Amplificar

**bolder** — amplifica o que já existe; não troca a direção. Aumente o contraste de escala tipográfica, comprometa a paleta onde ela estava tímida, deixe o momento autoral acontecer de verdade, quebre a simetria. *Não toca:* estrutura, cópia, fluxo. *Falha típica:* aumentar tudo — amplificação uniforme não é ênfase.

**overdrive** — passa do convencional deliberadamente. Só quando o usuário pede explicitamente e a superfície comporta (modos Persuadir ou Experimentar). Um dashboard em overdrive é um dashboard quebrado. Mesmo aqui, o piso de acessibilidade não cede.

**delight** — personalidade em momentos específicos: estado vazio, sucesso, transição, o detalhe que ninguém esperava. **Um por superfície.** Delight distribuído vira ruído, e delight em ação repetida vira atrito na décima vez.

**colorize** — cor estratégica em UI monocromática. Cor com trabalho definido: hierarquia, estado, categoria. Não decoração. Verifique contraste em cada par novo. *Falha típica:* colorir tudo e perder a hierarquia que o monocromático já dava.

## Reduzir

**quieter** — baixa o volume de design superestimulado. Reduza número de cores concorrentes, achate hierarquia excessiva, remova movimento decorativo, aumente espaço em branco. *Não toca:* conteúdo, funcionalidade.

**distill** — remove até restar o essencial. Elimine elemento que não serve à tarefa, mescle seção redundante, corte ornamento. **O teste:** remova mais uma coisa; se ainda funciona, ela sobrava. *Cuidado:* distill remove ornamento, não função. Cortar um estado de erro não é destilar.

## Corrigir dimensão específica

**typeset** — só tipografia. Escala, pesos, entrelinha, medida (65–75ch no corpo), tracking, balanceamento de heading, pares. *Não toca:* cor, espaçamento, estrutura.

**layout** — só espaçamento, ritmo e alinhamento. Base de espaçamento aplicada com disciplina, mais espaço acima do heading que abaixo, grupos apertados e separação generosa, grade coerente. *Não toca:* cor, tipo, conteúdo.

**adapt** — comportamento em outros tamanhos. Colapso de layout assimétrico, alvos de toque, transbordo, `100dvh`, áreas seguras. Teste com conteúdo real em 360, 768 e 1280. *Não toca:* a composição desktop que já funciona.

**optimize** — performance. Meça primeiro; só otimize o que mediu. Bundle, imagens, propriedades animadas, re-render. *Não toca:* comportamento visível. Se a otimização muda o que a pessoa vê, ela virou outra coisa.

**clarify** — só texto de interface. Botões nomeiam a ação, erros nomeiam problema e recuperação, labels sem jargão, voz consistente. *Nunca invente conteúdo factual* — marque como pendência.

## Completar

**polish** — passe final antes de publicar. Percorra `craft-floor` inteiro: contraste, profundidade, espaçamento, tipo, motion, estados, cópia, cobertura. Corrija o que falha. Polish é acabamento, não redesign: se você quer refazer uma seção, isso é outro pedido.

**harden** — prontidão para produção. Estados de erro reais, casos-limite (texto muito longo, zero itens, mil itens, rede lenta, offline), i18n e o que acontece quando o texto cresce 30%, timeout, tentativa de novo, preservação do que a pessoa digitou. É o verbo mais pulado e o que mais rende.

**onboard** — primeira execução, estados vazios e ativação. O estado vazio é design, não fallback: diga o que aquilo vai conter, por que está vazio, qual a próxima ação. Caminho até o primeiro valor real, o mais curto honesto.

**extract** — puxa tokens e componentes reutilizáveis para o sistema. Encontre a repetição, nomeie o padrão dominante, migre os desvios, atualize `DESIGN.md`. *Não toca:* aparência. Se o visual mudou, a extração está errada.

---

## Quando o verbo está errado

Se o pedido nomeia um verbo mas o problema real é outro, **diga antes de executar**. "Você pediu `bolder`, mas o que faz isso parecer tímido é o espaçamento uniforme, não a escala — sugiro `layout` primeiro." Executar o verbo errado com competência ainda é entregar a coisa errada.
