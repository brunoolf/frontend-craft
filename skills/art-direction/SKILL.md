---
name: art-direction
description: Como ir do brief ao mundo visual - escolher e comprometer com uma direcao concreta, paleta com papeis, pares tipograficos, materialidade e o momento memoravel. Use ao iniciar uma superficie nova, ao substituir o visual de um redesign, ou quando uma interface precisa parar de parecer generica. Traz referencias de estilo carregadas sob demanda.
---

# Direção de arte

Direção não é decoração aplicada no fim. É a decisão que torna todas as outras decisões possíveis — e que, quando falta, produz aquela interface competente que ninguém lembra.

## O problema do adjetivo

"Moderno", "clean", "premium", "minimalista", "profissional" não são direções. São o que todo mundo diz querer, e é por isso que tudo se parece. Um adjetivo não exclui nada, e direção que não exclui não decidiu.

Empurre até chegar numa **referência concreta**:

| Adjetivo | Direção |
|---|---|
| "clean e moderno" | "catálogo de leilão suíço — muito branco, uma serifada, foto como evidência" |
| "premium" | "manual de relojoaria — denso, técnico, nada supérfluo, ouro só onde importa" |
| "divertido" | "fanzine dos anos 90 — xerox, colagem, tipo que não se comporta" |

Duas ou três perguntas costumam bastar. Não faça um questionário.

## As quatro respostas

A direção está pronta quando você responde cada uma em uma frase:

1. **Que mundo é este?** Referência concreta, não adjetivo.
2. **Por que este produto merece este mundo?** Ligado ao usuário e à cena de uso — quem, onde, sob que luz, sob que pressão. Não ao seu gosto.
3. **Qual é o momento?** A coisa única que a pessoa lembra depois de fechar a aba.
4. **O que fica de fora?** O que este mundo torna proibido. Sem isso a direção não segura nada.

## Da direção às escolhas

**Cor por papel, não por gosto.** Defina `surface`, `text`, `border`, `accent` e os estados, e diga que trabalho a cor de destaque faz. Uma cor de destaque que aparece em nove lugares não é destaque. Claro ou escuro sai da cena de uso — quem usa isso, onde, sob que luz ambiente — nunca da categoria do produto.

**Tipografia como decisão, não default.** Uma família bem explorada em pesos e tamanhos supera três famílias mal combinadas. Ao parear, contraste é o ponto: mesma classe duas vezes vira acidente. Nenhuma fonte é banida por nome — o que se recusa é escolher por omissão. Se você não consegue dizer por que *esta* fonte serve *este* produto, volte.

**Materialidade.** Plano, vidro, papel, metal, impresso, tela? Isso decide sombra, borda, raio e ruído de uma vez só, e é o que a maioria dos projetos nunca decide — daí saem as interfaces sem caráter.

**Densidade e postura.** Apertado e técnico, ou arejado e editorial? Isso vem do modo da superfície (`surface-modes`), não do seu gosto.

**Postura de movimento.** Quieta, viva ou cinematográfica. Registre — é o que `fc-motion-engineer` vai honrar.

## Referências de estilo

Carregue **uma** quando ela servir a direção decidida. São pontos de partida, não fôrmas: sirva ao brief, não à referência.

- [Brutalista industrial](references/styles/brutalist.md) — grade rígida, contraste extremo de escala, cor utilitária, degradação analógica
- [Minimalista editorial](references/styles/minimalist.md) — monocromático quente, contraste tipográfico, grade plana, sem gradiente
- [Alta gama](references/styles/high-end.md) — profundidade háptica, materialidade, ritmo espacial, acabamento de agência
- [Editorial](references/styles/editorial.md) — hierarquia de revista, imagem como evidência, tipo com voz

Se nenhuma serve, não force. A maior parte do bom trabalho está fora de qualquer estilo catalogado.

Para consultar paletas, pares tipográficos ou estilos catalogados em volume, use `ui-ux-dataset`. Para extrair a direção de uma referência visual existente, `design-dna`. Para gerar imagens de referência antes de construir, `imagegen-web`.

## Comprometa

O erro mais comum não é escolher errado — é escolher pouco. Uma direção meio aplicada some: a paleta ousada usada só num botão, a serifada dramática só num heading e o resto no default.

Se você decidiu por um mundo, ele aparece na superfície inteira: fundo, espaçamento, ritmo, forma, movimento. Entre refinado e comprometido, comprometa.

## Registre

A direção precisa sobreviver à sessão. Entregue um bloco pronto para `DESIGN.md` com as quatro respostas e a razão de cada escolha. Direção sem o porquê registrado é reaberta do zero na próxima sessão, e o projeto vira uma média de três direções.
