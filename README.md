# Raspberry-Pi-Private-Cloud-Nextcloud-Tailscale-by-oscar
Ce projet consiste à transformer un Raspberry Pi 5 en un serveur de stockage cloud personnel sécurisé, accessible partout dans le monde sans abonnement, en utilisant Nextcloud pour la gestion des fichiers et Tailscale pour le réseau privé (VPN Mesh).

Voici un modèle de fichier README.md complet, structuré selon les standards de GitHub et adapté à votre projet Raspberry Pi + Nextcloud + Tailscale.

Vous pouvez copier ce code et le coller dans un fichier nommé README.md à la racine de votre dépôt GitHub.

Markdown
# ☁️ Mon Cloud Privé sur Raspberry Pi 5

[![Hardware](https://img.shields.io/badge/Hardware-Raspberry%20Pi%205-red)](https://www.raspberrypi.com/)
[![Software](https://img.shields.io/badge/Software-Nextcloud-blue)](https://nextcloud.com/)
[![Network](https://img.shields.io/badge/Network-Tailscale-informational)](https://tailscale.com/)

Ce projet consiste à transformer un **Raspberry Pi 5** en un serveur de stockage cloud personnel, sécurisé et accessible depuis n'importe où sans ouverture de ports (Port Forwarding), grâce à **Tailscale** et **Nextcloud**.



---

## 🛠️ Matériel Utilisé
- **Raspberry Pi 5** (Modèle 4GB ou 8GB).
- **NVMe Base/Hat** (pour des débits de lecture/écriture supérieurs à la SD).
- **SSD NVMe M.2**.
- **Alimentation 27W USB-C** officielle.
- **Refroidissement actif** (Active Cooler).

## 🚀 Fonctionnalités
- ✅ **Auto-hébergement** : Vos données restent chez vous.
- ✅ **Accès Universel** : Accès via PC, Mac, iOS et Android via Tailscale.
- ✅ **Sécurité** : Pas d'exposition sur l'internet public (VPN Mesh).
- ✅ **Performance** : Système tournant entièrement sur SSD NVMe.

---

## 📖 Guide d'Installation

### 1. Préparation du Système (OS)
Utilisez **Raspberry Pi Imager** pour installer *Raspberry Pi OS (64-bit)*. 
* Configurez le **SSH**, le **User** (`oscar`) et le **Wi-Fi** dans les options avancées.

### 2. Migration vers le SSD NVMe
Une fois connecté en SSH (`ssh oscar@oscarpi.local`), clonez votre carte SD vers le SSD pour plus de rapidité :
```bash
# Exemple via l'outil rpi-clone (version Jeff Geerling)
sudo rpi-clone nvme0n1

Configurez ensuite l'ordre de boot via sudo raspi-config (Advanced Options > Boot Order > NVMe).

3. Installation de Nextcloud
L'installation se fait via Snap pour une gestion simplifiée des dépendances :

Bash
sudo apt update && sudo apt upgrade -y
sudo apt install snapd
sudo snap install nextcloud
4. Configuration de Tailscale
Pour accéder à votre cloud en dehors de votre domicile :

Bash
curl -fsSL [https://tailscale.com/install.sh](https://tailscale.com/install.sh) | sh
sudo tailscale up
Récupérez l'adresse IP Tailscale de votre Pi (ex: 100.x.y.z) sur votre interface d'administration Tailscale.

5. Liaison Nextcloud + Tailscale
Il est impératif d'ajouter votre IP Tailscale aux domaines de confiance de Nextcloud :

Bash
sudo nextcloud.occ config:system:set trusted_domains 1 --value=VOTRE_IP_TAILSCALE
🔧 Dépannage (Logs d'erreurs rencontrées)
Erreur Wi-Fi (wpa_supplicant)
Si l'interface wlan0 refuse de se reconfigurer :

Bash
sudo killall wpa_supplicant
sudo rm /var/run/wpa_supplicant/wlan0
sudo systemctl restart NetworkManager
Erreur de Verrouillage APT
Si vous recevez l'erreur Could not open lock file /var/lib/dpkg/lock-frontend :

Vérifiez que vous utilisez bien sudo.

Attendez la fin des mises à jour automatiques au démarrage ou redémarrez.

📱 Accès Client
Installez Tailscale sur votre téléphone/ordinateur.

Connectez-vous au même compte.

Installez l'application Nextcloud et entrez l'adresse IP Tailscale de votre Raspberry Pi.

🔗 Références
Tuto Vidéo de base : Access Your Files ANYWHERE - Enrique Neyra

Documentation Nextcloud : nextcloud.com
