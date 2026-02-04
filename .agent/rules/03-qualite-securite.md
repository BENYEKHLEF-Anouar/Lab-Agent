---
trigger: always_on
---

# Qualité et Sécurité

## Validation et Sécurité

### Form Requests
- **TOUJOURS** utiliser des Form Requests pour la validation
- Créer des classes dédiées : `php artisan make:request StoreArticleRequest`
- Exemple :
```php
class StoreArticleRequest extends FormRequest
{
    public function rules(): array
    {
        return [
            'title' => 'required|string|max:255',
            'content' => 'required|string',
            'image' => 'nullable|image|max:2048',
        ];
    }
}
```

### Protection CSRF
- Toujours inclure `@csrf` dans les formulaires Blade
- Vérifier que le middleware `VerifyCsrfToken` est actif

### Mass Assignment Protection
- Définir `$fillable` ou `$guarded` dans TOUS les Models
- Préférer `$fillable` (whitelist) plutôt que `$guarded` (blacklist)

### XSS Protection
- Utiliser `{{ $variable }}` (échappement automatique) dans Blade
- Utiliser `{!! $html !!}` UNIQUEMENT pour du HTML de confiance
- Sanitiser les inputs utilisateurs

### SQL Injection
- Toujours utiliser Eloquent ou Query Builder (never raw SQL)
- Si raw SQL nécessaire, utiliser des bindings : `DB::select('...', [$param])`

### Authorization
- Utiliser les **Policies** pour toutes les opérations sensibles
- Vérifier les permissions dans les controllers : `$this->authorize('update', $article)`
- Implémenter les Gates si nécessaire

## Testing

### Types de Tests
- **Feature Tests** : Tester les endpoints HTTP
- **Unit Tests** : Tester les Services et logique métier
- **Browser Tests** (Dusk) : Tests end-to-end si nécessaire

### Couverture Minimale
- Tester TOUS les Services métier
- Tester les routes critiques (CRUD, auth)
- Tester les Policies d'autorisation

### Commandes
```bash
# Lancer tous les tests
php artisan test


# Tests spécifiques
php artisan test --filter=ArticleServiceTest
```

## Code Quality

### Standards PSR
- Respecter **PSR-12** (coding style)
- Utiliser **Laravel Pint** pour le formatting automatique
```bash
./vendor/bin/pint
```

### Documentation
- Commenter les méthodes complexes avec PHPDoc
- Documenter les Services et leurs responsabilités
- Créer un `README.md` pour chaque module complexe

## Performance

### Database
- Utiliser les **indexes** sur les colonnes fréquemment recherchées
- Éviter le problème **N+1** avec `with()` (eager loading)
```php
$articles = Article::with('user', 'comments')->get();
```
- Utiliser la **pagination** pour les listes longues
- Mettre en cache les requêtes coûteuses avec `Cache::remember()`

### Frontend
- Minimiser les fichiers JS/CSS avec Vite
- Lazy load les images : `loading="lazy"`
- Utiliser les CDN pour les assets statiques
- Optimiser les images (WebP, compression)

### Cache
- Cacher les vues : `php artisan view:cache`
- Cacher les routes : `php artisan route:cache`
- Cacher la config : `php artisan config:cache`
- Utiliser Redis pour le cache applicatif

## Monitoring et Logging

### Logs
- Utiliser les logs Laravel : `Log::info()`, `Log::error()`
- Configurer les channels dans `config/logging.php`
- Logger les erreurs critiques et les actions sensibles

### Error Handling
- Personnaliser les pages d'erreur (404, 500)
- Utiliser les Exception Handlers
- Ne JAMAIS exposer les stack traces en production

### Monitoring (Production)
- Monitorer les performances avec **Laravel Debugbar** (dev uniquement)

## Deployment

### Checklist Pré-Production
- [ ] Variables `.env` configurées pour la production
- [ ] `APP_DEBUG=false` en production
- [ ] Certificat SSL actif (HTTPS)
- [ ] Caches optimisés (`config:cache`, `route:cache`, `view:cache`)
- [ ] Assets compilés pour production : `npm run build`
- [ ] Migrations testées sur base de staging
- [ ] Backups automatiques configurés (spatie/laravel-backup)
- [ ] Logs configurés et rotatifs
- [ ] Tests passent : `php artisan test`

### Best Practices Deployment
- Utiliser des outils CI/CD (GitHub Actions, GitLab CI)
- Déployer via des scripts automatisés (Laravel Forge, Envoyer, Deployer)
- Avoir un environnement de staging identique à la production
- Faire des rollbacks si nécessaire avec Git tags