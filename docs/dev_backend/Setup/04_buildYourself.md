---
id: 04_build
tags:
  - backend
  - docker
  - famcal
---
# Build yourself

If you prefer to build yourself:

:::info
As you run the system without docker compose, think about the needed port mappings. you will need to expose all the ports, not only 80 for the frontend. 
We encourage to use the docker compose approach.
:::

### Frontend
Get files from GitHub

`git clone https://github.com/thomasIBAW/pa-frontend.git`

`cd pa-frontend` to enter the directory

then install dependencies
`npm install`

then run 
`npm run build`

to have a local version of the frontend.

To create the image run 
`docker build -t frontend .`

to run the container run
`docker run -d -p 80:80 --name frontend frontend` 

### Backend

Get files from Github
`git clone https://github.com/thomasIBAW/pa_backend.git` 

`cd pa_backend` to enter the directory

then install dependencies
`npm install`

Create a .env file.
Modify the .env file to reflect your environment

```env
; APPLICATION SETTINGS

; Define the port the backend will listen to:

port = <enter your port here as Number eg: 3005>
mongo_connection = <Set your mongo connection line eg: 'mongodb://localhost:27017'>

; will change to mongodb://db:27017 after deployment with docker-compose


; SECURITY SETTINGS
; Important : change the current "yourSecretString" to any random string:

mySecret = <Set your secret eg: "yourSecretString">

; Define the loglevel to be written to the logfile (debug, info, warn or error)
LOG_LEVEL: "debug" 

; Define the loglEvel for the console (debug, info, warn or error)
CONS_LOG_LEVEL: "debug" 
```
then build the image
`docker build -t backend .`

to start the container run 
`docker run -d -p 3005:3005 --name backend backend`



### Database
Get files from Github
`git clone https://github.com/thomasIBAW/pa-database.git`

`cd pa-database` to enter the directory

then build the image
`docker build -t database .`

to start the container run 
`docker run -d -p 27017:27017 --name db -v mongo-data:/data/db database` 

This starts the DB container, creates the database and collections, and initialize it with the needed indexes. The DB is now reachable on port 27017

:::warning
As the primary idea is to run all containers using docker compose (isolated network and only expose the frontend), I have not added any username or passwords to mongoDB. Feel free to modify the `Dockerfile`
:::

## Connection
once all the container run, open a broser to `http://localhost:80`  
