---
type: meeting
date: 2024-10-17
time: "10:00"
duration: "3h"
project: "[[02-Projects/ClientB-Migration-Cloud-AWS/_index|ClientB Migration Cloud AWS]]"
tags: [meeting, technique, clientb, cloud]
---

# 🤝 Réunion Audit Technique - Migration Cloud ClientB

## 📋 Informations

| Champ | Valeur |
|-------|--------|
| **Date** | 2024-10-17 |
| **Heure** | 10:00 - 13:00 |
| **Durée** | 3h |
| **Projet lié** | [[02-Projects/ClientB-Migration-Cloud-AWS/_index|ClientB Migration Cloud AWS]] |
| **Type** | Revue technique (architecture, sécurité, réseau) |
| **Lieu** | Sur site ClientB (Paris La Défense) |

---

## 👥 Participants

| Nom | Rôle | Organisation |
|-----|------|--------------|
| Nathalie Moreau | DSI | ClientB |
| Jérôme Dubois | RSSI | ClientB |
| Antoine Bernard | CTO | ClientB |
| Sarah Martin | DevOps Lead | ClientB |
| **Notre équipe** | | |
| Marc Lefèvre | Architecte Cloud | Agence |
| Émilie Durand | Security Engineer | Agence |
| Kevin Lambert | DevOps Senior | Agence |

---

## 🎯 Objectifs de la réunion

1. Validation architecture réseau hybride (VPN site-to-site AWS)
2. Revue stratégie sécurité et conformité (PCI-DSS, ISO 27001)
3. Présentation plan migration par vagues
4. Validation matrice IAM roles
5. Discussion disaster recovery strategy

---

## 💬 Notes & Discussions

### 1. Validation architecture réseau

**Présenté par Marc Lefèvre (Architecte Cloud)** :

✅ **Architecture multi-région validée** :
- **Région primary** : eu-west-1 (Irlande)
- **Région DR** : eu-central-1 (Francfort)
- **Justification** : Latence optimale France, data residency UE (RGPD)

✅ **Réseau hybride** :
- VPN site-to-site AWS opérationnel (setup terminé 16/10)
- Transit Gateway configuré (interconnexion VPCs + on-premise)
- Tests latence satisfaisants : 12ms moyenne Paris ↔ eu-west-1

**Questions équipe ClientB** :
- **Q (Sarah Martin - DevOps)** : "Bande passante VPN suffisante pour migration données ?"
  - **R** : VPN 10 Gbps provisionné. Migration volumineuse apps legacy (Vague 4) utiliseront AWS Snowball (transfert physique).

- **Q (Antoine Bernard - CTO)** : "Failover automatique eu-west-1 → eu-central-1 ?"
  - **R** : Oui, Route 53 health checks + failover policies (bascule automatique si eu-west-1 down).

**Décision** : Architecture réseau validée, pas de modification nécessaire.

### 2. Sécurité & Conformité

**Présenté par Émilie Durand (Security Engineer) + Discussion avec Jérôme Dubois (RSSI)** :

**PCI-DSS Level 1** :
- ✅ Applications payment isolées VPC dédiée
- ✅ Chiffrement at-rest KMS + in-transit TLS 1.3
- ✅ AWS Config rules pour validation conformité
- ✅ Logs immuables S3 Object Lock

**Point de vigilance RSSI** :
- ⚠️ Jérôme Dubois : "Matrice IAM roles doit être validée par moi personnellement avant toute migration PoC."
  - **Action** : Soumission matrice détaillée + documentation pour revue RSSI.

**ISO 27001** :
- ✅ Audit annuel prévu Mars 2025 (AWS artifacts disponibles)
- ✅ GuardDuty + CloudTrail activés
- ✅ Backup strategy conforme (RPO < 1h, RTO < 4h)

**RGPD** :
- ✅ Data residency UE uniquement (pas de région US)
- ✅ Encryption KMS clés gérées ClientB
- ✅ Scripts automatisés right to erasure

**Décision** : Stratégie sécurité validée, matrice IAM à soumettre formellement au RSSI.

### 3. Plan migration par vagues

**Présenté par Marc Lefèvre** :

**Vague 0 (PoC - Oct)** :
- 3 apps non-critiques
- **Statut actuel** : 2/3 migrées avec succès (API Users, API Notifications)
- 1 app en cours : API Analytics (bloquée : attente validation IAM RSSI)

**Vague 1-4 (Déc-Jan)** :
- 40 applications réparties sur 4 vagues
- Stratégie : 60% Rehost, 30% Replatform, 10% Refactor

**Questions équipe ClientB** :
- **Q (Nathalie Moreau - DSI)** : "Vague 3 (apps critiques) : quelle garantie zéro downtime ?"
  - **R** : Blue/green deployment systématique. Infrastructure dupliquée, bascule DNS instantanée, rollback rapide si incident.

- **Q (Sarah Martin - DevOps)** : "Formation équipes ops ClientB prévue quand ?"
  - **R** : 3 sessions planifiées Février 2025 (monitoring, incidents, scaling).

**Décision** : Planning vagues validé, go pour démarrer PoC vague 0 dès validation IAM.

### 4. Matrice IAM Roles

**Présenté par Émilie Durand** :

**Modèle proposé** :
- AWS Organizations (multi-comptes)
- SSO intégration Azure AD ClientB
- 4 roles principaux : Admin, DevOps, Developer, Auditor
- Service roles pour applications (EC2, Lambda, ECS)
- MFA obligatoire, pas de long-term credentials

**Discussion Jérôme Dubois (RSSI)** :
- 💬 "Modèle solide, conforme à nos standards sécurité."
- ⚠️ "Je dois valider formellement chaque role policy avant go PoC."
- 📅 "Je pars en congés demain (18/10) jusqu'au 22/10. Je valide dès mon retour."

**Blocage identifié** :
- Jérôme en congés 5 jours
- Son adjoint Kevin Rousseau présent mais pas scope décisionnel pour valider IAM
- **Impact** : Impossible finaliser PoC vague 0 (besoin accès IAM pour migrer API Analytics)

**Action critique** :
- Nathalie Moreau (DSI) : "Je vais voir si je peux accélérer la validation ou donner mandat à Kevin pour cette fois."

### 5. Disaster Recovery Strategy

**Présenté par Kevin Lambert (DevOps)** :

**Objectifs** :
- RPO < 1h (max perte données 1h)
- RTO < 4h (remise en service sous 4h)

**Stratégie** :
- Backups automatisés AWS Backup (quotidiens + rétention 30j)
- Réplication cross-region (eu-west-1 → eu-central-1)
- Disaster recovery drill prévu Février 2025

**Validation équipe ClientB** :
- ✅ Antoine Bernard (CTO) : "RPO/RTO conformes à nos exigences business."
- ✅ Sarah Martin : "Tests DR drill essentiels, à ne pas négliger."

**Décision** : DR strategy validée.

---

## ✅ Décisions prises

| # | Décision | Contexte | Impact |
|---|----------|----------|--------|
| 1 | **Architecture réseau hybride validée** | VPN site-to-site opérationnel, tests latence OK | Go pour migration technique |
| 2 | **Stratégie sécurité & conformité validée** | PCI-DSS, ISO 27001, RGPD couverts | Pas de risque compliance |
| 3 | **Planning vagues validé** | 4 vagues Déc-Jan, apps critiques en Vague 3 | Timeline claire pour équipes |
| 4 | **Matrice IAM à valider par RSSI** | Attente retour congés Jérôme (22/10) | Blocage PoC vague 0 (5j retard) |
| 5 | **Disaster Recovery strategy validée** | RPO < 1h, RTO < 4h conformes business | Tests DR drill prévus Fév 2025 |

---

## 🎯 Actions

| Action | Responsable | Deadline | Statut | Priorité |
|--------|-------------|----------|--------|----------|
| **Soumettre matrice IAM formellement au RSSI** | Émilie Durand | 17/10 soir | ✅ | Critique |
| **Valider matrice IAM roles** | Jérôme Dubois (RSSI) | 22/10 | 🚨 Bloqué | Critique |
| **Escalade DSI si validation retardée** | Marc Lefèvre | 20/10 | ⏳ | Haute |
| Finaliser migration API Analytics (PoC vague 0) | Kevin Lambert | 25/10 | 🚨 Bloqué IAM | Haute |
| Préparer deck présentation comité direction | Marc Lefèvre | 25/10 | ⏳ | Haute |
| Planifier sessions formation ops (Fév 2025) | Sarah Martin | 30/11 | ⏳ | Moyenne |

---

## ⚠️ Risques & Blocages identifiés

**Blocage immédiat** :
- 🚨 **Validation IAM RSSI** : Jérôme Dubois en congés jusqu'au 22/10
  - **Impact** : Impossible finaliser PoC vague 0, retard 5 jours Phase 2
  - **Mitigation** : Escalade DSI Nathalie Moreau pour accélérer validation ou mandat exceptionnel adjoint

**Risques discutés** :
1. **Compétences AWS équipe ClientB** : Formation prévue Fév, mais risque autonomie post-migration
   - **Mitigation** : Support agence 3 mois post-migration + runbooks détaillés

2. **Coûts AWS potentiellement supérieurs estimations** : Besoin monitoring fin fin financier
   - **Mitigation** : AWS Cost Explorer + Budgets + alertes dépassements

---

## 💡 Idées & Insights

### Insights techniques

- **Latence VPN excellente** (12ms) : Performance réseau ne sera pas problème migration
- **Équipe ClientB compétente** : Bonne compréhension enjeux cloud, facilite collaboration
- **Maturité sécurité** : RSSI Jérôme Dubois très pointu, processus validation rigoureux (bon signe qualité)

### À explorer

- **FinOps** : Sarah Martin intéressée par optimisation coûts AWS post-migration
  - → Atelier dédié prévu Février 2025 (Reserved Instances, Savings Plans)

---

## 🔄 Prochaines étapes

1. **Attente validation IAM RSSI** (deadline critique 22/10)
2. **Finaliser PoC vague 0** (dès déblocage IAM)
3. **Présentation comité direction ClientB** (30/10 - go/no-go Phase 3)

---

## 🔗 Liens

### Projet parent
- [[02-Projects/ClientB-Migration-Cloud-AWS/_index|ClientB Migration Cloud AWS]]
- [[02-Projects/ClientB-Migration-Cloud-AWS/plan-migration|Plan de migration détaillé]]

### Notes Zettelkasten liées
- [[06-Zettelkasten/Strategie-Migration-Cloud|Stratégie Migration Cloud]]
- [[06-Zettelkasten/Securite-AWS-IAM|Sécurité AWS IAM]]

---

## 📋 Suivi

- [x] Compte-rendu envoyé participants (17/10 soir)
- [x] Matrice IAM soumise RSSI (17/10 soir)
- [x] Action critique escalade DSI créée
- [ ] Prochaine réunion : Comité direction (30/10)

---

**Ambiance** : Réunion productive, collaboration excellente équipe ClientB. Point de vigilance : Dépendance RSSI pour validation IAM = risque planning.
