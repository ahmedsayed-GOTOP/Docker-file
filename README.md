# Node.js + MongoDB Docker Project

A containerized web application built with **Docker** and **Docker Compose**, using **Node.js**, **MongoDB**, and **Mongo Express**.

This project is adapted from [TechWorld with Nana's Docker tutorial](https://gitlab.com/nanuchi/techworld-js-docker-demo-app), with additional configuration for environment variables and Docker Compose.

## Architecture

The application consists of three services:

- **my-app:** Node.js web application running on port `3000`.
- **mongodb:** MongoDB database running on port `27017`.
- **mongo-express:** Web-based MongoDB management interface running on port `8080`.

All services communicate through a Docker Compose network. MongoDB data is persisted using a named Docker volume.

## Prerequisites

- Docker Engine
- Docker Compose plugin

## Getting Started

1. Clone the repository:

   ```bash
   git clone https://github.com/ahmedsayed-GOTOP/Docker-file.git
   cd Docker-file
   ```

2. Create your environment file:

   ```bash
   cp .env.example .env
   ```

3. Edit `.env` and set your own database credentials and connection string. Make sure the password in `MONGO_URL` matches `MONGO_INITDB_ROOT_PASSWORD`.

4. Build and start the services:

   ```bash
   docker compose up -d --build
   ```

5. Check the running containers:

   ```bash
   docker compose ps
   ```

## Access the Application

- Web application: http://localhost:3000
- Mongo Express: http://localhost:8080

## Useful Commands

```bash
# View service logs
docker compose logs -f

# Stop services
docker compose down

# Stop services and remove the database volume
docker compose down -v
```

**Warning:** `docker compose down -v` deletes the persisted MongoDB data.

## Technologies

- Docker
- Docker Compose
- Node.js
- Express.js
- MongoDB
- Mongo Express

## What I Practiced

- Building a Docker image using a Dockerfile.
- Running multiple containers with Docker Compose.
- Connecting application and database containers through a Docker network.
- Configuring services using environment variables.
- Persisting database data with Docker volumes.
- Testing application-to-database connectivity.## demo app - developing with Docker

This demo app shows a simple user profile app set up using 
- index.html with pure js and css styles
- nodejs backend with express module
- mongodb for data storage

All components are docker-based

### With Docker

#### To start the application

Step 1: Create docker network

    docker network create mongo-network 

Step 2: start mongodb 

    docker run -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb --net mongo-network mongo    

Step 3: start mongo-express
    
    docker run -d -p 8081:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password --net mongo-network --name mongo-express -e ME_CONFIG_MONGODB_SERVER=mongodb mongo-express   

_NOTE: creating docker-network in optional. You can start both containers in a default network. In this case, just emit `--net` flag in `docker run` command_

Step 4: open mongo-express from browser

    http://localhost:8081

Step 5: create `user-account` _db_ and `users` _collection_ in mongo-express

Step 6: Start your nodejs application locally - go to `app` directory of project 

    npm install 
    node server.js
    
Step 7: Access you nodejs application UI from browser

    http://localhost:3000

### With Docker Compose

#### To start the application

Step 1: start mongodb and mongo-express

    docker-compose -f docker-compose.yaml up
    
_You can access the mongo-express under localhost:8080 from your browser_
    
Step 2: in mongo-express UI - create a new database "my-db"

Step 3: in mongo-express UI - create a new collection "users" in the database "my-db"       
    
Step 4: start node server 

    npm install
    node server.js
    
Step 5: access the nodejs application from browser 

    http://localhost:3000

#### To build a docker image from the application

    docker build -t my-app:1.0 .       
    
The dot "." at the end of the command denotes location of the Dockerfile.
