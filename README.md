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
