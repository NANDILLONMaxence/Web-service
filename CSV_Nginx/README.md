### Documentation d'Installation, Configuration et Sécurisation de Nginx sous Debian

---

#### Introduction

Nginx est un serveur web léger, rapide et performant, connu pour sa haute capacité de gestion des connexions simultanées. Cette documentation fournit un guide complet pour l'installation, la configuration et la sécurisation de Nginx sous Debian XX.

---

#### Services de Page Web

##### Nginx Web Server

- **Description** :
  Nginx est un serveur web open-source utilisé pour servir des sites web statiques, dynamiques, et en tant que reverse proxy.

- **Fonctionnalités** :
  - Haute performance et faible utilisation des ressources
  - Gestion efficace des requêtes simultanées
  - Support des protocoles HTTP et HTTPS
  - Configuration flexible avec des blocs de serveurs et de localisation
  - Prise en charge de la réécriture d'URL et des modules tiers
  - Fonctionnalité de reverse proxy pour la mise en cache et la distribution de charge

---

### Installation de Nginx sur Debian XX

#### Étape 1 : Mise à jour du système
```bash
sudo apt update
sudo apt upgrade
```

#### Étape 2 : Installation de Nginx
```bash
sudo apt install nginx
```

#### Étape 3 : Vérification du statut de Nginx
```bash
sudo systemctl status nginx
```

---

### Configuration de Nginx

#### 1. Fichiers de Configuration Principaux
   - **/etc/nginx/nginx.conf** : Configuration globale de Nginx
   - **/etc/nginx/sites-available/** : Emplacement des fichiers de configuration des sites disponibles
   - **/etc/nginx/sites-enabled/** : Liens symboliques vers les sites actifs

#### 2. Configuration des Sites Web
   - **/etc/nginx/sites-available/** : Emplacement des fichiers de configuration des sites
   - **/etc/nginx/sites-enabled/** : Liens symboliques vers les sites actifs

#### 3. Configuration des Paramètres Généraux
   - **/etc/nginx/nginx.conf** : Définition de paramètres globaux comme les ports, les workers, etc.

#### 4. Gestion des Logs
   - **/var/log/nginx/** : Logs de Nginx, utiles pour le débogage et la surveillance

#### Exemple de Configuration de Site Web (site1.conf)
```nginx
server {
    listen 80;
    server_name example.com www.example.com;

    location / {
        root /var/www/html/example;
        index index.html index.htm;
    }

    error_page 404 /404.html;
    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
        root /var/www/html;
    }
}
```

---

### Sécurisation de Nginx

#### 1. Configuration du Pare-feu
   - Ouvrir les ports 80 (HTTP) et 443 (HTTPS)
   ```bash
   sudo ufw allow 'Nginx Full'
   ```

#### 2. Utilisation de Certificats SSL/TLS (Optionnel)
   - Utilisation de Let's Encrypt pour des certificats gratuits
   ```bash
   sudo apt install certbot python3-certbot-nginx
   sudo certbot --nginx
   ```

#### 3. Restreindre l'Accès aux Répertoires
   - Utilisation de directives dans les fichiers de configuration
   ```nginx
   location /private {
       deny all;
       return 403;
   }
   ```

#### 4. Protection contre les Attaques avec Nginx ModSecurity
   - Installation de ModSecurity pour la sécurité avancée
   ```bash
   sudo apt install libnginx-mod-security
   ```

#### 5. Mises à Jour Régulières
   - Garder le système et Nginx à jour avec les derniers correctifs de sécurité
   ```bash
   sudo apt update
   sudo apt upgrade
   ```

---

### Conclusion

Nginx est un serveur web puissant et léger, idéal pour servir des sites web à grande échelle. En suivant ce guide, vous avez installé, configuré et sécurisé Nginx sur votre système Debian XX, prêt à servir vos pages web de manière rapide, efficace et sécurisée.

---