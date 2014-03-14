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

### Viewing all roles
Once you log in you can run `\dg` to view all roles and their permissions. Roles
are synonymous with 'users'.

### Creating a new role
The SQL to create a new role is faily simple. We just type `CREATE ROLE
new_role` then pass in any permissions we wish to grant to the new role. So if I
wanted to create a new superuser role, the SQL would be as follows: `CREATE ROLE
new_su SUPERUSER`. Pretty simple.

If you are working on a rails app and you want to use a PG datastore, you might
need to create a new role with the ability to create a database (i.e. for a rake
command like `rake db:create`), and that requires authentication. To do that you 
might write the following SQL: `CREATE ROLE rails_app CREATEDB LOGIN PASSWORD 'rubyonrails'`.  

    CREATE ROLE name [ [ WITH ] option [ ... ] ]

    where option can be:

    SUPERUSER | NOSUPERUSER
        | CREATEDB | NOCREATEDB
        | CREATEROLE | NOCREATEROLE
        | CREATEUSER | NOCREATEUSER
        | LOGIN | NOLOGIN

### Viewing all databases
You can run `\l` to get a list of all databases.
