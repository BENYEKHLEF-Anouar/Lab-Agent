# Capacité : Créer Controller CRUD

## 🎯 Objectif
Générer un contrôleur pour manipuler une ressource via des actions standard.

## 📝 Format et Structure
- **Fichier Sortie** : `app/Http/Controllers/[Name]Controller.php`.

## ⚡ Règles d'Implémentation

### 1. Délégation
- Injecter le Service Métier.
- Ne pas mettre de logique métier dans le contrôleur.

### 2. Retour
- Retourner une Vue (`view()`) ou une Redirection (`redirect()->route()`).

## ✅ Points de Contrôle (Definition of Done)
- [ ] Route Model Binding utilisé.
- [ ] Méthodes standard implémentées (`index`, `store`, etc.).
