OpenNMS Playground using Docker
====

* [simple](./simple), starts OpenNMS, PostgreSQL and Helm/Grafana.
* [simple-kafka](./simple-kafka), starts OpenNMS, PostgreSQL, Helm/Grafana, one Minion and single cluster Kafka/Zookeeper.
* [cluster-kafka](./cluster-kafka), starts OpenNMS, PostgreSQL, Helm/Grafana, one Minion, Zookeeper cluster with 3 instances, Kafka cluster with 3 instances
* [cluster-kafka-shared](./cluster-kafka-shared), starts two OpenNMS environments (each with Horizon, PostgreSQL, and one Minion), Zookeeper cluster with 3 instances, Kafka cluster with 3 instances, Helm/Grafana with data sources for both environments.

Each directory contains more details about how to use the lab.