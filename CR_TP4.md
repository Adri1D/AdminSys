# CR TP4 Gestion des paquets

## Exercice 1. Commandes de base
 
*On commence par mettre à jour notre système avec les commandes vues en cours :*
`apt update && apt upgrade -y`

*On crée un alias pour la commande précédente afin de pouvoir l'utiliser plus rapidement.*
*Il faut enregistrer cet alias dans le fichier `~/.bashrc` pour qu'il ne soit pas perdu au prochain redémarrage.*

*Après avoir installé plusieurs paquets, on ne sait plus vraiment lesquels sont installés et on souhaite donc voir les 5 derniers paquets installés :*
`$ grep install /var/log/dpkg.log | tail -n 5`
>`tail -n 5` permet de voir seulement les 5 dernières lignes soit les 5 derniers paquets installés

*On souhaite savoir le nombre de paquets disponibles sur les dépôts Ubuntu :*
``