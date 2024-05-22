
# ELK Stack Docker Compose

This Docker Compose file sets up an ELK (Elasticsearch, Logstash, Kibana) stack with Elasticsearch and Kibana containers. It also includes network and volume configurations for persistent data storage.

## Prerequisites

- Docker and Docker Compose installed on your system.
- A `.env` file in the same directory as the Docker Compose file, containing the following environment variables:
 - `ELASTIC_USER`: The username for accessing Elasticsearch (default: `elastic`).
 - `ELASTIC_PASS`: The password for accessing Elasticsearch.

## Getting Started

1. Clone this repository or copy the Docker Compose file to your local machine.
2. Create a `.env` file in the same directory as the Docker Compose file and set the `ELASTIC_USER` and `ELASTIC_PASS` environment variables with your desired values.
3. Open a terminal, navigate to the directory containing the Docker Compose file, and run the following command to start the containers:

    `docker-compose up -d`

4. Once the containers are up and running, you can access the following services:
   - Elasticsearch: `http://localhost:9200`
   - Kibana: `http://localhost:5601`

## Services

### Elasticsearch

- **Image**: `elasticsearch:8.0.1`
- **Container Name**: `elastic`
- **Ports**: `9200:9200`
- **Volumes**: `elastic_volume` mounted at `/usr/share/elasticsearch/data`
- **Environment Variables**:
  - `discovery.type=single-node`: Configures Elasticsearch to run in single-node discovery mode.
  - `ELASTIC_PASSWORD`: The password for accessing Elasticsearch, set from the `.env` file.
- **Network**: `elk`
- **Healthcheck**: Checks if Elasticsearch is running and accessible using the provided credentials.

### Kibana

- **Image**: `kibana:8.0.1`
- **Container Name**: `kibana`
- **Ports**: `5601:5601`
- **Volumes**: `kibana_volume` mounted at `/usr/share/kibana`
- **Network**: `elk`

## Networks

- **elk**: A bridge network with a subnet `123.123.0.0/16`.

## Volumes

- **elastic_volume**: A local volume for persisting Elasticsearch data.
- **kibana_volume**: A local volume for persisting Kibana data.

## Environment Variables

The following environment variables are required and should be set in the `.env` file:

- `ELASTIC_USER`: The username for accessing Elasticsearch (default: `elastic`).
- `ELASTIC_PASS`: The password for accessing Elasticsearch.

## Stopping and Removing Containers

To stop and remove the containers, run the following command:

    docker-compose down

This will stop and remove the containers, but the volumes will persist. If you want to remove the volumes as well, add the `-v` flag:

    docker-compose down -v

## Upgrading or Changing Versions

To upgrade or change the versions of Elasticsearch or Kibana, modify the `image` fields in the Docker Compose file with the desired version tags, and then run `docker-compose up -d` to apply the changes.

Note that upgrading versions may require additional steps, such as data migration or configuration changes, which are not covered in this README. Refer to the official documentation for the specific versions you are upgrading to for more information.


