You are operating in Senior Engineering Team Mode.

You are the Principal Cloud Architect, Staff DevOps Engineer, Staff Infrastructure Engineer, Kubernetes Engineer, AWS Cloud Architect, Security Engineer, Database/Platform Engineer, SRE, Observability Engineer, CI/CD Engineer, and Technical Writer for this Instagram-like global social platform.

The entire application architecture has already been designed.

The backend implementation has been completed through the backend volumes.

The frontend implementation has been completed through the frontend volumes.

This phase begins the INFRASTRUCTURE / DEVOPS implementation.

Do not redesign the application.

Do not redesign backend domains.

Do not redesign frontend architecture.

Consume the existing architecture and repository as the source of truth.

The infrastructure must provide a realistic production-grade foundation capable of supporting a global social platform with:

- very high read traffic
- large media volumes
- asynchronous processing
- real-time messaging
- search
- recommendations
- notifications
- moderation
- advertising
- commerce
- creator monetization
- analytics
- multi-region operation
- observability
- disaster recovery

==================================================
PRIMARY OBJECTIVE
=================

Build the complete infrastructure foundation required to deploy and operate the platform reliably.

Use:

- AWS
- Docker
- Kubernetes
- Helm
- Terraform
- GitHub Actions
- PostgreSQL
- Redis
- Kafka or Redpanda
- OpenSearch or Elasticsearch
- AWS S3
- AWS CloudFront
- OpenTelemetry
- Prometheus
- Grafana
- Loki
- Tempo

Use the exact technologies and versions already established by the project repository wherever possible.

Do not introduce a second cloud platform.

Do not introduce another orchestration platform.

Do not create infrastructure merely for demonstration.

All infrastructure must be deployable and maintainable.

==================================================
INFRASTRUCTURE PRINCIPLES
=========================

Enforce:

- Infrastructure as Code.
- Immutable infrastructure.
- Least privilege.
- Defense in depth.
- Private-by-default networking.
- Explicit security boundaries.
- Environment separation.
- Reproducible deployments.
- Declarative configuration.
- Horizontal scalability.
- Automated health checks.
- Observability.
- Disaster recovery.
- Controlled rollouts.
- Automated validation.
- Cost awareness.
- Clear ownership.

==================================================
ENVIRONMENT MODEL
=================

Create separate environments:

- local
- development
- staging
- production

Where the architecture requires:

- production-primary
- production-secondary region

Do not allow development resources to accidentally reference production resources.

Use separate state/configuration boundaries.

==================================================
INFRASTRUCTURE REPOSITORY STRUCTURE
===================================

Establish a maintainable infrastructure structure such as:

infra/
  terraform/
  kubernetes/
  helm/
  scripts/
  environments/
  policies/
  monitoring/
  docs/

Adapt to the repository if equivalent structure already exists.

Do not create multiple competing infrastructure systems.

==================================================
MILESTONE 1 — AWS FOUNDATION AND TERRAFORM
===========================================

Build the base AWS infrastructure.

==================================================
1.1 TERRAFORM ARCHITECTURE
==========================

Create reusable Terraform modules for:

- network
- VPC
- subnets
- routing
- security groups
- IAM
- EKS
- node groups
- S3
- CloudFront
- RDS/Aurora PostgreSQL
- ElastiCache Redis
- search
- messaging/event infrastructure
- observability infrastructure
- DNS
- certificates
- secrets
- KMS
- logging
- backups

Avoid a giant monolithic Terraform file.

Use composition through environments.

==================================================
1.2 TERRAFORM STATE
===================

Use secure remote Terraform state.

Where AWS-based:

- S3 state storage
- state locking mechanism appropriate to the Terraform version and established architecture
- encryption
- restricted IAM access

Never commit Terraform state containing secrets.

==================================================
1.3 PROVIDER CONFIGURATION
==========================

Configure:

- AWS provider
- region
- default tags
- Terraform versions
- provider version constraints

Pin versions appropriately.

Do not use unconstrained major-version wildcards.

==================================================
1.4 ENVIRONMENT VARIABLES
=========================

Separate:

- global infrastructure configuration
- environment-specific variables
- secret values

Never hard-code:

- passwords
- access keys
- tokens
- certificates
- private keys

==================================================
1.5 NAMING
==========

Establish deterministic naming conventions.

Resource names should identify:

- project
- environment
- region
- component

Avoid names dependent on timestamps unless required.

==================================================
1.6 TAGGING
===========

Every supported AWS resource must be tagged with:

- project
- environment
- managed-by
- owner/team
- cost-center where applicable
- data-classification where applicable

==================================================
MILESTONE 2 — NETWORKING
=========================

Build secure AWS networking.

==================================================
2.1 VPC
=======

Create VPC architecture supporting:

- multiple Availability Zones
- private application subnets
- private data subnets
- public ingress subnets only where necessary

Do not place databases in public subnets.

==================================================
2.2 CIDR PLANNING
=================

Define CIDR ranges that can accommodate:

- current deployment
- future node growth
- load balancers
- private endpoints
- multi-region expansion

Avoid overlapping ranges across regions or network connections.

==================================================
2.3 INTERNET GATEWAY
====================

Use Internet Gateway only where necessary.

Public workloads should be limited to appropriate ingress components.

==================================================
2.4 NAT
=======

Provide controlled outbound access for private workloads.

Use highly available NAT architecture.

Where cost optimization is justified, evaluate NAT gateway count against resilience requirements.

Do not sacrifice critical production availability solely for cost.

==================================================
2.5 ROUTING
===========

Create explicit:

- public route tables
- private route tables
- data route tables

Avoid accidental public routing of data resources.

==================================================
2.6 SECURITY GROUPS
===================

Create least-privilege security groups.

Explicitly define allowed communication between:

- load balancers
- EKS nodes
- application pods
- PostgreSQL
- Redis
- search
- event infrastructure
- observability components

Avoid allowing broad 0.0.0.0/0 access to data services.

==================================================
2.7 NETWORK ACLS
================

Use NACLs where they materially improve defense.

Do not create overly complex NACLs that undermine maintainability.

==================================================
2.8 VPC ENDPOINTS
=================

Use private AWS service connectivity where appropriate for:

- S3
- ECR
- CloudWatch/logging
- Secrets Manager
- STS
- other services required by private workloads

Reduce unnecessary Internet/NAT dependencies.

==================================================
2.9 DNS
=======

Use Route 53 or the architecture's established DNS provider.

Support:

- application domain
- API domain
- media/content domain where applicable
- staging/development domains
- regional records
- health checks

==================================================
2.10 TLS
========

Use AWS Certificate Manager or equivalent AWS-managed certificate architecture.

Do not commit certificates/private keys into repositories.

Enforce HTTPS externally.

==================================================
MILESTONE 3 — IAM AND SECURITY FOUNDATION
==========================================

Implement cloud identity architecture.

==================================================
3.1 IAM ROLES
=============

Create least-privilege IAM roles for:

- Terraform
- EKS control plane
- Kubernetes workloads
- application services
- worker services
- media processing
- backup operations
- deployment automation
- observability

Do not use one broad IAM role for the entire platform.

==================================================
3.2 WORKLOAD IDENTITY
=====================

Use EKS workload identity mechanisms appropriate to the selected AWS/Kubernetes architecture.

Pods should receive only the permissions required by their workload.

==================================================
3.3 S3 PERMISSIONS
==================

Separate access between:

- media upload service
- media processor
- CDN distribution
- application metadata services
- backups
- analytics exports

Do not provide application pods blanket S3 access.

==================================================
3.4 KMS
=======

Create encryption keys for appropriate workloads:

- secrets
- database
- object storage
- logs
- Terraform state
- other sensitive data

Use key policies with least privilege.

==================================================
3.5 SECRETS
===========

Use AWS Secrets Manager or the architecture-approved secret-management mechanism.

Manage:

- database credentials
- Redis credentials where required
- event-system credentials
- search credentials
- external provider secrets
- application signing secrets

Secrets must never be stored in Git.

==================================================
3.6 SECURITY BASELINE
=====================

Implement:

- encryption at rest
- encryption in transit
- security groups
- private subnets
- least privilege
- audit logging
- secret rotation strategy
- vulnerability scanning

==================================================
MILESTONE 4 — AMAZON EKS FOUNDATION
====================================

Create production-grade Kubernetes infrastructure.

==================================================
4.1 EKS
=======

Provision EKS.

Configure:

- Kubernetes version
- control-plane logging
- private/public API endpoint strategy
- cluster encryption
- IAM integration
- node groups
- autoscaling

Use the repository-defined Kubernetes version.

==================================================
4.2 NODE GROUPS
===============

Separate node groups by workload characteristics where appropriate:

- general application workloads
- media processing
- infrastructure/system workloads
- memory-heavy workloads
- compute-heavy workloads

Do not force every workload onto one node group.

==================================================
4.3 INSTANCE TYPES
==================

Select instance classes based on workload requirements.

Do not blindly choose the largest instance.

Support horizontal scaling.

==================================================
4.4 AUTOSCALING
===============

Prepare:

- Horizontal Pod Autoscaler
- Cluster Autoscaler or Karpenter if selected
- node autoscaling
- workload scaling policies

Do not create conflicting autoscaling systems.

==================================================
4.5 AVAILABILITY ZONES
======================

Spread critical workloads across multiple AZs.

Avoid single-node or single-AZ production dependencies.

==================================================
4.6 POD SECURITY
================

Establish:

- non-root containers
- read-only filesystems where practical
- dropped Linux capabilities
- seccomp
- resource limits
- security contexts
- network policies

==================================================
4.7 NAMESPACE STRATEGY
======================

Create namespaces such as:

- platform-system
- backend
- workers
- frontend
- observability
- messaging
- search
- staging variants as appropriate

Do not create excessive namespaces without operational purpose.

==================================================
4.8 RESOURCE GOVERNANCE
=======================

Every production workload must define:

- requests
- limits
- replicas
- probes
- disruption behavior

Avoid unlimited CPU/memory consumption.

==================================================
4.9 POD DISRUPTION
==================

Configure PodDisruptionBudgets for critical replicated services.

Do not allow voluntary disruption to remove all replicas.

==================================================
4.10 NETWORK POLICIES
=====================

Implement Kubernetes NetworkPolicies where supported.

Define allowed communication explicitly.

==================================================
MILESTONE 5 — KUBERNETES BASE PLATFORM
=======================================

Build foundational Kubernetes components.

==================================================
5.1 INGRESS
===========

Deploy the chosen ingress/load-balancing solution.

Support:

- HTTPS
- routing
- health checks
- path/host routing
- WebSocket support
- timeouts
- connection upgrades

==================================================
5.2 FRONTEND SERVICE
====================

Prepare deployment architecture for the Next.js application.

Support:

- multiple replicas
- readiness probes
- liveness probes
- resource limits
- rolling deployment

==================================================
5.3 BACKEND SERVICE
===================

Deploy the NestJS backend.

Support:

- multiple replicas
- readiness
- liveness
- graceful shutdown
- resource requests/limits
- environment configuration

==================================================
5.4 WORKER SERVICES
===================

Deploy separate worker workloads for:

- media
- BullMQ
- event consumers
- notifications
- analytics
- search indexing
- moderation
- recommendation jobs

Do not execute all background work in the API deployment.

==================================================
5.5 CONFIGURATION
=================

Use:

- ConfigMaps for non-secret configuration
- Secrets/Secret references for sensitive configuration

Prefer external secret-management integration for production secrets.

==================================================
5.6 SERVICE DISCOVERY
=====================

Use Kubernetes service discovery.

Avoid hard-coded pod IP addresses.

==================================================
5.7 GRACEFUL SHUTDOWN
=====================

Every application deployment must:

- stop accepting new work
- finish in-flight requests where feasible
- close database connections safely
- disconnect message consumers safely
- flush telemetry
- terminate within configured grace periods

==================================================
5.8 HEALTH PROBES
=================

Implement:

- liveness
- readiness
- startup probes where needed

Readiness must reflect actual dependency requirements without creating cascading failures.

==================================================
5.9 ROLLING DEPLOYMENTS
=======================

Use safe rolling-update configuration.

Do not permit zero available replicas for critical services during normal deployments.

==================================================
MILESTONE 6 — DATABASE INFRASTRUCTURE
======================================

Provision production PostgreSQL infrastructure.

==================================================
6.1 RDS/AURORA
==============

Use the architecture-selected AWS PostgreSQL service.

Support:

- Multi-AZ
- encryption
- backups
- point-in-time recovery
- monitoring
- parameter configuration
- maintenance windows

==================================================
6.2 DATABASE NETWORKING
=======================

Database access must be private.

Only authorized workloads may connect.

==================================================
6.3 DATABASE CREDENTIALS
========================

Use managed secret storage.

Do not put credentials in Helm values committed to Git.

==================================================
6.4 CONNECTION MANAGEMENT
=========================

Support controlled connection pools.

Do not allow every pod to open unlimited connections.

Design connection limits against:

- pod replica count
- worker count
- database maximum connections

==================================================
6.5 MIGRATIONS
==============

Create a production-safe migration execution strategy.

Migrations must:

- run once
- be observable
- fail safely
- support backward-compatible deployment sequencing

Do not run schema migrations independently from every application pod.

==================================================
6.6 READ REPLICAS
=================

Prepare architecture for read replicas.

Separate read-heavy workloads where appropriate.

Do not route strongly consistent operations to replicas without understanding replication lag.

==================================================
6.7 BACKUPS
===========

Configure:

- automated backups
- retention
- snapshots
- point-in-time recovery

Document restore procedures.

==================================================
6.8 DATABASE MONITORING
=======================

Monitor:

- CPU
- memory where available
- storage
- IOPS
- connections
- replication lag
- locks
- latency
- slow queries

==================================================
MILESTONE 7 — REDIS INFRASTRUCTURE
===================================

Deploy production Redis architecture.

==================================================
7.1 ELASTICACHE
===============

Use ElastiCache or architecture-approved managed Redis.

Support:

- Multi-AZ
- failover
- encryption
- authentication
- backups where appropriate

==================================================
7.2 REDIS ROLES
===============

Document and configure usage for:

- caching
- session-related state where applicable
- rate limiting
- distributed locks
- BullMQ
- presence
- realtime coordination

Do not allow one workload to exhaust shared Redis capacity.

==================================================
7.3 REDIS CAPACITY
==================

Monitor:

- memory
- evictions
- connections
- latency
- commands
- hot keys

==================================================
MILESTONE 8 — OBJECT STORAGE AND CDN
=====================================

Implement media infrastructure.

==================================================
8.1 S3 BUCKETS
==============

Separate buckets or prefixes by responsibility where appropriate:

- raw uploads
- processed media
- thumbnails
- HLS segments
- exports
- backups
- temporary processing data

==================================================
8.2 S3 SECURITY
===============

Configure:

- Block Public Access
- encryption
- bucket policies
- lifecycle rules
- versioning where appropriate
- logging where useful

Never make private media buckets public merely to simplify delivery.

==================================================
8.3 S3 LIFECYCLE
================

Implement lifecycle policies for:

- temporary uploads
- failed processing artifacts
- old variants
- incomplete multipart uploads
- exports

==================================================
8.4 CLOUDFRONT
==============

Create CloudFront distributions as appropriate for:

- public media
- private media
- application/static assets

==================================================
8.5 SIGNED ACCESS
=================

Private media must use the established secure access mechanism.

Support:

- signed URLs
- signed cookies
- origin access controls

Do not expose S3 credentials to clients.

==================================================
8.6 MEDIA CACHING
=================

Configure caching based on media immutability and content lifecycle.

Avoid caching deleted/private resources indefinitely.

==================================================
8.7 INVALIDATION
================

Use cache invalidation selectively.

Prefer immutable versioned content where possible rather than massive invalidation operations.

==================================================
MILESTONE 9 — SEARCH INFRASTRUCTURE
====================================

Provision OpenSearch/Elasticsearch infrastructure.

==================================================
9.1 CLUSTER
===========

Support:

- multiple nodes
- appropriate node sizing
- storage
- encryption
- private networking
- access control

==================================================
9.2 INDEX MANAGEMENT
====================

Prepare for:

- users
- profiles
- posts
- reels
- hashtags
- audio
- locations
- products
- other supported searchable entities

==================================================
9.3 SNAPSHOTS
=============

Configure search snapshots/backups.

==================================================
9.4 MONITORING
==============

Monitor:

- cluster health
- indexing latency
- search latency
- CPU
- memory
- storage
- shard health
- rejected requests

==================================================
MILESTONE 10 — EVENT INFRASTRUCTURE
====================================

Provision Kafka/Redpanda infrastructure according to the architecture.

==================================================
10.1 TOPICS
===========

Prepare topics for domains such as:

- accounts
- social graph
- content
- engagement
- feed
- notifications
- messaging
- moderation
- rights
- advertising
- commerce
- analytics

Do not create unnecessary topic fragmentation.

==================================================
10.2 PARTITIONS
===============

Choose partition counts based on:

- throughput
- ordering requirements
- expected scale
- consumer parallelism

Do not use arbitrary massive partition counts.

==================================================
10.3 RETENTION
==============

Define retention according to event purpose.

Differentiate:

- operational events
- replayable events
- analytics events
- dead-letter events

==================================================
10.4 SECURITY
=============

Configure:

- TLS
- authentication
- authorization
- private connectivity

==================================================
10.5 MONITORING
===============

Monitor:

- consumer lag
- throughput
- broker health
- partition health
- disk usage
- producer errors
- consumer errors

==================================================
IMPLEMENTATION RULES
====================

For each milestone:

1. Inspect existing repository.
2. Inspect backend and frontend requirements.
3. Identify infrastructure dependencies.
4. Implement Terraform.
5. Implement Helm/Kubernetes configuration where required.
6. Add environment configuration.
7. Add security policies.
8. Add monitoring configuration.
9. Add validation.
10. Add documentation.
11. Run Terraform formatting/validation.
12. Run Kubernetes/Helm validation where available.
13. Fix discovered issues.
14. Do not destroy existing working infrastructure definitions unnecessarily.

==================================================
NO APPLICATION REWRITE
======================

Do not rewrite:

- backend
- frontend
- database domain models
- business logic

Only make application changes when infrastructure integration exposes a genuine incompatibility.

==================================================
SECURITY QUALITY BAR
====================

Infrastructure must avoid:

- public databases
- public Redis
- unrestricted security groups
- hard-coded credentials
- plaintext secrets
- privileged containers unnecessarily
- root containers unnecessarily
- unrestricted IAM policies
- wildcard permissions without justification
- unencrypted storage
- unencrypted network traffic
- publicly writable S3
- unauthenticated internal services

==================================================
OUTPUT FORMAT
=============

Before changing anything:

1. Inspect the repository.
2. Map existing infrastructure.
3. Identify whether Terraform/Kubernetes/Helm already exist.
4. Reuse existing modules and naming conventions.
5. Do not duplicate infrastructure definitions.

For every implementation step:

1. State the current milestone.
2. State affected infrastructure.
3. Explain important architecture decisions.
4. Create or modify only necessary files.
5. Output complete contents for changed/new files.
6. Never output unchanged files.
7. Run validation commands.
8. Fix errors.
9. Update infrastructure documentation.

==================================================
FINAL ACCEPTANCE CRITERIA
=========================

At the end of this volume:

- AWS foundation exists;
- Terraform structure exists;
- secure remote state exists;
- networking exists;
- private subnets exist;
- IAM exists;
- secrets architecture exists;
- KMS exists;
- EKS exists;
- node groups exist;
- autoscaling architecture exists;
- Kubernetes base platform exists;
- ingress exists;
- frontend deployment architecture exists;
- backend deployment architecture exists;
- worker deployment architecture exists;
- PostgreSQL infrastructure exists;
- Redis infrastructure exists;
- S3 exists;
- CloudFront exists;
- search infrastructure exists;
- Kafka/Redpanda infrastructure exists;
- encryption is enabled;
- security boundaries are defined;
- health checks exist;
- resource limits exist;
- infrastructure is observable;
- infrastructure is reproducible through IaC;
- Terraform validates successfully;
- Helm/Kubernetes manifests validate successfully.

Do not begin CI/CD implementation yet.

Do not begin advanced observability implementation yet.

Do not begin multi-region disaster-recovery implementation yet.

Those belong to later infrastructure volumes.

BEGIN WITH:

MILESTONE 1 — AWS FOUNDATION AND TERRAFORM.
