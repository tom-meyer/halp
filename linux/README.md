### Charge threshold

Set the upper limit:

    echo -n 85 > /sys/class/power_supply/BAT0/charge_control_end_threshold

On my Fedora machine, I kept getting "write error" with the above command, and
it turned the error was due to the current charge level being above what I was
trying to set.


### Users

    adduser # use this. helpful promts for a human
    useradd # low level for scripts and such


### Groups

    sudo usermod -aG lxd tom # add to group
    newgrp - lxd # spawn a new bash shell with group change applied


### iptables

    iptables -L -n -v

Maybe create a iptables README?

    iptables -I <chain> # insert rule at start of chain
    iptables -A <chain> # insert rule at end of chain


### Inspecting open ports

    netstat -nltp
    lsof -nPp <PID> | grep LISTEN # by pid (can be multiple pids separated by commas)


### Resize XFS

Check stuff:

    sudo lsblk
    df -hT /

To resize a filesystem on a partition, grow the partition before resizing:

    sudo growpart /dev/nvme0n1 1
    sudo xfs_growfs -d /

To resize a filesystem on an entire device (eg nvme1n1):

    sudo xfs_growfs -d /mnt/bigdisk

See [AWS guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/recognize-expanded-volume-linux.html) for more info.


### check swap

    swapon -s

### Add a 1G swapfile

    dd if=/dev/zero of=/swapfile bs=1G count=1
    chmod 600 /swapfile
    mkswap /swapfile
    swapon /swapfile

### Check for deep sleep support

    $ cat /sys/power/mem_sleep 
    s2idle [deep]

The thing in brackets is the mode that is enabled. If `deep` isn't present, the kernel doesn't support deep sleep.
