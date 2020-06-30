# satellite_grafana
Integration Satellite RedHat in Grafana (Datasource Postgres)

# 1 - Collect Pass Database Foreman Satellite
grep "password" /etc/foreman/database.yml | awk '{print $2}' | tr -d '"'

grep "jpa.config.hibernate.connection.password" /etc/candlepin/candlepin.conf | awk -F'=' '{print $2}'


# 2 - Configure Extern Access in Postgres
Edit the /var/lib/pgsql/data/postgresql.conf file:

vi /var/lib/pgsql/data/postgresql.conf

Remove the # and edit the following line to listen for inbound connections:

listen_addresses = '*'

Edit the /var/lib/pgsql/data/pg_hba.conf file:

vi /var/lib/pgsql/data/pg_hba.conf

Add the following line to the file:
host  all   all   satellite_server_ip/24   md5

Restart postgreSQL service to update with the changes:

systemctl restart postgresql

Note: Please take a snapshot/backup up of satellite server.


# 3 - Connect the Postgres with the Grafana
DataSource > PostgreSQL ( Insert Database Informations) and Test Connection with Database.

# 4 - Import the file Satellite65_stats.json in Grafana.
