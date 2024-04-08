## demo app - developing with Docker

Here we are cresting user profile app set up with help of : 
- index.html ,javascript and css styling and mongodb for data storage
- nodejs backend with express module
We can start the corresponding application either by using docker or by using docker compose.
### Using Docker
#### To start the application

Step 1: Create docker network
     docker network create mongo-network 

Step 2: start mongodb 

    docker run -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb --net mongo-network mongo    

Step 3: start mongo-express
    
    docker run -d -p 8080:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password --net mongo-network --name mongo-express -e ME_CONFIG_MONGODB_SERVER=mongodb mongo-express   

Step 4: open mongo-express from browser

    http://localhost:8080

Step 5: create `user-account` _db_ and `users` _collection_ in mongo-express


![image](https://github.com/Anushka-92/User_profile_app_using_docker/assets/92269153/8eb5168e-8fea-45fc-a813-d1790a16e7ec)

Step 6: Start your nodejs application locally - go to `app` directory of project 

    cd app
    npm install 
    node server.js
    
Step 7: Access you nodejs application UI from browser

    http://localhost:3000
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------    

### Using Docker Compose

#### To start the application

Step 1: start mongodb and mongo-express

    docker-compose -f docker-compose.yaml up
    
Step 2: in mongo-express UI - create a new database "my-db"

Step 3: in mongo-express UI - create a new collection "users" in the database "my-db"       
    
Step 4: start node server 

    cd app
    npm install
    node server.js
    
Step 5: access the nodejs application from browser 

    http://localhost:3000

#### To build a docker image from the application locally .

    docker build -t my-app:1.0 .       
    
    
### We need to create private repositories usig ECR 
   
For that purpose we need to have AWS CLI installed on our local machine and it need to be congfigured and login successfully through our editor .

After successfully creating repository by clicking on View push commands option present over there we can see :


![image](https://github.com/Anushka-92/User_profile_app_using_docker/assets/92269153/0579832c-f335-4ea5-b955-b9da43156fbb)
 
 
 Inside ECR of AWS we can create upto 1000 tags/versions of same images.
 After we have packaged our appication into docker image and save it into private repository , we need to deploy this into other development server / integration server of other environment , So we can use docker compose application for this 
deployment. 

The server needs to be logged in for private repository like the one that we have created using AWS ECR . 

 
 In order to deploy application we need to have docker-compose file in our direcetory , We can create all 3 containers(mongodb, mongo-express ,my-app ) with following command .
 
 docker-compose -f mongo.yaml up

 
 ![image](https://github.com/Anushka-92/User_profile_app_using_docker/assets/92269153/98c74fcd-a790-46f3-aee0-dec3a1ed2225)

    
    
    
 
