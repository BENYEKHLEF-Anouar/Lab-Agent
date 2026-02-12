# Capacité : Créer Service Métier

## 🎯 Objectif
Encapsuler la logique métier complexe dans une classe de Service dédiée, isolée du contrôleur.

## 📝 Format et Structure
- **Fichier Sortie** : `app/Services/[Nom]Service.php`.

## ⚡ Règles d'Implémentation

### 1. Responsabilité Unique
- Un Service par Domaine Métier.
- Pas de dépendances HTTP (`Request`, `Response`).

### 2. Méthodes
- Méthodes publiques explicites correspondant aux cas d'utilisation.
- Typage strict des arguments et retour.

## ✅ Points de Contrôle (Definition of Done)
- [ ] Namespace correct (`App\Services`).
- [ ] Injection des dépendances dans le constructeur.
