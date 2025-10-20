# Architecture Technique - Refonte Site Web ClientA

**Projet** : [[02-Projects/ClientA-Refonte-SiteWeb/_index|ClientA Refonte Site Web]]
**Version** : 1.1
**Dernière MAJ** : 2024-10-20

---

## 🏗️ Vue d'ensemble

### Architecture générale

```
┌─────────────────────────────────────────────────────┐
│                   User Browser                      │
└─────────────────┬───────────────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────────────┐
│              Vercel Edge Network (CDN)              │
│  ┌──────────────────────────────────────────────┐   │
│  │    Next.js 14 App Router (React Server      │   │
│  │           Components + Client)               │   │
│  └──────────────────┬───────────────────────────┘   │
└────────────────────┼─────────────────────────────────┘
                     │
        ┌────────────┼────────────┐
        │            │            │
        ▼            ▼            ▼
┌──────────────┐ ┌──────────┐ ┌────────────┐
│  Contentful  │ │  Resend  │ │   GA4 +    │
│     CMS      │ │   API    │ │  Vercel    │
│  (Headless)  │ │ (Email)  │ │ Analytics  │
└──────────────┘ └──────────┘ └────────────┘
```

### Stack technique

| Layer | Technologie | Justification |
|-------|-------------|---------------|
| **Framework** | Next.js 14 (App Router) | SSR/SSG, React Server Components, optimisations built-in |
| **Langage** | TypeScript | Type safety, meilleure DX, moins de bugs |
| **UI** | React 18 + Shadcn/ui | Composants accessibles (Radix), customisables |
| **Styling** | Tailwind CSS | Utility-first, DX rapide, bundle optimisé |
| **CMS** | Contentful | Headless, API GraphQL, preview mode |
| **Hosting** | Vercel | Edge network global, CI/CD natif Next.js |
| **Email** | Resend | API moderne, délivrabilité élevée, logs |
| **Monitoring** | Sentry + Vercel Analytics | Error tracking + Real User Monitoring |

---

## 📁 Structure du projet

```
clienta-website/
├── app/                          # Next.js App Router
│   ├── (marketing)/              # Route group (layout commun)
│   │   ├── page.tsx              # Homepage
│   │   ├── about/
│   │   ├── pricing/
│   │   ├── contact/
│   │   └── blog/
│   │       ├── page.tsx          # Liste articles
│   │       └── [slug]/           # Article individuel
│   ├── layout.tsx                # Root layout
│   ├── globals.css               # Tailwind imports
│   └── api/                      # API Routes
│       ├── contact/route.ts      # Formulaire contact
│       └── revalidate/route.ts   # Webhook Contentful
├── components/
│   ├── ui/                       # Shadcn/ui composants
│   │   ├── button.tsx
│   │   ├── card.tsx
│   │   └── ...
│   ├── layout/                   # Layout components
│   │   ├── header.tsx
│   │   ├── footer.tsx
│   │   └── navigation.tsx
│   └── sections/                 # Sections pages
│       ├── hero.tsx
│       ├── features.tsx
│       └── pricing-calculator.tsx
├── lib/
│   ├── contentful.ts             # Client Contentful + queries
│   ├── email.ts                  # Resend client
│   └── utils.ts                  # Helpers
├── types/
│   └── contentful.ts             # Types générés Contentful
├── public/
│   ├── images/
│   └── fonts/
├── .env.local                    # Variables environnement
├── next.config.js                # Config Next.js
├── tailwind.config.ts            # Config Tailwind
└── package.json
```

---

## 🔄 Flux de données

### Pages statiques (SSG)

Pages générées au build time, servies depuis CDN :

```typescript
// app/(marketing)/about/page.tsx
export default async function AboutPage() {
  // Données fetchées au build
  const teamMembers = await getTeamMembers();

  return <AboutPageContent team={teamMembers} />;
}

export const revalidate = 3600; // ISR : revalidate every hour
```

**Pages concernées** : Home, About, Pricing

### Blog (ISR - Incremental Static Regeneration)

Articles générés statiquement mais revalidés périodiquement :

```typescript
// app/(marketing)/blog/[slug]/page.tsx
export async function generateStaticParams() {
  const articles = await getAllArticleSlugs();
  return articles.map((slug) => ({ slug }));
}

export const revalidate = 600; // Revalidate every 10min
```

**Avantages** :
- Performance (pages servies depuis CDN)
- SEO optimal (HTML complet au premier load)
- Contenu frais sans rebuild complet

### Formulaire contact (API Route)

```typescript
// app/api/contact/route.ts
export async function POST(request: Request) {
  const body = await request.json();

  // 1. Validation Zod
  const validated = contactSchema.parse(body);

  // 2. Envoi email via Resend
  await resend.emails.send({
    from: 'website@clienta.com',
    to: 'sales@clienta.com',
    subject: `New contact from ${validated.name}`,
    html: generateEmailTemplate(validated)
  });

  // 3. Notification Slack (optionnel)
  await notifySlack(validated);

  return Response.json({ success: true });
}
```

---

## 🎨 Design System Architecture

### Pattern Atomic Design

Inspiré de [[06-Zettelkasten/Pattern-Design-Atomic|Pattern Design Atomic]]

```
Atoms (composants de base)
  ├── Button
  ├── Input
  ├── Label
  └── Icon

Molecules (combinaisons simples)
  ├── FormField (Label + Input + Error)
  ├── CardHeader (Icon + Title + Description)
  └── NavigationItem (Link + Icon)

Organisms (sections complexes)
  ├── Header (Logo + Navigation + CTA)
  ├── Hero (Headline + Description + CTA + Visual)
  └── PricingCard (Card + Features list + CTA)

Templates (layouts pages)
  ├── MarketingLayout (Header + Children + Footer)
  └── BlogLayout (Sidebar + Content)

Pages (instances templates avec vraies données)
  ├── HomePage
  ├── PricingPage
  └── BlogArticlePage
```

### Tokens de design

```typescript
// tailwind.config.ts
export default {
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#e6f0ff',
          // ...
          500: '#0066FF', // Bleu ClientA
          // ...
          900: '#001a44',
        },
        secondary: {
          500: '#00C896', // Vert accent
        }
      },
      typography: {
        DEFAULT: {
          css: {
            fontFamily: 'Inter, sans-serif',
            // ...
          }
        }
      }
    }
  }
}
```

---

## 🔌 Intégrations

### Contentful CMS

**Modèles de contenu** :
- `blogArticle` : Articles de blog
- `caseStudy` : Études de cas clients
- `pressRelease` : Communiqués presse

**GraphQL Query exemple** :

```graphql
query GetBlogArticle($slug: String!) {
  blogArticleCollection(where: { slug: $slug }, limit: 1) {
    items {
      title
      slug
      publishDate
      author {
        name
        avatar {
          url
        }
      }
      content {
        json
      }
      featuredImage {
        url
        title
      }
    }
  }
}
```

**Webhook revalidation** :
- Contentful → POST /api/revalidate → Next.js revalidate path
- Permet refresh contenu sans rebuild complet

### Resend (Email)

```typescript
// lib/email.ts
import { Resend } from 'resend';

const resend = new Resend(process.env.RESEND_API_KEY);

export async function sendContactEmail(data: ContactFormData) {
  return resend.emails.send({
    from: 'ClientA Website <noreply@clienta.com>',
    to: ['sales@clienta.com'],
    replyTo: data.email,
    subject: `New contact: ${data.company}`,
    html: renderContactEmailTemplate(data)
  });
}
```

### Analytics & Monitoring

**Google Analytics 4** :

```typescript
// lib/gtag.ts
export const GA_TRACKING_ID = process.env.NEXT_PUBLIC_GA_ID;

export const pageview = (url: string) => {
  window.gtag('config', GA_TRACKING_ID, {
    page_path: url,
  });
};

export const event = ({ action, category, label, value }: GtagEvent) => {
  window.gtag('event', action, {
    event_category: category,
    event_label: label,
    value: value,
  });
};
```

**Sentry** (Error tracking) :

```typescript
// sentry.client.config.ts
import * as Sentry from "@sentry/nextjs";

Sentry.init({
  dsn: process.env.NEXT_PUBLIC_SENTRY_DSN,
  tracesSampleRate: 0.1,
  environment: process.env.NEXT_PUBLIC_ENV,
});
```

---

## ⚡ Optimisations Performance

### Images

```tsx
// Utilisation Next.js Image
import Image from 'next/image';

<Image
  src="/hero-illustration.png"
  alt="ClientA Dashboard"
  width={1200}
  height={800}
  priority // LCP optimization
  placeholder="blur"
  blurDataURL="data:image/jpeg;base64,..."
/>
```

### Fonts

```typescript
// app/layout.tsx
import { Inter } from 'next/font/google';

const inter = Inter({
  subsets: ['latin'],
  display: 'swap',
  variable: '--font-inter',
});
```

### Code splitting

- React.lazy() pour composants lourds (animations, charts)
- Dynamic imports Next.js pour sections non-critiques

```typescript
import dynamic from 'next/dynamic';

const PricingCalculator = dynamic(
  () => import('@/components/pricing-calculator'),
  { ssr: false } // Client-side only
);
```

### Caching strategy

| Ressource | Strategy | Cache Duration |
|-----------|----------|----------------|
| Images static | Cache-Control: public, immutable | 1 year |
| Pages SSG | s-maxage=3600, stale-while-revalidate | 1h |
| API Routes | Cache-Control: no-store | No cache |
| Fonts | Cache-Control: public, immutable | 1 year |

---

## 🔐 Sécurité

### Headers HTTP

```javascript
// next.config.js
module.exports = {
  async headers() {
    return [
      {
        source: '/(.*)',
        headers: [
          {
            key: 'X-Content-Type-Options',
            value: 'nosniff',
          },
          {
            key: 'X-Frame-Options',
            value: 'SAMEORIGIN',
          },
          {
            key: 'X-XSS-Protection',
            value: '1; mode=block',
          },
        ],
      },
    ];
  },
};
```

### Validation formulaires

- Zod schemas côté serveur (API Routes)
- React Hook Form + Zod côté client
- CSRF protection (Vercel built-in)

### Variables d'environnement

```bash
# .env.local (non commité)
CONTENTFUL_SPACE_ID=xxx
CONTENTFUL_ACCESS_TOKEN=xxx
RESEND_API_KEY=re_xxx
NEXT_PUBLIC_GA_ID=G-xxx
SENTRY_DSN=https://xxx@sentry.io/xxx
```

---

## 🚀 CI/CD & Déploiement

### Pipeline Vercel

```yaml
# Automatique sur push main
1. Install dependencies (pnpm install)
2. Lint (next lint)
3. Type check (tsc --noEmit)
4. Build (next build)
5. Deploy to production (vercel deploy --prod)
```

### Environnements

| Env | Branch | URL | Usage |
|-----|--------|-----|-------|
| Production | main | clienta.com | Site live |
| Preview | * | xxx-preview.vercel.app | Review PRs |
| Development | local | localhost:3000 | Dev local |

### Rollback strategy

- Git revert commit → automatic redeploy
- Vercel dashboard : rollback to previous deployment (1-click)

---

## 📊 Monitoring & Observabilité

### Métriques clés

**Performance** (Vercel Analytics) :
- Real User Monitoring (RUM)
- Core Web Vitals par page
- Time to First Byte (TTFB)

**Errors** (Sentry) :
- Error rate
- Affected users
- Stack traces

**Business** (GA4) :
- Conversion rate formulaires
- Bounce rate par page
- Session duration

### Alertes

- Sentry : alert si error rate > 1% (Slack webhook)
- Vercel : alert si Core Web Vitals dégradés
- Uptime monitoring : UptimeRobot (ping /api/health every 5min)

---

## 🔗 Références

- Next.js 14 Docs : https://nextjs.org/docs
- Contentful GraphQL Playground : https://graphql.contentful.com/
- Vercel Dashboard : https://vercel.com/agency/clienta
- Architecture Microservices (inspiration) : [[06-Zettelkasten/Architecture-Microservices]]
