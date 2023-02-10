# Compte-Rendu TP6 Admin Système

## Exercice 2.

**On crée une première VM avec une interface résaux NAT ainsi qu'une interface en résaux interne (en autorisant la communication avec les autres VMs).**
**Ensuite on clone cette VM en supprimant l'interface NAT et en vérifiant que les addresses MAC sont différentes.**


*A l'aide de la commande `ip addr` on peut voir la liste des interfaces de la VM*
On remarque une interface appelée 'lo' qui correspond à l'addresse de bouclage (lo=loopback), elle correspond à la VM elle-même.


**Sur les VM utilisées le paquet `cloud-init` n'est pas installé mais dans le cas où il l'est on peut le supprimer avec :** 

`sudo apt-get remove cloud-init`

**On souhaite ensuite changer le nom du domaine et que ce changement soit effectif même après un redémarrage**
*Pour cela on change d'abord le nom du domaine :* 

`sudo hostnamectl set-hostname nom_hostname`


*Afin que ce changement persiste on modifie le fichier **/etc/hosts** :*

`sudo nano /etc/hosts`
>On remplace ensuite le nom de domaine associé à l'addresse IP *127.0.1.1*


## Exercice 3.
