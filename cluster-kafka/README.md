Kafka Cluster Demo
====

A `docker-compose` lab to start PostgreSQL 12, a cluster of 3 instances of Zookeeper 3.5, a cluster of 3 instances of Kafka 2.7, OpenNMS Horizon 27, Grafana 7, OpenNMS Helm 6.x, Grafana Imager Renderer for reports.

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

OpenNMS (WebUI and Karaf Shell) and Grafana are available on their respective default ports on your machine IP address or localhost.

The Kafka Manager (CMAK) is exposed on port 9000, and for external Minions, Kafka should be reachable on ports 9192, 9292 and 9392 respectively (using the machine IP address or localhost).