# Capacité : Implémenter Logique (Méthode)

## 🎯 Objectif
Coder l'algorithme métier, la transaction ou le traitement de données au sein d'une méthode de Service.

## ⚡ Règles d'Implémentation

### 1. Robustesse
- Utiliser `DB::transaction` pour les écritures multiples.
- Gestion des erreurs avec des Exceptions métiers (`throw new BusinessException`).

### 2. Retour
- Retourner des objets (Model) et non des tableaux.

## ✅ Points de Contrôle (Definition of Done)
- [ ] Code atomique.
- [ ] Exceptions gérées.
