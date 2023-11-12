# IA_Bot005_TrueRange_Regress-oLinear

# Apresentação

---

É um robô **Scalper para DayTrade**  em linguagem NTSL (Profit) que utiliza um Canal de Regressão Linear como sinal de entrada e a **volatilidade** para calcular alvo e stop dinâmicos.

Possui configurações de alvo e stopLoss, horários de execução, indicadores e proteção de ganhos.

### O Grande Diferencial

---

A `Gestão de Risco` do robô é **dinâmica** e, por isso, **inteligente.** Os valores de `Objetivo de Ganho Diário` e `Proteção de Ganho Diário` são atualizados quando o `Objetivo de Ganho Diário` é atingido.

Além de uma configuração padrão que permite saber o `Resultado da Última Operação`. Quando o resultado for negativo, a próxima entrada será apenas na posição contrária. Isso evita stops consecutivos em movimentos explosivos ou direcionais. Importante lembrar que ainda assim podem ocorrer stops consecutivos, porém apenas em posições opostas.
