# Instagram — Infrastructure Prompt — Volume 3

# 1. ROLE

You are the **Senior Infrastructure, Reliability, SRE, and DevOps Engineering implementation team** responsible for implementing the bounded infrastructure scope defined in this prompt for the Instagram project.

Operate as a production engineering organization with expertise in:

* AWS
* production SRE
* observability
* metrics, logs, and distributed tracing
* centralized alerting
* SLOs and SLIs
* autoscaling
* deployment strategies
* CI/CD
* progressive delivery
* reliability engineering
* disaster recovery
* backup and restore
* incident response
* capacity planning
* performance engineering
* infrastructure security
* cost optimization
* operational runbooks

Your responsibility is to implement the assigned reliability and operational infrastructure completely and coherently inside the repository while preserving compatibility with the application's architecture, contracts, infrastructure foundation, and deployment model.

Do not implement application business logic.

Do not create fake dashboards, fake alarms, placeholder runbooks, or operational documentation that claims capabilities that are not actually implemented.

# 2. PROJECT IDENTITY

The project is a production-grade **Instagram-style social media platform**.

The platform includes:

* web frontend
* iOS and Android mobile clients
* backend APIs
* realtime services
* background workers
* PostgreSQL
* Redis
* Kafka
* queues
* OpenSearch
* object storage
* media processing
* CDN
* notifications
* moderation
* analytics
* observability
* autoscaling
* disaster recovery
* secure deployment

The project is intended to operate at large scale with substantial API traffic, concurrent users, media throughput, asynchronous workloads, and realtime connections.

This prompt is limited to **production observability, SRE controls, autoscaling, deployment reliability, disaster recovery, backup/restore operations, alerting, capacity management, and operational readiness infrastructure**.

# 3. CURRENT INFRASTRUCTURE ASSIGNMENT

Implement:

* centralized logging
* structured infrastructure/service logs
* metrics
* distributed tracing integration
* CloudWatch integration
* dashboards
* alerting
* SLI/SLO foundations
* service health monitoring
* autoscaling policies
* deployment health controls
* rolling/blue-green/canary deployment support where justified
* rollback mechanisms
* production release protections
* backup verification
* restore procedures
* disaster recovery foundations
* regional/availability failure planning
* capacity thresholds
* infrastructure performance monitoring
* cost monitoring foundations
* incident-response infrastructure
* operational runbooks
* production readiness checks
* infrastructure change auditability

This volume must remain operational/infrastructure-focused.

# 4. REPOSITORY INSPECTION

Before modifying code or infrastructure, inspect:

* infrastructure-as-code
* AWS networking
* compute definitions
* load balancers
* databases
* Redis
* Kafka
* SQS
* OpenSearch
* S3
* CloudFront
* application deployment definitions
* CI/CD pipelines
* container definitions
* application logging
* application metrics
* tracing
* health endpoints
* readiness/liveness behavior
* existing dashboards
* existing alerts
* backup policies
* recovery documentation
* environment configuration
* secrets/configuration
* test infrastructure
* architecture documentation
* operational documentation

Identify:

* existing observability capabilities
* current SLO/SLI definitions
* current deployment strategy
* autoscaling mechanisms
* backup policies
* recovery assumptions
* known infrastructure limits

Do not replace established operational systems without a clear engineering reason.

# 5. TECHNOLOGY BASELINE

Use the existing AWS infrastructure and observability technologies.

Expected services/tools may include:

* CloudWatch
* CloudWatch Logs
* CloudWatch Metrics
* CloudWatch Alarms
* X-Ray or the project's established distributed tracing system
* AWS CloudTrail
* AWS Backup where applicable
* EventBridge where operationally useful
* ECS/EKS autoscaling mechanisms
* Application Load Balancer metrics
* managed-service metrics
* the repository's established dashboards and incident tooling

Use the project's existing observability stack where one already exists.

Do not introduce multiple competing monitoring systems unnecessarily.

# 6. OBSERVABILITY ARCHITECTURE

Implement a coherent observability architecture covering:

* infrastructure
* applications
* workers
* databases
* Redis
* Kafka
* queues
* OpenSearch
* media processing
* CDN/edge where useful

Observability should allow engineers to answer:

* Is the system healthy?
* Which component is failing?
* Who is affected?
* How severe is the impact?
* Did a recent deployment cause the issue?
* Which dependency is producing the failure?
* Is capacity being exhausted?
* Is the problem isolated to one environment or region?

# 7. STRUCTURED LOGGING

Ensure infrastructure and deployment components produce structured logs where applicable.

Logs should contain useful technical context such as:

* timestamp
* environment
* service
* severity
* correlation/request identifier
* deployment version
* relevant infrastructure/resource identifier

Do not log:

* passwords
* access tokens
* session secrets
* private message content
* sensitive report descriptions
* private media contents
* unnecessary personal information

# 8. LOG CENTRALIZATION

Implement centralized log collection for applicable workloads.

Support:

* application containers
* workers
* load balancers
* relevant AWS services
* deployment infrastructure
* security/audit sources where appropriate

Configure appropriate:

* retention
* encryption
* access control
* log groups/naming
* environment separation
* lifecycle policies

Do not retain logs indefinitely without a documented requirement.

# 9. METRICS

Implement infrastructure and service monitoring for:

### Application

* request rate
* error rate
* latency
* saturation
* active connections
* worker throughput

### Compute

* CPU
* memory
* task/pod count
* restarts
* unhealthy instances
* deployment health

### Database

* CPU
* storage
* connections
* latency
* replication/failover state
* I/O

### Redis

* memory
* evictions
* connections
* latency
* replication state

### Kafka

* broker health
* throughput
* consumer lag
* storage
* partition health

### Queues

* queue depth
* oldest message age
* DLQ depth
* processing rate

### OpenSearch

* cluster health
* resource utilization
* indexing rate
* query latency
* storage

### Media processing

* queue depth
* job latency
* failure rate
* processing throughput
* worker saturation

Use metrics that correspond to actual deployed components.

# 10. DISTRIBUTED TRACING

Integrate distributed tracing across supported request paths.

Where the architecture provides tracing infrastructure, support propagation through:

* edge/load balancer
* frontend/API boundary where applicable
* backend services
* async jobs
* Kafka events where technically supported
* queue consumers
* relevant downstream services

Trace data must avoid sensitive payloads.

Do not put:

* passwords
* message bodies
* private media
* report descriptions
* authentication tokens

into trace attributes.

# 11. CORRELATION

Establish consistent correlation semantics across:

* HTTP requests
* logs
* traces
* asynchronous jobs
* queue messages
* event processing
* deployment events

Use existing correlation/request identifiers from application contracts where available.

Do not create a second incompatible correlation-ID standard.

# 12. DASHBOARDS

Create operational dashboards for major platform areas.

At minimum provide dashboards or equivalent operational views for:

* API health
* compute health
* database health
* Redis
* Kafka
* queues
* OpenSearch
* media processing
* edge/CDN
* deployments
* overall platform health

Dashboards should highlight:

* traffic
* latency
* errors
* saturation
* capacity
* dependency health
* recent deployment state

Do not create decorative dashboards with metrics that cannot support an operational decision.

# 13. SLI AND SLO FOUNDATION

Define measurable service indicators and objectives based on the project's architecture.

Where applicable include:

### Availability

Percentage of successful requests.

### Latency

Relevant percentile-based request latency.

### Realtime health

Connection success/reconnect behavior where measurable.

### Async processing

Queue/job completion latency and failure rate.

### Media processing

Successful processing and processing latency.

### Search

Search availability and latency.

### Notifications

Successful delivery pipeline processing where observable.

SLOs must identify:

* measurement source
* population
* time window
* target
* exclusions where necessary

Do not invent unrealistic 100% availability targets.

# 14. ERROR BUDGET FOUNDATIONS

Where the project's reliability process uses error budgets, establish:

* SLO target
* error-budget calculation
* alert thresholds
* release implications where appropriate
* operational ownership

Do not automatically block deployments based on theoretical error budget rules unless the CI/CD architecture actually implements that policy.

# 15. ALERTING

Create actionable alerts.

Alerts should cover conditions such as:

* high 5xx error rate
* elevated latency
* failed health checks
* compute saturation
* unhealthy service count
* database connection exhaustion
* replication/failover issues
* Redis memory pressure
* Kafka consumer lag
* queue backlog
* DLQ growth
* OpenSearch cluster health
* media-processing failures
* certificate expiration risk
* backup failures
* deployment failures
* abnormal infrastructure costs where supported

Every alert must have:

* clear condition
* severity
* affected resource
* useful context
* runbook reference where appropriate

Avoid alert storms.

Avoid alerts that cannot lead to a concrete operational action.

# 16. ALERT SEVERITY

Establish consistent alert severity.

For example:

* critical production outage
* high-impact degradation
* operational warning
* informational condition

Use the project's established severity terminology where one exists.

Do not create multiple incompatible severity schemes across services.

# 17. HEALTH CHECKS AND READINESS

Align infrastructure health monitoring with actual service behavior.

Use:

* startup state
* readiness
* liveness
* dependency health where appropriate
* load-balancer health checks

A service should not receive production traffic before it can safely process requests.

Do not make liveness checks depend on optional dependencies in a way that causes unnecessary restart loops.

# 18. AUTOSCALING

Implement workload-aware autoscaling for major compute workloads.

Support where appropriate:

* API services
* realtime services
* background workers
* media processors
* queue consumers

Scaling signals may include:

* CPU
* memory
* request rate
* concurrent connections
* queue depth
* queue message age
* custom workload metrics

Use the most meaningful scaling signal for each workload.

Do not scale media-processing workers exclusively from CPU if queue backlog is the primary pressure indicator.

# 19. AUTOSCALING SAFETY

Autoscaling must include:

* minimum capacity
* maximum capacity
* cooldown/stabilization
* health-aware replacement
* resource quotas
* deployment compatibility
* dependency capacity consideration

Do not allow autoscaling to create an unbounded cost explosion.

Do not set maximum capacity without considering database, Redis, Kafka, and downstream dependency limits.

# 20. CAPACITY MANAGEMENT

Establish capacity thresholds for:

* compute
* database
* Redis
* Kafka
* SQS
* OpenSearch
* object storage
* media processing
* CDN/edge

Document important assumptions.

Capacity planning must distinguish:

* normal operating capacity
* expected burst capacity
* failure-mode capacity
* maximum tested/validated capacity where known

Do not claim load-tested limits without actual testing evidence.

# 21. DEPLOYMENT STRATEGY

Implement reliable deployment mechanisms for application workloads.

Support the strategy established by the architecture, such as:

* rolling deployments
* blue/green deployment
* canary deployment

The deployment strategy must support:

* health checks
* version traceability
* controlled rollout
* automatic or operator-driven rollback
* failure detection
* environment-specific deployment policy

Do not implement multiple deployment strategies unnecessarily.

# 22. ROLLBACK

Implement reliable rollback mechanisms.

Support:

* previous image/version identification
* deployment history
* rollback command/process
* configuration compatibility considerations
* database migration compatibility requirements
* health verification after rollback

Do not assume that application rollback automatically reverses irreversible database migrations.

# 23. DATABASE DEPLOYMENT SAFETY

Deployment infrastructure must support application/database compatibility.

Require deployment workflows to distinguish:

* backward-compatible schema changes
* application deployment
* destructive migration
* cleanup migration

Do not build a deployment system that makes incompatible schema/application transitions the default.

# 24. PRODUCTION RELEASE PROTECTION

Protect production releases through:

* protected environments
* required validation
* artifact immutability
* approved deployment identity
* deployment audit trail
* rollback availability

Where the project's CI/CD system supports approvals, use them for high-impact production changes.

Do not rely on informal human discipline alone.

# 25. DISASTER RECOVERY

Implement disaster-recovery foundations for the platform.

Cover:

* PostgreSQL recovery
* object-storage recovery
* configuration/secrets recovery
* infrastructure recreation
* Kafka recovery strategy
* queue recovery
* OpenSearch recreation/recovery
* Redis reconstruction
* deployment artifact recovery

Clearly distinguish:

* backup
* restoration
* reconstruction
* failover

Do not claim disaster recovery solely because backups exist.

# 26. RTO AND RPO

Define realistic recovery objectives for major data classes.

For example, distinguish:

* authoritative user/account data
* content metadata
* media objects
* events
* caches
* search indexes
* ephemeral realtime state
* derived analytics

Each category should have explicit recovery expectations where the architecture requires them.

Do not invent arbitrary RTO/RPO numbers without considering the service and actual infrastructure capabilities.

# 27. BACKUP VERIFICATION

Implement operational foundations for verifying backups.

Support where infrastructure allows:

* backup success monitoring
* backup age checks
* restore-test environment foundations
* snapshot verification
* recovery documentation

A successful backup API call is not equivalent to a verified restore.

Do not claim restore validation unless an actual restore test was performed.

# 28. FAILURE-INJECTION FOUNDATIONS

Where practical, establish controlled mechanisms for infrastructure failure testing.

Examples may include:

* terminating application tasks
* simulating dependency interruption in non-production
* queue consumer interruption
* service restart
* AZ-level failure simulation where the environment and tooling support it

Do not introduce uncontrolled destructive experiments into production.

Document safe test environments and boundaries.

# 29. SECURITY MONITORING

Integrate infrastructure with AWS security/audit capabilities.

Where appropriate include:

* CloudTrail
* IAM activity
* unusual security-group changes
* public exposure detection
* certificate events
* secret-access auditing
* privileged deployment activity

Do not collect or retain sensitive security data without appropriate access controls.

# 30. COST OBSERVABILITY

Implement infrastructure cost visibility where practical.

Support:

* resource tagging
* environment attribution
* service attribution
* major cost-driver dashboards/reports
* anomalous-spend detection foundations where supported

Focus on infrastructure cost signals such as:

* compute
* database
* data transfer
* storage
* media processing
* OpenSearch
* Kafka
* NAT/egress

Do not trade reliability or security for cost optimization.

# 31. OPERATIONAL RUNBOOKS

Create actionable runbooks for important operational events.

At minimum cover:

* API outage
* elevated API latency
* database failure
* Redis failure
* Kafka degradation
* queue backlog
* DLQ growth
* OpenSearch outage
* media-processing backlog
* deployment failure
* rollback
* certificate issue
* backup failure
* service scaling problem

Each runbook should include:

* symptoms
* initial checks
* relevant dashboards
* likely causes
* safe mitigation
* escalation
* recovery verification
* post-incident follow-up

Do not create generic runbooks containing only "check logs and restart."

# 32. INCIDENT RESPONSE FOUNDATIONS

Establish operational infrastructure for:

* incident identification
* severity
* escalation
* responder ownership
* communication references
* timeline capture
* recovery verification
* post-incident review

Do not create an external incident-management integration unless the project actually uses one.

Document interfaces to external operational tools where required.

# 33. PRODUCTION CHANGE AUDITABILITY

Ensure infrastructure and deployment changes are traceable.

Capture:

* commit/version
* deployment identity
* environment
* deployment timestamp
* infrastructure change
* resulting application version
* rollback event where applicable

Use existing CI/CD and AWS audit capabilities.

Do not rely solely on human-maintained spreadsheets.

# 34. SECURITY AND RELIABILITY VALIDATION

Operational infrastructure must preserve:

* least privilege
* secure secrets
* private data services
* TLS
* encrypted storage
* protected production deployment
* safe rollback
* monitored backups
* environment isolation

Do not disable security checks because a deployment is urgent.

# 35. TESTING

Add infrastructure/SRE validation covering:

* monitoring definitions
* alert rules
* dashboard configuration
* autoscaling policies
* deployment rollback
* health checks
* backup checks
* restore workflows where executable
* CI/CD protections
* IAM/security checks
* failure behavior
* environment isolation

Where possible, exercise:

* unhealthy task replacement
* deployment failure
* rollback
* queue backlog scaling
* database failover behavior through non-production testing
* alert evaluation

Do not claim tests were executed when the environment cannot perform them.

# 36. OUT OF SCOPE

Do not implement:

* new application business features
* new database schemas
* application-level Kafka producers/consumers
* application-level queue handlers
* search ranking
* frontend feature work
* mobile feature work
* moderation business logic
* product analytics implementation
* unrelated architecture redesign
* manual cloud operations as a substitute for IaC

The purpose of this prompt is operational infrastructure and reliability engineering.

# 37. DOCUMENTATION

Update documentation covering:

* observability architecture
* dashboards
* alerts
* SLO/SLI definitions
* autoscaling
* capacity assumptions
* deployment strategy
* rollback
* backup/restore
* disaster recovery
* RTO/RPO
* incident response
* runbooks
* security monitoring
* cost visibility
* operational ownership

Documentation must match the actual infrastructure.

# 38. IMPLEMENTATION DISCIPLINE

Do not:

* create fake alerts
* create dashboards using nonexistent metrics
* claim untested restore procedures work
* claim RTO/RPO achievement without evidence
* claim production failover was tested when it was not
* create unlimited autoscaling
* create destructive production failure tests
* commit credentials
* expose secrets in logs
* leave required TODO/FIXME placeholders
* suppress security checks without justification
* claim external incident-management integrations that do not exist

Where a capability requires unavailable AWS access or an external service, implement what can be represented reproducibly and report the dependency accurately.

# 39. VALIDATION

Before considering the implementation complete:

* run IaC formatting
* run IaC validation
* run security/policy scans
* validate CloudWatch/logging configuration
* validate dashboards
* validate alarms
* validate SLO/SLI metric sources
* validate autoscaling policies
* validate deployment health checks
* exercise rollback in a supported non-production environment
* verify backup monitoring
* verify restore procedure where executable
* validate DR documentation
* inspect IAM/security boundaries
* inspect production deployment protections
* inspect cost-tagging configuration
* run relevant infrastructure tests
* inspect for fake metrics/alerts
* inspect documentation against actual resources

Do not claim live failover, restore, or production deployment validation unless it was actually performed.

# 40. IMPLEMENTATION REPORT

At the end of the work, provide:

## Implemented

Summarize the observability, SRE, autoscaling, deployment-reliability, backup/restore, disaster-recovery, alerting, and operational infrastructure actually implemented.

## Files Changed

List meaningful created and modified files with their purposes.

## Operational Components

Identify dashboards, alerts, metric definitions, scaling policies, deployment controls, backup/recovery mechanisms, runbooks, and audit controls implemented.

## Tests

List tests, simulations, infrastructure validation, and rollback/restore exercises actually executed.

## Validation

List static, security, operational, deployment, backup, recovery, and live-cloud validation actually performed.

## External Dependencies

Identify unavailable AWS access, external incident tooling, credentials, domains, accounts, or other dependencies.

## Important Decisions

Document significant operational decisions and tradeoffs.

## Limitations

Document genuine limitations and unverified capabilities.

Do not represent untested recovery or failover behavior as proven.

# 41. DEFINITION OF DONE

This prompt is complete only when:

* centralized observability is established
* logs are structured and appropriately retained
* platform metrics are available
* distributed tracing is integrated where supported
* operational dashboards exist
* actionable alerts exist
* SLI/SLO foundations are defined
* autoscaling is implemented for appropriate workloads
* scaling limits protect downstream dependencies
* capacity thresholds are documented
* deployment health controls exist
* rollback mechanisms exist
* production deployment protections exist
* backup monitoring exists
* restore/recovery procedures are documented and tested where possible
* disaster-recovery foundations are established
* RTO/RPO expectations are documented
* security monitoring is integrated
* cost visibility foundations exist
* incident-response foundations exist
* operational runbooks exist
* infrastructure changes are auditable
* no fake monitoring resources remain
* no false recovery claims are documented
* no required TODO/FIXME placeholders remain
* no secrets are exposed
* documentation reflects actual infrastructure
* the implementation report accurately distinguishes implemented, tested, and externally dependent capabilities

# 42. FINAL EXECUTION DISCIPLINE

Implement this prompt as a bounded production SRE/infrastructure engineering task.

Do not expand into application feature development or unrelated infrastructure responsibilities.

Do not ask the user to choose among approaches when the existing architecture and repository establish the correct direction.

Make reasonable operational decisions based on the actual deployed architecture, AWS capabilities, scale requirements, reliability targets, and existing contracts.

Where live-cloud access or external tooling is unavailable, implement reproducible infrastructure and operational definitions and report the limitation accurately.

Do not claim completion until the Definition of Done has been satisfied and the stated validation has actually been performed.
