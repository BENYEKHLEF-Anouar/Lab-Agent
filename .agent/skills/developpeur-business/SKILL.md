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
> **Capacité** : Voir `resources/capacité-service.md`.
- **Entrées** : Nom du domaine, Méthodes.
- **Sorties** : `app/Services/[Nom]Service.php`.
- **✅ Points de Contrôle** : Namespace `App\Services`.

### Action B : Implémenter Logique (Méthode)
> **Description** : Coder le corps d'une méthode de service.
> **Capacité** : Voir `resources/capacité-logique.md`.
- **Entrées** : Signature, Règles.
- **Sorties** : Code PHP.
- **✅ Points de Contrôle** : Transaction, Exceptions.

### Action C : Définir Policy (Autorisation)
> **Description** : Créer et implémenter une Policy.
> **Capacité** : Voir `resources/capacité-policy.md`.
- **Entrées** : Modèle cible.
- **Sorties** : `app/Policies/[Model]Policy.php`.

### Action D : Gérer Rôles/Permissions (Spatie Permission)
> **Description** : Assigner des droits à un utilisateur.
> **Capacité** : Voir `resources/capacité-spatie-permission.md`.
- **Entrées** : Rôle, Permission.
- **✅ Points de Contrôle** : `HasRoles` implémenté.

---

## 🔄 Scénarios d'Exécution (Algorithmes)

### Scénario 1 : Implémentation d'une Feature Métier
1. **Design** : Définir l'interface du Service.
2. **Sécurité** : Créer la Policy via **Action C**.
3. **Logique** : Implémenter via **Action A** et **B**.

---

## ⚙️ Standards & Conventions
1. **Injection** : Constructeur.
2. **Typage** : `strict_types=1`.
3. **Nommage** : Verbe + Nom.