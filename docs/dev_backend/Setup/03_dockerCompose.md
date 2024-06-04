---
id: 03_docker
tags:
  - backend
  - docker
  - famcal
---
# Docker compose

The quickest way to run Family Calendar is using docker-compose. 


```yaml
version: '3.4'

services:
  db:
    image: ircnega/pa-db:1.0.0
    networks:
      - appIntern
    ports:
      - "27017"
  backend:
    image: ircnega/pa-backend:0.9.18
    ports:
      - "3005"
    restart: always
    environment:
      port: '3005'
      mongo_connection: 'mongodb://db:27017/'
      mySecret: 'yourSecretString' # Change this String to secure your Installation
      LOG_LEVEL: "debug" # Define the loglevel to be written to the logfile (debug, info, warn or error)
      CONS_LOG_LEVEL: "debug" # Define the loglovel for the console (debug, info, warn or error)
  frontend:
    image: ircnega/pa-frontend:0.9.33
    ports:
      - "80:80"
    restart: always
    environment:
      VITE_DEVSTATE: PROD # Defines if the System is running PROD
  mongo-express:
    image: mongo-express
    restart: always
    ports:
      - "8081:8081"
    environment:
      ME_CONFIG_MONGODB_URL: mongodb://db:27017/
  # docu:
  #     image: ircnega/pa-docu:0.9.20
  #     restart: always

```


