# TestBDD
**[!NOTE] Main psql postgres commands**

# ** This is level 1 **
#Open a Postgres session
$ sudo -i -u postgres
# Or : 
$ sudo -u postgres psql

# Create database and open it :
postgres=# CREATE DATABASE <database_name> WITH OWNER <username>;
$ psql -U bddOwnerName -d bddName

# Or, use pgcli (here, is an example with my admin name and my database name)
$ pgcli -h localhost -p 5432 -U manuangot pire2pire


# ** This is level 2 **
# You can check access privileges and administrators, in your database.
# In psql, use the command :\z
# Example with my datas
> pgcli -h localhost -p 5432 -U manuangot pire2pire
Password for manuangot:
Server: PostgreSQL 15.3 (Ubuntu 15.3-1.pgdg22.04+1)
Version: 3.5.0
Home: http://pgcli.com
pire2pire> \z
# Should return
+--------+------------------------+----------+-------------------+-------------------+----------+
| Schema | Name                   | Type     | Access privileges | Column privileges | Policies |
|--------+------------------------+----------+-------------------+-------------------+----------|
| public | user_table             | table    | <null>            |                   |          |
| public | user_table_user_id_seq | sequence | <null>            |                   |          |
+--------+------------------------+----------+-------------------+-------------------+----------+


# ** This is level 3" **
# Save database to export:
# Exit database, return to linux console and open postgres
$ sudo -i -u postgres

# Command to save a backup of my database. 
# Here, pire2pire is the name of the database that I want to save.
# p2pbackup.sql is the name of the backup file I assigned to it.
postgres@DESKTOP-IE72UJ2:~$  pg_dump -d pire2pire -f p2pbackup.sql

# You can use the "ls" command to verify that the backup has been created.
postgres@DESKTOP-IE72UJ2:~$ ls
15  p2pbackup.sql


# ** This is level 4" **
# Delete Database : 
# Beforehand, you must exit your database, using the "\q" command

pire2pire> \q
Goodbye!

# Return in postgres
> sudo -u postgres psql
[sudo] password for manu:
could not change directory to "/home/manu": Permission denied
psql (15.3 (Ubuntu 15.3-1.pgdg22.04+1))
Type "help" for help.

# Here is the command to delete my DB 
postgres=# DROP DATABASE pire2pire;
# The console sends me a confirmation message : 
DROP DATABASE

# You can check that the database has been deleted, with the command "\l"
postgres=# \l
                                             List of databases
   Name    |  Owner   | Encoding | Collate |  Ctype  | ICU Locale | Locale Provider |   Access privileges
-----------+----------+----------+---------+---------+------------+-----------------+-----------------------
 postgres  | postgres | UTF8     | C.UTF-8 | C.UTF-8 |            | libc            |
 template0 | postgres | UTF8     | C.UTF-8 | C.UTF-8 |            | libc            | =c/postgres          +
           |          |          |         |         |            |                 | postgres=CTc/postgres
 template1 | postgres | UTF8     | C.UTF-8 | C.UTF-8 |            | libc            | =c/postgres          +
           |          |          |         |         |            |                 | postgres=CTc/postgres
(3 rows)


# ** This is level 5" **
# Restore Database : 
# I have to start by recreating a database
postgres=# CREATE DATABASE pire2pire;
# The console sends me a confirmation message :
CREATE DATABASE

# I can assign privileges in this database, with the "GRANT" command :
postgres=# GRANT ALL PRIVILEGES ON DATABASE pire2pire TO manuangot;
# The console sends me a confirmation message :
GRANT
# I can check the privileges with the command "\du"
postgres=# \du
                                   List of roles
 Role name |                         Attributes                         | Member of
-----------+------------------------------------------------------------+-----------
 manuangot | Superuser, Create role, Create DB                          | {}
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}


# Here is the command to call my backup file
postgres=# \q
postgres@DESKTOP-IE72UJ2:~$ psql pire2pire < p2pbackup.sql
# Postgrey performs restore

SET
SET
SET
SET
SET
 set_config
------------

(1 row)

SET
SET
SET
SET
SET
SET
CREATE TABLE
ALTER TABLE
CREATE SEQUENCE
ALTER TABLE
ALTER SEQUENCE
ALTER TABLE
COPY 3
 setval
--------
      1
(1 row)

ALTER TABLE
ALTER TABLE
ALTER TABLE
ALTER TABLE
postgres@DESKTOP-IE72UJ2:~$ psql
psql (15.3 (Ubuntu 15.3-1.pgdg22.04+1))
Type "help" for help.

# ** This is level 6" **
# Restore Database : 
# I can now reopen and use my database (add tables or content...)
> pgcli -h localhost -p 5432 -U manuangot pire2pire
Password for manuangot:
Server: PostgreSQL 15.3 (Ubuntu 15.3-1.pgdg22.04+1)
Version: 3.5.0
Home: http://pgcli.com

pire2pire> SELECT * FROM user_table;
+---------+------------+----------------+--------------+---------------+
| user_id | user_name  | user_firstname | user_birthay | user_password |
|---------+------------+----------------+--------------+---------------|
| 1       | Angot      | Henri          | 27-07-1974   | password123   |
| 2       | LaBretonne | Nolween        | 10-06-1995   | newPassNoween |
| 4       |  Apeuprès  | Jean-Michel    | 03-02-1970   | pas456        |
+---------+------------+----------------+--------------+---------------+
SELECT 3
Time: 0.014s
pire2pire>














