#### Docker Commands

- How to create a DockerFile
- Push Docker to DockerHub;
- Pull Docker from DockerHub;
- Examples.

#### How to create a DockerFile
Docker have many Tags to use and each one is a specific type.

FROM
The base image for building a new image. This command must be on top of the dockerfile.

MAINTAINER
Optional, it contains the name of the maintainer of the image.

RUN
Used to execute a command during the build process of the docker image.

ADD
Copy a file from the host machine to the new docker image. There is an option to use an URL for the file, docker will then download that file to the destination directory.

ENV
Define an environment variable.

CMD
Used for executing commands when we build a new container from the docker image.

ENTRYPOINT
Define the default command that will be executed when the container is running.

WORKDIR
This is directive for CMD command to be executed.

USER
Set the user or UID for the container created with the image.

VOLUME
Enable access/linked directory between the container and the host machine.

Now let's stat to create our first dockerfile with dotnetcore and chrome.

Example:
Here we are using a dotnecore2.2 base image, and installing chrome(lastest version) also setting our work directory.

    FROM mcr.microsoft.com/dotnet/core/sdk:2.2
    
    RUN apt-get update && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    hicolor-icon-theme \
    libcanberra-gtk* \
    libgl1-mesa-dri \
    libgl1-mesa-glx \
    libpango1.0-0 \
    libpulse0 \
    libv4l-0 \
    fonts-symbola \
    --no-install-recommends \
    && curl -sSL https://dl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && echo "deb [arch=amd64] https://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google.list \
    && apt-get update && apt-get install -y \
    google-chrome-stable \
    --no-install-recommends \
    && apt-get purge --auto-remove -y curl \
    && rm -rf /var/lib/apt/lists/*
    
    WORKDIR /usr/src/app
	

#### Push Docker to DockerHub

Lets build a Dockerfile, please open a folder where is ur dockerfile and:
containerName inst a "dockerfile", is the new name ex: dotnetcore

    docker build -t containerName .

Now we have a Dockerfile lets Push then to DockerHub!
First we need to give a tag name.

Lets check docker images inside my computer

    docker images

Take a ID from "docker images" and give a tag 

    docker tag ID usuario_from_dockerHub/reponame:tagname(ex: 1.0)
Example: docker tag 949494949 sayoan/dotnetcore_22_chrome:1.0

Push a image to dockerhub

    docker push usuario/reponame:tagname


#### Pull Docker from DockerHub

    docker pull sayoan/dotnetcore_22_chrome:1.0
Check the docker IMAGE ID

    docker images

Now lets run the container

    docker run -t -i IMAGE_ID /bin/bash

We are inside container \o/

#### Examples

docker kill ID //matar

docker exec -it [container-id] bash

docker ps -a 


