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

# 4. Rechercher les paquets contenant "ansible" (option 1)
apt-cache search --name-only ansible

# 5. Rechercher les paquets contenant "ansible" (option 2)
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
