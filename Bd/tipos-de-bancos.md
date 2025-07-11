# Tipos de Bancos de Dados no Azure

O Microsoft Azure oferece uma variedade de serviços de banco de dados para atender diferentes necessidades e casos de uso. Abaixo está uma visão geral dos principais tipos de bancos de dados disponíveis:

## Bancos de Dados Relacionais

### Azure SQL Database

- Banco de dados relacional totalmente gerenciado baseado no SQL Server
- Escalabilidade automática, alta disponibilidade e proteção de dados
- Ideal para aplicações empresariais que necessitam de esquema rígido e transações ACID
- Modelos de compra: DTU e vCore

### Azure Database for MySQL

- Versão gerenciada do MySQL para aplicações que exigem esse sistema
- Compatível com MySQL 5.6, 5.7 e 8.0
- Ideal para aplicações web, blogs, e-commerce (CMS como WordPress, Drupal)
- Alta disponibilidade e backup automático

### Azure Database for PostgreSQL

- Serviço gerenciado do PostgreSQL com opções flexíveis
- Disponível em dois modos de implantação:
  - Servidor único
  - Hiperescala (Citus) para bancos de dados de vários terabytes
- Ideal para aplicações geoespaciais, análise de dados e cargas de trabalho que necessitam de tipos de dados avançados

### Azure Database for MariaDB

- Serviço gerenciado do MariaDB
- Compatível com MariaDB 10.2 e 10.3
- Alta disponibilidade e escalabilidade
- Segurança avançada e monitoramento integrado

## Bancos de Dados NoSQL

### Azure Cosmos DB

- Banco de dados NoSQL globalmente distribuído, multi-modelo
- Suporta vários modelos de dados: documentos, gráficos, chave-valor, coluna larga
- APIs múltiplas: SQL, MongoDB, Cassandra, Gremlin, Tabela do Azure
- Escalabilidade global com latência garantida de milissegundos
- Ideal para aplicações globais, IoT, jogos e aplicações web/móveis

### Azure Cache for Redis

- Serviço gerenciado do Redis
- Cache na memória para alta velocidade de acesso a dados
- Ideal para armazenamento temporário, filas de mensagens e cache de sessão
- Suporta replicação para alta disponibilidade

### Azure Table Storage

- Serviço de armazenamento de chave-valor NoSQL
- Parte do Azure Storage
- Esquema flexível para dados não estruturados
- Ideal para dados que não exigem joins complexos, chaves estrangeiras ou procedimentos armazenados

## Análise e Big Data

### Azure Synapse Analytics (antigo SQL Data Warehouse)

- Serviço de análise de dados em escala de petabyte
- Combina data warehouse empresarial e análise de big data
- Integração com Power BI, Azure Data Factory e Azure Machine Learning
- Ideal para business intelligence e cargas de trabalho analíticas

### Azure HDInsight

- Serviço de análise de código aberto totalmente gerenciado
- Suporta frameworks populares como Hadoop, Spark, Hive, LLAP, Kafka, Storm e R
- Ideal para processamento de grandes volumes de dados não estruturados

## Migração e Administração

### Azure Database Migration Service

- Serviço para migrar bancos de dados para o Azure
- Suporta migrações online (mínimo tempo de inatividade) e offline
- Compatível com SQL Server, MySQL, PostgreSQL, MongoDB e Oracle

### Azure SQL Managed Instance

- Instância totalmente gerenciada do SQL Server com quase 100% de compatibilidade com o SQL Server on-premises
- Ideal para migrações lift-and-shift com alterações mínimas
- Suporta recursos avançados como SQL Agent, Database Mail, Service Broker

## Diagrama de Tipos de Bancos de Dados no Azure

```
Azure Database Services
│
├── Bancos Relacionais
│   ├── Azure SQL Database
│   ├── Azure SQL Managed Instance
│   ├── Azure Database for MySQL
│   ├── Azure Database for PostgreSQL
│   └── Azure Database for MariaDB
│
├── Bancos NoSQL
│   ├── Azure Cosmos DB
│   │   ├── API SQL
│   │   ├── API MongoDB
│   │   ├── API Cassandra
│   │   ├── API Gremlin (grafo)
│   │   └── API Tabela
│   │
│   ├── Azure Cache for Redis
│   └── Azure Table Storage
│
├── Análise e Big Data
│   ├── Azure Synapse Analytics
│   └── Azure HDInsight
│
└── Migração e Administração
    └── Azure Database Migration Service
```

## Considerações para Escolha

Ao escolher um serviço de banco de dados no Azure, considere:

1. **Modelo de dados**: Relacional vs. NoSQL
2. **Escala esperada**: Volume de dados e número de transações
3. **Distribuição geográfica**: Necessidade de presença global
4. **Compatibilidade**: Necessidade de compatibilidade com sistemas existentes
5. **Requisitos de performance**: Latência, throughput
6. **Custo**: Diferentes serviços têm diferentes modelos de preço

O Azure oferece opções para praticamente qualquer caso de uso de banco de dados, permitindo que você escolha a melhor ferramenta para cada trabalho específico.
