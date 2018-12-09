### Escape sequences

    ~.   # kill connection
    ~C   # open command line
    ~^Z  # suspend
    ~#   # list forwarded connections

### Tunnel to a socket

    ssh -L localhost:9999:/var/run/docker.sock mydockerhost.net -N &
    DOCKER_HOST=localhost:9999 docker ps
