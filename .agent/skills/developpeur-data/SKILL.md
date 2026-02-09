---
name: developpeur-data
description: Crée les Migrations, Modèles Eloquent, Factories et Seeders, et optimise les requêtes.
---

# Skill : Développeur Data

## 🎯 Périmètre Global
**Mission** : Implémenter et maintenir la couche de persistance des données (Schéma BDD, Modèles Eloquent, Seeding), en garantissant l'intégrité et la performance des requêtes.

### 🚫 Interdictions Globales (Règles d'Or)
1. **Zéro Suppression** (Never Delete) : Ne jamais supprimer ou modifier une migration déjà jouée en production -> Créer une nouvelle migration.
2. **Protection de Masse** (Mass Assignment) : Toujours protéger les modèles avec `$fillable` (whitelist) et jamais `$guarded = []`.
3. **Convention de Nommage** (Naming) : Tables en `snake_case` Pluriel, Modèles en `PascalCase` Singulier.

---

## ⚡ Actions (Capacités Atomiques)

### Action A : Créer/Modifier Schéma (Migration)
> **Description** : Générer une migration Laravel pour altérer la structure de la base de données.
- **Entrées** : Description des changements (Nouvelle table ou Colonnes à ajouter).
- **Sorties** : `database/migrations/YYYY_MM_DD_HHMMSS_[action]_[table]_table.php`.
- **❌ Interdictions Spécifiques** :
  - Ne pas oublier la méthode `down()` pour le rollback.
  - Ne pas utiliser de types non standards sans raison (ex: `json` sur MySQL 5.7).
- **✅ Points de Contrôle (Definition of Done)** :
  - La migration s'exécute (`migrate`) et se rollback (`migrate:rollback`) sans erreur.
  - Les clés étrangères ont `constrained()->onDelete('cascade')` (si approprié).
- **📝 Instructions Détaillées** :
  1. Utiliser `php artisan make:migration`.
  2. Définir le schéma dans `up()`.
  3. Vérifier les index nécessaires.

### Action B : Définir Modèle Eloquent
> **Description** : Configurer la classe Eloquent reflétant une table.
- **Entrées** : Table associée, Relations, Attributs.
- **Sorties** : `app/Models/[ModelName].php`.
- **❌ Interdictions Spécifiques** :
  - Ne pas inclure de logique métier complexe dans le modèle.
- **✅ Points de Contrôle (Definition of Done)** :
  - `$fillable` est défini.
  - `$casts` est utilisé pour les types natifs (boolean, date, array).
  - Les méthodes de relation (`hasMany`, etc.) sont typées.

### Action C : Créer Jeu de Données (Factory/Seeder)
> **Description** : Générer des données de test réalistes.
- **Entrées** : Modèle cible.
- **Sorties** : `database/factories/[Model]Factory.php`, `database/seeders/[Model]Seeder.php`.
- **✅ Points de Contrôle (Definition of Done)** :
  - La Factory utilise `fake()` pour des données variées.
  - Le Seeder est appelé dans `DatabaseSeeder.php`.

---

## 🔄 Scénarios d'Exécution (Algorithmes)

### Scénario 1 : Création d'une Nouvelle Entité
1. **Migration** : Exécuter **Action A** pour créer la table.
2. **Model** : Exécuter **Action B** pour lier le code PHP.
3. **Data** : Exécuter **Action C** pour permettre le développement avec des données.
4. **Validation** : Lancer `php artisan migrate --seed` pour vérifier la chaîne complète.

---

## ⚙️ Standards & Conventions
1. **Migrations** : Utiliser la syntaxe anonyme (`return new class extends Migration`).
2. **ID** : Utiliser `$table->id()` (BigInt Auto Increment) par défaut, ou `$table->uuid('id')` si requis.
3. **Dates** : Toujours inclure `$table->timestamps()`.