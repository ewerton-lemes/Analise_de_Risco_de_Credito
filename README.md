# Análise de Risco de Crédito
Análise exploratória, de associação e de correlação aplicada a dados de empréstimos e risco de crédito utilizando Excel visando responder uma pergunta de negócio.

## Sobre o Projeto

Este projeto apresenta uma análise exploratória, de correlação e de associação (Information Value) de uma base de dados relacionada a empréstimo e risco de crédito com dados de 7000 clientes.
A base de dados é sintética (não possui dados reais), mas é baseada em comportamentos reais de empréstimos e usada para fins de análise, educação e práticas de modelagem preditiva.

Fonte: https://www.kaggle.com/datasets/deepakkaushal/financial-loan-credit-risk-dataset

Baixada em 07/09/2026

### Variáveis na base de dados (metadados)

**Loan_ID:** Identificador exclusivo atribuído a cada solicitação de empréstimo individual.

**Application_Date:** Data exata em que a solicitação foi enviada.

**Customer_Age:** Idade do principal solicitante do empréstimo.

**Gender:** Gênero informado pelo solicitante.

**Marital_Status:** Estado civil do solicitante.

**Education_Level:** Maior nível de escolaridade alcançado pelo solicitante.

**Employment_Type:** Situação profissional ou cargo corporativo do solicitante.

**Annual_Income:** Renda anual verificada do solicitante, expressa em unidades monetárias padrão.

**Credit_Score:** Pontuação numérica de crédito que avalia a capacidade de crédito do solicitante.

**Existing_Loans_Count:** Número de empréstimos ativos ou preexistentes que o solicitante possui atualmente em instituições financeiras.

**Number_of_Dependents:** Número de familiares ou dependentes legais que dependem da renda do solicitante.

**Home_Ownership:** Situação habitacional do solicitante.

**Region:** Localização geográfica ou continente de onde a solicitação foi enviada.

**Loan_Purpose:** Principal finalidade para a qual o empréstimo está sendo solicitado.

**Loan_Amount:** Valor monetário total solicitado para o empréstimo.

**Loan_Term_Months:** Duração total do contrato de empréstimo, especificada em meses.

**Interest_Rate:** Taxa percentual de juros associada ao empréstimo solicitado.

**Monthly_Installment:** Valor calculado da parcela mensal para o pagamento do empréstimo.

**Debt_to_Income_Ratio:** Razão entre o total das obrigações mensais de dívida do solicitante e sua renda mensal bruta, expressa em porcentagem. (DTI)

**Loan_Status:** Resultado operacional da solicitação de empréstimo.

**Repayment_Status:** Resultado histórico ou final de como o empréstimo está sendo pago.

## Objetivos

O objetivo desse projeto é responder a seguinte pergunta de negócio:

**Quais características dos clientes e dos empréstimos estão associadas à aprovação ou rejeição de uma solicitação de crédito?**

Para responder a essa pergunta, faremos inicialmente uma análise exploratória dos dados para conhecer bem a base de dados:

**Perfil do Cliente:** Customer_Age, Education_Level, Employment_Type, Home_Ownership, Gender, Marital_Status, Number_of_Dependents.

**Perfil financeiro do cliente:** Annual_Income, Credit_Score, Debt_to_Income_Ratio, Existing_Loans_Count.

**Características do empréstimo:** Loan_Amount, Loan_Term_Months, Interest_Rate, Monthly_Installment, Loan_Purpose, Loan_Status

Depois dessa análise exploratória, faremos uma análise de correlação entre as variáveis numéricas da base de dados.

Após essa análise de correlação, faremos o cálculo do Information Value das variáveis que possuem maior poder preditivo em relação à rejeição ou aprovação do empréstimo.

Em seguida calcularemos o R² (coeficiente de determinação) para avaliar a associação entre algumas variáveis.

Por fim, vamos cruzar os dados de Credit_Score e Debt_to_Income (DTI) para verificar a taxa de rejeição combinando essas variáveis.

## Principais Insights

**1. O comprometimento da renda está fortemente associado à rejeição**

Na tabela a seguir vemos que, para as faixas de DTI apresentadas, quanto maior o DTI, maior é a taxa de rejeição.

| Faixa de DTI | Taxa de rejeição |
|---|---:|
| < 20% | 0,2% |
| 20–30% | 0,2% |
| 30–40% | 1,9% |
| 40–50% | 4,4% |
| 50–60% | 3,4% |
| 60–70% | 12,0% |
| 70–80% | 24,8% |
| > 80% | **31,9%** |

Além disso, o Information Value (IV) = 3,65, indicando forte poder de discriminação na amostra. No cálculo do IV e da tabela acima foram considerados somente os clientes com créditos aprovados e rejeitados, os que possuíam crédito pendente não foram considerados. Além disso esse IV alto deve ser avaliado, pois pode ter ocorrido *data leakage*.

**2. O Crédit Score apresenta uma forte associado à rejeição.**

Na tabela segiunte vemos que, para as faixas de Credit Score apresentadas, quanto maior o maior o Credit_Score, menor é a taxa de rejeição.

| Faixa de Credit Score | Taxa de rejeição |
|---|---:|
| < 600 | **41,5%** |
| 600–649 | 9,2% |
| 650–699 | 1,9% |
| 700–749 | 0,4% |
| 750–799 | 0,0% |
| ≥ 800 | 0,0% |

O Information Value (IV) = 2,39 indica uma forte associação à rejeição. Nesse cálculo de IV e da tabela acima também foram considerados somente os clientes com créditos aprovados e rejeitados, os que possuíam crédito pendente não foram considerados. Além disso esse IV alto deve ser avaliado, pois pode ter ocorrido *data leakage*.

**3. Credit Score e DTI, analisados conjuntamente, permitem identificar perfis distintos**

As faixas de Credit Score e de DTI foram separadas dessa forma:

| Faixa | Intervalo de Credit Score | Significado |
|---|---:|---|
| **Muito baixo** | < 600 | Baixo histórico de crédito e maior indicação de risco |
| **Baixo** | 600–699 | Histórico de crédito abaixo do ideal |
| **Bom** | 700–759 | Histórico de crédito considerado favorável |
| **Muito bom** | ≥ 760 | Histórico de crédito muito favorável e menor indicação de risco |

| Faixa | Intervalo de DTI | Significado |
|---|---:|---|
| **Baixo comprometimento** | < 40% | Baixa parcela da renda comprometida com dívidas |
| **Comprometimento moderado** | 40%–59,9% | Parcela relevante da renda comprometida |
| **Alto comprometimento** | 60%–79,9% | Elevada parcela da renda comprometida |
| **Comprometimento muito alto** | ≥ 80% | Parcela muito elevada da renda comprometida com dívidas |

O heatmap abaixo mostra a taxa de rejeição para cada combinação entre faixa de Credit Score e DTI.

![Heatmap](https://raw.githubusercontent.com/ewerton-lemes/Analise_de_Risco_de_Credito/main/heatmap.png)


A análise conjunta de Credit Score e DTI evidencia que a combinação de baixa pontuação de crédito e elevado comprometimento da renda está associada às maiores taxas de rejeição, enquanto scores elevados combinados a baixo DTI apresentam taxas muito inferiores. Para a criação desse heatmap foram descartados os clientes que possuíam a informação de Credit Score ausente.

## Outros achados relevantes

**1. Valor solicitado**

A taxa de rejeição apresenta tendência de crescimento conforme aumenta o valor solicitado, passando de 4,33% na menor faixa para valores superiores a 20% nas faixas mais elevadas.

Information Value: 0,388.

**2. Finalidade do empréstimo**

A finalidade também apresenta diferenças relevantes nas taxas de rejeição. As maiores taxas foram observadas em Home (15,81%) e Business (12,50%), enquanto Medical apresentou 2,29%.

Information Value: 0,362.

## Observação sobre os insights

Acima estão listados os principais insights, os que estão diretamente relacionados à pergunta de negócio. As outras análise mencionadas nos Objetivos estão no arquivo excel, juntamente com seus insights, que está na pasta https://github.com/ewerton-lemes/Analise_de_Risco_de_Credito/tree/main/analise. A maioria deles são descritivos.

## Recomendações de negócio

1. Utilizar DTI como indicador central de capacidade de pagamento

Como o DTI foi a variável com maior poder de discriminação entre aprovados e rejeitados, recomenda-se utilizá-lo como um dos principais indicadores na avaliação do comprometimento financeiro do solicitante.

2. Combinar Credit Score e DTI na avaliação de risco
   
A análise mostra que histórico de crédito e comprometimento da renda capturam aspectos diferentes do risco. A utilização conjunta dessas variáveis pode proporcionar uma avaliação mais completa do perfil do solicitante.

3. Avaliar o valor solicitado em conjunto com a capacidade financeira

Valores de empréstimo mais elevados apresentaram maior associação com rejeições. Portanto, o valor solicitado deve ser analisado em relação à renda e ao DTI do cliente, evitando avaliar o montante isoladamente.

4. Aplicar análises diferenciadas conforme a finalidade do empréstimo

Como a finalidade apresentou diferenças relevantes nas taxas de rejeição, recomenda-se acompanhar o risco por tipo de empréstimo e investigar as razões dessas diferenças antes de estabelecer critérios específicos para cada finalidade.

5. Utilizar os resultados como apoio à decisão, não como regras automáticas
   
Os resultados identificam associações, e não relações causais. Antes de transformar esses padrões em regras de concessão de crédito, seria necessário validar os achados com dados adicionais e testar um modelo preditivo em dados fora da amostra.

## Dashboard

Na última aba da planilha que está no arquivo excel da pasta https://github.com/ewerton-lemes/Analise_de_Risco_de_Credito/tree/main/analise está um dashboard onde os insights podem ser vistos por meio de gráficos. Além disso há filtros para ver as informações, por exemplo, por gênero ou região do solicitante.

![Dashboard](https://raw.githubusercontent.com/ewerton-lemes/Analise_de_Risco_de_Credito/main/imagens/dashboard.png)








