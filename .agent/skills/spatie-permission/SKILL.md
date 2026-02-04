---
name: Spatie Permission
description: Expert en gestion des rôles et permissions avec spatie/laravel-permission
---

# Skill: Spatie Permission

## Description
Ce skill permet d'implémenter un système robuste de **gestion des rôles et permissions** dans Laravel en utilisant le package `spatie/laravel-permission`.

## Quand utiliser ce skill
- Créer un système d'autorisation basé sur les rôles (RBAC)
- Gérer les permissions granulaires
- Contrôler l'accès aux fonctionnalités
- Créer des systèmes multi-tenants
- Implémenter des niveaux d'accès hiérarchiques

## Installation

```bash
composer require spatie/laravel-permission
```

### Publier la configuration et les migrations
```bash
php artisan vendor:publish --provider="Spatie\Permission\PermissionServiceProvider"
php artisan migrate
```

### Ajouter le Trait dans le Model User
```php
use Spatie\Permission\Traits\HasRoles;

class User extends Authenticatable
{
    use HasRoles;
    
    // ...
}
```

## Concepts de Base

**Rôle** : Un groupe de permissions (ex: admin, editor, user)
**Permission** : Une action spécifique (ex: create-posts, delete-users)
**Guard** : Contexte d'authentification (ex: web, api)

## Création de Rôles et Permissions

### Via Seeder (Recommandé)
Créer `database/seeders/RolesAndPermissionsSeeder.php` :
```php
namespace Database\Seeders;

use Illuminate\Database\Seeder;
use Spatie\Permission\Models\Role;
use Spatie\Permission\Models\Permission;

class RolesAndPermissionsSeeder extends Seeder
{
    public function run(): void
    {
        // Reset cached roles and permissions
        app()[\Spatie\Permission\PermissionRegistrar::class]->forgetCachedPermissions();

        // Créer les permissions
        Permission::create(['name' => 'create articles']);
        Permission::create(['name' => 'edit articles']);
        Permission::create(['name' => 'delete articles']);
        Permission::create(['name' => 'publish articles']);
        
        Permission::create(['name' => 'create users']);
        Permission::create(['name' => 'edit users']);
        Permission::create(['name' => 'delete users']);
        
        Permission::create(['name' => 'view analytics']);

        // Créer les rôles et assigner les permissions
        $adminRole = Role::create(['name' => 'admin']);
        $adminRole->givePermissionTo(Permission::all());

        $editorRole = Role::create(['name' => 'editor']);
        $editorRole->givePermissionTo([
            'create articles',
            'edit articles',
            'publish articles',
        ]);

        $writerRole = Role::create(['name' => 'writer']);
        $writerRole->givePermissionTo([
            'create articles',
            'edit articles',
        ]);

        $userRole = Role::create(['name' => 'user']);
        // Aucune permission spéciale

        // Créer un utilisateur admin par défaut
        $admin = User::factory()->create([
            'name' => 'Admin User',
            'email' => 'admin@example.com',
        ]);
        $admin->assignRole('admin');
    }
}
```

Exécuter :
```bash
php artisan db:seed --class=RolesAndPermissionsSeeder
```

### Via Code
```php
use Spatie\Permission\Models\Role;
use Spatie\Permission\Models\Permission;

// Créer une permission
Permission::create(['name' => 'edit articles']);

// Créer un rôle
$role = Role::create(['name' => 'editor']);

// Assigner une permission à un rôle
$role->givePermissionTo('edit articles');

// Ou plusieurs
$role->givePermissionTo(['edit articles', 'delete articles']);
```

## Assigner des Rôles aux Utilisateurs

```php
// Assigner un rôle
$user->assignRole('admin');

// Assigner plusieurs rôles
$user->assignRole(['writer', 'editor']);
$user->assignRole('writer', 'editor');

// Synchroniser les rôles (remplace tous les rôles existants)
$user->syncRoles(['writer']);

// Retirer un rôle
$user->removeRole('writer');
```

## Assigner des Permissions Directement

```php
// Donner une permission directement à un utilisateur
$user->givePermissionTo('edit articles');

// Retirer une permission
$user->revokePermissionTo('edit articles');

// Synchroniser les permissions
$user->syncPermissions(['edit articles', 'delete articles']);
```

## Vérification dans le Code

### Vérifier les Rôles
```php
// Vérifier si l'utilisateur a un rôle
if ($user->hasRole('admin')) {
    // ...
}

// Vérifier plusieurs rôles (OU logique)
if ($user->hasAnyRole(['admin', 'editor'])) {
    // ...
}

// Vérifier plusieurs rôles (ET logique)
if ($user->hasAllRoles(['admin', 'editor'])) {
    // ...
}

// Vérifier un rôle exact
if ($user->hasExactRoles(['admin', 'editor'])) {
    // Utilisateur a UNIQUEMENT ces rôles
}
```

### Vérifier les Permissions
```php
// Vérifier une permission
if ($user->can('edit articles')) {
    // ...
}

// Ou via hasPermissionTo
if ($user->hasPermissionTo('edit articles')) {
    // ...
}

// Vérifier plusieurs permissions (OU logique)
if ($user->hasAnyPermission(['edit articles', 'delete articles'])) {
    // ...
}

// Vérifier plusieurs permissions (ET logique)
if ($user->hasAllPermissions(['edit articles', 'delete articles'])) {
    // ...
}
```

## Utilisation dans les Controllers

### Avec Policies (Recommandé)
```php
// ArticlePolicy.php
public function update(User $user, Article $article)
{
    return $user->can('edit articles') && $user->id === $article->user_id;
}

// ArticleController.php
public function update(Request $request, Article $article)
{
    $this->authorize('update', $article);
    
    // Update article
}
```

### Avec Middleware
```php
// Dans routes/web.php
Route::middleware(['role:admin'])->group(function () {
    Route::get('/admin/dashboard', [AdminController::class, 'dashboard']);
});

Route::middleware(['permission:edit articles'])->group(function () {
    Route::put('/articles/{article}', [ArticleController::class, 'update']);
});

// Ou plusieurs rôles/permissions
Route::middleware(['role:admin|editor'])->group(function () {
    // ...
});
```

### Vérification directe
```php
public function update(Request $request, Article $article)
{
    if (!auth()->user()->can('edit articles')) {
        abort(403, 'Non autorisé');
    }
    
    // Update article
}
```

## Utilisation dans Blade

### Directives @role et @can
```blade
@role('admin')
    <a href="/admin/dashboard">Admin Dashboard</a>
@endrole

@hasrole('admin')
    <a href="/admin/settings">Settings</a>
@endhasrole

@hasanyrole('admin|editor')
    <a href="/articles/create">Create Article</a>
@endhasanyrole

@can('edit articles')
    <button>Edit Article</button>
@endcan

@cannot('delete articles')
    <p>Vous ne pouvez pas supprimer cet article</p>
@endcannot
```

## UI d'Administration

### Liste des Rôles
```blade
<!-- resources/views/admin/roles/index.blade.php -->
<div class="space-y-4">
    @foreach($roles as $role)
    <div class="bg-white p-6 rounded-lg shadow">
        <div class="flex justify-between items-center">
            <div>
                <h3 class="text-xl font-bold">{{ $role->name }}</h3>
                <p class="text-sm text-gray-600">
                    {{ $role->permissions->count() }} permissions
                </p>
            </div>
            <div class="flex gap-2">
                <button data-hs-overlay="#edit-role-{{ $role->id }}" class="px-4 py-2 bg-blue-600 text-white rounded-lg">
                    <i data-lucide="edit" class="w-4 h-4"></i>
                </button>
            </div>
        </div>
        
        <div class="mt-4">
            <p class="text-sm font-medium mb-2">Permissions:</p>
            <div class="flex flex-wrap gap-2">
                @foreach($role->permissions as $permission)
                <span class="px-3 py-1 bg-blue-100 text-blue-800 text-xs rounded-full">
                    {{ $permission->name }}
                </span>
                @endforeach
            </div>
        </div>
    </div>
    @endforeach
</div>
```

### Formulaire d'Assignation de Rôle
```blade
<!-- resources/views/admin/users/edit-roles.blade.php -->
<form action="{{ route('admin.users.update-roles', $user) }}" method="POST">
    @csrf
    @method('PUT')
    
    <div class="space-y-4">
        <h3 class="text-lg font-bold">Assigner des rôles à {{ $user->name }}</h3>
        
        @foreach($roles as $role)
        <label class="flex items-center gap-3 p-3 border rounded-lg hover:bg-gray-50 cursor-pointer">
            <input 
                type="checkbox" 
                name="roles[]" 
                value="{{ $role->name }}"
                {{ $user->hasRole($role->name) ? 'checked' : '' }}
                class="rounded"
            >
            <div>
                <p class="font-medium">{{ $role->name }}</p>
                <p class="text-sm text-gray-600">{{ $role->permissions->count() }} permissions</p>
            </div>
        </label>
        @endforeach
    </div>
    
    <button type="submit" class="mt-6 px-4 py-2 bg-blue-600 text-white rounded-lg">
        Mettre à jour les rôles
    </button>
</form>
```

### Controller pour gérer les rôles
```php
// app/Http/Controllers/Admin/UserRoleController.php
namespace App\Http\Controllers\Admin;

use App\Http\Controllers\Controller;
use App\Models\User;
use Illuminate\Http\Request;
use Spatie\Permission\Models\Role;

class UserRoleController extends Controller
{
    public function edit(User $user)
    {
        $roles = Role::all();
        return view('admin.users.edit-roles', compact('user', 'roles'));
    }
    
    public function update(Request $request, User $user)
    {
        $request->validate([
            'roles' => 'array',
            'roles.*' => 'string|exists:roles,name',
        ]);
        
        $user->syncRoles($request->roles ?? []);
        
        return redirect()->back()->with('success', 'Rôles mis à jour');
    }
}
```

## Service Layer

### RoleService
```php
// app/Services/RoleService.php
namespace App\Services;

use App\Models\User;
use Spatie\Permission\Models\Role;
use Spatie\Permission\Models\Permission;

class RoleService
{
    public function getAllRoles()
    {
        return Role::with('permissions')->get();
    }
    
    public function createRole(string $name, array $permissions = [])
    {
        $role = Role::create(['name' => $name]);
        
        if (!empty($permissions)) {
            $role->givePermissionTo($permissions);
        }
        
        return $role;
    }
    
    public function updateRole(Role $role, array $permissions)
    {
        $role->syncPermissions($permissions);
        return $role;
    }
    
    public function deleteRole(Role $role)
    {
        $role->delete();
    }
    
    public function assignRoleToUser(User $user, string $roleName)
    {
        $user->assignRole($roleName);
    }
    
    public function syncUserRoles(User $user, array $roles)
    {
        $user->syncRoles($roles);
    }
}
```

## Guards Multiples

```php
// Créer des permissions pour différents guards
Permission::create(['name' => 'edit articles', 'guard_name' => 'web']);
Permission::create(['name' => 'edit articles', 'guard_name' => 'api']);

// Assigner avec guard
$user->givePermissionTo('edit articles', 'api');

// Vérifier avec guard
$user->hasPermissionTo('edit articles', 'api');
```

## Cache

Le package cache automatiquement les permissions. Pour vider le cache :

```php
app()[\Spatie\Permission\PermissionRegistrar::class]->forgetCachedPermissions();
```

Ou via Artisan :
```bash
php artisan permission:cache-reset
```

## Best Practices

1. **Utiliser des Seeders** pour créer les rôles/permissions
2. **Nommer les permissions en kebab-case** : `create-articles`, `edit-users`
3. **Grouper logiquement** : `articles.*`, `users.*`, `settings.*`
4. **Combiner avec Policies** pour une logique complexe
5. **Cache** : Penser à réinitialiser le cache après modifications
6. **Ne pas créer trop de rôles** : Préférer les permissions granulaires

## Permissions Super Admin

```php
// Dans App\Providers\AuthServiceProvider
use Illuminate\Support\Facades\Gate;

public function boot()
{
    Gate::before(function ($user, $ability) {
        return $user->hasRole('super-admin') ? true : null;
    });
}
```

## Artisan Commands Utiles

```bash
# Créer une permission
php artisan permission:create-permission "edit articles"

# Créer un rôle
php artisan permission:create-role admin

# Afficher les permissions/rôles
php artisan permission:show
```

## Testing

```php
use Spatie\Permission\Models\Role;
use Spatie\Permission\Models\Permission;

public function test_user_can_edit_article_with_permission()
{
    $user = User::factory()->create();
    $permission = Permission::create(['name' => 'edit articles']);
    $user->givePermissionTo($permission);
    
    $this->assertTrue($user->can('edit articles'));
}

public function test_admin_has_all_permissions()
{
    $user = User::factory()->create();
    $role = Role::create(['name' => 'admin']);
    $role->givePermissionTo(Permission::all());
    $user->assignRole($role);
    
    $this->assertTrue($user->hasRole('admin'));
    $this->assertTrue($user->can('any permission'));
}
```

## Erreurs Courantes

### 1. Permission/Role not found
**Problème** : Permission ou rôle n'existe pas
**Solution** : Vérifier les seeders et la base de données

### 2. Cache non actualisé
**Problème** : Changements non pris en compte
**Solution** : `php artisan permission:cache-reset`

### 3. Guard mismatch
**Problème** : Utilisation de guards différents
**Solution** : Spécifier le guard explicitement

## Ressources
- Documentation officielle : https://spatie.be/docs/laravel-permission
- GitHub : https://github.com/spatie/laravel-permission
- Package : https://packagist.org/packages/spatie/laravel-permission
