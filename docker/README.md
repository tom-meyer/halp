### Show available format names for any command

Print each line as json, and look at the keys:

      docker images --format='{{json .}}'

### Dockerfile apt-get

https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#run

      RUN apt-get update && apt-get install -y \
          curl \
       && rm -rf /var/lib/apt/lists/*
 
### Ubuntu setup

Abbreviated instructions from the offical documentation:

- https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/
- https://docs.docker.com/compose/install/#install-compose

      apt-get update
      apt-get install linux-image-extra-$(uname -r) linux-image-extra-virtual
      apt-get install apt-transport-https ca-certificates curl software-properties-common
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
      add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
      apt-get update
      apt-get install docker-ce
      # Go find out what version to use in the next line: https://github.com/docker/compose/releases
      curl -L https://github.com/docker/compose/releases/download/9.99.9/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
      curl http://localhost:15672/cli/rabbchmod +x /usr/local/bin/docker-compose

### Tunnel the docker socket

    ssh -L localhost:9999:/var/run/docker.sock mydockerhost.net -N &
    DOCKER_HOST=localhost:9999 docker ps
