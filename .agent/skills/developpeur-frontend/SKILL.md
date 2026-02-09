---
name: developpeur-frontend
description: Crée des interfaces UI riches avec Blade, Preline UI, Alpine.js et Tailwind CSS.
---

# Skill : Développeur Frontend

## 🎯 Périmètre Global
**Mission** : Concevoir des interfaces utilisateur modernes, responsives et interactives en utilisant le stack Blade + Preline UI + Alpine.js, tout en respectant le design system Tailwind CSS.

### 🚫 Interdictions Globales (Règles d'Or)
1. **Frameworks Légers** (No Heavy JS) : Ne pas utiliser React, Vue ou Angular. Utiliser Alpine.js pour l'interactivité.
2. **Priorité Utilitaires** (Utility-First) : Toujours préférer les classes Tailwind CSS aux styles CSS personnalisés (sauf exception rare).
3. **Accessibilité** (A11y) : Toujours inclure les attributs ARIA et garantir la navigation au clavier.
4. **Cohérence UI** (Consistency) : Utiliser les composants Preline UI existants avant d'en créer de nouveaux.

---

## ⚡ Actions (Capacités Atomiques)

### Action A : Créer/Modifier Composant Blade
> **Description** : Créer un composant Blade réutilisable pour l'UI.
- **Entrées** : Nom du composant, Props nécessaires, Layout cible.
- **Sorties** : `resources/views/components/[name].blade.php`.
- **✅ Points de Contrôle (Definition of Done)** :
  - Utilise `@props` pour définir les entrées.
  - Les styles sont gérés via Tailwind CSS.
  - Utilise `{{ $attributes->merge(['class' => '...']) }}` pour la flexibilité.

### Action B : Intégrer Composant Preline UI
> **Description** : Intégrer un composant interactif de Preline UI (Modal, Dropdown, Accordion).
- **Entrées** : Type de composant, Données à afficher.
- **Sorties** : Code HTML/Blade avec attributs `data-hs-*`.
- **📝 Instructions Détaillées** :
  1. Copier la structure depuis la doc Preline.
  2. Adapter les classes Tailwind au projet.
  3. Vérifier l'initialisation JS (si nécessaire via `HSStaticMethods.autoInit()`).

### Action C : Script Alpine.js Isolé
> **Description** : Ajouter de la logique réactive légère à un élément.
- **Entrées** : État initial, Comportement souhaité.
- **Sorties** : Attributs `x-data`, `x-on`, `x-show`, etc.
- **✅ Points de Contrôle (Definition of Done)** :
  - La logique est simple et contenue dans le HTML pour les petits cas.
  - Pour la logique complexe, utiliser une fonction `Alpine.data()` dans un fichier JS séparé.

---

## 🔄 Scénarios d'Exécution (Algorithmes)

### Scénario 1 : Création d'une Vue de Liste (Index)
1. **Structure** : Utiliser un layout de base (`layouts.app`).
2. **Tableau** : Intégrer un composant de table Preline UI.
3. **Icons** : Ajouter des Lucide Icons pour les actions (Edit, Delete).
4. **Interactivité** : Ajouter des tooltips ou des dropdowns d'action via Alpine/Preline.

---

## ⚙️ Standards & Conventions
1. **Icons** : Utiliser exclusivement Lucide Icons via `<i data-lucide="[name]"></i>`.
2. **Naming** : Composants Blade en `kebab-case` (ex: `button-primary.blade.php`).
3. **Responsive** : Toujours builder "Mobile First" avec les préfixes `sm:`, `md:`, `lg:`.
