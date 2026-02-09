---
description: Workflow complet pour ajouter une nouvelle fonctionnalité (CRUD)
---

# Workflow : Développement d'une Feature CRUD

Ce workflow guide le développement d'une nouvelle fonctionnalité de bout en bout, en respectant l'architecture MVC + Services.

## 🛠️ Étapes

### 📊 1. Couche Data (Skill: developpeur-data)
1.  **Migration** : Créer la table avec `php artisan make:migration`.
    - Définir les types, index et contraintes.
2.  **Model** : Créer le modèle Eloquent avec `$fillable` et relations.
3.  **Data** : Optionnel - Créer Factory et Seeder pour les tests.
// turbo
4.  **Run** : `php artisan migrate`.

### 🧠 2. Couche Business (Skill: developpeur-business)
1.  **Service** : Créer `app/Services/[Name]Service.php`.
    - Implémenter la logique de création, mise à jour, suppression.
    - Utiliser des transactions DB si nécessaire.
2.  **Policy** : Créer la Policy pour sécuriser les actions.

### 🌐 3. Couche HTTP (Skill: developpeur-http)
1.  **Request** : Créer les FormRequests pour la validation.
2.  **Controller** : Créer le contrôleur qui appelle le Service.
3.  **Routes** : Enregistrer les routes dans `web.php`.

### 🎨 4. Couche Frontend (Skill: developpeur-frontend)
1.  **Vues** : Créer les fichiers Blade dans `resources/views/[name]/`.
    - Utiliser les composants Preline UI.
    - Ajouter l'interactivité avec Alpine.js.
2.  **Icons** : Intégrer Lucide Icons.

## ✅ Validation Finale
1.  Tester le CRUD complet dans le navigateur.
// turbo
2.  Lancer les tests avec `php artisan test`.
3.  Vérifier le code avec Laravel Pint : `./vendor/bin/pint`.
