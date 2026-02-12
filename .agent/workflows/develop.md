---
description: Workflow complet pour ajouter une nouvelle fonctionnalité (CRUD)
---

# Workflow : Développement d'une Feature CRUD

Ce workflow guide le développement d'une nouvelle fonctionnalité de bout en bout, en respectant l'architecture MVC + Services.

## 🛠️ Étapes

### 📊 1. Couche Data (Skill: developpeur-data)
1.  **Migration** : Exécuter **Action A** pour créer la table.
    - *Entrée* : `php artisan make:migration create_[table]_table`.
2.  **Model** : Exécuter **Action B** pour configurer le modèle Eloquent.
    - *Check* : `$fillable` et relations.
3.  **Data** : Exécuter **Action C** pour générer Factory et Seeder.
// turbo
4.  **Run** : `php artisan migrate --seed`.

### 🧠 2. Couche Business (Skill: developpeur-business)
1.  **Service** : Exécuter **Action A** pour créer la classe Service.
    - *Check* : Namespace `App\Services`.
2.  **Logique** : Exécuter **Action B** pour implémenter les méthodes métier.
    - *Règle* : Transactions et Exceptions.
3.  **Policy** : Exécuter **Action C** pour sécuriser l'accès.

### 🌐 3. Couche HTTP (Skill: developpeur-http)
1.  **Request** : Exécuter **Action B** pour créer la FormRequest de validation.
2.  **Controller** : Exécuter **Action A** pour créer le contrôleur CRUD.
    - *Check* : Injection du Service.
3.  **Routes** : Exécuter **Action C** pour enregistrer les routes.

### 🎨 4. Couche Frontend (Skill: developpeur-frontend)
1.  **Composants** : Exécuter **Action A** ou **B** pour préparer les éléments UI.
2.  **Vues** : Assembler la page en utilisant les composants Blade et Preline.
3.  **Interactivité** : Exécuter **Action C** pour ajouter Alpine.js si nécessaire.

## ✅ Validation Finale
1.  Tester le CRUD complet dans le navigateur.
// turbo
2.  Lancer les tests avec `php artisan test`.
3.  Vérifier le code avec Laravel Pint : `./vendor/bin/pint`.
