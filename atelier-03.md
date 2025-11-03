# Challenge 4 — Authentification SSH et connexion Ansible aux nœuds cibles

## Objectif
Configurer l’authentification SSH entre la machine **control** et les machines **target01**, **target02** et **target03**, puis vérifier la connectivité avec Ansible.

## Étapes à suivre

### 🔧 Setup initial

```bash
# 1. Se placer dans le dossier de l’atelier et démarrer les machines virtuelles
cd ../atelier-03
vagrant up

# 2. Se connecter à la machine "control" et vérifier la présence de la commande ansible
vagrant ssh control
type ansible

# 3.1 Modifier le fichier /etc/hosts pour ajouter les hôtes du sandbox
sudo nano /etc/hosts

# Ajouter les lignes suivantes :
192.168.56.10  control.sandbox.lan      control
192.168.56.20  target01.sandbox.lan     target01
192.168.56.30  target02.sandbox.lan     target02
192.168.56.40  target03.sandbox.lan     target03

# 3.2 Vérifier la connectivité réseau avec les cibles
for HOST in target01 target02 target03; do ping -c 1 -q $HOST; done

# 4. Ajouter les clés SSH des hôtes cibles dans known_hosts
ssh-keyscan -t rsa target01 target02 target03 >> .ssh/known_hosts

# 5.1 Générer une paire de clés SSH pour l’utilisateur vagrant
ssh-keygen

# 5.2 Copier la clé publique sur chaque machine cible
ssh-copy-id vagrant@target01
ssh-copy-id vagrant@target02
ssh-copy-id vagrant@target03

# 6. Tester la connexion Ansible avec le module "ping"
ansible all -i target01,target02,target03 -u vagrant -m ping

target01 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
target02 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
target03 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```
