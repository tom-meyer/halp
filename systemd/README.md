### Use `service` or `systemctl`?

The `service` command is a wrapper that will call `systemctl` or an init.d
script, as appropriate for the system. This is an init system helper that
some distros provide (Ubuntu/Red Hat/Fedora).

The `systemctl` the script provided by systemd.

See it in action:

    systemctl status NetworkManager.service
    service NetworkManager status

### Systemd unit for docker compose

Barebones example. [Unit file reference][1] for more.

    [Unit]
    Description=My App
    Requires=docker.service
    After=docker.service

    [Service]
    ExecStart=/usr/local/bin/docker-compose -f /var/myapp/docker-compose.yml up
    ExecStop=/usr/local/bin/docker-compose -f /var/myapp/docker-compose.yml down -v

    [Install]
    WantedBy=multi-user.target
    
[1]: https://www.freedesktop.org/software/systemd/man/systemd.unit.html
