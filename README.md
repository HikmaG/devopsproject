<p align="center">
    <img src="https://user-images.githubusercontent.com/62269745/174906065-7bb63e14-879a-4740-849c-0821697aeec2.png#gh-light-mode-only" width="40%">
    <img src="https://user-images.githubusercontent.com/62269745/174906068-aad23112-20fe-4ec8-877f-3ee1d9ec0a69.png#gh-dark-mode-only" width="40%">
</p>

# Full-Stack Todo List Application

This repository hosts a full-stack Todo List application designed to allow users to create, manage, and organize their tasks efficiently. The application features a React-based frontend and a Node.js backend, utilizing MongoDB for data persistence.

## Technologies Used

- **Frontend**: React, Material-UI
- **Backend**: Node.js, Express
- **Database**: MongoDB
- **Other Tools**: Vite, React Toastify, Lucide Icons

## Project Structure

The project is divided into two main parts:
- **Frontend**: Located in the `frontend/` directory with its own [README](frontend/README.md).
- **Backend**: Located in the `backend/` directory with its own [README](backend/README.md).

## Features

- Create, view, update, and delete todo items.
- Organize tasks with tags/categories.
- Responsive user interface adaptable to different screen sizes.
- Real-time updates without page reloads.

## Contributing

Contributions are welcome! See the specific README files in the `frontend/` and `backend/` directories for more details on contributing.

## Live Demo

<h4 align="left">Live Preview is available at https://fullstack-todolist-1.onrender.com/</h4>

## Snapshots

<img src="./Frontend/src/assets/home-snapshot.png" alt="home page"/>

# Full Stack To-Do List Application - Docker Documentation
## Setup Instructions

## Prerequisites

Ensure you have the following installed on your system:
Docker, Docker Compose, Git, A text editor (VS Code) 

## Cloning the Repository
git clone repository-url 

cd fullstack-todo-list

## Building and Running the Containers
1) Ensure Docker is running on your machine.    

2) Navigate to the project root directory where docker-compose.yml is located. Create one if not there. 

3) Run the following command to build and start all services:

docker-compose up --build -d

4) Verify that all containers are running:
   
docker ps
6) Open a browser and navigate to:
Frontend: http://localhost:8080

Backend API: http://localhost:3000

MongoDB is running internally on port 27017.

## Stopping the Containers
To stop all running containers 

docker-compose down

To remove volumes and networks

docker-compose down -v

## Network and Security Configurations
## Docker Network

All services are part of a custom network named todo-network.
This allows seamless communication between the frontend, backend, and MongoDB services.

## Exposed Ports
Frontend (Container Port 80) (Host Port 8080)

Backend (Container Port 3000) (Host Port 3000)

MongoDB (Container Port 27017) (Host Port 27017)

## Environment Variables
MongoDB credentials are set using environment variables in docker-compose.yml:

   environment:
    MONGO_INITDB_ROOT_USERNAME: admin
    MONGO_INITDB_ROOT_PASSWORD: password
  
The backend service connects to MongoDB using:

   environment:
    MONGO_URI: mongodb://admin:password@mongo:27017/todo-db?authSource=admin

## Security Measures
MongoDB uses authentication to restrict unauthorized access.

The backend service is configured to only communicate with MongoDB within the internal Docker network.

No unnecessary ports are exposed to the public.

# Troubleshooting Guide
## Docker Daemon Not Running
Error: Cannot connect to the Docker daemon

Solution: Ensure Docker Desktop or the Docker service is running before executing commands.

## Containers Not Communicating
Error: Backend cannot connect to MongoDB.

Solution: Ensure MongoDB is running


docker logs todo-mongo

Check if MongoDB is reachable inside the backend container:

docker exec -it todo-backend bash

ping mongo

## Database Connection Issues
Error: MongoNetworkError: failed to connect to server

Solution: Ensure the correct environment variables are used in docker-compose.yml.

Restart the MongoDB container:

docker-compose restart mongo

## Application Not Loading in Browser 
Solution: 

Check logs for errors and restart:

docker logs todo-frontend 

docker-compose restart frontend

# Container Testing Script
## Testing Backend API
Run the following command to test if the backend is responding: 

curl -X GET http://localhost:3000/api/health

## Testing MongoDB Connection from Backend
Run the following command inside the backend container: 

docker exec -it todo-backend bash -c "node -e 'require(\"mongoose\").connect(process.env.MONGO_URI).then(() => console.log(\"MongoDB Connected\")).catch(err => console.log(err));'"

## Testing Frontend Accessibility
Open your browser and go to http://localhost:8080. The frontend should load the application UI. 

## Testing Container Network Connectivity
Check if backend can communicate with MongoDB: 
docker exec -it todo-backend ping -c 4 mongo