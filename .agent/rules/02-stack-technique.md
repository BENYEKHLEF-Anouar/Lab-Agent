---
trigger: always_on
---

# Stack Technique

## Backend
- **Framework** : Laravel (dernière version LTS recommandée)
- **PHP** : Version 8.2+ minimum
- **Templating** : Blade (moteur de templates Laravel)
- **ORM** : Eloquent
- **Database** : MySQL

## Frontend
- **UI Library** : **Preline UI** (composants Tailwind CSS pré-construits)
  - Documentation : https://preline.co/docs
  - Installation via CDN ou npm
  - Composants : modals, dropdowns, accordions, tabs, tooltips, etc.
- **Framework JS** : **Alpine.js** (v3+)
  - Intégration native avec Preline UI
  - Logique réactive légère
- **CSS Framework** : **Tailwind CSS** (v3+)
  - Configuration dans `tailwind.config.js`
  - Classes utilitaires
- **Icons** : **Lucide Icons** (bibliothèque d'icônes moderne)
  - Installation : `npm install lucide`
  - Usage : `<i data-lucide="icon-name"></i>` ou composants Alpine
- **Build Tool** : **Vite** (intégré dans Laravel)

## Libraries & Packages (Spatie)
- **spatie/laravel-permission** : Gestion des rôles et permissions


## Architecture

### Structure MVC Hybride (3-tier Architecture)
```
app/
├── Http/
│   ├── Controllers/      # Orchestration HTTP uniquement
│   ├── Requests/         # Form Request Validation
│   └── Middleware/       # Filtres HTTP
├── Services/             # Business Logic Layer
│   ├── ArticleService.php
│   └── UserService.php
```

### Principes Architecturaux

#### 1. **Controllers** (Couche de Présentation)
- Gèrent UNIQUEMENT les requêtes/réponses HTTP
- Délèguent toute logique métier aux **Services**
- Valident les inputs via **Form Requests**
- Exemple :
```php
public function store(StoreArticleRequest $request, ArticleService $service)
{
    $article = $service->create($request->validated());
    return redirect()->route('articles.index')
        ->with('success', 'Article créé avec succès');
}
```

#### 2. **Services** (Couche Métier)
- Contiennent TOUTE la logique métier
- Interagissent avec les **Models** et **Repositories**
- Sont injectés via Dependency Injection
- Peuvent utiliser d'autres Services
- Exemple : `ArticleService`, `UploadService`, `CommentService`

#### 3. **Models** (Couche Domaine)
- Représentent les entités métier (Eloquent)
- Contiennent UNIQUEMENT :
  - Relations (`hasMany`, `belongsTo`, etc.)
  - Scopes (query scopes)
  - Accessors/Mutators simples
  - Castings
- **PAS de logique métier complexe** dans les models

#### 4. **Repositories** (Optionnel - Data Access Layer)
- Utilisés UNIQUEMENT si la logique de requêtes devient complexe
- Abstraient l'accès aux données
- Pattern Repository pour découpler la logique métier de la persistance

### Architecture Multi-Page Application (MPA)
- **Server-Side Rendering** : Le HTML est généré côté serveur (Blade)
- **Alpine.js** : Ajoute de l'interactivité "sprinkles" sans framework lourd
- **Preline UI** : Composants pré-construits initialisés automatiquement
- **Navigation** : Rechargement de pages (ou turbo/livewire si besoin)

### Composants & Interactivité
- Utilisation de `x-data` Alpine.js pour isoler la logique des composants
- Composants Preline UI (`data-hs-*` attributes)
- Modales, Dropdowns, Accordions via Preline + Alpine
- Lucide Icons pour tous les icônes

## Conventions de Code

### Naming Conventions
- **Variables PHP** : `$camelCase`
- **Variables JS** : `camelCase`
- **Classes** : `PascalCase`
- **Methods** : `camelCase`
- **Routes** : `kebab-case` (ex: `/articles/create-draft`)
- **Views** : `kebab-case` (ex: `articles/create-form.blade.php`)
- **Database Tables** : `snake_case` pluriel (ex: `user_articles`)
- **Database Columns** : `snake_case` (ex: `created_at`)

### Organisation du Code
- **Services** : Extraire la logique métier complexe
- **Alpine.js** : Extraire les objets de données complexes dans des fichiers séparés (`resources/js/components/`)
- **Blade Components** : Créer des composants réutilisables (`resources/views/components/`)
- **Tailwind** : Utiliser `@apply` avec parcimonie, préférer les classes utilitaires

### Best Practices Laravel
- Toujours utiliser **Form Requests** pour la validation
- Utiliser les **Route Model Binding**
- Privilégier les **Eloquent Relationships** plutôt que les jointures manuelles
- Utiliser les **Policies** pour l'autorisation
- Implémenter les **Seeders** et **Factories** pour les tests
- Utiliser les **Migrations** pour toutes les modifications de schéma
- Respecter le principe **DRY** (Don't Repeat Yourself)