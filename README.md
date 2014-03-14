POSTGRESQL COMMAND LINE INTERFACE
=================================

Useful commands to navigate the PostgreSQL CLI
----------------------------------------------

### psql
`psql [option...] [dbname [username]]`

If you just type `psql` into the console, PG will try to connect to a database
with the same name as your host machine.

    mymac:~ username$ psql
    psql: FATAL:  database "username" does not exist
