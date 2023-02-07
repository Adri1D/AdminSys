# CR TP4 Gestion des paquets

## Exercice 1. Commandes de base
 
**On commence par mettre à jour notre système avec les commandes vues en cours :**

`apt update && apt upgrade -y`

**On crée un alias pour la commande précédente afin de pouvoir l'utiliser plus rapidement.**
**Il faut enregistrer cet alias dans le fichier `~/.bashrc` pour qu'il ne soit pas perdu au prochain redémarrage.**

**Après avoir installé plusieurs paquets, on ne sait plus vraiment lesquels sont installés et on souhaite donc voir les 5 derniers paquets installés :**

`$ grep install /var/log/dpkg.log | tail -n 5`
>`tail -n 5` permet de voir seulement les 5 dernières lignes soit les 5 derniers paquets installés


**Par curiosité, on souhaite connaitre le nombre de paquets disponibles sur les dépôts Ubuntu :**
`apt list | wc -l` 

On trouve :
```bash
71313
```
C'est le nombre de paquets disponibles en téléchargement.

**On souhaite savoir le nombre de paquets installés sur notre appareil :**
`dpkg -l | wc -l`
> `dpkg -l` affiche la liste des paquets et `wc -l` permet d'afficher le nombre de ligne soit le nombre de paquet.

Avec la commande dpkg on obtient :
```bash
423
```

`apt list --installed | wc -l`

Avec la commande apt on obtient :
```bash
419
```

Cette différence entre les 2 nombres de paquet s'explique car avec **dpkg** il y a des lignes de warning que wc compte, mais qu'il ne compte pas avec **apt**.


**On souhaite afficher les derniers paquets installé :**
`grep "apt install" /var/log/apt/history.log`
> Permet d'afficher l'historique des derniers paquets installés.
On trouve :
```bash
apt install glow
```

**Le paquet `glances` permet d'avoir des informations détaillées sur les performances et la consommation du système**

**Le paquet `tldr` fournit une version simplifiée et condensée de la documentation pour des commandes Unix**

**Le paquet `hollywood` permet de jouer dans le terminal grâce à l'affichage de caractères ASCII**


## Exercice 2.
**Pour connaître le paquet qu'y installe une commande, on utilise :**
`which -a nom_commande`

**On souhaite crée un script qui affiche le paquet qui a installé la commande passé en argument ; pour cela on écrit dans un script :**
`which -a $1`
> Executer ce script va afficher le paquet qui a installé la commande passé en argument.

## Exercice 3.
**On souhaite faire un script qui renvoie si le paquet associé à la commande entrée en argument est installé ou non :**
```bash
if dpkg -l | grep -i $1 > /dev/null
then
        echo "INSTALLE"
else
        echo "NON INSTALLE"
fi
```


## Exercice 4.
**Le fichier `/usr/share/man/man1/[.1.gz` est une manpage de la commande `[` qui est un opérateur de test de condition pour shell**

## Exercice 6.
**`/etc/apt/sources.list.d` est un répertoire qui contient des fichiers de configuration pour des dépôts supplémentaires pour apt.**
