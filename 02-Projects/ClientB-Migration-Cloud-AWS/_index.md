---
type: project
client: "ClientB (Finance)"
status: "🔵 En cours"
priority: "🟡 Moyenne"
start_date: 2024-09-15
deadline: 2025-02-28
budget: "80 jours / 120 000€"
tags: [project, para, cloud, infrastructure, aws]
---

# 🎯 Migration Infrastructure Cloud AWS - ClientB

## 📋 Informations projet

| Champ | Valeur |
|-------|--------|
| **Client** | [[ClientB]] (Secteur Finance - Fintech) |
| **Statut** | 🔵 En cours |
| **Priorité** | 🟡 Moyenne (Critical business impact mais timeline confortable) |
| **Date début** | 2024-09-15 |
| **Deadline** | 2025-02-28 |
| **Budget** | 80 jours / 120 000€ |
| **Ressources allouées** | 4 personnes (1 Architecte Cloud, 2 DevOps, 1 Security Engineer) |

---

## 🎯 Objectifs & Livrables

### Objectif principal

Migrer l'infrastructure on-premise de ClientB (actuellement datacenters privés OVH) vers AWS Cloud pour bénéficier de scalabilité, résilience, et réduire les coûts opérationnels de 35% sur 3 ans.

### Livrables attendus
- [x] Audit infrastructure existante (inventaire complet 150+ serveurs)
- [x] Architecture cloud cible (AWS Well-Architected Framework)
- [ ] Plan de migration détaillé par application (40 applications)
- [ ] Migration progressive par vagues (4 vagues sur 3 mois)
- [ ] Disaster Recovery Plan (RPO < 1h, RTO < 4h)
- [ ] Formation équipes ops ClientB (3 sessions)
- [ ] Documentation runbooks (monitoring, incidents, scaling)
- [ ] Tests de charge et disaster recovery

### Critères de succès
- **Disponibilité** : 99.9% SLA minimum (vs 98.5% actuel on-premise)
- **Performance** : Latence API < 200ms (p95) maintenue
- **Sécurité** : Conformité PCI-DSS, ISO 27001, RGPD
- **Coûts** : TCO cloud < 65% coûts on-premise sur 3 ans
- **Zéro incident** majeur pendant migration (downtime non planifié)

---

## 👥 Stakeholders

| Rôle | Nom | Contact | Responsabilité |
|------|-----|---------|----------------|
| Sponsor | Pierre Lefèvre | pierre.lefevre@clientb.com | Validation stratégique, budget, décisions go/no-go |
| DSI | Nathalie Moreau | nathalie.moreau@clientb.com | Owner technique, validation architecture, ressources IT |
| RSSI | Jérôme Dubois | jerome.dubois@clientb.com | Conformité sécurité, validation IAM, audits |
| CTO | Antoine Bernard | antoine.bernard@clientb.com | Validation applicative, contraintes produit |
| DevOps Lead | Sarah Martin | sarah.martin@clientb.com | Coordination équipes ops, runbooks, monitoring |

---

## 📊 Phases & Jalons

### Phase 1 : Audit & Évaluation (Sept 2024) ✅
- **Dates** : 2024-09-15 → 2024-09-30
- **Objectif** : Cartographier l'existant et évaluer complexité migration
- **Livrables** :
  - [x] Inventaire infrastructure (150 VMs, 80 DBs, 40 apps)
  - [x] Audit performances actuelles (baseline metrics)
  - [x] Analyse dépendances inter-applications (mapping complet)
  - [x] Assessment AWS Migration Readiness (score 68/100)
  - [x] Estimation TCO cloud vs on-premise (business case validé)

**Statut** : ✅ Terminée (30/09/2024)

**Findings clés** :
- 40% des applications legacy (monolithes Java 8, bases Oracle 11g)
- 15 applications critiques nécessitant migration prioritaire
- Besoin refactoring 8 applications pour cloud-native patterns

### Phase 2 : Planification & Design (Oct-Nov 2024) 🔵
- **Dates** : 2024-10-01 → 2024-11-30
- **Objectif** : Concevoir l'architecture cloud cible et stratégie migration
- **Livrables** :
  - [x] Architecture AWS multi-région (eu-west-1 primary, eu-central-1 DR)
  - [x] Design réseau (VPC, subnets, Transit Gateway, VPN hybride)
  - [x] Stratégie IAM & sécurité (AWS Organizations, SSO, GuardDuty)
  - [x] Plan de migration par vagues (4 vagues, 40 applications)
  - [ ] Proof of Concept (migration 3 apps non-critiques)
  - [ ] Runbooks automation (Terraform modules, CI/CD pipelines)
  - [ ] Plan disaster recovery détaillé

**Statut** : 🔵 En cours (75% complété)

**Avancement détaillé** :
- Architecture réseau validée par RSSI
- PoC vague 0 : 2/3 applications migrées avec succès
- **Blocage actif** : Attente validation RSSI sur matrice IAM roles (depuis 15/10)

### Phase 3 : Migration Progressive (Déc 2024 - Jan 2025) ⏳
- **Dates** : 2024-12-01 → 2025-01-31
- **Objectif** : Migrer applications par vagues avec validation progressive
- **Planning vagues** :
  - **Vague 1** (Déc 1-15) : 8 applications non-critiques (dev/staging envs)
  - **Vague 2** (Déc 16-31) : 12 applications business (CRM, Analytics, BI)
  - **Vague 3** (Jan 7-21) : 15 applications critiques (Payment, Core Banking)
  - **Vague 4** (Jan 22-31) : 5 applications legacy complexes (mainframe interfaces)

**Stratégie migration** :
- Lift & Shift (60% apps) : rehosting EC2
- Replatform (30% apps) : RDS, Elastic Beanstalk
- Refactor (10% apps) : serverless Lambda + DynamoDB

**Statut** : ⏳ Pas encore démarrée

### Phase 4 : Validation & Optimisation (Fév 2025) ⏳
- **Dates** : 2025-02-01 → 2025-02-28
- **Objectif** : Valider stabilité, optimiser coûts, fermer datacenters on-premise
- **Livrables** :
  - [ ] Tests de charge (simuler 150% charge normale)
  - [ ] Disaster Recovery drill (test RTO/RPO)
  - [ ] Optimisation coûts (Reserved Instances, Savings Plans)
  - [ ] Documentation finale (architecture as-built)
  - [ ] Formation équipes ClientB (3 sessions : ops, dev, security)
  - [ ] Décommissioning infrastructure on-premise

**Statut** : ⏳ Pas encore démarrée

---

## ✅ Tâches & Actions

### À faire cette semaine
- [ ] Finaliser PoC vague 0 (migration 3ème app : API Analytics)
- [ ] Relancer RSSI pour validation matrice IAM
- [ ] Préparer deck présentation comité direction (25/10)

### En cours
- [ ] Développement modules Terraform pour EC2 + RDS
- [ ] Setup CI/CD pipelines AWS CodePipeline
- [ ] Configuration monitoring (CloudWatch + Grafana)

### Bloqué
- [ ] **Validation matrice IAM roles** (Raison : RSSI en congés jusqu'au 22/10, son adjoint non décisionnaire. Impact : impossible finaliser PoC vague 0, retard 1 semaine sur planning Phase 2)

### Terminé
- [x] Inventaire complet infrastructure (150 VMs, 80 DBs)
- [x] Audit performances baseline (métriques CPU, RAM, IOPS, latence)
- [x] Architecture réseau AWS (VPC multi-AZ, Transit Gateway)
- [x] Design stratégie multi-région (primary eu-west-1, DR eu-central-1)
- [x] Setup compte AWS Organizations + Landing Zone
- [x] Configuration réseau hybride (VPN site-to-site on-premise ↔ AWS)
- [x] Migration 2/3 applications PoC vague 0

---

## 📝 Notes & Documentation

### Documentation technique
- [[02-Projects/ClientB-Migration-Cloud-AWS/plan-migration|Plan de migration détaillé par application]]
- Architecture AWS Diagrams : Lucidchart (https://lucid.app/clientb-aws-arch)
- Terraform Repository : https://github.com/agency/clientb-aws-infra
- Runbooks Notion : https://notion.so/clientb-runbooks

### Contraintes majeures

**Sécurité & Conformité** :
- **PCI-DSS Level 1** : applications payment doivent respecter normes strictes
- **ISO 27001** : audit annuel prévu Mars 2025, infra cloud doit être compliant
- **RGPD** : données personnelles UE uniquement (pas de région us-east-1)
- **Secrets Management** : AWS Secrets Manager obligatoire (pas de hardcoded credentials)

**Disponibilité 24/7** :
- Applications critiques ne peuvent tolérer downtime > 30min
- Stratégie migration : blue/green deployment avec rollback capability
- Fenêtres de maintenance : Dimanche 2h-6h AM uniquement

**Performances** :
- Latence API : maintenir < 200ms (p95) post-migration
- Throughput DB : 10K transactions/sec minimum (actuellement 8K)
- Monitoring proactif : alertes si dégradation > 10% baseline

---

## 🔄 Suivi d'avancement

### Avancement global
**40%** complété

**Breakdown** :
- Phase 1 (Audit) : 100% ✅
- Phase 2 (Planification) : 75% 🔵
- Phase 3 (Migration) : 0% ⏳
- Phase 4 (Validation) : 0% ⏳

### Burn budget
- **Consommé** : 32 jours / 80 jours (40%)
- **Prévisionnel fin Phase 2** : 42 jours (52.5%)
- **Budget Phase 3 (migration)** : 28 jours alloués
- **Buffer** : 10 jours (12.5%)

### Dernière mise à jour
2024-10-20

### Prochaines étapes
1. **Débloquer validation RSSI** (escalade à DSI Nathalie Moreau) - **Urgence : Haute, Deadline : 22/10**
2. **Finaliser PoC vague 0** (3ème app) - **Deadline : 25/10**
3. **Présentation comité direction** (go/no-go Phase 3) - **Date : 30/10**

---

## ⚠️ Risques & Blocages

| Risque | Probabilité | Impact | Mitigation |
|--------|-------------|--------|------------|
| **Downtime applications critiques pendant migration** | M | H | Blue/green deployment, tests exhaustifs pré-prod, rollback automatique |
| **Dépassement coûts AWS** (mauvaise estimation) | H | M | Reserved Instances + Savings Plans, monitoring budgets (AWS Cost Explorer), optimisation post-migration |
| **Compétences équipe ClientB insuffisantes** | M | M | Formation intensive 3 sessions, documentation runbooks détaillée, support post-migration 3 mois |
| **Latence accrue post-migration** | M | H | Architecture multi-AZ, CloudFront CDN, optimisation DB (RDS read replicas), tests de charge |
| **Non-conformité sécurité** (audit ISO 27001) | L | H | Validation RSSI chaque étape, AWS Config rules, GuardDuty, CloudTrail logging |
| **Legacy apps incompatibles cloud** | M | H | Assessment détaillé fait, plan refactoring 8 apps identifiées, budget dédié |
| **Dépendances cachées inter-apps** | M | M | Mapping dépendances fait Phase 1, tests d'intégration rigoureux, migration par vagues |

### Blocages actuels

- 🚨 **Validation matrice IAM roles** (depuis 15/10, 5 jours de retard) :
  - **Raison** : RSSI Jérôme Dubois en congés jusqu'au 22/10, son adjoint Kevin Rousseau ne peut valider (pas scope décisionnel)
  - **Impact** : Impossible finaliser PoC vague 0 (besoin accès IAM pour migration 3ème app), retard 1 semaine Phase 2
  - **Action** : Escalade à DSI Nathalie Moreau (20/10), demande validation exceptionnelle adjoint RSSI ou accélération retour Jérôme
  - **Deadline critique** : 22/10 (sinon décalage présentation comité direction)

---

## 💡 Idées & Améliorations

### Idées capturées

- [[00-Inbox/idee-automation-deployment-ci-cd|Automatisation déploiements avec AWS CodePipeline + GitOps]] (suggéré lors audit Phase 1)

### Optimisations possibles

- **FinOps** : Setup AWS Cost Anomaly Detection pour alertes dépassements budgets
- **Observabilité** : Centraliser logs avec AWS OpenSearch + Kibana dashboards
- **Auto-scaling intelligent** : Utiliser AWS Auto Scaling predictive scaling (ML) au lieu de rule-based
- **Disaster Recovery** : Implémenter AWS Backup cross-region pour RTO/RPO améliorés

---

## 🔗 Liens & Ressources

### Réunions
- [[07-Meetings/2024-10-17-Audit-Technique-ClientB|Réunion audit technique - 17/10/2024]]

### Notes Zettelkasten liées
- [[06-Zettelkasten/Strategie-Migration-Cloud|Stratégie Migration Cloud : 6R framework]] - méthodologie appliquée
- [[06-Zettelkasten/Securite-AWS-IAM|Sécurité AWS IAM Best Practices]] - référence pour design IAM

### Références externes
- AWS Architecture Diagrams : https://lucid.app/clientb-aws
- Terraform Infra Repository : https://github.com/agency/clientb-aws-infra
- AWS Well-Architected Review : https://console.aws.amazon.com/wellarchitected
- Runbooks Notion : https://notion.so/clientb-runbooks
- Dashboard Monitoring : https://grafana.clientb-aws.com

---

## 📅 Historique

### 2024-10-20
- Escalade blocage RSSI à DSI Nathalie Moreau
- Point budget : 32j consommés / 80j (on track)
- Développement modules Terraform pour vague 1

### 2024-10-17
- Réunion technique avec équipe DevOps ClientB
- Validation architecture réseau hybride (VPN site-to-site opérationnel)
- Setup environnement staging AWS (VPC, subnets, bastion hosts)

### 2024-10-15
- Soumission matrice IAM roles au RSSI pour validation
- Migration réussie 2/3 apps PoC vague 0 (API Users, API Notifications)

### 2024-10-01
- Début Phase 2 (Planification & Design)
- Workshop architecture AWS avec équipe ClientB (2 jours)
- Décisions : multi-région (eu-west-1 + eu-central-1), AWS Organizations, Transit Gateway

### 2024-09-30
- Fin Phase 1 (Audit) : livraison rapport complet (120 pages)
- Présentation findings à comité direction ClientB
- Validation business case migration (économies 35% TCO sur 3 ans)

### 2024-09-15
- Kickoff projet
- Démarrage inventaire infrastructure
- Setup accès on-premise ClientB (VPN, comptes SSH)

---

## 📋 Clôture (à compléter en fin de projet)

### Date de clôture
_À compléter (prévu 28/02/2025)_

### Résultats
_À compléter après Phase 4 et 1 mois de monitoring production_

**Métriques cibles** :
- Disponibilité ≥ 99.9%
- Latence API < 200ms (p95)
- Coûts cloud < 65% coûts on-premise
- Zéro incident majeur migration

### Retour d'expérience
_À compléter après rétrospective équipe_

### Archivage
- [ ] Documentation technique archivée (Confluence ClientB)
- [ ] Runbooks transférés équipe ops ClientB
- [ ] Accès AWS transférés (comptes IAM équipe ClientB)
- [ ] Projet déplacé vers [[05-Archives/2025-ClientB-Migration-AWS]]
- [ ] Facturation finalisée (validation DSI)
- [ ] Retour client collecté (CSAT, testimonial)
- [ ] Décommissioning datacenters on-premise validé
