# Comandos SQL Úteis para Azure SQL Database

Este documento contém comandos SQL básicos que podem ser úteis ao trabalhar com o Azure SQL Database. Esses comandos podem ser executados no Editor de Consultas do Portal Azure ou usando ferramentas como SQL Server Management Studio (SSMS) e Azure Data Studio.

## Consultas Básicas

### Visualizar todas as tabelas no banco de dados

```sql
SELECT table_name
FROM information_schema.tables
WHERE table_type = 'BASE TABLE'
ORDER BY table_name;
```

### Visualizar informações sobre colunas de uma tabela específica

```sql
SELECT column_name, data_type, character_maximum_length
FROM information_schema.columns
WHERE table_name = 'NomeDaSuaTabela';
```

### Consulta básica em uma tabela

```sql
-- Se estiver usando o banco de amostra AdventureWorksLT
SELECT TOP 10 * FROM SalesLT.Customer;
```

## Gerenciamento de Dados

### Criar uma tabela

```sql
CREATE TABLE Funcionarios (
    ID INT PRIMARY KEY IDENTITY(1,1),
    Nome NVARCHAR(100) NOT NULL,
    Cargo NVARCHAR(50),
    Departamento NVARCHAR(50),
    DataAdmissao DATE,
    Salario DECIMAL(10, 2)
);
```

### Inserir dados

```sql
INSERT INTO Funcionarios (Nome, Cargo, Departamento, DataAdmissao, Salario)
VALUES ('João Silva', 'Analista', 'TI', '2023-01-15', 5000.00);
```

### Atualizar dados

```sql
UPDATE Funcionarios
SET Salario = 5500.00
WHERE Nome = 'João Silva';
```

### Excluir dados

```sql
DELETE FROM Funcionarios
WHERE ID = 1;
```

## Monitoramento de Performance

### Verificar as consultas mais caras (em termos de recursos)

```sql
SELECT TOP 10
    q.query_id,
    q.query_text_id,
    qt.query_sql_text,
    rs.avg_cpu_time,
    rs.avg_logical_io_reads,
    rs.avg_duration,
    rs.count_executions
FROM sys.query_store_query q
JOIN sys.query_store_query_text qt ON q.query_text_id = qt.query_text_id
JOIN sys.query_store_plan p ON q.query_id = p.query_id
JOIN sys.query_store_runtime_stats rs ON p.plan_id = rs.plan_id
JOIN sys.query_store_runtime_stats_interval rsi ON rs.runtime_stats_interval_id = rsi.runtime_stats_interval_id
ORDER BY rs.avg_cpu_time DESC;
```

### Verificar estatísticas de tabela

```sql
-- Verificar estatísticas de uso para tabelas
SELECT
    OBJECT_NAME(s.[object_id]) AS TableName,
    s.name AS StatName,
    s.auto_created,
    s.user_created,
    s.no_recompute,
    s.has_filter,
    sp.last_updated,
    sp.rows,
    sp.rows_sampled,
    sp.modification_counter
FROM sys.stats s
CROSS APPLY sys.dm_db_stats_properties(s.[object_id], s.stats_id) AS sp
WHERE OBJECT_NAME(s.[object_id]) = 'NomeDaSuaTabela';
```

## Segurança

### Listar todos os usuários no banco de dados

```sql
SELECT name, type_desc, create_date
FROM sys.database_principals
WHERE type_desc IN ('SQL_USER', 'WINDOWS_USER', 'WINDOWS_GROUP')
ORDER BY name;
```

### Criar um novo usuário

```sql
CREATE USER NovoUsuario WITH PASSWORD = 'SenhaForte123!';
```

### Conceder permissões

```sql
-- Conceder permissão de leitura a uma tabela
GRANT SELECT ON Funcionarios TO NovoUsuario;

-- Conceder permissão de leitura a todo o esquema
GRANT SELECT ON SCHEMA::SalesLT TO NovoUsuario;
```

### Revogar permissões

```sql
REVOKE SELECT ON Funcionarios FROM NovoUsuario;
```

## Backup e Restauração (Comandos Administrativos)

Observação: No Azure SQL Database, backups automáticos são gerenciados pela plataforma. No entanto, você pode fazer exportações e cópias:

### Criar um banco de dados como cópia

```sql
-- Este comando deve ser executado no contexto master
CREATE DATABASE CopiaDoMeuBD AS COPY OF MeuBD;
```

## Dicas de Performance

### Criação de índice

```sql
-- Criar um índice não clusterizado
CREATE INDEX IX_Funcionarios_Departamento ON Funcionarios(Departamento);

-- Criar um índice clusterizado
CREATE CLUSTERED INDEX IX_Funcionarios_ID ON Funcionarios(ID);
```

### Reconstruir índice

```sql
ALTER INDEX IX_Funcionarios_Departamento ON Funcionarios REBUILD;
```

### Verificar fragmentação de índice

```sql
SELECT
    OBJECT_NAME(ind.OBJECT_ID) AS TableName,
    ind.name AS IndexName,
    indexstats.avg_fragmentation_in_percent,
    indexstats.page_count
FROM sys.dm_db_index_physical_stats(DB_ID(), NULL, NULL, NULL, NULL) indexstats
INNER JOIN sys.indexes ind ON ind.object_id = indexstats.object_id
    AND ind.index_id = indexstats.index_id
WHERE indexstats.avg_fragmentation_in_percent > 10
ORDER BY indexstats.avg_fragmentation_in_percent DESC;
```

## Observações Importantes

1. Os comandos de gerenciamento de servidor (como criação de logins a nível de servidor) devem ser executados no contexto do banco de dados `master`.

2. O Azure SQL Database tem algumas limitações em comparação com o SQL Server on-premises, especialmente em comandos administrativos.

3. Sempre siga as melhores práticas de segurança, como usar senhas fortes e limitar permissões ao mínimo necessário.

4. Para monitoramento mais avançado, utilize as ferramentas do portal Azure, como Azure SQL Analytics e Query Performance Insight.
