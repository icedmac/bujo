---
type: zettel
created: 2024-09-25
tags: [zettelkasten, architecture, backend, microservices]
domain: "Technique"
status: "🌿 Budding"
---

# Architecture Microservices

## 🔑 Concept principal

> Les microservices décomposent une application monolithique en services indépendants, déployables séparément, communiquant via APIs, chacun responsable d'un domaine métier spécifique.

---

## 📝 Développement

### Principes fondamentaux

**Single Responsibility** : Chaque service = 1 fonction métier  
**Autonomie** : Déploiement indépendant, base de données propre  
**Communication** : APIs REST/gRPC, messaging asynchrone  
**Décentralisation** : Pas de point central de défaillance

### Avantages

- Scalabilité indépendante par service
- Technologies hétérogènes possibles
- Résilience (failure isolation)
- Déploiement continu facilité

### Inconvénients

- Complexité opérationnelle accrue
- Latence réseau inter-services
- Gestion transactions distribuées difficile
- Debugging plus complexe

---

## 💡 Insights & Connexions

### Quand l'utiliser

✅ Applications large-scale (>10 devs)  
✅ Besoins scalabilité différente par module  
❌ MVP ou petite équipe (monolithe préférable)

### Limitations

- Over-engineering pour petits projets
- Coûts infrastructure plus élevés
- Besoin DevOps/observabilité matures

---

## 🔗 Liens

### Connexions directes
- [[06-Zettelkasten/Pattern-Design-Atomic]] - (similitude) Décomposition UI ≈ Décomposition backend
- [[02-Projects/ClientA-Refonte-SiteWeb/architecture]] - (référence) CMS Headless Contentful = approche microservices

### Projets
- [[02-Projects/ClientA-Refonte-SiteWeb/_index]] - Architecture découplée frontend/CMS

### Sources
- "Building Microservices" by Sam Newman
- Martin Fowler blog: https://martinfowler.com/microservices

---

## 🏷️ Métadonnées

| Champ | Valeur |
|-------|--------|
| **Domaine** | Technique (Backend, Architecture) |
| **Statut** | 🌿 Budding |
| **Confiance** | ⭐⭐⭐⭐ (4/5) |
| **Dernière révision** | 2024-10-15 |

---

## 📚 Évolution

### 2024-09-25
- Création initiale

### 2024-10-15
- Lien ajouté projet ClientA (CMS headless)
