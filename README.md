# DockerXNode

# I) Dockerfile (Docker image Setup)


1. specify a base image (including npm in this example)

FROM node:alpine

2. Add local files of the directory with the COPY command(path of the file relativly to the context, desired path in the image). In this example, we are adding a copy of the package.json file before running npm install command

COPY ./ ./

3. Install the dependencies

RUN npm install

4. Default command when the container start running(start the node server by using our start script)

CMD ["npm", "start"]



# II) Build the image ( . stands for the context)

Docker build .



# III) Tag the container(more handy than using container ids)

docker build -t qroux/docker_node .



# IV) Maping local port to container ports (Container have its own ports, you have to explicitly map machine ports to container ports)

docker run -p 8080:8080  qroux/docker_node

# Optionnal: command to override the initial command ("npm start") and launch the shell instead

docker run -it  qroux/docker_node sh



