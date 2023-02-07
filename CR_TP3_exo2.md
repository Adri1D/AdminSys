# CR TP3 exo2 

# Guide utilisation commande `chmod` pour gérer les permissions

## Les différentes options de `chmod`

### Mise en situation 

On dispose d'un dossier *test* dans */home*.

Ce dossier contient un fichier *fichier* et d'un sous-dossier *sstest*.

## 0. Situation par défaut, gestion des droits sur un fichier


On vient de créer tous ces fichiers : `mkdir test` et `touch fichier`

On dispose par défaut, tous les droits sur ce répertoire : `stat -c %A test` (permet d'afficher les différents droits sur *test*) ```bash
drwxr-xr-x``` 

On dispoe par défaut, les droits de lecture et d'écriture sur ce fichier : `stat -c %A fichier` ```bash
-rw-r--r--```

* Le 'd' signifie juste qu'il s'agit d'un dossier ('directory').
* Les 3 caractères suivants correspondent aux droits donnés à l'utilisateur sur ce fichier.
* Les 3 caractères suivants correspondent aux droits donnés aux membres du groupe sur ce fichier.
* Les 3 caractères suivants correspondent aux droits donnés au autres sur ce fichier.

Dans ces 3 cas, il y a 3 droits différents : 

* Le premier, exprimé par la lettre `r` pour '*read*' désigne le droit de lecture :

    > Pour un dossier il permet de voir le contenu du dossier notamment avec la commande `ls`.
    > Pour un fichier il permet de lire le fichier.

* Le second, exprimé par la lettre `w` pour '*write*' désigne le droit d'écriture : 

    > Pour un dossier il permet de de créer ou supprimer fichier dans ce dossier. 
    > Pour un fichier il permet de modifier le contenu de ce dernier, on peut utiliser par exemple : 
    `echo "echo Hello" > /test/fichier`

* Le dernier, exprimé par la lettre `x` pour '*execution*' désigne le droit d'exécution : 

    > Pour un dossier il permet de rentrer dans le fichier, ainsi que ses sous-dossiers.
    > Pour un fichier il permet d'exécuter le fichier en question.

## 1. Utilisation de chmod

* La commande *chmod* peut se décompose de cette façon : `chmod [u g o a] [+ - =] [r w x] nom_fichier`
    * *chmod* signifie 'changer le mode de fonctionnement' 

    * `[u g o a]` permet de choisir pour qui changer les droits : 
        * 'u' désigne l'utilisateur, le propriétaire du fichier,
        * 'g' désigne le groupe de l'utilisateur,
        * 'o' désigne les autres utilisateurs,
        * 'a' désigne tous les utilisateurs.

    * `[+ - =]` permet de choisir quel action réaliser sur le droit que l'on veut modifier :
        * '+' permet de rajouter un droit,
        * '-' permet de supprimer un droit,
        * '=' peremt donner exactement les droits préciser aux utilisateurs concernés.

* On peut aussi utiliser `chmod` de cette façon `chmod [0-7] [0-7] [0-7] nom_fichier`
Ici chaque chiffre est associé aux droits donnés respectivement à l'utilisateur, au groupe et aux autres.

Il y a une coorespondance en binaire avec 'r w x' : r -> 4, w -> 2, x -> 1

Cependant cette méthode en octale permet seulement de fixer les droits mais pas de les rajouter ou de les supprimer sans connaitre les droits déjà existants.

Elle est donc plus rapide pour configurer les droits mais pas pour les modifier. 

* Le 'sticky bit' permet de donner, indépendament des droits sur le fichier, le droit de renommer ou supprimer le fichier au propriétaire du fichier, au propriétaire du dossier, au root.

Avec la première méthode, il s'utilise avec : `chmod +t nom_fichier`

Avec la seconde méthode il s'utilise avec : `chmod 1***` (* = [0-7])
 
* Quelques exemples d'utilisation de *chmod* :

Pour donner les droits de lecture à l'utilisateur, retirer le droit d'écriture au groupe et donner uniquement le droit d'execution aux autres sur *fichier1* et *fichier2* : 
`chmod u+r g-w o=x fichier1 fichier2`
Pour uniquement donner le droit de lecture et d'écriture à tous les utilisateurs :
`chmod a=rw nom_fichier` ou encore `chmod 666 nom_fichier`.


## 2. Première situation
On dispose de tous les droits sur *fichier* mais seulement du droit de lecture sur *test*.

* On peut uniquement utiliser `ls` pour afficher le contenu de *test*.

* Dans le cas où le répertoire courant est `/home` on ne peut ni rentrer dans *test* ni dans *sstest* qui se trouve dans *test*.

* Cependant si le répertoire courant est `/home/test` on ne peut toujours pas accéder à *sstest* mais on peut retourner dans `/home` avec `cd ..` car c'est le dossier parent et que 
ses droits sont prioritaires sur ceux de *test*. 

## 3. Deuxième situation 
On dispose de tous les droits sur *fichier* mais uniquement des droits de lecture et d'écriture sur *test*

On ne peut rien faire sur *fichier* car sans le droit d'exécution sur *test* on ne peut pas du tout accéder aux fichier qu'il contient, que ce soit pour les lire, les modifier, les exécuter, les renommer ou encore les supprimer.

### Conclusion
* Pour agir sur un fichier, accéder ou agir sur un sous-dossier, il faut nécessairement les droits d'exécution sur son dossier parent.

* Ensuite si on possède les droits d'exe, il faut les droits de lecture pour lire le contenu d'un fichier ou d'un dossier et il faut les droits d'écriture pour modifier un fichier, renommer ou supprimer un fichier ou sous-dossier.