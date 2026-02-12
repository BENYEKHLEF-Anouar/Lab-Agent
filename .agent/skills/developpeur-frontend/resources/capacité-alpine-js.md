# Capacité : Script Alpine.js Isolé

## 🎯 Objectif
Ajouter une couche d'interactivité légère (Toggle, Tab, State) sans build complexe.

## ⚡ Règles d'Implémentation

### 1. Inline vs Externe
- **Inline** : Pour les interactions simples (`x-data="{ open: false }"`).
- **Externe** : Si logique > 5 lignes, utiliser `Alpine.data()` dans `app.js`.

### 2. Directives
- Utiliser `x-show` pour la visibilité (avec transition `x-transition`).
- Utiliser `x-model` pour la liaison de données formulaire.
- Utiliser `x-on:click` (ou `@click`) pour les événements.

## ✅ Points de Contrôle (Definition of Done)
- [ ] L'état est réactif.
- [ ] `x-cloak` est présent pour éviter le FOUC.
