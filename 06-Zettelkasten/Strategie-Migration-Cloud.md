---
type: zettel
created: 2024-09-20
tags: [zettelkasten, cloud, migration, aws, strategy]
domain: "Stratégie"
status: "🌳 Evergreen"
---

# Stratégie Migration Cloud : Framework 6R

## 🔑 Concept principal

> Le framework 6R d'AWS catégorise les stratégies de migration cloud en 6 approches (Rehost, Replatform, Refactor, Repurchase, Retire, Retain), guidant les décisions techniques et économiques.

---

## 📝 Développement

### Les 6 stratégies (6R)

**1. Rehost (Lift & Shift)** : Migration as-is vers cloud  
→ Rapide, faible risque, pas d'optimisation  
→ Use case : 60% migrations, apps stables

**2. Replatform (Lift & Reshape)** : Optimisations mineures  
→ Ex: DB → RDS, apps → Managed services  
→ Use case : 30% migrations, quick wins

**3. Refactor (Re-architect)** : Réécriture cloud-native  
→ Serverless, containers, microservices  
→ Use case : 10% migrations, apps critiques haute charge

**4. Repurchase** : Remplacer par SaaS  
→ Ex: Exchange → Google Workspace  
→ Use case : Legacy apps avec alternatives SaaS

**5. Retire** : Décommissionner  
→ Apps obsolètes identifiées lors audit  
→ Use case : 2-5% patrimoine apps

**6. Retain** : Garder on-premise  
→ Contraintes légales, apps critiques  
→ Use case : 10-15% apps temporairement

### Matrice de décision

| Critère | Rehost | Replatform | Refactor |
|---------|--------|------------|----------|
| Coût | Bas | Moyen | Élevé |
| Temps | Rapide | Moyen | Long |
| Risque | Faible | Moyen | Élevé |
| Bénéfices cloud | Limités | Moyens | Maximaux |
| Compétences | Faibles | Moyennes | Élevées |

---

## 💡 Insights & Connexions

### Pourquoi c'est important

- **Économique** : Prioriser quick wins (Rehost/Replatform 90%)
- **Risques** : Refactor uniquement si ROI justifié
- **Planning** : Framework structure décisions migration

### Quand l'utiliser

✅ Toute migration cloud (AWS, Azure, GCP)  
✅ Audit patrimoine applicatif  
✅ Business case migration

---

## 🔗 Liens

### Connexions directes
- [[02-Projects/ClientB-Migration-Cloud-AWS/plan-migration]] - (applique) 60% Rehost, 30% Replatform, 10% Refactor
- [[06-Zettelkasten/Securite-AWS-IAM]] - (complète) Sécurité post-migration

### Projets
- [[02-Projects/ClientB-Migration-Cloud-AWS/_index]] - Framework 6R guide migration 40 apps

### Sources
- AWS Migration Hub: https://aws.amazon.com/migration-hub
- AWS CAF (Cloud Adoption Framework)

---

## 🏷️ Métadonnées

| Champ | Valeur |
|-------|--------|
| **Domaine** | Stratégie (Cloud, Migration) |
| **Statut** | 🌳 Evergreen |
| **Confiance** | ⭐⭐⭐⭐⭐ (5/5) |
| **Dernière révision** | 2024-10-17 |

---

## 📚 Évolution

### 2024-09-20
- Création initiale audit ClientB

### 2024-10-17
- Ajout matrice décision
- Lien projet ClientB
