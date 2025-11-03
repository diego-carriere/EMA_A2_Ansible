# Challenge 1 — Installation et vérification d’Ansible avec Vagrant

## Objectif
Mettre en place une machine virtuelle Ubuntu via **Vagrant**, installer **Ansible**, et vérifier son installation.

## Étapes à suivre

```bash
# 1. Démarrer la machine virtuelle Ubuntu
vagrant up ubuntu

# 2. Se connecter à la machine virtuelle
vagrant ssh ubuntu

# 3. Mettre à jour la liste des paquets
sudo apt update

# 5. Rechercher les paquets contenant "ansible"
apt-cache search --names-only ansible

# 6. Installer Ansible
sudo apt install -y ansible

# 7. Vérifier la version installée
ansible --version

ansible 2.10.8
  config file = None
  configured module search path = ['/home/vagrant/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  executable location = /usr/bin/ansible
  python version = 3.10.12 (main, Aug 15 2025, 14:32:43) [GCC 11.4.0]


# 8. Se déconnecter et supprimer la VM
exit
vagrant destroy -f ubuntu
```

# Challenge 2 — Installation d’Ansible via le dépôt officiel PPA

## Objectif
Installer la dernière version stable d’**Ansible** depuis le dépôt officiel **PPA** et vérifier son installation.

## Étapes à suivre

```bash
# 1. Ajouter le dépôt officiel d’Ansible
sudo apt-add-repository ppa:ansible/ansible

# 2. Mettre à jour et installer Ansible
sudo apt install -y ansible

# 3. trouver la version de ansible
ansible --version

ansible [core 2.17.14]
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/home/vagrant/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  ansible collection location = /home/vagrant/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/bin/ansible
  python version = 3.10.12 (main, Aug 15 2025, 14:32:43) [GCC 11.4.0] (/usr/bin/python3)
  jinja version = 3.0.3
  libyaml = True

# 4. Se déconnecter et supprimer la VM
exit
vagrant destroy -f ubuntu
```

# Challenge 3 — Installation d’Ansible dans un environnement virtuel Python sur Rocky Linux

## Objectif
Configurer une machine **Rocky Linux** avec **Vagrant**, installer **Python 3.12**, créer un environnement virtuel, et y installer **Ansible**.

## Étapes à suivre

```bash
# 1. Démarrer la machine virtuelle Rocky Linux et se connecter
vagrant up rocky
vagrant ssh rocky

# 2. Mettre à jour le système
sudo dnf update

# 3. Rechercher les interpréteurs Python disponibles et installer python et pip
sudo dnf search python | grep ^python | grep -i interpreter
sudo dnf install python3.12 python3.12-pip

# 4. Créer un environnement virtuel pour Ansible et l'activer
python -m venv ~/.venv/ansible
source ~/.venv/ansible/bin/activate

# 5. Installer Ansible dans l’environnement virtuel
pip install ansible

# 6. Vérifier l’installation
ansible --version

ansible [core 2.15.13]
  config file = None
  configured module search path = ['/home/vagrant/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /home/vagrant/.venv/ansible/lib64/python3.9/site-packages/ansible
  ansible collection location = /home/vagrant/.ansible/collections:/usr/share/ansible/collections
  executable location = /home/vagrant/.venv/ansible/bin/ansible
  python version = 3.9.21 (main, Aug 19 2025, 00:00:00) [GCC 11.5.0 20240719 (Red Hat 11.5.0-5)] (/home/vagrant/.venv/ansible/bin/python)
  jinja version = 3.1.6
  libyaml = True

# 7. Se déconnecter et supprimer la VM
exit
vagrant destroy -f rocky  
```
