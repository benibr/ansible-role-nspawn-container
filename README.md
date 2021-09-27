# ansible-role-nspawn-container

**This is under heavy development and will change without beeing backwards compatible**

This role creates systemd-nspawn containers from a base image and makes them accessible via network.

The idea is that you setup a physical host via ansible and fill out host_vars files for the containers as if they were normal machines.
This role then looks for the physical_host reference inside the containers vars and spawn it on the corresponding host.
With the help of systemd-networkd, systemd-resolved and avahi-daemon/LLMNR the whole thing is aimed to work without IP address management.

Might be useful for creating nspawns on servers in your local network or for creating development containers on localhost.

## working features
* create containers from template
* add physical host interface to container namespace
* add veth interface to container
* add macvlan interface to container
* setup basic DNS inside the container
* automatic avahi/mDNS config
* bind mounts to the container
* no network namespace mode (like chroot)
* basic SSH key setup inside the container
* base image create eg. with debootstrap 
* use already existing namespace
* possibility to disable avahi

## planned feature
* check resolved setup depending on network connection
* skipping most of the steps if container already exists
* add the root users authorized keys to the container
* bind container SSH on random highport if netns is shared with host

## possible but not planned features
* static IP config inside the container
* bridge setup with DHCP

## Usage
See the default/main.yml for default values and usable variables. Additionally there are some example configs in the `example/` folder.

This project was forked from:
  https://opendev.org/openstack/openstack-ansible-nspawn_container_create/
