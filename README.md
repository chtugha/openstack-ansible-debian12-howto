# openstack-ansible-debian12-howto

An Instruction how to get openstack-ansible running on debian 12

First install a debian minimal image (commandline only) - only add ssh when the installer asks for packets.
You will need two network adapters at first.

login as root directly on the machine:

apt-get update

apt-get upgrade

apt-get dist-upgrade

apt-get install build-essential git chrony openssh-server python3-dev python3-pip python3-full sudo libffi-dev gcc wget ansible python3-openstackclient libssl-dev libdbus-glib-1-dev python3-venv

cd /

nano /etc/ssh/sshd_config  (change PermitRootLogin to yes)

systemctl restart ssh (now you can work via ssh as root)

python3 -m venv myenv

source /myenv/bin/activate

pip install -U pip

pip install kolla-ansible

cp -r /myenv/share/kolla-ansible/etc_examples/kolla /etc/kolla

ip a       (remember the name of the first network interface)

nano /etc/kolla/globals.yml

