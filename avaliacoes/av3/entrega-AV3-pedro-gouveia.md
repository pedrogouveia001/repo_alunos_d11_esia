# AV3 — Entrega individual

Estudante: Pedro Gouveia · Data: 12/10/2026 · Caso/recorte: Fila Clara — assistência de IA para propor testes e documentação das regras R1–R4

## Parecer

**1. Recomendação e problema.** Recomendo **adoção condicionada** da assistência de IA para propor testes e documentação das regras R1–R4. Beneficiária: a equipe de manutenção de Fila Clara. Resultado esperado: testes e textos que conferem as regras e que uma pessoa aprova. Restrições: nenhuma ferramenta ou política de dados confirmada (AV1.5); iniciativa sem nenhuma execução com usuários (AV1.6, M5); propostas plausíveis podem estar erradas (AV2, AV1.4).

| Alternativa | Processo e recursos | Benefício esperado / pressuposto | Limite, consequência do erro e esforço de verificação |
|---|---|---|---|
| A — sem IA | A manutenção escreve testes e documentação à mão, a partir das regras. | Nenhum risco de dados; quem escreve conhece a regra. | Mais tempo de escrita. O erro continua possível (quem escreve olhando o código copia o erro), e a revisão contra a regra é a mesma. |
| B — IA com condições | A IA propõe testes e textos usando só dados sintéticos; uma pessoa revisa contra R1–R4 antes de qualquer uso. | Rascunho mais rápido, pressupondo que a revisão pega os erros. Ganho de tempo **não comprovado**. | Proposta errada e convincente (AV2, AV1.4) e risco de vazamento de dados. Exige revisão de toda proposta. |

**Minha comparação e razão para a recomendação:** nas duas alternativas, a garantia vem da mesma coisa: conferir o resultado esperado contra a regra. A IA não elimina essa conferência; só pode acelerar o rascunho. Por isso recomendo B com condições e **começando pelo piloto**: se a IA não mostrar ganho sem aumentar erros, voltamos a A, que continua disponível.

**2. Autonomia e responsabilidade.**
- **A IA pode:** sugerir casos de teste, resultados esperados e textos de documentação.
- **Exige aceite humano:** todo teste e todo texto, antes de qualquer uso. Quem aprova é uma pessoa da manutenção **diferente** de quem pediu à IA. O critério é: o esperado foi tirado das regras R1–R4, e há pelo menos um caso capaz de falhar se o código estiver errado.
- **Intervenção e recusa:** a revisora rejeita a proposta que não cumprir o critério. Nada vai para produção a partir de uma sugestão da IA. Uma saída inadequada é simplesmente descartada, sem custo de desfazer.

**3. Verificação e contraponto.**
- **E1 (AV2):** entrada V-02 (Oficina, fechado) para uma pessoa da Oficina. Critério R3: vê, em qualquer estado. Resultado do candidato: não vê, observado em execução. **Interpretação:** uma proposta plausível, acompanhada de documentação coerente com ela, contrariava a regra. A conferência contra R3 pegou o erro, e é essa conferência que a condição de revisão exige.
- **E2 (AV1.4), contraponto:** o teste entregue junto com a função passava com a função errada, porque na entrada dele a ordem de chegada coincidia com a ordem de prioridade. **Efeito:** a revisão só funciona se olhar a **qualidade do teste**, não só se ele passa. Por isso o critério exige um caso capaz de falhar. Eu mudaria a recomendação para A se o piloto mostrar que testes desse tipo passam pela revisão.

**4. Riscos e mecanismos.**

| Risco e consequência no recorte | Mecanismo | Responsável | Evidência e como conferir o controle | Exceção/interrupção |
|---|---|---|---|---|
| 1 — Dado real (colaborador, incidente, acesso) enviado a ferramenta não autorizada, sem saber retenção ou treino. | Só dados sintéticos vão para a IA; conferência antes de enviar. | Pessoa que faz o pedido | Lista de verificação datada e assinada: fonte do material e itens conferidos. Outra pessoa confere a lista. | Uso de dado real só com decisão registrada da segurança e da gestora. Sem isso, o envio não acontece. |
| 2 — Teste ou texto errado aprovado como certo, dando falsa confiança. | Revisão por outra pessoa, esperado tirado das regras, um caso capaz de falhar. | Revisora da manutenção | Registro de revisão por proposta: regra, esperado, caso que pegaria o erro, decisão. | Uma proposta errada aprovada interrompe o piloto (condição da seção 5). |

**5. Maturidade e próximo passo.**
- **Estágio:** protótipo. Definição: artefato demonstrável em ambiente controlado. Fatos: M1 (demonstração com três exemplos sintéticos), M5 (zero execuções com usuários) e M6 (nenhum resultado medido).
- **Estágio rival:** piloto. Não se aplica porque responsável (M2), revisão (M3) e plano (M4) são preparação, não execução. **Lacuna:** execução do plano com resultados registrados.
- **Passo proposto:** executar o plano de M4 durante duas semanas, com as duas pessoas da manutenção, só com dados sintéticos, sob a responsável designada em M2.
- **Métrica:** taxa de aproveitamento = propostas aprovadas, com ou sem correção ÷ total de propostas revisadas. Contagem complementar: propostas erradas que a revisão aprovou.
- **Coleta e referência:** a revisora marca cada proposta numa planilha datada. Referência: as metas propostas abaixo, porque não há série anterior (M6). **Limite:** mede só os erros que a revisão percebeu.
- **Avanço (gestora decide):** 70% ou mais **e** nenhuma proposta errada aprovada.
- **Interrupção (responsável age):** abaixo de 40% **ou** qualquer proposta errada aprovada.
- As metas são **propostas**, não resultados.

**6. Fundamentação aplicada.**
- **F1, Fan et al. (2023, Seção IV):** a IA atua como sistema de sugestão, e cabe ao desenvolvedor filtrar a saída inventada antes que entre no código. **Aplica-se a:** revisão humana obrigatória (seção 2). **Minha inferência:** E1 mostra que, em Fila Clara, uma proposta plausível pode estar errada, o que confirma a necessidade desse filtro. **Limite:** o artigo trata de completar código, não de gerar testes. A taxa de 22% relatada para a Meta é de outro contexto e não serve como meta para o caso.
- **F2, Hou et al. (2024, Seção 8.1.1):** com intenção ambígua, a IA pode gerar código sintaticamente correto e funcionalmente incorreto. Os autores também registram vazamentos de dados pessoais durante o uso de prompts. **Aplica-se a:** revisão contra a regra, e não contra o código (seção 2), e ao risco 1 (seção 4). **Minha inferência:** E1 e E2 são exatamente esse padrão: código que roda, mas não cumpre R3 ou R2. **Limite:** é uma revisão de estudos. Mostra que os problemas existem, não com que frequência acontecerão em Fila Clara.

## Anexo — evidências, referências e procedência

**E1 — AV2** (`avaliacoes/av2/entrega-AV2-pedro-gouveia.md`, anexo, linha T2). Candidato: `return chamado["departamento"] == departamento and chamado["estado"] != "fechado"`. Entrada V-02 (Oficina, fechado), solicitante Oficina; esperado por R3: True; retorno: False. Status: inferido por leitura e observado em execução (`proposta T2 V-02 solicitante=Oficina esperado=True retorno=False DIVERGE`).

**E2 — AV1.4** (`exercicios/aula-4/registro-B4-pedro-gouveia.md`). Teste entregue: entrada TR-42, TR-44, TR-41, TR-43; asserção IDs == `["TR-42", "TR-44", "TR-41"]`. Esperado por R2 e retorno do candidato, para essa entrada: os dois iguais a TR-42, TR-44, TR-41. Na entrada de revisão (TR-41 a TR-44), o candidato devolve TR-42, TR-44, TR-41 e R2 exige TR-41, TR-42, TR-44. Status: inferido por leitura e observado em execução.

**F1:** Angela Fan, Beliz Gokkaya, Mark Harman, Mitya Lyubarskiy, Shubho Sengupta, Shin Yoo, Jie M. Zhang. *Large Language Models for Software Engineering: Survey and Open Problems*. arXiv:2310.03533, v4, 2023. Seção IV, "Code Generation and Completion", parágrafos iniciais. https://arxiv.org/abs/2310.03533v4

**F2:** Xinyi Hou, Yanjie Zhao, Yue Liu, Zhou Yang, Kailong Wang, Li Li, Xiapu Luo, David Lo, John Grundy, Haoyu Wang. *Large Language Models for Software Engineering: A Systematic Literature Review*. arXiv:2308.10620, v6, 2024. Seção 8.1.1, "Challenges in LLM Applicability", parágrafos "Data dependency" e "Ambiguity in code generation". https://arxiv.org/abs/2308.10620v6

**Procedência:** materiais simulados reaproveitados: contrato R1–R4, insumos de AV2, AV1.4, AV1.5 e AV1.6. Observações próprias: execuções da AV2 e da AV1.4 em cópias isoladas. Inferências: estágio de protótipo e relação entre as fontes e o caso. Propostas não executadas: piloto, métrica e metas de 70% e 40%. Os trechos de F1 e F2 foram lidos por mim em 12/10/2026, na versão HTML do arXiv, durante a preparação desta entrega; o fichamento L0 não foi entregue antes.
**IA:** Claude (Anthropic), modelo não informado; data: 12/10/2026; tarefa: explicar o enunciado, abrir os artigos, confirmar a seção dos trechos que escolhi, traduzir e organizar o texto no modelo; trecho aproveitado: redação e estrutura. A recomendação (usar com condições), a escolha dos trechos de F1 e F2, as regras de dados e revisão, o estágio de protótipo e a métrica vêm das minhas respostas nas atividades anteriores; conferi E1 e E2 contra os meus registros.

**Checklist:** [x] alternativas; [x] autonomia; [x] evidência/contraponto; [x] dois riscos; [x] maturidade/métrica; [x] duas fontes aplicadas; [x] procedência; [x] 3+2 páginas.
