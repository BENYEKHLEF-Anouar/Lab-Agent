# Capacité : Définir Routes

## 🎯 Objectif
Exposer les points d'entrée de l'application.

## 📝 Format et Structure
- **Fichiers Sortie** : `routes/web.php` ou `routes/api.php`.

## ⚡ Règles d'Implémentation

### 1. Nommage
- Toujours nommer les routes (`->name('posts.show')`).

### 2. Groupement
- Utiliser `Route::controller()` ou `Route::resource()` pour grouper.
- Appliquer les middlewares (auth) via `Route::middleware()`.

## ✅ Points de Contrôle (Definition of Done)
- [ ] Noms uniques.
- [ ] Middlewares corrects.
