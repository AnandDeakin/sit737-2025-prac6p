Overview
This project demonstrates how to Dockerize a web application, deploy it using Docker Compose, implement container health checks, and push the image to a Docker registry.

 Requirements
Git

Visual Studio Code

Node.js

Docker
 Steps Followed
1. Install Docker
Download and install Docker from https://www.docker.com/products/docker-desktop/.

2. Clone the Application
bash
Copy
Edit
git clone https://github.com/your-username/your-project-name.git
cd your-project-name
(Or use your own app.)

3. Create a Dockerfile
Created a Dockerfile with the following content:

Dockerfile
Copy
Edit
FROM node:20
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
4. Build the Docker Image
bash
Copy
Edit
docker build -t your-app-name .
5. Create Docker Compose File
Created docker-compose.yml:

yaml
Copy
Edit
version: '3.8'

services:
  web:
    build: .
    ports:
      - "3000:3000"
    restart: always
6. Start Docker Compose Environment
bash
Copy
Edit
docker-compose up
7. Test the Application
Open a browser and navigate to http://localhost:3000 to see the application running.

8. Push the Docker Image to Docker Hub
bash
Copy
Edit
docker login
docker tag your-app-name your-dockerhub-username/your-app-name
docker push your-dockerhub-username/your-app-name
9. health Check
Updated docker-compose.yml with health check:

yaml
Copy
Edit
version: '3.8'

services:
  web:
    build: .
    ports:
      - "3000:3000"
    restart: always
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:3000"]
      interval: 30s
      timeout: 10s
      retries: 3
