# WordPress Bedrock avec Docker

Projet WordPress moderne utilisant [Bedrock](https://roots.io/bedrock/) pour une meilleure organisation, sécurité et gestion des dépendances via Composer.

## 📋 Prérequis

- **Docker** et **Docker Compose**
- **PHP** 8.4+ et **Composer**
- **Git**
- **Node.js** et **npm** (optionnel, pour les assets)

## 🚀 Installation rapide

### 1. Créer le projet Bedrock

```bash
composer create-project roots/bedrock ./wp_debrock
```

### 2. Configuration de l'environnement

Le fichier `.env` est déjà configuré avec :

- **Base de données** : MariaDB avec les paramètres par défaut
- **Variables WordPress Bedrock** : DB_NAME, DB_USER, DB_PASSWORD, DB_HOST
- **Environnement** : development
- **URLs** : WP_HOME et WP_SITEURL
- **Clés de sécurité** : Générées automatiquement

### 3. Démarrer Docker

```bash
docker-compose up -d
```

### 4. Installer les dépendances

```bash
cd wp_debrock
composer install
```

### 5. Accéder au site

- **Site WordPress** : <http://localhost:8080>
- **Admin WordPress** : <http://localhost:8080/wp/wp-admin>
- **Adminer (base de données)** : <http://localhost:8088>

## 🗄️ Configuration de la base de données

### Connexion Adminer

- **Serveur** : `database`
- **Utilisateur** : `user`
- **Mot de passe** : `password`
- **Base de données** : `BedrockCMS`

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

### Serveur PHP intégré (sans Docker)

```bash
# Se placer dans le dossier web
cd wp_debrock/web

# Lancer le serveur PHP sur le port 8000
php -S localhost:8000 -t ./wp_debrock/web

# Ou sur un autre port
php -S localhost:9000 -t ./wp_debrock/web

# Accéder au site : http://localhost:8000
```

> **Note** : Le serveur PHP intégré est pour le développement uniquement. Pour la production, utilisez Docker ou un serveur web classique (Apache/Nginx).
>
> **Astuce** : Vous pouvez aussi utiliser [Symfony CLI](https://symfony.com/download) pour lancer le serveur plus facilement :
>
> ```bash
> symfony serve -d --port=8000
> ```

### WP-CLI (dans le conteneur Bedrock)

```bash
# Se connecter au conteneur
docker exec -it bedrock_container bash

# Commandes WP-CLI
wp plugin list
wp theme list
wp db export
```

## 🔐 Sécurité

- ✅ Fichier `.env` exclu de Git (contient les secrets)
- ✅ Clés de sécurité WordPress générées automatiquement
- ✅ WordPress core séparé dans `/web/wp/`
- ✅ Variables d'environnement pour les credentials

## 🌐 Environnements

Modifier `WP_ENV` dans `.env` :

- **development** : Mode développement avec debug activé
- **staging** : Environnement de test
- **production** : Production (désactive le debug)

## 📚 Ressources

- [Documentation Bedrock](https://roots.io/bedrock/docs/)
- [Documentation WordPress](https://wordpress.org/documentation/)
- [Communauté Roots](https://discourse.roots.io/)
- [Packagist WordPress](https://wpackagist.org/)

## 📝 Licence

MIT

## 👨‍💻 Auteur

**LeZouzouEnWeb** - [GitHub](https://github.com/LeZouzouEnWeb)
