---
type: zettel
created: 2024-10-10
tags: [zettelkasten, design, architecture, frontend]
domain: "Technique"
status: "🌳 Evergreen"
---

# Pattern Design Atomic

## 🔑 Concept principal

> Le Design Atomic est une méthodologie de création d'interfaces utilisateur qui décompose les composants en 5 niveaux hiérarchiques (Atomes → Molécules → Organismes → Templates → Pages), inspirée de la chimie.

---

## 📝 Développement

### Contexte

Créé par Brad Frost en 2013 pour répondre au besoin de **cohérence et réutilisabilité** dans les design systems. Face à la multiplication des devices et la complexité croissante des interfaces web, il fallait une méthodologie systématique pour organiser les composants UI.

### Les 5 niveaux de l'Atomic Design

```
Pages (instances concrètes)
  ↑
Templates (agencements de composants)
  ↑
Organismes (sections complexes)
  ↑
Molécules (groupes de composants simples)
  ↑
Atomes (composants de base)
```

#### 1. Atomes (Atoms)
**Définition** : Composants UI les plus basiques, indivisibles.

**Exemples** :
- `<Button>` - Bouton simple
- `<Input>` - Champ de texte
- `<Label>` - Étiquette
- `<Icon>` - Icône
- Tokens de design (couleurs, typographie, espacements)

**Caractéristiques** :
- Autonomes et réutilisables partout
- Pas de dépendances vers d'autres composants
- Configuration via props simples

```tsx
// Exemple : Atom Button
<Button variant="primary" size="md">
  Click me
</Button>
```

#### 2. Molécules (Molecules)
**Définition** : Groupes d'atomes qui forment une unité fonctionnelle simple.

**Exemples** :
- `<FormField>` = Label + Input + ErrorMessage
- `<SearchBar>` = Input + Button + Icon
- `<CardHeader>` = Icon + Title + Subtitle

**Caractéristiques** :
- Composent une fonction unique et claire
- Réutilisables dans différents contextes
- Composition de 2 à 5 atomes typiquement

```tsx
// Exemple : Molecule FormField
<FormField>
  <Label>Email</Label>
  <Input type="email" />
  <ErrorMessage>Invalid email</ErrorMessage>
</FormField>
```

#### 3. Organismes (Organisms)
**Définition** : Sections complexes composées de molécules et/ou atomes formant une section distincte de l'interface.

**Exemples** :
- `<Header>` = Logo + Navigation + UserMenu
- `<Hero>` = Headline + Description + CTA + Image
- `<ProductCard>` = Image + Title + Price + Rating + AddToCart

**Caractéristiques** :
- Forment des sections autonomes de l'interface
- Peuvent contenir logique métier
- Souvent spécifiques à un contexte (moins réutilisables)

```tsx
// Exemple : Organism Header
<Header>
  <Logo />
  <Navigation items={navItems} />
  <UserMenu user={currentUser} />
</Header>
```

#### 4. Templates
**Définition** : Structures de pages qui agencent les organismes sans contenu réel (wireframes de haut niveau).

**Exemples** :
- `<MarketingPageTemplate>` = Header + Hero + Features + CTA + Footer
- `<BlogArticleTemplate>` = Header + ArticleContent + Sidebar + Footer

**Caractéristiques** :
- Définissent la structure générale des pages
- Pas de contenu réel (placeholders)
- Réutilisables pour créer différentes pages

```tsx
// Exemple : Template
<MarketingPageTemplate>
  <Header />
  <Hero />
  <FeaturesSection />
  <CTASection />
  <Footer />
</MarketingPageTemplate>
```

#### 5. Pages
**Définition** : Instances spécifiques de templates avec contenu réel et données.

**Exemples** :
- `<HomePage>` utilise `<MarketingPageTemplate>` avec données homepage
- `<AboutPage>` utilise `<MarketingPageTemplate>` avec données about

**Caractéristiques** :
- Contenu réel et données spécifiques
- Tests utilisateurs effectués sur ce niveau
- Représentation fidèle de l'expérience utilisateur

```tsx
// Exemple : Page
<HomePage>
  <MarketingPageTemplate>
    <Hero
      title="Bienvenue sur notre site"
      description="La meilleure solution SaaS..."
      cta="Démarrer gratuitement"
    />
    {/* Contenu réel injecté */}
  </MarketingPageTemplate>
</HomePage>
```

### Explication détaillée

**Avantages** :
1. **Cohérence visuelle** : Design system unifié sur toute l'application
2. **Réutilisabilité** : Composants atomiques réutilisables partout
3. **Maintenabilité** : Modifications centralisées (modifier un atome = impact global)
4. **Collaboration** : Langage commun designers ↔ développeurs
5. **Testabilité** : Tests unitaires sur atomes, tests d'intégration sur organismes
6. **Documentation** : Storybook facilité (visualiser chaque niveau)

**Limites** :
1. **Sur-architecture** : Risque de trop décomposer (analyse paralysis)
2. **Courbe d'apprentissage** : Équipe doit comprendre la méthodologie
3. **Complexité initiale** : Setup design system prend du temps
4. **Frontière floue** : Distinction molécule vs organisme parfois subjective

### Exemples d'application

**Cas concret : Formulaire de contact**

```
Page: ContactPage
  ↓
Template: ContactPageTemplate
  ↓
Organism: ContactForm (formulaire complet)
  ↓
Molecules:
  - FormField (label + input + error)
  - FormField (label + textarea + error)
  - FormField (label + select + error)
  ↓
Atoms:
  - Label
  - Input
  - Textarea
  - Select
  - Button
  - ErrorMessage
```

---

## 💡 Insights & Connexions

### Pourquoi c'est important

- **Scalabilité** : Design systems avec 100+ composants restent maintenables
- **Productivité** : Développement plus rapide (réutilisation > recréation)
- **Qualité** : Cohérence visuelle garantie sur toute l'application
- **Adoption** : Méthodologie standard reconnue industrie (Airbnb, IBM, Salesforce...)

### Quand l'utiliser

✅ **Utiliser quand** :
- Projet web/mobile avec design system
- Équipe multi-personnes (collaboration designers + devs)
- Application complexe avec nombreuses pages
- Besoin de cohérence visuelle forte

❌ **Éviter quand** :
- Prototype rapide ou MVP (overkill)
- Site statique simple (< 5 pages)
- Équipe solo sans besoin réutilisabilité

### Limitations & contraintes

- **Pas dogmatique** : Adapter les 5 niveaux au contexte (parfois 3 niveaux suffisent)
- **Pas linéaire** : On ne construit pas toujours bottom-up (atomes → pages)
- **Frontières flexibles** : Ne pas perdre du temps à classifier "molécule ou organisme ?"

---

## 🔗 Liens

### Connexions directes
- [[06-Zettelkasten/Architecture-Microservices]] - (complète) Atomic Design pour UI ≈ Microservices pour backend
- [[02-Projects/ClientA-Refonte-SiteWeb/architecture]] - (illustre) Design system ClientA utilise Atomic Design

### Projets où c'est applicable
- [[02-Projects/ClientA-Refonte-SiteWeb/_index|ClientA Refonte Site Web]] - Design system basé sur ce pattern

### Sources & Références

**Livre** : "Atomic Design" by Brad Frost (2016) - https://atomicdesign.bradfrost.com
**Articles** :
- Brad Frost blog : https://bradfrost.com/blog/post/atomic-web-design/
- Storybook Atomic Design : https://storybook.js.org/tutorials/design-systems-for-developers/

---

## 🏷️ Métadonnées

| Champ | Valeur |
|-------|--------|
| **Domaine** | Technique (Frontend, Design Systems) |
| **Statut** | 🌳 Evergreen (mature, utilisée régulièrement) |
| **Confiance** | ⭐⭐⭐⭐⭐ (5/5 - pattern éprouvé industrie) |
| **Dernière révision** | 2024-10-20 |

---

## 📚 Évolution de la note

### 2024-10-10
- Création initiale suite à phase design ClientA

### 2024-10-20
- Ajout section "Exemples d'application" avec formulaire de contact
- Lien ajouté vers projet ClientA (utilisation concrète)
- Enrichissement insights (scalabilité, productivité)
