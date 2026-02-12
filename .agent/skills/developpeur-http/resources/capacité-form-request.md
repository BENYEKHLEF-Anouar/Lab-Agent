# Capacité : Créer FormRequest

## 🎯 Objectif
Valider et autoriser les données entrantes avant le contrôleur.

## 📝 Format et Structure
- **Fichier Sortie** : `app/Http/Requests/[Name]Request.php`.

## ⚡ Règles d'Implémentation

### 1. Autorisation
- `authorize()` doit vérifier les permissions (via Policy).

### 2. Validation
- Règles explicites dans `rules()`.
- Messages personnalisés si besoin.

## ✅ Points de Contrôle (Definition of Done)
- [ ] Règles complètes.
- [ ] Autorisation non vide (`true` ou check réel).
