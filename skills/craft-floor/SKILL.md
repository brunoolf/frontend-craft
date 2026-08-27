---
name: craft-floor
description: Piso de qualidade compartilhado por todos os agentes do frontend-craft. Carregue antes de escrever ou julgar qualquer UI. Traz as verificacoes mecanicas do resultado construido, os defaults de categoria que se deve recusar, e as arbitragens quando fontes de design se contradizem. Nao escolhe direcao visual; garante o piso sobre o qual a direcao acontece.
---

# Craft floor

Este é o piso. Ele não escolhe a direção — garante que qualquer direção seja executada com competência. Carregue depois que a direção estiver decidida e construa sem anunciar a checklist.

**Hierarquia de autoridade, em ordem:**

1. O brief do usuário e o mundo visual já comprometido (`DESIGN.md`).
2. Este documento.
3. Seu hábito.

Um brief que pede eyebrow em maiúsculas ganha. Seu reflexo de colocar um em toda seção, não.

## Verificar

Cada item é uma verificação do **resultado construído**, não da intenção. Rode todos juntos numa rodada de inspeção, não em viagens separadas.

- **Contraste:** texto de corpo e placeholder ≥4.5:1, texto grande ≥3:1. Sobre superfície colorida, tinja o texto secundário a partir daquele matiz ou do foreground — nunca cinza.
- **Profundidade:** sombras carregam deslocamento e desfoque suave. Um halo colorido com deslocamento zero é decoração, não profundidade.
- **Espaçamento:** grupos apertados, separação generosa, mais espaço acima de um heading do que abaixo. Leia os valores computados, não os pretendidos.
- **Tipografia:** medida do corpo 65–75ch, display no máximo 6rem, piso de tracking -0.04em, headings balanceados, degraus de escala e peso óbvios. Rode a cópia real em cada breakpoint e conserte o que transbordar.
- **Motion:** um momento autoral, não efeitos espalhados nem a mesma entrada idêntica em cada seção. Ease-out exponencial a partir de um default já visível. Vá além de transform e opacity: blur, backdrop-filter, clip-path, mask e shadow pertencem à paleta quando permanecem suaves.
- **Estados:** hover, disabled, loading, error, empty. Mais conteúdo real, controles funcionais, composição responsiva e foco de teclado.
- **Copy:** a linguagem do próprio produto. Controles nomeiam sua ação; erros nomeiam o problema e a recuperação.
- **Cobertura:** todo requisito do brief presente e localizável em segundos.

## Recusar

Estes são os **defaults da categoria**, não banimentos. As palavras do brief podem justificar qualquer um deles. Alcançar um quando o eixo estava livre significa que você não estava decidindo. Reconhecer isso significa reescrever o elemento, não amenizá-lo.

**Estruturas de página**

- Cards do mesmo tamanho com ícone + heading + texto *como estrutura da página*.
- O template hero-métrica: número grande, label pequeno, estatísticas de apoio, cor de destaque.
- Eyebrow em maiúsculas com tracking sobre toda seção. Um kicker nomeado é sistema; eyebrow em todo lugar é gramática que você não escolheu.
- Numeração de seção (01 / 02 / 03) a menos que a sequência carregue informação que o leitor precise.
- Modal para uma tarefa que não exige interrupção nem foco protegido.

**Hábitos de superfície**

- Texto com gradiente. Ênfase vem de peso ou tamanho.
- Vidro e blur como decoração em vez de efeito específico.
- `border-left`/`border-right` colorida acima de 1px em cards, itens de lista, callouts ou alertas.
- Sparklines, anéis de progresso e retângulos arredondados com sombra suave no lugar de conteúdo.
- Monoespaçada como fantasia de "técnico" em vez de para código, dados ou medição.
- Claro ou escuro escolhido por categoria. Escolha pela cena de uso: quem, onde, sob que luz ambiente.

**Motion**

- `linear` ou `ease-in-out` como curva padrão. Escolha a curva; não aceite a que veio de graça.
- Mudança de estado instantânea onde havia continuidade a preservar.
- `window.addEventListener('scroll')` para revelar elementos. Use `IntersectionObserver` ou o equivalente da sua biblioteca.
- Animar `top`, `left`, `width` ou `height`. Use `transform` e `opacity`; as demais propriedades entram só quando permanecem suaves sob medição.

## Arbitragens

As fontes deste plugin se contradizem em alguns pontos. Aqui as contradições estão resolvidas. **Esta seção é a autoridade** — se uma skill fundida ou preservada disser o contrário, este documento vence.

**Fontes tipográficas.** Nenhuma fonte é banida por nome. Inter, Roboto e Helvetica são tipos competentes; o problema nunca foi a fonte, foi tê-la escolhido por ser o default. Se você consegue dizer por que *esta* fonte serve *este* produto, ela passa. Se a resposta é "é a que estava lá", volte e escolha.

**Aninhamento.** Duas coisas diferentes usam a mesma palavra:

- *Aninhamento de conteúdo* — um card dentro de um card porque a informação foi empilhada sem hierarquia. Sempre errado. Achate.
- *Aninhamento de material* — uma casca externa com hairline e padding contendo um núcleo com raio concêntrico calculado, simulando placa em bandeja. É uma decisão de material, legítima quando o mundo visual comprometido pede materialidade. Não é default: se todo container do projeto tem casca dupla, virou template.

**Densidade de motion.** "Todo elemento anima na entrada" e "um momento autoral" se contradizem. O momento autoral vence. Revelação na entrada é permitida como *sistema de fundo* — uma curva, uma distância, aplicada com consistência e sem chamar atenção. O momento autoral é o que o usuário lembra. Um por superfície.

**Espaçamento macro.** Recomendações de `py-24` a `py-40` são para páginas de persuasão. Numa superfície de operação (dashboard, editor, configurações), esse respiro é desperdício e prejudica escaneabilidade. A escala de espaçamento decorre do modo da superfície — veja a skill `surface-modes`.

**Variância entre gerações.** A regra de "nunca repetir o mesmo layout" vale entre *projetos diferentes*, não dentro de um. Dentro de um projeto, consistência é o produto. Não introduza variação para provar criatividade.

## Completude

Entregue o trabalho inteiro. Sem `// resto da implementação aqui`, sem `...`, sem componente esboçado que "seguiria o mesmo padrão". Se o output não couber numa resposta, entregue arquivos completos em sequência e diga o que falta — nunca um arquivo pela metade fingindo estar pronto.

A única exceção são assets que só o usuário pode fornecer: imagens de produto, logotipos, conteúdo real. Marque-os explicitamente.

---

O piso segura a mecânica; ele nunca escolhe a direção. Com todas as verificações verdes, gaste a página no mundo comprometido — e entre refinado e comprometido, comprometa.
