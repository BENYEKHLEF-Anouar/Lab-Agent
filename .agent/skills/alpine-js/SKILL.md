---
name: Alpine.js
description: Expert en Alpine.js pour l'interactivité dans des applications Laravel avec Preline UI
---

# Skill: Alpine.js

## Description
Ce skill permet d'intégrer et d'utiliser efficacement **Alpine.js**, un framework JavaScript léger pour ajouter de l'interactivité aux applications Laravel avec server-side rendering.

## Quand utiliser ce skill
- Ajouter de l'interactivité légère aux vues Blade
- Gérer l'état local des composants UI
- Créer des formulaires dynamiques
- Intégration avec Preline UI
- Remplacer jQuery par une solution moderne

## Philosophie Alpine.js

**"Your new, lightweight, JavaScript framework"**

Alpine.js est conçu pour :
- Ajouter des "sprinkles" d'interactivité
- Rester dans le HTML (pas de build step complexe)
- Garder la logique proche du markup
- Remplacer jQuery pour les besoins simples

## Installation

### Via NPM
```bash
npm install alpinejs
```

### Dans `resources/js/app.js`
```javascript
import Alpine from 'alpinejs';

window.Alpine = Alpine;
Alpine.start();
```

### Via CDN (pour prototypage rapide)
```blade
<script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
```

## Directives Principales

### 1. `x-data` - Définir l'état du composant

```blade
<div x-data="{ open: false }">
  <!-- État disponible dans ce scope -->
</div>
```

**Avec fonction** :
```blade
<div x-data="dropdown()">
  <!-- ... -->
</div>

<script>
function dropdown() {
  return {
    open: false,
    toggle() {
      this.open = !this.open;
    }
  }
}
</script>
```

### 2. `x-show` - Afficher/Cacher (avec CSS)

```blade
<div x-data="{ open: false }">
  <button @click="open = !open">Toggle</button>
  <div x-show="open">
    Contenu visible si open = true
  </div>
</div>
```

**Avec transition** :
```blade
<div x-show="open" x-transition>
  Contenu avec animation
</div>
```

### 3. `x-if` - Rendu conditionnel (DOM)

```blade
<div x-data="{ show: true }">
  <template x-if="show">
    <div>Contenu (ajouté/retiré du DOM)</div>
  </template>
</div>
```

### 4. `x-for` - Boucles

```blade
<div x-data="{ items: ['Apple', 'Banana', 'Orange'] }">
  <template x-for="item in items" :key="item">
    <li x-text="item"></li>
  </template>
</div>
```

### 5. `x-model` - Two-way binding

```blade
<div x-data="{ message: '' }">
  <input type="text" x-model="message">
  <p x-text="message"></p>
</div>
```

**Modifiers** :
```blade
<input x-model.debounce.500ms="search"> <!-- Debounce 500ms -->
<input x-model.number="quantity">      <!-- Convertir en number -->
<input x-model.lazy="email">           <!-- Update on blur -->
```

### 6. `@click` / `x-on:click` - Event Listeners

```blade
<button @click="count++">Increment</button>
<button x-on:click="handleClick()">Click me</button>
```

**Modifiers** :
```blade
<button @click.prevent="submit">Submit</button>
<div @click.outside="close()">Modal</div>
<form @submit.prevent="save()">...</form>
<input @keydown.enter="search()">
```

### 7. `x-text` / `x-html` - Contenu texte/HTML

```blade
<span x-text="message"></span>
<div x-html="htmlContent"></div>
```

### 8. `:class` / `x-bind:class` - Classes dynamiques

```blade
<div :class="{ 'bg-blue-500': active, 'bg-gray-200': !active }">
  Contenu
</div>

<!-- Ou -->
<div :class="active ? 'bg-blue-500' : 'bg-gray-200'">
  Contenu
</div>
```

### 9. `x-cloak` - Cacher avant initialisation

```css
[x-cloak] { display: none !important; }
```

```blade
<div x-data="{ message: 'Hello' }" x-cloak>
  <p x-text="message"></p>
</div>
```

## Patterns Courants dans Laravel

### 1. Toggle / Accordion
```blade
<div x-data="{ open: false }">
  <button @click="open = !open" class="flex items-center gap-2">
    <span>Détails</span>
    <i data-lucide="chevron-down" :class="{ 'rotate-180': open }" class="w-4 h-4 transition-transform"></i>
  </button>
  
  <div x-show="open" x-transition x-cloak>
    <p>Contenu de l'accordion</p>
  </div>
</div>
```

### 2. Tabs
```blade
<div x-data="{ activeTab: 'tab1' }">
  <div class="border-b">
    <button @click="activeTab = 'tab1'" :class="{ 'border-blue-500 text-blue-600': activeTab === 'tab1' }">
      Tab 1
    </button>
    <button @click="activeTab = 'tab2'" :class="{ 'border-blue-500 text-blue-600': activeTab === 'tab2' }">
      Tab 2
    </button>
  </div>
  
  <div x-show="activeTab === 'tab1'" x-transition>Tab 1 Content</div>
  <div x-show="activeTab === 'tab2'" x-transition>Tab 2 Content</div>
</div>
```

### 3. Search/Filter
```blade
<div x-data="{ search: '', items: @json($articles) }">
  <input 
    type="text" 
    x-model.debounce.300ms="search" 
    placeholder="Rechercher..."
    class="border rounded px-4 py-2"
  >
  
  <template x-for="item in items.filter(i => i.title.toLowerCase().includes(search.toLowerCase()))" :key="item.id">
    <div class="p-4 border-b">
      <h3 x-text="item.title"></h3>
      <p x-text="item.description"></p>
    </div>
  </template>
</div>
```

### 4. Form avec Validation
```blade
<div x-data="formComponent()">
  <form @submit.prevent="submit">
    <div>
      <input 
        type="email" 
        x-model="form.email" 
        @blur="validateEmail"
        :class="{ 'border-red-500': errors.email }"
      >
      <p x-show="errors.email" x-text="errors.email" class="text-red-500 text-sm"></p>
    </div>
    
    <button type="submit" :disabled="loading" class="px-4 py-2 bg-blue-600 text-white rounded">
      <span x-show="!loading">Envoyer</span>
      <span x-show="loading" class="flex items-center gap-2">
        <i data-lucide="loader-2" class="w-4 h-4 animate-spin"></i>
        Envoi...
      </span>
    </button>
  </form>
</div>

<script>
function formComponent() {
  return {
    form: { email: '' },
    errors: {},
    loading: false,
    
    validateEmail() {
      if (!this.form.email.includes('@')) {
        this.errors.email = 'Email invalide';
      } else {
        delete this.errors.email;
      }
    },
    
    async submit() {
      this.loading = true;
      this.errors = {};
      
      try {
        const response = await fetch('/api/subscribe', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
            'X-CSRF-TOKEN': document.querySelector('meta[name="csrf-token"]').content
          },
          body: JSON.stringify(this.form)
        });
        
        if (!response.ok) {
          const data = await response.json();
          this.errors = data.errors || { general: 'Erreur' };
          return;
        }
        
        alert('Succès !');
        this.form = { email: '' };
      } catch (error) {
        this.errors = { general: 'Erreur réseau' };
      } finally {
        this.loading = false;
      }
    }
  }
}
</script>
```

### 5. AJAX avec Laravel (CRUD)
```blade
<div x-data="articlesComponent()">
  <!-- Liste -->
  <div class="space-y-4">
    <template x-for="article in articles" :key="article.id">
      <div class="p-4 border rounded">
        <h3 x-text="article.title"></h3>
        <p x-text="article.content"></p>
        <div class="flex gap-2 mt-2">
          <button @click="edit(article)">
            <i data-lucide="edit" class="w-4 h-4"></i>
          </button>
          <button @click="deleteArticle(article.id)">
            <i data-lucide="trash-2" class="w-4 h-4"></i>
          </button>
        </div>
      </div>
    </template>
  </div>
  
  <!-- Loading -->
  <div x-show="loading" class="text-center py-8">
    <i data-lucide="loader-2" class="w-8 h-8 animate-spin mx-auto"></i>
  </div>
</div>

<script>
function articlesComponent() {
  return {
    articles: [],
    loading: false,
    
    async init() {
      await this.fetchArticles();
    },
    
    async fetchArticles() {
      this.loading = true;
      const response = await fetch('/api/articles');
      this.articles = await response.json();
      this.loading = false;
    },
    
    edit(article) {
      // Ouvrir modal Preline avec données
      this.$dispatch('open-edit-modal', article);
    },
    
    async deleteArticle(id) {
      if (!confirm('Confirmer la suppression ?')) return;
      
      await fetch(`/api/articles/${id}`, {
        method: 'DELETE',
        headers: {
          'X-CSRF-TOKEN': document.querySelector('meta[name="csrf-token"]').content
        }
      });
      
      await this.fetchArticles();
    }
  }
}
</script>
```

## Intégration avec Preline UI

### Modal Alpine + Preline
```blade
<div x-data="modalComponent()">
  <button @click="openModal()" data-hs-overlay="#edit-modal">
    Éditer
  </button>
  
  <div id="edit-modal" class="hs-overlay hidden">
    <div class="hs-overlay-open:opacity-100 ...">
      <form @submit.prevent="save">
        <input type="text" x-model="form.title">
        <textarea x-model="form.content"></textarea>
        <button type="submit">Sauvegarder</button>
      </form>
    </div>
  </div>
</div>

<script>
function modalComponent() {
  return {
    form: { title: '', content: '' },
    
    async openModal() {
      const response = await fetch('/api/articles/1');
      this.form = await response.json();
      HSOverlay.open('#edit-modal');
    },
    
    async save() {
      await fetch('/api/articles/1', {
        method: 'PUT',
        headers: {
          'Content-Type': 'application/json',
          'X-CSRF-TOKEN': document.querySelector('meta[name="csrf-token"]').content
        },
        body: JSON.stringify(this.form)
      });
      
      HSOverlay.close('#edit-modal');
    }
  }
}
</script>
```

## Alpine Plugins

### Persist (localStorage)
```javascript
import Alpine from 'alpinejs';
import persist from '@alpinejs/persist';

Alpine.plugin(persist);
Alpine.start();
```

```blade
<div x-data="{ darkMode: $persist(false) }">
  <button @click="darkMode = !darkMode">Toggle Dark Mode</button>
</div>
```

### Focus
```javascript
import focus from '@alpinejs/focus';
Alpine.plugin(focus);
```

```blade
<div x-data="{ open: false }" x-trap="open">
  <button @click="open = true">Open</button>
  <div x-show="open">
    <input type="text" x-ref="firstInput">
  </div>
</div>
```

## Magic Properties

```blade
<!-- $el : Référence à l'élément DOM -->
<div @click="console.log($el)"></div>

<!-- $refs : Références nommées -->
<div x-data>
  <input x-ref="myInput">
  <button @click="$refs.myInput.focus()">Focus</button>
</div>

<!-- $dispatch : Émettre des événements -->
<button @click="$dispatch('notify', { message: 'Hello' })">Notify</button>

<!-- $watch : Observer des changements -->
<div x-data="{ count: 0 }" x-init="$watch('count', value => console.log(value))">
  <button @click="count++">{{ count }}</button>
</div>

<!-- $nextTick : Attendre le prochain cycle -->
<div x-data="{ show: false }">
  <button @click="show = true; $nextTick(() => $refs.input.focus())">Show</button>
  <input x-show="show" x-ref="input">
</div>
```

## Organisation du Code

### Composants dans des fichiers séparés
Créer `resources/js/components/article-form.js` :
```javascript
export default function articleForm() {
  return {
    form: { title: '', content: '' },
    errors: {},
    loading: false,
    
    async submit() {
      this.loading = true;
      // ...
    }
  }
}
```

Dans `resources/js/app.js` :
```javascript
import Alpine from 'alpinejs';
import articleForm from './components/article-form';

window.articleForm = articleForm;

Alpine.start();
```

Usage dans Blade :
```blade
<div x-data="articleForm()">
  <!-- ... -->
</div>
```

## Best Practices

1. **Garder la logique simple** : Alpine est pour l'interactivité légère
2. **Extraire les composants complexes** : Créer des fonctions séparées
3. **Utiliser x-cloak** : Éviter le flash de contenu non-initialisé
4. **Éviter la duplication** : Créer des composants réutilisables
5. **Combiner avec Preline** : Ne pas réinventer les composants UI
6. **CSRF Token** : Toujours inclure dans les requêtes AJAX

## Debugging

```blade
<!-- Afficher l'état dans la console -->
<div x-data="{ count: 0 }" x-init="$watch('count', value => console.log('Count:', value))">
  <button @click="count++">Count: <span x-text="count"></span></button>
</div>

<!-- Vue Alpine DevTools (Chrome Extension) -->
```

## Erreurs Courantes

### 1. x-cloak ne fonctionne pas
**Problème** : CSS manquant
**Solution** : Ajouter `[x-cloak] { display: none !important; }` dans le CSS

### 2. État non réactif
**Problème** : Modification directe de propriété d'objet
**Solution** : Réassigner l'objet entier ou utiliser `Alpine.store()`

### 3. CSRF Token manquant
**Problème** : 419 CSRF Token Mismatch
**Solution** : Inclure le token dans les headers fetch

## Ressources
- Documentation officielle : https://alpinejs.dev
- Alpine Toolbox : https://www.alpine-toolbox.com
- Alpine DevTools : Chrome Web Store
- GitHub : https://github.com/alpinejs/alpine
