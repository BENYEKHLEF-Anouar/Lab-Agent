# Capacité : Définir Policy (Autorisation)

## 🎯 Objectif
Sécuriser l'accès aux ressources via les Policies Laravel standard.

## 📝 Format et Structure
- **Fichier Sortie** : `app/Policies/[Model]Policy.php`.

## ⚡ Règles d'Implémentation

### 1. Mapping CRUD
- Implémenter `viewAny`, `view`, `create`, `update`, `delete`.
- Retourner `true`/`false`.

### 2. Admin
- Gérer le super-admin via `before()`.

## ✅ Points de Contrôle (Definition of Done)
- [ ] La Policy est enregistrée.
- [ ] Les règles sont logiques et sécurisées.
