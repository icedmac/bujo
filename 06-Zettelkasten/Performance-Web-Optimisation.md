---
type: zettel
created: 2024-10-12
tags: [zettelkasten, performance, web, frontend]
domain: "Technique"
status: "🌳 Evergreen"
---

# Performance Web & Core Web Vitals

## 🔑 Concept principal

> Les Core Web Vitals sont 3 métriques Google mesurant l'expérience utilisateur réelle : LCP (chargement), FID/INP (interactivité), CLS (stabilité visuelle). Critiques pour SEO et UX.

---

## 📝 Développement

### Les 3 Core Web Vitals

**LCP (Largest Contentful Paint)** : < 2.5s  
→ Temps chargement élément principal visible  
→ Optimisations : images optimisées, CDN, SSR, preload assets critiques

**FID (First Input Delay) / INP** : < 100ms  
→ Réactivité aux interactions utilisateur  
→ Optimisations : réduire JS main thread, code splitting, defer scripts

**CLS (Cumulative Layout Shift)** : < 0.1  
→ Stabilité visuelle (pas de décalages intempestifs)  
→ Optimisations : dimensions images explicites, réserver espace ads, éviter insertion dynamique

### Techniques d'optimisation

**Images** :
- Formats modernes (WebP, AVIF)
- Lazy loading (images below fold)
- Responsive images (srcset)
- CDN + compression

**JavaScript** :
- Code splitting (dynamic imports)
- Tree shaking (éliminer code mort)
- Minification + compression gzip/brotli
- Defer non-critical scripts

**CSS** :
- Critical CSS inline
- Purge unused CSS
- Minification

**Caching** :
- Service Workers (offline-first)
- HTTP cache headers
- CDN edge caching

---

## 💡 Insights & Connexions

### Pourquoi c'est important

- **SEO** : Core Web Vitals = facteur ranking Google depuis 2021
- **Conversion** : +1s load time = -7% conversions (étude Amazon)
- **UX** : Performance = perception qualité produit

### Quand l'utiliser

✅ **Toujours** pour sites publics (SEO critique)  
✅ Applications SaaS (rétention users)  
✅ E-commerce (impact conversion direct)

---

## 🔗 Liens

### Connexions directes
- [[02-Projects/ClientA-Refonte-SiteWeb/_index]] - (applique) Lighthouse > 90 requis, Core Web Vitals optimisés

### Projets
- [[02-Projects/ClientA-Refonte-SiteWeb/_index]] - Performance critique (critère succès)

### Sources
- Web.dev Core Web Vitals: https://web.dev/vitals
- Google Search Central: https://developers.google.com/search/docs/appearance/core-web-vitals

---

## 🏷️ Métadonnées

| Champ | Valeur |
|-------|--------|
| **Domaine** | Technique (Performance, Frontend) |
| **Statut** | 🌳 Evergreen |
| **Confiance** | ⭐⭐⭐⭐⭐ (5/5) |
| **Dernière révision** | 2024-10-18 |

---

## 📚 Évolution

### 2024-10-12
- Création initiale

### 2024-10-18
- Ajout lien projet ClientA
- Enrichissement techniques optimisation
