# B3 — Registro individual AV1.3

**Estudante:** Pedro Gouveia — **Bloco:** B3 (26/09/2026)
**O que a listagem e a documentação precisam cumprir, conforme R2/R4:** a listagem inclui `aberto` e `em_andamento`, exclui `fechado` e preserva a ordem de entrada (R2). A documentação descreve esse mesmo comportamento: o que entra, o que sai e a ordem (R4).

| Caso / estado a verificar | Entrada (IDs e ordem) | IDs esperados na ordem | Obrigação de R2 e como verificar |
|---|---|---|---|
| 1 / aberto | [TR-33] | [TR-33] | Inclusão de `aberto`: conferir que TR-33 aparece na saída. |
| 2 / em_andamento | [TR-31] | [TR-31] | Inclusão de `em_andamento`: conferir que TR-31 aparece na saída. |
| 3 / fechado | [TR-32] | [] | Exclusão de `fechado`: conferir que a saída é vazia. |

**Entrada combinada TR-31, TR-32, TR-33 → IDs esperados:** [TR-31, TR-33]
**Como conferiria a ordem:** na entrada, TR-31 está na posição 1 e TR-33 na posição 3; na saída, TR-31 deve vir antes de TR-33. TR-32 (posição 2, `fechado`) sai do meio sem alterar a ordem relativa dos demais. Caso adicional com a entrada invertida [TR-33, TR-31] → esperado [TR-33, TR-31]: a saída deve repetir a ordem da entrada. Uma implementação que ordenasse por ID devolveria [TR-31, TR-33] e seria detectada só por esse caso.
**Documentação proposta (até três frases):** A lista mostra chamados abertos e em andamento, sem os fechados. Eles aparecem na ordem de chegada: quem entrou primeiro aparece primeiro.

**Etapa em que admitiria IA / tarefa que ela faria / pessoa responsável por conferir:** etapa de teste; a IA escreveria os testes a partir dos casos acima; eu confiro o resultado.
**O que essa pessoa deve verificar antes de aprovar:** que cada teste gerado usa a entrada e a saída esperada da tabela (calculadas por R2, não pela implementação), que existe um teste por estado, que o caso combinado confere a ordem e que o caso invertido está incluído.
**Alternativa sem IA e comparação:** escrever os testes manualmente a partir da mesma tabela. Leva mais tempo, mas a conferência é a mesma, porque a garantia vem dos esperados derivados de R2. Com IA, o risco extra é ela produzir testes que conferem só o caso favorável ou omitem a ordem; por isso a verificação acima é obrigatória.
**O que os casos não verificam e o que me faria rever a aprovação:** a entrada de três registros já chega na ordem dos IDs e tem um chamado por estado; ela não distingue "preservar a ordem de entrada" de "ordenar por ID", nem testa vários chamados do mesmo estado. Eu reveria a aprovação se o caso invertido [TR-33, TR-31] falhasse ou se a documentação deixasse de mencionar a ordem.

**Origem dos dados e como fiz a análise:** entrada fictícia do enunciado; esperado por contrato: saídas esperadas calculadas por R2; inspeção própria: leitura de R2/R4 e comparação de posições; execução opcional: não realizada.
**Uso de IA neste registro:** ferramenta-modelo visível: Claude (Anthropic), modelo não informado; contexto/tarefa: explicar o enunciado e organizar minhas respostas no modelo; trecho aproveitado e minha verificação: redação e estrutura. Os casos, a saída combinada, o caso invertido, a documentação e a decisão sobre IA são meus; conferi cada saída contra R2.

**Revisão:** [x] três estados; [x] ordem; [x] texto; [x] aceite/limite; [x] uma página.
