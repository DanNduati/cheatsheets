# Postgres Cheatsheet
### Connection
### Login as postgres user
#### Local
```bash
$ su - postgres
```
#### Remote
```bash
$ ssh -l postgres <ip addr>
```
#### Connect to db
```
\c <database>
```
```
psql -h <ip addr> -p <port> -d <database> -U <user> -W
```
example
```
psql -h 139.162.187.190 -p 5432 -d rentlord -U postgres -W
```
### PSQL
#### Show table
Show table definition including indexes,constraints and triggers
```
\d TABLE_NAME
```
### Show details
More detailed table definition including description and physical disk size (psql)
```
\d+ TABLE_NAME
```
### List tables from current schema
```
\dt
```

### List tables from all schemas
```
\dt *.*
```
### Copy table data to CSV file
```
\copy (SELECT * FROM <table_name>) TO 'file_path_and_name.csv' WITH CSV
```