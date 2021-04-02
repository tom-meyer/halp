### Misc PSQL commands

Set namespace:

    set search_path = myproject, public;

Toggle extended display:

    \x
    select * from mytable \x\g\x

Toggle paging:

    \pset pager

Toggle query timings:

    \timings

Copy out to file:

    \copy (select * from mytable) to './mytable.csv'


## PSQL password file

psql is strict wrt perms; do: `chmod 0600 ~/.pgpass`

More here: https://www.postgresql.org/docs/current/libpq-pgpass.html

Format:

    hostname:port:database:username:password

Env var 'PGPASSFILE' can be set to point at alt path for the file.

### PSQL start up commands

Put `SET` and `\set` commands in `~/.psqlrc` to be executed upon psql start up.
