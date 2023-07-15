# Openhotspot
Openwisp &amp; openwrt hotspot

## Instalacion de openwisp en debian 11
Acceder por ssh

ssh -lroot -p22 12.345.657.89

python3 --version
apt install python3-pip
pip --version
apt-get install git
sudo apt-get install python3 python3-pip -y
sudo pip3 install ansible
python3 -m pip install --user ansible
ansible-galaxy install openwisp.openwisp2

## Choose a working directory
mkdir ~/openwisp2-ansible-playbook
cd ~/openwisp2-ansible-playbook

## Create inventory file
nano hosts
```
[openwisp2]
#89.117.53.163
```

nano playbook.yml

- hosts: openwisp2
  become: "{{ become | default('yes') }}"
  roles:
    - openwisp.openwisp2
  vars:
    openwisp2_shared_secret: 84River@Bta
    postfix_myhostname: localhost

apt install sshpass

ansible-playbook -i hosts playbook.yml -u root -k --become -K
coloca la contrasena de tu servidor

#Agregar ip a known
ssh-keyscan -H 192.168.1.162 >> ~/.ssh/known_hosts

ansible.cfg

[defaults]
module_set_locale=True
module_lang=it_IT.UTF-8
remote_port    = 2400
retry_files_enabled = False
nocows = 1

#roles_path = ~/.ansible/roles
roles_path = roles
collections_paths = collections


ansible_managed = Ansible managed: modified on %d-%m-%Y

# Use the YAML callback plugin.
stdout_callback = yaml

# Display execution times
callback_whitelist = timer, profile_tasks

# Python interpreter discovery
interpreter_python = /usr/bin/python3
python_interprete = python3

# Fact gathering caching
gathering = smart
fact_caching = jsonfile
fact_caching_connection = .ansible_cache
fact_caching_timeout = 28800

https://github.com/mikysal78/wifi.nnxx.ninux.org/tree/main
