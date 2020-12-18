# Dashboard de Horas Extras e Painel de Gestão de Pessoas

## Objetivo
Criação, através da ferrementa Data Google Studio, um Dashboard de Horas Extras e um Painel de Gestão de Pessoas para a empresa CESAN.

Tanto o dashboard quanto o painel buscam prover informações, organizadas de forma intuitiva, para subsidiar a tomada de decisões.

Todos os dados contidos no link abaixo são ilusórios e foram colocados apenas para formar uma base de simulação.

IMPORTANTE: Todos os passos abaixo estão diretamente voltados para a construção da ferramenta. Apesar de terem sido realizados, não estão listados demasi passos como: definição do problema, definições junto as partes interessadas, levantamento de requisitos, testes entre outros.

## Extração das Informações

As informações foram retiradas de diferentes fontes de dados para compor o painel final. Todos os dados utilizados estão armazenados dentro das fronteiras do sistema SAP e foram extraídos através de arquivos na extensão "txt" ou "xls". Cada extração, por convenção, será nomeada de relatório, onde destacamos:
- Relatório de Encargos:

| Campo | Tipo |
|-------|------|
| Matrícula | Inteiro |
| Nome | String |
| Rubrica salarial | String |
| Descrição da rubrica | String |
| Lotação | String |
| Montante | Decimal |

- Relatório de Horas Extras Estruturais para Pagamento:

| Campo | Tipo |
|-------|------|
| Lotação | String |
| Matrícula | Inteiro |
| Nome | String |
| Rubrica salarial | String |
| Descrição da rubrica | String |
| Quantidade | Decimal |
| Montante | Decimal |

- Relatório de Horas Extras Conjunturais para Pagamento:

| Campo | Tipo |
|-------|------|
| Lotação | String |
| Matrícula | Inteiro |
| Nome | String |
| Rubrica salarial | String |
| Descrição da rubrica | String |
| Quantidade | Decimal |
| Montante | Decimal |

- Relatório de tipos de Horas Extras para Comparação:

| Campo | Tipo |
|-------|------|
| Matrícula | Inteiro |
| Nome | String |
| Competência | String |
| Tipo de hora extra | String |
| Descrição da hora extra | String |
| Quantidade | Decimal |
| Lotação | String |

- Relatório de Treinamentos Realizados:

| Campo | Tipo |
|-------|------|
| Centro de custo | Inteiro |
| Resumo lotação | String |
| Descrição lotação | String |
| Matrícula | Inteiro |
| Nome | String |
| Código treinamento | Inteiro |
| Tipo de treinamento | String |
| Código evento | Inteiro |
| Descrição evento | String |
| Data evento | Data |
| Quantidade de horas | Decimal |
| Indicador se obrigatório | String |

- Relatório de Exames Periódicos Realizados:

| Campo | Tipo |
|-------|------|
| Nome | String |
| Data nascimento | Data |
| Status da programação | String |
| Data consulta | Data |
| Hora consulta | Hora |
| Tipo exame | String |
| Denominação exame | String |
| Número do serviço | Inteiro |
| Médico | String |
| Serviço | String |
| Status do serviço | String |

- Relatório de Afastamentos:

| Campo | Tipo |
|-------|------|
| Competência | String |
| Matricula | Inteiro |
| Nome | String |
| Lotação | Data |
| Número efetivo | Inteiro |
| Quadro lotação | Inteiro |
| Horas de trabalho | Decimal |
| Horas acumuladas | Decimal |

- Relatório de Absenteísmo:

| Campo | Tipo |
|-------|------|
| Centro de custo | Inteiro |
| Lotação | String |
| Descrição da lotação | String |
| Gerência | String |
| Diretoria | String |
| Matrícula | Inteiro |
| Nome | String |
| Regra do plano de horário | String |
| Horas efetivas | Decimal |
| Horas trabalhadas | Decimal |
| Atrasos | Decimal |
| Faltas | Decimal |
| DSRs | Decimal |
| Atestados | Decimal |
| Afastamentos | Decimal |
| Suspensões | Decimal |
| Ausências abonadas | Decimal |
| % Absenteísmo | Decimal |
| % Absenteísmo sem afastamentos | Decimal |

## Transformação das Informações

Após a extração dos relatórios acima especificados, os dados foram agrupados em um único recurso. Uma planilha no formato "xls".

Nesta planilha, foi feito o agrupamento dos dados unificando os resultados pela seguinte chave composta: "Diretoria", "Gerência" e "Lotação". Ou seja, apesar dos dados estarem detalhados por matricula, data e tipo de registro, eles foram agrupados pela visão de estrutura organizacional da empresa no tempo.

Mais precisamente, cada registro (ou tupla) tem, no mínimo, as informações de "Diretoria", "Gerência", "Lotação" e "Competência".

Nesta mesma planilha, os foram criados componentes para exportação dos dados no formato "csv".

## Análise da massa de dados

Após o tratamento das informações, especificado acima, os dados exportados foram analisados considerando medidas de tendência central e medidas de dispensão utilizando a linguagem Python.

Abaixo seguem alguns exemplos das análise realizada.

```python
import pandas as pd
import numpy as np

df = pd.read_csv('FatoHoras_Extras_201901_202009.csv')

# Média - valor de concentração dos dados
print(df['Qtde'].mean())
print(df['Montante'].mean())

# Mediana - separação das metades superior e inferior
print(df['Qtde'].quantile())

# Quantil - valor que está um certo percentual dos dados
print(df['Montante'].quantile(q=0.25))

# Moda - valor que mais se repete
print(df['Qtde'].mode())

# Amplitude - diferença entre o maior e o menor valor
print(df['Montante'].max() - df['Montante'].min())

# Variância - expressão da dispersão dos dados em relação ao valor esperado
print(df['Qtde'].var())

# Desvio Padrão - expressão da dispersão dos dados em relação a média
print(df['Qtde'].std())

# Desvio absoluto
print(df['Qtde'].mad())

# Covariância e Correlação - apenas para analisar a relação entre as variáveis 'Qtde' e 'Montante'
print(df.cov())
print(df.corr())
```

## Carga das Informações

Após a extração, transformação e análise dos dados, foi iniciada a carga dos dados em formato "csv". A carga levou em consideração os diferentes cenários e criou as seguintes tabelas:

- Fato_Absenteismo:

| Campo | Tipo |
|-------|------|
| Competência | String |
| Diretoria | String |
| Gerência | String |
| Lotação | String |
| Horas efetivas | Decimal |
| Horas trabalhadas | Decimal |
| Atrasos | Decimal |
| Faltas | Decimal |
| Dsr | Decimal |
| Atestado | Decimal |
| Afastamento | Decimal |
| Suspensão | Decimal |
| Ausências Abonadas | Decimal |

- Fato_Ausentes_Pcmso:

| Campo | Tipo |
|-------|------|
| Competência | String |
| Diretoria | String |
| Gerência | String |
| Lotação | String |
| Matrícula | String |
| Nome | String |
| Observação | String |

- Fato_Ausentes_Treinamentos:

| Campo | Tipo |
|-------|------|
| Competência | String |
| Diretoria | String |
| Gerência | String |
| Lotação | String |
| Matrícula | String |
| Data | Date |
| Nome | String |
| Treinamento | String |

- Fato_Numero_Pcmso:

| Campo | Tipo |
|-------|------|
| Competência | String |
| Diretoria | String |
| Gerência | String |
| Lotação | String |
| Não cumpriu | Inteiro |

- Fato_Numero_Treinamentos:

| Campo | Tipo |
|-------|------|
| Competência | String |
| Diretoria | String |
| Gerência | String |
| Lotação | String |
| Número de treinamentos | Inteiro |
| Ausentes em treinamentos | Inteiro |

- Fato_Remuneracoes:

| Campo | Tipo |
|-------|------|
| Competência | String |
| Diretoria | String |
| Gerência | String |
| Lotação | String |
| Quantidade | Decimal |
| Remuneração | Decimal |
| Encargos | Decimal |

- Fato_Horas_Extras:

| Campo | Tipo |
|-------|------|
| Competência | String |
| Diretoria | String |
| Gerência | String |
| Lotação | String |
| Tipo de hora extra | String |
| Código da hora extra | String |
| Quantidade | Decimal |
| Montante | Decimal |

## Criação do Dashboard

Após a carga de dados, foram criados campos utilizando da linguagem da própria ferramenta como, por exemplo, percentual de absenteísmo, além de filtros específicos para competência passadas.

Foram utilizados diferentes gráficos e tabelas com o intuito de facilitar a visualição e permitir a tomada de descisões.

Finalizada a construção da ferramenta, o layout visual apresentado foi dividido em dois paineis, abaixo mostrados e disponíveis no seguinte link: https://sites.google.com/view/relatoriohorasextrasteste/home.

### Dashboard de Horas Extras

![001_202019101405](https://user-images.githubusercontent.com/36538143/96493654-9cdbce80-121b-11eb-93ce-ee4d9c27ba35.JPG)

### Painel de Gestão de Pessoas

![001_202019101406](https://user-images.githubusercontent.com/36538143/96493894-f3e1a380-121b-11eb-95c1-b0acb8b54034.JPG)

