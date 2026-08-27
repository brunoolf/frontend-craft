---
name: motion-audit
description: Revisao read-only de motion - encontrar lugares que deveriam animar e nao animam, julgar animacoes existentes contra um padrao alto de craft, e produzir um plano priorizado de correcoes. Use para "o que poderia ser animado aqui", "revisa as animacoes", "o motion ta ruim" ou "faz isso parecer mais vivo". Propoe com valores exatos; nao implementa.
---

# Auditoria de motion

Read-only. Produz achados e planos com valores exatos, prontos para outro agente executar. Não edita.

Carregue `motion-principles` antes — é o critério contra o qual você julga.

## Três modos

O pedido determina qual rodar. Não rode os três por padrão.

### Encontrar oportunidades

*"O que poderia ser animado aqui?"* — varredura por movimento **ausente**.

Procure, nesta ordem de valor:

1. **Continuidade quebrada.** Elemento que vira outro sem transição: item de lista abrindo em detalhe, card virando modal, valor que muda de lugar. Maior retorno que existe.
2. **Feedback ausente.** Ação sem confirmação visual. Botão que não reage à pressão. Item adicionado que aparece do nada.
3. **Orientação ausente.** Painel, gaveta ou popover que aparece sem vir de lugar nenhum.
4. **Mudança de estado sem transição** onde havia continuidade a preservar.

**Rejeite mais do que propõe.** A maior parte de uma interface não deve animar. Uma proposta de motion para cada elemento é o mesmo erro que nenhuma. Para cada lugar aprovado, saiba dizer qual das cinco razões ele atende.

Formato: **onde**, **qual razão**, **propriedade + duração + curva exatas**, **o que acontece com reduced-motion**.

### Revisar o existente

*"Revisa as animações"* — julgamento contra o padrão. **A aprovação se ganha; o default é apontar.**

| Verificar | Falha típica |
|---|---|
| Razão | Anima porque dá, não porque comunica |
| Duração | Acima de 400ms sem razão; abaixo de 100ms virando piscada |
| Curva | `linear` ou `ease-in-out` por omissão |
| Simetria | Saída com a mesma duração da entrada (deve ser 70–80%) |
| Distância | Deslocamento de 100px onde 16px bastava |
| Densidade | Toda seção com a mesma entrada dramática |
| Interrupção | Clicar no meio reinicia em vez de reverter |
| Estado inicial | `opacity: 0` sem garantia de reversão |
| Reduced-motion | Ausente, ou removendo tudo em vez de remover o deslocamento |
| Performance | Propriedades de layout animadas; `backdrop-filter` em scroll; `will-change` permanente |
| Cleanup | Timeline sem destruição no unmount |
| Stagger | Sem teto — doze itens somando um segundo de espera |

### Planejar melhorias

*"Melhora o motion do app"* — audita e produz um roteiro executável por outro agente, possivelmente com modelo mais barato.

Cada item do plano precisa ser autossuficiente: arquivo e linha, o que está errado hoje, o valor exato que entra no lugar, e como verificar. Um plano que exige o executor julgar não é plano.

Ordene por **impacto sobre esforço**. Consertar um `ease-in-out` global costuma render mais que qualquer animação nova.

## Formato de achado

```
[Prioridade] Arquivo:linha — o padrão nomeado
  Hoje:     o que existe
  Problema: o critério violado
  Correção: propriedade, duração, curva, valores exatos
  Reduced:  o comportamento sob prefers-reduced-motion
  Trata:    fc-motion-engineer | fc-implementer
```

Prioridade: **Bloqueante** (quebra acessibilidade ou usabilidade) · **Alto** (a pessoa nota e a qualidade cai) · **Médio** (craft) · **Nota**.

## Regras

**Nomeie o padrão, não o sintoma.** "As animações estão ruins" não é achado. "Onze componentes usam `transition: all 0.3s ease-in-out`; `all` anima propriedades não intencionais e a curva é o default" é.

**Não confunda gosto com defeito.** Uma escolha deliberada de motion que difere do seu padrão, mas serve a direção registrada em `DESIGN.md`, não é achado.

**Ausência de motion pode ser certa.** Um dashboard quieto costuma ser um bom dashboard. Não trate a falta de animação como defeito automático.
