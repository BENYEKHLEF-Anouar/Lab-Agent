---
name: developpeur-frontend
description: Crée des interfaces UI riches avec Blade, Preline UI, Alpine.js et Tailwind CSS.
---

# Skill : Développeur Frontend

## 🎯 Périmètre Global
**Mission** : Concevoir des interfaces utilisateur modernes, responsives et interactives en utilisant le stack Blade + Preline UI + Alpine.js, tout en respectant le design system Tailwind CSS.

### 🚫 Interdictions Globales (Règles d'Or)
1. **Frameworks Légers** : Ne pas utiliser React, Vue ou Angular. Utiliser Alpine.js pour l'interactivité.
2. **Priorité Utilitaires** : Toujours préférer les classes Tailwind CSS aux styles CSS personnalisés.
3. **Cohérence UI** : Utiliser les composants Preline UI existants avant d'en créer de nouveaux.

---

## ⚡ Actions (Capacités Atomiques)

### Action A : Créer/Modifier Composant Blade
> **Description** : Créer un composant Blade réutilisable pour l'UI.
> **Capacité** : Voir `resources/capacité-composant-blade.md` pour les règles détaillées.
- **Entrées** : Nom du composant, Props nécessaires, Layout cible.
- **Sorties** : `resources/views/components/[name].blade.php`.
- **✅ Points de Contrôle (Definition of Done)** :
  - Utilise `@props`.
  - Flexibilité via `$attributes`.

### Action B : Intégrer Composant Preline UI
> **Description** : Intégrer un composant interactif de Preline UI (Modal, Dropdown, Accordion).
> **Capacité** : Voir `resources/capacité-preline-ui.md` pour les règles détaillées.
- **Entrées** : Type de composant, Données à afficher.
- **Sorties** : Code HTML/Blade avec attributs `data-hs-*`.
- **✅ Points de Contrôle (Definition of Done)** :
  - Structure HTML conforme à Preline.
  - Initialisation JS gérée.

### Action C : Script Alpine.js Isolé
> **Description** : Ajouter de la logique réactive légère à un élément.
> **Capacité** : Voir `resources/capacité-alpine-js.md` pour les règles détaillées.
- **Entrées** : État initial, Comportement souhaité.
- **Sorties** : Attributs `x-data`, `x-on`.
- **✅ Points de Contrôle (Definition of Done)** :
  - Logique simple ou externalisée si complexe.
  - `x-cloak` utilisé.

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
2. **Naming** : Composants Blade en `kebab-case`.
3. **Responsive** : Mobile First (`sm:`, `md:`, `lg:`).
