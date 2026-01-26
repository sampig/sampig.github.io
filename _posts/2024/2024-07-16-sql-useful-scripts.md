---
layout: post
title: "SQL: Basic Useful Scripts"
date: 2024-07-16 22:11:39 +0200
category: tutorial
tagline: ""
tags: [SQL, Database, MySQL, Oracle, PostgreSQL]
abstract : "A collection of basic useful SQL scripts for MySQL, Oracle, and PostgreSQL databases."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [MySQL](#mysql)
* [Oracle](#oracle)
* [PostgreSQL](#postgresql)
* [References](#references)

# Introduction

This post compiles useful SQL scripts and commands for common database administration tasks across MySQL, Oracle, and PostgreSQL. These scripts help with version checking, monitoring, user management, performance analysis, and maintenance operations.


# MySQL

## 1. Display version info of DB

```sql
mysql> SELECT @@version;
+-----------+
| @@version |
+-----------+
| 5.7.28    |
+-----------+
```

## 2. Display DB instance info

```sql
mysql> SHOW VARIABLES LIKE "%version%";
+-------------------------+------------------------------+
| Variable_name           | Value                        |
+-------------------------+------------------------------+
| innodb_version          | 5.7.28                       |
| protocol_version        | 10                           |
| slave_type_conversions  |                              |
| tls_version             | TLSv1,TLSv1.1,TLSv1.2        |
| version                 | 5.7.28                       |
| version_comment         | MySQL Community Server (GPL) |
| version_compile_machine | x86_64                       |
| version_compile_os      | macos10.14                   |
+-------------------------+------------------------------+
```

## 3. Display the status of DB schema

```sql
mysql> SELECT table_schema, SUM(data_length + index_length)/1024/1024 AS "Size (MB)" FROM information_schema.tables GROUP BY table_schema; 
+--------------------+------------+
| table_schema       | Size (MB)  |
+--------------------+------------+
| iems               | 2.70312500 |
| iems_quartz        | 0.64062500 |
| information_schema | 0.15625000 |
| mysql              | 2.58428860 |
| pdcs               | 0.06250000 |
| performance_schema | 0.00000000 |
| sys                | 0.01562500 |
+--------------------+------------+
```

## 4. Display DB connection info

```sql
mysql> SHOW PROCESSLIST;
+----+------+-----------------+------+---------+------+----------+------------------+
| Id | User | Host            | db   | Command | Time | State    | Info             |
+----+------+-----------------+------+---------+------+----------+------------------+
|  3 | root | localhost       | NULL | Query   |    0 | starting | SHOW PROCESSLIST |
|  5 | root | localhost:50373 | NULL | Sleep   |  527 |          | NULL             |
|  6 | root | localhost:50374 | NULL | Sleep   |  527 |          | NULL             |
|  7 | root | localhost:50382 | NULL | Sleep   | 1084 |          | NULL             |
|  8 | root | localhost:50383 | NULL | Sleep   |    2 |          | NULL             |
+----+------+-----------------+------+---------+------+----------+------------------+
```

## 5. Display status of cache hits

```sql
mysql> SHOW STATUS LIKE "Qcache_hits";
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| Qcache_hits   | 0     |
+---------------+-------+
```

## 6. Display use of the tables

```sql
mysql> SHOW OPEN TABLES WHERE In_use > 0;
+--------------------+------------------------------------------------------+--------+-------------+
| Database           | Table                                                | In_use | Name_locked |
+--------------------+------------------------------------------------------+--------+-------------+
| *****              | *****                                                |      ? |           ? |
...
```

## 7. Display slow log

```sql
mysql> SELECT * FROM mysql.slow_log;
```

## 8. Display index info

```sql
mysql> SHOW INDEX FROM mysql.user;
+-------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| Table | Non_unique | Key_name | Seq_in_index | Column_name | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment |
+-------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
| user  |          0 | PRIMARY  |            1 | Host        | A         |        NULL |     NULL | NULL   |      | BTREE      |         |               |
| user  |          0 | PRIMARY  |            2 | User        | A         |           4 |     NULL | NULL   |      | BTREE      |         |               |
+-------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+
```

## 9. Display status of procedure or function

```sql
mysql> SHOW PROCEDURE STATUS;
mysql> SHOW FUNCTION STATUS;
```

## 10. DB backup and restore

```bash
mysqldump -u username -p database_name > backup.sql
mysql -u username -p database_name < backup.sql
```

## 11. Search DB user

```sql
mysql> SELECT USER, Host FROM mysql.user;
+---------------+-----------+
| USER          | Host      |
+---------------+-----------+
| mysql.session | localhost |
| mysql.sys     | localhost |
| root          | localhost |
+---------------+-----------+
```

## 12. Create a new user and give permissions

```sql
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';  

GRANT ALL PRIVILEGES ON database_name.* TO 'newuser'@'localhost';  

FLUSH PRIVILEGES;
```

## 13. Change password for a user

```sql
ALTER USER 'username'@'host' IDENTIFIED BY 'new_password';  
FLUSH PRIVILEGES;
```

## 14. Optimize table

```sql
OPTIMIZE TABLE table_name;
```

## 15. Display DB status

```sql
mysql> SHOW STATUS;
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| *****         | ?     |
...
```

# Oracle

## 1. Search locked processes and unlock

```sql
SELECT L.SESSION_ID, S.SERIAL#, L.ORACLE_USERNAME, L.OS_USER_NAME, S.MACHINE, S.TERMINAL, O.OBJECT_NAME
  FROM V$LOCKED_OBJECT L
 INNER JOIN ALL_OBJECTS O ON O.OBJECT_ID = L.OBJECT_ID
 INNER JOIN V$SESSION S ON S.SID = L.SESSION_ID;
```

```sql
ALTER SYSTEM KILL SESSION 'SESSION_ID, SERIAL#';
```

## 2. Monitor queue

```sql
SELECT b.SID, b.serial#, b.username, machine, event, wait_time, ...
  FROM v$session_wait a, v$session b
 WHERE a.event = 'enqueue' ...;
```

## 3. Display tablespace I/O

```sql
SELECT df.tablespace_name, f.phyrds, f.phywrts ...
  FROM v$filestat f, dba_data_files df
 WHERE f.file# = df.file_id;
```

## 4. Display DB objects (an example for displaying table objects)

```sql
SELECT object_name
  FROM user_objects
 WHERE object_type = 'TABLE';
```

## 5. Display user privileges

```sql
SELECT * FROM session_privs;
```

## 6. Change user password

```sql
ALTER USER username IDENTIFIED BY "newpassword";
```

## 7. Create and delete a user

```sql
CREATE USER username IDENTIFIED BY "password";

DROP USER username CASCADE;
```

## 8. Give permissions to user

```sql
GRANT CREATE SESSION, CREATE TABLE TO username;
```

## 9. Display datafile I/O

```sql
SELECT substr(a.file#,1,2) "#", substr(a.name,1,30) "Name", a.status, a.bytes, b.phyrds, b.phywrts
  FROM v$datafile a, v$filestat b
 WHERE a.file# = b.file#;
```

# PostgreSQL

## 1. Display version info

```sql
SELECT version();
```

## 2. Display database size

```sql
SELECT pg_database.datname, 
       pg_size_pretty(pg_database_size(pg_database.datname)) AS size
  FROM pg_database
 ORDER BY pg_database_size(pg_database.datname) DESC;
```

## 3. Display table sizes

```sql
SELECT schemaname, tablename,
       pg_size_pretty(pg_total_relation_size(schemaname||'.'||tablename)) AS size
  FROM pg_tables
 WHERE schemaname NOT IN ('pg_catalog', 'information_schema')
 ORDER BY pg_total_relation_size(schemaname||'.'||tablename) DESC;
```

## 4. Display active connections

```sql
SELECT pid, usename, application_name, client_addr, state, query_start, query
  FROM pg_stat_activity
 WHERE state = 'active';
```

## 5. Display database connections info

```sql
SELECT datname, usename, application_name, client_addr, state, count(*)
  FROM pg_stat_activity
 GROUP BY datname, usename, application_name, client_addr, state;
```

## 6. Display locks

```sql
SELECT blocked_locks.pid AS blocked_pid,
       blocking_locks.pid AS blocking_pid,
       blocked_activity.usename AS blocked_user,
       blocking_activity.usename AS blocking_user,
       blocked_activity.query AS blocked_statement,
       blocking_activity.query AS blocking_statement
  FROM pg_catalog.pg_locks blocked_locks
  JOIN pg_catalog.pg_stat_activity blocked_activity ON blocked_activity.pid = blocked_locks.pid
  JOIN pg_catalog.pg_locks blocking_locks ON blocking_locks.locktype = blocked_locks.locktype
  JOIN pg_catalog.pg_stat_activity blocking_activity ON blocking_activity.pid = blocking_locks.pid
 WHERE NOT blocked_locks.granted;
```

## 7. Kill a query/connection

```sql
SELECT pg_terminate_backend(pid)
  FROM pg_stat_activity
 WHERE pid = <process_id>;
```

## 8. Display index usage

```sql
SELECT schemaname, tablename, indexname, idx_scan, idx_tup_read, idx_tup_fetch
  FROM pg_stat_user_indexes
 ORDER BY idx_scan ASC;
```

## 9. Display slow queries

```sql
SELECT pid, now() - pg_stat_activity.query_start AS duration, query, state
  FROM pg_stat_activity
 WHERE (now() - pg_stat_activity.query_start) > interval '5 minutes'
   AND state != 'idle';
```

## 10. Display table statistics

```sql
SELECT schemaname, tablename, 
       n_tup_ins AS inserts,
       n_tup_upd AS updates,
       n_tup_del AS deletes,
       n_live_tup AS live_tuples,
       n_dead_tup AS dead_tuples,
       last_vacuum,
       last_autovacuum,
       last_analyze,
       last_autoanalyze
  FROM pg_stat_user_tables
 ORDER BY schemaname, tablename;
```

## 11. Display user information

```sql
SELECT usename, usesuper, usecreatedb, usecreaterole
  FROM pg_user;
```

## 12. Create a new user and give permissions

```sql
CREATE USER newuser WITH PASSWORD 'password';

GRANT ALL PRIVILEGES ON DATABASE database_name TO newuser;

GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO newuser;
```

## 13. Change user password

```sql
ALTER USER username WITH PASSWORD 'new_password';
```

## 14. Display database objects

```sql
SELECT table_schema, table_name, table_type
  FROM information_schema.tables
 WHERE table_schema NOT IN ('pg_catalog', 'information_schema')
 ORDER BY table_schema, table_name;
```

## 15. Vacuum and analyze

```sql
VACUUM ANALYZE table_name;
```

## 16. DB backup and restore

```bash
pg_dump -U username -d database_name > backup.sql
psql -U username -d database_name < backup.sql
```

# References

1. [MySQL Documentation](https://dev.mysql.com/doc/){:target="_blank"}
2. [Oracle Database Documentation](https://docs.oracle.com/en/database/){:target="_blank"}
3. [PostgreSQL Documentation](https://www.postgresql.org/docs/){:target="_blank"}
