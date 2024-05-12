---
id: 02_setup
tags:
  - backend
  - docker
  - famcal
---

# Setup

![container.png](../../../static/img/container.png)

## Github Repositories
- ### Frontend
  - Github      : https://github.com/thomasIBAW/pa-frontend
  - Docker Hub  : https://hub.docker.com/repository/docker/ircnega/pa-frontend/general
  - The Frontend exposes the public view to the internet. It's a react application
- ### Backend
  - Github      : https://github.com/thomasIBAW/pa_backend
  - Docker Hub  : https://hub.docker.com/repository/docker/ircnega/pa-backend/general
  - Backend handels all requests from the frontend. Backend is the proxy to the Database. It runs on node.js
- ### Database
  - Github      : -
  - Docker Hub  : https://hub.docker.com/repository/docker/ircnega/famcal_db/general
- ### Documentation
  - Github      : https://github.com/thomasIBAW/pa-docu
  - Docker Hub  : https://hub.docker.com/repository/docker/ircnega/pa-docu/general


## Docker compose

The quickest way to run Family Calendar is through docker-compose. This Docker Compose file requires a running Traefik Proxy to handle Traefik Labels. (Traefik is not part of this deployment!)




```yaml
version: '3.4'

services:
  db:
    image: ircnega/famcal_db:0.1.0
    networks:
      - appIntern
    ports:
      - "27017"

  backend:
    image: ircnega/pa-backend:0.9.7
    networks:
      - traefik-proxy
      - appIntern
    ports:
      - "3005"
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.famsocket.rule=Host(`api.backend.famcal.ch`)"
      - "traefik.http.routers.famsocket.entrypoints=https"  
      - "traefik.http.routers.famsocket.tls.certresolver=le"  
      - "traefik.docker.network=traefik-proxy"
    restart: always
    environment:
      port: '3005'
      mongo_connection: 'mongodb://db:27017/'
      mySecret: 'yourSecretString' # Change this String to secure your Installation

  frontend:
    image: ircnega/pa-frontend:0.9.19
    ports:
      - "80"
    restart: always
    networks:
      - traefik-proxy
      - appIntern
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.famFrontend.rule=Host(`app.famcal.ch`)"
      - "traefik.http.routers.famFrontend.entrypoints=https"  
      - "traefik.http.routers.famFrontend.tls.certresolver=le"  
      - "traefik.http.routers.famFrontend.middlewares=https-redirect"  

      - "traefik.http.middlewares.https-redirect.redirectscheme.scheme=https"
      - "traefik.http.middlewares.https-redirect.redirectscheme.permanent=true"

      - "traefik.docker.network=traefik-proxy"
    environment:
      VITE_DEVSTATE: PROD # Defines if the System is running PROD
    mongo-express:
      image: mongo-express
      restart: always
      networks:
        - appIntern
      ports:
        - "8081:8081"
      environment:
        # ME_CONFIG_MONGODB_ADMINUSERNAME: xxx
        # ME_CONFIG_MONGODB_ADMINPASSWORD: xxx
        ME_CONFIG_MONGODB_URL: mongodb://db:27017/
        # ME_CONFIG_MONGODB_URL: mongodb://root:example@mongo:27017/
  docu:
      image: ircnega/pa-docu:latest
      restart: always
      labels:
        - "traefik.enable=true"
        - "traefik.http.routers.famDocs.rule=Host(`docs.famcal.ch`)"
        - "traefik.http.routers.famDocs.entrypoints=https"  
        - "traefik.http.routers.famDocs.tls.certresolver=le"  
        - "traefik.http.routers.famDocs.middlewares=https-redirect"  

        - "traefik.http.middlewares.https-redirect.redirectscheme.scheme=https"
        - "traefik.http.middlewares.https-redirect.redirectscheme.permanent=true"

        - "traefik.docker.network=traefik-proxy"
      networks:
        - traefik-proxy

networks:
  traefik-proxy:
    external: true
  appIntern:
    driver: bridge

```