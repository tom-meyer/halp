### Logging miscellanea

See how big the log is for a container:

    docker inspect --format='{{.LogPath}}' nethermind

Limit the size and do log rotation for a container:

    docker run --log-driver json-file --log-opt max-size=10m alpine echo derp

`json-file` is the default log driver but max-size is -1 by default. Details [here](https://docs.docker.com/config/containers/logging/json-file/). Note there are all sorts of log drivers.


### Good pattern for long running containers

* Use `--log-opt` for controlling size and rotation.
* Use `--restart always` to keep the container up across daemon or system restarts.


### Persistant interactive container

    docker create -it --dns 1.1.1.1 --name playground bash
    docker start -ai playground

Notes:
- The `-it` argument for docker create is super important. Without it, there is no docker start invocation that will attach to the container.
- If volumes are needed, add `-v ...` on the docker create
- Some images might need a resonable entry point, eg `--entrypoint /bin/bash`

### --format=???

Print available keys:

    docker images --format='{{json .}}'
    
Alternatively, some man pages documents the keys:

    man docker-volume-ls

### --filter=???

The --help output doesn't include the available filters. Man pages do though (mostly)!

    man docker-plugin-ls
    man docker-images   # no filters mentioned here
    man docker-image-ls # filters documented (I guess since this is prefered over `docker images`) 

### Dockerfile apt-get

https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#run

      RUN apt-get update && apt-get install -y \
          curl \
       && rm -rf /var/lib/apt/lists/*

### Post-install things

    sudo systemctl enable docker  # yum on amazonlinux doesn't do this
    sudo usermod -aG docker ec2-user

### Plugins miscellanea

* A plugin is a containerized driver binary that communicates with the docker daemon via a driver protocol through a unix socket
* Docker volume driver protocol: https://docs.docker.com/engine/extend/plugins_volume/#volume-plugin-protocol
* `curl` can be used to speak the protocol, see https://docs.docker.com/engine/extend/#debugging-plugins
* `docker plugin enable PLUGIN` creates the actual container and runs the driver binary
* A good example of a volume driver: https://github.com/vieux/docker-volume-sshfs
* Example commands below use `/usr/bin/runc` excutable, but on amazon linux the binary is called `docker-runc`.

List plugin containers:

      sudo runc --root /run/docker/runtime-runc/plugins.moby list

Get a shell within a conatainer:

      sudo runc --root /run/docker/runtime-runc/plugins.moby exec -t 1d512ea36285f9ab86f526aa76d1d11d0a1c6e4ea976b2e4e6e85a5b0f2c664d sh

See plugin stdout and stderr in the docker daemon logs:

      journalctl -n 10 -fu docker.service

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
