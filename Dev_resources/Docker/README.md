# Docker 101

**Docker image**: Conponent (OS, library, etc) encapsulated with its configuration in order to instanciate one of more containers.
**Docker container**: Instance of a docker image, running on a Docker client.

Container are designed to run a specific task: When an application finish its executions (or when it crashed), docker will close the container.

## Docker Container commands

### Start a container
#### 1. Start a simple container
With this command, docker will start a container. If the container doesn't exists yet, it will download it from the docker hub (This only happen the first time a container is run).
```Python
# Here we'll run a NodeJs container
docker run -d nodejs
```
The `-d` parameter means "detached": The container is run in the background, you won't see its logs appearing on your console.

#### 2. Starting in interactive mode
Some application requires to get inputs from the command line. However, by default, docker start in non-interactive mode. To **start in interactive mode**, add `-i` to the run command. And to show the commands prompted by your application, you need to **start in terminal mode** with the `-it` parameter:

```Python
# Run in interactive mode (no prompt allowed for the appplication, but interactiond are allowed)
docker run -i nodejs

# Run in interactive-terminal mode (application's prompt and interactions are allowed)
docker run -it nodejs
```
Now, you can type your command direclty to the app currently runnin, as if the app was running direclty in your console.

#### 3. Specifying an image version
You can **specify the desired version** of a image by adding a version tag:
```Python
docker run -d nodejs:14.11.0-strech
# Find tags of an image on: https://hub.docker.com/_/node?tab=description
```

#### 4. Port forwarding
Inside a Docker host, a docker container has an IP:Port. However, this IP:Port is local to the Docker host: it can't be used to acces to the container from internet. The Docker host has an IP:Port accessible from the internet. 

To give access to a container access to internet, we need to **link the Docker Host IP to the internal docker container IP**. And actually, IP are already connected. We just have to **map the ports**:

```Python
docker run -p 80:5000 nodejs
```

In this example, *80* is the outside port (the Docker Host port), while *5000* is the inside port (the container port inside the docker host). The outisde port **must be free**: If another container is using it, you can't use it again ! You have to choose another port.

#### 5. Volume mapping
By default, inside a docker container, the file stored/created will be remove once the container is closed. This is annoying, especially for databases ! Hopefully, you can map specific folder from inside the container to ouside. So that the data stored in this folder is constantly copied outside.

##### With other folder:
In this example, a directory was created in the Docker Host, and mapped to a folder inside the Docker container:
```Python
docker run -v /my/oustide/dir:/an/inside/dir nodejs
```

##### With other volume:
Here, we specify a volume name that will be created under `var/lib/docker/volumes/` on the Docker Host.
```Python
docker run -v data_volume:/an/inside/dir nodejs
```

You can also create a volume first, and then use it during the *run*, with:
```Python
docker volume create data_volume
```

#### 6. Environment Variables

In python, specify an environment variables like this:
```Python
color = os.environ.get('APP_COLOR')
```

And later, you can run a docker container while **specifying the environment variables**:
```Python
docker run -e APP_COLOR=green nodejs
```

#### 7. Networking

**Bridge**: Private internal network, withint a Docker Host. Containers get connected to this network **by default**. Containers can access each others using the internal IP given by the bridge network, if they need. Accessing any of this container from internet required to maps the ports.

```Python
docker run nodejs  # Bridge by default
```

**Host**: The internal network is replaced by the Docker host network: If a container start at port 5000, it will be automatically available from internet through this port.

```Python
docker run nodejs --network=host
```

**None**: Container are not attached to any network. They can't be accessed from internet, nor from other containers inside the same Docker host.

```Python
docker run nodejs --network=none
```

##### Create multiple bridges:
Useful to have two networks within the same Docker Host

```Python
docker network create \
    --driver bridge  # network type
    --subnet 182.18.0.0/16  # subnet
    custom-isolated-network  # network name
```

##### Listing all networks:
```Python
docker network ls
````

##### Built-in DNS server
To connect a container to another one (Eg: A python application to a database), we can use:
 - The internal IP: `mysql.connect(127.0.0.2)`
 - The container name: `mysql.connect(container_name)`
Using container name ensure we connects containers together, even if their ip change between deployments.

### Attach to a container
To see the logs of a currently running container, attach to it
```Python
docker attach container_name
```

### Listing / Getting details about containers
Useful to know the currently executer containers. It provides the list of the names of the container, that we can use later to stop a specific container.
```Python
# List all the running containers
docker ps

# List all the running and previously closed containers
docker ps -a
```

#### Getting a container's details
To get **more details** about a specific container, use:
```Python
docker inspect container_name
```

#### Displaying a container's logs
To get the logs of a container, use:
```Python
docker logs container_name
```

### Stop a container
```Python
docker stop nodejs
```

### Remove a container
To remove a container and clean all used space.
```Python
docker rm nodejs
```

<br>
<hr>
<br>

## Docker Image commands

### Download a docker image
This is an alternative to `docker run`: It will only download a docker image without running it.
```Python
docker pull nodejs
```

### List all images stored locally
List all images downloaded and stored locally. Usefull to later remove these images.
```Python
docker images
```

### Remove a docker image
To remove a docker image and clean all used space.
**Warning**: You must remove all containers using this images before removing it !
```Python
docker rmi nodejs
```

## Execute commands inside running containers

With `docker exec`, you can execute a command inside a docker container.
### Example: Displaying a file in a container
```Python
# container_name is the name of your container.
docker exec container_name cat /etc/hosts
```

<br>
<hr>
<br>

## Containerizing: Creating Docker images from applications

### Step 1: Create a Dockerfile
The *Dockerfile* contains all of the necessary instructions used to setup your application. It contains the dependencies, entry points, etc...

**Exemple for a flask application**:
```Python
# Define which OS should be used to run the application.
FROM Ubuntu 

# RUN instruction give commands to run to the OS
RUN apt-get update 
RUN apt-get install python

RUN pip install flask
RUN pip install flask-mysql

# Copy the source code to this folder
COPY . /opt/source_code 

# Define environment variables
ENV APP_COLOR "green"

# Define the working directory
WORKDIR /root

# Update the entrypoint with "flask" command
ENTRYPOINT FLASK_APP=/opt/source_code/app.py flask run  
```

**Avoid container closing**:
Usefull for application like *Ubuntu*, *nginx*, *mysql*:

```Python
# Examples
CMD command param1
CMD sleep 5

# Real life examples:
CMD nginx
CMD mysql
```

CAPS are instructions, while lowercase ara argument.

### Step 2: Build the image
Build the docker image:
```Python
docker build Dockerfile -t account_name/your_app_name
```

Each build's step is cached, so that if a build fail, the next time you build, docker will start back where the previous build crashed.

### Step 3: Pushing the image
Then push it to the docker hub:
```Python
docker push account_name/your_app_name
```

# Errors:

## Permission denied /var/run/docker.sock
After a fresh install, on trying to connect, this error can apprear:

![https://i.imgur.com/yMgMUS9.png](https://i.imgur.com/yMgMUS9.png)

**To solve it:**
```Python
sudo chmod 666 /var/run/docker.sock
```
