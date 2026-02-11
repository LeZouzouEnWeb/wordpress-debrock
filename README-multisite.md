# DEBROCK MUILTISITE

Il s'agit d'une configuration WordPress multisite basée sur Bedrock. Il comprend la configuration nécessaire pour exécuter un réseau multisite, y compris le fichier `.env.bedrock` avec les variables d'environnement requises.

## 📁 Structure du projet

```Plaintext
<Dépôt git>/
├── wp_debrock/          # Projet Bedrock
│   ├── web/             # Document root
│   │   ├── app/         # Plugins, themes, uploads
│   │   └── wp/          # WordPress core (géré par Composer)
│   ├── config/          # Configuration de l'environnement
│   ├── vendor/          # Dépendances Composer
│   └── .env             # Variables d'environnement
├── database/            # Données MariaDB persistantes
│   └── sql/             # Scripts SQL d'initialisation
├── docker-compose.yml   # Configuration Docker
└── .env                 # Variables Docker et WordPress

```

## 🔧 Commandes utiles

### Docker

```bash
# Démarrer les conteneurs
docker-compose up -d
# Arrêter les conteneurs
docker-compose down
# Voir les logs
docker-compose logs -f
# Redémarrer un service
docker-compose restart database
```

### Composer

```bash
# Installer un plugin
composer require wpackagist-plugin/nom-du-plugin
# Installer un thème
composer require wpackagist-theme/nom-du-theme
# Mettre à jour les dépendances
composer update
```

### Serveur PHP

#### Démarrer le serveur Apache avec Wampserver par exemple

- Ajouter une entrée dans le fichier `hosts` pour les sous-domaines (ex: `127.0.0.1 site1.localhost site2.localhost`)
- Configurer les hôtes virtuels Apache pour pointer vers le dossier `wp_debrock/web`
- Redémarrer Apache
- Accéder à `http://site1.localhost` ou `http://site2.localhost` pour voir les sites du réseau multisite
- Pour les sous-répertoires, accéder à `http://localhost/site1` ou `http://localhost/site2`
- Pour le domain mapping, configurer les domaines externes pour qu'ils pointent vers `localhost` et accéder à `http://site1.com` ou `http://site2.com`
- Assurez-vous que les configurations DNS et les hôtes virtuels sont correctement configurés pour le type de multisite choisi :
  - C:\wamp64\bin\apache\apacheX.X.X\conf\extra\httpd-vhosts.conf

```text-plain
<VirtualHost *:80>
    ServerName monsite.test
    ServerAlias site1.monsite.test site2.monsite.test
    DocumentRoot "C:/path/to/wp_debrock/web"
    <Directory "C:/path/to/wp_debrock/web">
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

- C:\Windows\System32\drivers\etc\hosts :

```text-plain
127.0.0.1 monsite.test
::1    monsite.test
```

- Accéder au site : http://monsite.test
- Accéder au réseau multisite : http://monsite.test/wp-admin/network
- Accéder à un site spécifique : http://monsite.test/site1 ou http://site1.monsite.test
- Accéder à l'administration d'un site : http://monsite.test/site1/wp-admin ou http://site1.monsite.test/wp-admin
- Accéder à l'administration du réseau : http://monsite.test/wp-admin/network
- Accéder à l'administration du site principal : http://monsite.test/wp-admin
- Accéder à l'administration du site secondaire : http://monsite.test/site2/wp-admin ou http://site2.monsite.test/wp-admin

## 🛠️ Configuration de config/application.php (version Bedrock)

WordPress va donner du code type :

```text-plain
define('MULTISITE', true);
define('SUBDOMAIN_INSTALL', false);
define('DOMAIN_CURRENT_SITE', 'monsite.test');
define('PATH_CURRENT_SITE', '/');
define('SITE_ID_CURRENT_SITE', 1);
define('BLOG_ID_CURRENT_SITE', 1);
```

⚠️ Sous Bedrock, il faut le remplacer par :

````text-plain
Config::define('MULTISITE', true);
Config::define('SUBDOMAIN_INSTALL', false);
Config::define('DOMAIN_CURRENT_SITE', 'monsite.test');
Config::define('PATH_CURRENT_SITE', '/');
Config::define('SITE_ID_CURRENT_SITE', 1);
Config::define('BLOG_ID_CURRENT_SITE', 1);
```text

Toujours dans application.php.


## 🛠️ Configuration de la base de données

- **Serveur** : `database`
- **Utilisateur** : `user`
- **Mot de passe** : `password`
- **Base de données** : `BedrockCMS`
- **Préfixe des tables** : `wp_`

## 🌐 Configuration multisite

- **Type de multisite** :
  1. Sous-domaines (ex: site1.monsite.test, site2.monsite.test)
  2. Sous-répertoires (ex: monsite.test/site1, monsite.test/site2)
  3. Domain mapping (ex: site1.com, site2.com pointant vers le même WordPress)
- **Domaine principal** : `monsite.test`
- **URL d'accueil** : `http://monsite.test`
- **URL du site** : `http://monsite.test/wp`
````
