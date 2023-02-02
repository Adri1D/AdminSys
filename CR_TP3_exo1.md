# CR TP3 Exo1 : Utilisateurs, Groupes et Permissions

## 0. Mise en situation

**On souhaite gérer deux équipes ; une équipe de développeur et une équipe d'infra** 
Les utilisateurs concernés sont Alice, Bob, Charlie, Dave.

**On veut d'abord créer les groupes, pour cela :**
`groupadd dev`
``groupadd infra`

**On souhaite ajouter les 4 utilisateurs avec bash pour shell, pour cela on utilise la commande :**`useradd -m nom_utilisateur -s /bin/bash`
> -m permet de créer un répertoire /home
> -s permet de changer le shell (dans notre cas par bash).

**Pour vérifier les accès on peut par exemple vouloir afficher les membres d'un groupe, pour cela on va utiliser :**
`cat /etc/passwd` ou encore `less /etc/group`

**Pour configurer les droits sur certains fichiers, on peut souhaiter changer un utilisateur de groupe, pour cela on va utiliser la coomande** `usermod` **qui permet de gérer les utilisateurs :** `usermod -g nom_groupe nom_utilisateur` 
> -g permet de définir le groupe comme groupe primaire pour l'utilisateur.

**Suite à un changement de poste au sein de l'entreprise on souhaite changer les répertoires prioritaires des utilisateurs, pour cela on va utiliser :**
`chgrp -R nom_groupe /home/nom_utilisateur`

**Après avoir créer 2 répertoires** *dev* **et** *infra* **avec** `mkdir` **on souhaite donner le droit d'écriture aux membres de ce groupe :**
`chmod g+x /home/nom_utilisateur/`
> on rajoute juste le droit d'écrire en sachant que par défaut les membres du groupe possèdent le droit de lecture et le droit d'exécution sur le répertoire. 

**Par sécurité on veut que seul le propriétaire d'un fichier puisse le renommmer ou le supprimer :**`chmod +t nom_fichier`
> +t permet d'activer le `sticky bit` qui permet, indépendament des droits donnés, de ne permettre qu'au créateur du fichier et au root de pouvoir le renommer ou de le supprimer.

**Si l'on souhaite se connecter sur la session d'alice pour changer des droits d'accès par exemple, on ne peut pas car il n'y a pas de mot de passe défini par défaut**
Donc soit il n'y a pas de mot de passe, soit il y en a un que l'on ne connait pas donc on ne peut pas se connecter sur la session d'alice sans passer par le root.

**Alice vient de prendre le job et souhaite activer son compte, il faut donc lui créer un mot de passe :**`sudo passwd alice`
> On doit soit utiliser sudo pour se donner les droits ou passer en root
```bash
[sudo] password for adrien:
New password:
Retype new password:
passwd: password updated successfully
```

**On souhaite récupérer les id de Alice :**`id Alice`
```bash
uid=1001(alice) gid=1001(dev) groups=1001(dev)
```
On pourrait utiliser : `id -g alice` pour récupérer l'id de son groupe, ou encore rajouter `-n` pour récupérer directement le nom du groupe.

**Après avoir remarqué une action annormale de la part de l'id 1003, on souhaite retrouver l'utilisateur associé :** 
On cherche donc le nom associé à l'id 1003, qui est stocké dans passwd donc utilise la commande `getent` qui permet de trouver l'entrée correspondante dans un répertoire donc : `getent passwd 1003`
```bash
charlie:x:1003:1002::/home/charlie:/bin/bash
```
