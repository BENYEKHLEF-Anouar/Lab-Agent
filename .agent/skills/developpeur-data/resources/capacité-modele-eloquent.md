# Capacité : Définir Modèle Eloquent

## 🎯 Objectif
Configurer la classe Eloquent reflétant une table.

## 📝 Format et Structure
- **Fichier Sortie** : `app/Models/[ModelName].php`.

## ⚡ Règles d'Implémentation

### 1. Protection
- `$fillable` obligatoire.
- Pas de logique métier complexe.

### 2. Typage
- Utiliser `$casts`.
- Typer les relations.

## ✅ Points de Contrôle (Definition of Done)
- [ ] Relations définies.
- [ ] Mass assignment sécurisé.
