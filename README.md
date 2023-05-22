<p align="right">
    <img src="https://github.com/AnastasiaTECHWRITER/create-and-deploy-image/assets/134202043/6559f7e9-2e21-4fb0-9a96-d0ff531b8ed8" width="55" height="55">
</p>

# Create and deploy image
This article contains the instructions on how to prepare the container image file and your IT infrastructure, and then deploy this image to the **Kubernetes** tool. In this scenario, we assume working with the **ExampleApp** that listens to the **8800** port. 
<details>
<summary>What is Kubernetes?</summary>
<br>
Kubernetes is an open-source container-orchestration tool designed by Google. It allows running your applications across on-site deployments and public clouds, and supports hybrid scenarios. Read the following Google documentation article to learn more about Kubernetes: <p><a href="https://cloud.google.com/learn/what-is-kubernetes">What is Kubernetes?</a></p> .
</details>
Follow the steps below to upload the image to Kubernetes.

## 1. Install Docker
Install Docker Desktop, depending on your OS:

**For Windows:**
1. Make sure you meet the [installation requirements](https://docs.docker.com/desktop/install/windows-install/#system-requirements).
2. [Download](https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe) Docker Desktop for Windows.
3. Follow the [installation prompts](https://docs.docker.com/desktop/install/windows-install/#install-docker-desktop-on-windows) (both: interactive and command prompt deployment scenario are supported).

**For Linux:**
1. Make sure you meet the [installation requirements](https://docs.docker.com/desktop/install/linux-install/#system-requirements).
2. Download the distributive and follow the installation prompts, depending on your Linux distribution:
 - [Debian](https://docs.docker.com/desktop/install/debian/)
 - [Fedora](https://docs.docker.com/desktop/install/fedora/)
 - [Ubunty](https://docs.docker.com/desktop/install/ubuntu/)
 - [Arch](https://docs.docker.com/desktop/install/archlinux/)

## 2. Create catalogs
Create the directories where the ExampleApp code, Docker resources and the Dockerfile will be located. You can keep all resources in the root directory, however, the example shows the structure with a dedicated subdirectory for each resource:
Run the ```mkdir``` command:

```
mkdir quickstart_docker
mkdir quickstart_docker/application
mkdir quickstart_docker/docker
mkdir quickstart_docker/docker/application
```
where:

the ```quickstart_docker/``` is the root project directory;

the ```/application``` directory contains ExampleApp code;

the ```/docker``` directory contains Docker resources;

and the ```/docker/application``` is a directory for the Dockerfile. A **Dockerfile** is a text document with all commands a user could call to assemble an image. Read the [Docker Docs article](https://docs.docker.com/engine/reference/builder/) to learn more about Dockerfile.

## 3. Prepare application
1. Copy the **application.py** file (ExampleApp) to the ```/application``` directory you created on the step 2.
2. From **application.py**, run a http server with the following parameters:
```
import http.server
import socketserver

PORT = 8000

Handler = http.server.SimpleHTTPRequestHandler

httpd = socketserver.TCPServer(("", PORT), Handler)

print("serving at port", PORT)
httpd.serve_forever()
```

## 4. Prepare Dockerfile
Docker can build images automatically by reading the instructions from a Dockerfile. 
To prepare your Dockerfile, do the following:
1. Create the **Dockerfile** for the ExampleApp in the ```/docker/application``` directory you created on the step 2. 
2. Edit the file as follows:

```
# Use base image from the registry
FROM python:3.5

# Set the working directory to /app
WORKDIR /app

# Copy the 'application' directory contents into the container at /app
COPY ./application /app

# Make port 8000 available to the world outside this container
EXPOSE 8000

# Execute 'python /app/application.py' when container launches
CMD ["python", "/app/application.py"]
```
3. Save your edits.

## 5. Build new container image
In terminal, run the following command:
```
docker build . -f-docker/application/Dockerfile -t exampleapp
```
where
``` -``` is a working directory, build context; 

```-f docker/application/Dockerfile``` is the path to your Dockerfile;

```-t exampleapp``` - applies a tag to the container image which identifies your image version.

Read the [Docker Docs article](https://docs.docker.com/engine/reference/builder/) to learn more about image assembling.

## 6. Review images list
Finally, review the list of the available images and identify your container image file. 

For that, run the following command in terminal:
```$ docker images```

The default docker images will show all top level images, their repository and tags, and their size:
| REPOSITORY| TAG | IMAGE ID | CREATED | SIZE |
|--|--|--|--|--|
| exampleapp | latest | 83wse0edc28a | 2 seconds ago | 153MB |
| python | 3.6 | 05sob8636w3f | 6 weeks ago| 153MB |

**Now you can pull the image to the repository.**
# What is next?
- Review the following [Docker Docs article](https://docs.docker.com/get-started/orchestration/) to learn more about deployment and orchestration in **Kubernetes**.
- For any feedback about this article, feel free to contact the Technical Documentation team at <technical-writers@domainname.com>.
