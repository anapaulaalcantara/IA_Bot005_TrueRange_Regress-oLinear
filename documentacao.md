# Apresentação

---

É um robô **Scalper para DayTrade** que utiliza um Canal de Regressão Linear como sinal de entrada e a **volatilidade** para calcular alvo e stop dinâmicos.

Possui configurações de alvo e stopLoss, horários de execução, indicadores e proteção de ganhos.

### O Grande Diferencial

---

A `Gestão de Risco` do robô é **dinâmica** e, por isso, **inteligente.** Os valores de `Objetivo de Ganho Diário` e `Proteção de Ganho Diário` são atualizados quando o `Objetivo de Ganho Diário` é atingido.

Além de uma configuração padrão que permite saber o `Resultado da Última Operação`. Quando o resultado for negativo, a próxima entrada será apenas na posição contrária. Isso evita stops consecutivos em movimentos explosivos ou direcionais. Importante lembrar que ainda assim podem ocorrer stops consecutivos, porém apenas em posições opostas.

---

# Configurando Nova Automação

---

Os parâmetros de configurações gerais definem o modo de funcionamento do robô.

Este robo foi desenvolvido para especificamente para operar no Mini Índice na periodicidade de 15 segundos. Algumas configurações são essências para o funcionamento correto da estratégia:

### Editar Automação

- **Geral**
    - Ativo → WIN (contrato atual)
    - Periodicidade → 15 segundos
    - Quantidade por Ordem → 1
    - Quantidade Máxima da Posição → 1 (deve ser igual a Quantidade por Ordem)



- **Entrada**
    - Modo de Execução
        - Realizar envio de ordens no fechamento do candle
        - [x]  Limitar execução ao fechar o candle ou atualização de posição



---

# Editar Parâmetros

---

## Configurações Gerais

Nesse grupo de parâmetros você pode configurar Gain, Loss, janela de negociação e encerramento.

- nGainMulti (0.0) = Fator multiplicador da volatilidade que calcula o alvo GAIN da ordem OCO
- nLossMulti (0.0) = Fator multiplicador da volatilidade que calcula o stop Loss da ordem OCO
- nLimitadorStopLoss(000) = Limita o valor máximo do stop Loss
- HoraEntrada(0000) = Horário inicial para abertura de posições
- HoraFim(0000) = Horário final para abertura de posições
- HoraEncerramento(0000) = Horário de fechamento de operações

Atenção: o fator multiplicador deve ser separados por ponto `.`  e não por vírgula  `,` 

---

## Indicadores

Nesse grupo de parâmetros podem ser configurados os períodos dos indicadores.

- periodoTrueRange(0) = período do indicador de voltatilidade TrueRange que faz o calculo do alvo Gain e stop Loss
- períodoCanal(00) = Período do indicador Canal de Regressão Linear onde então posicionadas as ordens de entrada da posição
- desvioCanal(0.0) = Desvio do indicador Canal de Regressão Linear

---

## Proteção Ganhos

Nesse grupo de parâmetros podem ser configurados a gestão de risco baseada no limite de perda diária, objetivo de ganho diário e proteção de ganho.

- pLimitePerdaDiaria(00.00) = limite de perda diária.
- pObjetivoGanhoDiario(00.00) = objetivo de ganho diário
- pProtecaoGanho(00.00) = proteção de ganho
- pTempoReal(false) = não alterar

Atenção: os valores devem ser separados por ponto(.) e não por vírgula(,)

---

# O Cérebro do Robô

---

**O grande diferencial do robô é a inteligência para administrar o risco.** 

## Gestão de Risco Financeiro

A gestão de risco do robô é dinâmica e, por isso, inteligente. Ela atualiza os resultados quando um dos seguintes parâmetros é atingido:

- Limite de perda diária
- Objetivo de ganho diário
- Proteção de ganhos
    
    ### Limite de perda diária
    
    Quando atingir o Limite de Perda Diária as operações do robô serão interrompidas após o encerramento da posição. Ou seja, não abre mais posições nesse dia.
    
    ### Proteção de ganhos
    
    Quando o robô atinge o limite de Proteção de Ganhos as operações do robô serão interrompidas após o encerramento da posição. Ou seja, não abre mais posições nesse dia.
    
    ### Objetivo de ganho diário
    
    Quando o robô atinge o Objetivo de Ganho Diário, duas coisas acontecem:
    
    - O valor de Objetivo de Ganho Diário é atualizado para um novo valor, somando o Objetivo de Ganho Diário à Proteção de Ganhos. Então agora você tem um novo Objetivo de Ganho Diário e ele irá se manter até ser atingido novamente e recalculado ou, ao atingir o Limites de Perda ou a Proteção de Ganhos, as operações do robô serão interrompidas após o encerramento da posição***.***
    - O valor de Proteção de Ganhos é atualizado para um novo valor, diminuindo do novo valor de Objetivo de Ganho Diário à Proteção de Ganhos. Então agora você tem um novo valor para Proteção de Ganhos e  e ele irá se manter até ser atingido novamente e recalculado ou, ao atingir os Limites de Perda, as operações do robô serão interrompidas após o encerramento da posição***.***

A principal vantagem é continuar operando em dias favoráveis e buscar objetivos de ganhos maiores sempre protegendo uma parte do lucro. 

---

## Abertura de Posição

O robô só abre posição se:

- Estiver dentro do horário de operação
- Não tiver atingido o Limite de Perda Diária
- Não tiver atingido a Proteção de Ganhos
- Resultado da última operação for positivo.
- Resultado da última operação for negativo, somente irá entrar na posição contrária.

---

## Ordens OCO

O robô administra as posições com ordens OCO (one-Cancel-Others) de alvo e stopLoss que são atualizadas a cada fechamento do candle. Quando uma das ordens é executada a outra é cancelada automaticamente.

---

## Alvo e StopLoss Dinâmicos

O mercado é dinâmico e o robô acompanha o seu movimento.  Ao invés de usar alvo e stopLoss fixos, as ordens são recalculadas e reposicionadas de acordo com a volatilidade do período  a cada fechamento do candle. 

---

## Proteção Stop Loss

É uma segurança caso a volatilidade seja muito grande, é possível limitar o valor de stopLoss e fechar a posição a mercado.

---

## Resultado da Última Operação

Quando o resultado for negativo, a próxima entrada será apenas na posição contrária. Isso evita stops consecutivos em movimentos explosivos ou direcionais. Importante lembrar que ainda assim pode ocorrer stops consecutivos, porém apenas em posições opostas.

---

## Recursos Gráficos

Plotagem do indicador Canal de Regressão Linear, Linha Central e desvio Superior e Inferior.

---

# Limitações do Backtest

Devido a uma limitação da plataforma e como o Canal de Regressão linear é dinâmico, **não é possível fazer backtest dessa estratégia**. Sugiro que faça replay de mercado e use a conta simulador  em tempo real para observar o comportamento do robô.

No modo simulador ou replay as ordens não entram na fila como nas operações em conta real. Isso pode gerar divergências no resultado.

Esta é uma estratégia que funciona, porém não é possível dar garantias de resultados positivos. Seja cauteloso e faça os testes com as suas configurações de parâmetros antes de usar em conta real.

Este robô foi testado em conta simulador em tempo real e em conta real.
