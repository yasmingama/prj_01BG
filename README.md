Exercicio:

Desafio Final Objetivo: Combinar tudo o que foi aprendido. Dado um conjunto de dados fictício sobre vendas (por exemplo, id_cliente, valor_compra, data_compra): • Identifique os clientes com maior valor de compra. • Agrupe as compras por ano e calcule o total de vendas anuais. • Salve os resultados em um formato de sua escolha (CSV, JSON, etc.
Resposta:

# Desafio Final - Análise de Vendas com Python e Pandas

# Etapa 1: Importação das bibliotecas necessárias
import pandas as pd
from io import StringIO

# Etapa 2: Criando um conjunto de dados fictício
data = StringIO("""
id_cliente,valor_compra,data_compra
101,250.50,2021-03-15
102,100.00,2021-07-22
103,310.20,2022-01-10
101,500.00,2022-05-30
104,75.99,2022-11-03
102,200.00,2023-02-12
105,980.00,2023-08-19
103,150.00,2023-10-21
""")

df = pd.read_csv(data, parse_dates=['data_compra'])

# Etapa 3: Identificar os clientes com maior valor de compra (total por cliente)
clientes_top = df.groupby('id_cliente')['valor_compra'].sum().sort_values(ascending=False)
print("Clientes com maior valor de compra:")
print(clientes_top)

# Etapa 4: Agrupar as compras por ano e calcular o total de vendas anuais
df['ano'] = df['data_compra'].dt.year
vendas_anuais = df.groupby('ano')['valor_compra'].sum()
print("\nTotal de vendas por ano:")
print(vendas_anuais)

# Etapa 5: Salvando os resultados em arquivos CSV e JSON
clientes_top.to_csv('clientes_top.csv', header=['valor_total_compras'])
vendas_anuais.to_json('vendas_anuais.json', orient='index')

# Fim do desafio!
print("\nArquivos 'clientes_top.csv' e 'vendas_anuais.json' foram gerados com sucesso.")

