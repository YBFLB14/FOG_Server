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

---

### **3. Redémarrer dnsmasq**
Après avoir configuré le fichier, redémarrez le service pour appliquer les modifications :
```bash
sudo systemctl restart dnsmasq
```
