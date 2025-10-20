---
type: project
client: "ClientA (Secteur Tech)"
status: "🔵 En cours"
priority: "⚠️ Haute"
start_date: 2024-10-01
deadline: 2024-12-31
budget: "45 jours / 60 000€"
tags: [project, para, web, frontend]
---

# 🎯 Refonte complète du site web ClientA

## 📋 Informations projet

| Champ | Valeur |
|-------|--------|
| **Client** | [[ClientA]] (Secteur Tech - SaaS B2B) |
| **Statut** | 🔵 En cours |
| **Priorité** | ⚠️ Haute |
| **Date début** | 2024-10-01 |
| **Deadline** | 2024-12-31 |
| **Budget** | 45 jours / 60 000€ |
| **Ressources allouées** | 3 personnes (1 designer, 2 développeurs frontend) |

---

## 🎯 Objectifs & Livrables

### Objectif principal

Moderniser complètement le site web corporate de ClientA pour améliorer l'image de marque, optimiser l'acquisition de leads B2B et améliorer les performances techniques (SEO, vitesse, accessibilité).

### Livrables attendus
- [x] Audit UX/UI et technique de l'existant
- [x] Maquettes Figma (desktop + mobile)
- [ ] Développement frontend (React + Next.js)
- [ ] Intégration CMS Headless (Contentful)
- [ ] Migration contenu + redirections SEO
- [ ] Tests A/B sur landing pages
- [ ] Documentation technique
- [ ] Formation équipe marketing client

### Critères de succès
- Performance Lighthouse > 90 sur toutes les pages
- Temps de chargement < 2s (LCP)
- Accessibilité WCAG 2.1 AA
- +30% taux de conversion sur landing pages (vs baseline actuelle)
- Zéro régression SEO (maintien positions Google)

---

## 👥 Stakeholders

| Rôle | Nom | Contact | Responsabilité |
|------|-----|---------|----------------|
| Sponsor | Marie Dubois | marie.dubois@clienta.com | Validation stratégique et budget |
| Product Owner | Thomas Martin | thomas.martin@clienta.com | Priorisation features, recette |
| CTO ClientA | Alexandre Chen | alex.chen@clienta.com | Validation architecture technique |
| Chef Marketing | Sophie Bernard | sophie.bernard@clienta.com | Contenu, SEO, tracking analytics |

---

## 📊 Phases & Jalons

### Phase 1 : Audit & Conception (Oct 2024) ✅
- **Dates** : 2024-10-01 → 2024-10-31
- **Objectif** : Comprendre l'existant, définir la nouvelle expérience
- **Livrables** :
  - [x] Audit technique (performance, SEO, accessibilité)
  - [x] Audit UX (heatmaps, analytics, interviews utilisateurs)
  - [x] Benchmark concurrents (5 acteurs majeurs)
  - [x] Wireframes basse fidélité
  - [x] Maquettes Figma haute fidélité validées
  - [x] Design system (composants, tokens, guidelines)

**Statut** : ✅ Terminée (31/10/2024)

### Phase 2 : Développement (Nov 2024) 🔵
- **Dates** : 2024-11-01 → 2024-11-30
- **Objectif** : Développer le nouveau site en production-ready
- **Livrables** :
  - [x] Setup architecture Next.js 14 (App Router)
  - [x] Intégration Contentful CMS
  - [ ] Développement composants UI (design system)
  - [ ] Pages principales (Home, About, Pricing, Blog, Contact)
  - [ ] Formulaires avec validation et envoi (Resend API)
  - [ ] SEO technique (metadata, sitemap, robots.txt)
  - [ ] Analytics & tracking (GA4, Hotjar)

**Statut** : 🔵 En cours (65% complété)

### Phase 3 : Tests, Migration & Déploiement (Déc 2024) ⏳
- **Dates** : 2024-12-01 → 2024-12-31
- **Objectif** : Garantir qualité, migrer contenu, déployer en prod
- **Livrables** :
  - [ ] Tests end-to-end (Playwright)
  - [ ] Tests accessibilité (axe DevTools)
  - [ ] Tests performance (Lighthouse CI)
  - [ ] Migration contenu (200+ pages)
  - [ ] Plan de redirections SEO (301)
  - [ ] Déploiement sur Vercel (production)
  - [ ] Monitoring post-launch (Sentry, Vercel Analytics)
  - [ ] Formation équipe ClientA

**Statut** : ⏳ Pas encore démarrée

---

## ✅ Tâches & Actions

### À faire aujourd'hui
- [ ] Finaliser page Pricing avec calculateur dynamique
- [ ] Review PR #23 (composant Hero)
- [ ] Préparer démo client pour vendredi

### En cours
- [ ] Développement blog (listing + articles individuels)
- [ ] Intégration formulaire contact avec Resend
- [ ] Optimisation images (Next Image + Cloudinary)

### Bloqué
- [ ] Tests A/B landing pages (Raison : Attente accès compte Vercel Edge Config côté client)

### Terminé
- [x] Setup projet Next.js 14 + TypeScript + Tailwind
- [x] Intégration Contentful (types, queries GraphQL)
- [x] Composants design system (Button, Card, Input, Modal)
- [x] Page Home complète (desktop + mobile)
- [x] Page About avec timeline interactive
- [x] Navigation responsive avec menu mobile
- [x] Footer avec sitemap et liens sociaux
- [x] SEO metadata dynamiques par page

---

## 📝 Notes & Documentation

### Documentation technique
- [[02-Projects/ClientA-Refonte-SiteWeb/architecture|Architecture technique détaillée]]
- [[02-Projects/ClientA-Refonte-SiteWeb/specifications|Spécifications fonctionnelles]]
- Design system Figma : https://figma.com/clienta-design-system
- Repository GitHub : https://github.com/agency/clienta-website

### Spécifications

**Stack technique** :
- **Framework** : Next.js 14 (App Router, React Server Components)
- **Styling** : Tailwind CSS + Shadcn/ui
- **CMS** : Contentful (Headless)
- **Hosting** : Vercel (Edge Network)
- **Analytics** : Google Analytics 4 + Vercel Analytics
- **Monitoring** : Sentry (errors) + Vercel Speed Insights

**Contraintes** :
- SEO critique : site actuel bien positionné, zéro régression acceptable
- Accessibilité WCAG 2.1 AA obligatoire (secteur public dans clientèle)
- Performance Core Web Vitals au vert (impact SEO Google)
- Multilingue pas nécessaire (marché français uniquement)

---

## 🔄 Suivi d'avancement

### Avancement global
**65%** complété

**Breakdown** :
- Phase 1 (Conception) : 100% ✅
- Phase 2 (Développement) : 65% 🔵
- Phase 3 (Tests & Déploiement) : 0% ⏳

### Dernière mise à jour
2024-10-20

### Prochaines étapes
1. Finaliser développement pages restantes (Pricing, Blog, Contact) - **Deadline : 25/11**
2. Commencer migration contenu Contentful (200+ pages) - **Début : 20/11**
3. Setup tests automatisés (Playwright + Lighthouse CI) - **Deadline : 01/12**

---

## ⚠️ Risques & Blocages

| Risque | Probabilité | Impact | Mitigation |
|--------|-------------|--------|------------|
| Délais serrés Phase 2 (scope creep) | H | H | Geler périmètre, prioriser MVP, reporter features secondaires en Phase 4 |
| Migration contenu complexe (200+ pages) | M | H | Automatisation scripts, allocation 1 semaine full-time |
| Dépendance accès Vercel client | H | M | Escalade au sponsor, fallback sur compte agence temporaire |
| Régression SEO post-migration | M | H | Plan redirections 301 exhaustif, monitoring Search Console quotidien post-launch |
| Performance sur contenu riche | M | M | Lazy loading, optimisation images Cloudinary, CDN Vercel |

### Blocages actuels
- ⚠️ **Accès Vercel Edge Config** (depuis 15/10) : Attente validation DSI ClientA pour accès compte. Impact : impossibilité de tester A/B testing. **Action** : Escalade à Marie Dubois (sponsor) - Deadline : 22/10.

---

## 💡 Idées & Améliorations

### Idées en attente

- [[00-Inbox/idee-amelioration-ux-mobile-clientA|Amélioration parcours mobile avec bottom navigation]] (suggéré lors user tests 10/10)
- [[00-Inbox/idee-optimisation-performance-clientA|Optimisation performance avec Edge Functions]] (suggestion CTO ClientA 18/10)

### Optimisations possibles

- **Post-launch** : Implémenter progressive web app (PWA) pour expérience app-like mobile
- **Phase 4 potentielle** : Espace client privé avec authentification (pas dans scope actuel)
- **SEO avancé** : Implémenter schema.org markup pour rich snippets Google

---

## 🔗 Liens & Ressources

### Réunions
- [[07-Meetings/2024-10-15-Kickoff-ClientA|Réunion kickoff - 15/10/2024]]
- [[07-Meetings/2024-10-18-Suivi-ClientA|Point d'avancement - 18/10/2024]]

### Notes Zettelkasten liées
- [[06-Zettelkasten/Pattern-Design-Atomic|Pattern Design Atomic]] - utilisé pour architecture composants
- [[06-Zettelkasten/Architecture-Microservices|Architecture Microservices]] - référence pour découpage CMS headless
- [[06-Zettelkasten/Performance-Web-Optimisation|Performance Web & Core Web Vitals]] - guide optimisation

### Références externes
- Figma Design System : https://figma.com/clienta-ds
- Contentful Space : https://app.contentful.com/spaces/abc123
- GitHub Repository : https://github.com/agency/clienta-website
- Vercel Dashboard : https://vercel.com/agency/clienta
- Analytics GA4 : https://analytics.google.com/clienta

---

## 📅 Historique

### 2024-10-20
- Développement page Pricing (calculateur interactif avec logique pricing tiers)
- Review et merge PR #22 (composant Testimonials avec carrousel)
- Point avec Thomas Martin : validation wireframes blog

### 2024-10-18
- Réunion suivi avec ClientA : présentation avancement Phase 2
- Décision : reporter feature "comparateur concurrents" en Phase 4
- Mise à jour budget : consommé 28j / 45j (62%)

### 2024-10-15
- Kickoff officiel projet avec équipe ClientA
- Validation définitive maquettes Figma
- Accès fournis : Contentful, GA4, Vercel

### 2024-10-01
- Démarrage projet
- Setup repository GitHub
- Audit technique de l'existant (ancien site WordPress)

---

## 📋 Clôture (à compléter en fin de projet)

### Date de clôture
_À compléter_

### Résultats
_À compléter après déploiement et 1 mois de monitoring_

### Retour d'expérience
_À compléter après rétrospective équipe_

### Archivage
- [ ] Documentation archivée dans Notion
- [ ] Livrables transmis (code source, accès, documentation)
- [ ] Projet déplacé vers [[05-Archives/2024-ClientA-Refonte]]
- [ ] Facturation finalisée
- [ ] Retour client collecté (NPS, testimonial)
