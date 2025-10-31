# Análise de Séries Temporais — Fundamentos Teóricos

Este repositório tem como objetivo estudar e aplicar **modelos clássicos de séries temporais**, analisando propriedades como **estacionariedade**, **tendência** e **sazonalidade**, e explorando os principais modelos estatísticos da família **ARIMA**: **AR**, **ARMA**, **SARIMA** e **SARIMAX**.

---

##  O que é uma Série Temporal?

Uma **série temporal** é um conjunto de observações coletadas ao longo do tempo em intervalos regulares — por exemplo, vendas mensais, temperatura diária ou número de acessos por hora.  
O foco da análise é entender **como o tempo influencia os dados** e construir modelos capazes de **prever valores futuros**.

As séries temporais costumam apresentar três componentes principais:

1. **Tendência:** direção de longo prazo (crescimento ou queda).
2. **Sazonalidade:** padrões que se repetem periodicamente (ex: aumento de vendas em dezembro).
3. **Ruído:** variações aleatórias não explicadas por tendência nem sazonalidade.

---

##  Estacionariedade

Uma série é considerada **estacionária** quando suas propriedades estatísticas — como média, variância e covariância — **não mudam ao longo do tempo**.  
Em outras palavras, ela oscila em torno de uma média constante e não apresenta tendência ou sazonalidade persistente.

Por que isso é importante?  
Modelos como **AR**, **ARMA**, **SARIMA** e **SARIMAX** assumem que as relações entre períodos passados e futuros **são estáveis**.  
Se a série não for estacionária, o modelo pode gerar previsões imprecisas.

### Como testar a estacionariedade?

Existem dois testes estatísticos principais:

- **ADF (Augmented Dickey-Fuller):**  
  Hipótese nula: a série não é estacionária.  
  Se o p-valor < 0.05, rejeita-se a hipótese nula e conclui-se que a série é estacionária.

- **KPSS (Kwiatkowski–Phillips–Schmidt–Shin):**  
  Hipótese nula: a série é estacionária.  
  Se o p-valor < 0.05, rejeita-se a hipótese nula e conclui-se que a série não é estacionária.

O ideal é que o teste ADF indique estacionariedade e o KPSS não a rejeite, confirmando a consistência do resultado.

---

##  Diferenciação

A **diferenciação** é o processo utilizado para **remover tendências** e tornar a série estacionária.  
Ela consiste em subtrair o valor atual do valor anterior, reduzindo a dependência de longo prazo e estabilizando a média da série.

- **d:** número de diferenciações aplicadas para remover tendência.  
- **D:** número de diferenciações sazonais para eliminar padrões periódicos.

Após aplicar a diferenciação, é comum refazer os testes de estacionariedade para confirmar se a série está pronta para modelagem.

---

##  Sazonalidade

A **sazonalidade** ocorre quando há **padrões que se repetem em intervalos regulares de tempo**, como:

- aumento nas vendas no final do ano;  
- maior consumo de energia durante o verão;  
- ciclos de produção agrícola a cada estação.

Identificar e modelar corretamente a sazonalidade é fundamental para previsões mais realistas.  
Ela pode ser observada em gráficos de linha e confirmada por funções como a **ACF** (autocorrelação), que mostra a relação entre valores de diferentes períodos.

---

##  Modelos de Séries Temporais

### 1. AR (AutoRegressive)

O modelo **AR(p)** supõe que o valor atual de uma série depende linearmente de um número definido de **valores passados**.  
É indicado para séries estacionárias que apresentam autocorrelação significativa entre observações próximas.

---

### 2. ARMA (AutoRegressive Moving Average)

O modelo **ARMA(p, q)** combina dois componentes:

- **AR (AutoRegressivo):** dependência dos valores passados;  
- **MA (Média Móvel):** dependência dos erros passados.

Esse modelo é ideal para séries **estacionárias e não sazonais**, nas quais há padrões de dependência de curto prazo.

---

### 3. SARIMA (Seasonal ARIMA)

O modelo **SARIMA(p, d, q)(P, D, Q, s)** é uma generalização do ARIMA que considera **componentes sazonais**.  
Ele modela tanto as relações de curto prazo (não sazonais) quanto as de longo prazo (sazonais), sendo amplamente utilizado em previsões reais.

- **p, d, q:** parâmetros não sazonais (autorregressivo, diferenciação, média móvel).  
- **P, D, Q:** parâmetros sazonais.  
- **s:** período da sazonalidade (por exemplo, 12 para dados mensais com padrão anual).

O SARIMA é especialmente útil em séries que apresentam **tendência e padrões periódicos**, como vendas, temperatura ou produção industrial.

---

### 4. SARIMAX (Seasonal ARIMA com Exogenous)

O modelo **SARIMAX** é uma extensão direta do **SARIMA**, mas com um recurso adicional:  
ele permite incluir **variáveis exógenas (X)** — ou seja, fatores externos que também influenciam a série.

Essas variáveis podem representar eventos, campanhas, indicadores econômicos ou qualquer outro fator externo que ajude o modelo a compreender melhor os padrões da série.

Exemplos de uso:

- Prever vendas considerando também **gastos com marketing**.  
- Estimar demanda levando em conta **temperatura ou feriados**.  
- Projetar consumo energético com base em **índices de produção industrial**.

Em resumo:
> O **SARIMAX** é o mesmo modelo **SARIMA**, mas com um parâmetro adicional que permite incorporar variáveis externas (exógenas), tornando-o mais flexível e realista.

---

##  Resumo Comparativo

| Modelo | Usa valores passados | Usa erros passados | Considera sazonalidade | Aceita variáveis externas | Requer série estacionária |
|:--------|:----------------------|:--------------------|:-------------------------|:----------------------------|:---------------------------|
| **AR** | ✔️ | ❌ | ❌ | ❌ | ✔️ |
| **ARMA** | ✔️ | ✔️ | ❌ | ❌ | ✔️ |
| **SARIMA** | ✔️ | ✔️ | ✔️ | ❌ | ⚙️ (obtida via diferenciação) |
| **SARIMAX** | ✔️ | ✔️ | ✔️ | ✔️ | ⚙️ (obtida via diferenciação) |

---

##  Conclusão

- **Estacionariedade** é essencial para que o modelo capture relações temporais consistentes.  
- **Diferenciação** é o principal método para remover tendências e estabilizar a série.  
- **Sazonalidade** deve ser identificada e modelada quando houver padrões periódicos claros.  
- O **SARIMAX** amplia o SARIMA, permitindo considerar **variáveis externas** que afetam o comportamento da série.  
- Juntos, esses modelos formam uma base sólida para análises e previsões temporais confiáveis.

Esses fundamentos são a base para qualquer projeto de previsão temporal robusto e servem como guia para os notebooks e scripts deste repositório.
