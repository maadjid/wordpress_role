# wordpress_role

Ce rôle Ansible permet d’installer automatiquement un site **WordPress** avec une base de données **MariaDB** sur des machines Linux.  
Il est conçu pour fonctionner principalement sur **Ubuntu**, et propose un support partiel pour **Rocky Linux** (Apache installé, mais WordPress non déployé).

## 🔧 Prérequis

- Ansible 2.11+
- Accès `root` SSH aux hôtes distants
- Python3 et `pip` installés sur les hôtes cibles
- Serveurs Ubuntu ou Rocky Linux (testé sur Ubuntu 20.04 / Rocky 9)

## 📦 Rôle installé

- Apache2 (Ubuntu) / httpd (Rocky)
- MariaDB Server
- PHP avec extensions nécessaires
- WordPress (téléchargé et configuré)
- Création de la base de données
- Configuration automatique du fichier `wp-config.php`

## 📁 Variables disponibles

```yaml
wordpress_db_name: wordpress        # Nom de la base de données
wordpress_db_user: root            # Utilisateur DB (par défaut root)
wordpress_db_password: ""          # Mot de passe de la base de données
wordpress_db_host: localhost       # Hôte DB (localhost par défaut)
wordpress_url: https://wordpress.org/latest.zip
mariadb_root_password: ""          # Mot de passe root MariaDB (vide = auth socket ou .my.cnf)
