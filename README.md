# ansible-role-nspawn-container
This role creates systemd-nspawn containers from a base image and makes them accessible via network.

The idea is that you setup a physical host via ansible and fill out host_vars files for the containers as if they were normal machines.
This role then looks for the physical_host reference inside the containers vars and spawn it on the corresponding host.
With the help of systemd-networkd, systemd-resolved and avahi-daemon the whole thing works without IP address management.

Might be usefull for creating nspawns on servers in your local network or for creating development containers on localhost.

## working features
* create containers from template
* add host interface to container namespace
* add veth interface to container
* add macvlan interface to container
* setup basic DNS inside the container
* automatic avahi/mDNS config
* bind mounts to the container
* no network namespace mode (like chroot)
* basic SSH key setup inside the container

## planned feature
* use already existing namespace
* skipping most of the steps if container already exists
* base image create eg. with debootstrap 
* add the root users authorized keys to the container

## possible but not planned features
* static IP config inside the container
* bridge setup with DHCP
* possibility to disable avahi

## preparation
```bash
# prepare base images in /var/lib/machines

# prepare debian base image
debootstrap --include=systemd-container,vim,openssh-server,avahi-daemon --arch=amd64 buster ./debian-buster-amd64

# prepare ubuntu base image
debootstrap --components=main,universe --arch=amd64 --include vim,openssh-server,avahi-daemon bionic ./ubuntu-bionic-amd64 http://de.archive.ubuntu.com/ubuntu

# prepare archlinux base image
pacstrap -i archlinux-rolling-amd64/ base avahi openssh python
```

```
# enable services on host and in base image
systemctl enable avahi-daemon
systemctl enable systemd-networkd
systemctl enable systemd-resolved
```

## Usage
See the default/main.yml for default values and usable variables. Additionally there are some example configs in the example/ folder.

This project was froked from:
  https://opendev.org/openstack/openstack-ansible-nspawn_container_create/
