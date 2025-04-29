1.

- The HOST_PORT:CONTAINER_PORT
  This setting is 27018:27017 by default in LibreChat repo.
  27018 → is the port on your host machine (your laptop).
  27017 → is the port inside the container (where MongoDB is running internally).

- To keep it simple locally, make the two ports same
  make sure everywhere using 27017:27017 instead of 27018:27017
  This will make sure both laptop/desktop and container can access MongoDB container through port 27017

- Make sure define the container in docker-compose.yml

```yml
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
