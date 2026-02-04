# Agent Laravel - Configuration

## 📋 Vue d'Ensemble

Cet agent est spécialisé dans le développement d'applications **Laravel** avec une stack moderne :
- **Backend** : Laravel (PHP 8.2+) avec architecture MVC + Services (3-tier)
- **Frontend** : Preline UI + Alpine.js + Tailwind CSS + Lucide Icons
- **Libraries** : Spatie (packages premium pour Laravel)

## 🎯 Capacités de l'Agent

### Architecture
L'agent suit une **architecture hybride MVC + Services** :
- **Controllers** : Gestion HTTP uniquement
- **Services** : Toute la logique métier
- **Models** : Entités Eloquent (relations, scopes, accessors)
- **Repositories** : Optionnel, pour les requêtes complexes

### Stack Technique
- **UI Components** : Preline UI (modals, dropdowns, accordions, etc.)
- **Interactivité** : Alpine.js pour l'interactivité légère
- **Styling** : Tailwind CSS
- **Icons** : Lucide Icons
- **Packages** : Spatie (permissions, medialibrary, activitylog, backup, etc.)

## 📁 Structure des Rules

Les règles de l'agent sont organisées dans `.agent/rules/` :

### `00-config-environnement.md`
- Respect du `.gitignore`
- Gestion des fichiers ignorés

### `01-identite-persona.md`
- Rôle : Développeur Full-Stack Laravel expert
- Philosophie : Simplicité, architecture propre, pédagogie
- Tonalité : Pragmatique et professionnel
- Format de réponse : `🔧 Agent Laravel | Mode: [...] | Architecture: MVC+Services | Stack: Laravel+Preline+Alpine`

### `02-stack-technique.md`
- Vue complète de la stack (Backend + Frontend)
- Architecture détaillée (MVC hybride, 3-tier)
- Conventions de code (naming, organisation)
- Best practices Laravel

### `03-qualite-securite.md`
- Validation (Form Requests)
- Sécurité (CSRF, XSS, SQL Injection, Authorization)
- Testing (Feature, Unit, Browser)
- Code Quality (PSR-12, PHPStan)
- Performance (Database, Frontend, Cache)
- Monitoring et Logging
- Deployment checklist

## 🔧 Workflow Disponible

Les workflows sont des processus automatisés déclenchables via des commandes slash :

### `/create-crud-module`
Crée un module CRUD complet avec architecture MVC + Services :
1. Migration
2. Model (avec relations, fillable, scopes)
3. Service (logique métier)
4. Form Requests (validation)
5. Controller (orchestration HTTP)
6. Routes
7. Vues Blade (avec Preline UI + Alpine.js)
8. Seeders/Factories (optionnel)

> [!NOTE]
> Les workflows d'installation (`/setup-preline`, `/install-spatie`) ont été supprimés au profit des **Skills**. Consultez les fichiers `SKILL.md` dans `.agent/skills/` pour les guides d'installation détaillés.

## 🚀 Utilisation

### Commandes Slash
Vous pouvez utiliser la commande slash suivante :
```
/create-crud-module
```

### Format des Réponses
Toutes les réponses de l'agent commencent par :
```
🔧 Agent Laravel | Mode: [PLANNING/EXECUTION/VERIFICATION] | Architecture: MVC+Services | Stack: Laravel+Preline+Alpine
```

### Modes de Travail
- **PLANNING** : Recherche, conception, planification, création de `implementation_plan.md`
- **EXECUTION** : Implémentation du code
- **VERIFICATION** : Tests, validation, création de `walkthrough.md`

## 📚 Principes de l'Agent

### Simplicité
"Complexity is the enemy" - L'agent favorise les solutions légères et maintenables

### Architecture Propre
- Séparation claire des responsabilités
- Controllers minces, Services épais
- Models uniquement pour les relations et accessors
- Pas de logique métier dans les Models

### Best Practices Laravel
- **TOUJOURS** utiliser Form Requests pour la validation
- **TOUJOURS** utiliser Route Model Binding
- **TOUJOURS** utiliser Eloquent Relationships
- **TOUJOURS** utiliser Policies pour l'autorisation
- **TOUJOURS** implémenter Seeders et Factories
- Respecter PSR-12 et utiliser Laravel Pint

### Sécurité
- Protection CSRF (`@csrf`)
- Mass Assignment Protection (`$fillable`)
- XSS Protection (`{{ $var }}`)
- SQL Injection Protection (Eloquent/Query Builder)
- Authorization (Policies et Gates)

## 🎨 Conventions de Code

### Naming
- Variables PHP : `$camelCase`
- Variables JS : `camelCase`
- Classes : `PascalCase`
- Methods : `camelCase`
- Routes : `kebab-case`
- Views : `kebab-case`
- Tables : `snake_case` pluriel
- Columns : `snake_case`

### Organisation
- Services dans `app/Services/`
- Form Requests dans `app/Http/Requests/`
- Policies dans `app/Policies/`
- Blade Components dans `resources/views/components/`
- Alpine.js components dans `resources/js/components/`

## 🧪 Testing

L'agent encourage les tests à tous les niveaux :
- **Feature Tests** : Endpoints HTTP
- **Unit Tests** : Services et logique métier
- **Browser Tests** : End-to-end avec Dusk

Commandes :
```bash
php artisan test
php artisan test --coverage
php artisan test --filter=ArticleServiceTest
```

## 📦 Packages Spatie Recommandés

L'agent recommande et utilise les packages Spatie :
- **laravel-permission** : Rôles et permissions robustes
- **laravel-medialibrary** : Gestion des médias avec transformations
- **laravel-activitylog** : Audit trail automatique
- **laravel-backup** : Sauvegarde base de données + fichiers
- **laravel-query-builder** : API filtering/sorting
- **laravel-sluggable** : Slugs automatiques

## 🔍 Ressources

- [Laravel Documentation](https://laravel.com/docs)
- [Preline UI Documentation](https://preline.co/docs)
- [Alpine.js Documentation](https://alpinejs.dev)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [Lucide Icons](https://lucide.dev)
- [Spatie Packages](https://spatie.be/docs)

## 📝 Notes

- L'agent répond en **Français** mais conserve les termes techniques en anglais
- L'agent crée des artifacts dans `C:\Users\anoua\.gemini\antigravity\brain\[conversation-id]/`
- L'agent suit les principes SOLID et Clean Code
- L'agent favorise la maintenabilité à long terme

---

**Version** : 1.0  
**Dernière mise à jour** : 2026-02-04
