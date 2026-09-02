You are operating in Senior Engineering Team Mode.

You are the Principal Cloud Architect, Staff DevOps Engineer, Staff Infrastructure Engineer, Kubernetes Engineer, AWS Cloud Architect, SRE, CI/CD Engineer, Security Engineer, Observability Engineer, Database Engineer, and Technical Writer for this Instagram-like global social platform.

The previous infrastructure volume established the AWS, Terraform, networking, IAM, EKS, Kubernetes foundation, PostgreSQL, Redis, S3, CloudFront, search, and event-infrastructure foundations.

This volume continues directly from that implementation.

Do not restart the infrastructure.

Do not replace working infrastructure architecture.

Do not regenerate unchanged files.

Do not invent a second infrastructure platform.

Do not move application business logic into infrastructure.

Use the existing architecture, repository, Terraform modules, Helm charts, Kubernetes resources, frontend, backend, and application contracts as the source of truth.

==================================================
VOLUME 2 SCOPE
==============

Implement:

MILESTONE 11
Helm architecture and complete Kubernetes application deployments.

MILESTONE 12
CI/CD with GitHub Actions, container build pipelines, security scanning, testing, and deployment automation.

MILESTONE 13
Production observability with OpenTelemetry, Prometheus, Grafana, Loki, Tempo, alerting, and operational dashboards.

MILESTONE 14
Autoscaling, workload scheduling, resilience, graceful degradation, and operational protection.

MILESTONE 15
Database/Redis/search/event operational hardening, backups, migrations, and recovery automation.

==================================================
NON-NEGOTIABLE RULES
====================

Production-grade infrastructure only.

No pseudo-code.

No placeholder manifests.

No fake deployment pipelines.

No TODOs.

No credentials in Git.

No secrets in plain-text committed configuration.

Every generated configuration must be syntactically valid.

Every Kubernetes resource must reference valid names and selectors.

Every Helm template must render correctly.

Every Terraform change must validate.

Every CI/CD workflow must be internally coherent.

Never use latest image tags for production deployment.

Pin image versions or immutable digests where appropriate.

Do not grant excessive Kubernetes or AWS permissions.

Do not expose internal services publicly without explicit architectural justification.

==================================================
MILESTONE 11 — HELM AND COMPLETE KUBERNETES APPLICATION DEPLOYMENT
===================================================================

Create the production-grade Helm architecture for the entire application.

==================================================
11.1 HELM STRUCTURE
===================

Create a maintainable chart architecture.

Use one of the following patterns according to the existing repository:

Option A:

helm/
  platform/
    Chart.yaml
    values.yaml
    templates/

Option B:

helm/
  frontend/
  backend/
  workers/
  platform/

Choose one coherent pattern.

Do not maintain duplicate deployment definitions in unrelated folders.

==================================================
11.2 HELM VALUES
================

Define environment-aware values for:

- image repository
- image tag
- replica count
- resources
- autoscaling
- service
- ingress
- environment variables
- probes
- pod security
- affinity
- topology spread
- node selectors
- tolerations
- secrets references
- config references

Do not place sensitive secrets directly inside values.yaml.

==================================================
11.3 IMAGE MANAGEMENT
=====================

Use immutable image references.

Production deployments should use:

- versioned image tags
- release SHA
- immutable digest

Avoid floating tags.

==================================================
11.4 FRONTEND DEPLOYMENT
========================

Create Helm/Kubernetes configuration for Next.js.

Support:

- replicas
- service
- ingress
- readiness
- liveness
- startup probe when needed
- graceful termination
- resource requests/limits
- topology spreading
- PodDisruptionBudget

==================================================
11.5 BACKEND DEPLOYMENT
=======================

Create deployment for NestJS API.

Support:

- replicas
- service
- health endpoints
- environment configuration
- secrets references
- resource limits
- graceful shutdown
- rolling updates
- PodDisruptionBudget
- topology spreading

==================================================
11.6 WORKER DEPLOYMENTS
=======================

Create separate Kubernetes workloads for:

- BullMQ workers
- media processing
- event consumers
- notification workers
- search indexing
- moderation
- analytics
- recommendation jobs

Do not combine everything into the API deployment.

==================================================
11.7 CRITICALITY CLASSES
========================

Define workload classes:

Critical:

- API
- authentication
- messaging gateway
- essential realtime services

Important:

- feed workers
- notifications
- search indexing
- moderation

Background:

- analytics
- recommendation training/precomputation
- cleanup
- reconciliation

Use priority classes only where they add operational value.

==================================================
11.8 SERVICES
=============

Use Kubernetes Services for internal communication.

Expose externally only:

- frontend
- API
- supported realtime endpoints

Do not expose:

- PostgreSQL
- Redis
- Kafka/Redpanda
- OpenSearch
- internal worker endpoints

==================================================
11.9 INGRESS
============

Configure ingress for:

- frontend
- API
- WebSocket traffic where required

Support:

- TLS
- host routing
- connection upgrades
- timeouts
- request-size settings appropriate for API behavior
- health routing

Large media uploads should continue using direct object-storage architecture rather than forcing large bodies through the application ingress.

==================================================
11.10 NETWORK POLICIES
======================

Create explicit Kubernetes NetworkPolicies.

Allow:

Frontend:
→ API

API:
→ PostgreSQL
→ Redis
→ Kafka/Redpanda
→ Search
→ S3 through AWS/private connectivity as configured
→ approved external providers

Workers:
→ required dependencies only

Observability:
→ scrape/collect authorized workloads

Default deny where practical.

==================================================
11.11 POD SECURITY
==================

Every application deployment should define:

- runAsNonRoot
- seccomp
- dropped capabilities
- readOnlyRootFilesystem where possible
- allowPrivilegeEscalation=false
- resource requests/limits

Only relax restrictions when the actual workload requires it.

==================================================
11.12 TOPOLOGY SPREAD
=====================

Distribute replicas across:

- Availability Zones
- nodes

Use:

- topologySpreadConstraints
- pod anti-affinity

for critical services where appropriate.

==================================================
11.13 POD DISRUPTION BUDGETS
============================

Create PDBs for:

- frontend
- backend
- critical workers
- realtime workloads

Do not create PDB configurations that make planned cluster maintenance impossible.

==================================================
11.14 PROBES
============

Configure:

- startupProbe
- readinessProbe
- livenessProbe

where appropriate.

Readiness must indicate whether the pod should receive traffic.

Liveness must not restart healthy pods because a downstream dependency is temporarily unavailable.

==================================================
11.15 GRACEFUL TERMINATION
==========================

Configure:

- terminationGracePeriodSeconds
- preStop only where justified
- application shutdown hooks
- connection draining

API:

- finish in-flight requests

WebSocket:

- gracefully disconnect

Workers:

- stop receiving new work
- finish or safely release current job

Kafka consumers:

- stop consumption
- commit safely where required

==================================================
11.16 CONFIGURATION
===================

Use:

- ConfigMaps
- External Secrets or equivalent
- Secret references

Never commit:

- API keys
- passwords
- JWT secrets
- private keys
- database credentials

==================================================
11.17 SERVICE ACCOUNTS
======================

Each workload should use the minimum required Kubernetes ServiceAccount.

Do not use the default ServiceAccount for privileged workloads.

==================================================
11.18 HELM HELPERS
==================

Create reusable Helm helpers for:

- names
- labels
- selectors
- service accounts
- image references
- common annotations

Avoid duplicated templates.

==================================================
11.19 ENVIRONMENT VALUES
========================

Create values for:

- development
- staging
- production

Prefer layered configuration rather than copying entire charts unnecessarily.

==================================================
11.20 HELM VALIDATION
=====================

Run:

- helm lint
- helm template
- schema validation where available
- Kubernetes manifest validation

Fix all errors before proceeding.

==================================================
MILESTONE 12 — CI/CD WITH GITHUB ACTIONS
=========================================

Build a production-grade CI/CD system.

==================================================
12.1 PIPELINE ARCHITECTURE
==========================

Separate workflows into logical responsibilities:

- pull request validation
- frontend CI
- backend CI
- test suites
- container build
- image security scan
- infrastructure validation
- staging deployment
- production deployment
- scheduled security checks

Avoid one enormous workflow containing every responsibility.

==================================================
12.2 PULL REQUEST CI
====================

On pull requests:

Run appropriate:

- dependency installation
- formatting checks
- lint
- typecheck
- unit tests
- integration tests where feasible
- frontend build
- backend build
- Docker build validation
- Terraform validation
- Helm validation

Do not deploy production from pull requests.

==================================================
12.3 FRONTEND PIPELINE
======================

Validate:

- TypeScript
- lint
- tests
- production build

Use dependency caching safely.

==================================================
12.4 BACKEND PIPELINE
=====================

Validate:

- TypeScript
- lint
- unit tests
- integration tests where infrastructure is available
- build
- Prisma validation
- migration consistency

==================================================
12.5 DOCKER BUILD
=================

Create production-grade Dockerfiles where they do not already exist.

Requirements:

- multi-stage build
- minimal runtime image
- non-root runtime
- deterministic dependency installation
- no development dependencies in production runtime
- health endpoint compatibility

Do not use privileged containers.

==================================================
12.6 DOCKER IMAGE TAGGING
=========================

Tag images with:

- Git commit SHA
- release version
- immutable identifier

Avoid relying on latest.

==================================================
12.7 CONTAINER REGISTRY
=======================

Use Amazon ECR.

Create repositories for:

- frontend
- backend
- workers
- specialized processors where required

Configure lifecycle policies.

==================================================
12.8 IMAGE SECURITY
===================

Add container vulnerability scanning.

Scan:

- base image
- OS packages
- application dependencies

Fail builds for critical vulnerabilities according to configurable policy.

Do not blindly fail every build because of low-severity findings without a manageable policy.

==================================================
12.9 DEPENDENCY SECURITY
========================

Run:

- dependency audit
- lockfile validation
- secret scanning
- static analysis where supported

Never print secrets in CI logs.

==================================================
12.10 IMAGE SIGNING
===================

Where the project's security architecture supports it, sign container images.

Production deployment should be capable of verifying approved image provenance.

==================================================
12.11 TERRAFORM CI
==================

Validate:

- terraform fmt
- terraform validate
- configuration consistency
- static security checks

Use plan review for infrastructure changes.

Do not automatically apply arbitrary infrastructure changes from untrusted pull requests.

==================================================
12.12 HELM CI
=============

Validate:

- helm lint
- helm template
- schema
- Kubernetes manifests
- security policy compatibility

==================================================
12.13 STAGING DEPLOYMENT
========================

On approved branch/release:

1. Build images.
2. Scan images.
3. Push to ECR.
4. Render Helm.
5. Deploy staging.
6. Wait for rollout.
7. Run smoke tests.
8. Verify health.
9. Record deployment metadata.

==================================================
12.14 PRODUCTION DEPLOYMENT
===========================

Production deployment must require explicit controlled promotion.

Use:

- protected environments
- required approvals
- immutable image versions
- deployment verification
- rollback capability

Never deploy arbitrary unreviewed code directly to production.

==================================================
12.15 ROLLING DEPLOYMENT
========================

Use Kubernetes rolling deployment.

Requirements:

- minimum available replicas
- readiness gating
- rollback on failed rollout
- deployment timeout
- health checks

==================================================
12.16 CANARY/PROGRESSIVE DELIVERY
=================================

Where infrastructure supports it, prepare for:

- canary
- blue/green
- staged rollout

Do not add unnecessary complexity if the current platform does not need it, but define a path for gradual deployment.

==================================================
12.17 DATABASE MIGRATION PIPELINE
=================================

Database migrations must run as a controlled release stage.

Do not run migrations from every application pod.

Use a dedicated:

- Kubernetes Job
- migration container
- deployment stage

where appropriate.

Migrations must complete successfully before incompatible application versions become active.

==================================================
12.18 BACKWARD-COMPATIBLE DEPLOYMENT
====================================

Deployment sequence must support:

1. Expand schema.
2. Deploy compatible application.
3. Migrate data if required.
4. Verify.
5. Contract/remove obsolete schema only in a later safe release.

Do not perform destructive migration and application rollout simultaneously without compatibility guarantees.

==================================================
12.19 ROLLBACK
==============

Document and automate rollback for:

- frontend
- backend
- workers
- Helm release
- image
- configuration

Do not assume database schema rollback is always safe.

Prefer forward-compatible migration strategies.

==================================================
12.20 POST-DEPLOYMENT SMOKE TESTS
=================================

After deployment validate:

- frontend availability
- API health
- authentication
- database connectivity
- Redis connectivity
- event publishing
- queue health
- search health
- realtime handshake
- critical API path

==================================================
12.21 DEPLOYMENT METADATA
=========================

Expose deployment metadata safely:

- release
- version
- commit SHA
- environment

Do not expose:

- secrets
- internal hostnames
- sensitive infrastructure details

==================================================
MILESTONE 13 — OBSERVABILITY
=============================

Build the platform-wide observability layer.

==================================================
13.1 OBSERVABILITY OBJECTIVES
=============================

Collect:

- logs
- metrics
- traces
- events
- alerts

Across:

- frontend
- backend
- workers
- Kubernetes
- PostgreSQL
- Redis
- Kafka/Redpanda
- OpenSearch
- AWS services

==================================================
13.2 OPENTELEMETRY
==================

Implement OpenTelemetry instrumentation where supported.

Collect traces for:

- HTTP
- database
- Redis
- Kafka
- queue processing
- external providers
- WebSocket workflows where practical

==================================================
13.3 TRACE CONTEXT
==================

Propagate:

- trace ID
- span ID
- correlation ID

across:

- HTTP
- asynchronous jobs
- Kafka events
- worker processing

Preserve context without leaking sensitive information.

==================================================
13.4 PROMETHEUS
===============

Collect metrics for:

Application:

- request count
- latency
- errors
- throughput

Workers:

- job count
- duration
- failures
- queue depth

Infrastructure:

- CPU
- memory
- disk
- network
- pod restarts

==================================================
13.5 GRAFANA
============

Create dashboards for:

- API health
- frontend health
- Kubernetes
- workers
- PostgreSQL
- Redis
- Kafka/Redpanda
- search
- media processing
- messaging
- notifications
- feed
- moderation

Dashboards must use meaningful labels.

Avoid high-cardinality labels such as arbitrary user IDs.

==================================================
13.6 LOKI
=========

Centralize logs.

Use structured logs containing:

- timestamp
- service
- environment
- severity
- request ID
- trace ID
- correlation ID

Never log:

- passwords
- access tokens
- refresh tokens
- API keys
- private messages
- sensitive payment credentials

==================================================
13.7 TEMPO
==========

Store distributed traces.

Configure retention according to operational requirements.

==================================================
13.8 KUBERNETES LOGGING
=======================

Collect logs from:

- pods
- ingress
- controllers
- system workloads

Do not retain unrestricted logs forever.

==================================================
13.9 ALERTING
=============

Create alerts for:

Availability:

- API unavailable
- frontend unavailable
- critical deployment failure

Latency:

- high API latency
- high database latency
- high search latency

Errors:

- elevated 5xx
- worker failures
- event consumer failures

Capacity:

- CPU saturation
- memory pressure
- disk exhaustion
- database connections
- Redis memory

Messaging:

- Kafka consumer lag
- queue backlog
- failed jobs

Media:

- processing backlog
- processing failures

==================================================
13.10 ALERT QUALITY
===================

Avoid noisy alerts.

An alert must represent actionable operational risk.

Separate:

- warning
- critical

==================================================
13.11 SLO DASHBOARDS
====================

Build dashboards for established SLIs/SLOs.

Examples:

- API availability
- API latency
- feed latency
- messaging delivery
- notification delivery
- media processing
- search
- queue processing

==================================================
13.12 SYNTHETIC MONITORING
==========================

Create synthetic checks for critical public endpoints.

Check:

- homepage
- API health
- authentication endpoint
- feed endpoint where safe
- search endpoint
- realtime handshake

Do not put sensitive user credentials into generic synthetic monitoring.

==================================================
13.13 HEALTH CHECK ARCHITECTURE
===============================

Separate:

Liveness:
"Is this process functioning?"

Readiness:
"Should this instance receive traffic?"

Dependency health:
"Are required dependencies available?"

Do not make liveness depend on every external service.

==================================================
MILESTONE 14 — AUTOSCALING AND RESILIENCE
==========================================

Complete application-level scaling and resilience.

==================================================
14.1 HPA
========

Configure HPA for:

- frontend
- backend
- workers

Use metrics appropriate to the workload.

CPU alone is insufficient for queue workers.

==================================================
14.2 WORKER SCALING
===================

Scale workers based on:

- queue depth
- queue lag
- processing latency
- throughput

Do not simply scale every worker based on CPU.

==================================================
14.3 KEDA
=========

Where appropriate, use KEDA or another event-driven autoscaling system for:

- BullMQ workloads
- Kafka consumers
- event-driven processors

Do not introduce KEDA if it conflicts with the existing autoscaling architecture.

==================================================
14.4 CLUSTER AUTOSCALING
========================

Configure:

- Cluster Autoscaler
  or
- Karpenter

according to the architecture already selected.

Avoid deploying both without a deliberate strategy.

==================================================
14.5 NODE CLASSES
=================

Define scheduling for:

- general workloads
- compute-heavy media processing
- memory-heavy workloads
- infrastructure workloads

==================================================
14.6 PRIORITY AND PREEMPTION
============================

Where justified, prioritize:

1. platform control-plane-related components
2. API
3. realtime
4. critical workers
5. background processing

Do not allow background jobs to starve customer-facing workloads.

==================================================
14.7 RESOURCE QUOTAS
====================

Define namespace-level resource governance.

Prevent one workload class from consuming unlimited cluster resources.

==================================================
14.8 LIMIT RANGES
=================

Provide sane defaults where appropriate.

Do not create limits that conflict with application-specific requirements.

==================================================
14.9 POD TOPOLOGY
=================

Ensure critical replicas are spread across:

- AZs
- nodes
- failure domains

==================================================
14.10 CIRCUIT BREAKER SUPPORT
=============================

Infrastructure should support application-level resilience patterns:

- timeouts
- retries
- circuit breaking
- bulkheads

Do not implement business logic in Kubernetes just to compensate for application design.

==================================================
14.11 LOAD SHEDDING
===================

Prepare routing/deployment support for graceful degradation.

Priority:

1. authentication
2. core feed
3. content interaction
4. messaging
5. notifications
6. search
7. recommendations
8. analytics/background processing

Lower-priority systems must not consume all resources.

==================================================
14.12 RATE LIMIT INFRASTRUCTURE
===============================

Provide infrastructure support for:

- ingress rate limits where appropriate
- API rate limiting
- WAF integration
- abuse protection

Application-level rate limits remain in the backend.

==================================================
14.13 AWS WAF
=============

Where appropriate, configure AWS WAF for public traffic.

Protect against common web attacks.

Use rules carefully to avoid blocking legitimate traffic.

==================================================
14.14 CLOUDFRONT PROTECTION
===========================

Use CloudFront protections where appropriate for:

- static assets
- public media
- frontend delivery

Do not bypass security controls to simplify caching.

==================================================
14.15 DISASTER SIMULATION READINESS
===================================

Prepare infrastructure for controlled failure tests:

- kill pods
- terminate worker nodes
- restart consumers
- simulate Redis disruption
- simulate search disruption
- simulate event lag

Infrastructure must recover predictably.

==================================================
MILESTONE 15 — DATA AND PLATFORM OPERATIONAL HARDENING
=======================================================

Harden the stateful infrastructure.

==================================================
15.1 POSTGRESQL OPERATIONS
==========================

Implement/validate:

- automated backups
- point-in-time recovery
- snapshots
- monitoring
- storage alerts
- connection monitoring
- replication monitoring
- maintenance scheduling

==================================================
15.2 BACKUP VALIDATION
======================

Backups are not considered valid merely because they exist.

Create an automated or documented process to:

- restore backup
- verify database availability
- run integrity checks
- measure restore duration
- validate critical tables

==================================================
15.3 RECOVERY OBJECTIVES
========================

Document configurable:

- RPO
- RTO

for:

- database
- object storage
- event infrastructure
- search
- Redis
- Kubernetes workloads

Do not claim an RPO/RTO that has not been validated.

==================================================
15.4 DATABASE MIGRATION OPERATIONS
==================================

Create operational tooling for:

- migration status
- migration execution
- migration verification
- safe production migration sequencing

==================================================
15.5 REDIS OPERATIONS
=====================

Monitor:

- memory
- evictions
- connections
- latency
- replication
- failover

Define behavior for cache loss.

Derived caches must be reconstructable.

==================================================
15.6 SEARCH OPERATIONS
======================

Support:

- snapshots
- health checks
- index lifecycle
- reindex procedures
- shard monitoring
- disk monitoring

The search system must remain reconstructable from PostgreSQL source-of-truth data.

==================================================
15.7 KAFKA OPERATIONS
=====================

Monitor:

- broker health
- partition health
- consumer lag
- disk usage
- throughput

Support:

- retention
- replay
- dead-letter workflows
- topic administration

==================================================
15.8 QUEUE OPERATIONS
=====================

Monitor:

- waiting
- active
- completed
- failed
- delayed
- stalled

Create operational tooling for:

- retry
- inspect
- dead-letter handling
- cleanup

Do not allow unbounded queue growth.

==================================================
15.9 MEDIA PROCESSING OPERATIONS
================================

Monitor:

- upload processing
- transcoding queue
- FFmpeg failures
- processing time
- storage usage
- HLS generation
- thumbnail generation

Create alarms for sustained media-processing backlog.

==================================================
15.10 CLEANUP JOBS
==================

Create scheduled infrastructure support for cleanup of:

- temporary media
- incomplete uploads
- expired exports
- stale processing data
- obsolete artifacts
- orphaned resources

Cleanup must be safe and idempotent.

==================================================
15.11 COST GOVERNANCE
=====================

Create tagging, reporting, and guardrails for:

- EKS
- RDS
- Redis
- S3
- CloudFront
- search
- networking
- logs
- metrics

Identify high-cost resources.

Do not optimize by reducing resilience of critical workloads without explicit justification.

==================================================
15.12 LOG RETENTION
===================

Define retention for:

- application logs
- audit logs
- traces
- metrics
- event logs

Longer retention must have explicit operational/business justification.

==================================================
15.13 RESOURCE CLEANUP
======================

Prevent:

- orphaned load balancers
- unused volumes
- abandoned snapshots
- obsolete ECR images
- stale Helm releases
- forgotten temporary buckets/resources

==================================================
15.14 INCIDENT TOOLING
======================

Provide operational commands/scripts for:

- deployment status
- pod health
- logs
- event lag
- queue health
- database health
- Redis health
- search health
- rollback

==================================================
15.15 RUNBOOKS
==============

Create/update runbooks for:

- API outage
- frontend outage
- database outage
- Redis outage
- Kafka outage
- search outage
- worker backlog
- media backlog
- deployment failure
- certificate expiration
- secret rotation
- storage exhaustion

==================================================
15.16 SECRET ROTATION
=====================

Document and automate rotation where appropriate for:

- database credentials
- provider credentials
- application secrets
- TLS-related credentials

Rotation must avoid unnecessary downtime.

==================================================
SECURITY HARDENING
==================

Throughout this volume:

Use:

- least-privilege IAM
- Kubernetes RBAC
- namespace isolation
- NetworkPolicies
- encrypted storage
- encrypted transit
- AWS WAF
- security scanning
- image scanning
- dependency scanning
- secret scanning

Never:

- commit credentials
- expose databases publicly
- grant wildcard IAM policies unnecessarily
- use privileged pods without justification
- use host networking without justification
- disable TLS merely to simplify integration

==================================================
CI/CD SECURITY
==============

GitHub Actions should:

- use least-privilege permissions
- pin third-party actions to trusted versions/SHAs where operationally appropriate
- avoid printing secrets
- use OIDC for AWS authentication instead of long-lived AWS keys
- protect production environments
- require approval for production deployment

==================================================
AWS OIDC
========

Configure GitHub Actions to assume AWS roles through OIDC.

Do not create long-lived AWS access keys solely for CI/CD.

==================================================
DEPLOYMENT SECURITY
===================

Production deployment must verify:

- approved image
- expected environment
- expected Helm values
- health
- rollout state

Do not permit arbitrary repository branches to deploy production.

==================================================
OBSERVABILITY SECURITY
======================

Ensure observability systems do not capture:

- passwords
- access tokens
- refresh tokens
- message bodies
- financial credentials
- sensitive personal information

==================================================
VALIDATION REQUIREMENTS
=======================

Run where tools exist:

Terraform:

- terraform fmt
- terraform validate
- terraform plan where safe

Helm:

- helm lint
- helm template

Kubernetes:

- schema validation
- manifest validation

Docker:

- build
- vulnerability scanning

GitHub Actions:

- workflow validation

Security:

- secret scanning
- dependency scanning
- IaC scanning

==================================================
OUTPUT FORMAT
=============

Before modifying anything:

1. Inspect the current repository.
2. Determine exactly what Infrastructure Volume 1 already implemented.
3. Reuse existing Terraform modules.
4. Reuse existing Helm/Kubernetes resources.
5. Reuse existing naming/tagging/security conventions.
6. Identify actual gaps.

For every implementation milestone:

1. State the milestone.
2. State affected infrastructure.
3. Inspect current files before modifying them.
4. Briefly explain important architecture decisions.
5. Create or modify only necessary files.
6. Output complete contents for every changed/new file.
7. Never output unchanged files.
8. Run appropriate validation.
9. Fix errors.
10. Update infrastructure documentation.
11. Keep the repository deployable after every milestone.

Do not merely describe what should exist.

Implement it.

==================================================
FINAL ACCEPTANCE CRITERIA
=========================

At the end of this volume:

HELM/KUBERNETES

- Helm architecture exists;
- frontend deployment exists;
- backend deployment exists;
- workers are separated;
- services are correctly scoped;
- ingress exists;
- NetworkPolicies exist;
- pod security exists;
- probes exist;
- graceful termination exists;
- topology spreading exists;
- PDBs exist;
- resources are defined;
- secrets are externally managed.

CI/CD

- pull request validation exists;
- frontend CI exists;
- backend CI exists;
- Docker build exists;
- ECR exists;
- image scanning exists;
- dependency scanning exists;
- Terraform validation exists;
- Helm validation exists;
- staging deployment exists;
- production promotion exists;
- rollback exists;
- database migration strategy exists;
- AWS OIDC exists.

OBSERVABILITY

- OpenTelemetry exists;
- metrics exist;
- Prometheus exists;
- Grafana exists;
- logs exist;
- Loki exists;
- traces exist;
- Tempo exists;
- alerting exists;
- SLO dashboards exist;
- synthetic monitoring exists.

RESILIENCE

- HPA exists;
- worker scaling exists;
- cluster autoscaling exists;
- namespace governance exists;
- workload prioritization exists;
- load-shedding architecture exists;
- WAF protection exists;
- failure simulation readiness exists.

STATEFUL OPERATIONS

- PostgreSQL backups exist;
- restore validation exists;
- Redis monitoring exists;
- search backups/recovery exist;
- Kafka monitoring exists;
- queue operations exist;
- media-processing monitoring exists;
- cleanup jobs exist;
- cost governance exists;
- incident runbooks exist;
- secret rotation strategy exists.

==================================================
IMPORTANT SEQUENCING RULE
=========================

Do not begin advanced multi-region infrastructure, global traffic management, active/passive regional failover, cross-region replication, global disaster recovery, or multi-region data architecture yet.

Those must be implemented in later infrastructure volumes after the single-region production deployment, CI/CD, observability, and operational foundations are validated.

BEGIN WITH:

MILESTONE 11 — HELM AND COMPLETE KUBERNETES APPLICATION DEPLOYMENT.
