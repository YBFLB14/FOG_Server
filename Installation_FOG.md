# Guide d'installation de FOG sur Debian/Ubuntu

Ce tutoriel présente les étapes nécessaires pour installer et configurer **FOG**, un logiciel open-source utilisé pour déployer des systèmes d'exploitation sur plusieurs ordinateurs à la fois via le réseau. Le serveur FOG va permettre de faciliter les déploiementS, la gestion des machines à distance, sans avoir besoin de supports physiques comme des clés USB ou des CD.

**FOG** utilise la technologie **PXE** (Preboot eXecution Environment), qui permet aux ordinateurs de démarrer directement depuis le réseau. Ce processus permet aux machines de se connecter à un serveur FOG, de télécharger une image système et de l'installer automatiquement. Ainsi, il devient possible d'installer ou de réinstaller des systèmes d'exploitation sur plusieurs ordinateurs simultanément, ce qui est particulièrement utile dans les environnements professionnels ou éducatifs.


## Prérequis

Avant de commencer, assurez-vous d'avoir :

- Une machine Debian ou Ubuntu avec des privilèges root.
- une machine avec 2 cartes, l'une permettant d'accéder à internet et l'autre permettant de communiquer avec les machines cible dans le réseau interne.
- Un serveur DHCP fonctionnel (sous Windows ou Linux)

## Étape 1 : Mise à jour des paquets

Commencer par mettre à jour le système pour s'assurer que tous les paquets sont à jour :

```bash
sudo apt update && sudo apt upgrade 
```

## Étape 2 : Installer les dépendances nécessaires

Installer git sur votre machine pour pouvoir ensuite cloner le dépôt git de FOG.

```bash
sudo apt install git
```
![Installation de git](/img/install_git.png)



## Étape 3 : Cloner le dépôt FOG

Cloner maintenant le dépôt officiel de FOG pour obtenir les derniers fichiers de configuration et le code source de FOG.

```bash
cd /root
git clone https://github.com/FOGProject/fogproject.git
cd fogproject
```

![Clonage du git](/img/image.png)

Cela télécharge FOG dans le répertoire `/root/fogproject`.
<br> 
<br>
## Étape 4 : Personnalisation du serveur FOG avant installation 

on se place dans le bon répertoire  et on lance l'installation.

![alt text](/omg/lancement_install.png)

Lors de l'installation de **FOG**, le script d'installation vous posera plusieurs questions auxquelles il faudra répondre en fonction des vos besoins.
<br>

### **1. Version de Linux**

**Question 1** : "What version of Linux would you like to run the installation for?"

![alt text](/img/OS_question.png)

- **Réponse entrée** : 2
- **Explication** : Cette question demande de spécifier la distribution Linux sur laquelle FOG sera installé c'est_à-dire votre système d'exploitation actuelle.

<br>

### **2. Type d'installation**

- **Question** : "What type of installation would you like to do ?"

![alt text](/img/type_install_question.png)

- **Réponse entrée** : Normal
- **Explication** :  Cette question vous demande de choisir le mode d'installation pour le serveur FOG. Il existe deux options principales :<br> 

    *  **Normal Server (N)** : Il s'agit du mode d'installation standard, qui installe tous les composants nécessaires de FOG sur le serveur. Ce mode est recommandé si vous n'êtes pas sûr de l'option à choisir.<br> 

    * **Storage Node (S)** : Ce mode est destiné à installer uniquement les logiciels nécessaires pour que ce serveur agisse comme un nœud dans un groupe de stockage. Ce choix est utilisé si vous souhaitez configurer un serveur uniquement pour stocker des images et non pour gérer le déploiement ou d'autres services.

<br>

### **3. Changer l'interface réseau par défaut**

- **Question** : "Would you like to change the default network interface from ens33 ?"

![alt text](/img/interface_reseau.png)

- **Réponse** : Yes / ens37 (réseau local)
- **Explication** : Le script détecte les interfaces réseau disponibles sur votre système et vous demande si vous souhaitez changer l'interface par défaut utilisée pour la communication réseau de FOG. Par exemple, dans ce cas, l'interface `ens33` est utilisée par défaut.


### 4. **Configuration du DHCP**

![alt text](/img/dhcp.png)

- **Question a** : "Would you like to setup a router address for the DHCP server ?"
- **Réponse** : Non
- **Explication** : Cette question vous demande si vous souhaitez spécifier une adresse de passerelle pour le serveur **DHCP** de FOG.


<br>

- **Question b** : "Would you like DHCP to handle DNS?"
- **Réponse** : Non
- **Explication** : Cette question demande si vous souhaitez que le serveur **DHCP** gère également les requêtes **DNS**.

<br>

- **Question c** : "Would you like to use the FOG server for DHCP service?"
- **Réponse** : Yes
- **Explication** : Cette question vous demande si vous souhaitez que le serveur **FOG** fournisse également le service **DHCP** pour gérer l'attribution des adresses IP aux machines clientes.


#### 5. **Installer des packs de langues supplémentaires**

- **Question** : "Would you like to install the additional language packs ?"

![alt text](/img/langage.png)

- **Réponse** : Non
- **Description** : Cette question vous propose d'installer des packs de langues supplémentaires pour FOG.

#### 6. **Activer HTTPS pour le serveur FOG**

- **Question** : "Would you like to enable HTTPS for your FOG server?"

![alt text](/img/https.png)

- **Réponse** : Yes
- **Description** : Cette question vous demande si vous souhaitez activer HTTPS pour sécuriser l'accès au serveur FOG. Si vous souhaitez sécuriser les connexions, tapez `Y`. Si vous préférez ne pas utiliser HTTPS, tapez `N`.

#### 7. **Changer le nom du serveur**

- **Question** : "Would you like to change it?"

![alt text](/img/name_server.png)


- **Description** : Vous êtes ensuite invité à indiquer si vous souhaitez changer le nom du serveur. Si vous êtes satisfait du nom par défaut (généralement `fog-server`), tapez `N`.

#### 8. **Accepter l'envoi d'informations anonymes**

- **Question** : "Are you ok with sending this information ?"

![alt text](/img/envoie_donnees.png)

- **Description** : FOG vous demande si vous êtes d'accord pour envoyer des informations anonymes à des fins d'amélioration du logiciel. Tapez `N` si vous préférez ne pas envoyer d'informations.

## Étape 9 : Finaliser la configuration via l'interface web

L'installation de FOG est maintenant terminée. Tu peux finaliser la configuration via l'interface web.

1. Ouvre ton navigateur et accède à l'URL suivante :

   ```
   https://<@IP du serveur>/fog/management
   ```


2. Connecte-toi avec les identifiants par défaut (ou les identifiants que tu as configurés lors de l'installation).

3. Clique sur **"Install/Update Now"** pour compléter la configuration et préparer ton serveur FOG pour gérer les images et les machines PXE.

## Étape 10 : Seconde partie de l'installation

