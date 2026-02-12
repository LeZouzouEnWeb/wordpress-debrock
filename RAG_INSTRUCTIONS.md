# 📦 Projet Thèmes WordPress – Corbisier.fr

Ce document définit les règles officielles et obligatoires de développement des thèmes WordPress CorbiDev destinés aux environnements WordPress multisite. 👉 Remplace toute version orientée plugins. 👉 Spécifique aux thèmes WordPress uniquement. 👉 Aucune référence à d'autres projets ou conversations n'est autorisée.

---

## 🎯 Objectifs du projet

Centraliser l'ensemble des thèmes WordPress CorbiDev · Garantir une cohérence technique, fonctionnelle et métier · Imposer une convention de nommage stricte · Faciliter la maintenance, l'évolution et la réutilisation du code.

---

## ❗ Règles obligatoires (non négociables)

### Nature du projet

Thèmes WordPress exclusivement. ❌ Aucun comportement de plugin. ❌ Aucun hook métier générique hors contexte thème.

### Fichiers WordPress obligatoires

Chaque thème doit contenir : `style.css` (en-tête WordPress obligatoire), `functions.php`, `header.php`, `footer.php`. L'absence de l'un de ces fichiers rend le thème non conforme.

---

## 🧠 Séparation des responsabilités

Séparation stricte entre : 🧠 logique métier (PHP pur, services) · 🌍 internationalisation · 🎨 rendu (templates, HTML) · 🧩 langages (PHP, HTML, CSS, JS).

### Architecture & code

Utilisation exclusive de classes pour la logique. ❌ Aucune logique métier dans `header.php`, `footer.php`, `page.php`, `single.php`, etc. Les templates consomment uniquement des données.

---

## 🎨 CSS & Front

Utilisation obligatoire de Vite, Vue et Tailwind CSS.
⚠️ Interdit :
`<script src="https://cdn.tailwindcss.com"></script>`

Je ne veux que des components.
Je ne veux pas de class tailwind directement dans les vues, sauf cas particuliers (1 à 3 class maxi suffisent pour l'élément)
Cette règle vaut pour tout.

---

## 🧩 Convention de nommage

Format obligatoire : `wp-corbidev-****-theme` (\*\*\*\* = sous-domaine). Exemples : `music.corbisier.fr` → `wp-corbidev-music-theme` · site principal → `wp-corbidev-corbisier-theme`.

---

## 📝 En-tête standard obligatoire (`style.css`)

exemple :

```css
/*
Theme Name: CorbiDev – **** Theme
Theme URI: https://github.com/CorbiDev/wp-corbidev-****-theme
Author: CorbiDev
Author URI: https://github.com/CorbiDev
Description: Thème WordPress CorbiDev.
Version: 1.0.0
Requires at least: 6.0
Tested up to: 6.5
Requires PHP: 8.4
Text Domain: corbidevtheme
*/
```

---

## 🌍 Séparation Langue / Métier – Architecture

```
wp-corbidev-nom-du-theme/
├── assets/{css,js,images,icons}
├── includes/{core,services,helpers}
├── languages
├── templates/{parts,layouts}
├── functions.php
├── header.php
├── footer.php
├── index.php
├── style.css
└── readme.md
```

❌ Aucun dossier `public`.

---

## 🧠 Logique métier

❌ Aucune chaîne affichable · ❌ Aucun HTML · ❌ Aucun appel direct à `_e()` ou `__()` · ✅ PHP métier uniquement (services, règles, traitements).

---

## 🌐 Internationalisation (i18n)

Tous les textes affichés doivent être **en anglais**. ❌ Aucun texte visible en français (front ou admin). L'i18n sert uniquement à la localisation future. Fonctions obligatoires : `__()`, `_e()`, `esc_html__()`. Traductions dans `/languages` (`.po` / `.mo`).

---

## 🧪 Bonnes pratiques générales

Toutes les classes, méthodes, fonctions et fichiers sont commentés. Commentaires en **français**, noms techniques en **anglais**, PHPDoc / JSDoc obligatoires. Compatible WordPress classique & Bedrock · Accès sécurisés par rôles · Versionnement sémantique · Code clair et maintenable.

---

## 🔒 Anti-régression

❌ Chaînes en dur interdites (`echo 'string'`). Toute sortie doit passer par i18n.  
CI : détection du français (`grep -R "[àâçéèêëîïôûù]" .`).

---

## 🧩 Templates de référence

### header.php

```php
<?php if (!defined('ABSPATH')) exit; ?><!DOCTYPE html>
<html <?php language_attributes(); ?>><head>
<meta charset="<?php bloginfo('charset'); ?>">
<meta name="viewport" content="width=device-width, initial-scale=1">
<?php wp_head(); ?></head>
<body <?php body_class(); ?>><?php wp_body_open(); ?>
```

### footer.php

```php
<?php if (!defined('ABSPATH')) exit; ?>
<?php wp_footer(); ?></body></html>
```

---

## 🔐 Fichiers interdits

`wp-config.php`, `composer.lock`, `.env`, `.htaccess`, configs serveur, scripts d'installation · dossiers `public/`, `node_modules/`, `vendor/`, `tests/`, `scripts/`.

---

## 🧱 Theme Parent

Le thème Starter (zip en pièce jointe) est le parent des autres thèmes.
C'est le seul et unique thème parent

---

## 🧪 Checklist avant merge

Structure conforme · Textes en anglais · Aucune chaîne en dur · Logique en classes · Commentaires complets

---

## 📌 Règle finale

> Toute décision ou implémentation doit provenir exclusivement de ce projet. Toute référence externe est interdite.
> Tu n'as pas le droits de modifier des fichiers des zip sans me le dire, ni pourquoi pour éviter toute régression. Tu dois toujours te référer uniquement aux derniers zip envoyé. Si absent, prendre celui du projet.
> Par simplicité , et sauf demande strict, tu ne zip que les dossiers et fichiers (complet) ayant subit une modification.

✍️ **Auteur : CorbiDev** · 🔗 https://github.com/CorbiDev
