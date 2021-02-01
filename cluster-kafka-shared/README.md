Shared Kafka Cluster Demo with Mulple OpenNMS instances
====

A `docker-compose` lab to start 2 OpenNMS environments sharing the same Kafka/Zookepeer cluster. Each OpenNMS environment has a PostgreSQL 12, Horizon 27, and Minion 27. Then Grafana 7 with OpenNMS Helm 6.x is available with data sources for both OpenNMS environments.

This uses a custom 'Instance ID' to make sure the Kafka Topics used by one OpenNMS/Minion pair won't interfere with the other pair. For more information:

https://hackmd.io/XGpvmJoYT7iYyourTmU5Bw

The environment 1, uses an Instance ID of `DC1` and has a location called `Apex`; whereas the environment 2, uses an Instance ID of `DC2` and has a location called `Durham`.

It includes a modified configuration for `Pollerd` and `Collectd` to gather data every 30 seconds.

Kafka was configured to expose the client ports inside the Docker network and outside of it, in case you want to have  Minions runing outside Docker. It also expose JMX metrics on port 9999 to use CMAK (Kafka Manager) and to collect data from OpenNMS.

The Kafka Producer feature has been enabled in OpenNMS.

> No volumes are defined, meaning all data will be lost when stoping the lab.

## Usage

To start the lab:

```shell
docker-compose up -d
```

Wait a couple of minutes to make sure everything is running. You could use the following command to verify the status:

```shell
docker-compose ps
```

To stop the lab:

```shell
docker-compose down -v
```

To have shell access to OpenNMS:

```shell
docker-compose exec opennms bash
```

To access the database:

```shell
docker-compose exec database psql -U opennms opennms
```

OpenNMS Environment 1 contains:
- OpenNMS WebUI on port 8980
- OpenNMS Karaf Shell on port 8101
- PostgreSQL on port 5432
- Minon Karaf Shell on port 8201
- Minion listening for SNMP traps on port 1162
- Minion listening for Syslog messages on port 1514
- Minion listening for Netflow packets on port 8877

OpenNMS Environment 2 contains:
- OpenNMS WebUI on port 8981
- OpenNMS Karaf Shell on port 8102
- PostgreSQL on port 5433
- Minon Karaf Shell on port 8202
- Minion listening for SNMP traps on port 1163
- Minion listening for Syslog messages on port 1515
- Minion listening for Netflow packets on port 8878

OpenNMS environments are available on their respective ports on your machine IP address or localhost.

Grafana is available on port 3000 and contains data sources for both OpenNMS environments.

The Kafka Manager (CMAK) is exposed on port 9000, and for external Minions, Kafka should be reachable on ports 9192, 9292 and 9392 respectively (using the machine IP address or localhost).