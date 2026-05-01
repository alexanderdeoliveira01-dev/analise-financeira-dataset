# analise-financeira-dataset
# Análise de Dados - Cartão de Crédito

Projeto de análise exploratória utilizando Python, Pandas e Matplotlib.

# 📊 Análise Financeira - Credit Card Dataset

Este notebook tem como objetivo analisar as características financeiras do dataset 
"default_of_credit_card_clients".

Serão analisadas as variáveis relacionadas a valores de fatura (BILL_AMT) e pagamentos (PAY_AMT), 
utilizando estatísticas descritivas, histogramas e transformações logarítmicas para melhor compreensão dos dados.
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Carregar o dataset
df = pd.read_excel('default_of_credit_card_clients__courseware_version_1_21_19.xls')

# Visualizar os primeiros dados
df.head()
## Exercício 1 - Listas de características financeiras

Criação de listas contendo as variáveis de valores de fatura e pagamentos.
bill_features = ['BILL_AMT1', 'BILL_AMT2', 'BILL_AMT3',
                 'BILL_AMT4', 'BILL_AMT5', 'BILL_AMT6']

pay_features = ['PAY_AMT1', 'PAY_AMT2', 'PAY_AMT3',
                'PAY_AMT4', 'PAY_AMT5', 'PAY_AMT6']
                ## Exercício 2 - Estatísticas descritivas das faturas

Analisando medidas como média, mediana, mínimo e máximo.
df[bill_features].describe()
### 🔎 Análise

Observa-se que os valores apresentam grande variação entre mínimo e máximo, indicando presença de outliers.

A média e a mediana diferem em várias colunas, o que sugere distribuição assimétrica.

Valores negativos podem representar créditos ou ajustes na fatura, o que faz sentido no contexto financeiro.
## Exercício 3 - Histogramas das faturas
df[bill_features].hist(bins=20, figsize=(12,8))
plt.suptitle('Distribuição dos Valores de Fatura')
plt.show()
### 🔎 Análise

As distribuições são assimétricas à direita, com concentração em valores menores e poucos valores muito altos.

Isso indica que a maioria dos clientes possui faturas baixas, enquanto poucos possuem gastos elevados.
## Exercício 4 - Estatísticas descritivas dos pagamentos
df[pay_features].describe()
### 🔎 Análise

Os dados mostram muitos valores próximos de zero, indicando que vários clientes não realizaram pagamentos em determinados meses.

Há também grande variação entre mínimo e máximo, com alguns pagamentos muito altos.
## Exercício 5 - Histogramas dos pagamentos
df[pay_features].hist(bins=20, figsize=(12,8), xrot=45)
plt.suptitle('Distribuição dos Pagamentos')
plt.show()
### 🔎 Análise

Os histogramas mostram forte concentração em zero, indicando muitos meses sem pagamento.

A distribuição é altamente assimétrica.
## Exercício 6 - Contagem de pagamentos iguais a zero
mask_zero = df[pay_features] == 0
zeros_count = mask_zero.sum()

zeros_count
### 🔎 Análise

Há uma grande quantidade de valores iguais a zero, o que confirma o comportamento observado nos histogramas.

Isso indica que muitos clientes não efetuaram pagamento em determinados períodos.
## Exercício 7 - Transformação logarítmica dos pagamentos
# Filtrar apenas valores maiores que zero
df_pay_nonzero = df[pay_features][df[pay_features] > 0]

# Aplicar log10
df_log = df_pay_nonzero.apply(np.log10)

# Plotar histogramas
df_log.hist(bins=20, figsize=(12,8))
plt.suptitle('Pagamentos (log10) - Valores > 0')
plt.show()
### 🔎 Análise

Após a transformação logarítmica, os dados ficam mais distribuídos e menos assimétricos.

O uso do log reduz o impacto de valores extremos e facilita a análise dos padrões de pagamento.

Essa técnica é comum em análise de dados quando há grande variação de escala.
## ✅ Conclusão

A análise mostrou que:

- Os valores de fatura possuem grande variação e presença de outliers.
- Os pagamentos apresentam muitos valores iguais a zero.
- As distribuições são assimétricas, especialmente nos pagamentos.
- A transformação logarítmica melhora a visualização e interpretação dos dados.

Esses padrões são esperados em dados financeiros, onde há grande diversidade no comportamento dos clientes.
