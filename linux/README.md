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
