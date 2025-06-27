# Ansible Role: k3d

Ce rôle Ansible permet de **déployer automatiquement un cluster K3d (K3s in Docker)** avec **NGINX** sur une machine locale.  
Il installe `docker`, `k3d`, `kubectl`, crée un cluster `k3d-lab`, et applique un manifest Kubernetes exposant un service NGINX.

## 📦 Prérequis

Avant d'utiliser ce rôle, assurez-vous que :

- 🐧 Vous êtes sur un système **Linux (de préférence Ubuntu/Debian)**
- 🔧 Vous avez `sudo` configuré **sans mot de passe** (nécessaire pour Ansible sans prompt)
- 🐍 Vous avez **Python 3** installé
- 🔧 Vous avez installé **Ansible** (≥ 2.9)

### Installation des outils nécessaires :

```bash
sudo apt update
sudo apt install -y ansible curl python3-pip
pip3 install --user docker

🧾 Variables

Aucune variable obligatoire à ce jour. Les noms et ports sont fixés dans les tâches (modifiable dans les fichiers si besoin) :
Nom de la variable	Description	Valeur par défaut
k3d_cluster_name	Nom du cluster k3d	k3d-lab
nginx_port	Port NodePort exposé pour NGINX	30080
🛠️ Rôle utilisé dans un playbook

- name: Déploiement du cluster k3d avec NGINX
  hosts: localhost
  become: true
  roles:
    - maadjid.k3d

🧪 Exemple d'exécution

ansible-playbook test-k3d.yaml

🧠 Tâches réalisées par le rôle

    Installation de Docker

    Installation de k3d

    Installation de kubectl

    Création du cluster k3d s’il n’existe pas

    Copie d’un manifest nginx.yaml

    Application du manifest

    Le service nginx est exposé sur le port 30080

❗ Erreurs fréquentes
Erreur	Cause probable	Solution
sudo: a password is required	Ansible ne peut pas exécuter sudo sans mot de passe	Ajouter prenom ALL=(ALL) NOPASSWD:ALL dans sudo visudo
Empty reply from server	Le service NGINX est mal exposé ou le manifest incorrect	Vérifier le port 30080, le manifest YAML, et les pods
No context exists with name "k3d-lab"	kubectl ne trouve pas le contexte	Lancer kubectl config get-contexts et utiliser le bon avec use-context
provided hosts list is empty	Inventaire Ansible manquant	Ajouter -i localhost, dans la commande ou créer un fichier hosts
🔁 Test manuel du cluster

k3d cluster list
kubectl config use-context k3d-k3d-lab
kubectl get nodes
kubectl get pods
curl http://localhost:30080