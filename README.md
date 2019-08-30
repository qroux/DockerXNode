# DockerXNode

1) Dockerfile (Docker image Setup)

specify a base image (including npm in this example)

FROM node:alpine

Add local files of the directory with the COPY command(path of the file relativly to the context, desired path in the image)
in this example, we are adding a copy of the package.json file before running npm install command

COPY ./ ./

Install the dependencies

RUN npm install

Default command when the container start running(start the node server by using our start script)

CMD ["npm", "start"]


2) Build the image ( . stands for the context)

Docker build .


3) Tag the container(more handy than using container ids)

docker build -t qroux/docker_node .


4) Maping local port to container ports (Container have its own ports, you have to explicitly map machine ports to container ports)

docker run -p 8080:8080  qroux/docker_node


