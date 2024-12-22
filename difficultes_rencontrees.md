# Difficultés Rencontrées Lors de l'Installation de FOG

## Dépendance du serveur au autres composants de l'infrastructure
- **Dépendance au serveur DHCP** : Pour déployer des OS et communiquer avec les machines clientes, il faut que celle-ci obtiennent tout d'abord une adresse IP puis une fois cela fait soit c'est le DHCP lui même qui fourni l'adresse du serveur FOG soit c'est un ProxyDHCP qui va agir comme un DHCP mais sans fournir d'adresse IP uniquement en fournissant l'adresse IP du serveur FOG. Dans l'infrastructure c'était un serveur DHCP externe qui a été crée et donc si celui_ci n'arrivait pas à attribuer d'adresse IP à la machine, le déploiement ne peux pas se faire.

---

## Téléchargement de l'OS d'une machine enregistré
- **Description** : Après qu'une machine est été enregitré et quel appaissent dans le serveur FOG, il faut récupérer l'OS de la machine master pour ensuite la déployé les clone. le problème est que j'ai lancé la tâche pour récupérer l'OS mais la tâche ne se termine jamais.

---

## Téléchargement incomplet de FOG
- **Description** : Lors de l'installation de FOG , il est demandé de se rendre dans son nvigateur et d'ouvrir la page d'accueil de FOG. Lors de la première connexion, il est demander de réaliser une update et la cohse que j'ai mis du temps a comprendre est qu'il faut revenir dans le terminal ou j'avait réaliser l'installation et ensuite taper entrer pour qu'il termine l'installation complète sinon, le serveur FOG ne pourra jamais serivr a udéploiement d'OS.

---

## Capture d'un OS

lancement de la tâche de capture mais pas d'abotuissement de la tâche car mémoire insuffisante et besoin de lancer le boot à partir de PXE pour avoir la capture