# 🤖 Agents Claude pour Bullet Journal

Agents spécialisés pour automatiser la génération de revues hebdomadaires et mensuelles à partir des notes quotidiennes.

## 📋 Agents disponibles

### 1. Weekly Aggregator
**Fichier** : `weekly-aggregator.md`

**Mission** : Générer revues hebdomadaires automatiquement à partir des notes quotidiennes

**Triggers** :
- `/weekly 2024-W42`
- `/weekly` (semaine en cours)
- "génère ma revue hebdomadaire"

**Workflow** :
1. Scanne toutes les dailies de la semaine (lundi-dimanche)
2. Extrait projets actifs, tâches complétées, réunions, apprentissages, idées
3. Agrège par projet avec calcul métriques
4. Génère `01-Weekly/YYYY-Www.md` complète

**Exemple** :
```
/weekly 2024-W42

→ Scanne 01-Daily/2024-10-14.md → 2024-10-20.md
→ Extrait 2 projets, 23 tâches, 3 réunions, 5 apprentissages
→ Génère 01-Weekly/2024-W42.md
```

---

### 2. Monthly Aggregator
**Fichier** : `monthly-aggregator.md`

**Mission** : Générer revues mensuelles stratégiques à partir des revues hebdomadaires

**Triggers** :
- `/monthly 2024-10`
- `/monthly Oct 2024`
- "génère ma revue mensuelle"

**Workflow** :
1. Scanne toutes les weeklies du mois
2. Extrait progression projets (début → fin mois), budgets, vélocités
3. Calcule métriques globales (productivité, Zettelkasten, well-being)
4. Analyse tendances et génère insights stratégiques
5. Définit objectifs mois suivant
6. Génère `01-Monthly/YYYY-MM.md` complète

**Exemple** :
```
/monthly 2024-10

→ Scanne 01-Weekly/2024-W40.md → 2024-W44.md (5 semaines)
→ Extrait progression projets, métriques, apprentissages
→ Calcule : ClientA 45%→65% (+20pts), Productivité 95%
→ Génère 01-Monthly/2024-10.md
```

---

## 🚀 Comment utiliser

### Avec Claude Code

Les agents sont automatiquement détectés par Claude Code si ce dossier `.claude/agents/` est présent.

**Utilisation** :
```bash
# Depuis n'importe où dans le vault
/weekly 2024-W42
/monthly 2024-10

# Ou via langage naturel
"Peux-tu générer ma revue hebdomadaire pour la semaine 42 ?"
"Crée la revue mensuelle d'octobre"
```

### Workflow recommandé

**Hebdomadaire** (chaque dimanche soir ou vendredi) :
```bash
# 1. Assurer que toutes les dailies de la semaine sont remplies
# 2. Lancer l'agent
/weekly

# 3. Réviser la weekly note générée
# 4. Ajuster manuellement si nécessaire (actions semaine prochaine)
```

**Mensuelle** (dernier jour du mois) :
```bash
# 1. Assurer que toutes les weeklies du mois sont complètes
# 2. Lancer l'agent
/monthly

# 3. Réviser la monthly note générée
# 4. Ajuster objectifs mois suivant si nécessaire
```

---

## 📊 Données extraites et calculées

### Weekly Aggregator extrait des dailies :

| Donnée | Source daily | Agrégation |
|--------|-------------|------------|
| **Projets actifs** | Section "Projets actifs aujourd'hui" | Liste unique + fréquence mentions |
| **Tâches complétées** | `[x]` dans section "Tâches" | Total + groupement par projet |
| **Réunions** | Liens `[[07-Meetings/...]]` | Liste + contexte |
| **Apprentissages** | Section "Apprentissages" + 💡 | Synthèse par thème |
| **Idées** | Liens `[[00-Inbox/idee-...]]` | Liste avec statut |
| **Blocages** | Mots-clés "bloqué", ⚠️, 🚨 | Par projet |
| **Humeur/Énergie** | Emoji + score X/10 | Moyennes hebdomadaires |

### Monthly Aggregator extrait des weeklies :

| Donnée | Source weekly | Calcul |
|--------|--------------|--------|
| **Progression projets** | "Avancement : XX%" | Début mois → Fin mois (delta) |
| **Budget consommé** | "Budget : Xj / Yj" | Total mois + burn rate |
| **Vélocité** | "Vélocité : +X pts/sem" | Moyenne + tendance |
| **Heures facturables** | "Heures facturables : Xh / Yh" | Total + ratio |
| **Zettelkasten** | Notes `[[06-Zettelkasten/...]]` | Total + répartition domaines |
| **Well-being** | Humeur + Énergie moyennes | Moyenne mois + tendance |
| **Highlights** | 🏆, ✨, 🚀 markers | Liste synthétique |

---

## ⚙️ Configuration

### Weekly Aggregator

Paramètres par défaut dans l'agent :
```yaml
work_days: [monday, tuesday, wednesday, thursday, friday]
include_weekends: true
detail_level: "medium"
include_mood_metrics: true
min_project_mentions: 1
auto_suggest_actions: true
```

### Monthly Aggregator

Paramètres par défaut dans l'agent :
```yaml
exclude_partial_weeks: false
min_achievement_threshold: 15  # % pour highlight
enable_budget_projection: true
enable_burnout_detection: true
burnout_threshold: 6.0
auto_carry_forward: true
```

**Personnalisation** : Éditer directement les fichiers `.md` des agents pour ajuster les seuils.

---

## 🎯 Qualité des synthèses

### Weekly : Niveau tactique
- Focus : Exécution quotidienne
- Détail : Tâches individuelles, événements spécifiques
- Ton : Opérationnel
- Métriques : Quotidiennes et hebdomadaires

### Monthly : Niveau stratégique
- Focus : Vision d'ensemble et tendances
- Détail : Patterns, progressions, insights
- Ton : Réflexif et stratégique
- Métriques : Mensuelles et comparatives

---

## 🔍 Validation automatique

Les agents effectuent des validations :

**Weekly Aggregator** :
- ✅ Toutes les dailies de la semaine identifiées
- ✅ Tous les projets actifs détectés
- ✅ Liens `[[...]]` valides
- ✅ Métriques calculées cohérentes

**Monthly Aggregator** :
- ✅ Toutes les weeklies du mois identifiées
- ✅ Progressions projets logiques (pas de régressions)
- ✅ Calculs budgets cohérents
- ✅ Liens vers weeklies, projets, Areas valides
- ⚠️ Alertes si données incohérentes

---

## 🛠️ Dépannage

### Weekly note incomplète
**Cause** : Certaines dailies manquent des sections
**Solution** : L'agent passe gracefully les sections manquantes, mais la weekly sera moins riche

### Monthly metrics incorrectes
**Cause** : Weeklies avec données manquantes ou format différent
**Solution** : Vérifier que les weeklies suivent le template standard

### Agent ne trouve pas les notes
**Cause** : Format de nom de fichier incorrect
**Solution** : Vérifier nommage :
- Daily : `YYYY-MM-DD.md` dans `01-Daily/`
- Weekly : `YYYY-Www.md` dans `01-Weekly/`
- Monthly : `YYYY-MM.md` dans `01-Monthly/`

### Liens cassés dans notes générées
**Cause** : Projets/réunions référencés n'existent plus
**Solution** : Nettoyer références obsolètes ou archiver projets terminés

---

## 🚀 Améliorations futures

### Prévues
- [ ] Détection automatique semaine/mois en cours (pas besoin spécifier)
- [ ] Comparaisons période N vs N-1 (évolution)
- [ ] Graphiques ASCII avancés pour tendances
- [ ] Export métriques CSV pour analyse externe
- [ ] Suggestions actions basées sur patterns historiques

### En réflexion
- [ ] Détection burnout risk (mood/energy bas prolongés)
- [ ] ML pour prédire vélocité future
- [ ] Intégration calendrier pour jours fériés
- [ ] Calcul ROI projets si données financières
- [ ] Génération automatique rapports clients

---

## 📚 Voir aussi

- **Templates** : `08-Templates/weekly-review.md`, `monthly-review.md`
- **Documentation** : `README.md` (workflows quotidiens/hebdomadaires/mensuels)
- **Exemples** : `01-Weekly/2024-W42.md`, `01-Monthly/2024-10.md`

---

**Note** : Ces agents sont conçus pour Claude Code mais peuvent être adaptés pour d'autres systèmes d'automatisation (scripts Python, Obsidian Templater, etc.).
