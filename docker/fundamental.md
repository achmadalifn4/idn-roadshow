# Docker

# Install Docker
## Setup Docker Apt Repository
```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

## Install The Docker Packages
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

# Container Management
Create and Start a Container from an Image.
```
docker run -d -p 80:80 nginx
```
Display the List of Active Containers with details like ID, image, status, ports, etc.
```
docker ps
```
Stop a Running Container.
```
docker stop mycontainer
```
Restart a Stopped Container
```
docker restart mycontainer
```
Remove a Specific Container.
```
docker rm mycontainer
```

# Image Management
Downloading Images.
```
docker pull nginx
```
Display the List of Images.
```
docker images
```
Detailed List of the Image Layers and Their Changes.
```
docker history nginx
```
Remove a Specific Docker Image
```
docker rmi myimage
```
# Network Management
Displays the list of networks with details like ID, name, driver, etc.
```
docker network ls
```
Create a new Docker network.
```
docker network create --driver bridge mynetwork
```
Connect a container to a Docker network.
```
docker network connect mynetwork mycontainer
```
Displays detailed information about the network, like connected containers, options, IP, etc.
```
docker network inspect mynetwork
```
# Volume Management
Create a new Docker volume for persistent storage.
```
docker volume create myvolume 
```
Displays the list of volumes with details like name, driver, etc.
```
docker volume ls 
```
Attach a volume to a container for persistent storage.
```
docker run -v myvolume:/data nginx 
```
Remove a specific Docker volume.
```
docker volume rm myvolume 
```
# Monitoring and Log
Displays output logs for the specified container.
```
docker logs mycontainer 
```
Provides a real-time overview of resource usage for all running containers.
```
docker stats 
```
Opens an interactive shell in the container, if bash is used as command.
```
docker exec -it mycontainer bash 
```
Displays detailed JSON with full information about the container, including network status, mounted volumes, configuration settings, etc.
```
docker inspect mycontainer
```
# Dockerfile
Create the docker-compose.yml file.
```
FROM node:20-bullseye-slim
WORKDIR /app
ADD . /app/
RUN apt update && \
    apt install -y iputils-ping traceroute whois libsocket-getaddrinfo-perl && \
    ln -s /bin/ping /usr/bin/ping && \
    apt clean && rm -rf /var/lib/apt/lists/*
RUN npm install 
EXPOSE 3000
CMD ["npm", "start"]
```
Then build image.
```
docker build -t myimage .
```
