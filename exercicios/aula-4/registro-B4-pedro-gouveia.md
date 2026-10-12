# B4 — Registro individual AV1.4

**Estudante:** Pedro Gouveia — **Bloco:** B4 (02/10/2026)
**Critério de aceite por R2:** a listagem mostra `aberto` e `em_andamento`, esconde `fechado` e mantém a ordem de chegada. Prioridade (impacto + urgência) não altera a ordem.

| Entrada | IDs esperados por R2 | IDs do candidato | Status | Mecanismo/trecho essencial |
|---|---|---|---|---|
| TR-41, TR-42, TR-43, TR-44 | TR-41, TR-42, TR-44 | **TR-42, TR-44, TR-41** | Inferido por leitura e observado em execução | `sorted(ativos, key=lambda c: c["impacto"] + c["urgencia"], reverse=True)` reordena por escore (6, 4, 2) |

O filtro está certo (TR-43 sai), mas a ordem não: o candidato troca a ordem de chegada pela de prioridade.

**Teste entregue — o que verifica e o que não consegue distinguir:** na entrada do teste, a ordem de chegada (TR-42, TR-44, TR-41) coincide com a ordem decrescente de escore (6, 4, 2). Por isso R2 e o candidato produzem a mesma lista, e o teste passa nos dois casos. Ele confere o filtro do fechado, mas **não distingue** "manter a ordem de chegada" de "ordenar por prioridade".
**Trecho do teste:** entrada TR-42, TR-44, TR-41, TR-43; asserção: IDs == `["TR-42", "TR-44", "TR-41"]`. Esperado por R2 para essa entrada: TR-42, TR-44, TR-41. Retorno do candidato: TR-42, TR-44, TR-41. Iguais.
**Decisão e motivo:** **rejeitar.** O candidato descumpre a preservação da ordem de R2 na entrada de revisão, e o teste entregue não seria capaz de detectar esse erro.
**Comparação entre manter e ajustar / responsável pelo aceite:** manter exibiria os chamados fora da ordem de chegada, contrariando R2, com um teste verde que dá falsa confiança. Ajustar exige uma mudança de uma linha e um teste novo. A aprovação fica com a pessoa responsável pela manutenção de Fila Clara.
**Ajuste proposto:** remover a ordenação e devolver a lista filtrada como está:
```python
def listar_ativos_proposta(chamados):
    return [c for c in chamados if c["estado"] in ("aberto", "em_andamento")]
```
Substituir o teste por um em que a ordem de chegada seja diferente da ordem de prioridade.

| Caso para conferir o ajuste: entrada e ordem | IDs esperados | Resultado / status |
|---|---|---|
| TR-41, TR-42, TR-43, TR-44 | TR-41, TR-42, TR-44 | TR-41, TR-42, TR-44 — previsto por leitura e observado em execução; coincide |

Com essa entrada, o candidato original devolveria TR-42, TR-44, TR-41 e falharia; a versão ajustada passa. É o caso que separa as duas.

**Limite remanescente e condição para rever o parecer:** conferi duas entradas, ambas com um único chamado fechado; não testei vários chamados com o mesmo escore nem lista vazia. Eu reveria a rejeição se R2 fosse alterada oficialmente para ordenar por prioridade.
**Origem dos dados e da análise:** candidato, teste e entrada simulados do enunciado; método próprio: inspeção, depois execução em cópia isolada (`python -B av14.py`, Python 3.12.10). Saída: revisão → proposta `['TR-42', 'TR-44', 'TR-41']`, ajustada `['TR-41', 'TR-42', 'TR-44']`; entrada do teste → as duas `['TR-42', 'TR-44', 'TR-41']`.
**Uso de IA neste registro:** Claude (Anthropic), modelo não informado; tarefa: explicar o enunciado, corrigir meu cálculo da entrada do teste, organizar o texto e escrever o script de execução; trecho aproveitado: redação, estrutura e script. A identificação do fechado, a ordem por escore e a conclusão de que o teste não distingue as duas versões são minhas; conferi a execução contra a leitura.

**Revisão:** [x] comparação com R2; [x] alcance do teste; [x] ajuste/revalidação; [x] status; [x] uma página.
