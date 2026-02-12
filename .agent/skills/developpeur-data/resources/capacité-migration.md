# Capacité : Créer/Modifier Schéma (Migration)

## 🎯 Objectif
Générer une migration Laravel pour altérer la structure de la base de données de manière sécurisée et réversible.

## 📝 Format et Structure
- **Fichier Sortie** : `database/migrations/YYYY_MM_DD_HHMMSS_[action]_[table]_table.php`.

## ⚡ Règles d'Implémentation

### 1. Sécurité
- Ne pas oublier `down()`.
- Ne pas utiliser de types spécifiques non standards.

### 2. Contraintes
- Clés étrangères avec `constrained()`.
- Index sur les colonnes de recherche.

## ✅ Points de Contrôle (Definition of Done)
- [ ] Migration et Rollback sans erreur.
