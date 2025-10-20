# 📔 Bullet Journal + Zettelkasten + PARA pour Obsidian

Système complet de gestion de projets professionnels combinant :
- 📋 **Bullet Journal** pour le suivi quotidien et la productivité
- 🧠 **Zettelkasten** pour la gestion des connaissances
- 📂 **PARA** pour l'organisation des informations (Projects, Areas, Resources, Archives)

---

## 🎯 À qui s'adresse ce système ?

**Profil idéal** :
- Gestion de **4-7 projets professionnels longs** (3+ mois) simultanément
- Organisation par **client**
- Besoin de tracer : suivi d'avancement, idées stratégiques, documentation technique, réunions
- Revues régulières : **quotidiennes** (matin/soir), **hebdomadaires**, **mensuelles**
- Niveau Obsidian : **intermédiaire**
- Infrastructure : **Desktop + Git**

---

## 📁 Structure du Vault

```
📁 VaultName/
├── 📁 00-Inbox/              # Capture rapide (notes brutes, fichiers temporaires)
├── 📁 01-Daily/              # Notes quotidiennes (format YYYY-MM-DD)
├── 📁 01-Weekly/             # Revues hebdomadaires (format YYYY-Www)
├── 📁 01-Monthly/            # Revues mensuelles (format YYYY-MM)
├── 📁 02-Projects/           # PARA Projects (projets actifs par client)
│   ├── ClientA-Refonte/
│   ├── ClientB-Migration/
│   └── ClientC-Audit/
├── 📁 03-Areas/              # PARA Areas (domaines de responsabilité permanents)
│   ├── Technical-Skills/
│   └── Strategy-Innovation/
├── 📁 04-Resources/          # PARA Resources (veille, références, bibliothèque)
├── 📁 05-Archives/           # PARA Archives (projets terminés, ancien contenu)
├── 📁 06-Zettelkasten/       # Notes de connaissances atomiques réutilisables
├── 📁 07-Meetings/           # Notes de réunions structurées
└── 📁 08-Templates/          # Templates Markdown
    ├── daily-note.md
    ├── weekly-review.md
    ├── monthly-review.md
    ├── project.md
    ├── meeting.md
    ├── zettel.md
    └── idea.md
```

---

## 🔌 Plugins nécessaires

### Installation des plugins

1. Ouvrir Obsidian : **Settings** (⚙️) → **Community plugins**
2. Cliquer sur **Browse** et installer :

#### Essentiels (gratuits)
- ✅ **Templater** - Moteur de templates avec variables dynamiques
- ✅ **Periodic Notes** - Création automatique des notes Daily/Weekly/Monthly
- ✅ **Calendar** - Vue calendrier et navigation rapide
- ✅ **Dataview** - Requêtes dynamiques (dashboards)
- ✅ **Tasks** - Gestion avancée des tâches

3. **Activer** chaque plugin après installation
4. Les configurations sont **déjà pré-configurées** dans `.obsidian/` 🎉

---

## ⚙️ Configuration des plugins

### 1. Periodic Notes

**Déjà configuré automatiquement !** Vérifie simplement que :

- **Daily notes** :
  - Format : `YYYY-MM-DD`
  - Dossier : `01-Daily`
  - Template : `08-Templates/daily-note.md`

- **Weekly notes** :
  - Format : `YYYY-[W]ww`
  - Dossier : `01-Weekly` ⚠️ (dossier séparé)
  - Template : `08-Templates/weekly-review.md`

- **Monthly notes** :
  - Format : `YYYY-MM`
  - Dossier : `01-Monthly` ⚠️ (dossier séparé)
  - Template : `08-Templates/monthly-review.md`

### 2. Templater

**Déjà configuré automatiquement !** Vérifie dans Settings → Templater :

- **Template folder** : `08-Templates`
- **Trigger on file creation** : ✅ Activé
- **Folder templates** (automatisation par dossier) :
  - `02-Projects` → `project.md`
  - `07-Meetings` → `meeting.md`
  - `06-Zettelkasten` → `zettel.md`

### 3. Calendar

Aucune configuration nécessaire. Utilise les paramètres de Periodic Notes.

### 4. Dataview

Aucune configuration nécessaire au démarrage. Utilisé dans les templates pour les requêtes dynamiques.

### 5. Tasks

Configure selon préférences (optionnel) :
- Date format : `YYYY-MM-DD`
- Global task filter : `#task` (si tu veux filtrer)

---

## 🚀 Démarrage rapide

### Jour 1 : Configuration initiale (15 min)

1. **Cloner ce repository Git** :
   ```bash
   git clone [votre-url-git] MonVault
   cd MonVault
   ```

2. **Ouvrir dans Obsidian** :
   - Obsidian → **Open folder as vault** → Sélectionner `MonVault`

3. **Installer les plugins** (voir section Plugins ci-dessus)

4. **Créer ta première note quotidienne** :
   - Cliquer sur l'icône **Calendar**
   - Cliquer sur aujourd'hui → note automatiquement créée avec template ! 🎉

### Jour 2-7 : Mise en place des projets

1. **Créer tes projets actifs** :
   - Aller dans `02-Projects/`
   - Créer nouveau dossier : `ClientX-NomProjet`
   - Créer note `_index.md` dans ce dossier → template `project.md` appliqué automatiquement
   - Remplir les métadonnées (client, deadline, budget...)

2. **Personnaliser les domaines** (Areas) :
   - `03-Areas/Competences-Techniques/` → créer notes sur tes compétences clés
   - `03-Areas/Strategie-Innovation/` → documenter tes axes stratégiques

3. **Commencer le Zettelkasten** :
   - Quand tu lis un article ou as une idée réutilisable → créer note dans `06-Zettelkasten/`
   - Template `zettel.md` appliqué automatiquement
   - Lier avec `[[autres notes]]`

---

## 📅 Workflows quotidiens

### 🌅 Routine du matin (10 min)

1. **Ouvrir la daily note** (via Calendar ou `Ctrl/Cmd + D`)
2. Remplir **Revue Matinale** :
   - **Priorités du jour** : 3 tâches max
   - **Projets actifs** : lister les projets à toucher aujourd'hui
   - **Intention** : une phrase sur l'état d'esprit

### 🌙 Routine du soir (10 min)

1. **Remplir Revue du Soir** :
   - **Réalisations** : ce qui a été accompli
   - **Apprentissages** : ce que tu as appris
   - **À reporter demain** : tâches non finies
   - **Réflexions** : pensées libres

### 📅 Revue hebdomadaire (30-45 min)

**Quand** : Vendredi après-midi ou Dimanche soir

1. Créer **weekly note** :
   - Méthode 1 : Via Calendar (cliquer sur numéro de semaine)
   - Méthode 2 : `Ctrl/Cmd + P` → "Open weekly note"
   - Note créée dans `01-Weekly/` (ex: `2024-W42.md`)
2. **Revue par projet** : avancement, blocages, prochaines étapes
3. **Idées & Réflexions** : capturer insights de la semaine
4. **Actions semaine prochaine** : planifier 3-5 actions clés
5. **Bilan** : points positifs, améliorations, focus

### 📆 Revue mensuelle (1-2h)

**Quand** : Dernier jour du mois

1. Créer **monthly note** :
   - Méthode 1 : Via Calendar (créer manuellement dans `01-Monthly/`)
   - Méthode 2 : `Ctrl/Cmd + P` → "Open monthly note"
   - Note créée dans `01-Monthly/` (ex: `2024-10.md`)
2. **Bilan objectifs** : taux de réalisation
3. **Revue projets** : tableau de bord complet
4. **Métriques** : KPIs et évolution
5. **Zettelkasten** : voir les nouvelles notes créées (query Dataview automatique)
6. **Planification mois prochain** : priorités stratégiques

---

## 🧠 Utiliser le Zettelkasten

### Principe : Notes atomiques réutilisables

**Quand créer une note Zettelkasten ?**
- Tu lis un concept utile (article, livre, formation)
- Tu as une idée technique/stratégique réutilisable
- Tu veux documenter une solution à un problème récurrent

**Processus** :
1. Créer note dans `06-Zettelkasten/`
2. **Titre** : concept clair (ex: "Pattern Strategy pour API REST")
3. **Concept principal** : résumé en 1 phrase
4. **Développement** : explication + exemples
5. **Liens** : relier avec `[[autres notes]]`
6. **Métadonnées** : domaine, statut (🌱 Seedling → 🌳 Evergreen)

**Statuts de maturité** :
- 🌱 **Seedling** : idée nouvelle, peu développée
- 🌿 **Budding** : note enrichie, quelques connexions
- 🌳 **Evergreen** : note mature, bien connectée, utilisée régulièrement

---

## 🗂️ Système PARA expliqué

### 📂 Projects (02-Projects)
**Objectif à court terme** avec **date de fin**

Exemples :
- `ClientA-Refonte-SiteWeb/`
- `ClientB-Migration-Cloud/`
- `ClientC-Audit-Securite/`

**Organisation** :
```
02-Projects/
└── ClientA-Refonte/
    ├── _index.md (vue projet complète)
    ├── specifications.md
    ├── architecture.md
    └── suivi-taches.md
```

### 📑 Areas (03-Areas)
**Responsabilités continues** sans date de fin

Exemples :
- `Technical-Skills/` : compétences techniques, veille techno, formations, certifications
- `Strategy-Innovation/` : stratégie, réflexions, innovations, veille business

**Structure suggérée** :
```
03-Areas/
└── Technical-Skills/
    ├── _index.md (vue d'ensemble compétences)
    └── notes-specific/
```

### 📚 Resources (04-Resources)
**Sujets d'intérêt** : références, veille, articles, checklists, guides

Exemples :
- `AWS-Documentation.md` : liens et ressources AWS
- `Next-js-Performance-Checklist.md` : checklist optimisation performance
- `Design-Patterns-Catalog.md` : catalogue patterns réutilisables
- `Security-Resources.md` : guides sécurité, OWASP, etc.

### 🗄️ Archives (05-Archives)
**Projets terminés**, ancien contenu

Quand archiver :
- Projet complété → déplacer de `02-Projects` vers `05-Archives`
- Garder structure pour référence future

**Structure** :
```
05-Archives/
└── ClientX-MVP-Ecommerce/
    ├── _index.md (résumé projet archivé)
    └── docs/ (documentation projet)
```

---

## 📊 Dashboards avec Dataview

### Dashboard Projets Actifs

Créer `02-Projects/_dashboard.md` :

```markdown
# 📊 Dashboard Projets

## Projets en cours

\`\`\`dataview
TABLE status as Statut, priority as Priorité, deadline as Deadline, budget as Budget
FROM "02-Projects"
WHERE status = "🔵 En cours"
SORT priority DESC, deadline ASC
\`\`\`

## Projets haute priorité

\`\`\`dataview
TABLE client, deadline, budget
FROM "02-Projects"
WHERE priority = "⚠️ Haute" AND status = "🔵 En cours"
SORT deadline ASC
\`\`\`
```

### Dashboard Réunions à venir

Créer `07-Meetings/_upcoming.md` :

```markdown
# 🤝 Réunions à venir

\`\`\`dataview
TABLE date, time, project, duration
FROM "07-Meetings"
WHERE date >= date(today)
SORT date ASC
LIMIT 10
\`\`\`
```

---

## 🔄 Git : Versioning & Synchronisation

### Configuration initiale

```bash
git init
git add .
git commit -m "Initial commit: Bullet Journal + Zettelkasten + PARA setup"
git remote add origin [votre-url-git]
git push -u origin main
```

### Workflow quotidien

```bash
# Le matin : récupérer les changements
git pull

# Le soir : sauvegarder
git add .
git commit -m "Daily update: $(date +%Y-%m-%d)"
git push
```

### .gitignore fourni

Le fichier `.gitignore` exclut automatiquement :
- `.obsidian/workspace*` (configurations locales)
- `.obsidian/cache` (cache Obsidian)
- `.DS_Store` (macOS)
- `.trash/` (corbeille Obsidian)

**Inclut** : templates, configurations plugins, structure

---

## 💡 Astuces & Bonnes pratiques

### Capture rapide

**Inbox** : toujours capturer dans `00-Inbox/` d'abord
- Idée rapide → `00-Inbox/idee-YYYY-MM-DD.md`
- Fichier reçu → `00-Inbox/attachments/`
- **Traiter l'inbox** régulièrement (hebdo) :
  - Transformer en projet, zettel, ou supprimer

### Liens intelligents

- **Projets** : `[[02-Projects/ClientA-Refonte/_index|ClientA Refonte]]`
- **Zettelkasten** : `[[Pattern-Strategy-API]]`
- **Réunions** : `[[2024-10-20-Kickoff-ClientA]]`

### Tags vs Dossiers

**Dossiers** pour structure (PARA)
**Tags** pour catégorisation transversale :
- `#urgent` `#bloqué` `#idee` `#technique` `#strategie`

### Raccourcis utiles

| Action | Raccourci |
|--------|-----------|
| Créer daily note | `Ctrl/Cmd + D` (via Calendar) |
| Recherche | `Ctrl/Cmd + O` |
| Graph view | `Ctrl/Cmd + G` |
| Command palette | `Ctrl/Cmd + P` |

---

## 🆘 Troubleshooting

### Les templates ne s'appliquent pas automatiquement

1. Vérifier **Templater** activé : Settings → Community plugins
2. Vérifier **Folder templates** configurés : Settings → Templater
3. Redémarrer Obsidian

### Les dates dans templates ne fonctionnent pas

- Utilise la syntaxe Templater : `{{date:YYYY-MM-DD}}`
- Vérifier que **Templater** est activé

### Dataview queries ne s'affichent pas

1. Activer **Dataview** : Settings → Community plugins
2. Vérifier syntaxe : trois backticks + `dataview`
3. Activer **JavaScript Queries** dans Settings → Dataview (si nécessaire)

### Git conflicts

```bash
# Récupérer version distante (écraser local)
git fetch origin
git reset --hard origin/main

# Ou fusionner manuellement
git pull
# Résoudre conflits dans fichiers
git add .
git commit -m "Merge conflicts resolved"
git push
```

---

## 🎓 Ressources complémentaires

### Méthodes
- **Bullet Journal** : [bulletjournal.com](https://bulletjournal.com)
- **Zettelkasten** : [zettelkasten.de](https://zettelkasten.de)
- **PARA** : Tiago Forte - "Building a Second Brain"

### Obsidian
- Documentation : [help.obsidian.md](https://help.obsidian.md)
- Forum : [forum.obsidian.md](https://forum.obsidian.md)
- Discord communautaire

### Plugins
- Templater : [github.com/SilentVoid13/Templater](https://github.com/SilentVoid13/Templater)
- Dataview : [github.com/blacksmithgu/obsidian-dataview](https://github.com/blacksmithgu/obsidian-dataview)

---

## 🚀 Prochaines étapes

1. ✅ Installer plugins
2. ✅ Créer première daily note
3. ✅ Créer 2-3 projets actifs
4. ✅ Documenter domaines (Areas)
5. ✅ Créer première note Zettelkasten
6. ✅ Faire première revue hebdomadaire
7. 🔄 Itérer et personnaliser !

---

**Bon courage dans ton organisation ! 🎯📔🧠**
