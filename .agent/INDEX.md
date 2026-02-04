# 📋 Index de l'Agent Laravel

Bienvenue dans la documentation de votre Agent Laravel !

## 🚀 Quick Start

1. **Vue d'ensemble** : Lisez le [SUMMARY.md](SUMMARY.md)
2. **Documentation** : Consultez le [README.md](README.md)
3. **Index** : Ce fichier [INDEX.md](INDEX.md)

---

## 📁 Navigation Rapide

### 📖 Documentation Principale
- [README.md](README.md) - Documentation complète de l'agent
- [SUMMARY.md](SUMMARY.md) - Résumé et guide d'utilisation
- [INDEX.md](INDEX.md) - Ce fichier

### 📜 Rules - 4 Directives Permanentes
| Fichier | Description |
|---------|-------------|
| [00-config-environnement.md](rules/00-config-environnement.md) | Respect du .gitignore |
| [01-identite-persona.md](rules/01-identite-persona.md) | Rôle et philosophie de l'agent |
| [02-stack-technique.md](rules/02-stack-technique.md) | Stack + Architecture MVC+Services |
| [03-qualite-securite.md](rules/03-qualite-securite.md) | Sécurité, tests, performance |

### 🔧 Workflows - 1 Processus Automatisé
| Commande | Fichier | Description |
|----------|---------|-------------|
| `/create-crud-module` | [create-crud-module.md](workflows/create-crud-module.md) | Créer un module CRUD complet |

### 🎯 Skills - 6 Guides Détaillés
| Skill | Fichier | Contenu |
|-------|---------|---------|
| **Preline UI** | [preline-ui/SKILL.md](skills/preline-ui/SKILL.md) | Installation, composants, intégration |
| **Lucide Icons** | [lucide-icons/SKILL.md](skills/lucide-icons/SKILL.md) | Installation, bibliothèque d'icônes |
| **Alpine.js** | [alpine-js/SKILL.md](skills/alpine-js/SKILL.md) | Directives, patterns, intégration |
| **Tailwind CSS** | [tailwind-css/SKILL.md](skills/tailwind-css/SKILL.md) | Configuration, classes, patterns |
| **Spatie Permission** | [spatie-permission/SKILL.md](skills/spatie-permission/SKILL.md) | Installation, rôles, permissions |
| **Spatie Media Library** | [spatie-medialibrary/SKILL.md](skills/spatie-medialibrary/SKILL.md) | Installation, uploads, conversions |

---

## 🎯 Par Cas d'Usage

### Démarrer un Nouveau Projet
1. Lire [rules/02-stack-technique.md](rules/02-stack-technique.md) - Comprendre l'architecture
2. Installer Preline : [skills/preline-ui/SKILL.md](skills/preline-ui/SKILL.md)
3. Créer le premier module : `/create-crud-module`

### Installer Preline UI + Lucide
→ Consulter [skills/preline-ui/SKILL.md](skills/preline-ui/SKILL.md) - Section "Installation"

### Installer Spatie Packages
- **Permission** : [skills/spatie-permission/SKILL.md](skills/spatie-permission/SKILL.md) - Section "Installation"
- **Media Library** : [skills/spatie-medialibrary/SKILL.md](skills/spatie-medialibrary/SKILL.md) - Section "Installation"

### Utiliser les Composants UI
- **Modals, Dropdowns** : [skills/preline-ui/SKILL.md](skills/preline-ui/SKILL.md)
- **Icônes** : [skills/lucide-icons/SKILL.md](skills/lucide-icons/SKILL.md)
- **Interactivité** : [skills/alpine-js/SKILL.md](skills/alpine-js/SKILL.md)

### Comprendre l'Architecture
→ [rules/02-stack-technique.md](rules/02-stack-technique.md) - Architecture MVC+Services 3-tier

### Assurer la Qualité du Code
→ [rules/03-qualite-securite.md](rules/03-qualite-securite.md) - Validation, tests, sécurité

---

## 🎨 Stack Technique

### Frontend
- UI → [preline-ui/SKILL.md](skills/preline-ui/SKILL.md)
- Icons → [lucide-icons/SKILL.md](skills/lucide-icons/SKILL.md)
- JS → [alpine-js/SKILL.md](skills/alpine-js/SKILL.md)
- CSS → [tailwind-css/SKILL.md](skills/tailwind-css/SKILL.md)

### Backend
- Architecture → [rules/02-stack-technique.md](rules/02-stack-technique.md)
- Permissions → [spatie-permission/SKILL.md](skills/spatie-permission/SKILL.md)
- Médias → [spatie-medialibrary/SKILL.md](skills/spatie-medialibrary/SKILL.md)

---

## 📊 Structure de l'Agent (15 fichiers)

```
.agent/
├── 📄 Docs (3)       - Navigation
├── 📜 Rules (4)      - Directives permanentes
├── 🔧 Workflows (1)  - Processus automatisé
└── 🎯 Skills (6)     - Documentation détaillée
```

### Philosophie
- **Rules** → L'agent suit ces directives en permanence
- **Skills** → Consultés quand on travaille avec une bibliothèque
- **Workflows** → Processus automatisé pour créer un module

---

## 💡 Principe de Responsabilité Unique

| Type | Quand consulter | Exemples |
|------|-----------------|----------|
| **Rules** | Jamais (toujours actif) | Architecture, Sécurité |
| **Skills** | Quand on utilise X | Installation Preline, Lucide |
| **Workflows** | Quand on crée Y | Module CRUD complet |

---

## 📝 Statistiques

- **Total** : 14 fichiers
- **Docs** : 3 directives de navigation (README, INDEX, SUMMARY)
- **Rules** : 4 directives permanentes
- **Skills** : 6 guides complets
- **Workflows** : 1 processus automatisé
- **Duplication** : 0 ✅

---

## ✨ Architecture Optimale

Cette structure suit les meilleurs principes :
- ✅ **Single Responsibility** : Chaque fichier a un rôle unique
- ✅ **DRY** : Aucune duplication
- ✅ **Séparation des préoccupations** : Rules / Skills / Workflows
- ✅ **Maintenabilité** : Facile à mettre à jour

---

**🚀 Bon développement avec votre Agent Laravel !**
