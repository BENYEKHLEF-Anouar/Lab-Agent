# Capacité : Intégrer Composant Preline UI

## 🎯 Objectif
Intégrer les composants interactifs de la bibliothèque Preline UI (Modales, Accordéons, Dropdowns).

## ⚡ Règles d'Implémentation

### 1. Structure HTML
- Copier la structure exacte depuis la documentation Preline UI.
- Conserver les attributs `data-hs-*` qui pilotent l'interactivité.

### 2. Adaptation
- Adapter les classes de couleur/taille pour correspondre au design system du projet.
- S'assurer que les IDs sont uniques sur la page.

### 3. Initialisation JS
- Si le contenu est chargé dynamiquement (AJAX/Livewire), réinitialiser Preline :
  ```js
  HSStaticMethods.autoInit();
  ```

## ✅ Points de Contrôle (Definition of Done)
- [ ] Le composant s'affiche correctement.
- [ ] L'interaction (ouverture/fermeture) fonctionne.
- [ ] Pas d'erreurs JS en console.
