# DockerXNode

# I) In the project directory: Create a Dockerfile (Docker image Setup/ Dockerfile content).
Fill it with base image(FROM), copy localfile into the image(COPY), run some command to install dependencies(RUN), setup initial command when the Container start(CMD


1. specify a base image (including npm in this example)

FROM node:alpine

2. Add local files of the directory with the COPY command(path of the file relativly to the context, desired path in the image). In this example, we are adding a copy of the package.json file before running npm install command

COPY ./ ./usr/app

3. Install the dependencies

RUN npm install

4. Default command when the container start running(start the node server by using our start script)

CMD ["npm", "start"]



# II) In the terminal: Build the image ( . stands for the context)

Docker build .



# III) In the terminal: Tag the container created(more handy than using container ids)

docker build -t qroux/docker_node .



# IV) In the terminal: Maping local port to container ports (Container have its own ports, you have to explicitly map machine ports to container ports)

docker run -p 8080:8080  qroux/docker_node

# Optionnal: In the terminal: command to override the initial command ("npm start") and launch the shell instead

docker run -it  qroux/docker_node sh

# Optionnal: when rebuilding after a minor change, it's better to split the COPY instruction into several instruction in order to let docker use the cache insted of re-running npm install.

In this example, we only need the package.json to run the "RUN npm install".

instead of:
COPY ./ ./usr/app

use:
COPY ./package.json ./usr/app
RUN npm install
COPY ./ ./usr/app



