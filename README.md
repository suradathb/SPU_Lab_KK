# SPU LAB KK Project - Documentation
 ### 1.Project Structure:
```
project-root/ 
|-- frontend/ 
|   |-- Dockerfile
|   |-- package.json
|   |-- public/
|   |-- src/
|   |   |-- ...
|
|-- backend/ 
|   |-- Dockerfile
|   |-- main.py
|   |-- requirements.txt
|
|-- docker-compose.yml
```
### 2.Frontend Dockerfile('frontend/Dockerfile')
```
# Use an official Node runtime as a parent image
FROM node:14

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install app dependencies
RUN npm install

# Copy the app source code into the container
COPY . .

# Expose port 3000 to the outside world
EXPOSE 3000

# Command to run the application
CMD ["npm", "start"]

```