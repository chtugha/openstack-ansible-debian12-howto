# openstack-ansible-debian12-howto

An Instruction how to get openstack-ansible running on debian 12

First install a debian minimal image (commandline only) - only add ssh when the installer asks for packets.
You will need two network adapters at first.

login as root directly on the machine:

apt-get update

apt-get upgrade

apt-get dist-upgrade

apt-get install build-essential git chrony openssh-server python3-dev python3-pip python3-full sudo libffi-dev gcc wget python3-openstackclient libssl-dev libdbus-glib-1-dev python3-venv apt-transport-https ca-certificates curl gnupg2 software-properties-common pwgen pipx

cd /

nano /etc/ssh/sshd_config  (change PermitRootLogin to yes)

systemctl restart ssh (now you can work via ssh as root)

nano /etc/apt/sources.list

add the following line:  deb http://ppa.launchpad.net/ansible/ansible/ubuntu focal main

apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367

apt-get update -y

apt-get install ansible

curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list

apt-get update -y

apt-get install docker-ce

wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -

echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" | sudo tee  /etc/apt/sources.list.d/pgdg.list

apt-get update -y

apt-get install postgresql-10 python3-openstacksdk

cd /tmp

wget https://github.com/docker/compose/releases/download/v2.27.0/docker-compose-linux-x86_64

mv docker-compose-linux-x86_64 /usr/bin/docker-compose

chmod +x /usr/bin/docker-compose

curl -fsSL https://deb.nodesource.com/setup_20.x | bash -

apt install nodejs

npm install npm --global

apt install docker-compose-plugin

pipx ensurepath

pipx install docker-compose==2.27.0

wget https://github.com/ansible/awx/archive/refs/tags/17.1.0.zip

unzip 17.1.0.zip

cd /tmp/awx-17.1.0/installer/

pwgen -N 1 -s 30

copy the PW

nano inventory

change following lines:   admin_password=YourPassword   secret_key=TheKeyYouGenerated

ansible-playbook -i inventory install.yml

change the lines with the errors from docker_compose to docker.community.docker_compose_v2

run again and again till it works..

nano ./roles/local_docker/tasks/compose.yml

change        restarted: blabla       to     state: present

ansible-galaxy collection install community.docker

cd /tmp/awx-17.1.0/installer/roles/image_build/files

cp launch_awx.sh /usr/bin/launch_awx.sh

cp launch_awx_task.sh /usr/bin/launch_awx_task.sh

cd /root/.awx/awxcompose/

docker-compose up

cd /

find . -name update-ca-trust

cp ./var/lib/docker/overlay2/e1e7e807915be1bba963abe8fff42c1b8c935b21005b7ccafda7d477b42d03f6/diff/usr/bin/update-ca-trust ./usr/bin/update-ca-trust







