# openstack-ansible-debian12-howto

An Instruction how to get openstack-ansible running on debian 12

First install a debian minimal image (commandline only) - only add ssh when the installer asks for packets.

apt-get update

apt-get upgrade

apt-get install build-essential git chrony openssh-server python3-dev python3-pip sudo libffi-dev gcc wget ansible
