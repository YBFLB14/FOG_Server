# Mise en place du proxyDHCP

## **Introduction**
Le ProxyDHCP est intéressant dans les environnements où un serveur DHCP principal existe déjà et ne peut pas être modifié pour fournir les options nécessaires au démarrage PXE. Cette configuration permet auxclients PXE reçoivent les bonnes instructions pour se connecter au serveur FOG.

Ce guide explique comment configurer le fichier **dnsmasq.conf** pour que `dnsmasq` agisse comme ProxyDHCP.

---

## **Configuration**

### **1. Installer dnsmasq**
Installez le paquet `dnsmasq` avec la commande suivante :
```bash
sudo apt install dnsmasq
```

### **2. Fichier de configuration dnsmasq.conf**
Créez ou modifiez le fichier de configuration :
```bash
sudo nano /etc/dnsmasq.conf
```

Vous pouvez retrouver un exemple de configuration [ici](https://github.com/YBFLB14/FOG_Server/blob/35ada1b53ab4f9257d2b3d775d03e2a2d5c423ac/2_ProxyDHCP_Setup/dnsmasq.conf).

**Explication de chaque option**

### **Options générales**
- **`port=0`** : Désactive la fonction DNS de `dnsmasq`, limitant son rôle à celui de ProxyDHCP.
- **`log-dhcp`** : Active les journaux détaillés des requêtes DHCP pour aider au débogage.
- **`tftp-root=/tftpboot`** : Définit le répertoire racine où les fichiers TFTP sont stockés.

### **Options DHCP de base**
- **`dhcp-boot=undionly.kpxe,192.168.1.205`** : Définit le fichier de démarrage par défaut et l’adresse du serveur TFTP pour les clients BIOS.
- **`dhcp-no-override`** : Empêche `dnsmasq` de modifier les champs "nom du serveur" et "fichier de démarrage" définis par le DHCP principal.

### **Classes de clients et architectures**
- **`dhcp-vendorclass=BIOS,PXEClient:Arch:00000`** : Associe le tag `BIOS` aux clients utilisant un BIOS traditionnel.
- **`dhcp-vendorclass=UEFI32,PXEClient:Arch:00006`** : Associe le tag `UEFI32` aux clients UEFI 32 bits.
- **`dhcp-vendorclass=UEFI,PXEClient:Arch:00007`** : Associe le tag `UEFI` aux clients UEFI génériques.
- **`dhcp-vendorclass=UEFI64,PXEClient:Arch:00009`** : Associe le tag `UEFI64` aux clients UEFI 64 bits.

### **Fichiers de démarrage spécifiques aux architectures**
- **`dhcp-boot=net:UEFI32,i386-efi/ipxe.efi,,192.168.1.205`** : Fichier de démarrage pour UEFI 32 bits.
- **`dhcp-boot=net:UEFI,ipxe.efi,,192.168.1.205`** : Fichier de démarrage générique pour UEFI.
- **`dhcp-boot=net:UEFI64,ipxe.efi,,192.168.1.205`** : Fichier de démarrage pour UEFI 64 bits.

### **Messages et services PXE**
- **`pxe-prompt="Booting FOG Client", 2`** : Affiche un message pendant 2 secondes avant de continuer automatiquement.
- **`pxe-service=X86PC, "Boot to FOG", undionly.kpxe`** : Service PXE pour les clients BIOS.
- **`pxe-service=X86-64_EFI, "Boot to FOG UEFI", ipxe.efi`** : Service PXE pour les clients UEFI 64 bits.

### **Plage ProxyDHCP**
- **`dhcp-range=192.168.1.205,proxy`** : Définit que `dnsmasq` agit en tant que ProxyDHCP sur l’IP `192.168.1.205` sans attribuer d’adresses IP.

---

### **3. Redémarrer dnsmasq**
Après avoir configuré le fichier, redémarrez le service pour appliquer les modifications :
```bash
sudo systemctl restart dnsmasq
```
