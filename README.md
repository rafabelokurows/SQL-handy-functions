# Handy SQL snippets

Here you'll find some handy code snippets, tips and tricks for SQL that I found while working on different SQL databases, mainly Microsoft SQL Server.
If you like it, feel free to share it, fork it, etc., just make sure to give credit. Thanks!

## Finding columns by column name on all tables (and views) of a database

This will go through the schema of your database and look for every column that fits your filters, in this case, a substring through a LIKE comparison.
```
SELECT      COLUMN_NAME AS 'ColumnName'
            ,TABLE_NAME AS  'TableName'
FROM        INFORMATION_SCHEMA.COLUMNS
WHERE       lower(COLUMN_NAME) LIKE '%string%'
ORDER BY    TableName
            ,ColumnName;
```
Parameters/filters:  
- %string% is the text you're looking for  

Result: It will output the all columns with column name and table name

## Retrieving lost queries

This query goes to the execution plans of the database and retrieves the last queries executed allowing to retrieve queries you might have lost in the last minutes/hours.

```
SELECT top 10 t.[text], s.last_execution_time
FROM sys.dm_exec_cached_plans AS p
INNER JOIN sys.dm_exec_query_stats AS s
   ON p.plan_handle = s.plan_handle
CROSS APPLY sys.dm_exec_sql_text(p.plan_handle) AS t
WHERE t.[text] LIKE N'%-----yourtexthere-----%'
ORDER BY s.last_execution_time DESC
```
Tested on: SQL Server
