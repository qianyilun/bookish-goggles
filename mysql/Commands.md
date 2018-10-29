## MySQL Common Commands

- Access monitor: `mysql -u [username] -p;` (will prompt for password: secret)
- Show all databases: `show databases;`
- Select database: `use [database];`
- Show all tables: `show tables;`
- Show table structure: `describe [table];`
- Create new table with columns: `CREATE TABLE [table] ([column] VARCHAR(120), [another-column] DATETIME);`
- Adding a column: `ALTER TABLE [table] ADD COLUMN [column] VARCHAR(120);`
- Adding a column with an unique, auto-incrementing ID: `ALTER TABLE [table] ADD COLUMN [column] int NOT NULL AUTO_INCREMENT PRIMARY KEY;`
- Inserting a record: `INSERT INTO [table] ([column], [column]) VALUES ('[value]', [value]');`
- MySQL function for datetime input: `NOW()`
- Selecting records: `SELECT * FROM [table];`
- Counting records: `SELECT COUNT([column]) FROM [table];`
- Counting and selecting grouped records: `SELECT *, (SELECT COUNT([column]) FROM [table]) AS count FROM [table] GROUP BY [column];`
- Updating records: `UPDATE [table] SET [column] = '[updated-value]' WHERE [column] = [value];`
- Deleting records: `DELETE FROM [table] WHERE [column] = [value];`
- Delete all records in a table: `truncate table [table];`
- Deleting tables: `DROP TABLE [table];`
- Logout: `exit;`