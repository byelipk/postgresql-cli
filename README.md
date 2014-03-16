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

### Logging in with a newly created role
To log into psql with your newly created role, you can type the following into
your terminal: `psql -U rails_app -W rails_app_development`

Let's break this down. You'll see it's pretty simple. The `-U` flag allows to 
enter a user name so that we do not end up trying to connect as the superuser -
which is not a best pactice as it is a security risk! The `-W` flag means that 
psql will prompt us for our password before logging us into the database. 
Finally we pass in the name of the database at the end of the command.


### Viewing all databases
You can run `\l` to get a list of all databases.

### Viewing database tables
Run `\dt` to view all tables inside a databse.

### Importing data
Inside psql you can run `\i path_to_dataset` in order to import sql data into an
*empty* database. PGAdmin III allows you to import .tar files, but not raw sql.
So using the command line to import new data into an empty database is a very
efficient alternative.
