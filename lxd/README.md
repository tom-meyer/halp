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
