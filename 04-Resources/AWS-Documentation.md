---
type: resource
title: "AWS Documentation & Guides"
category: "Cloud"
tags: [resource, aws, cloud, documentation]
created: 2024-09-15
last_accessed: 2024-10-18
---

# ☁️ AWS Documentation & Guides

> Ressources de référence AWS utilisées régulièrement pour projets clients et montée en compétences cloud.

---

## 📚 Documentation officielle

### Core Services

**Compute**
- [EC2 User Guide](https://docs.aws.amazon.com/ec2/) - Compute instances, AMI, Auto Scaling
- [Lambda Developer Guide](https://docs.aws.amazon.com/lambda/) - Serverless functions
- [ECS Documentation](https://docs.aws.amazon.com/ecs/) - Container orchestration

**Storage**
- [S3 User Guide](https://docs.aws.amazon.com/s3/) - Object storage
- [EBS Documentation](https://docs.aws.amazon.com/ebs/) - Block storage
- [EFS User Guide](https://docs.aws.amazon.com/efs/) - File storage

**Database**
- [RDS User Guide](https://docs.aws.amazon.com/rds/) - Managed relational databases
- [DynamoDB Developer Guide](https://docs.aws.amazon.com/dynamodb/) - NoSQL database
- [ElastiCache User Guide](https://docs.aws.amazon.com/elasticache/) - In-memory caching

**Networking**
- [VPC User Guide](https://docs.aws.amazon.com/vpc/) - Virtual Private Cloud
- [Route 53 Developer Guide](https://docs.aws.amazon.com/route53/) - DNS service
- [CloudFront Developer Guide](https://docs.aws.amazon.com/cloudfront/) - CDN

**Security**
- [IAM User Guide](https://docs.aws.amazon.com/iam/) - Identity & Access Management ⭐
- [AWS Security Best Practices](https://aws.amazon.com/architecture/security-identity-compliance/)
- [Secrets Manager User Guide](https://docs.aws.amazon.com/secretsmanager/)

---

## 🏗️ Architecture & Best Practices

### Frameworks officiels

**AWS Well-Architected Framework** ⭐⭐⭐
- [Framework Overview](https://aws.amazon.com/architecture/well-architected/)
- [6 Pillars](https://aws.amazon.com/architecture/well-architected/#The_6_pillars_of_the_Framework):
  1. Operational Excellence
  2. Security
  3. Reliability
  4. Performance Efficiency
  5. Cost Optimization
  6. Sustainability
- **Utilisation** : Audit ClientB, architecture validation

**AWS Cloud Adoption Framework (CAF)** ⭐⭐
- [CAF Overview](https://aws.amazon.com/cloud-adoption-framework/)
- 6 perspectives : Business, People, Governance, Platform, Security, Operations
- **Utilisation** : Stratégie migration ClientB

**Migration Strategies (6R)** ⭐⭐⭐
- [Migration Hub](https://aws.amazon.com/migration-hub/)
- Framework 6R : Rehost, Replatform, Refactor, Repurchase, Retire, Retain
- **Utilisation** : Plan migration ClientB (60% Rehost, 30% Replatform, 10% Refactor)
- **Note Zettelkasten** : [[06-Zettelkasten/Strategie-Migration-Cloud]]

---

## 🎓 Guides d'apprentissage

### Certification AWS Solutions Architect

**Ressources officielles**
- [AWS Certified Solutions Architect - Associate](https://aws.amazon.com/certification/certified-solutions-architect-associate/)
- [Exam Guide](https://d1.awsstatic.com/training-and-certification/docs-sa-assoc/AWS-Certified-Solutions-Architect-Associate_Exam-Guide.pdf)
- [Sample Questions](https://d1.awsstatic.com/training-and-certification/docs-sa-assoc/AWS-Certified-Solutions-Architect-Associate_Sample-Questions.pdf)

**Préparation personnelle**
- [ ] Lire tous les whitepapers clés (en cours)
- [ ] AWS Skill Builder (training gratuit)
- [ ] Practice exams (planifié Nov 2024)
- [ ] Certification visée : Janvier 2025

**Whitepapers essentiels** ⭐
1. [AWS Security Best Practices](https://docs.aws.amazon.com/whitepapers/latest/aws-overview-security-processes/aws-overview-security-processes.pdf)
2. [AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/wellarchitected-framework.pdf)
3. [AWS Migration Strategies](https://docs.aws.amazon.com/prescriptive-guidance/latest/migration-strategies/welcome.html)
4. [Cost Optimization Pillar](https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/welcome.html)

---

## 🔧 Outils & CLI

### AWS CLI
- [CLI Command Reference](https://awscli.amazonaws.com/v2/documentation/api/latest/index.html)
- Installation : `pip install awscli`
- Configuration : `aws configure`

**Commandes fréquentes** :
```bash
# EC2
aws ec2 describe-instances
aws ec2 start-instances --instance-ids i-xxx
aws ec2 stop-instances --instance-ids i-xxx

# S3
aws s3 ls
aws s3 cp file.txt s3://bucket-name/
aws s3 sync ./local s3://bucket-name/

# IAM
aws iam list-users
aws iam list-roles
aws iam get-user

# CloudFormation
aws cloudformation describe-stacks
aws cloudformation create-stack --stack-name xxx --template-body file://template.yml
```

### Infrastructure as Code

**AWS CloudFormation**
- [User Guide](https://docs.aws.amazon.com/cloudformation/)
- Templates YAML/JSON pour infrastructure versionnée

**AWS CDK** (Cloud Development Kit)
- [Developer Guide](https://docs.aws.amazon.com/cdk/)
- Infrastructure as Code en TypeScript/Python/Java
- **Intérêt** : Type safety, refactoring, tests unitaires infra

---

## 📊 Monitoring & Observability

### CloudWatch
- [CloudWatch User Guide](https://docs.aws.amazon.com/cloudwatch/)
- Logs, metrics, alarms, dashboards
- **Utilisation** : Monitoring applications ClientB post-migration

### AWS X-Ray
- [Developer Guide](https://docs.aws.amazon.com/xray/)
- Distributed tracing pour microservices

---

## 💰 Cost Management

### AWS Cost Explorer
- [User Guide](https://docs.aws.amazon.com/cost-management/latest/userguide/ce-what-is.html)
- Analyse coûts et utilisation

### FinOps Resources
- [AWS Cloud Economics Center](https://aws.amazon.com/economics/)
- [Cost Optimization Best Practices](https://aws.amazon.com/pricing/cost-optimization/)
- **Prochaine étape** : Approfondir FinOps pour ClientB (optimisation post-migration)

---

## 🔗 Projets utilisant ces ressources

### Projets actifs
- [[02-Projects/ClientB-Migration-Cloud-AWS/_index]] - Migration 40 apps
  - Framework 6R ✅
  - IAM best practices ✅
  - Well-Architected review (planifié post-migration)

### Notes Zettelkasten associées
- [[06-Zettelkasten/Securite-AWS-IAM]] - IAM best practices
- [[06-Zettelkasten/Strategie-Migration-Cloud]] - Framework 6R

### Area technique liée
- [[03-Areas/Technical-Skills/_index]] - Cloud & Infrastructure

---

## 📅 Historique d'utilisation

### Oct 2024
- IAM User Guide : Résolution blocage MFA service roles ClientB
- Migration Strategies : Application framework 6R ClientB
- VPC User Guide : Validation architecture réseau ClientB

### Sept 2024
- Well-Architected Framework : Audit ClientB
- CAF : Stratégie migration ClientB
- EC2 + RDS : Architecture compute/database ClientB

### Août 2024
- CloudFront : Setup CDN ClientA (Next.js + Vercel)
- S3 : Storage static assets ClientA

---

## 🎯 Prochaines lectures

- [ ] AWS Step Functions (orchestration serverless)
- [ ] AWS CDK Workshop (IaC moderne)
- [ ] FinOps on AWS (optimisation coûts)
- [ ] AWS Landing Zone (multi-account architecture)
