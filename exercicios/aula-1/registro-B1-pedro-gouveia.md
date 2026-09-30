# B1 — Registro individual AV1.1

**Estudante:** Pedro Gouveia — **Bloco:** B1 (25/09/2026)
Origem: cartões C1–C3 fictícios do enunciado.

| Cartão | Como faria sem IA / entrada e resultado | Modalidade e justificativa ligada ao cartão | Verificação de aceite | Responsável humano |
|---|---|---|---|---|
| C1 | Ler R2 no contrato, separar suas três condições (estados incluídos, estado excluído, ordem) e escrever uma verificação para cada uma → lista de critérios de aceite. | **Com assistência.** Admitiria IA para produzir o primeiro rascunho dos critérios. O contrato está aprovado e as entradas são válidas, então há referência fixa para conferir o rascunho. | Cada critério precisa distinguir o caso da evidência: `aberto` e `em_andamento` entram, `fechado` sai, e a ordem de entrada se mantém. Critério que não detecta nenhum desses erros é rejeitado. | Pessoa responsável pela manutenção |
| C2 | Ler R3, listar as combinações de departamento (Oficina/Laboratório) e estado (aberto/em_andamento/fechado) e escolher as que provam a regra → entrada fictícia + saída esperada. | **Com assistência.** Admitiria IA para escrever o teste a partir dos casos; a escolha dos casos e da saída esperada fica comigo, porque a IA tende a testar só o caso favorável. | O teste deve cobrir os dois departamentos e incluir um chamado `fechado`, já que R3 vale "independentemente do estado". A saída esperada vem de R3, não do código. | Quem escreve o teste, com revisão de outra pessoa |
| C3 | Antes de decidir, reunir: a regra nova escrita, os dados e perfis afetados, as verificações feitas e quem aprova. Resultado: decisão documentada de autorizar ou não. | **Sem delegar a decisão.** Faltam as quatro informações acima; não há critério contra o qual conferir nada. Um erro de visibilidade expõe chamados de outro departamento em produção. | Não autorizo nas condições atuais. Reavalio quando as quatro informações chegarem e houver um teste equivalente ao de C2 para a regra nova. | Aprovador formal da mudança (ainda não definido) |

**Trecho essencial de evidência**
- **Cartão analisado:** C2. **Regra considerada:** R3.
- **Entrada:** Oficina tem O1 (aberto), O2 (em_andamento) e O3 (fechado); Laboratório tem L1 (aberto).
- **Saída esperada:** um usuário da Oficina vê O1, O2 e O3 e **não** vê L1. Um usuário do Laboratório vê só L1. (Teste planejado, não executado.)
- **Isso sustenta minha escolha porque** o esperado sai de R3, não da implementação. Com ele, eu confiro o teste produzido com assistência: se a IA omitir O3 (fechado) ou não testar o outro departamento, o teste não cobre R3 e é rejeitado.
- **C1 (complementar):** entrada A (aberto), B (fechado), C (em_andamento), nessa ordem → saída esperada **A, C**. Pega a inclusão de B e a inversão da ordem.

**Alternativa para o cartão C1:** fazer sem IA.
**Comparação com minha escolha:** sem IA, gasto mais tempo escrevendo, mas o esforço de revisão e o risco são os mesmos, porque a garantia vem do mesmo caso de verificação. A IA acelera o rascunho; a responsabilidade pelo aceite continua com a pessoa responsável pela manutenção.
**Limite da delegação e condição para rever a escolha:** em C1, eu mudaria para **sem IA** se R2 deixasse de estar aprovada ou se a IA, na conferência, produzisse critérios que não distinguem o caso A/B/C. Em C3, eu autorizaria quando existissem a regra nova escrita, a lista de dados afetados, um teste equivalente ao de C2 e um aprovador nomeado. Urgência não substitui essas verificações.

**Procedência/IA:** ferramenta: Claude (Anthropic), modelo não informado; tarefa delegada: revisar e reescrever o texto a partir das minhas decisões por cartão; trecho aproveitado: estrutura e casos de teste; minha verificação/intervenção: conferi os casos contra R2 e R3 do contrato. O raciocínio e a decisão registrados são meus.

**Revisão:** [x] três decisões; [x] evidência localizada; [x] alternativa e limite; [x] até uma página.
