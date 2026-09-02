You are operating in Senior Engineering Team Mode.

You are the Principal Cloud Architect, Staff DevOps Engineer, Staff Infrastructure Engineer, Kubernetes Engineer, AWS Solutions Architect, SRE, Database Architect, Networking Engineer, Security Engineer, Observability Engineer, Disaster Recovery Engineer, CI/CD Engineer, and Technical Writer for this Instagram-like global social platform.

The previous infrastructure volumes established:

- AWS foundation
- Terraform architecture
- remote Terraform state
- VPC and networking
- private/public subnet strategy
- IAM
- KMS
- secrets architecture
- EKS
- Kubernetes foundation
- Helm architecture
- frontend deployment
- backend deployment
- worker deployments
- ingress
- NetworkPolicies
- pod security
- autoscaling foundations
- PostgreSQL infrastructure
- Redis infrastructure
- S3
- CloudFront
- OpenSearch/Elasticsearch
- Kafka/Redpanda
- GitHub Actions
- ECR
- CI/CD
- image scanning
- OIDC
- OpenTelemetry
- Prometheus
- Grafana
- Loki
- Tempo
- alerting
- operational monitoring
- backup foundations
- resilience foundations
- WAF
- operational hardening

This volume moves the platform from a strong single-region production foundation toward global, highly available, observable, recoverable infrastructure.

Do not restart the infrastructure.

Do not replace working infrastructure architecture.

Do not regenerate unchanged files.

Do not invent another cloud provider.

Do not create duplicate deployment systems.

Do not move application business logic into Terraform or Kubernetes.

Use the existing repository and all previous architecture decisions as the source of truth.

==================================================
VOLUME 3 SCOPE
==============

Implement:

MILESTONE 16
Production security hardening, governance, compliance-oriented controls, and infrastructure policy enforcement.

MILESTONE 17
Multi-region AWS architecture and global traffic management.

MILESTONE 18
Cross-region data, media, event, cache, and search replication strategy.

MILESTONE 19
Disaster recovery, regional failover, backup restoration, and business-continuity automation.

MILESTONE 20
Final infrastructure integration, cost optimization, chaos validation, capacity planning, and production readiness.

==================================================
NON-NEGOTIABLE RULES
====================

Production-grade infrastructure only.

No pseudo-code.

No placeholder Terraform.

No placeholder Kubernetes manifests.

No fake disaster recovery.

No fake failover.

No fake monitoring.

No fake replication.

No TODOs.

No secrets in Git.

No hard-coded production credentials.

Every Terraform module must validate.

Every Helm chart must render.

Every Kubernetes manifest must validate.

Every IAM policy must be least privilege.

Every cross-region mechanism must have explicitly defined consistency semantics.

Do not claim active-active support unless the architecture actually implements it.

Do not claim zero-downtime failover unless it has been designed and validated.

Do not claim an RPO/RTO without evidence.

==================================================
MILESTONE 16 — SECURITY, GOVERNANCE, AND POLICY ENFORCEMENT
============================================================

Harden the entire AWS/Kubernetes platform.

==================================================
16.1 AWS ACCOUNT STRATEGY
=========================

Where the project's operational model supports it, define separation between:

- development
- staging
- production

Where appropriate, prepare for separate AWS accounts.

Do not place production and development workloads into the same security boundary unless explicitly justified.

Document account boundaries.

==================================================
16.2 ORGANIZATIONAL CONTROLS
============================

Where AWS Organizations is used, define:

- organizational units
- account boundaries
- security contacts
- centralized logging
- service-control policy strategy

Do not create unrestricted organization-wide policies.

==================================================
16.3 CLOUDTRAIL
===============

Enable organization/account-level API auditing as appropriate.

Capture:

- management events
- relevant data events
- authentication-related activity
- security-relevant activity

Send logs to protected destinations.

==================================================
16.4 CENTRALIZED AUDIT LOGGING
==============================

Create protected storage for:

- CloudTrail
- AWS Config
- VPC flow logs
- security findings
- infrastructure audit information

Use encryption and restrictive access.

Audit logs should not be mutable by ordinary application roles.

==================================================
16.5 AWS CONFIG
===============

Where used, define configuration rules for:

- public S3
- unrestricted security groups
- encryption
- IAM policy risks
- public databases
- public snapshots
- disabled logging
- missing tags
- unencrypted resources

==================================================
16.6 SECURITY HUB
=================

Where appropriate, integrate AWS Security Hub or the architecture-approved security findings aggregation mechanism.

Expose actionable infrastructure findings.

==================================================
16.7 GUARDDUTY
==============

Where appropriate, enable AWS threat detection.

Create operational routing for critical findings.

==================================================
16.8 VULNERABILITY MANAGEMENT
=============================

Integrate infrastructure vulnerability scanning.

Scan:

- container images
- operating system packages
- Terraform
- Kubernetes manifests
- Helm charts
- dependencies

Critical findings must have defined remediation workflows.

==================================================
16.9 POLICY AS CODE
===================

Introduce policy-as-code where appropriate.

Possible tools:

- OPA
- Gatekeeper
- Kyverno
- Terraform policy tooling

Select one coherent approach.

Enforce policies such as:

- no privileged containers without exception
- no public data stores
- no missing resource limits
- no unapproved images
- no host networking without exception
- required labels
- required probes
- required security contexts

Do not deploy multiple overlapping policy engines without architectural justification.

==================================================
16.10 KUBERNETES RBAC
=====================

Audit Kubernetes RBAC.

Ensure:

- developers cannot access production secrets unnecessarily
- workloads use dedicated ServiceAccounts
- cluster-admin is tightly restricted
- CI/CD has only deployment permissions required
- read-only operational access is separated from mutation access

==================================================
16.11 SECRET ACCESS POLICY
==========================

Audit every secret consumer.

Define:

- who can read
- which workload can read
- how secrets rotate
- how access is revoked

==================================================
16.12 KEY ROTATION
==================

Ensure KMS and secret rotation policies are documented.

Rotation must be compatible with:

- database
- application
- external providers
- CI/CD
- Kubernetes workloads

==================================================
16.13 NETWORK SECURITY
======================

Audit:

- security groups
- NetworkPolicies
- NACLs
- WAF rules
- ingress
- egress
- VPC endpoints

Remove unnecessary open paths.

==================================================
16.14 EGRESS CONTROL
====================

Where practical, control outbound traffic from workloads.

Allow external access only where application dependencies require it.

Document approved destinations for sensitive services.

==================================================
16.15 WAF
=========

Harden AWS WAF rules.

Consider protection for:

- common web attacks
- bot abuse
- request floods
- suspicious patterns
- rate anomalies

Do not create rules that accidentally block normal platform traffic.

Use monitoring before enforcing aggressive rules.

==================================================
16.16 DDOS PROTECTION
=====================

Use AWS-native DDoS protections appropriate to the architecture.

Document:

- standard protections
- advanced protections where justified
- escalation procedure

Do not claim DDoS immunity.

==================================================
16.17 CONTAINER SECURITY
========================

Enforce:

- non-root
- read-only filesystem where feasible
- dropped capabilities
- seccomp
- no privilege escalation
- approved base images
- image scanning
- image signing where supported

==================================================
16.18 SUPPLY-CHAIN SECURITY
===========================

Harden CI/CD against supply-chain attacks.

Implement where practical:

- lockfiles
- dependency integrity
- SBOM generation
- image provenance
- image signing
- verification before production deployment

==================================================
16.19 SBOM
==========

Generate software bills of materials for production images.

Store them in an appropriate artifact repository.

==================================================
16.20 INFRASTRUCTURE AUDIT
==========================

Create automated checks preventing:

- public S3
- public RDS
- open Redis
- open Elasticsearch/OpenSearch
- unrestricted Kubernetes APIs
- wildcard IAM permissions without approved exception
- secrets committed to repository

==================================================
MILESTONE 17 — MULTI-REGION AWS ARCHITECTURE
=============================================

Extend the architecture to multiple AWS regions.

Use the regions selected by the project's architecture.

Do not hard-code region names when the project requires configurable regional deployment.

==================================================
17.1 REGION MODEL
=================

Define:

- primary region
- secondary region

Optionally prepare additional regions.

The architecture must explicitly distinguish:

- primary
- secondary
- read-only/standby
- active-active

Do not label a region active-active unless the application supports it.

==================================================
17.2 REGIONAL TERRAFORM
=======================

Refactor Terraform composition so the same modules can create:

- region A
- region B

without copying entire infrastructure stacks.

Use reusable module composition.

==================================================
17.3 REGIONAL STATE
===================

Maintain clear Terraform state boundaries between regions/environments.

Do not allow accidental cross-region destruction.

==================================================
17.4 REGIONAL NETWORKING
========================

Create equivalent VPC structures in each region.

Ensure CIDR ranges do not conflict.

Prepare:

- VPC peering
  or
- Transit Gateway
  or
- other appropriate inter-region connectivity

Only when actually required.

==================================================
17.5 INTER-REGION CONNECTIVITY
==============================

Define secure communication between regions for:

- replication
- event transport
- control operations
- application failover

Do not route all application traffic cross-region unnecessarily.

==================================================
17.6 REGIONAL EKS
=================

Create independent EKS clusters per region when the global architecture requires it.

Each region must operate independently enough to survive loss of the other region.

==================================================
17.7 REGIONAL APPLICATION STACK
===============================

Deploy in each region:

- frontend
- backend
- workers
- realtime
- event consumers
- required supporting services

Do not create a single-region control dependency that prevents a regional failover.

==================================================
17.8 GLOBAL TRAFFIC MANAGEMENT
==============================

Use appropriate AWS services for global routing, such as:

- Route 53
- AWS Global Accelerator
- CloudFront

Select a coherent combination.

==================================================
17.9 DNS FAILOVER
=================

Support health-aware DNS or global routing.

Possible states:

- primary healthy
- primary degraded
- primary unavailable
- secondary active

Failover must be explicit and observable.

==================================================
17.10 HEALTH CHECKS
===================

Global health checks must verify meaningful service health.

Do not consider an HTTP 200 from a superficial endpoint enough to prove that the entire region is healthy.

Use separate:

- edge health
- API health
- dependency health
- application readiness

==================================================
17.11 REGIONAL TRAFFIC POLICY
=============================

Define routing strategy:

- latency-based
- geolocation
- weighted
- failover

Choose based on the application's data consistency requirements.

==================================================
17.12 WEBSOCKET GLOBAL ROUTING
==============================

Ensure realtime traffic can survive regional routing.

Account for:

- long-lived connections
- reconnect behavior
- regional affinity
- session state
- global routing

Do not assume existing WebSocket connections automatically migrate during failover.

Clients must reconnect safely.

==================================================
17.13 CDN GLOBAL DELIVERY
=========================

CloudFront should provide global media/static delivery.

Ensure origins are appropriately regionalized where architecture requires.

==================================================
17.14 GLOBAL TLS
================

Use regional/global certificate management appropriate to:

- CloudFront
- Application Load Balancers
- regional endpoints

==================================================
17.15 GLOBAL OBSERVABILITY
==========================

Dashboards must distinguish:

- region
- environment
- service
- workload

Do not mix regional metrics into ambiguous totals.

==================================================
17.16 GLOBAL INCIDENT RESPONSE
==============================

Create procedures for:

- regional degradation
- regional failover
- traffic restoration
- secondary promotion
- rollback to primary

==================================================
MILESTONE 18 — CROSS-REGION DATA AND SERVICE REPLICATION
=========================================================

Implement realistic replication architecture.

Do not assume all data can or should be synchronously replicated.

==================================================
18.1 DATA CLASSIFICATION
========================

Classify platform data:

Tier 0:
Security/identity/privacy-critical data.

Tier 1:
Operational source-of-truth transactional data.

Tier 2:
Derived content/discovery data.

Tier 3:
Caches and ephemeral state.

Tier 4:
Analytics/derived reporting data.

Define recovery expectations for each.

==================================================
18.2 POSTGRESQL REPLICATION
===========================

Implement the architecture appropriate for the selected PostgreSQL service.

Possible model:

- primary region
- cross-region read replica/standby
- controlled promotion during disaster

Do not implement unsupported multi-primary behavior.

==================================================
18.3 DATABASE CONSISTENCY
=========================

Explicitly document:

- strong consistency
- read-after-write
- eventual consistency

for regional access.

Privacy-sensitive operations must not rely on stale replicas where that could expose protected content.

==================================================
18.4 DATABASE FAILOVER
======================

Create documented and automatable promotion procedures.

Validate:

- replication health
- lag
- DNS update
- application connection recovery
- schema compatibility

==================================================
18.5 REDIS MULTI-REGION
=======================

Determine which Redis state is:

- disposable cache
- regional ephemeral state
- session-critical
- coordination-critical

Do not replicate disposable cache state unnecessarily.

Loss of Redis should not make the application unrecoverable when PostgreSQL is source of truth.

==================================================
18.6 REALTIME PRESENCE
======================

Presence may remain region-local/ephemeral where architecture permits.

Document this behavior.

Do not create unnecessary strong global consistency for ephemeral presence.

==================================================
18.7 OBJECT STORAGE REPLICATION
===============================

Configure cross-region S3 replication where required.

Classify:

- raw media
- processed media
- HLS segments
- thumbnails
- exports
- critical artifacts

Avoid replicating disposable temporary content unnecessarily.

==================================================
18.8 MEDIA FAILOVER
===================

Ensure media URLs remain resolvable after region failure.

CloudFront/origin architecture must have a valid secondary origin strategy where required.

==================================================
18.9 SEARCH REPLICATION
=======================

Search is derived data.

Define recovery through:

- snapshots
- replicated data
- complete reindexing from source of truth

Do not make search the authoritative data store.

==================================================
18.10 KAFKA/REDPANDA CROSS-REGION
=================================

Define the event replication strategy.

Consider:

- MirrorMaker-style replication
- managed cross-region streaming
- replicated topics

Choose a coherent approach.

Explicitly define:

- source region
- destination region
- topic mapping
- duplicate handling
- ordering
- failure recovery

==================================================
18.11 EVENT REPLAY
==================

The architecture must support rebuilding derived systems after failure.

Potential replays:

- search indexes
- recommendation state
- analytics
- notification derivatives
- feed caches

==================================================
18.12 BULLMQ MULTI-REGION
=========================

Define which queues are:

- region-local
- globally coordinated
- failover capable

Do not allow the same job to execute twice merely because two regions become active unless idempotency is guaranteed.

==================================================
18.13 S3 EXPORT REPLICATION
===========================

Ensure privacy/data exports remain recoverable without exposing them publicly.

==================================================
18.14 SECRETS MULTI-REGION
==========================

Replicate/coordinate secrets securely across regions.

Do not manually copy secrets into files.

==================================================
18.15 KMS MULTI-REGION
======================

Use appropriate multi-region KMS architecture where required.

Ensure application workloads can decrypt only authorized resources.

==================================================
18.16 CONFIGURATION REPLICATION
===============================

Feature flags and dynamic configuration must have explicit consistency semantics.

Security-critical configuration changes must not silently lag between regions.

==================================================
18.17 DATA RECOVERY MATRIX
==========================

Create a matrix:

Data type
→ source of truth
→ replication
→ RPO
→ RTO
→ failover behavior
→ restoration process

==================================================
MILESTONE 19 — DISASTER RECOVERY AND BUSINESS CONTINUITY
=========================================================

Turn backups and replication into tested recovery workflows.

==================================================
19.1 DISASTER SCENARIOS
=======================

Prepare recovery for:

- pod failure
- node failure
- AZ failure
- EKS failure
- Redis failure
- search failure
- Kafka failure
- database failure
- region failure
- accidental configuration deletion
- compromised deployment
- corrupted derived data

==================================================
19.2 RECOVERY RUNBOOKS
======================

Create runbooks for each scenario.

Each runbook must include:

- detection
- decision criteria
- prerequisites
- commands/tools
- validation
- rollback
- communication

Do not create vague one-page descriptions.

==================================================
19.3 DATABASE RESTORE TEST
==========================

Automate or document an actual restore validation process.

Validate:

- backup availability
- restore
- migration compatibility
- critical-table integrity
- application connectivity
- read/write functionality

==================================================
19.4 POINT-IN-TIME RECOVERY
===========================

Prepare and document PITR.

Include operational verification.

==================================================
19.5 REGION FAILOVER
====================

Create a controlled failover workflow.

Potential sequence:

1. Detect regional failure.
2. Confirm failure scope.
3. Freeze unsafe writes if required.
4. Validate secondary readiness.
5. Promote required stateful services.
6. Redirect global traffic.
7. Reconnect applications.
8. Validate critical paths.
9. Monitor.
10. Restore normal operations later.

Do not automate destructive actions without safe guards.

==================================================
19.6 FAILBACK
=============

Create a controlled failback procedure.

Do not simply switch traffic back.

Verify:

- data synchronization
- replication direction
- schema state
- queue state
- application state
- media availability

==================================================
19.7 READ-ONLY DEGRADATION
==========================

Where technically feasible, define graceful degradation for regional emergencies.

Potentially preserve:

- public content browsing
- profile viewing
- search
- cached media

while restricting unsafe write operations.

Do not present this as a guarantee unless actually implemented.

==================================================
19.8 INCIDENT COMMAND
=====================

Document operational roles:

- incident commander
- infrastructure lead
- application lead
- database lead
- communications lead

==================================================
19.9 RECOVERY VALIDATION
========================

After recovery verify:

- authentication
- feed
- content
- messaging
- notifications
- uploads
- search
- moderation
- advertising
- commerce
- creator analytics

Prioritize critical user paths.

==================================================
19.10 BACKUP RETENTION
======================

Define:

- daily
- weekly
- long-term

retention where required.

Apply lifecycle policies.

==================================================
19.11 BACKUP ENCRYPTION
=======================

All protected backups must use encryption.

==================================================
19.12 BACKUP ACCESS CONTROL
===========================

Backup restoration must require elevated authorization.

Do not allow ordinary application pods to restore production databases.

==================================================
19.13 IMMUTABLE BACKUPS
=======================

Where security architecture requires it, implement protected/immutable backup strategies.

==================================================
19.14 DISASTER RECOVERY DRILLS
==============================

Create automated or documented exercises for:

- database restore
- region failover
- search rebuild
- event replay
- media recovery

Record results and identified weaknesses.

==================================================
19.15 RPO/RTO DOCUMENTATION
===========================

Do not invent a single global number.

Document targets by subsystem.

==================================================
19.16 DATA INTEGRITY
====================

After recovery, perform reconciliation checks for:

- transactional data
- event streams
- media metadata
- search
- analytics
- queues

==================================================
MILESTONE 20 — FINAL INFRASTRUCTURE ENGINEERING AND PRODUCTION READINESS
=========================================================================

Perform a complete repository-wide infrastructure audit.

==================================================
20.1 TERRAFORM AUDIT
====================

Review:

- module composition
- variable definitions
- outputs
- dependencies
- state boundaries
- provider versions
- IAM
- encryption
- tags
- lifecycle
- drift risk

Run validation.

==================================================
20.2 TERRAFORM FORMAT
=====================

Ensure all Terraform is formatted consistently.

==================================================
20.3 TERRAFORM PLAN REVIEW
==========================

Run plans for applicable environments.

Identify:

- unexpected resource replacement
- destructive changes
- security drift
- accidental public exposure

Never blindly apply a plan containing unexpected destruction.

==================================================
20.4 HELM AUDIT
===============

Review:

- values
- templates
- names
- labels
- selectors
- probes
- resources
- security contexts
- RBAC
- ingress
- secrets

==================================================
20.5 KUBERNETES AUDIT
=====================

Verify:

- deployments
- services
- ingress
- ConfigMaps
- external secrets
- ServiceAccounts
- RBAC
- NetworkPolicies
- HPA
- PDB
- priority classes
- topology spread
- node selectors
- tolerations

==================================================
20.6 CI/CD AUDIT
================

Review:

- permissions
- OIDC
- environment protection
- secrets
- image immutability
- scans
- approvals
- rollback

==================================================
20.7 SUPPLY-CHAIN AUDIT
=======================

Verify:

- SBOM
- image provenance
- dependency lockfiles
- signed artifacts
- trusted registries
- pinned GitHub Actions where appropriate

==================================================
20.8 COST AUDIT
===============

Review major cost drivers:

- EKS
- EC2
- NAT gateways
- RDS
- Redis
- search
- Kafka
- S3
- CloudFront
- observability
- cross-region transfer

Do not reduce resilience just to reduce cost.

==================================================
20.9 RESOURCE RIGHTSIZING
=========================

Use actual metrics to identify:

- oversized nodes
- oversized databases
- low-utilization workloads
- unnecessary replicas
- excessive log retention
- unnecessary cross-region replication

Do not make destructive rightsizing decisions solely from static assumptions.

==================================================
20.10 CAPACITY PLANNING
=======================

Create capacity models for:

- API requests
- WebSocket connections
- feed generation
- search
- database connections
- Redis memory
- event throughput
- queue depth
- media processing
- object storage
- CDN bandwidth

Define scaling thresholds.

==================================================
20.11 TRAFFIC SCENARIOS
=======================

Model:

- normal traffic
- peak traffic
- viral content
- launch/event spike
- regional traffic surge

Ensure the infrastructure can scale without overwhelming the database.

==================================================
20.12 HOTSPOT ANALYSIS
======================

Identify potential hotspots:

- Redis hot keys
- database hot rows
- Kafka partitions
- queue bottlenecks
- API endpoints
- media origins
- WAF rules

==================================================
20.13 CHAOS ENGINEERING
=======================

Prepare controlled failure tests.

Test:

- kill API pod
- kill worker pod
- terminate node
- lose AZ
- block Redis
- delay Kafka
- make search unavailable
- increase database latency

Verify graceful degradation.

==================================================
20.14 CHAOS SAFETY
==================

Chaos tests must:

- run only in controlled environments
- have abort procedures
- have monitoring
- avoid accidental production damage
- record outcomes

==================================================
20.15 SECURITY INCIDENT RESPONSE
================================

Create infrastructure procedures for:

- leaked credential
- compromised container
- suspicious IAM activity
- malicious deployment
- exposed bucket
- WAF attack
- compromised CI runner

==================================================
20.16 SECRET COMPROMISE
=======================

Define emergency workflow:

1. Detect.
2. Disable/rotate credential.
3. Revoke access.
4. Validate workloads.
5. Investigate.
6. Restore service.
7. Audit affected resources.

==================================================
20.17 CERTIFICATE EXPIRATION
============================

Automate certificate renewal where possible.

Alert before expiration.

==================================================
20.18 DOMAIN/DNS FAILURE
========================

Document recovery for:

- DNS misconfiguration
- certificate mismatch
- routing failure
- health-check failure

==================================================
20.19 OBSERVABILITY FINAL AUDIT
===============================

Verify all major services emit:

- logs
- metrics
- traces
- health information

Dashboards must distinguish:

- region
- environment
- service
- severity

==================================================
20.20 ALERT FATIGUE AUDIT
=========================

Review:

- duplicate alerts
- noisy alerts
- missing severity
- missing ownership
- missing runbooks

Every critical alert should have an actionable response path.

==================================================
20.21 SLA/SLO AUDIT
===================

Review actual measured performance against defined targets.

Do not claim compliance without evidence.

==================================================
20.22 DOCUMENTATION FINALIZATION
================================

Create/update:

- infrastructure architecture
- AWS architecture
- region map
- Terraform module map
- Kubernetes architecture
- Helm architecture
- networking
- IAM
- secrets
- database
- Redis
- search
- Kafka
- S3
- CloudFront
- CI/CD
- observability
- security
- disaster recovery
- backup
- failover
- incident response
- cost governance
- capacity planning
- chaos testing

==================================================
20.23 INFRASTRUCTURE PROJECT INDEX
==================================

Create a definitive infrastructure index:

Component
→ Terraform module
→ AWS resource
→ Kubernetes resource
→ Helm chart
→ Environment
→ Region
→ Dependencies
→ Security boundary
→ Monitoring
→ Backup
→ Recovery procedure

==================================================
20.24 RELEASE READINESS CHECKLIST
=================================

Create a checklist covering:

Infrastructure:

- Terraform valid
- state secure
- networking secure
- IAM least privilege
- encryption enabled

Kubernetes:

- probes
- resources
- PDB
- NetworkPolicies
- RBAC
- autoscaling

Applications:

- frontend deployed
- backend deployed
- workers deployed
- migrations controlled

Data:

- PostgreSQL backup
- Redis recovery
- search recovery
- Kafka recovery
- S3 recovery

Security:

- WAF
- vulnerability scanning
- secret scanning
- SBOM
- image provenance

Observability:

- logs
- metrics
- traces
- alerts
- dashboards

Global:

- secondary region
- global routing
- failover
- replication
- disaster recovery

==================================================
20.25 PRODUCTION GO/NO-GO
=========================

Define explicit conditions for:

GO:

- validation passes
- security findings acceptable
- backups verified
- failover tested
- monitoring active
- rollback available
- critical paths validated

NO-GO:

- unresolved critical security issue
- unvalidated destructive migration
- missing database recovery
- missing production monitoring
- broken failover
- invalid infrastructure
- uncontrolled secrets
- unbounded resource consumption

==================================================
20.26 FINAL VALIDATION
======================

Run every applicable validation available in the repository.

Terraform:

- fmt
- validate
- plan

Helm:

- lint
- template

Kubernetes:

- schema validation
- manifest validation

Docker:

- build
- scan

Security:

- dependency scan
- secret scan
- IaC scan
- container scan

CI:

- workflow validation

Operations:

- smoke tests
- deployment checks
- recovery checks

Fix actual failures before declaring the infrastructure complete.

==================================================
INFRASTRUCTURE DESIGN PRINCIPLES
================================

Throughout all milestones:

Never hide complexity by deleting required infrastructure.

Never create unnecessary complexity merely to make the architecture appear enterprise-grade.

Prefer managed AWS services for stateful systems when already established.

Prefer immutable deployment artifacts.

Prefer automation over manual repetition.

Prefer explicit failure modes over hidden assumptions.

Prefer reversible deployments.

Prefer observability by default.

Prefer least privilege.

Prefer data-source-of-truth clarity.

Prefer eventual consistency where it is safe and materially improves scalability.

Use stronger consistency where privacy/security/business correctness requires it.

==================================================
FINAL OUTPUT RULES
==================

Before modifying anything:

1. Inspect the repository.
2. Identify previous infrastructure volumes.
3. Reuse existing Terraform modules.
4. Reuse existing Helm charts.
5. Reuse existing Kubernetes conventions.
6. Reuse existing CI/CD workflows.
7. Reuse existing observability.
8. Identify actual gaps.

For every milestone:

1. State the milestone.
2. State affected infrastructure.
3. Inspect current implementation.
4. Explain important architecture decisions.
5. Create/modify only required files.
6. Output complete contents for every changed/new file.
7. Never output unchanged files.
8. Run validation.
9. Fix failures.
10. Update documentation.
11. Keep the repository deployable.

Do not merely provide architecture suggestions.

Actually implement the infrastructure.

==================================================
FINAL ACCEPTANCE CRITERIA
=========================

At the end of this volume:

SECURITY

- cloud governance exists;
- audit logging exists;
- configuration compliance exists;
- threat detection exists where selected;
- policy-as-code exists;
- RBAC is hardened;
- network boundaries are enforced;
- supply-chain security is improved;
- secrets are protected;
- image provenance is addressed.

MULTI-REGION

- primary region exists;
- secondary region exists;
- regional Terraform composition exists;
- regional networking exists;
- regional EKS exists;
- application workloads can operate regionally;
- global routing exists;
- health-aware failover exists;
- global observability exists.

DATA

- PostgreSQL replication/recovery strategy exists;
- Redis role classification exists;
- S3 replication exists where required;
- search recovery exists;
- Kafka/Redpanda replication/recovery exists;
- event replay exists;
- configuration consistency is documented;
- recovery matrix exists.

DISASTER RECOVERY

- backup restore is validated;
- PITR is documented;
- region failover is defined;
- failback is defined;
- recovery runbooks exist;
- incident roles exist;
- integrity checks exist;
- RPO/RTO targets are documented and evidence-based;
- disaster exercises are defined.

FINAL ENGINEERING

- Terraform is valid;
- Helm is valid;
- Kubernetes manifests are valid;
- CI/CD is secure;
- costs are governed;
- capacity is modeled;
- chaos testing is available;
- incident response is documented;
- observability is complete;
- infrastructure documentation is complete;
- production go/no-go criteria exist.

==================================================
CRITICAL SEQUENCING RULE
========================

This is the final major infrastructure volume.

Do not begin a new application implementation phase.

After completing this volume, the project should have a complete:

Master Architecture
→ Backend
→ Frontend
→ Infrastructure
→ CI/CD
→ Observability
→ Security
→ Multi-Region
→ Disaster Recovery

implementation pipeline.

The infrastructure must consume, rather than redefine, the application contracts established by the architecture, backend, and frontend phases.

BEGIN WITH:

MILESTONE 16 — PRODUCTION SECURITY HARDENING, GOVERNANCE, COMPLIANCE-ORIENTED CONTROLS, AND INFRASTRUCTURE POLICY ENFORCEMENT.
