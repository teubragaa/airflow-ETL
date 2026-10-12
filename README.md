# Pipeline ETL com Python, Apache Airflow e Docker

## Sobre o projeto

Este projeto consiste no desenvolvimento de um pipeline ETL (*Extract, Transform, Load*) para processar dados de usuários a partir de um arquivo CSV e armazená-los em um banco de dados SQLite.

O fluxo é orquestrado pelo Apache Airflow, que permite definir a sequência de execução das tarefas, suas dependências e a programação das execuções. O ambiente é executado utilizando Docker Compose.

## Tecnologias utilizadas

- **Python:** implementação da lógica do pipeline.
- **Pandas:** leitura e manipulação dos dados do arquivo CSV.
- **Apache Airflow:** orquestração e agendamento das tarefas.
- **SQLite:** armazenamento dos dados processados.
- **Docker e Docker Compose:** configuração e execução do ambiente.

## Arquitetura do pipeline

O pipeline é dividido nas seguintes etapas:

1. **Start:** inicia o fluxo de execução.
2. **Setup Database:** cria a tabela `users`, caso ela não exista, e limpa os registros anteriores.
3. **Extract:** lê os dados do arquivo `data/users.csv` utilizando Pandas.
4. **Transform:** recupera os dados da etapa de extração por meio do XCom do Airflow. Nesta versão, os dados são mantidos sem alterações.
5. **Load:** insere os registros na tabela `users` do banco SQLite.
6. **End:** finaliza o fluxo de execução.

## Fluxo de execução

```text
Start
  ↓
Setup Database
  ↓
Extract
  ↓
Transform
  ↓
Load
  ↓
End
```

## Estrutura do projeto

```text
airflow-ETL/
├── dags/
│   └── data_pipeline_etl.py
├── data/
│   └── users.csv
└── docker-compose.yaml
```

## Como funciona

O Apache Airflow executa as tarefas na ordem definida pela DAG `users_etl_pipeline`. Os dados extraídos são transmitidos entre as tarefas por meio do XCom e, ao final do processo, são inseridos no banco SQLite.

A DAG está configurada para execução diária, com `catchup=False`, evitando a execução automática de períodos anteriores à data atual.

## Objetivos de aprendizagem

- Compreender o funcionamento de um processo ETL.
- Manipular dados com Python e Pandas.
- Criar e executar DAGs no Apache Airflow.
- Definir dependências entre tarefas.
- Utilizar XCom para compartilhar dados entre tarefas.
- Executar serviços utilizando Docker Compose.
- Armazenar dados em um banco de dados relacional.

