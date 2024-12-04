## Multi-Container Docker Application with CI/CD: Calculator App Project

#### Complete Project Instructions: [DevOps Foundations Course/Project](https://github.com/shiftkey-labs/DevOps-Foundations-Course/tree/master/Project)

#### Submission by - **CARMAHN MCCALLA**

### Project Overview

- **Brief project description:** What is the purpose of your application?

 - The application is a simple calculator with a React app in the frontend for user input, and a python/flash api in the backend that processes the calculations. 

- The idea of the project is to package the components inside of Docker containers to make deployment more effiencent. Additionally, a CI/CD pipeline is set up through Github Actions to ensure automatic updates occur when changes are made to the codebase. 


- **Which files are you implmenting? and why?:**

- Dockerfiles for the frontend & backend:
    - frontend: creates the React app container which provides an interface for the users to type in calculations
    - backend: creates the container for the backend  Python API which processes the calculations inputted
- docker-compose.yml: connects the backend and frontend of the application with multi-containerization  
- github-actions.yml: automates the process of build/deployment for the CI/CD pipieline 


- _**Any other explanations for personal note taking.**_

- chose to do the pipline through Github Actions as I find the platform easier to work with 

***

### Docker Implementation

**Explain your Dockerfiles:**

- **Backend Dockerfile** (Python API):
    - Here please explain the `Dockerfile` created for the Python Backend API. 
    - This can be a simple explanation which serves as a reference guide, or revision to you when read back the readme in future. 

The purpose of this file is to set up the backend environment for the application. The API is written in Python using Flask (a python framework). The duties of this file are:
- use the base image python:3.9-slim to set up environment
- set the working directory & copy code into the container
- install the dependencies needed to run the backend of the app & make accessible on port 5001

***
- **Frontend Dockerfile** (React App):
    - This file sets up the React app in the frontend. It also installs dependencies, copies code into the container, and sets the working directory. 
    - use the base image node:14-alpine to set up environment
    - builds the app using npm (Node.js Package Manager) 
    - is accessible on port 3000

**Use this section to document your choices and steps for building the Docker images.**
<!-- Include explanation here EXPLAIN THE STEPS AND LINES YOU PUT INTO CMD LINE TO BUILD IMGS-->
- To build the images, I made one image for the frontend (running React on port 3000) and one for the backend (runnning Python Flask on port 5001, which was changed from 5000 due to troubleshooting).
- BUILDING FRONTEND IMAGE (COMMANDS):
    - FIRST: navigate to frontend folder in directory
    - docker build -t frontend-image .
    - docker run -p 3000:3000 frontend-image
- BUILDING BACKEND IMAGE (COMMANDS):
    - FIRST: navigate to backend folder in directory
    - docker build -t backend-image .
    - docker run -p 5001:5001 backend-image
- DOCKER COMPOSE
    - FIRST: navigate to Project folder in directory
    - docker-compose up --build

- When I ran those commands, they both ran smoothly and were accesible from their respective browser urls; BACKEND:(http://localhost:5001/api/test) & FRONTEND: (http://localhost:3000)
- The calculator app is working; tested add(), multiply(), subtract(), and division() funtionality.

### Docker Compose YAML Configuration

**Break down your `docker-compose.yml` file:**

- **Services:** List the services defined. What do they represent?
- **Networking:** How do the services communicate with each other?
- **Volumes:** Did you use any volume mounts for persistent data?
- **Environment Variables:** Did you define any environment variables for configuration? 

**Use this section to explain how your services interact and are configured within `docker-compose.yml`.**

- There are 2 defined services; frontend & backend. 
    - frontend: represents the React app, which is exposed on port 3000 from the dockerfile in its directory
    - backend:  represents the Flask api, which is exposed on port 5001 from the dockerfile in its directory

- I used a bridge network for the services to communicate through docker-compose, defined as 'calcapp-network'.

- no, I did not use volume mounts 

- no, I did not use environment variables here

### CI/CD Pipeline (YAML Configuration)

**Explain your CI/CD pipeline:**

- What triggers the pipeline (e.g., push to main branch)?
- What are the different stages (build, test, deploy)?
- How are Docker images built and pushed to a registry (if applicable)?

**Use this section to document your automated build and deployment process.**

- everytime new code is pushed to the master branch of the repo, the pipeline should be triggered. 
- build stage builds the frontend and backend images
- test stage ensures both parts of the application (front/backend) are working as they should be; npm test for the front and pytest for the back


<!-- NOTE: It is not compulsory to include detailed explanations, writing succint concise points would also sufice. Make sure maintain readability and clarity. -->


### CI/CD Pipeline (YAML Configuration)

**Simply explain your CI/CD pipeline:**

- What triggers the pipeline (e.g., push to main branch)?
- What are the different stages (build, test, deploy)?
- How are Docker images built and pushed to a registry?

**Use this section to document your automated build, and docker process.**

- explained above


### Assumptions

- List any assumptions you made while creating the Dockerfiles, `docker-compose.yml`, or CI/CD pipeline. 

- I assumed that I wouldn't need any extra troubleshooting with Docker, since I;'ve already used it before on the weekly tasks so i had Docker Hub & related dependencies installed
- I assumed that the pipline would work just as well using secret variables instead of ENV ones 
- I assumed that the app code (front & back end) was funtional
- I assumed the dockerfile setup would be similar to the week 2 activity set up 

### Lessons Learned

- What challenges did you encounter while working with Docker and CI/CD?
   
- What did you learn about containerization and automation?

**Use this section to reflect on your experience and learnings when implementing this project.**

 - I forgot to close out of my tester windows when trying to run the app; sometimes I would get the error that the ports were already in use and I had to troubleshoot to figure out why 
    - I had to do additional research when figuring out how to define networks in the docker compose files, especially using this documentation: https://docs.docker.com/compose/how-tos/networking/ 
    - Sometimes the app frontend would run but the backend calculations were not running and only gave back error; I had to do some reinstalls of flask to make sure it was working 
    - I learned how to properly use docker-compose; I was able to configure an image/container relatiey easily when I was just using "one folder" like in the week2 exercise, but I find it much more concise to bundle the frontend/backend together. 

- The indentation in my github-actions file was off, so I had to correct those to help the pipeline run 


### Future Improvements

- How could you improve your Dockerfiles, `docker-compose.yml`, or CI/CD pipeline? 
- (Optional-Just for personal reflection) Are there any additional functionalities you would like to consider for the calculator application to crate more stages in the CI/CD pipeline or add additional configuration in the Dockerfiles?

**Use this section to brainstorm ways to enhance your project.**

- more tests could be added to the pipeline to further prevent errors/ catch them early
- the calculator frontend could have more improved ui, especially with the calculation display & answer (although it'sfine for what it needs to do) 
- also there could be functionality for brackets to do more complex calculations, (ex: 5x5+3 currently gives 8; it does not store operations in progress like a scientific calc would)






<!-- BEST OF LUCK! -->
