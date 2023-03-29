## Developing with Docker

This repository demonstrates the use of docker for local development for Node.js application plus integrating it with Mongodb and Mongoexpress conatiners.
- index.html with pure js and css styles
- nodejs backend with express module
- mongodb for data storage

All components are docker-based

### Install docker and start Mongodb container

Step 1: Install Docker on local machine. We can download it from the official Docker website: https://www.docker.com/get-started

step 2: Install the MongoDB image from the Docker Hub repository by running the following command in terminal:

    docker pull mongo

step 3 : Start a MongoDB container by running the following command in terminal:

    docker run -d -p 27017:27017 --name mongodb mongo
    
 Note: This above command starts a MongoDB container in detached mode (-d), maps the container's port 27017 to your local port 27017 (-p 27017:27017), and gives the container a name (--name mongodb).   


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

    cd app
    npm install 
    node server.js
    
Step 7: Access you nodejs application UI from browser

    http://localhost:3000
