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
