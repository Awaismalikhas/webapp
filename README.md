


# Web Application Deployment with Jenkins and Docker

This project demonstrates how to deploy a simple Python Flask web application using Jenkins and Docker. The Flask application is containerized using Docker and the deployment is managed via Jenkins pipeline.

## Prerequisites

- Docker installed on the host machine
- Jenkins installed and set up with the necessary plugins
- A Docker Hub account for pushing images
- Flask library installed

## Project Structure

```
├── Dockerfile
├── Jenkinsfile
├── app.py
├── requirements.txt
```

### Files Description

1. **Dockerfile**
   - Defines a Docker image that uses the Ubuntu 20.04 base image.
   - Installs Python 3 and Flask.
   - Copies the application code (`app.py`) into the Docker image.
   - Runs the Flask application on port `8000`.

2. **Jenkinsfile**
   - A declarative Jenkins pipeline that defines four stages:
     - **Code**: Clones the code from a GitHub repository.
     - **Build**: Builds a Docker image for the Flask app.
     - **Push to Docker Hub**: Tags and pushes the built Docker image to Docker Hub using credentials.
     - **Deploy**: Deploys the Docker container to run the Flask app on port `8000`.

3. **app.py**
   - A simple Python Flask web application that responds with basic messages at two routes:
     - `/`: Displays "Welcome!" message.
     - `/how are you`: Responds with "I am good, how about you?"

4. **requirements.txt**
   - Contains the Flask dependency for the Python application.

## Getting Started

### 1. Build and Run Locally

You can build and run the Flask app locally using Docker:

```bash
# Build Docker image
docker build -t my-web-app .

# Run the container
docker run -d -p 8000:8000 my-web-app
```

Access the web application at: `http://localhost:8000`

### 2. Jenkins Pipeline Setup

1. **Code Stage**: Jenkins will clone the code from a GitHub repository.

2. **Build Stage**: Jenkins will build a Docker image from the Dockerfile.

3. **Push to Docker Hub Stage**: Jenkins will push the built image to your Docker Hub repository using the credentials specified in Jenkins.

4. **Deploy Stage**: Jenkins will run the Docker container, exposing it on port 8000.

### Jenkins Configuration

Make sure to configure the following in Jenkins:

- **Docker Hub credentials**: Create a new Jenkins credential with ID `dockerHUb` that stores your Docker Hub username and password.
- **GitHub repository**: Replace the Git URL in the Jenkinsfile with your own repository if necessary.

## Flask Application

The application has the following routes:

- `/`: Displays a welcome message.
- `/how are you`: Responds with a message.

## Docker Hub

Once the image is built, it is pushed to Docker Hub with the tag `my-web-app:latest`.

You can pull and run the image from Docker Hub as follows:

```bash
docker pull <dockerHubUser>/my-web-app:latest
docker run -d -p 8000:8000 <dockerHubUser>/my-web-app:latest
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
