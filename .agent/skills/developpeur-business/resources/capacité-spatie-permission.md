# Capacité : Gérer Rôles/Permissions (Spatie Permission)

## 🎯 Objectif
Gérer les droits d'accès dynamiques via Spatie Permission.

## ⚡ Règles d'Implémentation

### 1. Assignation
- Utiliser `$user->assignRole('role_name')`.
- Utiliser `$user->givePermissionTo('permission_name')`.

### 2. Vérification
- Utiliser `$user->can('permission_name')`.
- Utiliser `@can` dans Blade.

## ✅ Points de Contrôle (Definition of Done)
- [ ] Les rôles et permissions existent en BDD (Seeder).
- [ ] Le trait `HasRoles` est sur le modèle `User`.
