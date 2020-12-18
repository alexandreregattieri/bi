# Dashboard de Horas Extras e Painel de Gestão de Pessoas

## Objetivo:
Criação, através da ferrementa Data Google Studio, um Dashboard de Horas Extras e um Painel de Gestão de Pessoas para a empresa CESAN.

Tanto o dashboard quanto o painel buscam prover informações, organizadas de forma intuitiva, para subsidiar a tomada de decisões.

Todos os dados contidos no link abaixo são ilusórios e foram colocados apenas para formar uma base de simulação.

## Extração das Informações:

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

- Relatório de Exames Periódicos Realizados:

- Relatório de Afastamentos:

- Relatório de Absenteísmo:

| Campo | Tipo |
|-------|------|
| Centro de Custo | Inteiro |
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

## Transformação das Informações:

## Carga das Informações:

## Criação do Dashboard:

## Visualização do Modelo Final:

Link: https://sites.google.com/view/relatoriohorasextrasteste/home

### Dashboard de Horas Extras

![001_202019101405](https://user-images.githubusercontent.com/36538143/96493654-9cdbce80-121b-11eb-93ce-ee4d9c27ba35.JPG)

### Painel de Gestão de Pessoas

![001_202019101406](https://user-images.githubusercontent.com/36538143/96493894-f3e1a380-121b-11eb-95c1-b0acb8b54034.JPG)


