# openstack-ansible-debian12-howto

An Instruction how to get openstack-ansible running on debian 12

First install a debian minimal image (commandline only) - only add ssh when the installer asks for packets.

apt-get update

apt-get upgrade

apt-get dist-upgrade

apt-get install build-essential git chrony openssh-server python3-dev python3-pip python3-full sudo libffi-dev gcc wget ansible python3-openstackclient libssl-dev libdbus-glib-1-dev python3-venv
