---
type: meeting
date: 2024-10-15
time: "14:00"
duration: "2h"
project: "[[02-Projects/ClientA-Refonte-SiteWeb/_index|ClientA Refonte Site Web]]"
tags: [meeting, kickoff, clienta]
---

# 🤝 Kickoff Projet - Refonte Site Web ClientA

## 📋 Informations

| Champ | Valeur |
|-------|--------|
| **Date** | 2024-10-15 |
| **Heure** | 14:00 - 16:00 |
| **Durée** | 2h |
| **Projet lié** | [[02-Projects/ClientA-Refonte-SiteWeb/_index|ClientA Refonte Site Web]] |
| **Type** | Kickoff officiel |
| **Lieu** | Visioconférence (Google Meet) |

---

## 👥 Participants

| Nom | Rôle | Organisation |
|-----|------|--------------|
| Marie Dubois | Sponsor | ClientA |
| Thomas Martin | Product Owner | ClientA |
| Alexandre Chen | CTO | ClientA |
| Sophie Bernard | Chef Marketing | ClientA |
| **Notre équipe** | | |
| Lucas Moreau | Chef de projet | Agence |
| Camille Petit | Designer UX/UI | Agence |
| Julien Rousseau | Lead Developer Frontend | Agence |

---

## 🎯 Objectifs de la réunion

1. Aligner équipes sur vision et objectifs projet
2. Valider définitivement maquettes Figma (dernière itération)
3. Présenter planning détaillé Phase 2 (Développement)
4. Organiser accès techniques (Contentful, Vercel, GA4)
5. Définir processus de communication et rituels

---

## 📝 Ordre du jour

1. **Introduction et présentation équipes** (15min)
2. **Rappel contexte et objectifs business** (15min)
3. **Validation maquettes Figma finales** (30min)
4. **Présentation architecture technique** (20min)
5. **Planning Phase 2 et jalons** (20min)
6. **Organisation projet : rituels, communication** (15min)
7. **Questions / Réponses** (5min)

---

## 💬 Notes & Discussions

### 1. Introduction et présentation équipes

- Tour de table des participants
- Marie Dubois (Sponsor) : Projet stratégique pour ClientA, besoin site qui reflète innovation produit SaaS
- Thomas Martin (PO) : Axe prioritaire = acquisition leads B2B, taux conversion landing pages

### 2. Rappel contexte et objectifs business

**Contexte actuel** (présenté par Sophie Bernard - Marketing) :
- Site WordPress 2019 = vieillissant, performances médiocres
- Trafic organique -15% YoY → besoin impératif amélioration SEO
- Taux rebond élevé (68%) sur pages clés
- Difficulté mise à jour contenu (équipe marketing bloquée par technique)

**Objectifs quantifiés** :
- **Performance** : Lighthouse score > 90 (actuellement 45)
- **Acquisition** : +30% leads qualifiés formulaires (baseline 150/mois)
- **Conversion** : +25% taux conversion landing pages (actuellement 2.1%)
- **SEO** : Maintien positions + amélioration Core Web Vitals
- **Autonomie** : Équipe marketing autonome sur contenu (CMS Headless)

**Budget & Timeline confirmés** :
- 60 000€ / 45 jours
- Go-live : 31 décembre 2024 (impératif business)

### 3. Validation maquettes Figma finales

**Présentation** par Camille Petit (Designer) :
- Walkthrough complet design system (couleurs, typographie, composants)
- Présentation maquettes 5 pages principales (Home, About, Pricing, Blog, Contact)
- Démonstration responsive (mobile, tablet, desktop)

**Feedback ClientA** :
- ✅ Validation globale très positive
- ✅ Marie Dubois : "Design moderne qui reflète bien notre positionnement tech"
- ⚠️ Ajustement mineur demandé : CTA "Démarrer essai gratuit" plus visible sur Hero (augmenter taille bouton)
- ⚠️ Sophie Bernard : Ajouter section "Témoignages clients" sur homepage (oublié dans wireframes)

**Décisions** :
1. Ajustements mineurs à faire d'ici vendredi 18/10
2. Maquettes finales validées sous réserve ajustements
3. Design system Figma transféré à équipe dev (lien partagé dans Slack)

### 4. Présentation architecture technique

**Présentation** par Julien Rousseau (Lead Dev) et Alexandre Chen (CTO ClientA) :

**Stack validée** :
- ✅ Next.js 14 (App Router) : Alexandre approuve choix React Server Components
- ✅ Contentful CMS : Sophie Bernard satisfaite interface utilisateur simple
- ✅ Vercel hosting : Alexandre valide Edge Network performance
- ✅ Monitoring : Sentry + Vercel Analytics

**Questions techniques ClientA** :
- **Q (Alexandre)** : "Peut-on intégrer notre outil analytics interne en plus de GA4 ?"
  - **R** : Oui, Vercel permet custom scripts. On intègrera via Google Tag Manager.

- **Q (Thomas)** : "Migration 200+ pages WordPress : combien de temps ?"
  - **R** : 1 semaine automatisée (export XML → Contentful), 1 semaine revue manuelle qualité.

- **Q (Sophie)** : "Formation équipe marketing sur Contentful ?"
  - **R** : Oui, 1 session 2h prévue fin Phase 2 (décembre).

**Décision architecture** :
- Multi-région pas nécessaire (trafic France uniquement)
- CDN Vercel suffisant pour performance Europe
- Backup Contentful automatique (snapshot quotidien)

### 5. Planning Phase 2 et jalons

**Phase 2 : Développement (Nov 2024)** :
- Semaine 1-2 : Pages principales (Home, About, Pricing)
- Semaine 3 : Blog (listing + articles)
- Semaine 4 : Formulaires, intégrations, SEO technique

**Jalons clés** :
- **08/11** : Demo pages Home + About (validation intermédiaire)
- **22/11** : Demo complète site (toutes pages fonctionnelles)
- **30/11** : Fin développement Phase 2

**Phase 3 : Tests & Déploiement (Déc 2024)** :
- 01-15/12 : Tests, migration contenu
- 16-22/12 : Recette ClientA
- 23-31/12 : Déploiement production

**Risques identifiés** :
- ⚠️ Délais serrés fin année (congés Noël)
- ⚠️ Migration contenu WordPress complexe (200+ pages)
- **Mitigation** : Geler scope Phase 2, reporter features secondaires en Phase 4 post-launch

### 6. Organisation projet

**Rituels décidés** :
- **Daily Standup** : 10h tous les matins (Slack asynchrone)
- **Demo hebdo** : Vendredi 15h (présentation avancement ClientA)
- **Point bloquants** : Ad-hoc sur Slack channel dédié

**Communication** :
- **Slack** : Channel `#clienta-refonte` (équipe mixte agence + ClientA)
- **Email** : Pour décisions officielles et validations
- **Figma** : Commentaires sur maquettes
- **GitHub** : Issues pour bugs/features

**Accès à fournir** :
- ✅ Contentful : Espace créé, accès fournis à Sophie + Thomas
- ✅ Vercel : Compte créé, accès fournis à Alexandre (CTO)
- ✅ GA4 : Accès fournis à notre équipe (tag manager)
- ⏳ Ancien site WordPress : Export XML à fournir par équipe tech ClientA (deadline 18/10)

---

## ✅ Décisions prises

| # | Décision | Contexte | Impact |
|---|----------|----------|--------|
| 1 | **Maquettes Figma validées** (sous réserve ajustements mineurs) | Design présenté et approuvé par équipe ClientA | Démarrage dev Phase 2 possible dès 18/10 |
| 2 | **Stack technique confirmée** (Next.js + Contentful + Vercel) | Validation CTO Alexandre Chen | Architecture finalisée, pas de changement technique |
| 3 | **Planning Phase 2 validé** (Nov 2024, go-live 31/12) | Timeline alignée avec contraintes business | Engagement équipe sur deadline 31/12 |
| 4 | **Rituels projet** (Daily standup, demo hebdo vendredi) | Organisation communication et suivi | Transparence et réactivité garanties |
| 5 | **Scope gelé Phase 2** (features secondaires → Phase 4 post-launch) | Risque délais identifié | Priorité MVP, éviter scope creep |

---

## 🎯 Actions

| Action | Responsable | Deadline | Statut | Priorité |
|--------|-------------|----------|--------|----------|
| Ajuster maquettes Figma (CTA Hero + Témoignages) | Camille Petit | 18/10 | ✅ Fait | Haute |
| Fournir export XML WordPress (200+ pages) | Équipe tech ClientA | 18/10 | ✅ Fait | Haute |
| Transférer accès Contentful, Vercel, GA4 | Thomas Martin | 16/10 | ✅ Fait | Haute |
| Setup projet GitHub + CI/CD Vercel | Julien Rousseau | 16/10 | ✅ Fait | Haute |
| Créer Slack channel `#clienta-refonte` | Lucas Moreau | 15/10 | ✅ Fait | Moyenne |
| Planifier session formation Contentful (déc) | Sophie Bernard | 30/11 | ⏳ | Basse |

---

## ⚠️ Risques & Blocages identifiés

**Risques discutés** :
1. **Délais serrés** : Timeline ambitieuse 31/12 avec congés Noël
   - **Mitigation** : Geler scope, prioriser MVP, équipe disponible période fêtes si nécessaire

2. **Migration contenu complexe** : 200+ pages WordPress à migrer
   - **Mitigation** : Automatisation scripts export/import, allocation 2 semaines dédiées

3. **Dépendance équipe ClientA** : Besoin feedbacks rapides pour avancer
   - **Mitigation** : Rituels hebdos + channel Slack réactif

**Aucun blocage immédiat identifié**.

---

## 🔄 Prochaines étapes

1. **Démarrage Phase 2 développement** (18/10)
2. **Première demo intermédiaire** (08/11 - pages Home + About)
3. **Point hebdo vendredi suivant** (25/10)

---

## 💡 Idées & Insights

### Idées émergentes pendant réunion

- **Témoignages clients** : Sophie Bernard suggère vidéos témoignages (pas que texte)
  - → Capturé dans [[00-Inbox/idee-amelioration-ux-mobile-clientA|Amélioration UX avec témoignages vidéo]]

- **Analytics avancé** : Alexandre Chen intéressé par heatmaps Hotjar au-delà GA4
  - → À évaluer budget Phase 3, option Hotjar (coût +150€/mois)

### À explorer

- Feature "Comparateur concurrents" mentionnée par Thomas Martin
  - → Non prioritaire Phase 2, évaluer Phase 4 post-launch

---

## 🔗 Liens

### Projet parent
- [[02-Projects/ClientA-Refonte-SiteWeb/_index|ClientA Refonte Site Web]]

### Réunions liées
- [[07-Meetings/2024-10-18-Suivi-ClientA|Point d'avancement - 18/10/2024]] (suivante)

### Documentation référencée
- Maquettes Figma : https://figma.com/clienta-design-system
- Architecture technique : [[02-Projects/ClientA-Refonte-SiteWeb/architecture]]
- Spécifications : [[02-Projects/ClientA-Refonte-SiteWeb/specifications]]

---

## 📋 Suivi

- [x] Compte-rendu envoyé aux participants (15/10 soir)
- [x] Actions créées et assignées (Slack + Notion)
- [x] Documentation mise à jour (architecture, specs)
- [x] Prochaine réunion planifiée (18/10 - Point avancement)

---

**Ambiance générale** : Très positive ! Équipe ClientA enthousiaste, confiance établie. Marie Dubois (Sponsor) : "Ravis de travailler avec vous, on sent le professionnalisme". 🎉
