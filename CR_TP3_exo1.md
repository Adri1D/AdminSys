# CR TP3 Exo1 : Utilisateurs, Groupes et Permissions

## 0. Mise en situation

On souhaite gérer deux équipes ; une équipe de développeur et une équipe d'infra 
Les utilisateurs concernés sont Alice, Bob, Charlie, Dave.

On veut d'abord créer les groupes, pour cela :
`groupadd dev`
``groupadd infra`

On souhaite ajouter les 4 utilisateurs avec bash pour shell, pour cela on utilise la commande :
`useradd -m nom_utilisateur -s /bin/bash`

> -m permet de créer un répertoire /home
> -s permet de changer le shell (dans notre cas par bash).

Pour vérifier les accès on peut par exemple vouloir afficher les membres d'un groupe, pour cela on va utiliser :
`cat /etc/passwd` ou encore `less /etc/group`

Pour configurer les droits sur certains fichiers, on peut souhaiter changer un utilisateur de groupe, pour cela on va utiliser la coomande `usermod` qui permet de gérer les utilisateurs : 
`usermod -g nom_groupe nom_utilisateur` 
> -g permet de définir le groupe comme groupe primaire pour l'utilisateur.

Suite à un changement de poste au sein de l'entreprise on souhaite changer les répertoires prioritaires des utilisateurs, pour cela on va utiliser :
`chgrp -R nom_groupe /home/nom_utilisateur`

Après avoir créer 2 répertoires *dev* et *infra* avec `mkdir` on souhaite donner le droit d'écriture aux membres de ce groupe :
`chmod g+x /home/nom_utilisateur/`
> on rajoute juste le droit d'écrire en sachant que par défaut les membres du groupe possèdent le droit de lecture et le droit d'exécution sur le répertoire. 