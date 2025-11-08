# Idempotence et commandes Ad-hoc

Ce guide reprend les commandes de l'exercice `à vous de jouer` du cours [ci-joint](https://formations.microlinux.fr/ansible/idempotence/#creer-et-recreer-un-utilisateur).

## 1. Setup
```bash
[ema@sandbox:rendu] $ cd ~/formation-ansible/atelier-07
[ema@sandbox:atelier-07] $ vagrant up
[ema@sandbox:atelier-07] $ vagrant ssh ansible
```

## 2. Installation des paquets tree, git et nmap sur toutes les cibles
```bash
[vagrant@ansible ema]$ ansible all -m package -a "name=tree"
debian | CHANGED => {
    "cache_update_time": 1761245363,
    "cache_updated": false,
    "changed": true,
    "stderr": "",
    "stderr_lines": [],
    "stdout": "Reading package lists...\nBuilding dependency tree...\nReading state information...\nThe following NEW packages will be installed:\n  tree\n0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.\nNeed to get 52.5 kB of archives.\nAfter this operation, 116 kB of additional disk space will be used.\nGet:1 http://httpredir.debian.org/debian bookworm/main amd64 tree amd64 2.1.0-1 [52.5 kB]\nFetched 52.5 kB in 3s (20.8 kB/s)\nSelecting previously unselected package tree.\r\n(Reading database ... \r(Reading database ... 5%\r(Reading database ... 10%\r(Reading database ... 15%\r(Reading database ... 20%\r(Reading database ... 25%\r(Reading database ... 30%\r(Reading database ... 35%\r(Reading database ... 40%\r(Reading database ... 45%\r(Reading database ... 50%\r(Reading database ... 55%\r(Reading database ... 60%\r(Reading database ... 65%\r(Reading database ... 70%\r(Reading database ... 75%\r(Reading database ... 80%\r(Reading database ... 85%\r(Reading database ... 90%\r(Reading database ... 95%\r(Reading database ... 100%\r(Reading database ... 34138 files and directories currently installed.)\r\nPreparing to unpack .../tree_2.1.0-1_amd64.deb ...\r\nUnpacking tree (2.1.0-1) ...\r\nSetting up tree (2.1.0-1) ...\r\nProcessing triggers for man-db (2.11.2-2) ...\r\n",
    "stdout_lines": [
        "Reading package lists...",
        "Building dependency tree...",
        "Reading state information...",
        "The following NEW packages will be installed:",
        "  tree",
        "0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.",
        "Need to get 52.5 kB of archives.",
        "After this operation, 116 kB of additional disk space will be used.",
        "Get:1 http://httpredir.debian.org/debian bookworm/main amd64 tree amd64 2.1.0-1 [52.5 kB]",
        "Fetched 52.5 kB in 3s (20.8 kB/s)",
        "Selecting previously unselected package tree.",
        "(Reading database ... ",
        "(Reading database ... 5%",
        "(Reading database ... 10%",
        "(Reading database ... 15%",
        "(Reading database ... 20%",
        "(Reading database ... 25%",
        "(Reading database ... 30%",
        "(Reading database ... 35%",
        "(Reading database ... 40%",
        "(Reading database ... 45%",
        "(Reading database ... 50%",
        "(Reading database ... 55%",
        "(Reading database ... 60%",
        "(Reading database ... 65%",
        "(Reading database ... 70%",
        "(Reading database ... 75%",
        "(Reading database ... 80%",
        "(Reading database ... 85%",
        "(Reading database ... 90%",
        "(Reading database ... 95%",
        "(Reading database ... 100%",
        "(Reading database ... 34138 files and directories currently installed.)",
        "Preparing to unpack .../tree_2.1.0-1_amd64.deb ...",
        "Unpacking tree (2.1.0-1) ...",
        "Setting up tree (2.1.0-1) ...",
        "Processing triggers for man-db (2.11.2-2) ..."
    ]
}
rocky | SUCCESS => {
    "changed": false,
    "msg": "Nothing to do",
    "rc": 0,
    "results": []
}
suse | CHANGED => {
    "changed": true,
    "cmd": [
        "/usr/bin/zypper",
        "--quiet",
        "--non-interactive",
        "--xmlout",
        "install",
        "--type",
        "package",
        "--auto-agree-with-licenses",
        "--no-recommends",
        "--",
        "+tree"
    ],
    "name": [
        "tree"
    ],
    "rc": 0,
    "state": "present",
    "stderr": "",
    "stderr_lines": [],
    "stdout": "<?xml version='1.0'?>\n<stream>\n<install-summary download-size=\"56772\" space-usage-diff=\"116508\" space-usage-installed=\"116508\" space-usage-removed=\"0\" packages-to-change=\"1\" need-restart=\"0\" need-reboot=\"0\">\n<to-install>\n<solvable type=\"package\" name=\"tree\" edition=\"1.7.0-150000.3.2.1\" arch=\"x86_64\" repository=\"repo-sle-update\" summary=\"File listing as a tree\">\n<description>Tree is a recursive directory listing command that produces a depth\nindented listing of files, which is colorized ala dircolors if the\nLS_COLORS environment variable is set and output is to tty.</description></solvable>\n</to-install>\n</install-summary>\n<prompt id=\"0\">\n<text>Backend:  classic_rpmtrans\nContinue?</text>\n<option default=\"1\" value=\"y\" desc=\"Yes, accept the summary and proceed with installation/removal of packages.\"/>\n<option value=\"n\" desc=\"No, cancel the operation.\"/>\n<option value=\"v\" desc=\"Toggle display of package versions.\"/>\n<option value=\"a\" desc=\"Toggle display of package architectures.\"/>\n<option value=\"r\" desc=\"Toggle display of repositories from which the packages will be installed.\"/>\n<option value=\"m\" desc=\"Toggle display of package vendor names.\"/>\n<option value=\"d\" desc=\"Toggle between showing all details and as few details as possible.\"/>\n<option value=\"g\" desc=\"View the summary in pager.\"/>\n</prompt>\n<download url=\"http://fr2.rpmfind.net/linux/opensuse/update/leap/15.6/sle/x86_64/tree-1.7.0-150000.3.2.1.x86_64.rpm\" percent=\"-1\" rate=\"-1\"/>\n<download url=\"http://fr2.rpmfind.net/linux/opensuse/update/leap/15.6/sle/x86_64/tree-1.7.0-150000.3.2.1.x86_64.rpm\" percent=\"0\" rate=\"0\"/>\n<download url=\"http://fr2.rpmfind.net/linux/opensuse/update/leap/15.6/sle/x86_64/tree-1.7.0-150000.3.2.1.x86_64.rpm\" percent=\"96\" rate=\"54764\"/>\n<download url=\"http://fr2.rpmfind.net/linux/opensuse/update/leap/15.6/sle/x86_64/tree-1.7.0-150000.3.2.1.x86_64.rpm\" rate=\"54764\" done=\"1\"/>\n</stream>\n",
    "stdout_lines": [
        "<?xml version='1.0'?>",
        "<stream>",
        "<install-summary download-size=\"56772\" space-usage-diff=\"116508\" space-usage-installed=\"116508\" space-usage-removed=\"0\" packages-to-change=\"1\" need-restart=\"0\" need-reboot=\"0\">",
        "<to-install>",
        "<solvable type=\"package\" name=\"tree\" edition=\"1.7.0-150000.3.2.1\" arch=\"x86_64\" repository=\"repo-sle-update\" summary=\"File listing as a tree\">",
        "<description>Tree is a recursive directory listing command that produces a depth",
        "indented listing of files, which is colorized ala dircolors if the",
        "LS_COLORS environment variable is set and output is to tty.</description></solvable>",
        "</to-install>",
        "</install-summary>",
        "<prompt id=\"0\">",
        "<text>Backend:  classic_rpmtrans",
        "Continue?</text>",
        "<option default=\"1\" value=\"y\" desc=\"Yes, accept the summary and proceed with installation/removal of packages.\"/>",
        "<option value=\"n\" desc=\"No, cancel the operation.\"/>",
        "<option value=\"v\" desc=\"Toggle display of package versions.\"/>",
        "<option value=\"a\" desc=\"Toggle display of package architectures.\"/>",
        "<option value=\"r\" desc=\"Toggle display of repositories from which the packages will be installed.\"/>",
        "<option value=\"m\" desc=\"Toggle display of package vendor names.\"/>",
        "<option value=\"d\" desc=\"Toggle between showing all details and as few details as possible.\"/>",
        "<option value=\"g\" desc=\"View the summary in pager.\"/>",
        "</prompt>",
        "<download url=\"http://fr2.rpmfind.net/linux/opensuse/update/leap/15.6/sle/x86_64/tree-1.7.0-150000.3.2.1.x86_64.rpm\" percent=\"-1\" rate=\"-1\"/>",
        "<download url=\"http://fr2.rpmfind.net/linux/opensuse/update/leap/15.6/sle/x86_64/tree-1.7.0-150000.3.2.1.x86_64.rpm\" percent=\"0\" rate=\"0\"/>",
        "<download url=\"http://fr2.rpmfind.net/linux/opensuse/update/leap/15.6/sle/x86_64/tree-1.7.0-150000.3.2.1.x86_64.rpm\" percent=\"96\" rate=\"54764\"/>",
        "<download url=\"http://fr2.rpmfind.net/linux/opensuse/update/leap/15.6/sle/x86_64/tree-1.7.0-150000.3.2.1.x86_64.rpm\" rate=\"54764\" done=\"1\"/>",
        "</stream>"
    ],
    "update_cache": false
}
[vagrant@ansible ema]$ ansible all -m package -a "name=nmap"
...
[vagrant@ansible ema]$ ansible all -m package -a "name=git"
...
```

## 3. Désinstallation des trois paquets
```bash
[vagrant@ansible ema]$ ansible all -m package -a "name=tree state=absent"
...
[vagrant@ansible ema]$ ansible all -m package -a "name=nmap state=absent"
...
[vagrant@ansible ema]$ ansible all -m package -a "name=git state=absent"
suse | CHANGED => {
    "changed": true,
    "cmd": [
        "/usr/bin/zypper",
        "--quiet",
        "--non-interactive",
        "--xmlout",
        "remove",
        "--type",
        "package",
        "git"
    ],
    "name": [
        "git"
    ],
    "rc": 0,
    "state": "absent",
    "stderr": "",
    "stderr_lines": [],
    "stdout": "<?xml version='1.0'?>\n<stream>\n<install-summary download-size=\"0\" space-usage-diff=\"-3662\" space-usage-installed=\"0\" space-usage-removed=\"3662\" packages-to-change=\"1\" need-restart=\"0\" need-reboot=\"0\">\n<to-remove>\n<solvable type=\"package\" name=\"git\" edition=\"2.51.0-150600.3.12.1\" arch=\"x86_64\" repository=\"@System\" summary=\"Fast, scalable, distributed revision control system\">\n<description>Git is a fast, scalable, distributed revision control system with an\nunusually rich command set that provides both high-level operations and\nfull access to internals.\n\nThis package itself only provides the README of git but with the\npackages it requires, it brings you a complete Git environment\nincluding GTK and email interfaces and tools for importing source code\nrepositories from other revision control systems such as subversion,\nCVS, and GNU arch.</description></solvable>\n</to-remove>\n</install-summary>\n<prompt id=\"0\">\n<text>Backend:  classic_rpmtrans\nContinue?</text>\n<option default=\"1\" value=\"y\" desc=\"Yes, accept the summary and proceed with installation/removal of packages.\"/>\n<option value=\"n\" desc=\"No, cancel the operation.\"/>\n<option value=\"v\" desc=\"Toggle display of package versions.\"/>\n<option value=\"a\" desc=\"Toggle display of package architectures.\"/>\n<option value=\"r\" desc=\"Toggle display of repositories from which the packages will be installed.\"/>\n<option value=\"m\" desc=\"Toggle display of package vendor names.\"/>\n<option value=\"d\" desc=\"Toggle between showing all details and as few details as possible.\"/>\n<option value=\"g\" desc=\"View the summary in pager.\"/>\n</prompt>\n</stream>\n",
    "stdout_lines": [
        "<?xml version='1.0'?>",
        "<stream>",
        "<install-summary download-size=\"0\" space-usage-diff=\"-3662\" space-usage-installed=\"0\" space-usage-removed=\"3662\" packages-to-change=\"1\" need-restart=\"0\" need-reboot=\"0\">",
        "<to-remove>",
        "<solvable type=\"package\" name=\"git\" edition=\"2.51.0-150600.3.12.1\" arch=\"x86_64\" repository=\"@System\" summary=\"Fast, scalable, distributed revision control system\">",
        "<description>Git is a fast, scalable, distributed revision control system with an",
        "unusually rich command set that provides both high-level operations and",
        "full access to internals.",
        "",
        "This package itself only provides the README of git but with the",
        "packages it requires, it brings you a complete Git environment",
        "including GTK and email interfaces and tools for importing source code",
        "repositories from other revision control systems such as subversion,",
        "CVS, and GNU arch.</description></solvable>",
        "</to-remove>",
        "</install-summary>",
        "<prompt id=\"0\">",
        "<text>Backend:  classic_rpmtrans",
        "Continue?</text>",
        "<option default=\"1\" value=\"y\" desc=\"Yes, accept the summary and proceed with installation/removal of packages.\"/>",
        "<option value=\"n\" desc=\"No, cancel the operation.\"/>",
        "<option value=\"v\" desc=\"Toggle display of package versions.\"/>",
        "<option value=\"a\" desc=\"Toggle display of package architectures.\"/>",
        "<option value=\"r\" desc=\"Toggle display of repositories from which the packages will be installed.\"/>",
        "<option value=\"m\" desc=\"Toggle display of package vendor names.\"/>",
        "<option value=\"d\" desc=\"Toggle between showing all details and as few details as possible.\"/>",
        "<option value=\"g\" desc=\"View the summary in pager.\"/>",
        "</prompt>",
        "</stream>"
    ],
    "update_cache": false
}
rocky | CHANGED => {
    "changed": true,
    "msg": "",
    "rc": 0,
    "results": [
        "Removed: perl-Git-2.47.3-1.el9_6.noarch",
        "Removed: git-2.47.3-1.el9_6.x86_64"
    ]
}
debian | CHANGED => {
    "changed": true,
    "stderr": "",
    "stderr_lines": [],
    "stdout": "Reading package lists...\nBuilding dependency tree...\nReading state information...\nThe following packages were automatically installed and are no longer required:\n  git-man liberror-perl patch\nUse 'sudo apt autoremove' to remove them.\nThe following packages will be REMOVED:\n  git\n0 upgraded, 0 newly installed, 1 to remove and 0 not upgraded.\nAfter this operation, 46.0 MB disk space will be freed.\n(Reading database ... \r(Reading database ... 5%\r(Reading database ... 10%\r(Reading database ... 15%\r(Reading database ... 20%\r(Reading database ... 25%\r(Reading database ... 30%\r(Reading database ... 35%\r(Reading database ... 40%\r(Reading database ... 45%\r(Reading database ... 50%\r(Reading database ... 55%\r(Reading database ... 60%\r(Reading database ... 65%\r(Reading database ... 70%\r(Reading database ... 75%\r(Reading database ... 80%\r(Reading database ... 85%\r(Reading database ... 90%\r(Reading database ... 95%\r(Reading database ... 100%\r(Reading database ... 36183 files and directories currently installed.)\r\nRemoving git (1:2.39.5-0+deb12u2) ...\r\n",
    "stdout_lines": [
        "Reading package lists...",
        "Building dependency tree...",
        "Reading state information...",
        "The following packages were automatically installed and are no longer required:",
        "  git-man liberror-perl patch",
        "Use 'sudo apt autoremove' to remove them.",
        "The following packages will be REMOVED:",
        "  git",
        "0 upgraded, 0 newly installed, 1 to remove and 0 not upgraded.",
        "After this operation, 46.0 MB disk space will be freed.",
        "(Reading database ... ",
        "(Reading database ... 5%",
        "(Reading database ... 10%",
        "(Reading database ... 15%",
        "(Reading database ... 20%",
        "(Reading database ... 25%",
        "(Reading database ... 30%",
        "(Reading database ... 35%",
        "(Reading database ... 40%",
        "(Reading database ... 45%",
        "(Reading database ... 50%",
        "(Reading database ... 55%",
        "(Reading database ... 60%",
        "(Reading database ... 65%",
        "(Reading database ... 70%",
        "(Reading database ... 75%",
        "(Reading database ... 80%",
        "(Reading database ... 85%",
        "(Reading database ... 90%",
        "(Reading database ... 95%",
        "(Reading database ... 100%",
        "(Reading database ... 36183 files and directories currently installed.)",
        "Removing git (1:2.39.5-0+deb12u2) ..."
    ]
}
```

## 4. Copie du fichier `/etc/fstab` du Control Host vers les Target Hosts sous forme d'un fichier
```bash
[vagrant@ansible ema]$ ansible all -m copy -a "src=/etc/fstab dest=/tmp/test3.txt"
rocky | SUCCESS => {
    "changed": false,
    "checksum": "0fe1d6fcaf1695fb3ef9d8a42d45d04e5e0c11c2",
    "dest": "/tmp/test3.txt",
    "gid": 0,
    "group": "root",
    "mode": "0644",
    "owner": "root",
    "path": "/tmp/test3.txt",
    "secontext": "unconfined_u:object_r:user_home_t:s0",
    "size": 679,
    "state": "file",
    "uid": 0
}
debian | SUCCESS => {
    "changed": false,
    "checksum": "0fe1d6fcaf1695fb3ef9d8a42d45d04e5e0c11c2",
    "dest": "/tmp/test3.txt",
    "gid": 0,
    "group": "root",
    "mode": "0644",
    "owner": "root",
    "path": "/tmp/test3.txt",
    "size": 679,
    "state": "file",
    "uid": 0
}
suse | SUCCESS => {
    "changed": false,
    "checksum": "0fe1d6fcaf1695fb3ef9d8a42d45d04e5e0c11c2",
    "dest": "/tmp/test3.txt",
    "gid": 0,
    "group": "root",
    "mode": "0644",
    "owner": "root",
    "path": "/tmp/test3.txt",
    "size": 679,
    "state": "file",
    "uid": 0
}
```
## 5. Suppression du fichier `/tmp/test3.txt` sur les Target Hosts
```bash
[vagrant@ansible ema]$ ansible all -m file -a "path=/tmp/test3.txt state=absent"
debian | CHANGED => {
    "changed": true,
    "path": "/tmp/test3.txt",
    "state": "absent"
}
rocky | CHANGED => {
    "changed": true,
    "path": "/tmp/test3.txt",
    "state": "absent"
}
suse | CHANGED => {
    "changed": true,
    "path": "/tmp/test3.txt",
    "state": "absent"
}
```
## 6. Affichage de l'espace utilisé par la partition principale sur tous les Target Hosts
```bash
[vagrant@ansible ema]$ ansible all -m command -a "df -h /"
debian❘ CHANGED | IC=0 >> Filesystem
/dev/mapper/debian--12--vg-root rocky CHANGED | IC=0 >>
Filesystem
Size Used Avail Use% Mounted on
62G 1.7G 57G 3% /
Size Used Avail Use% Mounted on
/dev/sda2
61G 2.0G 59G 4% /
suse❘ CHANGED | Ic=0 >>
Filesystem /dev/sda3
Size Used Avail Use% Mounted on 64G 2.3G 58G 4% /
```
## 7. Cleanup du projet
```bash
[vagrant@ansible ema]$ exit
logout
Connection to 127.0.0.1 closed.
[ema@sandbox:atelier-07] $ vagrant destroy -f
==> ansible: Forcing shutdown of VM...
==> ansible: Destroying VM and associated drives...
==> suse: Forcing shutdown of VM...
==> suse: Destroying VM and associated drives...
==> debian: Forcing shutdown of VM...
==> debian: Destroying VM and associated drives...
==> rocky: Forcing shutdown of VM...
==> rocky: Destroying VM and associated drives...
```
