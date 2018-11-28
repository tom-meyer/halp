### check swap

    swapon -s

### Add a 1G swapfile

    dd if=/dev/zero of=/swapfile bs=1G count=1
    chmod 600 /swapfile
    mkswap /swapfile
    swapon /swapfile
