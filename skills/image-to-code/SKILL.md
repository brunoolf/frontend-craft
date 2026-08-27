---
name: image-to-code
description: Transformar mockup, screenshot ou referencia visual em codigo de interface funcional. Cobre a leitura estruturada da imagem, a extracao do sistema implicito antes de escrever markup, e a verificacao contra o original. Use quando o usuario fornece uma imagem de design para implementar ou quer reproduzir a aparencia de uma referencia.
---

# Imagem para código

Adaptada da skill original do taste-skill, que era escrita para outro runtime. O método é o mesmo; as ferramentas são as deste ambiente.

## O erro que define o resultado

A tentação é começar pelo topo da imagem e ir descendo, escrevendo markup. Isso produz uma reprodução que parece certa numa largura e desmorona em qualquer outra, com dezenas de valores mágicos e nenhum sistema.

**Extraia o sistema antes de escrever qualquer markup.**

## 1. Leia a imagem estruturalmente

Antes de código, responda:

- **Grade.** Quantas colunas, qual gutter, qual largura máxima do container. Meça a partir de elementos alinhados.
- **Escala de espaçamento.** Meça os espaços verticais reais e procure a base. Valores como 16, 24, 32, 48, 64 revelam base 8; 12, 20, 28 revelam base 4.
- **Escala tipográfica.** Meça cada tamanho distinto. Agrupe os quase-iguais — costumam ser o mesmo degrau.
- **Cores.** Extraia os valores. Agrupe por papel (superfície, texto, borda, destaque), não por matiz.
- **Raio, sombra, borda.** Também são escalas.
- **Repetição.** O que aparece mais de uma vez é componente, não instância.

## 2. Escreva o sistema

Converta as medidas em tokens antes de qualquer JSX. Se o projeto já tem `DESIGN.md`, reconcilie: use os tokens existentes onde forem próximos e reporte as divergências reais em vez de criar uma segunda escala paralela.

## 3. Construa de fora para dentro

Layout e grade primeiro; depois componentes; depois detalhe. Construir de dentro para fora produz componentes que não encaixam.

## 4. Verifique

Compare lado a lado com a imagem. Procure especificamente:

- Espaçamento vertical entre seções — o defeito mais comum e o mais visível.
- Pesos de fonte. Confundir 500 com 600 muda a percepção inteira.
- Cor de texto secundário. Quase nunca é o cinza que parece à primeira vista.
- Alinhamento óptico versus matemático. Ícone ao lado de texto quase sempre precisa de ajuste de 1px.
- Contraste de escala entre display e corpo.

## O que a imagem não te diz

Uma imagem é um estado, numa largura. Você é responsável por tudo que ela omite:

- **Todos os breakpoints.** A imagem não mostra o mobile. Derive do sistema, não do palpite.
- **Todos os estados.** Hover, foco, disabled, loading, erro, vazio. Nenhum aparece no mockup.
- **Conteúdo real.** O mockup tem o texto do tamanho perfeito. O produto não terá. Teste com texto longo e curto.
- **Movimento.** Se a direção pede, veja `motion-principles`.
- **Acessibilidade.** Contraste do mockup frequentemente falha. Quando falhar, ajuste e **avise** — não reproduza um defeito de acessibilidade por fidelidade.

## Fidelidade versus correção

Reproduza a intenção, não os defeitos. Quando o mockup viola algo do `craft-floor` — contraste insuficiente, alvo de toque pequeno, medida de linha de 120 caracteres — implemente a versão correta e liste o que mudou e por quê. Fidelidade pixel a pixel a um erro não é serviço.

A exceção é quando o usuário diz explicitamente que quer fidelidade exata. Aí implemente como pedido e reporte os problemas em separado.

## Se não houver imagem

Se o usuário quer uma referência visual antes de construir, gere primeiro com `imagegen-web` — uma imagem por seção, não um board comprimido — e depois aplique este método sobre elas.
