---
name: developpeur-http
description: Gère les Routes, Controllers, et FormRequests pour orchestrer les requêtes.
---

# Skill : Développeur HTTP

## 🎯 Périmètre Global
**Mission** : Orchestrer les requêtes entrantes, valider les données utilisateurs, et retourner les réponses (HTML ou JSON) en déléguant la logique métier aux Services.

### 🚫 Interdictions Globales (Règles d'Or)
1. **Contrôleurs Fins** : Un contrôleur ne doit jamais contenir de logique métier.
2. **Validation Obligatoire** : Ne jamais traiter d'input sans passer par une FormRequest.
3. **Sécurité Prioritaire** : Toujours vérifier les autorisations (Policies).

---

## ⚡ Actions (Capacités Atomiques)

### Action A : Créer Controller CRUD
> **Description** : Générer un contrôleur pour une ressource.
> **Capacité** : Voir `resources/capacité-controller-crud.md`.
- **Entrées** : Nom de la ressource.
- **Sorties** : `app/Http/Controllers/[Name]Controller.php`.
- **✅ Points de Contrôle** : Injection Service, Retour Vue/Redirect.

### Action B : Créer FormRequest
> **Description** : Créer une classe de validation pour une requête.
> **Capacité** : Voir `resources/capacité-form-request.md`.
- **Entrées** : Règles.
- **Sorties** : `app/Http/Requests/[Name]Request.php`.
- **✅ Points de Contrôle** : `authorize()` implémenté.

### Action C : Définir Routes
> **Description** : Enregistrer les routes.
> **Capacité** : Voir `resources/capacité-routes.md`.
- **Entrées** : Verbe, URI, Action.
- **Sorties** : `routes/web.php` ou `api.php`.
- **✅ Points de Contrôle** : Routes nommées.

---

## 🔄 Scénarios d'Exécution (Algorithmes)

### Scénario 1 : Ajout d'une Route CRUD complète
1. **Route** : Action C.
2. **Request** : Action B.
3. **Controller** : Action A.

---

## ⚙️ Standards & Conventions
1. **Naming** : Suffixe `Controller`.
2. **Structure** : Ordre standard CRUD.
