---
type: resource
title: "Next.js Performance Optimization Checklist"
category: "Frontend"
tags: [resource, nextjs, performance, webperf, checklist]
created: 2024-08-15
last_accessed: 2024-10-18
---

# ⚡ Next.js Performance Optimization Checklist

> Checklist complète d'optimisation performance Next.js 14 basée sur projets réels (ClientA) et best practices officielles.

---

## 🎯 Core Web Vitals Targets

| Metric | Good | Needs Improvement | Poor |
|--------|------|-------------------|------|
| **LCP** (Largest Contentful Paint) | ≤ 2.5s | 2.5s - 4.0s | > 4.0s |
| **FID/INP** (First Input Delay / Interaction to Next Paint) | ≤ 100ms / ≤ 200ms | 100-300ms / 200-500ms | > 300ms / > 500ms |
| **CLS** (Cumulative Layout Shift) | ≤ 0.1 | 0.1 - 0.25 | > 0.25 |

**Objectif projets** : Tous les metrics dans la zone "Good" (75th percentile)

---

## 📦 1. Code Splitting & Lazy Loading

### Dynamic Imports
```tsx
// ✅ Good - Lazy load heavy components
import dynamic from 'next/dynamic'

const HeavyChart = dynamic(() => import('@/components/HeavyChart'), {
  loading: () => <Skeleton />,
  ssr: false // Si pas besoin SSR
})

// ❌ Bad - Import statique de composant lourd
import HeavyChart from '@/components/HeavyChart'
```

### Route-based Code Splitting
```tsx
// ✅ Next.js fait automatiquement le splitting par route
// app/about/page.tsx sera un bundle séparé

// Optimisation : Précharger routes importantes
<Link href="/about" prefetch={true}>About</Link>
```

### Client Components Boundaries
```tsx
// ✅ Good - Server Component par défaut, Client Component ciblé
// app/page.tsx (Server Component)
import ClientInteractiveWidget from './ClientWidget'

export default function Page() {
  return (
    <div>
      <h1>Static Content (SSR)</h1>
      <ClientInteractiveWidget /> {/* Seul ce composant hydraté côté client */}
    </div>
  )
}

// ❌ Bad - Tout le composant parent en 'use client'
'use client'
export default function Page() { /* ... */ }
```

**Résultats ClientA** : -35KB bundle initial après lazy loading carousel

---

## 🖼️ 2. Image Optimization

### Next.js Image Component
```tsx
import Image from 'next/image'

// ✅ Good - Optimisation automatique
<Image
  src="/hero.jpg"
  alt="Hero"
  width={1200}
  height={600}
  priority // Pour LCP image
  placeholder="blur"
  blurDataURL="data:image/jpeg;base64,..."
/>

// ❌ Bad - <img> standard
<img src="/hero.jpg" alt="Hero" />
```

### Lazy Loading Images
```tsx
// ✅ Images below-the-fold avec loading="lazy"
<Image
  src="/gallery-1.jpg"
  alt="Gallery"
  width={800}
  height={600}
  loading="lazy" // Lazy load automatique
/>
```

### Format & Compression
- **Formats** : WebP (défaut Next.js), AVIF si supporté
- **Compression** : Quality 75-80 (balance qualité/taille)
- **Responsive** : Utiliser `sizes` prop pour responsive images

**Résultats ClientA** : LCP 3.2s → 1.8s après optimisation images carousel

---

## 🎨 3. Font Optimization

### Next.js Font Optimization
```tsx
// app/layout.tsx
import { Inter } from 'next/font/google'

const inter = Inter({
  subsets: ['latin'],
  display: 'swap', // Évite FOIT (Flash of Invisible Text)
  preload: true,
  variable: '--font-inter',
})

export default function RootLayout({ children }) {
  return (
    <html lang="en" className={inter.variable}>
      <body>{children}</body>
    </html>
  )
}
```

**Checklist** :
- [ ] Utiliser `next/font` (auto-hébergement + optimisation)
- [ ] `display: 'swap'` pour éviter FOIT
- [ ] Limiter nombre de font weights (2-3 max)
- [ ] Précharger fonts critiques

---

## 🚀 4. Rendering Strategies

### Server Components (par défaut Next.js 14)
```tsx
// ✅ Server Component (default) - Pas d'hydratation JS
async function ProductList() {
  const products = await fetchProducts() // Fetch côté serveur
  return <div>{products.map(p => <ProductCard key={p.id} {...p} />)}</div>
}
```

### Streaming SSR
```tsx
// app/dashboard/page.tsx
import { Suspense } from 'react'

export default function Dashboard() {
  return (
    <>
      <Header /> {/* Render immédiat */}
      <Suspense fallback={<Skeleton />}>
        <SlowDataComponent /> {/* Stream après */}
      </Suspense>
    </>
  )
}
```

### Static Generation (recommandé quand possible)
```tsx
// app/blog/[slug]/page.tsx
export async function generateStaticParams() {
  const posts = await getAllPosts()
  return posts.map(post => ({ slug: post.slug }))
}

// Pages générées au build → ultra rapides
```

**Choix stratégie** :
- **Static** : Pages contenu (blog, marketing) → Lighthouse 95+
- **SSR avec Streaming** : Pages dynamiques (dashboard) → Bon compromis
- **Client-side** : Interactions temps réel → Dernier recours

---

## 📊 5. Bundle Analysis

### Analyzer Webpack
```bash
# Installation
npm install @next/bundle-analyzer

# next.config.js
const withBundleAnalyzer = require('@next/bundle-analyzer')({
  enabled: process.env.ANALYZE === 'true',
})

module.exports = withBundleAnalyzer({
  // ... config
})

# Exécution
ANALYZE=true npm run build
```

**Actions ClientA** :
- Identifié `moment.js` (200KB) → remplacé par `date-fns` (20KB)
- Tree-shaking `lodash` → imports spécifiques (`lodash/get`)

---

## 🔄 6. Caching Strategies

### Static Assets
```tsx
// next.config.js
module.exports = {
  images: {
    minimumCacheTTL: 31536000, // 1 an
  },
}
```

### API Routes Caching
```tsx
// app/api/data/route.ts
export const revalidate = 3600 // Revalidate toutes les heures

export async function GET() {
  const data = await fetchData()
  return Response.json(data)
}
```

### Client-side Caching (SWR)
```tsx
import useSWR from 'swr'

function Profile() {
  const { data, error } = useSWR('/api/user', fetcher, {
    revalidateOnFocus: false,
    dedupingInterval: 10000, // 10s
  })
  // ...
}
```

---

## 🧪 7. Performance Testing

### Lighthouse CI
```bash
# Installation
npm install -D @lhci/cli

# Configuration .lighthouserc.json
{
  "ci": {
    "collect": {
      "url": ["http://localhost:3000/"],
      "numberOfRuns": 3
    },
    "assert": {
      "assertions": {
        "categories:performance": ["error", { "minScore": 0.9 }],
        "first-contentful-paint": ["error", { "maxNumericValue": 2000 }],
        "largest-contentful-paint": ["error", { "maxNumericValue": 2500 }]
      }
    }
  }
}

# Exécution
npm run build && lhci autorun
```

### Real User Monitoring
```tsx
// app/layout.tsx
export function reportWebVitals(metric) {
  // Envoyer à analytics (Google Analytics, Vercel Analytics...)
  if (metric.label === 'web-vital') {
    console.log(metric) // LCP, FID, CLS, FCP, TTFB
  }
}
```

**Métriques ClientA (Oct 2024)** :
- Lighthouse Performance : 87 → 92 (+5)
- LCP : 2.3s → 1.8s (-22%)
- FID : 45ms → 35ms
- CLS : 0.08 (stable)

---

## 🔍 8. Advanced Optimizations

### Prefetching
```tsx
// ✅ Prefetch routes importantes
<Link href="/products" prefetch={true}>Products</Link>

// ⚠️ Désactiver prefetch si trop de liens
<Link href="/article" prefetch={false}>Article</Link>
```

### React Suspense Boundaries
```tsx
<Suspense fallback={<Spinner />}>
  <Suspense fallback={<Skeleton />}>
    <CriticalData />
  </Suspense>
  <Suspense fallback={<Skeleton />}>
    <NonCriticalData />
  </Suspense>
</Suspense>
```

### Edge Functions (à explorer)
- [[00-Inbox/idee-optimisation-performance-clientA]] - Vercel Edge Functions
- Potentiel : Latence <50ms (vs 200-300ms origin)

---

## ✅ Checklist Complète

### Images
- [ ] Utiliser `next/image` partout
- [ ] `priority` pour LCP image
- [ ] `loading="lazy"` pour images below-the-fold
- [ ] Formats WebP/AVIF
- [ ] Responsive images avec `sizes`

### Code
- [ ] Server Components par défaut
- [ ] Dynamic imports pour composants lourds
- [ ] Bundle analysis (`@next/bundle-analyzer`)
- [ ] Tree-shaking vérifié (no unused exports)

### Fonts
- [ ] `next/font` pour auto-hébergement
- [ ] `display: 'swap'`
- [ ] Max 2-3 font weights

### Rendering
- [ ] Static generation quand possible
- [ ] Streaming SSR pour pages dynamiques
- [ ] Suspense boundaries appropriées

### Caching
- [ ] Revalidation ISR configurée
- [ ] API routes avec `revalidate`
- [ ] CDN headers optimisés (Vercel auto)

### Monitoring
- [ ] Lighthouse CI dans pipeline
- [ ] Real User Monitoring (RUM)
- [ ] Core Web Vitals tracking

---

## 🔗 Ressources & Projets

### Projets utilisant cette checklist
- [[02-Projects/ClientA-Refonte-SiteWeb/_index]] - Lighthouse 92/100 ✨

### Notes Zettelkasten associées
- [[06-Zettelkasten/Performance-Web-Optimisation]] - Core Web Vitals

### Documentation officielle
- [Next.js Performance](https://nextjs.org/docs/app/building-your-application/optimizing)
- [Web.dev Core Web Vitals](https://web.dev/vitals/)
- [Vercel Analytics](https://vercel.com/analytics)

### Area technique liée
- [[03-Areas/Technical-Skills/_index]] - Performance Web

---

## 📅 Dernière mise à jour : 18 Oct 2024

**Résultats projet ClientA** :
- Lighthouse Performance : 87 → 92 (+5 points)
- LCP : 2.3s → 1.8s (-22%)
- Bundle size : -35KB (carousel lazy loading)
- Feedback client : ⭐⭐⭐⭐⭐ "Performance exceptionnelle"
