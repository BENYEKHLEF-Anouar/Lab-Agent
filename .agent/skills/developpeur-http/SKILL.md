---
name: developpeur-http
description: Gère les Routes, Controllers, et FormRequests pour orchestrer les requêtes.
---

# Skill : Développeur HTTP

## 🎯 Périmètre Global
**Mission** : Orchestrer les requêtes entrantes, valider les données utilisateurs, et retourner les réponses (HTML ou JSON) en déléguant la logique métier aux Services.

### 🚫 Interdictions Globales (Règles d'Or)
1. **Contrôleurs Fins** (No Fat Controllers) : Un contrôleur ne doit jamais contenir de logique métier ou de requêtes Eloquent complexes.
2. **Validation Obligatoire** (Mandatory Validation) : Ne jamais traiter d'input sans passer par une FormRequest.
3. **Sécurité Prioritaire** (Security First) : Toujours vérifier les autorisations (Policies) avant de traiter une action.

---

## ⚡ Actions (Capacités Atomiques)

### Action A : Créer Controller CRUD
> **Description** : Générer un contrôleur pour une ressource.
- **Entrées** : Nom de la ressource (ex: `Article`).
- **Sorties** : `app/Http/Controllers/[Name]Controller.php`.
- **✅ Points de Contrôle (Definition of Done)** :
  - Utilise le Route Model Binding.
  - Injecte le Service correspondant dans les méthodes nécessaires.
  - Retourne des vues Blade ou des Redirects avec messages flash.

### Action B : Créer FormRequest
> **Description** : Créer une classe de validation pour une requête.
- **Entrées** : Règles de validation.
- **Sorties** : `app/Http/Requests/[Name]Request.php`.
- **✅ Points de Contrôle (Definition of Done)** :
  - La méthode `authorize()` retourne un test de Policy (ex: `$this->user()->can(...)`).
  - Les règles sont complètes et les messages d'erreur sont personnalisés si nécessaire.

### Action C : Définir Routes
> **Description** : Enregistrer les routes dans le fichier approprié.
- **Entrées** : Verbe HTTP, URI, Action du contrôleur.
- **Sorties** : `routes/web.php` ou `routes/api.php`.
- **✅ Points de Contrôle (Definition of Done)** :
  - Utilise les routes nommées (`->name('...')`).
  - Groupe les routes par middleware (auth, admin) ou par préfixe.

---

## 🔄 Scénarios d'Exécution (Algorithmes)

### Scénario 1 : Ajout d'une Route CRUD complète
1. **Route** : Ajouter `Route::resource()` ou les routes individuelles.
2. **Request** : Créer les FormRequests pour `store` et `update`.
3. **Controller** : Implémenter les méthodes en appelant le Service.
4. **Auth** : Appliquer le middleware ou vérifier la Policy.

---

## ⚙️ Standards & Conventions
1. **Naming** : Contrôleurs au singulier + suffixe `Controller` (ex: `ArticleController`).
2. **Structure** : Garder les méthodes dans l'ordre standard : `index`, `create`, `store`, `show`, `edit`, `update`, `destroy`.
