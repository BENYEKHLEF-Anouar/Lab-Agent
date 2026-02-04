---
name: Tailwind CSS
description: Expert en Tailwind CSS pour le styling d'applications Laravel
---

# Skill: Tailwind CSS

## Description
Ce skill permet d'utiliser efficacement **Tailwind CSS**, un framework CSS utility-first, dans des applications Laravel pour créer des interfaces modernes et responsive.

## Quand utiliser ce skill
- Installation et configuration de Tailwind dans Laravel
- Création de designs responsive
- Personnalisation du thème Tailwind
- Optimisation des builds de production
- Intégration avec Preline UI et Alpine.js

## Installation dans Laravel

### Via NPM
```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

### Configuration `tailwind.config.js`
```javascript
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./resources/**/*.blade.php",
    "./resources/**/*.js",
    "./resources/**/*.vue",
    "./node_modules/preline/dist/*.js",
  ],
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#eff6ff',
          100: '#dbeafe',
          200: '#bfdbfe',
          300: '#93c5fd',
          400: '#60a5fa',
          500: '#3b82f6',
          600: '#2563eb',
          700: '#1d4ed8',
          800: '#1e40af',
          900: '#1e3a8a',
        },
      },
      fontFamily: {
        sans: ['Inter', 'system-ui', 'sans-serif'],
        mono: ['Fira Code', 'monospace'],
      },
    },
  },
  plugins: [
    require('preline/plugin'),
  ],
}
```

### Dans `resources/css/app.css`
```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer components {
  .btn {
    @apply px-4 py-2 rounded-lg font-medium transition-colors;
  }
  
  .btn-primary {
    @apply bg-blue-600 text-white hover:bg-blue-700;
  }
  
  .btn-secondary {
    @apply bg-gray-200 text-gray-800 hover:bg-gray-300;
  }
}
```

### Compiler les assets
```bash
npm run dev
npm run build  # Production
```

## Classes Utilitaires Essentielles

### Layout
```blade
<!-- Container -->
<div class="container mx-auto px-4">Content</div>

<!-- Flexbox -->
<div class="flex items-center justify-between gap-4">...</div>
<div class="flex flex-col md:flex-row">...</div>

<!-- Grid -->
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">...</div>
```

### Spacing (padding/margin)
```blade
<!-- p-4 = padding: 1rem (16px) -->
<div class="p-4">Padding all sides</div>
<div class="px-4 py-2">Padding horizontal & vertical</div>
<div class="mt-4 mb-8">Margin top & bottom</div>

<!-- Échelle: 0, 0.5, 1, 2, 3, 4, 5, 6, 8, 10, 12, 16, 20, 24, 32, 40, 48, 56, 64 -->
```

### Typography
```blade
<!-- Tailles -->
<h1 class="text-4xl font-bold">Heading 1</h1>
<h2 class="text-3xl font-semibold">Heading 2</h2>
<p class="text-base text-gray-700">Paragraph</p>
<small class="text-sm text-gray-500">Small text</small>

<!-- Alignement -->
<p class="text-left">Left</p>
<p class="text-center">Center</p>
<p class="text-right">Right</p>

<!-- Line height -->
<p class="leading-relaxed">Relaxed line height</p>
<p class="leading-tight">Tight line height</p>
```

### Colors
```blade
<!-- Text -->
<p class="text-blue-600">Blue text</p>
<p class="text-red-500">Red text</p>

<!-- Background -->
<div class="bg-blue-600 text-white">Blue background</div>
<div class="bg-gradient-to-r from-blue-500 to-purple-600">Gradient</div>

<!-- Border -->
<div class="border border-gray-300">Border</div>
<div class="border-2 border-blue-500">Thick blue border</div>
```

### Responsive Design
```blade
<!-- Mobile first -->
<div class="text-sm md:text-base lg:text-lg xl:text-xl">
  Responsive text
</div>

<!-- Breakpoints: sm (640px), md (768px), lg (1024px), xl (1280px), 2xl (1536px) -->
<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4">...</div>
```

### States (hover, focus, active)
```blade
<button class="bg-blue-600 hover:bg-blue-700 active:bg-blue-800 transition-colors">
  Hover me
</button>

<input class="border focus:ring-2 focus:ring-blue-500 focus:border-transparent">

<a class="text-blue-600 hover:text-blue-800 hover:underline">Link</a>
```

### Transitions & Animations
```blade
<!-- Transition -->
<div class="transition-all duration-300 ease-in-out">Smooth transition</div>

<!-- Hover transform -->
<div class="transform hover:scale-105 transition-transform">Scale on hover</div>

<!-- Animations -->
<div class="animate-spin">Spinning</div>
<div class="animate-pulse">Pulsing</div>
<div class="animate-bounce">Bouncing</div>
```

## Patterns Courants dans Laravel

### 1. Card Component
```blade
<div class="bg-white rounded-lg shadow-md overflow-hidden">
  <img src="image.jpg" alt="Image" class="w-full h-48 object-cover">
  <div class="p-6">
    <h3 class="text-xl font-bold mb-2">Card Title</h3>
    <p class="text-gray-600 mb-4">Card description</p>
    <button class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700">
      Action
    </button>
  </div>
</div>
```

### 2. Form Styling
```blade
<form class="space-y-6">
  <div>
    <label for="email" class="block text-sm font-medium text-gray-700 mb-2">
      Email
    </label>
    <input 
      type="email" 
      id="email" 
      class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
      placeholder="vous@example.com"
    >
    @error('email')
      <p class="mt-1 text-sm text-red-600">{{ $message }}</p>
    @enderror
  </div>
  
  <div>
    <label for="message" class="block text-sm font-medium text-gray-700 mb-2">
      Message
    </label>
    <textarea 
      id="message" 
      rows="4"
      class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
    ></textarea>
  </div>
  
  <button type="submit" class="w-full px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors">
    Envoyer
  </button>
</form>
```

### 3. Navigation/Navbar
```blade
<nav class="bg-white shadow-sm">
  <div class="container mx-auto px-4">
    <div class="flex items-center justify-between h-16">
      <a href="/" class="text-xl font-bold text-gray-900">Logo</a>
      
      <div class="hidden md:flex items-center space-x-8">
        <a href="#" class="text-gray-700 hover:text-blue-600 transition-colors">Home</a>
        <a href="#" class="text-gray-700 hover:text-blue-600 transition-colors">About</a>
        <a href="#" class="text-gray-700 hover:text-blue-600 transition-colors">Contact</a>
      </div>
      
      <button class="md:hidden">
        <i data-lucide="menu" class="w-6 h-6"></i>
      </button>
    </div>
  </div>
</nav>
```

### 4. Table
```blade
<div class="overflow-x-auto">
  <table class="min-w-full divide-y divide-gray-200">
    <thead class="bg-gray-50">
      <tr>
        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
          Nom
        </th>
        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
          Email
        </th>
        <th class="px-6 py-3 text-right text-xs font-medium text-gray-500 uppercase tracking-wider">
          Actions
        </th>
      </tr>
    </thead>
    <tbody class="bg-white divide-y divide-gray-200">
      @foreach($users as $user)
      <tr class="hover:bg-gray-50">
        <td class="px-6 py-4 whitespace-nowrap">
          <div class="text-sm font-medium text-gray-900">{{ $user->name }}</div>
        </td>
        <td class="px-6 py-4 whitespace-nowrap">
          <div class="text-sm text-gray-500">{{ $user->email }}</div>
        </td>
        <td class="px-6 py-4 whitespace-nowrap text-right text-sm font-medium">
          <button class="text-blue-600 hover:text-blue-900">Edit</button>
        </td>
      </tr>
      @endforeach
    </tbody>
  </table>
</div>
```

### 5. Alert/Notification
```blade
<!-- Success -->
<div class="flex items-center gap-3 p-4 bg-green-50 border border-green-200 rounded-lg">
  <i data-lucide="check-circle" class="w-5 h-5 text-green-600"></i>
  <p class="text-sm text-green-800">Opération réussie !</p>
</div>

<!-- Error -->
<div class="flex items-center gap-3 p-4 bg-red-50 border border-red-200 rounded-lg">
  <i data-lucide="x-circle" class="w-5 h-5 text-red-600"></i>
  <p class="text-sm text-red-800">Une erreur est survenue</p>
</div>

<!-- Warning -->
<div class="flex items-center gap-3 p-4 bg-yellow-50 border border-yellow-200 rounded-lg">
  <i data-lucide="alert-triangle" class="w-5 h-5 text-yellow-600"></i>
  <p class="text-sm text-yellow-800">Attention !</p>
</div>
```

## Personnalisation du Thème

### Colors Custom
```javascript
// tailwind.config.js
theme: {
  extend: {
    colors: {
      brand: {
        light: '#3fbaeb',
        DEFAULT: '#0fa9e6',
        dark: '#0c87b8',
      }
    }
  }
}
```

Usage :
```blade
<div class="bg-brand text-white">Brand color</div>
<div class="bg-brand-light">Light brand</div>
```

### Fonts Custom
```javascript
theme: {
  extend: {
    fontFamily: {
      sans: ['Inter', 'sans-serif'],
      heading: ['Poppins', 'sans-serif'],
    }
  }
}
```

Usage :
```blade
<h1 class="font-heading">Heading with Poppins</h1>
<p class="font-sans">Body with Inter</p>
```

## Dark Mode

### Configuration
```javascript
// tailwind.config.js
module.exports = {
  darkMode: 'class', // ou 'media'
  // ...
}
```

### Usage
```blade
<div class="bg-white dark:bg-gray-900 text-gray-900 dark:text-white">
  Contenu adaptatif
</div>

<button class="bg-blue-600 hover:bg-blue-700 dark:bg-blue-500 dark:hover:bg-blue-600">
  Button
</button>
```

### Toggle Dark Mode (avec Alpine)
```blade
<div x-data="{ darkMode: false }" :class="{ 'dark': darkMode }">
  <button @click="darkMode = !darkMode">
    <i :data-lucide="darkMode ? 'sun' : 'moon'" class="w-5 h-5"></i>
  </button>
  
  <div class="bg-white dark:bg-gray-900 min-h-screen">
    <!-- Content -->
  </div>
</div>
```

## Composants Blade avec Tailwind

### Button Component
```blade
<!-- resources/views/components/button.blade.php -->
@props(['variant' => 'primary', 'size' => 'md'])

@php
$variants = [
    'primary' => 'bg-blue-600 text-white hover:bg-blue-700',
    'secondary' => 'bg-gray-200 text-gray-800 hover:bg-gray-300',
    'danger' => 'bg-red-600 text-white hover:bg-red-700',
];

$sizes = [
    'sm' => 'px-3 py-1.5 text-sm',
    'md' => 'px-4 py-2',
    'lg' => 'px-6 py-3 text-lg',
];

$classes = $variants[$variant] . ' ' . $sizes[$size];
@endphp

<button {{ $attributes->merge(['class' => 'rounded-lg font-medium transition-colors ' . $classes]) }}>
    {{ $slot }}
</button>
```

Usage :
```blade
<x-button variant="primary" size="lg">Submit</x-button>
<x-button variant="danger">Delete</x-button>
```

## Performance & Production

### Purge CSS (automatique avec Tailwind v3+)
Le `content` dans `tailwind.config.js` détermine quels fichiers scanner.

### Build de Production
```bash
npm run build
```

Le build optimisé :
- Supprime les classes non utilisées
- Minifie le CSS
- Optimise pour la performance

## Best Practices

1. **Mobile First** : Commencer par le mobile, puis ajouter les breakpoints
2. **Utiliser @apply avec parcimonie** : Préférer les classes utilitaires directement
3. **Composants réutilisables** : Créer des Blade Components pour les patterns répétitifs
4. **Cohérence** : Définir des couleurs et espacements custom dans le config
5. **Dark Mode** : Prévoir le dark mode dès le début si nécessaire
6. **Accessibility** : Utiliser les classes de focus et les états hover

## Plugins Utiles

```bash
npm install -D @tailwindcss/forms
npm install -D @tailwindcss/typography
npm install -D @tailwindcss/aspect-ratio
```

```javascript
// tailwind.config.js
plugins: [
  require('@tailwindcss/forms'),
  require('@tailwindcss/typography'),
  require('@tailwindcss/aspect-ratio'),
  require('preline/plugin'),
],
```

## Ressources
- Documentation officielle : https://tailwindcss.com/docs
- Tailwind UI : https://tailwindui.com
- Tailwind Components : https://tailwindcomponents.com
- Headless UI : https://headlessui.com
