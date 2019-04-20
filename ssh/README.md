### Escape sequences

    ~.   # kill connection
    ~C   # open command line
    ~^Z  # suspend
    ~#   # list forwarded connections

### Tunnel to a socket

    ssh -L localhost:9999:/var/run/docker.sock mydockerhost.net -N &
    DOCKER_HOST=localhost:9999 docker ps

### Shut up and keygen

    ssh-keygen -t rsa -b 4096 -C mykey -N '' -f ./my_id_rsa

The above generates a key pair, see `openssl/README.md` for generating just a private key.

### VPN

From https://hackertarget.com/ssh-examples-tunnels/

(This is a work in progress)

On the jump box:

> PermitRootLogin yes
> PermitTunnel yes

    ip addr add 10.10.10.10/32 peer 10.10.10.2 dev tun0
    ip link set tun0 up
    echo 1 > /proc/sys/net/ipv4/ip_forward
    iptables -t nat -A POSTROUTING -s 10.10.10.2 -o enp7s0 -j MASQUERADE

On localhost (routes to a single host, 1.2.3.4 -- adjust as needed):

    ip addr add 10.10.10.2/32 peer 10.10.10.10 dev tun0
    ip link set tun0 up
    ip route add 1.2.3.4/32 dev tun0
    ssh -v -w any root@jump

Tear down:

    ip route del 1.2.3.4/32 dev tun0
    ip link set tun0 down
