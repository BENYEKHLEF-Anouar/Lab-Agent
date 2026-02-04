---
name: Lucide Icons
description: Expert en utilisation de Lucide Icons dans des applications Laravel avec Alpine.js
---

# Skill: Lucide Icons

## Description
Ce skill permet d'intégrer et d'utiliser efficacement **Lucide Icons**, une bibliothèque d'icônes modernes open-source, dans des applications Laravel.

## Quand utiliser ce skill
- Installation de Lucide Icons dans un projet Laravel
- Utilisation d'icônes dans Blade templates
- Intégration avec Alpine.js pour des icônes dynamiques
- Création de composants Blade avec icônes
- Animations et transitions d'icônes

## Installation

### Via NPM
```bash
npm install lucide
```

### Méthode 1 : Auto-initialisation (Recommandé)
Dans `resources/js/app.js` :
```javascript
import { createIcons, icons } from 'lucide';

document.addEventListener('DOMContentLoaded', () => {
  createIcons({ icons });
});
```

### Méthode 2 : Import Sélectif (Performance)
```javascript
import { createIcons, Plus, Edit, Trash, X, Check, AlertCircle } from 'lucide';

document.addEventListener('DOMContentLoaded', () => {
  createIcons({
    icons: {
      Plus,
      Edit,
      Trash,
      X,
      Check,
      AlertCircle,
    }
  });
});
```

## Usage de Base

### Syntaxe Simple
```blade
<i data-lucide="icon-name" class="w-5 h-5"></i>
```

### Avec Classes Tailwind
```blade
<i data-lucide="check-circle" class="w-6 h-6 text-green-500"></i>
```

### Dans les Boutons
```blade
<button class="flex items-center gap-2 px-4 py-2 bg-blue-600 text-white rounded-lg">
  <i data-lucide="plus" class="w-4 h-4"></i>
  Ajouter
</button>
```

### Dans les Liens
```blade
<a href="#" class="flex items-center gap-2 text-blue-600 hover:text-blue-800">
  <i data-lucide="external-link" class="w-4 h-4"></i>
  Voir plus
</a>
```

## Bibliothèque d'Icônes par Catégorie

### Actions CRUD
```blade
<!-- Créer -->
<i data-lucide="plus-circle" class="w-5 h-5"></i>
<i data-lucide="plus" class="w-5 h-5"></i>

<!-- Lire/Voir -->
<i data-lucide="eye" class="w-5 h-5"></i>

<!-- Éditer -->
<i data-lucide="edit" class="w-5 h-5"></i>
<i data-lucide="pencil" class="w-5 h-5"></i>

<!-- Supprimer -->
<i data-lucide="trash-2" class="w-5 h-5"></i>
<i data-lucide="x-circle" class="w-5 h-5"></i>

<!-- Sauvegarder -->
<i data-lucide="save" class="w-5 h-5"></i>
```

### Navigation
```blade
<i data-lucide="home" class="w-5 h-5"></i>
<i data-lucide="menu" class="w-5 h-5"></i>
<i data-lucide="chevron-down" class="w-4 h-4"></i>
<i data-lucide="chevron-right" class="w-4 h-4"></i>
<i data-lucide="chevron-left" class="w-4 h-4"></i>
<i data-lucide="chevron-up" class="w-4 h-4"></i>
<i data-lucide="arrow-left" class="w-5 h-5"></i>
<i data-lucide="arrow-right" class="w-5 h-5"></i>
<i data-lucide="external-link" class="w-4 h-4"></i>
```

### Statuts et Feedbacks
```blade
<!-- Succès -->
<i data-lucide="check-circle" class="w-5 h-5 text-green-500"></i>
<i data-lucide="check" class="w-5 h-5 text-green-500"></i>

<!-- Erreur -->
<i data-lucide="x-circle" class="w-5 h-5 text-red-500"></i>
<i data-lucide="alert-circle" class="w-5 h-5 text-red-500"></i>

<!-- Avertissement -->
<i data-lucide="alert-triangle" class="w-5 h-5 text-yellow-500"></i>

<!-- Info -->
<i data-lucide="info" class="w-5 h-5 text-blue-500"></i>

<!-- Chargement -->
<i data-lucide="loader-2" class="w-5 h-5 animate-spin"></i>
```

### Fichiers et Médias
```blade
<i data-lucide="file" class="w-5 h-5"></i>
<i data-lucide="file-text" class="w-5 h-5"></i>
<i data-lucide="file-image" class="w-5 h-5"></i>
<i data-lucide="image" class="w-5 h-5"></i>
<i data-lucide="upload" class="w-5 h-5"></i>
<i data-lucide="download" class="w-5 h-5"></i>
<i data-lucide="paperclip" class="w-5 h-5"></i>
```

### Utilisateurs et Social
```blade
<i data-lucide="user" class="w-5 h-5"></i>
<i data-lucide="users" class="w-5 h-5"></i>
<i data-lucide="user-plus" class="w-5 h-5"></i>
<i data-lucide="user-minus" class="w-5 h-5"></i>
<i data-lucide="heart" class="w-5 h-5"></i>
<i data-lucide="message-circle" class="w-5 h-5"></i>
<i data-lucide="mail" class="w-5 h-5"></i>
<i data-lucide="bell" class="w-5 h-5"></i>
```

### Paramètres et Outils
```blade
<i data-lucide="settings" class="w-5 h-5"></i>
<i data-lucide="search" class="w-5 h-5"></i>
<i data-lucide="filter" class="w-5 h-5"></i>
<i data-lucide="calendar" class="w-5 h-5"></i>
<i data-lucide="clock" class="w-5 h-5"></i>
<i data-lucide="lock" class="w-5 h-5"></i>
<i data-lucide="unlock" class="w-5 h-5"></i>
```

### Commerce
```blade
<i data-lucide="shopping-cart" class="w-5 h-5"></i>
<i data-lucide="shopping-bag" class="w-5 h-5"></i>
<i data-lucide="credit-card" class="w-5 h-5"></i>
<i data-lucide="dollar-sign" class="w-5 h-5"></i>
<i data-lucide="tag" class="w-5 h-5"></i>
```

## Intégration avec Alpine.js

### Icône Dynamique
```blade
<div x-data="{ icon: 'check' }">
  <i :data-lucide="icon" class="w-5 h-5"></i>
</div>
```

**Note** : Nécessite une réinitialisation :
```javascript
Alpine.effect(() => {
  createIcons({ icons });
});
```

### Toggle Icon (Chevron)
```blade
<button 
  x-data="{ open: false }" 
  @click="open = !open"
  class="flex items-center gap-2"
>
  <span>Menu</span>
  <i :data-lucide="open ? 'chevron-up' : 'chevron-down'" class="w-4 h-4 transition-transform"></i>
</button>
```

### État Conditionnel
```blade
<div x-data="{ saved: false }">
  <button @click="saved = !saved" class="flex items-center gap-2">
    <i :data-lucide="saved ? 'heart' : 'heart'" :class="{ 'text-red-500 fill-red-500': saved }" class="w-5 h-5"></i>
    <span x-text="saved ? 'Enregistré' : 'Enregistrer'"></span>
  </button>
</div>
```

## Composants Blade Réutilisables

### Composant Icon Simple
Créer `app/View/Components/Icon.php` :
```php
namespace App\View\Components;

use Illuminate\View\Component;

class Icon extends Component
{
    public function __construct(
        public string $name,
        public string $size = 'w-5 h-5',
        public string $color = ''
    ) {}

    public function render()
    {
        return view('components.icon');
    }
}
```

Créer `resources/views/components/icon.blade.php` :
```blade
<i 
  data-lucide="{{ $name }}" 
  class="{{ $size }} {{ $color }} {{ $attributes->get('class') }}"
  {{ $attributes->except('class') }}
></i>
```

Usage :
```blade
<x-icon name="plus" size="w-6 h-6" color="text-blue-500" />
<x-icon name="edit" class="hover:text-gray-700" />
```

### Composant Button Icon
```blade
<!-- resources/views/components/button-icon.blade.php -->
@props(['icon', 'variant' => 'primary'])

@php
$classes = [
    'primary' => 'bg-blue-600 text-white hover:bg-blue-700',
    'secondary' => 'bg-gray-200 text-gray-800 hover:bg-gray-300',
    'danger' => 'bg-red-600 text-white hover:bg-red-700',
];
@endphp

<button {{ $attributes->merge(['class' => 'flex items-center gap-2 px-4 py-2 rounded-lg transition-colors ' . $classes[$variant]]) }}>
  <i data-lucide="{{ $icon }}" class="w-4 h-4"></i>
  {{ $slot }}
</button>
```

Usage :
```blade
<x-button-icon icon="plus" variant="primary">
  Ajouter Article
</x-button-icon>

<x-button-icon icon="trash-2" variant="danger">
  Supprimer
</x-button-icon>
```

## Animations

### Spin (Chargement)
```blade
<i data-lucide="loader-2" class="w-6 h-6 animate-spin text-blue-600"></i>
```

### Pulse (Notification)
```blade
<i data-lucide="bell" class="w-5 h-5 animate-pulse text-red-500"></i>
```

### Bounce (Alerte)
```blade
<i data-lucide="alert-circle" class="w-5 h-5 animate-bounce text-yellow-500"></i>
```

### Transition avec Alpine
```blade
<div x-data="{ show: false }">
  <button @click="show = !show" class="flex items-center gap-2">
    <span>Détails</span>
    <i 
      data-lucide="chevron-down" 
      class="w-4 h-4 transition-transform duration-300"
      :class="{ 'rotate-180': show }"
    ></i>
  </button>
  
  <div x-show="show" x-transition>
    Contenu des détails
  </div>
</div>
```

## Classes Utilitaires

Définir dans `resources/css/app.css` :
```css
@layer utilities {
  .icon-xs { @apply w-3 h-3; }
  .icon-sm { @apply w-4 h-4; }
  .icon-md { @apply w-5 h-5; }
  .icon-lg { @apply w-6 h-6; }
  .icon-xl { @apply w-8 h-8; }
  .icon-2xl { @apply w-10 h-10; }
}
```

Usage :
```blade
<i data-lucide="plus" class="icon-sm"></i>
<i data-lucide="user" class="icon-lg"></i>
```

## Accessibilité

### Icône seule (bouton)
```blade
<button aria-label="Éditer l'article" class="p-2 hover:bg-gray-100 rounded">
  <i data-lucide="edit" class="w-5 h-5"></i>
</button>
```

### Icône avec texte
```blade
<button class="flex items-center gap-2">
  <i data-lucide="trash-2" class="w-4 h-4"></i>
  <span>Supprimer</span>
</button>
```

### Icône décorative
```blade
<div class="flex items-center gap-2">
  <i data-lucide="info" class="w-4 h-4 text-blue-500" aria-hidden="true"></i>
  <span>Information importante</span>
</div>
```

## Performance

### Import Sélectif
Pour réduire la taille du bundle, importez uniquement les icônes utilisées :
```javascript
import { 
  createIcons, 
  Plus, Edit, Trash, Eye, Save, 
  CheckCircle, XCircle, AlertTriangle,
  ChevronDown, ChevronUp, ChevronLeft, ChevronRight
} from 'lucide';

document.addEventListener('DOMContentLoaded', () => {
  createIcons({
    icons: {
      Plus, Edit, Trash, Eye, Save,
      CheckCircle, XCircle, AlertTriangle,
      ChevronDown, ChevronUp, ChevronLeft, ChevronRight
    }
  });
});
```

## Réinitialisation après AJAX

```javascript
// Après fetch/axios
fetch('/api/articles')
  .then(res => res.json())
  .then(data => {
    document.getElementById('content').innerHTML = data.html;
    createIcons({ icons }); // Réinitialiser les icônes
  });
```

## Erreurs Courantes

### 1. Icône ne s'affiche pas
**Problème** : `createIcons()` non appelé
**Solution** : Vérifier que `createIcons()` est dans `DOMContentLoaded`

### 2. Icône manquante (import sélectif)
**Problème** : Icône non importée
**Solution** : Ajouter l'icône dans la liste des imports

### 3. Conflit avec Alpine
**Problème** : Icônes dynamiques ne se mettent pas à jour
**Solution** : Appeler `createIcons()` dans `Alpine.effect()`

### 4. Mauvaise taille
**Problème** : Taille non définie
**Solution** : Toujours spécifier `w-* h-*` (Lucide ignore les tailles par défaut)

## Best Practices

1. **Toujours spécifier la taille** avec les classes Tailwind `w-* h-*`
2. **Utiliser des classes utilitaires** pour les tailles cohérentes
3. **Import sélectif** pour optimiser la performance
4. **Ajouter aria-label** sur les boutons icon-only
5. **Préférer le rendu serveur** aux icônes dynamiques
6. **Combiner avec Preline UI** pour une expérience cohérente

## Ressources
- Site officiel : https://lucide.dev
- Icons Explorer : https://lucide.dev/icons
- GitHub : https://github.com/lucide-icons/lucide
- NPM : https://www.npmjs.com/package/lucide
