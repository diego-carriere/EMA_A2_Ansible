# Atelier Ansible — Configuration et Tests

Ce document retrace les étapes de configuration et de test de l'atelier 06 **Ansible**
utilisant un control host (`control`) et trois target hosts (`target01`, `target02`, `target03`).  
Toutes les commandes et sorties affichées ont été conservées à des fins de documentation.

---

## 1. Configuration des hôtes et ssh

Affichage du contenu du fichier `/etc/hosts` après modification :
```bash
vagrant@control:~$ cat /etc/hosts | tail -n 5
# 192.168.56.20 test.target01.lan target01
# 192.168.56.30 test.target02.lan target02
# 192.168.56.40 test.target03.lan target03
```
Ajout des clés publiques des hôtes dans `known_hosts`

```bash
vagrant@control:~$ ssh-keyscan -t rsa target01 target02 target03 >> ~/.ssh/known_hosts
# target01:22 SSH-2.0-OpenSSH_8.9p1 Ubuntu-3ubuntu0.13
# target02:22 SSH-2.0-OpenSSH_8.9p1 Ubuntu-3ubuntu0.13
# target03:22 SSH-2.0-OpenSSH_8.9p1 Ubuntu-3ubuntu0.13
```
Copie de la clé publique vers chaque cible (ici exemple uniquement sur `target01`)

```bash
vagrant@control:~$ ssh-copy-id vagrant@target01
# /usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/vagrant/.ssh/id_rsa.pub"
# /usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
# /usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
# vagrant@target01's password: 

# Number of key(s) added: 1
```

## 2. Installation et test de Ansible

Installation
```bash
vagrant@control:~$ sudo apt install ansible
```
test via `ping` de ansible vers les targets
```bash
vagrant@control:~$ ansible all -i target01,target02,target03 -m ping

# target01 | SUCCESS => {
#    "ansible_facts": {"discovered_interpreter_python": "/usr/bin/python3"},
#    "changed": false,
#    "ping": "pong"
#}
#target02 | SUCCESS => {
#    "ansible_facts": {"discovered_interpreter_python": "/usr/bin/python3"},
#    "changed": false,
#    "ping": "pong"
#}
#target03 | SUCCESS => {
#    "ansible_facts": {"discovered_interpreter_python": "/usr/bin/python3"},
#    "changed": false,
#    "ping": "pong"
#}
```
## 5. Création et setup du projet Ansible

Création du dossier et du fichier de configuration :
```bash
vagrant@control:~$ mkdir -v ~/monprojet && touch ansible.cfg
#mkdir: created directory '/home/vagrant/monprojet'
```
Configuration de l’environnement avec `direnv`

```bash
vagrant@control:~/monprojet$ sudo apt install -y direnv && echo 'eval "$(direnv hook bash)"' >>
~/.bashrc && source ~/.bashrc
```
Création du fichier `.envrc` pour exporter la variable `ANSIBLE_CONFIG`
```bash
vagrant@control:~/monprojet$ echo 'export ANSIBLE_CONFIG=$(expand_path ansible.cfg)' > .envrc && direnv allow
# direnv: loading ~/monprojet/.envrc
# direnv: export +ANSIBLE_CONFIG
```
Ajout d'informations dans le fichier `ansible.cfg`
```bash
vagrant@control:~/monprojet$ printf "[defaults] \ninventory = ./hosts\nlog_path = ~/journal/ansible.log\n" > ansible.cfg
```
Création du dossier de journalisation et du fichier d’inventaire puis test de la journalisation
```bash
vagrant@control:~$ mkdir journal && touch hosts
vagrant@control:~/monprojet/projets/ema$ ansible all -i target01,target02,target03 -m ping && cat ~/journal/ansible.log
# target02 | SUCCESS => {"changed": false, "ping": "pong"}
# target03 | SUCCESS => {"changed": false, "ping": "pong"}
# target01 | SUCCESS => {"changed": false, "ping": "pong"}
```
Définition de l’inventaire (hosts)
```bash
[testlab]
target01
target02
target03

[testlab:vars]
ansible_python_interpreter=/usr/bin/python3
ansible_user=vagrant
ansible_become=yes
```

## 10. Tests finaux Ansible
Vérification du ping
```bash
vagrant@control:~/monprojet$ ansible all -m ping -o
# target01 | SUCCESS => {"changed": false,"ping": "pong"}
# target02 | SUCCESS => {"changed": false,"ping": "pong"}
# target03 | SUCCESS => {"changed": false,"ping": "pong"}
```
Exécution d’une commande sur toutes les cibles
```bash
vagrant@control:~/monprojet$ ansible all -a "head -n 1 /etc/shadow"
# target03 | CHANGED | rc=0 >>
# root:*:19977:0:99999:7:::
# target02 | CHANGED | rc=0 >>
# root:*:19977:0:99999:7:::
# target01 | CHANGED | rc=0 >>
# root:*:19977:0:99999:7:::
```
## 11. Nettoyage de l’environnement Vagrant

```bash
vagrant@control:~/monprojet$ exit
logout
```
Destruction des machines virtuelles
```bash
[ema@sandbox:atelier-06] $ vagrant destroy -f
#==> target03: Forcing shutdown of VM...
#==> target03: Destroying VM and associated drives...
#==> target02: Forcing shutdown of VM...
#==> target02: Destroying VM and associated drives...
#==> target01: Forcing shutdown of VM...
#==> target01: Destroying VM and associated drives...
#==> control: Forcing shutdown of VM...
#==> control: Destroying VM and associated drives...
```



