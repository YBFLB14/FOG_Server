# Déploiement d'OS avec PXE

## **Introduction**

Ce projet détaille l'installation et la configuration de **FOG**, une solution open-source pour déployer des systèmes d'exploitation sur plusieurs ordinateurs via le réseau. **FOG** utilise la technologie **PXE** (Preboot eXecution Environment) pour permettre aux machines clientes de démarrer sur le réseau, télécharger une image système et l’installer automatiquement. Il permet d'éviter d'utiliser des supports physiques comme des clés USB.

---

## **Objectifs**
1. **Simplifier le déploiement d’OS** : Standardiser et accélérer l'installation des systèmes sur plusieurs machines.
2. **Automatiser les processus** : Centraliser la capture et le déploiement des images via PXE.
3. **Optimiser la gestion IT** : Inventorier les machines et sauvegarder les configurations pour des restaurations rapides.

---

## **Fonctionnalités principales**
- **Déploiement centralisé** : Installation rapide via le réseau.
- **Capture d’images systèmes** : Sauvegarde de configurations existantes.
- **Support BIOS et UEFI** : Compatibilité large avec divers matériels.
- **Inventaire matériel** : Suivi des configurations matérielles des clients.

---

## **Technologies**
- **FOG** : Gestion des déploiements.
- **MySQL** : Stockage des données (machines, tâches).
- **Apache** : Interface web.
- **TFTP, NFS** : Transferts de fichiers et partage des images.

---

### **Utilisation**
1. Installez et configurez FOG en suivant la documentation officielle.
2. Configurez les machines pour démarrer via PXE.
3. Capturez ou déployez les images selon vos besoins.
