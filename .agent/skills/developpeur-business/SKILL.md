---
name: developpeur-business
description: Implémente les Services, la logique métier, et définit les Policies/Gates.
---

# Skill : Développeur Business

## 🎯 Périmètre Global
**Mission** : Encapsuler la logique métier complexe et les règles d'autorisation dans des classes dédiées (Services, Actions, Policies), garantissant l'indépendance vis-à-vis du framework HTTP.

### 🚫 Interdictions Globales (Règles d'Or)
1. **No HTTP** : Ne jamais importer `Illuminate\Http\Request` ou `Response` dans un Service.
2. **No Controller Logic** : Ne jamais écrire de logique métier dans un Contrôleur -> Déléguer au Service.
3. **Atomicité** : Utiliser des transactions DB pour toute opération impliquant plusieurs écritures.

---

## ⚡ Actions (Capacités Atomiques)

### Action A : Créer Service Métier
> **Description** : Créer une classe de Service pour encapsuler un domaine métier.
- **Entrées** : Nom du domaine (ex: `Article`), Méthodes requises.
- **Sorties** : `app/Services/[Nom]Service.php`.
- **❌ Interdictions Spécifiques** :
  - Ne pas créer de Service "Fourre-tout". Un Service = Un Domaine.
- **✅ Points de Contrôle (Definition of Done)** :
  - La classe est dans le namespace `App\Services`.
  - Les méthodes sont typées (arguments et retour).
  - Aucune dépendance à `Request` ou `Auth::user()` (passer l'user en paramètre).

### Action B : Implémenter Logique (Méthode)
> **Description** : Coder le corps d'une méthode de service (Algorithme, Transaction, Event).
- **Entrées** : Signature de la méthode, Règles de gestion.
- **Sorties** : Code PHP dans la méthode.
- **✅ Points de Contrôle (Definition of Done)** :
  - Utilisation de `DB::transaction` si modifications multiples.
  - Gestion des exceptions (`throw` si erreur métier).
  - Retourne des objets typés (DTO ou Model) et non des tableaux associatifs flous.

### Action C : Définir Policy (Autorisation)
> **Description** : Créer et implémenter une Policy pour sécuriser l'accès aux ressources.
- **Entrées** : Modèle cible (ex: `Article`).
- **Sorties** : `app/Policies/[Model]Policy.php`.
- **✅ Points de Contrôle (Definition of Done)** :
  - La Policy est enregistrée (automatique en Laravel 11 ou via AuthServiceProvider).
  - Les méthodes standard (`view`, `create`, `update`, `delete`) sont implémentées.

### Action D : Gérer Médias (Spatie MediaLibrary)
> **Description** : Ajouter la gestion des fichiers à un modèle.
- **Entrées** : Fichier uploadé, Collection cible.
- **✅ Points de Contrôle (Definition of Done)** :
  - Le modèle implémente `HasMedia` et utilise `InteractsWithMedia`.
  - Utilise `addMedia()` pour le stockage et `getFirstMediaUrl()` pour la récupération.

### Action E : Gérer Rôles/Permissions (Spatie Permission)
> **Description** : Assigner des droits à un utilisateur.
- **Entrées** : Nom du rôle ou de la permission.
- **✅ Points de Contrôle (Definition of Done)** :
  - Utilise les méthodes `$user->assignRole()` ou `$user->givePermissionTo()`.
  - Vérifie les droits via `@can` dans Blade ou `$user->can()` dans le Service.

---

## 🔄 Scénarios d'Exécution (Algorithmes)

### Scénario 1 : Implémentation d'une Feature Métier
1. **Design** : Définir l'interface du Service (`interface` ou `class` publique).
2. **Sécurité** : Créer la Policy associée au modèle manipulé via **Action C**.
3. **Logique** : Implémenter les méthodes du Service via **Action A** et **B**.

---

## ⚙️ Standards & Conventions
1. **Injection** : Préférer l'injection de dépendance dans le constructeur.
2. **Typage** : `strict_types=1` obligatoire sur tous les fichiers PHP.
3. **Nommage** : Verbe + Nom pour les méthodes (ex: `publishArticle`, `archiveUser`).