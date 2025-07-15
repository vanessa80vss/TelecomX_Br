Projeto: Análise de Evasão de Clientes (Churn) - ETL + EDA

Este repositório contém o processo completo de ETL (Extração, Transformação e Limpeza) dos dados de clientes, seguido de uma Análise Exploratória de Dados (EDA) focada em entender o comportamento dos clientes que cancelaram o serviço (Churn).

📚 Introdução

O objetivo deste projeto é compreender os fatores que levam à evasão de clientes em uma empresa de serviços (telecom, por exemplo). A análise parte de um dataset no formato JSON hospedado no GitHub e percorre as seguintes etapas:
ETL completo com tratamento de colunas aninhadas (dicts)
Limpeza e transformação de dados
Criação de colunas derivadas
Análise visual de cancelamentos (Churn)

📁 Dataset

Origem: JSON no GitHub (contendo colunas aninhadas como customer, phone, internet, account)
Total de registros: 7.267
Fonte: Projeto fictício para aprendizado em Data Science

⚙️ 1. Processo de ETL

✅ Importação de bibliotecas e leitura do JSON

import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

✅ Normalização das colunas aninhadas (dicts)

Colunas tratadas com pd.json_normalize():
customer
phone
internet
account (incluindo Charges.Monthly e Charges.Total)

✅ Renomeação de colunas para nomes mais amigáveis

Exemplos:
gender → Genero
SeniorCitizen → Idoso
tenure → Meses_De_Contrato
Charges.Monthly → Valor_Mensal

✅ Conversão de tipos e valores nulos

Colunas numéricas foram convertidas com pd.to_numeric(..., errors='coerce')
Removidos registros com Churn ou Valor_Total nulos

✅ Criação da coluna Valor_Diario
df['Valor_Diario'] = df['Valor_Mensal'] / 30

✅ Salvar dataset limpo
df.to_csv('df_limpo.csv', index=False)

2. Análise Exploratória (EDA)

✅ 2.1 Análise descritiva

df.describe()
df.select_dtypes(include='object').nunique()
df['Cancelamento'].value_counts(normalize=True)

✅ 2.2 Distribuição do Churn

sns.countplot(x='Cancelamento', data=df, palette='pastel')

✅ 2.3 Churn por variáveis categóricas

sns.countplot(x='Tipo_Contrato', hue='Cancelamento', data=df, palette='Set2')
sns.countplot(x='Metodo_Pagamento', hue='Cancelamento', data=df, palette='Set3')

✅ 2.4 Churn por variáveis numéricas

sns.boxplot(x='Cancelamento', y='Meses_De_Contrato', data=df, palette='Set2')
sns.boxplot(x='Cancelamento', y='Valor_Total', data=df, palette='Set1')

🔎 Conclusões e Insights
Clientes com contratos mensais são os que mais cancelam.
Métodos de pagamento automáticos estão associados a menor evasão.
Clientes com menor tempo de contrato são mais propensos ao churn.

💡 Recomendações

Incentivar contratos anuais com benefícios para reduzir churn.
Promover pagamentos automáticos com descontos.
Implementar programas de fidelidade para clientes novatos nos primeiros 6 meses.

📄 Como usar este repositório

Clone o repositório:
1 - git clone https://github.com/vanessa80vss/TelecomX_Br.git
2- Execute o notebook TelecomX_Br.ipynb

🚀 Próximos passos

Treinamento de modelos de Machine Learning para previsão de churn.
Análise com features de valor preditivo.
Dashboard interativo.

📅 Status: Concluído (ETL + EDA)

Autor: Vanessa Santos

