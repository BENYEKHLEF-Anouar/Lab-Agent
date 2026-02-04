---
description: Create CRUD module with Services architecture
---

# Workflow: Create CRUD Module

Ce workflow crée un module CRUD complet avec architecture MVC + Services + 3-tier.

## Étapes

### 1. Créer la Migration
```bash
php artisan make:migration create_[table_name]_table
```
- Définir les colonnes dans le fichier de migration
- Ajouter les index nécessaires
- Ajouter les foreign keys si nécessaire

### 2. Créer le Model
```bash
php artisan make:model [ModelName]
```
- Définir `$fillable` ou `$guarded`
- Ajouter les relations (hasMany, belongsTo, etc.)
- Ajouter les castings si nécessaire
- Ajouter les scopes pour les requêtes courantes

### 3. Créer le Service
```bash
php artisan make:class Services/[ModelName]Service
```
- Implémenter les méthodes : `getAll()`, `getById($id)`, `create($data)`, `update($id, $data)`, `delete($id)`
- Injecter d'autres services si nécessaire
- Gérer la logique métier complexe

### 4. Créer les Form Requests
```bash
php artisan make:request Store[ModelName]Request
php artisan make:request Update[ModelName]Request
```
- Définir les règles de validation
- Customiser les messages d'erreur si nécessaire
- Implémenter `authorize()` si besoin

### 5. Créer le Controller
```bash
php artisan make:controller [ModelName]Controller --resource
```
- Injecter le Service dans le constructeur
- Déléguer toute logique aux Services
- Utiliser les Form Requests pour la validation
- Retourner les vues appropriées

### 6. Créer les Routes
Dans `routes/web.php` :
```php
Route::resource('[resource-name]', [ModelName]Controller::class);
```

### 7. Créer les Vues Blade
```bash
# Structure de dossier
resources/views/[resource-name]/
├── index.blade.php    # Liste
├── show.blade.php     # Détail
├── create.blade.php   # Création
└── edit.blade.php     # Édition
```
- Utiliser Preline UI pour les composants
- Intégrer Alpine.js pour l'interactivité
- Utiliser Lucide Icons pour les icônes

### 8. Créer les Seeders et Factories (optionnel)
// turbo
```bash
php artisan make:seeder [ModelName]Seeder
php artisan make:factory [ModelName]Factory
```

### 9. Exécuter les Migrations
// turbo
```bash
php artisan migrate
```

### 10. Tester l'application
- Tester manuellement via le navigateur
- Créer des tests automatisés si nécessaire

## Exemple Complet : Module Article

**Migration** :
```php
Schema::create('articles', function (Blueprint $table) {
    $table->id();
    $table->string('title');
    $table->text('content');
    $table->string('image')->nullable();
    $table->timestamps();
});
```

**Model** :
```php
class Article extends Model
{
    protected $fillable = ['title', 'content', 'image'];
}
```

**Service** :
```php
class ArticleService
{
    public function getAll() {
        return Article::latest()->paginate(10);
    }
    
    public function create(array $data) {
        return Article::create($data);
    }
}
```

**Controller** :
```php
public function index(ArticleService $service)
{
    $articles = $service->getAll();
    return view('articles.index', compact('articles'));
}
```
