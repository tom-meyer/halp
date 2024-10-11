### Active connections

Active connections are available to query in `pg_stat_activity`.

    SELECT pid, usename, datname, client_addr, state, query FROM pg_stat_activity;
    \dS pg_stat_activity

Having a bunch of idle connections is generally not bad. Issues arise when
multiple concurrent queries are going on.

Kill a connection with:

    SELECT pg_terminate_backend(12345); -- use the pid from the pg_stat_activity table

### Max connections

    SHOW max_connections;

RDS instances set max_connections based on the instance class memory, specifically: `LEAST({DBInstanceClassMemory/9531392},5000)`


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
