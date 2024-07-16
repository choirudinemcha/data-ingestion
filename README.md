# Data Ingestion

## Docker services:
- Airflow:5053
- Redis:6739
- Flower:5555
- Mysql:5057
- PostgreSql:5051
- Portainer:5052
- Grafana:5056

## Prerequisites
Make sure docker engine and docker compose are installed on your computer.

Docke Engine
```url
https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04
```

Docker Compose
```url
https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-compose-on-ubuntu-20-04
```

## Installation Steps

For the installation docker service using docker compose
1. Make sure docker-compose.yaml, Dockerfile and requirements.txt in your working directory
2. Configure Docker Compose, Open the docker-compose.yaml file and adjust the necessary settings, such as container name, used ports, and environment variables.
3. Build Docker Image
Open a terminal or command prompt, navigate to your working directory containing the docker-compose.yaml and Dockerfile files, then run the following command to build the Docker image and install dependencies:
using docker compose v2
```bash
sudo docker compose build
```
4. Initializes a Docker container containing Apache Airflow using Docker Compose
```bash
sudo ​​docker compose up -d airflow-init
```
5. Run Container
Once the build process completes, run the following command to create and start container:
```bash
sudo docker compose up -d
```
6. Verify the Installation
To see what images are installed in docker
```bash
docker images
```
To see what container are running in docker
```bash
docker ps -a
```
Make sure the **port** is the same as set in docker-compose.yaml

- Apache Airflow

Open a browser and access the URL http://localhost:5053 or adjust it according to the port you configured in the docker-compose.yaml file. You will see the Apache Airflow interface.

- Mysql

try to connect via a data base manager like dbeaver or phpmyadmin enter according to the credential and port that you configured in docker-compose.yaml

if you want to grant all access to an existing user or to create a new user:
1. connection as root user in database manager
2. run query

create user and password
```sql
CREATE USER 'your_username'@'%' IDENTIFIED BY 'your_password';
```

grant all permissions to the user
```sql
GRANT ALL ON *.* TO 'your_username'@'%';
```

to apply the changes immediately
```sql
FLUSH PRIVILEGES;
```

- portainer

Open a web browser and enter the URL https://localhost:9443 to access the Portainer.

When accessing Portainer via the web you may receive the following error message: "Client sent an HTTP request to an HTTPS server" change http to https
```link
https://portal.portainer.io/knowledge/client-sent-an-http-request-to-an-https-server

```

- Grafana
Open a web browser and enter the URL http://192.168.10.202:3000/ to access Grafana


## Kafka

## Prerequisites
Make sure java JDK 11 are installed on your computer

## Installation Steps

1. Install Java JDK version 11
```bash
wget -O- https://apt.corretto.aws/corretto.key | sudo apt-key
```
```bash
sudo add-apt-repository 'deb https://apt.corretto.aws stable main'
```
```bash
sudo apt-get update; sudo apt-get install -y java-11-amazon-corretto-jdk
```
2. Download Apache Kafka from https://kafka.apache.org/downloads under Binary Downloads
or using wget command
```bash
wget https://archive.apache.org/dist/kafka/3.0.0/kafka_2.13-3.0.0.tgz
```
3. Download and extract the contents to a directory of your choice, for example ~/kafka_2.13-3.0.0 .
```bash
tar xzf kafka_2.13-3.0.0.tgz
```
## How to Running Program

Go to folder your kafka extract location

1. Starting Zookeeper

Kafka relies on Zookeeper, in order to make it run we will have to run Zookeeper first.

```bash
bin/zookeeper-server-start.sh config/zookeeper.properties
```

2. Starting Kafka server

Next, we have to start Kafka broker server:
```bash
bin/kafka-server-start.sh config/server.properties
```

3. Create Topics

Messages are published in topics. Use this command to create a new topic. example create topic name = test

```bash
bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic test
```

4. list all available topics, by running the following command

```bash
bin/kafka-topics.sh --list --bootstrap-server localhost:9092
```

5. Sending Messages

Next, we have to send messages, producers are used for that purpose. Let’s initiate a producer. 

```bash
bin/kafka-console-producer.sh --broker-list localhost:9092 --topic topic_name
```

6. Consuming Messages

Messages that are stored should be consumed too. Let’s started a console based consumer.

```bash
bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic topic_name --from-beginning
```











