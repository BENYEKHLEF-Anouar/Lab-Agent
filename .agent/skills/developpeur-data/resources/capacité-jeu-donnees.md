# Capacité : Créer Jeu de Données (Seeder via CSV)

## 🎯 Objectif
Peupler la base de données avec des données réelles et maîtrisées, importées depuis des fichiers CSV, plutôt que des données aléatoires.

## ⚡ Règles d'Implémentation

### 1. Source de Données (CSV)
- Placer les fichiers CSV dans `database/data/` (créer le dossier si nécessaire).
- Format : En-têtes correspondants (si possible) aux colonnes, séparateur `,` ou `;`.
- Encodage : UTF-8.

### 2. Seeder
- Ne **JAMAIS** utiliser de `Factory` ni de fausses données (`fake()`).
- Lire le fichier CSV ligne par ligne.
- Utiliser `fopen()`, `fgetcsv()` pour parser le fichier.
- Insérer les données via le Modèle (pour profiter des Mutators) ou `DB::table()` (pour la performance de masse).

### 3. Exemple de Code (Seeder)
```php
/**
 * Run the database seeds.
 */
public function run(): void
{
    // Chemin vers le fichier CSV
    $csvFile = fopen(database_path('data/users.csv'), 'r');
    $firstLine = true;

    while (($data = fgetcsv($csvFile, 2000, ',')) !== FALSE) {
        // Ignorer la première ligne (en-têtes)
        if ($firstLine) {
            $firstLine = false;
            continue;
        }

        // Création via Eloquent (recommandé pour la logique)
        User::create([
            'name'      => $data[0],
            'email'     => $data[1],
            'password'  => bcrypt('password'), // Mot de passe par défaut
        ]);
        
        // OU insertion via DB (recommandé pour la vitesse sur gros volumes)
        // DB::table('users')->insert([...]);
    }

    fclose($csvFile);
}
```

## ✅ Points de Contrôle (Definition of Done)
- [ ] Dossier `database/data/` créé.
- [ ] Fichier CSV présent et bien formaté.
- [ ] Seeder implémenté sans `fake()`.
- [ ] Données correctement insérées en base (`php artisan db:seed`).
