# AV2 — Entrega individual

Estudante: Pedro Gouveia · Data: 30/09/2026 · Via: inspeção + execução opcional

## Análise

**1. Recorte e requisito.**
- **O que avalio:** a função `pode_visualizar_proposta` e a documentação que a acompanha. Quem usa o resultado é a manutenção de Fila Clara, para decidir o aceite.
- **Fora do escopo:** autenticação, banco de dados e validação de entradas externas.
- **Regra (R3):** a pessoa vê o chamado se, e somente se, ele for do mesmo departamento. Estado e prioridade não importam.
- **R4:** a documentação deve dizer o mesmo que R3.
- **Critério de aceite, definido antes de testar:** o código acerta todos os casos da matriz, e a documentação não acrescenta nem retira nenhuma condição de R3.

**2. Estratégia.**
- **Eixos:** departamento (igual ou diferente) × estado (aberto ou fechado), formando os 4 casos T1–T4, com uma pessoa da Oficina. O estado entra na matriz porque R3 diz que ele **não** deve mudar a decisão, e isso precisa ser testado.
- **Caso decisivo:** T2, Oficina com chamado fechado. É o único que mostra se o estado interfere.
- **Caso de controle:** T1, Oficina com chamado aberto. Mostra que o código funciona no caso simples.
- **Casos extras:** T5 testa o estado `em_andamento`; T6 testa uma pessoa do Laboratório.

**3. Evidência.**
- **Código:** acerta T1, T3, T4 e T5. **Erra T2 e T6:** R3 permite ver um chamado fechado do próprio departamento, e o código bloqueia. A causa é o trecho `and chamado["estado"] != "fechado"` (anexo, E2).
- **Documentação:** diz que "chamados fechados ficam indisponíveis" (E3). Repete o mesmo erro do código.
- Código e texto concordam entre si, mas **os dois contrariam R3**. Concordarem não prova que estão certos.

**4. Decisão.**
- **Código: rejeitado.** Erra no caso decisivo.
- **Documentação: rejeitada.** Descreve uma regra diferente de R3.
- **Alternativa descartada:** aceitar com condição e corrigir depois. Não serve, porque o erro está no centro da regra.
- **Correção proposta:** remover o trecho do estado, deixando `return chamado["departamento"] == departamento`. Testei de novo e a versão corrigida acerta os 6 casos (anexo).
- **Nova documentação:** "A pessoa vê os chamados do próprio departamento, em qualquer estado. Chamados de outros departamentos não aparecem. Prioridade não altera a decisão."
- **Responsável pelo aceite:** a pessoa responsável pela manutenção de Fila Clara.
- **Mudaria minha decisão se:** R3 fosse alterada oficialmente para esconder chamados fechados.

**5. Procedência e limites.**
- **Origem:** contrato, código, documentação e dados de `insumos.md`, todos simulados. O caso T5 foi construído por mim.
- **Inferido × observado:** previ os resultados de T1–T4 lendo o código e depois confirmei executando. A nova documentação é só uma proposta.
- **Limite:** não variei a prioridade separadamente do departamento. Seis casos não provam que a correção está certa em todos os cenários, mas um único erro (T2) já basta para rejeitar.
- **IA:** Claude (Anthropic), modelo não informado, em 30/09/2026. Usei para explicar o enunciado, organizar o texto e escrever o script de teste. A matriz, a identificação dos erros e as decisões são minhas, e conferi a execução contra a minha previsão.

## Anexo técnico

**Dados:** registros V-01 a V-04 de `insumos.md` e V-05 construído por mim.

| Caso | Chamado | Quem pede | Esperado (R3) | Código retornou | Status | Resultado |
|---|---|---|---|---|---|---|
| T1 | V-01 Oficina, aberto | Oficina | vê | vê | inferido e observado | ✅ controle |
| T2 | V-02 Oficina, fechado | Oficina | vê | **não vê** | inferido e observado | ❌ decisivo |
| T3 | V-03 Laboratório, aberto | Oficina | não vê | não vê | inferido e observado | ✅ |
| T4 | V-04 Laboratório, fechado | Oficina | não vê | não vê | inferido e observado | ✅ |
| T5 | V-05 Oficina, em_andamento | Oficina | vê | vê | observado | ✅ |
| T6 | V-04 Laboratório, fechado | Laboratório | vê | **não vê** | observado | ❌ |

**E1 — contrato** (`insumos.md`): "R3: `pode_visualizar` permite acesso somente à pessoa do mesmo departamento do chamado, independentemente de estado ou prioridade."

**E2 — código e caminho lógico:**
```python
return (
    chamado["departamento"] == departamento
    and chamado["estado"] != "fechado"
)
```
- T2: departamento igual → True; estado `fechado` → False; True **e** False = **False**. R3 espera True.
- T1: departamento igual → True; estado `aberto` → True; True e True = True. Correto.

**E3 — documentação** (`insumos.md`): "chamados fechados ficam indisponíveis". Contradiz o "independentemente de estado" de R3.

**Execução:** Python 3.12.10, arquivo separado `av2_verifica.py`, sem alterar o repositório. Comando: `python -B av2_verifica.py`.
```
proposta T1 V-01 solicitante=Oficina esperado=True retorno=True OK
proposta T2 V-02 solicitante=Oficina esperado=True retorno=False DIVERGE
proposta T3 V-03 solicitante=Oficina esperado=False retorno=False OK
proposta T4 V-04 solicitante=Oficina esperado=False retorno=False OK
proposta T5 V-05 solicitante=Oficina esperado=True retorno=True OK
proposta T6 V-04 solicitante=Laboratório esperado=True retorno=False DIVERGE
```

**Versão corrigida, testada de novo:**
```
ajustada T1 V-01 solicitante=Oficina esperado=True retorno=True OK
ajustada T2 V-02 solicitante=Oficina esperado=True retorno=True OK
ajustada T3 V-03 solicitante=Oficina esperado=False retorno=False OK
ajustada T4 V-04 solicitante=Oficina esperado=False retorno=False OK
ajustada T5 V-05 solicitante=Oficina esperado=True retorno=True OK
ajustada T6 V-04 solicitante=Laboratório esperado=True retorno=True OK
```
