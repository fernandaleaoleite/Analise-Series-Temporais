# 📊 Análise de Séries Temporais — Fundamentos Teóricos

Este repositório tem como objetivo estudar e aplicar **modelos clássicos de séries temporais**, analisando propriedades como **estacionariedade**, **tendência** e **sazonalidade**, e explorando os principais modelos estatísticos da família **ARIMA**: **AR**, **ARMA** e **SARIMA**.

---

## 🧠 O que é uma Série Temporal?

Uma **série temporal** é um conjunto de observações coletadas ao longo do tempo em intervalos regulares — por exemplo, vendas mensais, temperatura diária ou número de acessos por hora.  
O foco desse tipo de análise é entender **como o tempo influencia os dados** e construir modelos capazes de **prever valores futuros**.

As séries temporais costumam apresentar três componentes principais:

1. **Tendência:** direção de longo prazo (crescimento ou queda).
2. **Sazonalidade:** padrões que se repetem periodicamente (ex: vendas que sobem todo dezembro).
3. **Ruído:** variações aleatórias não explicadas por tendência nem sazonalidade.

---

## ⚖️ Estacionariedade

Um dos conceitos mais importantes em séries temporais é a **estacionariedade**.

Uma série é **estacionária** quando suas propriedades estatísticas — como média, variância e covariância — **não mudam ao longo do tempo**.  
Em outras palavras, ela **oscila em torno de um valor constante**, sem tendência ou padrões sazonais persistentes.

Por que isso é importante?  
➡️ Modelos como **AR**, **ARMA** e **SARIMA** partem da suposição de que os relacionamentos entre períodos passados e futuros **são estáveis**.  
Se a série não for estacionária, o modelo pode gerar previsões enganosas.

### 🔍 Como testar a estacionariedade?

Existem dois testes estatísticos principais:

- **ADF (Augmented Dickey-Fuller):**  
  - Hipótese nula: a série **não é estacionária**.  
  - Se o *p-valor* < 0.05 → rejeita-se a hipótese nula → a série **é estacionária**.

- **KPSS (Kwiatkowski–Phillips–Schmidt–Shin):**  
  - Hipótese nula: a série **é estacionária**.  
  - Se o *p-valor* < 0.05 → rejeita-se a hipótese nula → a série **não é estacionária**.

O ideal é que:
> O ADF indique estacionariedade e o KPSS **não a rejeite**, confirmando o resultado.

---

## 🔁 Diferenciação

A **diferenciação** é o processo de **remover tendências e tornar a série estacionária**.

Ela consiste em subtrair o valor atual pelo valor anterior:

\[
Y'_t = Y_t - Y_{t-1}
\]

Essa transformação elimina a dependência linear de longo prazo, estabilizando a média da série.  
Se ainda houver tendência ou padrão sazonal, podem ser aplicadas **diferenciações adicionais**, tanto simples quanto sazonais.

- **d:** número de diferenciações não sazonais (remove tendência).  
- **D:** número de diferenciações sazonais (remove padrões periódicos).  

Após aplicar a diferenciação, é comum **refazer os testes de estacionariedade** para confirmar o resultado antes da modelagem.

---

## 🔄 Sazonalidade

A **sazonalidade** representa **padrões que se repetem em intervalos fixos de tempo** — por exemplo:

- Aumento no consumo de energia durante o verão.  
- Queda de vendas após feriados.  
- Ciclos econômicos anuais ou trimestrais.

Detectar e modelar corretamente a sazonalidade é essencial para previsões mais realistas.  
Ela pode ser identificada visualmente (gráficos) ou por meio de funções estatísticas como **ACF** (Autocorrelation Function), que mostra correlações entre períodos separados por certo intervalo de tempo.

---

## ⚙️ Modelos de Séries Temporais

### 🔹 AR (AutoRegressive)

O modelo **AR(p)** supõe que o valor atual da série depende linearmente de **p observações anteriores**.

\[
Y_t = c + \phi_1 Y_{t-1} + \phi_2 Y_{t-2} + ... + \phi_p Y_{t-p} + \varepsilon_t
\]

- **p:** número de defasagens (lags) consideradas.  
- **ϕ:** coeficientes que medem o impacto de cada valor passado.  
- **ε:** ruído branco (erro aleatório).

Ele é indicado para séries estacionárias que apresentam **autocorrelação significativa** entre valores próximos no tempo.

---

### 🔹 ARMA (AutoRegressive Moving Average)

O modelo **ARMA(p, q)** combina dois componentes:

- **AR(p):** dependência dos valores passados.  
- **MA(q):** dependência dos erros passados (médias móveis dos resíduos).

\[
Y_t = c + \sum_{i=1}^{p}\phi_i Y_{t-i} + \sum_{j=1}^{q}\theta_j \varepsilon_{t-j} + \varepsilon_t
\]

- **p:** número de termos autorregressivos.  
- **q:** número de termos de média móvel.  

O **ARMA** é adequado para séries **estacionárias e não sazonais**.

---

### 🔹 SARIMA (Seasonal ARIMA)

O **SARIMA(p, d, q)(P, D, Q, s)** é uma generalização do ARIMA que inclui **componentes sazonais**.

Ele modela tanto as **relações de curto prazo** (não sazonais) quanto as **de longo prazo** (sazonais), sendo um dos modelos mais completos e utilizados em previsão.

- **p, d, q:** componentes não sazonais (autorregressivo, diferenciação, média móvel).  
- **P, D, Q:** componentes sazonais (autorregressivo, diferenciação, média móvel).  
- **s:** período da sazonalidade (ex: 12 para dados mensais com ciclo anual).

Essa combinação permite capturar tendências e padrões repetitivos de forma robusta.

---

## 🧾 Resumo Comparativo

| Modelo | Usa valores passados | Usa erros passados | Considera sazonalidade | Requer série estacionária |
|:--------|:----------------------|:--------------------|:-------------------------|:---------------------------|
| **AR** | ✔️ | ❌ | ❌ | ✔️ |
| **ARMA** | ✔️ | ✔️ | ❌ | ✔️ |
| **SARIMA** | ✔️ | ✔️ | ✔️ | ⚙️ (obtida via diferenciação) |

---

## 🧩 Conclusão

- **Estacionariedade** é a base para qualquer modelagem temporal confiável.  
- **Diferenciação** é o método para estabilizar séries e remover tendências.  
- **Sazonalidade** precisa ser reconhecida e modelada quando há padrões periódicos.  
- Os modelos **AR**, **ARMA** e **SARIMA** evoluem em complexidade conforme incorporam dependências e sazonalidades.  

Esses fundamentos são essenciais para análises preditivas robustas e interpretações estatísticas corretas em qualquer projeto de séries temporais.

---
