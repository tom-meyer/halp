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
