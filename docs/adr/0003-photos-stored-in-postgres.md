# Bottle photos are stored in Postgres

Bottle photos are stored in Postgres as `bytea`, resized to about 800px when uploaded, rather than as files on a volume with only a path in the database. The user wants all of the collection's information in Postgres, and a personal Collection has at most a few hundred small photos, so the database stays small and a single `pg_dump` backs up everything.
