Commands
--------

    lxc launch ubuntu:22.10 rstudio # create and run a container
    lxc list  # list containers on host
    lxc exec mycontainer bash # run bash inside a container


Autostart
---------

By default, containers start on boot. To turn off:

    lxc config set mycontainer boot.autostart false


Install
-------

The easy way is to hold your nose and use snap

    sudo snap install lxd


Install from source
-------------------

TODO


LXC vs LXD
----------

LXC is the low-level engine.

LXD is the modern manager built on top of LXC.

Confusingly, the `lxc` executable is used for the lxd framework (while
the older lxc commands look like `lxc-BLAH`.


AppArmor
--------

There can be a bad combination of AppArmor on the host conflicting with AppArmor in the container (I've seen this with Ubuntu containers so far).

> [38517.177553] audit: type=1400 audit(1776177330.338:2782): apparmor="DENIED" operation="sendmsg" class="file" namespace="root//lxd-mycontainer_<var-snap-lxd-common-lxd>" profile="rsyslogd" name="/run/systemd/journal/dev-log" pid=6123 comm="systemd-journal" requested_mask="r" denied_mask="r" fsuid=1000000 ouid=1000000

The fix is to loosen up the confinement inside the container:

    # Get a root shell
    lxc exec mycontainer -- bash
    
    # Inside the container:
    mkdir -p /etc/apparmor.d/local
    tee -a /etc/apparmor.d/local/usr.sbin.rsyslogd <<EOF
    # Allow rsyslog/systemd-journal to send logs to the journal socket
    /run/systemd/journal/dev-log rw,
    EOF
    
    apparmor_parser -r /etc/apparmor.d/usr.sbin.rsyslogd  # reparse the main config, which picks up the `local` one
    
    # (C-d) to exit
    
    # Then back on the host, restart the container
    lxc restart mycontainer
