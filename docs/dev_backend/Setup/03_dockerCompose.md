---
id: 03_docker
tags:
  - backend
  - docker
  - famcal
---
# Docker compose

The quickest way to run Family Calendar is using docker-compose. 

Create a folder and add a `docker-compose.yml` file

Edit the file and add :

```yaml
services:
  db:
    image: ircnega/pa-db:1.0.0
    ports:
      - "27017"
    volumes:
      - mongo-data:/data/db
  backend:
    image: ircnega/pa-backend:0.9.18
    ports:
      - "3005"
    restart: always
    environment: # Check and adapt these settings
      port: '3005'
      mongo_connection: 'mongodb://db:27017/' # only change if you know what you do :) 
      mySecret: 'changeThisSecret' # ACTION NEEDED -> Change this String to secure your Installation
      LOG_LEVEL: "debug" # Define the loglevel to be written to the logfile (debug, info, warn or error)
      CONS_LOG_LEVEL: "debug" # Define the loglovel for the console (debug, info, warn or error)
  frontend:
    image: ircnega/pa-frontend:0.9.33
    ports:
      - "80:80"
    restart: always
    environment:
      VITE_DEVSTATE: PROD # only change if you know what you do :)
  mongo-express:
    image: mongo-express
    restart: always
    ports:
      - "8081:8081"
    environment:
      ME_CONFIG_MONGODB_URL: mongodb://db:27017/
      ME_CONFIG_BASICAUTH_USERNAME: "admin" # you can change this String to your mongo-express username
      ME_CONFIG_BASICAUTH_PASSWORD: "youradminpassword" # ACTION NEEDED -> Change this String to your mongo-express password

volumes:
  mongo-data:

```

Start the family calendar by running `docker compose up -d`

once all the containers are running, open a broser to `http://localhost:80`  

:::info
The only container that will be reachable is the `frontend`. If you need to reach the `backend` for any API integration, then you will have to map a port to the internal port. 

The DB Data is mounted in a volume for persistence.

VITE_DEVSTATE: PROD in `frontend` means that the connection to the `backend` is proxied directly from nginx to the `backend`  container. If this value is changed, then the `backend` container will be accessed using `http://localhost:3005`(hardcoded)

mongo-express is used to access the db for troubleshooting and debug. mongo-express is not needed for family calendar to work. 
:::


