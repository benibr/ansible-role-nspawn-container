# ansible-nspawn
This role creates systemd-nspawn containers from a base image and makes them accessible via network

## working features
* create containers from template
* add host interface to container namespace
* add veth interface to container
* add macvlan interface to container
* setup basic DNS inside the container

## planned feature
* automatic avahi/mDNS config
* static IP config inside the container
* basic SSH key setup inside the container
* bind mounts to the container

## possible but not planned feature
* base image create eg. with debootstrap 
* bridge setup with DHCP

This project was froked from:
  https://opendev.org/openstack/openstack-ansible-nspawn_container_create/
