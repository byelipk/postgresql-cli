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


### Logging in
On the Mac PG sets the `SUPERUSER` to the name of the host machine and creates a
new database owned by the `SUPERUSER` called `postgres`. On Ubuntu
linux, my experience has been that PG will set the `SUPERUSER` to `postgres`.

On a Mac we can log into PG with the following command: `sudo -u user psql
postgres`. A shorter form of would be `psql postgres`. 

All that is going on here is that we are invoking the `psql` command as the root
user in order to connect to the database that PG created especially for the
`SUPERUSER`.
