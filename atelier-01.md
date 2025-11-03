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

# 8. Consulter l’historique des commandes
history
