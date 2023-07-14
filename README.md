# Openhotspot
Openwisp &amp; openwrt hotspot

## Instalacion de openwisp en debian 11
Acceder por ssh
ssh -lroot -p22 12.345.657.89

python3 --version
apt install python3-pip
pip --version
apt-get install git
 python3 -m pip install --user ansible
 ansible-galaxy install openwisp.openwisp2

ansible-galaxy collection install "community.general:>=3.6.0"
ansible-galaxy collection install "ansible.posix"

## Choose a working directory
mkdir ~/openwisp2-ansible-playbook
cd ~/openwisp2-ansible-playbook

## Create inventory file
nano hosts
```
[openwisp2]
openwisp2.mydomain.com
#89.117.53.156
```

nano playbook.yml

- hosts: openwisp2
  become: "{{ become | default('yes') }}"
  roles:
    - openwisp.openwisp2
  vars:
    openwisp2_shared_secret: 84River@Bta

apt install sshpass

ansible-playbook -i hosts playbook.yml -u root -k --become -K
coloca la contrasena de tu servidor

