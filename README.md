## Demo App - Developing and Containerized with Docker

This demo app shows a simple user profile app set up using 
- index.html with pure js and css styles
- nodejs backend with express module
- mongodb for data storage

All components are docker-based

### With Docker

#### Application Workflow During Development
![Dev-Workflow](https://github.com/nirdeshkumar02/Docker-Conceptual-Project/blob/master/Application_Workflow_During_Development.png)

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

### With Docker Compose

#### Application Workflow During Containerization
![Dev-Workflow](https://github.com/nirdeshkumar02/Docker-Conceptual-Project/blob/master/Application_Workflow_During_Containerization.png)

Now, You are going to use application inside docker container using docker compose, For that You don't need to provide the localhost mongo url. You can Replace it with the name of container name which will run mongodb in container for you. 
For Refrence take a look in server.js file. 

Create a Dockerfile for your application.

#### To start the application

Step 1: Build Image of Application then start mongodb and mongo-express

    docker-compose -f docker-compose.yaml up
    
_You can access the mongo-express under localhost:8080 from your browser_
    
Step 2: in mongo-express UI - create a new database "my-db"

Step 3: in mongo-express UI - create a new collection "users" in the database "my-db"       
    
Step 4: access the nodejs application from browser 

    `http://localhost:3000`
