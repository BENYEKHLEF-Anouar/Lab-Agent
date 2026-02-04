---
name: Spatie Media Library
description: Expert en gestion des médias avec spatie/laravel-medialibrary
---

# Skill: Spatie Media Library

## Description
Ce skill permet de gérer efficacement les fichiers médias (images, documents, vidéos) dans Laravel en utilisant le package `spatie/laravel-medialibrary`.

## Quand utiliser ce skill
- Upload et gestion d'images
- Génération automatique de thumbnails
- Conversion d'images (redimensionnement, recadrage)
- Gestion de fichiers multiples par modèle
- Organisation des médias en collections
- Responsive images

## Installation

```bash
composer require spatie/laravel-medialibrary
```

### Publier et migrer
```bash
php artisan vendor:publish --provider="Spatie\MediaLibrary\MediaLibraryServiceProvider"
php artisan migrate
```

## Configuration de Base

### Implémenter HasMedia dans le Model
```php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Spatie\MediaLibrary\HasMedia;
use Spatie\MediaLibrary\InteractsWithMedia;

class Article extends Model implements HasMedia
{
    use InteractsWithMedia;
    
    // Optionnel: Enregistrer les collections de médias
    public function registerMediaCollections(): void
    {
        $this->addMediaCollection('images')
            ->useDisk('public');
            
        $this->addMediaCollection('documents')
            ->acceptsMimeTypes(['application/pdf', 'application/msword']);
            
        $this->addMediaCollection('featured_image')
            ->singleFile(); // Une seule image
    }
}
```

## Upload de Médias

### Upload Simple
```php
// Depuis une requête
$article->addMedia($request->file('image'))
    ->toMediaCollection('images');

// Depuis un chemin
$article->addMedia('/path/to/file.jpg')
    ->toMediaCollection('images');

// Depuis une URL
$article->addMediaFromUrl('https://example.com/image.jpg')
    ->toMediaCollection('images');
```

### Upload avec Nom Personnalisé
```php
$article->addMedia($request->file('image'))
    ->usingName('Article featured image')
    ->usingFileName('custom-filename.jpg')
    ->toMediaCollection('images');
```

### Upload avec Propriétés Custom
```php
$article->addMedia($request->file('image'))
    ->withCustomProperties(['alt' => 'Image description', 'caption' => 'My caption'])
    ->toMediaCollection('images');
```

## Récupération des Médias

### Obtenir tous les médias
```php
$medias = $article->getMedia('images');
```

### Obtenir le premier média
```php
$media = $article->getFirstMedia('images');
```

### Obtenir l'URL
```php
$url = $article->getFirstMediaUrl('images');

// Avec conversion (thumbnail)
$url = $article->getFirstMediaUrl('images', 'thumb');
```

### Obtenir le chemin
```php
$path = $article->getFirstMediaPath('images');
```

## Conversions d'Images

### Définir les Conversions
```php
use Spatie\MediaLibrary\MediaCollections\Models\Media;

class Article extends Model implements HasMedia
{
    use InteractsWithMedia;
    
    public function registerMediaConversions(Media $media = null): void
    {
        $this->addMediaConversion('thumb')
            ->width(150)
            ->height(150)
            ->sharpen(10);
            
        $this->addMediaConversion('medium')
            ->width(800)
            ->height(600)
            ->keepOriginalImageFormat();
            
        $this->addMediaConversion('large')
            ->width(1920)
            ->height(1080)
            ->format('webp')
            ->quality(90);
            
        // Responsive images
        $this->addMediaConversion('responsive')
            ->withResponsiveImages();
    }
}
```

### Conversions Avancées
```php
public function registerMediaConversions(Media $media = null): void
{
    // Fit (crop to exact size)
    $this->addMediaConversion('square')
        ->fit('crop', 300, 300);
        
    // Contain (fit inside dimensions)
    $this->addMediaConversion('contained')
        ->fit('contain', 800, 600)
        ->background('ffffff');
        
    // Optimisation automatique
    $this->addMediaConversion('optimized')
        ->width(1200)
        ->optimize();
        
    // Watermark
    $this->addMediaConversion('watermarked')
        ->watermark(public_path('watermark.png'))
        ->watermarkPosition('bottom-right')
        ->watermarkWidth(100)
        ->watermarkHeight(40);
}
```

## Utilisation dans les Controllers

### ArticleController avec Upload
```php
namespace App\Http\Controllers;

use App\Models\Article;
use App\Services\ArticleService;
use Illuminate\Http\Request;

class ArticleController extends Controller
{
    public function __construct(
        private ArticleService $articleService
    ) {}
    
    public function store(Request $request)
    {
        $request->validate([
            'title' => 'required|string|max:255',
            'content' => 'required|string',
            'featured_image' => 'nullable|image|max:2048',
            'gallery.*' => 'nullable|image|max:2048',
        ]);
        
        $article = $this->articleService->create($request->all());
        
        // Upload featured image
        if ($request->hasFile('featured_image')) {
            $article->addMedia($request->file('featured_image'))
                ->toMediaCollection('featured_image');
        }
        
        // Upload gallery images
        if ($request->hasFile('gallery')) {
            foreach ($request->file('gallery') as $image) {
                $article->addMedia($image)->toMediaCollection('gallery');
            }
        }
        
        return redirect()->route('articles.show', $article)
            ->with('success', 'Article créé avec succès');
    }
    
    public function update(Request $request, Article $article)
    {
        $request->validate([
            'title' => 'required|string|max:255',
            'featured_image' => 'nullable|image|max:2048',
        ]);
        
        $this->articleService->update($article->id, $request->all());
        
        // Remplacer l'image featured
        if ($request->hasFile('featured_image')) {
            $article->clearMediaCollection('featured_image');
            $article->addMedia($request->file('featured_image'))
                ->toMediaCollection('featured_image');
        }
        
        return redirect()->back()->with('success', 'Article mis à jour');
    }
}
```

## Service Layer

### MediaService
```php
namespace App\Services;

use Spatie\MediaLibrary\HasMedia;
use Illuminate\Http\UploadedFile;

class MediaService
{
    public function uploadSingle(HasMedia $model, UploadedFile $file, string $collection = 'default'): void
    {
        $model->clearMediaCollection($collection);
        $model->addMedia($file)->toMediaCollection($collection);
    }
    
    public function uploadMultiple(HasMedia $model, array $files, string $collection = 'default'): void
    {
        foreach ($files as $file) {
            $model->addMedia($file)->toMediaCollection($collection);
        }
    }
    
    public function deleteMedia(HasMedia $model, int $mediaId): void
    {
        $media = $model->getMedia()->find($mediaId);
        if ($media) {
            $media->delete();
        }
    }
    
    public function clearCollection(HasMedia $model, string $collection): void
    {
        $model->clearMediaCollection($collection);
    }
    
    public function getMediaUrl(HasMedia $model, string $collection, string $conversion = ''): ?string
    {
        return $model->getFirstMediaUrl($collection, $conversion);
    }
}
```

## Utilisation dans Blade

### Afficher une Image
```blade
@if($article->hasMedia('featured_image'))
    <img 
        src="{{ $article->getFirstMediaUrl('featured_image', 'medium') }}" 
        alt="{{ $article->getFirstMedia('featured_image')->name }}"
        class="w-full h-auto rounded-lg"
    >
@endif
```

### Responsive Images
```blade
@if($article->hasMedia('featured_image'))
    {!! $article->getFirstMedia('featured_image')->img('responsive', ['class' => 'w-full h-auto']) !!}
@endif
```

### Galerie d'Images
```blade
<div class="grid grid-cols-1 md:grid-cols-3 gap-4">
    @foreach($article->getMedia('gallery') as $media)
    <div class="relative group">
        <img 
            src="{{ $media->getUrl('thumb') }}" 
            alt="{{ $media->name }}"
            class="w-full h-48 object-cover rounded-lg"
        >
        <div class="absolute inset-0 bg-black bg-opacity-50 opacity-0 group-hover:opacity-100 transition-opacity flex items-center justify-center">
            <button 
                @click="viewImage('{{ $media->getUrl() }}')"
                class="px-4 py-2 bg-white text-gray-900 rounded-lg"
            >
                <i data-lucide="eye" class="w-4 h-4"></i>
            </button>
            <form action="{{ route('media.delete', $media->id) }}" method="POST" class="ml-2">
                @csrf
                @method('DELETE')
                <button type="submit" class="px-4 py-2 bg-red-600 text-white rounded-lg">
                    <i data-lucide="trash-2" class="w-4 h-4"></i>
                </button>
            </form>
        </div>
    </div>
    @endforeach
</div>
```

### Formulaire d'Upload
```blade
<form action="{{ route('articles.store') }}" method="POST" enctype="multipart/form-data">
    @csrf
    
    <div class="space-y-6">
        <!-- Featured Image -->
        <div>
            <label class="block text-sm font-medium mb-2">Image principale</label>
            <input 
                type="file" 
                name="featured_image" 
                accept="image/*"
                class="block w-full text-sm text-gray-500 file:mr-4 file:py-2 file:px-4 file:rounded-lg file:border-0 file:bg-blue-50 file:text-blue-700 hover:file:bg-blue-100"
            >
            @error('featured_image')
                <p class="mt-1 text-sm text-red-600">{{ $message }}</p>
            @enderror
        </div>
        
        <!-- Gallery -->
        <div x-data="{ files: [] }">
            <label class="block text-sm font-medium mb-2">Galerie d'images</label>
            <input 
                type="file" 
                name="gallery[]" 
                multiple 
                accept="image/*"
                @change="files = Array.from($event.target.files)"
                class="block w-full text-sm text-gray-500 file:mr-4 file:py-2 file:px-4 file:rounded-lg file:border-0 file:bg-blue-50 file:text-blue-700 hover:file:bg-blue-100"
            >
            
            <!-- Preview -->
            <div x-show="files.length > 0" class="mt-4 grid grid-cols-3 gap-4">
                <template x-for="(file, index) in files" :key="index">
                    <div class="relative">
                        <img :src="URL.createObjectURL(file)" class="w-full h-32 object-cover rounded-lg">
                        <p x-text="file.name" class="mt-1 text-xs text-gray-600 truncate"></p>
                    </div>
                </template>
            </div>
        </div>
    </div>
    
    <button type="submit" class="mt-6 px-4 py-2 bg-blue-600 text-white rounded-lg">
        Créer l'article
    </button>
</form>
```

## Upload avec Alpine.js + Drag & Drop

```blade
<div 
    x-data="uploadComponent()" 
    @drop.prevent="handleDrop($event)" 
    @dragover.prevent 
    @dragenter.prevent
    class="border-2 border-dashed border-gray-300 rounded-lg p-8 text-center hover:border-blue-500 transition-colors"
>
    <input 
        type="file" 
        multiple 
        @change="handleFiles($event.target.files)" 
        class="hidden" 
        x-ref="fileInput"
    >
    
    <button type="button" @click="$refs.fileInput.click()" class="px-4 py-2 bg-blue-600 text-white rounded-lg">
        Sélectionner des fichiers
    </button>
    
    <p class="mt-2 text-sm text-gray-600">Ou glissez-déposez des fichiers ici</p>
    
    <!-- Preview -->
    <div x-show="files.length > 0" class="mt-6 grid grid-cols-4 gap-4">
        <template x-for="(file, index) in files" :key="index">
            <div class="relative group">
                <img :src="file.preview" class="w-full h-24 object-cover rounded-lg">
                <button 
                    @click="removeFile(index)" 
                    class="absolute top-0 right-0 bg-red-600 text-white p-1 rounded-full opacity-0 group-hover:opacity-100 transition-opacity"
                >
                    <i data-lucide="x" class="w-3 h-3"></i>
                </button>
            </div>
        </template>
    </div>
</div>

<script>
function uploadComponent() {
    return {
        files: [],
        
        handleFiles(fileList) {
            const newFiles = Array.from(fileList).map(file => ({
                file: file,
                preview: URL.createObjectURL(file)
            }));
            this.files.push(...newFiles);
        },
        
        handleDrop(event) {
            this.handleFiles(event.dataTransfer.files);
        },
        
        removeFile(index) {
            URL.revokeObjectURL(this.files[index].preview);
            this.files.splice(index, 1);
        }
    }
}
</script>
```

## Gestion Dynamic (AJAX)

```blade
<div x-data="mediaGallery({{ $article->id }})">
    <!-- Upload form -->
    <form @submit.prevent="upload">
        <input type="file" @change="selectedFile = $event.target.files[0]" accept="image/*">
        <button type="submit" :disabled="!selectedFile || uploading">
            <span x-show="!uploading">Upload</span>
            <span x-show="uploading" class="flex items-center gap-2">
                <i data-lucide="loader-2" class="w-4 h-4 animate-spin"></i>
                Uploading...
            </span>
        </button>
    </form>
    
    <!-- Gallery -->
    <div class="grid grid-cols-4 gap-4 mt-4">
        <template x-for="media in medias" :key="media.id">
            <div class="relative group">
                <img :src="media.url" class="w-full h-24 object-cover rounded">
                <button @click="deleteMedia(media.id)" class="absolute top-0 right-0 bg-red-600 text-white p-1 rounded opacity-0 group-hover:opacity-100">
                    <i data-lucide="trash-2" class="w-3 h-3"></i>
                </button>
            </div>
        </template>
    </div>
</div>

<script>
function mediaGallery(articleId) {
    return {
        medias: [],
        selectedFile: null,
        uploading: false,
        
        async init() {
            await this.fetchMedias();
        },
        
        async fetchMedias() {
            const response = await fetch(`/api/articles/${articleId}/media`);
            this.medias = await response.json();
        },
        
        async upload() {
            if (!this.selectedFile) return;
            
            this.uploading = true;
            const formData = new FormData();
            formData.append('image', this.selectedFile);
            
            try {
                await fetch(`/api/articles/${articleId}/media`, {
                    method: 'POST',
                    headers: {
                        'X-CSRF-TOKEN': document.querySelector('meta[name="csrf-token"]').content
                    },
                    body: formData
                });
                
                await this.fetchMedias();
                this.selectedFile = null;
            } finally {
                this.uploading = false;
            }
        },
        
        async deleteMedia(mediaId) {
            if (!confirm('Supprimer ce média ?')) return;
            
            await fetch(`/api/media/${mediaId}`, {
                method: 'DELETE',
                headers: {
                    'X-CSRF-TOKEN': document.querySelector('meta[name="csrf-token"]').content
                }
            });
            
            await this.fetchMedias();
        }
    }
}
</script>
```

## Best Practices

1. **Validation** : Toujours valider type et taille de fichier
2. **Collections** : Utiliser des collections distinctes pour différents types  de médias
3. **Conversions** : Toujours générer des thumbnails pour économiser la bande passante
4. **Optimisation** : Utiliser `optimize()` pour réduire la taille des fichiers
5. **Responsive** : Utiliser `withResponsiveImages()` pour les images adaptatives
6. **Sécurité** : Vérifier les types MIME côté serveur
7. **Nettoyage** : Supprimer les médias orphelins périodiquement

## Artisan Commands

```bash
# Régénérer toutes les conversions
php artisan media-library:regenerate

# Nettoyer les médias orphelins
php artisan media-library:clean
```

## Ressources
- Documentation officielle : https://spatie.be/docs/laravel-medialibrary
- GitHub : https://github.com/spatie/laravel-medialibrary
- Package : https://packagist.org/packages/spatie/laravel-medialibrary
