# 🚀 Lab-Agent

Bienvenue dans **Lab-Agent**, un projet Laravel moderne conçu pour une productivité maximale. Ce projet intègre une configuration **Smart Agent** (`.agent/`) pour assister le développement.

---

## 📂 Qu'est-ce que le dossier `.agent` ?

Le dossier `.agent/` contient "l'intelligence" locale de votre assistant IA. Il définit précisément comment l'agent doit coder, les bibliothèques à utiliser et les processus à suivre pour garantir un code propre et cohérent.

Il est divisé en trois piliers :

### 📜 1. Rules (Règles)
Les **Rules** sont les directives permanentes de l'agent. Elles définissent :
- **Architecture** : MVC + Services (3-tier).
- **Sécurité** : Validation systématique, protection CSRF/XSS.
- **Identité** : Expert Laravel pragmatique.
- **Environnement** : Respect strict du `.gitignore`.

### 🎯 2. Skills (Compétences)
Les **Skills** sont des guides techniques détaillés pour chaque technologie utilisée dans le projet. L'agent les consulte pour implémenter des composants :
- **Preline UI** & **Tailwind CSS** (Design)
- **Alpine.js** (Interactivité)
- **Lucide Icons** (Icônes)
- **Spatie Packages** (Permissions & Médias)

### 🔧 3. Workflows (Processus)
Les **Workflows** sont des processus automatisés ou semi-automatisés pour des tâches complexes.
- `/create-crud-module` : Génère un CRUD complet (Migration → Model → Service → Controller → Vues).

