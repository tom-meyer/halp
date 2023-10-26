Barebones examples. [Unit file reference][1] for more.


### Systemd unit for docker container run in the foreground

Runs the continer in the foreground (no `-d`). Limits the logging to a small
file, as journald captures output.

    [Unit]
    Description=My App
    Requires=docker.service
    After=docker.service

    [Service]
    ExecStart=/usr/bin/docker run \
        --rm --name my-app \
        --log-driver json-file --log-opt max-size=1m  \
        my-app:active
    Restart=always


    [Install]
    WantedBy=multi-user.target


### Systemd unit for docker compose (or background containers)

Here the ExecStart command exits after starting the containers. ExecStop is
required to shut things down.

This same pattern could be used to run a single container using `docker run -d ...`
for the ExecStart, and `docker stop <NAME>` for the ExecStop.

    [Unit]
    Description=My App
    Requires=docker.service
    After=docker.service

    [Service]
    ExecStart=/usr/local/bin/docker-compose -f /var/myapp/docker-compose.yml up
    ExecStop=/usr/local/bin/docker-compose -f /var/myapp/docker-compose.yml down -v

    [Install]
    WantedBy=multi-user.target


### Use `service` or `systemctl`?

The `service` command is a wrapper that will call `systemctl` or an init.d
script, as appropriate for the system. This is an init system helper that
some distros provide (Ubuntu/Red Hat/Fedora).

The `systemctl` the script provided by systemd.

See it in action:

    systemctl status NetworkManager.service
    service NetworkManager status

[1]: https://www.freedesktop.org/software/systemd/man/systemd.unit.html
