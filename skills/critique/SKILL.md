---
name: critique
description: Critica de design read-only com heuristica, scoring e caca a padroes genericos de IA. Traz a lista de padroes buscaveis via Grep para achado objetivo antes de julgamento subjetivo. Use quando o pedido e vago sobre o que esta errado - "melhora isso", "parece feito por IA", "ta generico" - ou como revisao antes de publicar.
---

# Crítica de design

Seu produto é uma lista priorizada de achados precisos o bastante para outra pessoa consertar sem adivinhar.

## Ordem

1. **Leia o contexto.** `DESIGN.md` e `PRODUCT.md`. Uma escolha que viola sua preferência mas serve uma direção registrada **não é achado** — é a direção funcionando.
2. **Estabeleça o modo** (`surface-modes`). Critério errado produz achado errado com confiança.
3. **Varra os padrões buscáveis** (abaixo). Objetivo primeiro.
4. **Julgue o que a busca não pega.**
5. **Priorize e entregue.**

## Varredura objetiva

Rode com `Grep` nos arquivos de UI. Cada acerto é candidato, não veredito — verifique antes de reportar.

**Motion e transição**

| Padrão | Por quê |
|---|---|
| `transition:\s*all` | Anima propriedades não intencionais; custo imprevisível |
| `ease-in-out\|ease;\|linear` | Curva default, não escolhida |
| `addEventListener\(['"]scroll` | Reflow contínuo; use IntersectionObserver |
| `will-change` | Verificar se é permanente |
| `transition.*\b(width\|height\|top\|left\|margin\|padding)\b` | Propriedade de layout animada |

**Layout e superfície**

| Padrão | Por quê |
|---|---|
| `h-screen\|100vh` | Salta no Safari iOS; use `100dvh` |
| `z-\[?[0-9]{3,}` | Z-index arbitrário; sinal de guerra de camadas |
| `bg-gradient-to-.*bg-clip-text` | Texto com gradiente |
| `border-l-[248]\|border-l-\[` | Borda lateral colorida grossa |
| `backdrop-blur` | Verificar se está em elemento fixo, não em container que rola |
| `rounded-\[?[0-9]` fora do token | Raio ad hoc |

**Tipografia e cor**

| Padrão | Por quê |
|---|---|
| `text-gray-[45]00\|#(6\|7\|8)[0-9a-f]{5}` como texto secundário | Cinza puro em vez de tinta do matiz |
| `uppercase.*tracking-` | Candidato a eyebrow repetido — conte as ocorrências |
| `#[0-9a-fA-F]{3,6}` em componente | Cor hard-coded onde existe token |
| `font-size` ou `text-[` com valor fora da escala | Degrau inventado |

**Acessibilidade (bloqueantes)**

| Padrão | Por quê |
|---|---|
| `outline:\s*none\|outline-none` | Verificar se há substituto de foco |
| `<div[^>]*onClick` | Interativo sem semântica |
| `alt=""` em imagem de conteúdo | |
| `tabIndex=\{?-?[1-9]` | `tabindex` positivo quebra a ordem |
| `aria-` em elemento que já tem semântica nativa | ARIA redundante costuma indicar elemento errado |

**Conteúdo**

`lorem\|ipsum\|TODO\|FIXME\|placeholder\|Your Company\|Lorem` — texto de preenchimento em código de UI.

**Contagem estrutural.** Conte, não só encontre: quantas seções repetem a mesma estrutura de card, quantos eyebrows em maiúsculas, quantas grades de exatamente três colunas idênticas. Repetição é o achado — uma ocorrência é escolha, seis é template.

## Julgamento

O que a busca não pega:

- **Tem um ponto de vista?** A superfície poderia ser de qualquer produto da categoria com a troca do logotipo? Esse é o defeito raiz do qual quase todos os outros derivam.
- **Hierarquia.** A coisa mais importante parece a mais importante? Três coisas gritando é nenhuma.
- **Ritmo.** As seções têm todas o mesmo peso e o mesmo espaçamento? Isso é o que faz uma página parecer um formulário.
- **Compromisso.** A direção foi meio aplicada? Paleta ousada só num botão, serifada só num heading e o resto no default.
- **Cobertura do brief.** Tudo que foi pedido está presente e localizável em segundos?
- **Estados reais.** Vazio, erro e carregando existem, ou só o caminho feliz foi desenhado?

## Os padrões de "feito por IA"

Quando o usuário diz "parece feito por IA", ele geralmente está vendo alguns destes. Nomeie os que encontrar:

1. Grade de três a seis cards idênticos de ícone + título + parágrafo como estrutura da página.
2. Hero com número grande, label pequeno e três estatísticas de apoio.
3. Eyebrow em maiúsculas com tracking antes de toda seção.
4. Texto com gradiente para dar ênfase.
5. Todas as seções com o mesmo padding vertical e a mesma entrada animada.
6. Ícones genéricos de biblioteca no peso padrão, um por feature.
7. Depoimento com avatar redondo, cinco estrelas, cargo em cinza.
8. Cinza neutro puro em tudo que é secundário.
9. Simetria perfeita em toda seção — sempre texto à esquerda, imagem à direita.
10. Copy que descreve categoria em vez de produto: "solução poderosa", "experiência perfeita".

## Formato

Cada achado com três partes obrigatórias:

```
[Prioridade] arquivo:linha
  O quê:   o padrão ou regra violada, concreto
  Por quê: a consequência para quem usa
  Trata:   fc-art-director | fc-design-system | fc-ux-architect | fc-motion-engineer | fc-implementer
```

**Prioridade:** Bloqueante (quebrado, ilegível, inacessível, ou o brief não foi atendido) · Alto (a pessoa nota, a qualidade percebida cai) · Médio (craft) · Nota.

Ordenado. Uma lista de quarenta itens sem ordem é o mesmo que nenhuma lista.

## Regras

**O brief vence.** Estética fixada pelo usuário não é achado. Anote como decisão deliberada e siga.

**Sem elogio de enchimento.** Não abra amaciando. Se algo está bem resolvido e é útil saber — porque deve ser preservado numa mudança — diga isso por essa razão.

**Não invente achado.** Se a superfície está sólida, diga que está sólida e por quê. Rigor performático é tão inútil quanto complacência.

**Você não conserta.** Se souber a correção exata, escreva-a como instrução para o agente dono.
