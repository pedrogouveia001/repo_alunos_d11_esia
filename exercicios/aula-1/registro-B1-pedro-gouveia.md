# B1 — Registro individual AV1.1

**Estudante:** Pedro Gouveia — **Bloco:** B1 (25/09/2026)
Origem: cartões C1–C3 fictícios do enunciado.

| Cartão | Processo sem IA / entrada → saída | Modalidade e justificativa ligada ao cartão | Verificação de aceite | Responsável humano |
|---|---|---|---|---|
| C1 | Ler R2 → escrever critérios de aceite verificáveis | **Com assistência.** Contrato aprovado e entradas válidas: há referência para conferir o rascunho da IA. | Aplicar cada critério ao caso da evidência abaixo; critério que não distingue o caso é rejeitado. | Pessoa responsável pela manutenção |
| C2 | Ler R3 → montar entrada e saída esperada do teste | **Com assistência.** A regra é clara, mas a escolha dos casos é minha: a IA tende a testar só o caso favorável. | Teste cobre os três estados e os dois departamentos (ver evidência). | Quem escreve o teste, com revisão de outra pessoa |
| C3 | Receber pedido → decidir sobre implantação | **Sem delegar a decisão.** Faltam regra nova, dados afetados, verificação e aprovador; não há critério contra o qual conferir. | Não autorizo; reavalio quando as 4 informações ausentes chegarem. | Aprovador formal da mudança (ainda não definido) |

**Trecho essencial de evidência:**
- **C1** — Entrada: A (aberto), B (fechado), C (em_andamento), nessa ordem de chegada. Saída esperada: **A, C**. Pega os dois erros prováveis: incluir B (fechado) ou inverter a ordem.
- **C2** — Entrada: Oficina tem O1 (aberto), O2 (em_andamento), O3 (fechado); Laboratório tem L1 (aberto). Usuário da Oficina → vê **O1, O2, O3** e **não vê L1**. Repetir com usuário do Laboratório → vê só **L1**. O3 (fechado) testa o trecho "independentemente do estado", que um teste só com chamados abertos não cobriria.

**Alternativa para o cartão C1:** fazer sem IA.
**Comparação com minha escolha (restrição e consequência):** sem IA leva mais tempo, mas o risco é o mesmo, porque a garantia vem do mesmo caso de verificação. A IA acelera o rascunho; não transfere a responsabilidade.
**Limite da delegação e condição para rever a escolha (C3):** autorizo quando houver regra nova escrita, lista dos dados afetados, teste equivalente ao de C2 para a regra nova e aprovador nomeado. Urgência não substitui verificação.

**Procedência/IA:** ferramenta: Claude (Anthropic), modelo não informado; tarefa delegada: revisar e reescrever o texto a partir das minhas decisões por cartão; trecho aproveitado: estrutura e casos de teste; minha verificação/intervenção: conferi os casos contra R2 e R3 do contrato. O raciocínio e a decisão registrados são meus.

**Revisão:** [x] três decisões; [x] evidência localizada; [x] alternativa e limite; [x] até uma página.
