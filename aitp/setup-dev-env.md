## Install necessary tools

1. Install Terraform

- option 1: https://developer.hashicorp.com/terraform/install
- option 2: brew install terraform

2. https://www.docker.com/get-started/

3. https://www.mongodb.com/products/tools/compass

## Run application & connect to the MongoDB in Docker

- The HOST_PORT:CONTAINER_PORT
  This setting is 27018:27017 by default in the LibreChat repo.
  27018 → is the port exposed to your hosting machine (where MongoDB is accessed by local app running on your laptop).
  27017 → is the port exposed to other containers running in Docker (where MongoDB is accessed by other containers).

- To keep it simple, change the two ports to be same 27017
  change the port in the docker-compose.override.yml to be 27017:27017 instead of 27018:27017
  This will make sure both laptop/desktop and containers can access the MongoDB container through the same port 27017

```yml
# docker-compose.override.yml
mongodb:
  container_name: chat-mongodb
  expose:
    - 27017
  ports:
    - 27017:27017
  image: mongo
  # restart: always
  volumes:
    - ./data-node:/data/db
  command: mongod --noauth
```

## Modify .env file to run locally

1. The Mongo URI

   1.1 Access MongoDB running in a local Docker container
   MONGO_URI=mongodb://127.0.0.1:27017/LibreChat

   1.2 Access Azure CosmosDB MongoDB
   MONGO_URI=mongodb://{CosmosAccountName}:{CosmosAccountKey}@{CosmosAccountKey}.mongo.cosmos.azure.com:10255/?ssl=true&retrywrites=false&replicaSet=globaldb&maxIdleTimeMS=120000&appName=@{CosmosAccountKey}@

2.
