---
name: Preline UI Integration
description: Expert en intégration de Preline UI dans des applications Laravel avec Alpine.js et Tailwind CSS
---

# Skill: Preline UI Integration

## Description
Ce skill permet d'intégrer et d'utiliser efficacement **Preline UI**, une bibliothèque de composants Tailwind CSS pré-construits, dans des applications Laravel.

## Quand utiliser ce skill
- Installation de Preline UI dans un projet Laravel
- Création de modales, dropdowns, accordions, tabs, tooltips
- Intégration avec Alpine.js pour l'interactivité
- Debugging de composants Preline UI
- Création de composants Blade réutilisables basés sur Preline

## Installation

### Via NPM
```bash
npm install preline
```

### Configuration Tailwind
Dans `tailwind.config.js` :
```javascript
module.exports = {
  content: [
    './resources/**/*.blade.php',
    './resources/**/*.js',
    './node_modules/preline/dist/*.js',
  ],
  plugins: [
    require('preline/plugin'),
  ],
}
```

### Initialisation
Dans `resources/js/app.js` :
```javascript
import 'preline';
// Auto-initialisation des composants
```

## Composants Principaux

### 1. Modales (`data-hs-overlay`)

**Bouton déclencheur** :
```blade
<button type="button" data-hs-overlay="#modal-id" class="px-4 py-2 bg-blue-600 text-white rounded-lg">
  Ouvrir Modal
</button>
```

**Structure de la Modal** :
```blade
<div id="modal-id" class="hs-overlay hidden w-full h-full fixed top-0 left-0 z-[60] overflow-x-hidden overflow-y-auto">
  <div class="hs-overlay-open:opacity-100 hs-overlay-open:duration-500 opacity-0 transition-all sm:max-w-lg sm:w-full m-3 sm:mx-auto">
    <div class="flex flex-col bg-white border shadow-sm rounded-xl">
      <!-- Header -->
      <div class="flex justify-between items-center py-3 px-4 border-b">
        <h3 class="font-bold text-gray-800">Titre Modal</h3>
        <button type="button" data-hs-overlay-close class="inline-flex items-center justify-center">
          <i data-lucide="x" class="w-4 h-4"></i>
        </button>
      </div>
      <!-- Body -->
      <div class="p-4 overflow-y-auto">
        <p>Contenu de la modal</p>
      </div>
      <!-- Footer -->
      <div class="flex justify-end items-center gap-x-2 py-3 px-4 border-t">
        <button type="button" data-hs-overlay-close class="px-3 py-2 text-sm border rounded-lg">
          Annuler
        </button>
        <button type="button" class="px-3 py-2 text-sm bg-blue-600 text-white rounded-lg">
          Confirmer
        </button>
      </div>
    </div>
  </div>
</div>
```

**API JavaScript** :
```javascript
// Ouvrir
HSOverlay.open('#modal-id');

// Fermer
HSOverlay.close('#modal-id');
```

### 2. Dropdowns (`data-hs-dropdown`)

```blade
<div class="hs-dropdown relative inline-flex">
  <button type="button" class="hs-dropdown-toggle px-4 py-2 bg-white border rounded-lg flex items-center gap-2">
    Actions
    <i data-lucide="chevron-down" class="w-4 h-4"></i>
  </button>
  
  <div class="hs-dropdown-menu transition-[opacity,margin] duration-300 hs-dropdown-open:opacity-100 opacity-0 hidden bg-white shadow-md rounded-lg p-2 mt-2">
    <a class="flex items-center gap-x-3 py-2 px-3 rounded-lg hover:bg-gray-100" href="#">
      <i data-lucide="edit" class="w-4 h-4"></i>
      Éditer
    </a>
    <a class="flex items-center gap-x-3 py-2 px-3 rounded-lg hover:bg-gray-100" href="#">
      <i data-lucide="trash-2" class="w-4 h-4"></i>
      Supprimer
    </a>
  </div>
</div>
```

### 3. Accordions (`data-hs-accordion`)

```blade
<div class="hs-accordion-group">
  <div class="hs-accordion active" id="accordion-1">
    <button class="hs-accordion-toggle py-3 inline-flex items-center gap-x-3 w-full font-semibold text-left">
      <i data-lucide="chevron-right" class="hs-accordion-active:rotate-90 w-4 h-4"></i>
      Section 1
    </button>
    <div class="hs-accordion-content w-full overflow-hidden transition-[height] duration-300">
      <p class="text-gray-600">Contenu de la section 1</p>
    </div>
  </div>
</div>
```

### 4. Tabs (`data-hs-tab`)

```blade
<div class="border-b border-gray-200">
  <nav class="flex space-x-2" role="tablist">
    <button type="button" class="hs-tab-active:border-blue-600 hs-tab-active:text-blue-600 py-4 px-1 inline-flex items-center gap-2 border-b-2 border-transparent active" data-hs-tab="#tab-1" role="tab">
      Tab 1
    </button>
    <button type="button" class="hs-tab-active:border-blue-600 hs-tab-active:text-blue-600 py-4 px-1 inline-flex items-center gap-2 border-b-2 border-transparent" data-hs-tab="#tab-2" role="tab">
      Tab 2
    </button>
  </nav>
</div>

<div class="mt-3">
  <div id="tab-1" role="tabpanel">
    <p>Contenu Tab 1</p>
  </div>
  <div id="tab-2" class="hidden" role="tabpanel">
    <p>Contenu Tab 2</p>
  </div>
</div>
```

### 5. Tooltips (`data-hs-tooltip`)

```blade
<div class="hs-tooltip inline-block">
  <button type="button" class="hs-tooltip-toggle">
    <i data-lucide="info" class="w-4 h-4"></i>
  </button>
  <span class="hs-tooltip-content hs-tooltip-shown:opacity-100 hs-tooltip-shown:visible opacity-0 transition-opacity inline-block absolute invisible z-10 py-1 px-2 bg-gray-900 text-xs font-medium text-white rounded shadow-sm" role="tooltip">
    Information utile
  </span>
</div>
```

## Intégration avec Alpine.js

### Modal avec données dynamiques
```blade
<div x-data="articleModal()">
  <button @click="openModal(1)" data-hs-overlay="#edit-modal">
    Éditer
  </button>
  
  <div id="edit-modal" class="hs-overlay hidden">
    <div class="...">
      <input type="text" x-model="form.title">
      <textarea x-model="form.content"></textarea>
    </div>
  </div>
</div>

<script>
function articleModal() {
  return {
    form: { title: '', content: '' },
    
    async openModal(id) {
      const response = await fetch(`/api/articles/${id}`);
      this.form = await response.json();
      HSOverlay.open('#edit-modal');
    }
  }
}
</script>
```

### Dropdown avec état Alpine
```blade
<div x-data="{ selected: null }" class="hs-dropdown">
  <button class="hs-dropdown-toggle">
    <span x-text="selected || 'Sélectionner'"></span>
  </button>
  <div class="hs-dropdown-menu">
    <a @click="selected = 'Option 1'" href="#">Option 1</a>
    <a @click="selected = 'Option 2'" href="#">Option 2</a>
  </div>
</div>
```

## Composants Blade Réutilisables

### Modal Component
Créer `resources/views/components/preline/modal.blade.php` :
```blade
@props(['id', 'title'])

<div id="{{ $id }}" class="hs-overlay hidden w-full h-full fixed top-0 left-0 z-[60] overflow-x-hidden overflow-y-auto">
  <div class="hs-overlay-open:opacity-100 hs-overlay-open:duration-500 opacity-0 transition-all sm:max-w-lg sm:w-full m-3 sm:mx-auto">
    <div class="flex flex-col bg-white border shadow-sm rounded-xl">
      <div class="flex justify-between items-center py-3 px-4 border-b">
        <h3 class="font-bold text-gray-800">{{ $title }}</h3>
        <button type="button" data-hs-overlay-close>
          <i data-lucide="x" class="w-4 h-4"></i>
        </button>
      </div>
      <div class="p-4 overflow-y-auto">
        {{ $slot }}
      </div>
      @isset($footer)
        <div class="flex justify-end items-center gap-x-2 py-3 px-4 border-t">
          {{ $footer }}
        </div>
      @endisset
    </div>
  </div>
</div>
```

Usage :
```blade
<x-preline.modal id="my-modal" title="Mon Modèle">
  <p>Contenu de la modal</p>
  
  <x-slot:footer>
    <button data-hs-overlay-close>Annuler</button>
    <button>Confirmer</button>
  </x-slot:footer>
</x-preline.modal>
```

## Personnalisation

### Thème Custom
Dans `resources/css/app.css` :
```css
@layer components {
  .hs-overlay {
    @apply backdrop-blur-sm;
  }
  
  .hs-dropdown-menu {
    @apply shadow-xl border border-gray-100;
  }
  
  .hs-accordion-active {
    @apply text-blue-600;
  }
}
```

### Dark Mode
```blade
<div class="hs-dropdown-menu bg-white dark:bg-gray-800 text-gray-900 dark:text-white">
  <!-- Contenu -->
</div>
```

## Debugging

### Vérifier l'initialisation
```javascript
console.log('Preline loaded:', typeof HSOverlay !== 'undefined');
console.log('Preline methods:', window.HSStaticMethods);
```

### Réinitialiser après AJAX
```javascript
// Après insertion de HTML dynamique
document.getElementById('container').innerHTML = newHTML;
window.HSStaticMethods.autoInit();
```

## Erreurs Courantes

### 1. Modal ne s'ouvre pas
**Problème** : `data-hs-overlay` et l'ID ne correspondent pas
**Solution** : Vérifier que `data-hs-overlay="#modal-id"` correspond à `id="modal-id"`

### 2. Styles manquants
**Problème** : Preline non inclus dans Tailwind config
**Solution** : Vérifier `tailwind.config.js` et inclure `./node_modules/preline/dist/*.js`

### 3. Icônes ne s'affichent pas
**Problème** : Lucide non initialisé
**Solution** : Appeler `createIcons()` après le chargement du DOM

### 4. Conflits Alpine
**Problème** : Incompatibilité de version
**Solution** : Utiliser Alpine.js v3+ (compatible avec Preline)

## Best Practices

1. **Toujours utiliser Lucide Icons** dans les composants Preline
2. **Créer des composants Blade** pour les patterns répétitifs
3. **Utiliser Alpine.js** pour la logique dynamique
4. **Tester sur mobile** (tous les composants sont responsive)
5. **Accessibility** : Ajouter `aria-label` sur les boutons icon-only

## Ressources
- Documentation officielle : https://preline.co/docs
- Exemples : https://preline.co/examples
- GitHub : https://github.com/htmlstreamofficial/preline
