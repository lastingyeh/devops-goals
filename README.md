# docker

### network

- create network default (bridge)

      $ docker network create goals-net

### backend (./backend)

- Features

  - volume

  - environment override building image

  - expose port

  - connect to network 'goals-net' 

  - no network alternatively

        $ docker inspect <container>

      - find host-ip from 'NetworkSettings.Networks.bridge.IPAddress'

      - use host-ip replaced

      - 'host.docker.internal' can't use in linux (just enable in windows/mac)

- Create Dockerfile and build image

      $ docker build -t goals-node ./backend

- Run container [goals-backend] 

      $ docker run --name goals-backend -v $PWD/backend:/app -v logs:/app/logs -v /app/node_modules --rm -d -e MONGODB_USERNAME=user --network goals-net -p 8000:8000 goals-node

### frontend (./frontend)

- Features

  - volume (hot reload)

  - environment (hot reload)

  - expose port
  
- Create Dockerfile and build image

      $ docker build -t goals-react ./frontend

- Run container [goals-frontend] 

      $ docker run --name goals-frontend -v $PWD/frontend:/app -v /app/node_modules --rm -it -e CHOKIDAR_USEPOLLING=true -p 3000:3000 goals-react

### mongodb 

- Features

  - volume (data storage)

  - environment (auth user)

  - connect to network 'goals-net' 

- Run container [mongodb] 

      $ docker run --name mongodb --rm -v data:/data/db -d --network goals-net -e MONGO_INITDB_ROOT_USERNAME=user -e MONGO_INITDB_ROOT_PASSWORD=secret mongo


# docker-compose

- up & build

      $ docker-compose up -d --build 

- down 

      $ docker-compose down

---
references

- [Docker & Kubernetes: The Practical Guide](https://www.udemy.com/course/docker-kubernetes-the-practical-guide/)

- [Docker-compose](https://docs.docker.com/compose/compose-file/)

- [Docker](https://docker.com)