# Spécifications fonctionnelles - Refonte Site Web ClientA

**Projet** : [[02-Projects/ClientA-Refonte-SiteWeb/_index|ClientA Refonte Site Web]]
**Version** : 1.2
**Dernière MAJ** : 2024-10-18

---

## 🎯 Vision & Objectifs

### Contexte

ClientA est un éditeur SaaS B2B dans le secteur de la gestion de projet collaborative. Leur site actuel (WordPress 2019) souffre de :
- Performance médiocre (Lighthouse 45/100)
- UX datée et peu engageante
- SEO en baisse (-15% trafic organique YoY)
- Difficulté de maintenance (code legacy)

### Objectifs business

1. **Acquisition** : +30% leads qualifiés via formulaires
2. **Conversion** : +25% taux conversion landing pages
3. **Image de marque** : Site moderne reflétant innovation produit
4. **SEO** : Maintien positions actuelles + amélioration technique
5. **Performance** : Core Web Vitals au vert (impact SEO Google)

---

## 📱 Pages & Fonctionnalités

### Page d'accueil (/)

**Objectif** : Capter attention, expliquer value proposition, pousser à l'action

**Sections** :
1. **Hero** : Headline impactant + CTA primaire "Démarrer essai gratuit"
2. **Social Proof** : Logos clients (30+ entreprises), témoignages
3. **Features Clés** : 6 fonctionnalités principales avec icônes
4. **Demo Interactive** : Vidéo produit + screenshots interface
5. **Pricing Teaser** : 3 plans tarifaires (lien vers /pricing)
6. **CTA Final** : Formulaire contact ou démo

**Fonctionnalités techniques** :
- Animations scroll (Framer Motion)
- Lazy loading images
- Video player optimisé (React Player)

### Page About (/about)

**Objectif** : Rassurer, humaniser la marque, storytelling

**Sections** :
1. Mission & Vision de ClientA
2. Timeline interactive (historique 2018-2024)
3. Équipe (photos + bios 12 personnes clés)
4. Valeurs d'entreprise (4 piliers)
5. Recrutement (lien carrières)

### Page Pricing (/pricing)

**Objectif** : Convertir leads avec transparence tarifaire

**Sections** :
1. **Tableau comparatif** : 3 plans (Starter, Business, Enterprise)
2. **Calculateur dynamique** : Slider nombre utilisateurs → prix temps réel
3. **FAQ Pricing** : 10 questions fréquentes
4. **CTA** : Démarrer essai 14j gratuit

**Fonctionnalités** :
- Toggle mensuel/annuel (-20% annuel)
- Logique calcul : `base_price + (users - included_users) * price_per_user`
- Feature comparison (checkmarks par plan)

### Page Blog (/blog)

**Objectif** : SEO, thought leadership, nurturing leads

**Features** :
- Listing articles (pagination 12/page)
- Filtres par catégorie (Product, Industry, Tips)
- Recherche full-text
- Article individuel avec :
  - Table of contents automatique
  - Related articles (3)
  - CTA inline "Try for free"
  - Social sharing buttons

**CMS** : Contentful pour gestion contenu

### Page Contact (/contact)

**Objectif** : Générer leads qualifiés

**Formulaire** :
- Nom, Email, Société, Téléphone
- Type demande (Demo, Support, Partenariat)
- Message libre
- Consent RGPD

**Intégration** :
- Envoi email via Resend API
- Notification Slack équipe sales
- Auto-responder confirmation client

---

## 🎨 Design System

### Identité visuelle

- **Couleurs primaires** :
  - Primary : `#0066FF` (bleu ClientA)
  - Secondary : `#00C896` (vert accent)
  - Neutral : Gray 50-900 palette
- **Typographie** :
  - Headings : Inter Bold
  - Body : Inter Regular
- **Composants** : Basés sur Shadcn/ui (Radix primitives)

### Responsive breakpoints

- Mobile : < 768px
- Tablet : 768px - 1024px
- Desktop : > 1024px

---

## ⚡ Performances & SEO

### Core Web Vitals cibles

- **LCP** (Largest Contentful Paint) : < 2.5s
- **FID** (First Input Delay) : < 100ms
- **CLS** (Cumulative Layout Shift) : < 0.1

### Optimisations

- Next.js Image (automatic optimization)
- Static generation pages (SSG) sauf blog (ISR)
- Edge caching Vercel CDN
- Font optimization (next/font)
- Critical CSS inline

### SEO On-Page

- Metadata dynamiques (title, description par page)
- Open Graph tags (partage social)
- Sitemap.xml automatique
- Robots.txt optimisé
- Structured data (schema.org)

---

## 🔐 Conformité & Accessibilité

### RGPD

- Bandeau cookies (Cookiebot)
- Politique confidentialité + CGU
- Opt-in formulaires
- Droit accès/suppression données

### Accessibilité WCAG 2.1 AA

- Contraste texte/fond ≥ 4.5:1
- Navigation clavier complète
- Alt text images
- Labels formulaires
- Skip to content link
- Focus indicators visibles

---

## 📊 Analytics & Tracking

### Google Analytics 4

- Pageviews
- Events personnalisés :
  - `click_cta_hero`
  - `form_submit_contact`
  - `video_play_demo`
  - `pricing_calculator_use`

### Hotjar

- Heatmaps pages clés (Home, Pricing)
- Session recordings (échantillon 10%)

---

## 🚀 Plan de migration

### Contenu

- **200+ pages** à migrer depuis WordPress
- Export XML → transformation → import Contentful
- Nettoyage contenu obsolète (identification avec client)

### Redirections SEO

- Mapping ancien → nouveau URLs
- Redirections 301 (Next.js rewrites)
- Monitoring Search Console 30j post-launch

### Planning

1. **Semaine 1** : Export contenu WordPress
2. **Semaine 2** : Modélisation Contentful + import automatisé
3. **Semaine 3** : Revue manuelle + ajustements
4. **Semaine 4** : Tests redirections + go-live

---

## ✅ Critères d'acceptation

### Phase 2 (Développement)

- [ ] Toutes les pages fonctionnelles (responsive)
- [ ] Score Lighthouse > 90 (Performance, Accessibility, Best Practices, SEO)
- [ ] Zéro erreurs console navigateur
- [ ] Formulaires opérationnels avec validation
- [ ] Intégration CMS complète

### Phase 3 (Mise en production)

- [ ] Tests E2E passent (Playwright)
- [ ] Migration contenu vérifiée
- [ ] Redirections 301 testées
- [ ] Monitoring configuré (Sentry, Analytics)
- [ ] Formation équipe ClientA effectuée

---

## 📚 Références

- Maquettes Figma : https://figma.com/clienta-specs
- Ancien site : https://old.clienta.com
- Benchmark concurrents : [[02-Projects/ClientA-Refonte-SiteWeb/benchmark-competitors]]
