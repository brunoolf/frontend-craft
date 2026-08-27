---
name: ux-patterns
description: Padroes de UX para interface web - arquitetura de informacao, hierarquia, carga cognitiva, estados de interface (vazio, carregando, erro, sucesso), formularios, navegacao, UX copy, e as diferencas entre desktop e web mobile. Use ao desenhar ou revisar fluxo, estrutura de tela, estados ou textos de interface.
---

# Padrões de UX

Carregue `surface-modes` antes desta skill. O modo decide quais padrões se aplicam — densidade que é defeito numa landing é virtude num dashboard.

## Hierarquia

Uma tela responde três perguntas, nesta ordem: **onde estou**, **o que posso fazer**, **o que aconteceu**.

- Uma coisa é a mais importante e parece a mais importante. Se três gritam, nenhuma é ouvida.
- Ação primária, secundária e terciária são visualmente distintas. Dois botões com o mesmo peso não são hierarquia.
- O que a pessoa veio buscar está acima da dobra ou a um scroll óbvio.

## Carga cognitiva

Toda coisa que a pessoa precisa segurar na cabeça entre um passo e outro é um erro em potencial.

- Não faça lembrar o que você pode mostrar. Se o passo 3 precisa de um valor do passo 1, exiba o valor.
- Agrupe por tarefa, não por tipo técnico. "Notificações" reúne todas; não espalhe entre Conta, Privacidade e Avançado.
- Sete itens é onde uma lista sem estrutura começa a exigir esforço. Acima disso, agrupe ou dê busca.
- Progressive disclosure onde o avançado é raro — mas nunca esconda o que a maioria precisa.

## Estados

Um componente sem estes está pela metade:

**Vazio.** O mais negligenciado e o mais formador — é o primeiro que a pessoa vê. Nunca "Nenhum resultado". Diga o que aquilo vai conter, por que está vazio e qual a próxima ação. Distinga *vazio porque é novo* de *vazio porque o filtro não achou* — são situações opostas.

**Carregando.** Abaixo de 300ms, nada. Até 3s, indicador. Acima, progresso com noção de quanto falta. Skeleton só quando a forma final é conhecida — senão ele mente sobre o layout.

**Erro.** Nomeia o problema **e** a recuperação. "Algo deu errado" não é mensagem. Erro de campo fica junto do campo. Erro de sistema preserva o que a pessoa digitou — perder um formulário preenchido por causa de um 500 é falha de design, não de backend.

**Sucesso.** Proporcional. Confirmação discreta para o comum; celebração só para o marco real.

**Parcial.** Metade carregou, metade falhou. Mostre o que veio e o que faltou, com opção de tentar de novo só a parte que falhou.

## Formulários

- Uma coluna. Layouts de duas colunas criam ambiguidade de ordem de leitura.
- Label acima do campo, sempre visível. Placeholder como label desaparece exatamente quando é preciso.
- Peça o mínimo. Todo campo é uma chance de desistência — justifique cada um.
- Valide na saída do campo, não a cada tecla. Mostrar erro enquanto a pessoa ainda digita é hostil.
- Mensagem de erro específica: "A senha precisa de 8 caracteres", não "Senha inválida".
- Formato aceito é generoso: telefone com ou sem traço, cartão com ou sem espaço. Normalize você.
- Campo obrigatório marcado, e opcional também quando a maioria é obrigatória.
- `autocomplete` e `inputmode` corretos. Teclado numérico em campo de CEP é acabamento barato e muito notado.

## Navegação

- A pessoa sempre sabe onde está. Estado ativo inequívoco.
- Voltar funciona. Se você quebrou o botão do navegador, quebrou o produto.
- URL reflete o estado onde faz sentido — poder compartilhar e recarregar é funcionalidade.
- Ação destrutiva com confirmação **ou** desfazer. Prefira desfazer: confirmação vira reflexo e deixa de proteger.

## UX copy

- Botão nomeia a ação: "Salvar alterações", não "Enviar" nem "OK".
- Voz do produto, consistente. Se em algum lugar é "você", é "você" em todos.
- Sem culpar a pessoa. "O e-mail não parece válido", não "Você digitou errado".
- Sem jargão interno vazando. "Sincronizar" pode não significar nada para quem usa.
- Números e datas em formato legível na localidade. Um ISO 8601 cru numa tela de usuário é vazamento de banco de dados.
- **Nunca invente conteúdo factual.** Preço, prazo, garantia, número de clientes: se não pode verificar, marque como pendência do usuário. Preencher com plausível é o pior defeito possível.

## Desktop e web mobile

**Desktop:** hover pode carregar informação, mas nunca ser o único caminho. Foco de teclado visível e ordem de Tab lógica. Atalhos para ação repetida. Clique com botão direito onde houver expectativa.

**Web mobile:** alvos de toque com no mínimo 24×24px (WCAG 2.2), 44×44 como meta em superfície primariamente móvel. Espaçamento entre alvos — dois botões destrutivos vizinhos é armadilha. Nada depende de hover. Respeite as áreas seguras (notch, indicador de home). `100dvh` em vez de `100vh`. A parte inferior da tela é a mais alcançável; ação primária pertence lá em fluxo longo.

Não presuma toque por largura de tela. Laptops têm tela sensível ao toque; tablets têm mouse. Projete para ambos onde não custa.
