# ansible-nspawn
This role creates systemd-nspawn containers from a base image and makes them accessible via network

## preparation
```bash
# prepare base images in /var/lib/machines

# prepare debian base image
debootstrap --include=systemd-container,vim,openssh-server,avahi-daemon --arch=amd64 buster ./debian-buster-amd64

# prepare ubuntu base image
debootstrap --arch=amd64 --include vim,openssh-server,avahi-daemon bionic ./ubuntu-bionic-amd64 http://de.archive.ubuntu.com/ubuntu

# prepare archlinux base image
pacstrap -i archlinux-rolling-amd64/ base avahi openssh
```
```
# enable services
systemctl enable avahi-daemon
systemctl enable systemd-networkd
```

## working features
* create containers from template
* add host interface to container namespace
* add veth interface to container
* add macvlan interface to container
* setup basic DNS inside the container
* automatic avahi/mDNS config
* bind mounts to the container

## planned feature
* static IP config inside the container
* basic SSH key setup inside the container

## possible but not planned feature
* base image create eg. with debootstrap 
* bridge setup with DHCP

This project was froked from:
  https://opendev.org/openstack/openstack-ansible-nspawn_container_create/
