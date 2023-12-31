# Openhotspot
Openwisp &amp; openwrt hotspot

## Instalacion de openwisp en debian 11
Acceder por ssh

ssh -lroot -p22 12.345.657.89
apt install sudo
apt-get install git -y
sudo apt-get install python3 python3-pip -y
sudo pip3 install ansible
sudo apt install ansible
python3 -m pip install --user ansible
ansible-galaxy install openwisp.openwisp2

## Choose a working directory
mkdir ~/openwisp2-ansible-playbook
cd ~/openwisp2-ansible-playbook

## Create inventory file
nano hosts
```
[openwisp2]
89.117.53.163
```

nano playbook.yml

- hosts: openwisp2
  become: "{{ become | default('yes') }}"
  roles:
    - openwisp.openwisp2
  vars:
    openwisp2_shared_secret: 84River@Bta
    postfix_myhostname: localhost

nano ansible.cfg
[defaults]
# Python interpreter discovery
host_key_checking = false


ansible-galaxy install -r requirements.yml

apt install sshpass

ansible-playbook -i hosts playbook.yml -u root -k --become -K
coloca la contrasena de tu servidor

https://github.com/openwisp/ansible-openwisp-wifi-login-pages/
https://github.com/mikysal78/wifi.nnxx.ninux.org/tree/main

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

-------------------------------------------
## Openwisp dev
```
mkdir -p ~/openwisp-dev/roles
mkdir -p ~/openwisp-dev/collections
cd ~/openwisp-dev/
nano ansible.cfg
```

```
[defaults]
roles_path=~/openwisp-dev/roles
collections_paths=~/openwisp-dev/collections
host_key_checking = false
```

```
nano requirements.yml
```

```
---
roles:
  - src: https://github.com/openwisp/ansible-openwisp2.git
    version: master
    name: openwisp.openwisp2-dev
collections:
  - name: community.general
    version: ">=3.6.0"
```

```
ansible-galaxy install -r requirements.yml
nano hosts
```

```
[wifibro]
uniq.edu.mx
```
```
nano playbook.yml
```

```
- hosts: wifibro
  become: "{{ become | default('yes') }}"
  roles:
    - openwisp.openwisp2-dev
  vars:
    openwisp2_network_topology: true
    openwisp2_radius: true
    openwisp2_monitoring: true
```

```
apt install sudo
apt-get install git -y
sudo apt-get install python3 python3-pip -y
python3 -m pip install --user ansible
export PATH=$PATH:~/.local/bin
apt install sshpass
ansible-playbook -i hosts playbook.yml -u root -k --become -K
```

https://github.com/mikysal78/wifi.nnxx.ninux.org/tree/main
