# MongoDB Dump and Restore with Docker Compose

This guide will walk you through the process of taking a MongoDB dump using Docker Compose, copying it to a local machine.

## Prerequisites

1. [Docker](https://docs.docker.com/get-docker/) installed on your local machine.
2. [Docker Compose](https://docs.docker.com/compose/install/) installed on your local machine.
3. [MongoDB Compass](https://www.mongodb.com/try/download/compass) installed for GUI access to MongoDB.


## Step 1: Create Docker Compose File

Create a `docker-compose.yml` file in your project directory with the following contents:

```yaml
version: '3'
services:
  mongodb:
    image: mongo:latest
    container_name: local-mongodb
    ports:
      - "27017:27017"
    environment:
          MONGO_INITDB_ROOT_USERNAME: YOUR_MONGODB_USERNAME
          MONGO_INITDB_ROOT_PASSWORD: YOUR_MONGODB_PASSWORD
```

Replace <YOUR_MONGODB_USERNAME> and <YOUR_MONGODB_PASSWORD> with your MongoDB credentials.

## Step 2: Start MongoDB Container
Run the following command to start the MongoDB container:

```bash
docker-compose up -d
```

## Step 3: Take a MongoDB Dump
Open a terminal and execute the following command to take a MongoDB dump inside the Docker container:

```bash
docker exec -it <your-container-name> mongodump --uri="<YOUR_MONGODB_URI_STRING>" --out=/dump
```

Replace <your-container-name> with the actual container name, and <YOUR_MONGODB_URI_STRING> with your MongoDB URI string.

`--out=/dump:` This tells mongodump where to store the dump files. In this case, the dump will be stored in the /dump directory inside the container.

## Step 4: Copy the Dump to Your Local Machine
To copy the dump from the Docker container to your local machine, run:

```bash docker cp <your-container-name>:/dump /path/on/host/machine```







