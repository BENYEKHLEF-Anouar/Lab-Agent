---
name: developpeur-data
description: Crée les Migrations, Modèles Eloquent, Factories et Seeders, et optimise les requêtes.
---

# Skill : Développeur Data

## 🎯 Périmètre Global
**Mission** : Implémenter et maintenir la couche de persistance des données (Schéma BDD, Modèles Eloquent, Seeding), en garantissant l'intégrité et la performance des requêtes.

### 🚫 Interdictions Globales (Règles d'Or)
1. **Zéro Suppression** : Ne jamais supprimer ou modifier une migration déjà jouée en production.
2. **Protection de Masse** : Toujours protéger les modèles avec `$fillable` et jamais `$guarded = []`.
3. **Convention de Nommage** : Tables en `snake_case` Pluriel, Modèles en `PascalCase` Singulier.

---

## ⚡ Actions (Capacités Atomiques)

### Action A : Créer/Modifier Schéma (Migration)
> **Description** : Générer une migration Laravel pour altérer la structure de la base de données.
> **Capacité** : Voir `resources/capacité-migration.md`.
- **Entrées** : Description des changements.
- **Sorties** : `database/migrations/[timestamp]_[action]_[table].php`.
- **✅ Points de Contrôle** : `up()` et `down()` valides.

### Action B : Définir Modèle Eloquent
> **Description** : Configurer la classe Eloquent reflétant une table.
> **Capacité** : Voir `resources/capacité-modele-eloquent.md`.
- **Entrées** : Table, Relations, Attributs.
- **Sorties** : `app/Models/[ModelName].php`.
- **✅ Points de Contrôle** : `$fillable`, `$casts`.

### Action C : Créer Jeu de Données (Seeder via CSV)
> **Description** : Peupler la base de données avec des données réelles importées depuis des fichiers CSV.
> **Capacité** : Voir `resources/capacité-jeu-donnees.md`.
> **🚫 Interdiction** : Ne pas utiliser de `Factory` ni de fausses données (`Faker`). Utiliser exclusivement des fichiers CSV.
- **Entrées** : Fichier CSV source (`database/data/*.csv`).
- **Sorties** : `database/seeders/[Model]Seeder.php`.
- **✅ Points de Contrôle** : `fopen()`, `fgetcsv()`, `create()`.

---

## 🔄 Scénarios d'Exécution (Algorithmes)

### Scénario 1 : Création d'une Nouvelle Entité
1. **Migration** : Exécuter **Action A**.
2. **Model** : Exécuter **Action B**.
3. **Data** : Exécuter **Action C** (Import CSV).
4. **Validation** : `migrate --seed`.

---

## ⚙️ Standards & Conventions
1. **Migrations** : Syntaxe anonyme.
2. **ID** : `$table->id()`.
3. **Dates** : `$table->timestamps()`.