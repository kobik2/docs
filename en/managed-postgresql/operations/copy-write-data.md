# Copying and populating a table from a local machine

You can both [copy](#copy) data from a table to a local file and [populate](#write) a table with data from a local file using the [psql]({{ pg-docs }}/app-psql.html) interactive terminal.

## Getting started {#before-you-begin}

1. [Get an SSL certificate](../../managed-postgresql/operations/connect.md#get-ssl-cert).
1. Install the dependencies:

   ```bash
   sudo apt update && sudo apt install --yes postgresql-client
   ```

## Copying data from a table {#copy}

To copy table data to a file, run this command:

```bash
psql "host=c-<cluster ID>.rw.{{ dns-zone }} \
    port={{ port-mgp }} \
    sslmode=verify-full \
    dbname=<DB name> \
    user=<username> \
    target_session_attrs=read-write" \
    -c "\copy (SELECT * FROM <table name>) to stdout(DELIMITER '<delimiter character>')" \
    >> <local file name>
```

## Populating a table with data {#write}

{% note info %}

You need to create a table in advance. The number of columns and data types in a local file must match the {{ mpg-name }} table parameters.

{% endnote %}

To populate your table with data from a local file, run this command:

```bash
cat <name of local file> | \
psql "host=c-<cluster ID>.rw.{{ dns-zone }} \
    port={{ port-mgp }} \
    sslmode=verify-full \
    dbname=<DB name> \
    user=<username> \
    target_session_attrs=read-write" \
    -c "COPY <table name> FROM stdin (DELIMITER '<delimiter character>')"
```
