# SPU LAB KK Project - Documentation

### Action Git Step Clone
CMD : **git clone https://github.com/suradathb/SPU_Lab_KK.git name**

### Test before building to create Docker image 
```
cd <projectname>/frontend
npm install
npm start

And

cd <projectname>/backend/app
uvicorn main:app --reload

```

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
### 3.Backend Dockerfile (backend/Dockerfile):
```
# Use the official Python image
FROM python:3.9

# Set the working directory in the container
WORKDIR /app

# Copy the requirements file into the container
COPY requirements.txt .

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application code into the container
COPY . .

# Expose port 8000 to the outside world
EXPOSE 8000

# Command to run the application
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```
### 4.Backend requirements.txt (backend/requirements.txt):
```
fastapi>=0.68.0,<0.69.0
pydantic>=1.8.0,<2.0.3
uvicorn>=0.15.0,<0.16.0
python-multipart
et-xmlfile
pandas
openpyxl
aiofiles
```
### 5.Docker Compose (docker-compose.yml):
```
version: '3'
services:
  frontend:
    build:
      context: ./frontend
    ports:
      - "3000:3000"
    depends_on:
      - backend

  backend:
    build:
      context: ./backend
    ports:
      - "8000:8000"
```
### Usage:
1. Make sure you have Docker and Docker Compose installed.
2. Navigate to the project root in the terminal.
3. Run **docker-compose up --build to build** and start both containers.
Access the React app at http://localhost:3000 and the FastAPI app at http://localhost:8000.



