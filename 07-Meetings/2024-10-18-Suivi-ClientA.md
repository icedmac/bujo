---
type: meeting
date: 2024-10-18
time: "15:00"
duration: "1h"
project: "[[02-Projects/ClientA-Refonte-SiteWeb/_index|ClientA Refonte Site Web]]"
tags: [meeting, suivi, clienta]
---

# 🤝 Point d'avancement - Refonte Site Web ClientA

## 📋 Informations

| Champ | Valeur |
|-------|--------|
| **Date** | 2024-10-18 |
| **Heure** | 15:00 - 16:00 |
| **Durée** | 1h |
| **Projet lié** | [[02-Projects/ClientA-Refonte-SiteWeb/_index|ClientA Refonte Site Web]] |
| **Type** | Suivi hebdomadaire |

---

## 👥 Participants

| Nom | Rôle | Organisation |
|-----|------|--------------|
| Thomas Martin | Product Owner | ClientA |
| Alexandre Chen | CTO | ClientA |
| Lucas Moreau | Chef de projet | Agence |
| Julien Rousseau | Lead Developer | Agence |

---

## 🎯 Objectifs de la réunion

- Présenter avancement Phase 2 développement (J+3)
- Démontrer pages Home et About (première itération)
- Recueillir feedbacks et ajustements
- Valider prochaines priorités

---

## 💬 Notes & Discussions

### Démonstration avancement

**Présenté par Julien Rousseau** :

✅ **Setup technique** :
- Repository GitHub configuré
- CI/CD Vercel opérationnel (preview deployments automatiques)
- Intégration Contentful fonctionnelle

✅ **Pages développées** :
- **Homepage** : 90% complète (Hero, Features, Social Proof, CTA)
- **About** : 80% complète (Mission, Timeline interactive, Équipe)
- **Navigation** : Header responsive + Footer

### Feedbacks ClientA

**Thomas Martin (PO)** :
- ✅ Très satisfait du rendu visuel (fidèle aux maquettes)
- ✅ Performance excellente (Lighthouse 94/100 déjà)
- ⚠️ Demande ajustement : Section "Témoignages" homepage → carrousel au lieu de grille statique
- 💡 Suggestion : Ajouter animation scroll sur features (effet fade-in)

**Alexandre Chen (CTO)** :
- ✅ Architecture technique solide
- ✅ Code quality bonne (review PR satisfaisante)
- 💡 Suggestion : Implémenter Open Graph tags dès maintenant (SEO partage social)

---

## ✅ Décisions prises

| # | Décision | Contexte | Impact |
|---|----------|----------|--------|
| 1 | **Reporter feature "Comparateur concurrents"** en Phase 4 | Scope Phase 2 trop chargé, risque deadline | Allègement charge, focus MVP |
| 2 | **Ajustement témoignages** (carrousel au lieu grille) | Feedback UX Thomas Martin | 1 jour dev supplémentaire |
| 3 | **Prioriser page Pricing** semaine prochaine | Business priority élevée | Planning ajusté |

---

## 🎯 Actions

| Action | Responsable | Deadline | Statut | Priorité |
|--------|-------------|----------|--------|----------|
| Ajuster témoignages homepage (carrousel) | Julien Rousseau | 22/10 | 🔵 | Haute |
| Ajouter animations scroll features | Camille Petit | 25/10 | ⏳ | Moyenne |
| Implémenter Open Graph tags | Julien Rousseau | 21/10 | 🔵 | Haute |
| Développer page Pricing (priorité) | Julien Rousseau | 25/10 | ⏳ | Haute |

---

## 🔄 Prochaines étapes

1. Finaliser ajustements homepage (carrousel, OG tags)
2. Développer page Pricing avec calculateur dynamique
3. Prochaine demo : **25/10** (Pricing + Blog)

---

## 🔗 Liens

### Projet parent
- [[02-Projects/ClientA-Refonte-SiteWeb/_index|ClientA Refonte Site Web]]

### Réunions liées
- [[07-Meetings/2024-10-15-Kickoff-ClientA|Kickoff - 15/10/2024]] (précédente)

---

## 📋 Suivi

- [x] Compte-rendu envoyé (18/10 soir)
- [x] Actions créées dans Notion
- [x] Prochaine réunion planifiée (25/10)
