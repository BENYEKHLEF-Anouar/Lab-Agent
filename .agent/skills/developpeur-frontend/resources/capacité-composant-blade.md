# Capacité : Créer/Modifier Composant Blade

## 🎯 Objectif
Créer un composant Blade réutilisable pour structurer l'interface utilisateur.

## 📝 Format et Structure
- **Fichier Sortie** : `resources/views/components/[name].blade.php`.

## ⚡ Règles d'Implémentation

### 1. Props et Attributs
- Utiliser `@props(['label', 'type' => 'text'])` pour définir les entrées avec valeurs par défaut.
- Utiliser `{{ $attributes->merge(['class' => '...']) }}` pour permettre l'ajout de classes depuis l'appelant.

### 2. Styles (Tailwind CSS)
- Définir les classes utilitaires directement dans le HTML.
- Utiliser `@class([])` pour les classes conditionnelles complexes.

## ✅ Points de Contrôle (Definition of Done)
- [ ] Le composant est autonome.
- [ ] Il accepte des attributs arbitraires (`$attributes`).
- [ ] Les props sont typées ou ont des défauts.
