##OVERLAY FS

    \#prepare layers
    sudo mkdir -p /var/log.tmpfs
    sudo mount -t tmpfs -o rw,nosuid,nodev,noexec,relatime,size=512m,mode=0775 tmpfs /var/log.tmpfs
    sudo mkdir -p /var/log.tmpfs/upper
    sudo mkdir -p /var/log.tmpfs/work
    sudo chown -R root:syslog /var/log.tmpfs
    sudo chmod -R u=rwX,g=rwX,o=rX /var/log.tmpfs

    \#prepare overlay
    sudo mkdir -p /var/log.overlay
    sudo chown root:syslog /var/log.overlay
    sudo chmod u=rwX,g=rwX,o=rX /var/log.overlay

    \#start overlay
    sudo mount -t overlay -o rw,lowerdir=/var/log,upperdir=/var/log.tmpfs/upper,workdir=/var/log.tmpfs/work overlay /var/log.overlay
    sudo mount --bind /var/log.overlay /var/log


# https://wiki.archlinux.org/index.php/Profile-sync-daemon
