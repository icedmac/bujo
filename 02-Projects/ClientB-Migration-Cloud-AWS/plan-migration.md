# Plan de Migration Cloud AWS - ClientB

**Projet** : [[02-Projects/ClientB-Migration-Cloud-AWS/_index|ClientB Migration Cloud AWS]]
**Version** : 1.3
**Dernière MAJ** : 2024-10-20

---

## 🎯 Stratégie Globale

### Framework 6R d'AWS

Référence : [[06-Zettelkasten/Strategie-Migration-Cloud|Stratégie Migration Cloud 6R]]

| Stratégie | % Apps | Description | Use Cases |
|-----------|--------|-------------|-----------|
| **Rehost** (Lift & Shift) | 60% (24 apps) | Migration serveurs as-is vers EC2 | Apps stables sans refactoring nécessaire |
| **Replatform** (Lift & Reshape) | 30% (12 apps) | Migration avec optimisations mineures | Bases de données → RDS, apps → Elastic Beanstalk |
| **Refactor** (Re-architect) | 8% (3 apps) | Réécriture cloud-native | APIs haute charge → Lambda + DynamoDB |
| **Retire** | 2% (1 app) | Décommissionnement | App obsolète identifiée lors audit |

**Total** : 40 applications

---

## 📊 Planning par Vagues

### Vague 0 : Proof of Concept (Oct 2024) 🔵

**Objectif** : Valider processus migration sur 3 apps non-critiques

| App | Type | Stratégie | Statut | Notes |
|-----|------|-----------|--------|-------|
| API Users | REST API | Rehost (EC2 t3.medium) | ✅ Migré | Performance OK, latence -10% vs on-prem |
| API Notifications | Microservice | Rehost (EC2 t3.small) | ✅ Migré | Monitoring CloudWatch configuré |
| API Analytics | Analytics | Replatform (RDS PostgreSQL) | 🔵 En cours | Bloqué : validation IAM RSSI |

**Lessons learned** :
- Migration EC2 plus rapide que prévu (3j vs 5j estimé)
- Besoin automatiser snapshots DB (AWS Backup)
- Documentation runbooks essentielle pour équipe ClientB

### Vague 1 : Applications Non-Critiques (Déc 1-15, 2024) ⏳

**Objectif** : Migrer environnements dev/staging pour familiariser équipes

| App | Type | Stratégie | Downtime Max | Complexité |
|-----|------|-----------|--------------|------------|
| Intranet RH | Web App | Rehost (EC2 + RDS MySQL) | 4h | Faible |
| Outil BI interne | Analytics | Replatform (Redshift) | 8h | Moyenne |
| API Reporting | REST API | Rehost (EC2) | 2h | Faible |
| CRM interne | SaaS Legacy | Rehost (EC2 + EBS) | 6h | Faible |
| Monitoring Grafana | Observability | Rehost (EC2) | 1h | Faible |
| Wiki Confluence | Documentation | Rehost (EC2 + RDS PostgreSQL) | 4h | Faible |
| GitLab | Dev Tools | Rehost (EC2 + EFS) | 4h | Moyenne |
| Jenkins CI/CD | Dev Tools | Replatform (AWS CodeBuild) | 8h | Moyenne |

**Total** : 8 applications | **Budget** : 6 jours | **Fenêtre** : 2 semaines

**Risques** :
- GitLab : données Git volumineuses (500GB), prévoir bande passante suffisante
- Jenkins : refactoring pipelines pour AWS CodeBuild (estimation 2j)

### Vague 2 : Applications Business (Déc 16-31, 2024) ⏳

**Objectif** : Migrer apps business non-critiques pour Noël

| App | Type | Stratégie | Downtime Max | Complexité |
|-----|------|-----------|--------------|------------|
| CRM Salesforce | SaaS Integration | Replatform (EC2 + API Gateway) | 2h | Moyenne |
| ERP SAP BI | Analytics | Rehost (EC2 r5.2xlarge + RDS Oracle) | 4h | Haute |
| Plateforme E-learning | Web App | Rehost (EC2 + S3 + CloudFront) | 4h | Moyenne |
| API Marketing Automation | REST API | Rehost (EC2) | 1h | Faible |
| Data Warehouse | BI | Replatform (Redshift + Glue) | 12h | Haute |
| Plateforme Support Client | SaaS | Rehost (EC2 + RDS PostgreSQL) | 3h | Moyenne |
| API Webhooks Tiers | Integration | Rehost (EC2) | 30min | Faible |
| Dashboard Analytics | Web App | Refactor (Lambda + DynamoDB + S3) | 2h | Haute |
| API Scoring Client | ML | Rehost (EC2 g4dn.xlarge GPU) | 2h | Moyenne |
| Plateforme Onboarding | Web App | Rehost (EC2 + RDS MySQL) | 2h | Moyenne |
| API Notifications Push | Microservice | Refactor (SNS + Lambda) | 1h | Moyenne |
| ETL Data Pipeline | Batch Jobs | Replatform (AWS Glue + Step Functions) | 4h | Haute |

**Total** : 12 applications | **Budget** : 10 jours | **Fenêtre** : 2 semaines

**Risques** :
- SAP BI : licences Oracle coûteuses sur RDS, évaluer migration PostgreSQL (post-migration)
- Data Warehouse : migration données volumineuses (5TB), utiliser AWS Snowball
- Dashboard Analytics : refactoring complet (seule app serverless), tests rigoureux nécessaires

### Vague 3 : Applications Critiques (Jan 7-21, 2025) ⏳

**Objectif** : Migrer cœur métier avec haute disponibilité

| App | Type | Stratégie | Downtime Max | Complexité |
|-----|------|-----------|--------------|------------|
| **Core Banking API** | REST API | Rehost (EC2 Auto Scaling + ALB + RDS PostgreSQL Multi-AZ) | **0min** (blue/green) | **Très Haute** |
| **Payment Gateway** | API | Rehost (EC2 + RDS MySQL Multi-AZ + ElastiCache) | **0min** (blue/green) | **Très Haute** |
| **Customer Portal** | Web App | Rehost (EC2 + CloudFront + S3) | **30min** | Haute |
| **API Transactions** | REST API | Rehost (EC2 Auto Scaling + RDS PostgreSQL) | **0min** (blue/green) | Haute |
| **Fraud Detection** | ML | Rehost (EC2 g4dn.xlarge + RDS) | **1h** | Haute |
| **KYC Verification** | API | Rehost (EC2 + RDS MySQL + S3) | **30min** | Moyenne |
| **API Wallet** | Microservice | Rehost (EC2 + DynamoDB) | **0min** (blue/green) | Haute |
| **Reporting Réglementaire** | Batch | Replatform (AWS Batch + S3) | **2h** | Moyenne |
| **API Loans** | REST API | Rehost (EC2 + RDS PostgreSQL) | **1h** | Moyenne |
| **Customer Data Platform** | Data | Replatform (RDS + S3 + Athena) | **4h** | Haute |
| **API Credit Scoring** | ML | Rehost (EC2 + RDS + SageMaker endpoint) | **1h** | Haute |
| **Messaging Backbone** | Message Queue | Replatform (Amazon MQ / SQS + SNS) | **2h** | Haute |
| **API Accounts** | REST API | Rehost (EC2 Auto Scaling + RDS) | **0min** (blue/green) | Haute |
| **Audit Log System** | Logging | Replatform (CloudWatch Logs + S3) | **2h** | Moyenne |
| **API Documents** | Storage | Rehost (EC2 + S3 + Glacier) | **1h** | Moyenne |

**Total** : 15 applications | **Budget** : 12 jours | **Fenêtre** : 2 semaines

**Contraintes critiques** :
- **PCI-DSS** : Payment Gateway, Transactions API doivent respecter normes strictes
- **Zero downtime** : Core Banking, Payment, Transactions (blue/green deployment obligatoire)
- **Compliance** : Audit logs IMMUABLES (S3 Object Lock + Glacier Vault Lock)
- **Performance** : Latence API < 200ms (p95), débit 10K TPS minimum

**Stratégie blue/green** :
1. Déployer nouvelle infra AWS (green)
2. Synchronisation données temps réel (AWS DMS / custom replication)
3. Tests exhaustifs environnement green
4. Bascule DNS / Load Balancer (cutover 0 downtime)
5. Monitoring intensif 48h
6. Rollback rapide si incident (simple DNS switch back)

### Vague 4 : Applications Legacy Complexes (Jan 22-31, 2025) ⏳

**Objectif** : Migrer dernières apps (les plus complexes techniquement)

| App | Type | Stratégie | Downtime Max | Complexité |
|-----|------|-----------|--------------|------------|
| **Mainframe Interface** | Legacy | Rehost (EC2 + IBM MQ bridge) | **8h** | **Très Haute** |
| **Legacy ERP Custom** | Monolith | Rehost (EC2 r5.4xlarge + RDS Oracle RAC) | **12h** | **Très Haute** |
| **Batch Comptabilité** | COBOL Batch | Replatform (AWS Mainframe Modernization) | **24h** | **Très Haute** |
| **API Legacy SOAP** | Web Service | Rehost (EC2 + API Gateway) | **4h** | Haute |
| **Archivage Régulateur** | Storage | Replatform (S3 Glacier Deep Archive) | **6h** | Moyenne |

**Total** : 5 applications | **Budget** : 10 jours | **Fenêtre** : 10 jours

**Risques majeurs** :
- **Mainframe** : Complexité intégration, peu de compétences équipe, besoin expert IBM
- **COBOL** : Migration vers AWS Mainframe Modernization (service récent), risques techniques élevés
- **Oracle RAC** : Licensing complexe sur AWS, coût élevé, évaluer alternatives PostgreSQL
- **Budget dépassement** : Vague 4 potentiellement 15j (vs 10j estimé), buffer prévu

---

## 🏗️ Architecture Cible AWS

### Réseau Multi-Région

```
┌─────────────────────────────────────────────────────────────┐
│                     AWS Organization                        │
│  ┌───────────────────────────────────────────────────────┐  │
│  │  Account Production (eu-west-1 PRIMARY)               │  │
│  │  ┌────────────────────────────────────────────────┐   │  │
│  │  │  VPC 10.0.0.0/16                               │   │  │
│  │  │  ├── Public Subnets (3 AZs)                    │   │  │
│  │  │  │   └── NAT Gateway, ALB, CloudFront          │   │  │
│  │  │  ├── Private Subnets (3 AZs)                   │   │  │
│  │  │  │   └── EC2, ECS, Lambda                      │   │  │
│  │  │  └── Database Subnets (3 AZs)                  │   │  │
│  │  │      └── RDS Multi-AZ, ElastiCache, DynamoDB   │   │  │
│  │  └────────────────────────────────────────────────┘   │  │
│  └────────────────────┬──────────────────────────────────┘  │
│                       │                                     │
│  ┌────────────────────┴──────────────────────────────────┐  │
│  │  Account DR (eu-central-1 SECONDARY)                  │  │
│  │  ┌────────────────────────────────────────────────┐   │  │
│  │  │  VPC 10.1.0.0/16                               │   │  │
│  │  │  └── Same architecture (standby)               │   │  │
│  │  └────────────────────────────────────────────────┘   │  │
│  └───────────────────────────────────────────────────────┘  │
│                                                             │
│  ┌───────────────────────────────────────────────────────┐  │
│  │  Transit Gateway (inter-VPC + on-premise hybrid)      │  │
│  └────────────────┬──────────────────────────────────────┘  │
└───────────────────┼──────────────────────────────────────────┘
                    │
          ┌─────────┴─────────┐
          │   On-Premise      │
          │   (VPN Site-to-   │
          │    Site)          │
          └───────────────────┘
```

### Services AWS par Catégorie

**Compute** :
- EC2 (Auto Scaling Groups)
- ECS Fargate (containerized apps)
- Lambda (serverless APIs)
- AWS Batch (jobs batch)

**Database** :
- RDS Multi-AZ (PostgreSQL, MySQL, Oracle)
- DynamoDB (NoSQL haute performance)
- ElastiCache (Redis cache)
- Redshift (Data Warehouse)

**Storage** :
- S3 (object storage, archiving)
- EBS (block storage EC2)
- EFS (shared file storage)
- Glacier (archivage long-terme)

**Networking** :
- VPC (réseau isolé)
- ALB / NLB (load balancing)
- Route 53 (DNS)
- CloudFront (CDN)
- Transit Gateway (interconnexion)
- VPN Site-to-Site (hybrid cloud)

**Security** :
- IAM (identités et accès)
- AWS Organizations (multi-comptes)
- GuardDuty (threat detection)
- AWS WAF (web firewall)
- Secrets Manager (secrets management)
- CloudTrail (audit logs)

**Monitoring** :
- CloudWatch (métriques, logs, alarmes)
- X-Ray (tracing distribué)
- AWS Config (conformité configuration)

---

## 🔐 Stratégie Sécurité & Conformité

### Conformité réglementaire

**PCI-DSS Level 1** :
- Applications payment isolées dans VPC dédiée
- Chiffrement at-rest (EBS, RDS, S3) avec KMS
- Chiffrement in-transit (TLS 1.3)
- Logs immuables (S3 Object Lock)
- Scans vulnérabilités réguliers (AWS Inspector)

**ISO 27001** :
- AWS Config Rules pour validation configuration
- GuardDuty pour détection menaces
- CloudTrail activé sur tous comptes
- Audit annuel Mars 2025 (AWS artifacts fournis)

**RGPD** :
- Données personnelles UE uniquement (eu-west-1, eu-central-1)
- Data residency policy stricte
- Encryption KMS clés gérées ClientB
- Right to erasure implementé (scripts automatisés)

### IAM Strategy

**Modèle** : Least Privilege Access

```
AWS Organizations
├── Root Account (MFA obligatoire)
│
├── Production Account
│   ├── IAM Roles (AssumeRole from SSO)
│   │   ├── AdminRole (break-glass uniquement)
│   │   ├── DevOpsRole (deploy, monitoring)
│   │   ├── DeveloperRole (read-only prod)
│   │   └── AuditorRole (logs, compliance)
│   │
│   └── Service Roles (EC2, Lambda, ECS)
│
├── DR Account (same structure)
│
└── Shared Services Account
    └── AWS SSO (Identity Provider = Azure AD ClientB)
```

**Best Practices appliquées** :
- Référence : [[06-Zettelkasten/Securite-AWS-IAM|Sécurité AWS IAM Best Practices]]
- MFA obligatoire pour tous utilisateurs humains
- Pas de long-term credentials (access keys), uniquement temporary via SSO
- Service roles pour applications (pas de user credentials hardcodés)
- Secrets dans AWS Secrets Manager (rotation automatique 90j)
- IAM policies restrictives (deny by default)

---

## 📈 Monitoring & Observabilité

### Stack monitoring

**Métriques** :
- CloudWatch Metrics (CPU, RAM, IOPS, network)
- CloudWatch Custom Metrics (app-specific)
- Dashboards Grafana (visualisation)

**Logs** :
- CloudWatch Logs (centralisé)
- Retention policy : 90 jours (audit logs 7 ans S3 Glacier)
- Logs Insights pour recherches

**Tracing** :
- AWS X-Ray (distributed tracing)
- Latence end-to-end API calls

**Alertes** :
- CloudWatch Alarms → SNS → PagerDuty
- Seuils : CPU > 80%, Latency > 500ms, Error rate > 1%

---

## 💰 Optimisation Coûts

### Stratégie FinOps

**Phase migration** (6 mois) :
- On-Demand instances (flexibilité)
- Coûts élevés acceptés temporairement

**Post-migration** (stabilisation) :
- **Reserved Instances** : 70% instances (engagement 1 an, -40% coût)
- **Savings Plans** : Compute Savings Plans (flexibility)
- **Spot Instances** : 20% workloads non-critiques (batch, dev)
- **Right-sizing** : Analyser CloudWatch, ajuster instance types

**Outils** :
- AWS Cost Explorer (analyse coûts)
- AWS Budgets (alertes dépassements)
- Cost Anomaly Detection (alertes anomalies ML)
- Trusted Advisor (recommandations optimisation)

**Target** :
- **An 1** : Coûts 80% on-premise (phase migration, redundancy)
- **An 2** : Coûts 65% on-premise (optimisation, Reserved Instances)
- **An 3** : Coûts 60% on-premise (fully optimized)

---

## ✅ Critères de validation

### Par application

- [ ] Tests fonctionnels (scenarios end-to-end)
- [ ] Tests performances (load testing, baseline comparison)
- [ ] Tests sécurité (scan vulnérabilités, pen testing)
- [ ] Tests disaster recovery (backup/restore, failover)
- [ ] Documentation runbooks (monitoring, incidents, scaling)
- [ ] Formation équipe ops ClientB

### Par vague

- [ ] Zero incident majeur (downtime non planifié)
- [ ] Performance = baseline on-premise (±10%)
- [ ] Monitoring opérationnel (alarmes, dashboards)
- [ ] Rollback plan testé et validé
- [ ] Go/No-Go comité validé avant vague suivante

---

## 📚 Références

- AWS 6R Migration Strategy : [[06-Zettelkasten/Strategie-Migration-Cloud]]
- AWS IAM Best Practices : [[06-Zettelkasten/Securite-AWS-IAM]]
- Architecture Diagrams : https://lucid.app/clientb-aws-arch
- Terraform Modules : https://github.com/agency/clientb-aws-infra
- Runbooks : https://notion.so/clientb-runbooks
