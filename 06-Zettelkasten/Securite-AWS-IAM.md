---
type: zettel
created: 2024-09-18
tags: [zettelkasten, security, aws, iam, cloud]
domain: "Technique"
status: "🌳 Evergreen"
---

# Sécurité AWS IAM Best Practices

## 🔑 Concept principal

> AWS IAM (Identity & Access Management) gère l'authentification et autorisation dans AWS. Best practices : Least Privilege, MFA obligatoire, roles over users, pas de long-term credentials.

---

## 📝 Développement

### Principes fondamentaux

**Least Privilege** : Accorder uniquement permissions nécessaires  
**Defense in Depth** : Plusieurs couches sécurité  
**Assume Breach** : Concevoir système résilient même si compromis

### 10 Best Practices IAM

1. **Root account** : MFA activé, jamais utilisé (break-glass uniquement)
2. **Users** : Pas de long-term access keys, SSO obligatoire
3. **Roles** : Prefer roles over users (AssumeRole temporary credentials)
4. **MFA** : Obligatoire pour utilisateurs humains
5. **Policies** : Deny by default, grant explicit permissions
6. **Service roles** : Applications utilisent roles (EC2, Lambda, ECS)
7. **Secrets** : AWS Secrets Manager (rotation auto 90j)
8. **Audit** : CloudTrail activé, logs immuables S3
9. **Permissions boundaries** : Limiter max permissions IAM entities
10. **Policy conditions** : Restrict by IP, time, MFA status

### Architecture IAM multi-comptes

```
AWS Organizations
├── Root Account (MFA, unused)
├── Production Account
│   ├── SSO (Azure AD / Okta)
│   └── Roles (Admin, DevOps, Developer, Auditor)
├── Staging Account
└── Dev Account
```

---

## 💡 Insights & Connexions

### Pourquoi c'est important

- **Compliance** : PCI-DSS, ISO 27001 exigent IAM rigoureux
- **Breach prevention** : 90% breaches = credentials compromises
- **Audit** : CloudTrail = traçabilité complète

### Quand l'utiliser

✅ Toute architecture AWS  
✅ Multi-comptes (Organizations)  
✅ Conformité réglementaire

### Limitations

- Courbe apprentissage IAM complexe
- Policies JSON verbeux
- Debugging permissions difficile (IAM Policy Simulator)

---

## 🔗 Liens

### Connexions directes
- [[02-Projects/ClientB-Migration-Cloud-AWS/_index]] - (applique) Modèle IAM SSO + roles
- [[06-Zettelkasten/Strategie-Migration-Cloud]] - (complète) Sécurité post-migration

### Projets
- [[02-Projects/ClientB-Migration-Cloud-AWS/_index]] - Matrice IAM validée RSSI, MFA obligatoire

### Sources
- AWS Security Best Practices: https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html
- CIS AWS Foundations Benchmark

---

## 🏷️ Métadonnées

| Champ | Valeur |
|-------|--------|
| **Domaine** | Technique (Sécurité, Cloud) |
| **Statut** | 🌳 Evergreen |
| **Confiance** | ⭐⭐⭐⭐⭐ (5/5) |
| **Dernière révision** | 2024-10-17 |

---

## 📚 Évolution

### 2024-09-18
- Création initiale phase architecture ClientB

### 2024-10-17
- Ajout section multi-comptes
- Lien projet ClientB (matrice IAM)
