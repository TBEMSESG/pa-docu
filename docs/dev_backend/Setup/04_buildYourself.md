---
id: 04_build
tags:
  - backend
  - docker
  - famcal
---
# Build yourself

If you prefer to build yourself:

Create a folder somewhere in your system, let's say its `/script`

`cd /script` to enter this folder

### Frontend
Get files from GitHub

`git clone https://github.com/thomasIBAW/pa-frontend.git`

`cd pa-frontend` to enter the directory

then install dependencies
`npm install`

`cd ..` to go back to `/script`
### Backend

Get files from Github
`git clone https://github.com/thomasIBAW/pa_backend.git` 

`cd pa_backend` to enter the directory

then install dependencies
`npm install`

`cd ..` to go back to `/script`

### Database
Get files from Github
`git clone https://github.com/thomasIBAW/pa-database.git`

:::info
There is nothing to do at db level, as we will create a completely new db that will be initialized at build.
:::

## Build all images 

create a file called `docker-compose.yml` in `/script`

Add the folloewing content to the newly created file

```yaml
services:
  db:
    build: /pa-database
    # ports:
    #   - "27017"
    volumes:
      - mongo-data:/data/db
  backend:
    build: /pa_backend
    # ports:
    #   - "3005"
    restart: always
    environment: # Check and adapt these settings
      port: '3005'
      mongo_connection: 'mongodb://db:27017/' # only change if you know what you do :) 
      mySecret: 'changeThisSecret' # ACTION NEEDED -> Change this String to secure your Installation
      LOG_LEVEL: "debug" # Define the loglevel to be written to the logfile (debug, info, warn or error)
      CONS_LOG_LEVEL: "debug" # Define the loglovel for the console (debug, info, warn or error)
  frontend:
    build:
      context: /pa-frontend
      args:
        VITE_DEVSTATE: PROD # only change if you know what you do :)
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
      ME_CONFIG_BASICAUTH_USERNAME: "admin" # you can change this String to your mongo-express web username
      ME_CONFIG_BASICAUTH_PASSWORD: "youradminpassword" # ACTION NEEDED -> Change this String to your mongo-express web password

volumes:
  mongo-data:

```

Run `docker compose build` 

run `docker compose up -d`


### Important considerations

This starts the DB container, creates the database and collections, and initialize it with the needed indexes. The DB is only reachable from within the docker compose created network.

If you need to run the frontend on a different port (because 80 is already in use), the use 5173, which is already in the allowed oringins. If you need to use another port, then you have to adapt CORS settings on `/pa_backend/index.js`.

mongo-express is used to access the db for troubleshooting and debug. mongo-express is not needed for family calendar to work. 

:::warning
As the primary idea is to run all containers using docker compose (isolated network and only expose the frontend), I have not added any username or passwords to mongoDB. Feel free to modify the `Dockerfile` in case you wuold prefer to have one.
:::

## Connection
once all the containers are running, open a broser to `http://localhost:80`  
