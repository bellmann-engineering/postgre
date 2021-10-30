Arbeiten mit Konsolenbefehlen
-----------------------------

### Alle Datenbanken anzeigen

    postgres=# \l
                                      List of databases
       Name    |  Owner   | Encoding |   Collate   |    Ctype    |   Access privileges
    -----------+----------+----------+-------------+-------------+-----------------------
     postgres  | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
     template0 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
               |          |          |             |             | postgres=CTc/postgres
     template1 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres          +
               |          |          |             |             | postgres=CTc/postgres
    (3 rows)

oder ohne vorherigen Login mit "***sudo -u postgres psql -l***"

### Benutzer auflisten

    postgres-# \du
                                 List of roles
     Role name |                   Attributes                   | Member of
    -----------+------------------------------------------------+-----------
     postgres  | Superuser, Create role, Create DB, Replication | {}
     yolo      | Superuser                                      | {}

### Zu einer Datenbank verbinden

    postgres=#\c Datenbankname

    You are now connected to database "Datenbankname" as user "postgres".

### Tabellen anzeigen

    postgres=#\dt 

### Schemas anzeigen

    postgres=#\dn

### Funktionen anzeigen

    postgres=#\df oder df+

### Sequenzen anzeigen

    postgres=#\ds

### Views anzeigen

    postgres=#\dv

### Datenbank und Benutzer mit Rechten erstellen

    CREATE datenbank;
    CREATE USER benutzer WITH PASSWORD 'Geheim';  
    GRANT ALL PRIVILEGES ON DATABASE datenbank to benutzer; 

### Alle verfügbaren Konsolenbefehle anzeigen

    postgres=#\?

### Eine bestimmte Datenbankgröße auslesen

    select pg_database_size('Datenbankname');

oder in schön

    SELECT pg_size_pretty(pg_database_size('Datenbankname'));

oder alle vorhanden Datenbankgrößen anzeigen

    select datname, pg_size_pretty(pg_database_size(datname)) as size from pg_database;

### Offene Datenbankverbindungen anzeigen

    SELECT datname,usename,client_addr,client_port FROM pg_stat_activity ;

### Die Konfiguration neu laden (ohne Neustart)

    select pg_reload_conf();

### Logfile Rotation anwerfen

    select pg_rotate_logfile()

### PostgreSQL verlassen

    postgres=#\q

Backup und Wiederherstellung
----------------------------

### Ein Datenbank Backup erstellen

    pg_dump --user username --host hostname -b -F c datenbank > /tmp/datenbank.dump 

### Alle verfügbaren Datenbanken sichern

    pg_dumpall

### Datenbank wiederherstellen

    pg_restore --user username --host hostname -c -d datenbank datenbank.dump


