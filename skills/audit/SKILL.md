---
name: audit
description: Auditoria tecnica read-only de acessibilidade (WCAG 2.2), performance e comportamento responsivo em interface web. Traz os criterios verificaveis, os padroes buscaveis e o formato de achado com evidencia medida. Use quando algo esta lento ou travando, quando quebra no mobile, quando ha duvida sobre acessibilidade, ou como verificacao antes de publicar.
---

# Auditoria técnica

Você produz fatos verificáveis. Onde não puder medir, diga que não mediu e o que seria preciso.

## Acessibilidade — WCAG 2.2

**Contraste.** Corpo e placeholder ≥4.5:1. Texto grande (≥24px, ou ≥18.66px bold) ≥3:1. Componentes de UI, bordas de campo e indicador de foco ≥3:1 (SC 1.4.11). Calcule os pares que **de fato ocorrem** — um token que falha numa combinação que nunca acontece não é achado.

**Teclado.** Todo interativo alcançável por Tab, em ordem lógica. `tabindex` positivo quebra a ordem e é achado. Armadilha de foco só dentro de modal, e com saída por Escape. Indicador de foco visível: `outline: none` sem substituto é **bloqueante**. Modal devolve o foco ao gatilho ao fechar.

**Semântica.** Headings em ordem, sem pular nível. Um `<h1>` por página. Landmarks (`main`, `nav`, `header`, `footer`). Todo campo com label associado — `placeholder` não é label. `<button>` para ação, `<a>` para navegação. `<div onClick>` é achado.

**Imagem e mídia.** `alt` significativo em imagem de conteúdo; `alt=""` em decorativa. Nenhuma informação transmitida só por cor. Vídeo com legenda.

**Movimento.** `prefers-reduced-motion` respeitado. Nada que pisque entre 3 e 55 Hz. Carrossel automático com controle de pausa.

**Alvos de toque.** Mínimo 24×24 CSS px com espaçamento adequado (SC 2.5.8). 44×44 é a meta em superfície primariamente móvel.

**Formulários.** Erro identificado em texto (não só cor), associado ao campo, e anunciado por região viva. `autocomplete` nos campos de identidade.

## Performance

**Layout shift (CLS).** Imagem e vídeo com `width`/`height` ou `aspect-ratio`. Fonte com `font-display` e métricas de fallback ajustadas. Conteúdo injetado acima da dobra — banner, aviso — é a causa mais comum.

**LCP.** O maior elemento acima da dobra carrega cedo. `priority` ou `fetchpriority="high"` **só** nele. Fonte do heading pré-carregada.

**Bundle.** O que entra no caminho crítico. Biblioteca importada inteira quando um símbolo basta. Ícones importados um a um de pacote sem tree-shaking. WebGL ou engine de animação carregada de forma síncrona. Fronteira de client component alta demais em Next.

**Animação.** Propriedades que disparam layout. `backdrop-filter` em container que rola. `filter: blur` em área grande. Handler de scroll sem throttle. Múltiplos `requestAnimationFrame` competindo.

**Imagem.** Formato moderno. Dimensão real versus exibida — servir 3000px para exibir 400 é o desperdício mais comum. `loading="lazy"` abaixo da dobra. `sizes` correto em imagem responsiva.

**Render (React).** Objeto ou função recriada em prop de componente memoizado. Lista longa sem virtualização. Estado alto demais na árvore causando re-render em cascata. `key` por índice em lista que reordena.

## Responsivo

Teste com **conteúdo real**. A maioria dos defeitos aparece no texto de verdade, não no placeholder.

Verifique 360px, 768px, 1280px e um viewport muito largo. Procure:

- Transbordo horizontal — o corpo da página nunca rola na horizontal.
- Alvo de toque que colapsou abaixo do mínimo.
- Texto quebrando em uma palavra por linha.
- Layout assimétrico que não colapsa em coluna única.
- Tabela ou bloco de código sem container próprio de `overflow-x`.
- `h-screen` / `100vh` em vez de `100dvh` — o primeiro salta no Safari iOS.
- Elemento sobreposto com margem negativa criando conflito de toque no mobile.

## Padrões buscáveis

```
outline:\s*none|outline-none          foco removido
<div[^>]*onClick                       interativo sem semântica
tabIndex=\{?-?[1-9]                    tabindex positivo
100vh|h-screen                         viewport instável no iOS
addEventListener\(['"]scroll           reflow contínuo
transition.*\b(width|height|top|left)  propriedade de layout animada
<img(?![^>]*alt=)                      imagem sem alt
role="button"                          verificar se devia ser <button>
z-\[?[0-9]{3,}                         z-index arbitrário
import \* as|from ['"]lodash['"]       import não tree-shakeable
```

Acerto é candidato, não veredito. Verifique antes de reportar.

## Formato

```
[Severidade] arquivo:linha
  Critério:  o nomeado — "WCAG 2.2 SC 1.4.3" ou "CLS: imagem sem dimensão"
  Evidência: o valor medido — "3.1:1, mínimo 4.5:1"
  Correção:  o que muda
  Trata:     fc-implementer | fc-design-system | fc-motion-engineer
```

**Severidade:** Bloqueante (barreira de acesso ou quebra funcional) · Alto (impacto real e mensurável) · Médio · Nota.

## Regras

**Meça, não presuma.** "Isso pode estar lento" não é achado. Ou mediu, ou declara que não conseguiu e o que faltou.

**Verifique antes de reportar.** O suposto problema pode ter tratamento em outro arquivo. Falso positivo por reflexo destrói a confiança na lista inteira.

**Acessibilidade não é opinião.** Contraste e alvo de toque são números. Reporte o número.

**Você não conserta.** Produz achados; os agentes de escrita tratam.
