# PROJECT 1 — INSTAGRAM-LIKE GLOBAL SOCIAL PLATFORM

# BACKEND PROMPT — VOLUME 5

# MODERATION, TRUST & SAFETY, ANALYTICS, ADMINISTRATION, RESILIENCE & PRODUCTION HARDENING

You are the Staff Backend Engineering team responsible for implementing the moderation, trust and safety, analytics, administrative, resilience, data-governance, and production-hardening systems of a production-grade Instagram-like global social platform.

This prompt is fully standalone. It does not depend on any other prompt, document, previous conversation, previous implementation, previous architecture, previous volume, approval, or hidden context.

You must inspect the current repository before making changes and integrate with compatible existing implementation.

Repository state is the source of truth for existing code.

Implement real production functionality.

Do not generate pseudo-code.

Do not create placeholder implementations.

Do not use TODO/FIXME as substitutes for required implementation.

Do not claim functionality exists when it has not been implemented.

Do not regenerate unchanged files.

Preserve existing working unrelated functionality.

==================================================

1. BACKEND SCOPE
   ==================================================

Implement production backend capabilities for:

- content reporting
- user reporting
- abuse reporting
- moderation cases
- moderation queues
- moderation decisions
- content moderation state
- automated moderation integration
- manual moderation workflows
- administrative authorization
- audit logging
- account enforcement
- trust and safety controls
- spam prevention
- abuse prevention
- suspicious activity detection
- analytics event collection
- analytics processing
- product metrics
- operational metrics
- data retention
- deletion workflows
- privacy-aware analytics
- resilience
- disaster recovery support
- operational backfills
- data repair workflows
- production hardening

==================================================
2. REQUIRED TECHNOLOGY
======================

Use:

Backend:

- Node.js
- NestJS
- TypeScript

Persistence:

- PostgreSQL
- Prisma ORM

Caching:

- Redis

Event streaming:

- Kafka or Redpanda

Background processing:

- BullMQ

Search:

- OpenSearch or Elasticsearch

Storage:

- AWS S3

CDN:

- AWS CloudFront

Media processing:

- FFmpeg

Real-time:

- Socket.IO
- WebSockets

Push:

- Firebase Cloud Messaging
- Apple Push Notification service

Infrastructure:

- Docker
- Kubernetes
- Helm
- Terraform
- AWS
- GitHub Actions

Observability:

- OpenTelemetry
- Prometheus
- Grafana
- Loki
- Tempo

==================================================
3. DOMAIN MODULES
=================

Create or integrate modules for:

- moderation
- reports
- moderation-cases
- enforcement
- trust-safety
- abuse-prevention
- risk-signals
- analytics
- audit
- administration
- retention
- deletion
- data-repair
- operational-jobs

Keep administrative and moderation capabilities isolated from ordinary user APIs.

==================================================
4. REPORT MODEL
===============

Implement a durable Report model.

A report should contain appropriate information such as:

- report ID
- reporter ID where applicable
- target type
- target ID
- reason/category
- description where supported
- status
- priority
- created timestamp
- updated timestamp
- resolution metadata

Do not store more personal information than required.

==================================================
5. REPORT TARGETS
=================

Support reporting of:

- users
- posts
- reels
- stories
- comments
- messages where product policy permits

The reporting API must verify that the target exists or otherwise safely normalize the response to avoid unnecessary enumeration.

==================================================
6. REPORT CREATION
==================

Implement:

1. authenticate reporter when authentication is required
2. validate target
3. validate report category
4. enforce rate limits
5. prevent abusive report flooding
6. persist report
7. create moderation case or queue item
8. emit event
9. return safe response

Do not synchronously run expensive moderation workflows inside the report request.

==================================================
7. REPORT ABUSE PREVENTION
==========================

Protect against:

- mass reporting
- automated reporting
- duplicate reports
- malicious targeting
- report flooding

Apply configurable controls using:

- Redis
- per-user limits
- per-IP limits
- per-target limits
- behavioral signals

Do not automatically trust report volume as proof that content violates policy.

==================================================
8. MODERATION CASE MODEL
========================

Implement a ModerationCase model representing a reviewable trust-and-safety issue.

Support:

- case ID
- target
- originating report/event
- state
- priority
- assigned reviewer where applicable
- decision
- timestamps
- evidence references where appropriate
- appeal state where supported

==================================================
9. MODERATION CASE STATES
=========================

Support appropriate states such as:

- open
- queued
- under_review
- escalated
- actioned
- rejected
- appealed
- resolved
- closed

State transitions must be validated.

Invalid administrative state changes must be rejected.

==================================================
10. MODERATION DECISIONS
========================

Support decisions such as:

- no_action
- content_allowed
- content_restricted
- content_removed
- account_warned
- account_restricted
- account_suspended
- account_disabled

The exact decision set must remain configurable.

==================================================
11. MODERATION AUTHORIZATION
============================

Administrative actions require strong authorization.

At minimum distinguish:

- normal user
- moderator
- senior moderator
- administrator

Do not trust role values directly from the client.

Use server-side authorization.

Sensitive administrative operations should be audited.

==================================================
12. ADMIN SESSION SECURITY
==========================

Administrative sessions must be more strictly protected than ordinary sessions.

Support:

- stronger session lifetime
- explicit revocation
- audit logging
- suspicious-login detection
- optional MFA integration points where supported

Never reuse ordinary client trust assumptions for privileged operations.

==================================================
13. MODERATION EVIDENCE
=======================

When storing evidence references:

- protect private content
- minimize copied data
- use secure object access
- maintain integrity metadata where appropriate
- avoid publicly accessible URLs

Do not duplicate large media unnecessarily.

Prefer secure references to authoritative media objects.

==================================================
14. AUTOMATED MODERATION
========================

Create an integration abstraction for automated moderation providers.

Possible capabilities:

- image classification
- video classification
- spam detection
- text classification
- abuse detection

The domain must not depend directly on one vendor.

Use provider adapters.

==================================================
15. MODERATION PROVIDER FAILURE
===============================

If automated moderation is unavailable:

- classify the failure
- retry where appropriate
- preserve content state safely
- avoid accidental publication of content that requires successful safety checks
- avoid blocking unrelated product functionality
- emit telemetry

The failure policy must depend on content category and risk level.

==================================================
16. MODERATION STATE
====================

Content should support moderation states such as:

- pending
- approved
- restricted
- rejected
- removed

Do not expose content in prohibited states through ordinary APIs.

==================================================
17. ENFORCEMENT
===============

Enforcement actions must propagate to:

- content retrieval
- feeds
- search
- discovery
- recommendations
- notifications
- messaging
- media access

Derived systems may lag, but authoritative request-time access checks must protect users.

==================================================
18. ACCOUNT ENFORCEMENT
=======================

Support account enforcement actions such as:

- warning
- temporary restriction
- temporary suspension
- permanent disablement

An account-level enforcement must affect:

- authentication
- session validity
- content creation
- messaging
- engagement
- API access
- background processing where relevant

==================================================
19. CONTENT RESTRICTION
=======================

Restricted content must support granular behavior.

For example, content may be:

- hidden entirely
- unavailable in recommendation
- unavailable in search
- age/region restricted where applicable
- visible only to authorized audiences

Do not implement restriction solely in the frontend.

==================================================
20. SPAM DETECTION
==================

Implement backend signals for:

- repeated identical content
- abnormal follow velocity
- abnormal like activity
- mass messaging
- account-creation bursts
- suspicious upload patterns
- high-frequency API behavior

Signals may be asynchronous.

Do not block normal actions solely based on one weak signal.

==================================================
21. RISK SCORING
================

Where risk scoring is implemented, make the scoring system:

- versioned
- observable
- configurable
- deterministic enough to debug

Record the rule/model version used for important enforcement decisions.

==================================================
22. RATE LIMITING
=================

Create differentiated limits for:

- authentication
- account creation
- follow actions
- engagement
- messaging
- uploads
- reporting
- search
- notification operations
- administrative APIs

Use Redis for distributed rate-limit state.

==================================================
23. ADMIN API
=============

Create protected administrative endpoints for:

- report review
- moderation case retrieval
- moderation decision
- account enforcement
- content enforcement
- audit lookup
- operational status
- safe data-repair operations

Administrative APIs must never be exposed as ordinary user endpoints.

==================================================
24. AUDIT RECORD MODEL
======================

Create durable AuditRecord entries for sensitive actions.

Record appropriate fields such as:

- audit ID
- actor ID
- actor role
- action
- target type
- target ID
- timestamp
- request/correlation ID
- safe metadata

Never store secrets.

==================================================
25. AUDIT IMMUTABILITY
======================

Audit records should be append-oriented.

Normal administrative APIs must not allow arbitrary editing or deletion of historical audit records.

Corrections should be represented as additional audit events.

==================================================
26. MODERATION AUDIT TRAIL
==========================

For a moderation case, maintain a clear history of:

- created
- assigned
- reviewed
- decision made
- enforcement applied
- appealed
- resolved

This must permit investigators to understand what happened without relying on application logs alone.

==================================================
27. APPEALS
===========

Where appeals are supported:

- store appeal request
- authenticate requester
- verify eligibility
- enforce appeal limits
- prevent repeated abuse
- preserve original decision
- assign/review appeal separately
- record final outcome

Do not mutate historical moderation decisions to hide their previous state.

==================================================
28. USER PRIVACY
================

Moderation systems must minimize exposure of personal data.

Reviewers should access only the information necessary for the task.

Private data should not be copied broadly into moderation records.

==================================================
29. ANALYTICS EVENT MODEL
=========================

Implement a structured analytics-event contract.

Each event should include:

- event ID
- event type
- version
- actor identifier where appropriate
- target identifier where appropriate
- timestamp
- session/context identifiers where appropriate
- platform
- application version where useful
- correlation/trace ID
- bounded event properties

Avoid collecting unnecessary sensitive information.

==================================================
30. ANALYTICS EVENTS
====================

Capture important product events such as:

- registration
- login
- profile view
- follow
- unfollow
- post creation
- post view
- reel play
- reel completion
- story view
- like
- comment
- save
- share
- message sent
- search
- notification interaction
- report
- moderation decision

Analytics collection must not block user requests.

==================================================
31. EVENT INGESTION
===================

Route analytics through asynchronous infrastructure.

Preferred flow:

application event
→ durable/event pipeline
→ Kafka/Redpanda
→ analytics consumer
→ processing/aggregation
→ analytical storage or reporting subsystem

Do not perform expensive aggregation inside request handlers.

==================================================
32. ANALYTICS IDEMPOTENCY
=========================

Analytics consumers must tolerate duplicate events.

Use:

- event IDs
- deduplication
- deterministic aggregation

Avoid double counting due to retries.

==================================================
33. ANALYTICS RETENTION
=======================

Define retention periods appropriate to event categories.

High-volume raw events may have shorter retention than aggregated metrics.

Retention must be configurable.

Do not retain personal data indefinitely without a valid reason.

==================================================
34. PRODUCT METRICS
===================

Provide backend metrics for:

- daily/weekly active users
- registrations
- successful logins
- follows
- posts
- reels
- stories
- engagement
- messaging
- search usage
- notification delivery
- moderation volume

Metrics must distinguish operational telemetry from product analytics.

==================================================
35. OPERATIONAL METRICS
=======================

Expose Prometheus metrics for:

- request rate
- latency
- error rate
- database latency
- Redis latency
- Kafka lag
- queue depth
- worker failure
- media-processing failure
- search latency
- WebSocket connections
- push delivery
- moderation queue depth

==================================================
36. DATA RETENTION
==================

Define explicit retention handling for:

- logs
- traces
- analytics events
- moderation records
- audit logs
- expired media
- deleted accounts
- outbox records
- queue/dead-letter records

Never allow temporary operational records to grow without bound.

==================================================
37. DATA DELETION
=================

Implement deletion workflows covering:

- user account
- profile
- content
- media
- search documents
- cached records
- feed candidates
- notifications where applicable
- analytics identifiers where required
- device records
- sessions

Deletion should be orchestrated asynchronously after authoritative state changes.

==================================================
38. ACCOUNT DELETION
====================

Account deletion should:

1. mark account deleted
2. invalidate sessions
3. prevent further authentication
4. block new interactions
5. remove public visibility
6. emit deletion event
7. enqueue cleanup
8. propagate to derived systems
9. delete eligible media
10. remove search representations
11. clean device registrations
12. clean relevant caches

Deletion jobs must be resumable.

==================================================
39. DATA REPAIR
===============

Create controlled operational mechanisms for correcting derived data.

Examples:

- rebuild profile search document
- rebuild content search document
- recompute counter
- rebuild feed candidate set
- repair notification count
- repair stale moderation state

Data-repair operations must be:

- authenticated
- authorized
- auditable
- idempotent
- observable

==================================================
40. BACKFILL JOBS
=================

Large backfills must use BullMQ or controlled batch workers.

Do not run massive unrestricted operations inside one HTTP request.

Backfills must support:

- batching
- checkpoints
- retries
- rate limits
- pause/resume
- progress metrics

==================================================
41. DATABASE RESILIENCE
=======================

Implement backend behavior for:

- connection exhaustion
- transient database errors
- deadlocks
- transaction retries where safe
- statement timeouts
- slow queries

Do not automatically retry arbitrary transactions when doing so could duplicate side effects.

==================================================
42. REDIS RESILIENCE
====================

Redis failures should not destroy durable business data.

For cache use:

- fall back to database
- degrade performance safely

For ephemeral presence:

- allow temporary loss

For rate limiting:

- apply a safe configured fallback policy

Do not silently allow unlimited abuse merely because Redis is unavailable.

==================================================
43. KAFKA/REDPANDA RESILIENCE
=============================

Handle:

- producer failure
- consumer failure
- lag
- partition reassignment
- poison events
- duplicate events

Outbox-backed critical events must remain durable until publication succeeds.

==================================================
44. BULLMQ RESILIENCE
=====================

Workers must survive:

- process restart
- job timeout
- dependency outage
- duplicate delivery
- deployment interruption

Use:

- retry policies
- backoff
- lock renewal
- job idempotency
- dead-letter handling

==================================================
45. SEARCH RESILIENCE
=====================

Search indexes are derived.

If OpenSearch/Elasticsearch is unavailable:

- writes to authoritative systems continue
- indexing is retried
- search may degrade gracefully
- rebuild remains possible

Do not make search infrastructure a hard dependency for ordinary transactional correctness.

==================================================
46. OBJECT STORAGE RESILIENCE
=============================

S3 failures should be handled as dependency failures.

Upload state must not become permanently inconsistent due to one failed request.

Use retries for safe operations.

Do not retry unboundedly.

==================================================
47. THIRD-PARTY FAILURE HANDLING
================================

External providers such as:

- FCM
- APNS
- payment providers
- automated moderation providers
- map/geolocation providers where later used

must be accessed through adapters.

Classify:

- retryable errors
- permanent errors
- authorization/configuration errors

==================================================
48. CIRCUIT-BREAKING
====================

For expensive or unreliable external dependencies, support appropriate protective patterns:

- timeout
- retry
- exponential backoff
- circuit breaker
- bulkhead
- fallback

Do not combine unlimited retries with long timeouts.

==================================================
49. TIMEOUT POLICY
==================

Every external network dependency should have an explicit timeout.

Timeouts should prevent one slow provider from consuming all application resources.

Do not use infinite request waits.

==================================================
50. GRACEFUL DEGRADATION
========================

Define fallback behavior.

Examples:

Search unavailable:
→ transactional content APIs remain available.

Push unavailable:
→ in-app notifications still work.

Recommendation unavailable:
→ chronological or fallback discovery feed.

Analytics unavailable:
→ user operation still succeeds where analytics is non-critical.

Redis unavailable:
→ database-backed operation continues where practical.

==================================================
51. BACKUP REQUIREMENTS
=======================

PostgreSQL must have:

- automated backups
- point-in-time recovery capability where infrastructure supports it
- retention policies
- restore validation

Backups must not be considered valid merely because a backup job reports success.

Restore testing is required.

==================================================
52. OBJECT DATA PROTECTION
==========================

Important S3 objects must have appropriate:

- durability
- versioning where justified
- lifecycle rules
- encryption
- access controls

Never expose broad write permissions.

==================================================
53. SECRET MANAGEMENT
=====================

Secrets must use secure configuration/secret-management mechanisms.

Never commit:

- JWT signing keys
- AWS keys
- database passwords
- Redis credentials
- Kafka credentials
- FCM credentials
- APNS credentials
- moderation-provider credentials

==================================================
54. IAM
=======

Use least-privilege AWS IAM permissions.

Application workloads should have only the S3 and AWS permissions they require.

Separate:

- application permissions
- worker permissions
- deployment permissions
- administrative permissions

==================================================
55. NETWORK SECURITY
====================

Production architecture must separate:

- public ingress
- application workloads
- databases
- queues
- caches
- internal services

Databases should not be publicly reachable.

==================================================
56. ADMINISTRATIVE ACTION PROTECTION
====================================

Sensitive administrative actions should support:

- strong authentication
- authorization
- audit logging
- rate limiting
- explicit target validation
- concurrency protection

Dangerous actions should have clear confirmation semantics on the API side.

==================================================
57. PRODUCTION CONFIGURATION
============================

Configuration must support:

- environment-specific values
- feature flags
- moderation thresholds
- rate limits
- queue concurrency
- retention policies
- provider settings
- ranking thresholds
- high-degree-account thresholds

Avoid recompiling the application for routine configuration changes where practical.

==================================================
58. FEATURE FLAGS
=================

Feature flags must be server-authoritative.

Support controlled rollout of risky backend functionality.

Feature-flag evaluation must not weaken security.

A disabled feature must not leave partially accessible endpoints.

==================================================
59. MIGRATION SAFETY
====================

Database changes must use safe migration practices.

For high-risk changes:

- add new schema
- backfill
- switch reads/writes
- remove old schema only after verification

Avoid destructive migrations that assume all data has already migrated.

==================================================
60. DEPLOYMENT SAFETY
=====================

Backend deployment should support:

- rolling updates
- readiness checks
- liveness checks
- graceful shutdown
- connection draining
- worker shutdown handling

Application shutdown must avoid abandoning acknowledged durable jobs or partially written state where possible.

==================================================
61. GRACEFUL SHUTDOWN
=====================

On shutdown:

- stop accepting new traffic
- finish safe in-flight operations
- close database connections
- close Redis connections
- stop consuming new jobs where appropriate
- allow current jobs to complete or return safely
- close WebSocket infrastructure gracefully

==================================================
62. WORKER SHUTDOWN
===================

Workers must not lose durable jobs during deployment.

Use queue semantics that allow interrupted jobs to become available again safely.

Ensure long-running media/moderation jobs use appropriate heartbeats/locks.

==================================================
63. SECURITY MONITORING
=======================

Emit security signals for:

- repeated login failures
- suspicious token reuse
- abnormal account creation
- mass following
- mass messaging
- suspicious content uploads
- report abuse
- administrative anomalies

Security telemetry must be privacy-aware.

==================================================
64. DATA ACCESS CONTROL
=======================

Administrative queries must apply least privilege.

Do not allow a generic administrative endpoint to query arbitrary database tables.

Expose purpose-built operations.

==================================================
65. API VERSIONING
==================

Maintain explicit API versions.

Breaking changes should use a new version or a compatible migration strategy.

Do not silently change response contracts used by web/mobile clients.

==================================================
66. BACKWARD COMPATIBILITY
==========================

When modifying existing APIs or schemas:

- preserve current behavior where possible
- support migration paths
- maintain old fields while transitioning where appropriate
- update clients before removing contracts

==================================================
67. TESTING — MODERATION
=========================

Implement tests for:

- report creation
- duplicate reports
- report limits
- moderation case lifecycle
- moderator authorization
- invalid state transitions
- moderation decisions
- account enforcement
- content restriction
- appeal behavior
- audit records

==================================================
68. TESTING — RESILIENCE
=========================

Test:

- database timeout
- Redis outage
- Kafka outage
- queue outage
- search outage
- S3 failure
- FCM failure
- APNS failure
- moderation-provider failure
- worker restart
- API restart
- duplicate event processing
- stale derived data
- retry storms

==================================================
69. TESTING — DATA GOVERNANCE
==============================

Test:

- account deletion
- content deletion
- media cleanup
- search cleanup
- cache cleanup
- device cleanup
- session invalidation
- retention jobs
- backfills
- data repair

==================================================
70. TESTING — SECURITY
=======================

Test:

- privilege escalation
- unauthorized moderation
- unauthorized audit access
- administrative IDOR
- report abuse
- rate-limit bypass
- token replay
- secret leakage
- unsafe provider configuration
- malicious event payload
- malicious backfill parameters

==================================================
71. PERFORMANCE TESTING
=======================

Test:

- high report volume
- large moderation queues
- analytics bursts
- large deletion workflows
- large backfills
- high Kafka throughput
- worker saturation
- administrative query load

Administrative operations must not starve user-facing workloads.

==================================================
72. OBSERVABILITY
=================

Instrument:

- moderation workflows
- report processing
- enforcement
- analytics pipeline
- audit operations
- data deletion
- backfills
- repair jobs
- database retries
- external-provider failures

Metrics should include:

- moderation queue depth
- moderation latency
- report rate
- false/duplicate report rate where measurable
- enforcement rate
- analytics lag
- deletion backlog
- backfill progress
- repair failures
- dependency error rate

==================================================
73. ALERTING
============

Alert on:

- moderation queue explosion
- analytics pipeline lag
- deletion backlog
- repeated worker failures
- Kafka lag
- dead-letter growth
- database saturation
- Redis failure
- S3 failure rate
- provider outage
- suspicious administrative activity
- backup failure

==================================================
74. DISASTER RECOVERY
=====================

Define operational recovery for:

- database restoration
- event replay
- search rebuild
- feed regeneration
- cache regeneration
- queue recovery
- worker replacement

Recovery procedures must avoid creating duplicate business side effects.

==================================================
75. DATA CONSISTENCY REPAIR
===========================

Provide reconciliation concepts for:

- engagement counters
- notification counts
- search indexes
- feed candidate state
- moderation state
- media-processing state

Reconciliation should compare authoritative data with derived systems.

==================================================
76. SYSTEM RECONCILIATION
=========================

Background reconciliation jobs should be:

- bounded
- schedulable
- observable
- idempotent
- resumable

Do not run a complete global reconciliation in one unbounded operation.

==================================================
77. OPERATIONAL RUNBOOK DATA
============================

Backend code and operational documentation should identify:

- major failure modes
- expected fallback
- recovery action
- relevant telemetry
- safe operational commands/jobs

Do not document unsafe direct database mutation as the primary recovery strategy.

==================================================
78. ACCEPTANCE CRITERIA
=======================

This implementation is complete only when:

- reporting works
- moderation cases work
- moderation states work
- moderation decisions work
- administrative authorization works
- enforcement works
- audit logging works
- appeal handling exists where supported
- automated moderation adapters exist
- moderation failure handling exists
- spam controls exist
- risk signals exist
- analytics events are captured
- analytics are processed asynchronously
- analytics are idempotent
- retention exists
- deletion workflows exist
- account deletion propagates
- media cleanup exists
- search cleanup exists
- backfills exist
- data repair operations exist
- database resilience exists
- Redis resilience exists
- Kafka/Redpanda resilience exists
- BullMQ resilience exists
- search resilience exists
- S3 failure handling exists
- external-provider adapters exist
- retry/timeout/circuit-breaker behavior exists where appropriate
- graceful degradation exists
- backups are configured
- restore validation exists
- secret management is enforced
- IAM follows least privilege
- network security is defined
- administrative actions are protected
- feature flags are safe
- migration strategy is safe
- deployment/shutdown behavior is safe
- security monitoring exists
- observability exists
- alerts exist
- disaster recovery mechanisms exist
- reconciliation exists
- automated tests cover critical functionality
- TypeScript compiles
- database migrations succeed
- no required functionality remains a placeholder

==================================================
79. IMPLEMENTATION FINISHING RULE
=================================

Do not stop after creating interfaces, entities, controllers, queues, or documentation.

Implement the actual working functionality for the complete scope above.

Inspect the current repository first.

Reuse compatible infrastructure.

Integrate with the existing backend rather than unnecessarily replacing it.

Modify only the files required.

Validate:

- formatting
- linting
- TypeScript
- Prisma schema/migrations
- API behavior
- background workers
- Kafka/Redpanda processing
- Redis behavior
- search integration
- S3 workflows
- moderation workflows
- administrative authorization
- audit behavior
- deletion workflows
- retry behavior
- failure handling
- unit tests
- integration tests
- security tests
- resilience tests

The resulting backend must be a production-grade trust-and-safety, analytics, administration, data-governance, resilience, and operational-hardening subsystem capable of supporting a globally scaled social platfor

You are operating in Senior Engineering Team Mode.

You are the Principal Software Architect, Staff Backend Engineer, Database Architect, Distributed Systems Engineer, Security Engineer, QA Engineer, DevOps Engineer, Observability Engineer, and Technical Writer for this Instagram-like global social platform.

The previous backend volumes have already established:

- Backend foundation and application architecture.
- Authentication, accounts, profiles, creators, businesses, sessions, and devices.
- Follow relationships, private accounts, blocks, restrictions, close friends, and social graph primitives.
- PostgreSQL + Prisma persistence.
- Redis caching and distributed coordination.
- Kafka/Redpanda event architecture and the transactional outbox.
- BullMQ background jobs.
- WebSocket/Socket.IO real-time infrastructure.
- S3 media storage abstraction.
- Image/video processing and media workflows.
- HLS video delivery.
- Posts, carousels, drafts, stories, highlights, reels.
- Captions, hashtags, mentions, locations, audio.
- Rights-management primitives.
- Visibility, publication, scheduling, deletion, and restoration.
- Home/following feeds, story tray, Reels feed, Explore.
- Recommendation candidate generation and ranking.
- Trending systems.
- Search and indexing.
- Engagement aggregates, impressions, watch behavior, and negative feedback.
- Messaging and conversations.
- Message requests, attachments, reactions, replies, delivery/read state.
- Presence and typing indicators.
- Notifications and push delivery.
- Reports, moderation cases, moderation actions, safety workflows, and appeals.
- Copyright/rights claims, regional restrictions, takedowns, and restoration.
- Creator/business analytics.
- Advertising primitives.
- Commerce primitives.
- Administration, RBAC, feature flags, dynamic configuration, and audit logging.
- Privacy export/deletion workflows.
- Observability and testing foundations.

This volume is the final backend expansion and hardening phase.

The goal is not to invent another unrelated architecture.

The goal is to integrate, complete, harden, optimize, and productionize the backend so that the entire platform behaves as one coherent distributed system.

Do not rewrite already-correct modules merely for stylistic reasons.

Do not generate pseudo-code.

Do not generate TODOs.

Do not generate placeholders.

Do not leave incomplete services.

Do not leave fake implementations.

Do not use "implement later", "same as above", "omitted for brevity", or equivalent shortcuts.

Every generated file must contain real production-oriented implementation.

Every implementation must compile.

Every API contract must be internally consistent.

Every database relationship must be valid.

Every asynchronous workflow must be idempotent.

Every event consumer must be safe to retry.

Every background job must be retry-safe.

Every mutation that crosses services or domains must be designed for partial failure.

Maintain backward compatibility with everything produced in previous backend volumes.

Never regenerate unchanged files.

Never replace an existing production implementation with an inferior abstraction.

Use the architecture established by the previous volumes as the source of truth.

==================================================
GLOBAL BACKEND OBJECTIVES
=========================

The final backend must provide:

1. Strong domain boundaries.
2. Clear application/service/repository responsibilities.
3. Reliable transactional behavior.
4. Idempotent asynchronous processing.
5. Correct event ordering where required.
6. Distributed-systems safety.
7. Horizontal scalability.
8. Efficient database access.
9. Effective Redis utilization without creating consistency bugs.
10. Search consistency with source-of-truth data.
11. Feed and recommendation integration.
12. Comprehensive anti-abuse protections.
13. Fraud-resistance foundations.
14. Strong privacy guarantees.
15. Regional data and policy enforcement.
16. Data lifecycle management.
17. Operational visibility.
18. Resiliency under dependency failure.
19. Load-testable APIs.
20. Comprehensive automated tests.
21. Production-grade API documentation.
22. Clear operational runbooks.
23. Final repository consistency across all backend modules.

==================================================
TECHNOLOGY REQUIREMENTS
=======================

Use the established technology stack:

- Node.js
- NestJS
- TypeScript
- PostgreSQL
- Prisma ORM
- Redis
- Kafka or Redpanda
- BullMQ
- OpenSearch or Elasticsearch
- AWS S3
- CloudFront
- FFmpeg
- HLS where applicable
- Socket.IO / WebSockets where applicable
- Firebase Cloud Messaging
- Apple Push Notification Service
- OpenTelemetry
- Prometheus
- Grafana
- Loki
- Tempo

The exact versions must follow the repository configuration and established architecture.

Do not introduce another major framework unless absolutely necessary and architecturally justified.

==================================================
ARCHITECTURAL PRINCIPLES
========================

Continue enforcing:

- Domain-Driven Design.
- Clean Architecture.
- SOLID.
- Dependency inversion.
- Repository pattern.
- Service/application layer separation.
- Explicit transaction boundaries.
- Immutable domain events where appropriate.
- Transactional outbox.
- Idempotent event handling.
- Idempotent jobs.
- Defense in depth.
- Least privilege.
- Zero-trust assumptions between internal components.
- Explicit validation.
- Explicit authorization.
- Explicit privacy enforcement.
- Observable critical workflows.
- Fail closed for security-sensitive operations.
- Fail safe where availability is more important and the architecture permits it.

==================================================
VOLUME 5 SCOPE
==============

This volume covers:

MILESTONE 41
Platform-wide integration and domain orchestration.

MILESTONE 42
Advanced anti-abuse, spam, bot, rate-limit, and trust systems.

MILESTONE 43
Fraud detection and suspicious behavior workflows.

MILESTONE 44
Advanced feed/recommendation/search integration and consistency.

MILESTONE 45
Advanced creator monetization and platform financial primitives.

MILESTONE 46
Advanced commerce transaction and fulfillment backend foundations.

MILESTONE 47
Data platform, analytics pipelines, event lake, and warehouse integration boundaries.

MILESTONE 48
Multi-region backend behavior, regional routing, consistency, and disaster recovery.

MILESTONE 49
Performance engineering, load protection, resilience engineering, and capacity controls.

MILESTONE 50
Final backend integration, security hardening, test completion, documentation, and release readiness.

==================================================
MILESTONE 41 — PLATFORM-WIDE DOMAIN ORCHESTRATION
==================================================

Build a coherent orchestration layer across the previously implemented domains.

The objective is NOT to create one giant service.

The objective is to create explicit application workflows that coordinate multiple bounded contexts safely.

Implement workflows such as:

- User registration completion.
- Profile completion.
- Follow user.
- Accept follow request.
- Publish post.
- Publish reel.
- Publish story.
- Story expiration.
- Post engagement.
- Reel engagement.
- Comment creation.
- Comment moderation.
- Save to collection.
- Share content.
- Send message.
- Receive message.
- Notification creation.
- Report content.
- Moderation escalation.
- Rights claim.
- Rights takedown.
- Content restoration.
- Account restriction.
- Account suspension.
- Account deletion.
- Privacy export.
- Privacy deletion.
- Creator analytics aggregation.
- Advertising event processing.
- Commerce product tagging.
- Commerce purchase lifecycle where supported.
- Recommendation feedback.
- Search indexing.
- Content deletion propagation.

Requirements:

- Use explicit use cases.
- Avoid circular domain dependencies.
- Do not allow controllers to orchestrate business logic.
- Use domain/application services for workflows.
- Publish integration events through the existing outbox architecture.
- Track correlation IDs.
- Track causation IDs where appropriate.
- Make every workflow retry-safe.
- Design compensating actions for multi-step operations.
- Distinguish synchronous guarantees from eventual consistency.
- Record workflow failures.
- Provide retry and dead-letter behavior.
- Ensure duplicate requests cannot produce duplicate business effects.

Create integration contracts for:

- synchronous application calls
- asynchronous events
- scheduled jobs
- domain events
- integration events

Document which consistency model applies to each workflow.

==================================================
MILESTONE 42 — ADVANCED ANTI-ABUSE AND TRUST SYSTEM
====================================================

Implement a reusable anti-abuse framework.

The platform must be resistant to:

- spam
- account farming
- bot activity
- fake engagement
- mass following
- mass unfollowing
- credential abuse
- scraping
- message spam
- comment spam
- malicious links
- automated content creation abuse
- giveaway abuse
- promotion abuse
- repeated account creation
- coordinated abusive behavior

Implement:

- API rate limiting.
- Endpoint-specific limits.
- User-level limits.
- Account-level limits.
- IP-level limits.
- Device-level limits.
- Session-level limits.
- Anonymous request controls.
- Adaptive rate limiting.
- Sliding-window controls.
- Token bucket where appropriate.
- Burst protection.
- Distributed rate-limit counters using Redis.
- Redis Lua scripts where atomicity requires them.
- Rate-limit response metadata.
- Retry-after semantics.
- Internal anti-abuse decision service.

Create risk signals including:

- Account age.
- Session age.
- Device familiarity.
- IP reputation.
- Request velocity.
- Action velocity.
- Action diversity.
- Follow/unfollow patterns.
- Comment patterns.
- Messaging patterns.
- Content publishing patterns.
- Login anomalies.
- Geographic anomalies where legally and architecturally appropriate.
- Repeated failed actions.
- Block/report concentration.
- Suspicious engagement loops.

Implement trust states such as:

- unknown
- low trust
- normal trust
- elevated trust
- highly trusted
- restricted
- under review
- suspended

Do not blindly hard-code these decisions into controllers.

Create a policy/decision abstraction that can evolve.

The trust engine must support:

- score calculation
- reason codes
- feature inputs
- thresholds
- temporary restrictions
- permanent enforcement actions
- appeal state
- audit trail

Prevent trust logic from becoming impossible to test.

Create dedicated tests for false-positive resistance.

==================================================
MILESTONE 43 — FRAUD AND SUSPICIOUS ACTIVITY
=============================================

Implement fraud-oriented backend foundations.

The system must support suspicious activity detection around:

- authentication
- account creation
- password changes
- email changes
- phone changes
- payment-related activity
- creator monetization
- advertiser billing
- commerce actions
- excessive promotional behavior
- referral systems if present
- gift systems if present

Create:

- FraudEvent.
- RiskAssessment.
- RiskDecision.
- RiskSignal.
- RiskCase.
- FraudReview.
- TemporaryHold.
- FraudAction.
- FraudAppeal.

Support decisions such as:

- allow
- challenge
- delay
- throttle
- block
- hold
- review

Maintain reason codes.

Never expose internal fraud scoring details to untrusted clients.

Implement fraud events as asynchronous events where real-time blocking is not required.

Support synchronous risk checks for security-sensitive workflows.

Ensure risk decisions are auditable.

Ensure fraud evaluation is deterministic where required for testability.

Support feature versioning.

A fraud decision must record which rules/features/version generated the result.

==================================================
MILESTONE 44 — FEED, RECOMMENDATION, AND SEARCH INTEGRATION
============================================================

Complete cross-domain integration between content, engagement, social graph, feed, recommendation, and search.

Implement source-of-truth synchronization for:

- content creation
- content updates
- content deletion
- user blocks
- restrictions
- visibility changes
- account suspension
- content reports
- moderation actions
- rights takedowns
- private-account state
- follow relationships
- unfollow relationships

A piece of content must stop appearing in all inappropriate discovery surfaces after removal or visibility changes propagate.

Implement invalidation events.

Implement cache invalidation.

Implement search de-indexing.

Implement recommendation exclusion.

Implement feed tombstone handling where necessary.

Ensure deleted or restricted content cannot remain visible due to stale caches indefinitely.

Build a unified eligibility layer that can answer:

- Can user A see content B?
- Can user A discover content B?
- Can user A interact with content B?
- Can content B be recommended to user A?
- Can content B be indexed for user A?
- Can content B appear in search?
- Can content B appear in Explore?
- Can content B appear in Reels?
- Can content B appear in hashtag discovery?
- Can content B appear in audio discovery?

Centralize shared policy decisions without turning every domain into one monolithic service.

Implement:

- content eligibility
- account eligibility
- social relationship eligibility
- geography/region eligibility
- rights eligibility
- moderation eligibility
- recommendation eligibility
- age/policy eligibility where supported

Feed and recommendation systems must consume the eligibility abstraction.

Search must apply the appropriate visibility and safety restrictions.

==================================================
RECOMMENDATION CONSISTENCY
==========================

Ensure recommendation systems handle:

- deleted content
- private content
- blocked users
- muted users
- restricted users
- previously consumed content
- content under moderation
- region-limited content
- rights-limited media

Implement exclusion caches where useful.

Implement recommendation invalidation events.

Do not store sensitive recommendation reasons in client-visible responses unless explicitly designed.

==================================================
SEARCH CONSISTENCY
==================

Implement reliable search synchronization.

Support:

- index creation
- index update
- index deletion
- delayed retry
- failed indexing retry
- dead-letter indexing events
- reindex jobs
- consistency verification
- orphan detection
- missing-index detection

Implement administrative reconciliation jobs.

A source-of-truth PostgreSQL record must always be treated as authoritative over OpenSearch/Elasticsearch.

==================================================
MILESTONE 45 — CREATOR MONETIZATION
====================================

Extend creator/business backend capabilities into production-oriented monetization primitives.

Support architectural foundations for:

- subscriptions
- creator memberships
- paid content
- digital gifts
- tips
- creator payouts
- monetized content
- earning records
- revenue share
- platform fees
- payout holds
- payout eligibility
- payout states
- refunds
- disputes
- chargebacks

Do not assume a specific external payment processor beyond the abstraction already established.

Create provider interfaces.

The domain layer must remain provider-neutral.

Implement:

- WalletLedger or equivalent accounting abstraction.
- LedgerEntry.
- RevenueEvent.
- CreatorEarning.
- PlatformFee.
- PayoutRequest.
- Payout.
- Refund.
- Dispute.
- Chargeback.
- SettlementRecord.

Financial data must use decimal-safe monetary representations.

Never use floating-point arithmetic for money.

Every financial mutation must be idempotent.

Every financial transaction must have a unique external reference where applicable.

Do not silently mutate finalized accounting records.

Use immutable ledger entries where appropriate.

Corrections must be represented through compensating entries.

Create audit records for financial operations.

Protect financial endpoints using stronger authorization.

==================================================
CREATOR SUBSCRIPTIONS
=====================

Implement backend primitives for:

- subscription plans
- subscriber relationships
- billing state
- entitlement state
- renewal
- cancellation
- expiration
- grace periods
- entitlement validation

A creator subscriber entitlement must be independently verifiable.

Do not infer entitlement solely from stale client state.

Support webhook-based external payment updates through idempotent handlers.

==================================================
CREATOR PAYOUTS
===============

Implement:

- payout eligibility calculation
- minimum payout threshold
- payout request
- payout processing
- payout failure
- payout cancellation where supported
- payout reconciliation

Sensitive payout information must be protected.

Do not store provider secrets in the database.

==================================================
MILESTONE 46 — ADVANCED COMMERCE BACKEND
=========================================

Extend commerce foundations into transaction-ready architecture.

Support:

- products
- product variants
- inventory references
- product collections
- product tags
- product media
- storefront metadata
- carts where supported
- checkout session abstraction
- orders
- order items
- payment state
- fulfillment state
- shipment state
- returns
- refunds
- cancellations

Create domain-neutral external provider interfaces.

Do not bind business logic directly to one payment or shipping vendor.

Implement:

- Order
- OrderItem
- Checkout
- CheckoutItem
- PaymentAttempt
- Refund
- Fulfillment
- Shipment
- ReturnRequest
- InventoryReservation

Ensure order state transitions are explicit.

Do not allow arbitrary state mutation.

Use state machines or equivalent guarded transition services.

Examples:

Order:

- draft
- pending_payment
- paid
- processing
- fulfilled
- cancelled
- refunded
- partially_refunded
- failed

Payment:

- pending
- authorized
- captured
- failed
- cancelled
- refunded
- partially_refunded
- disputed

Implement idempotent payment webhook processing.

Implement inventory reservation expiration.

Avoid overselling through appropriate transactional locking or reservation patterns.

Commerce data must respect privacy requirements.

==================================================
MILESTONE 47 — DATA PLATFORM AND ANALYTICS INTEGRATION
=======================================================

Build production-oriented backend boundaries for large-scale analytical data.

The transactional database must not become the analytics warehouse.

Implement event publication for:

- impressions
- views
- watch time
- likes
- comments
- follows
- unfollows
- shares
- saves
- searches
- profile visits
- story views
- reel views
- message events where analytically permitted
- notification interactions
- moderation actions
- ad events
- commerce events
- creator earnings events

Every analytics event must include appropriate metadata such as:

- event ID
- event type
- event timestamp
- actor reference where permitted
- target reference where permitted
- request/correlation ID where relevant
- source
- schema version
- producer version

Do not expose private message contents through analytics events.

Do not put sensitive payloads into generic event streams.

Implement event schema versioning.

Support:

- event envelope validation
- producer contracts
- consumer compatibility
- dead-letter events
- replay
- deduplication
- retention policies

Create a data export abstraction that can feed future:

- data lake
- warehouse
- BI
- machine learning
- recommendation training
- moderation analytics
- finance reporting

Do not assume a particular warehouse technology unless already defined by the architecture.

==================================================
ANALYTICS RECONCILIATION
========================

Create reconciliation jobs capable of detecting mismatches between:

- raw event counts
- aggregate counters
- materialized analytics tables
- creator dashboards
- advertising metrics
- commerce metrics

Reconciliation must be observable.

Do not directly rewrite source financial records to correct analytics discrepancies.

==================================================
MILESTONE 48 — MULTI-REGION AND DISASTER RECOVERY
==================================================

Finalize backend behavior for a global deployment model.

The architecture must support:

- regional API instances
- regional application workers
- geographically distributed clients
- region-aware routing
- data locality rules
- primary/replica database topologies
- read replicas
- regional caches
- replicated event streams
- cross-region event delivery
- failover
- degraded operation

Define which data is:

- region-local
- globally replicated
- eventually consistent
- strongly consistent
- user-home-region anchored
- globally authoritative

Do not pretend that every operation is globally strongly consistent.

Explicitly document consistency guarantees.

==================================================
CROSS-REGION IDENTITY
=====================

Identity must remain globally unique.

Use stable IDs that are not generated from region-local numeric sequences unless collision resistance is guaranteed.

Session validation must remain correct during regional failover.

Security-sensitive events must be replicated reliably.

==================================================
CROSS-REGION SOCIAL GRAPH
=========================

Follow relationships and blocks must have clear consistency semantics.

Blocks and privacy restrictions require stronger consistency guarantees than recommendation counters.

Do not allow stale privacy state to expose protected content.

==================================================
CROSS-REGION CONTENT
====================

Content metadata and media storage must support regional access.

Media remains stored through the S3 abstraction.

CloudFront or equivalent delivery must not bypass authorization requirements for private content.

Signed URLs or equivalent access controls must be used where appropriate.

==================================================
DISASTER RECOVERY
=================

Define and implement backend mechanisms for:

- database backup validation
- restore verification
- point-in-time recovery procedures
- event replay
- queue recovery
- search reindexing
- cache reconstruction
- derived-state rebuilding
- media metadata reconstruction
- cross-region failover

Create operational scripts or backend tooling where appropriate.

Do not create fake backup systems.

Where actual infrastructure automation belongs to Terraform/Kubernetes/CI/CD, create only the application-level contracts and operational hooks required by the backend.

==================================================
MILESTONE 49 — PERFORMANCE AND RESILIENCE
==========================================

Perform a final performance-oriented pass across all backend domains.

Identify and eliminate:

- N+1 database queries.
- Unbounded pagination.
- Unbounded query results.
- Synchronous expensive work.
- Duplicate external requests.
- Excessive serialization.
- Excessive Redis calls.
- Duplicate event publication.
- Duplicate job execution.
- Unnecessary search requests.
- Repeated permission queries.
- Excessive database transactions.
- Hot keys.
- Cache stampedes.
- Event consumer bottlenecks.

Implement:

- cursor pagination
- bounded page sizes
- request timeouts
- dependency timeouts
- circuit breakers where appropriate
- retry budgets
- exponential backoff
- jitter
- bulkheads
- concurrency controls
- queue concurrency limits
- dead-letter processing
- backpressure
- graceful degradation

Never retry blindly.

Never retry non-idempotent operations without an idempotency strategy.

==================================================
DATABASE PERFORMANCE
====================

Review indexes across all Prisma models.

Create indexes for:

- frequently filtered columns
- foreign keys where needed
- composite query patterns
- createdAt sorting
- chronological feed retrieval
- unread message retrieval
- notification retrieval
- moderation case queues
- creator analytics
- advertising event processing
- commerce transaction retrieval

Remove redundant indexes where justified.

Avoid over-indexing high-write tables.

Review:

- query plans
- slow queries
- lock contention
- long transactions
- pagination efficiency

Use raw SQL only when Prisma cannot safely express an essential optimized query and encapsulate it behind a repository or dedicated data-access abstraction.

==================================================
REDIS PERFORMANCE
=================

Audit Redis usage.

Prevent:

- unbounded keys
- infinite TTLs for temporary data
- key explosion
- hot keys
- stampedes
- race conditions
- inconsistent invalidation

All temporary data must have explicit TTL policy.

Use atomic operations when state transitions require them.

==================================================
EVENT SYSTEM PERFORMANCE
========================

Audit Kafka/Redpanda topics.

Ensure:

- partition keys are intentional
- consumers are idempotent
- consumer lag is measurable
- retries are bounded
- dead-letter handling exists
- poison messages cannot permanently block partitions
- schema versions are explicit

==================================================
QUEUE PERFORMANCE
=================

Audit BullMQ jobs.

Every job must define:

- payload
- queue
- attempts
- backoff
- timeout
- concurrency expectations
- idempotency key where required
- dead-letter/recovery strategy

Jobs that trigger external side effects must be idempotent.

==================================================
LOAD SHEDDING
=============

Implement graceful load shedding strategies for:

- expensive search
- recommendation generation
- analytics processing
- media metadata inspection
- non-critical notifications
- background recommendations
- trend calculations

Critical functionality must remain available when non-critical dependencies degrade.

==================================================
DEGRADED MODE
=============

Define backend degradation behavior for:

- Redis unavailable
- Kafka unavailable
- OpenSearch unavailable
- push provider unavailable
- email provider unavailable
- object storage unavailable
- recommendation service unavailable
- analytics pipeline unavailable

Distinguish:

- hard dependency
- soft dependency
- eventually consistent dependency

Do not make every dependency a hard dependency.

==================================================
MILESTONE 50 — FINAL BACKEND INTEGRATION AND RELEASE READINESS
===============================================================

Perform a final repository-wide backend engineering pass.

Do not rewrite working code unnecessarily.

Inspect every backend module generated in previous volumes.

Validate:

- module dependency graph
- imports
- exports
- provider registration
- NestJS module configuration
- Prisma models
- Prisma migrations
- DTOs
- entities
- repositories
- services
- use cases
- controllers
- guards
- interceptors
- pipes
- exception filters
- event publishers
- event consumers
- queue processors
- WebSocket gateways
- scheduled jobs
- configuration
- logging
- metrics
- tracing
- tests

==================================================
API CONTRACT AUDIT
==================

Every HTTP endpoint must define:

- method
- route
- authentication requirement
- authorization requirement
- request validation
- request schema
- response schema
- status codes
- error behavior
- pagination where applicable
- rate limits where applicable
- idempotency behavior where applicable

Ensure endpoint naming is consistent.

Ensure REST semantics are consistent.

Ensure errors use the established error contract.

Do not leak internal exception details.

==================================================
WEBSOCKET CONTRACT AUDIT
========================

Every WebSocket event must define:

- client-to-server event
- server-to-client event
- payload schema
- authentication requirements
- authorization requirements
- room semantics
- ordering requirements
- retry behavior
- duplicate handling

Ensure unauthorized users cannot subscribe to protected rooms.

==================================================
EVENT CONTRACT AUDIT
====================

Every Kafka/Redpanda event must define:

- event name
- version
- event ID
- timestamp
- producer
- aggregate reference
- correlation ID
- causation ID where needed
- payload schema
- retention expectations
- compatibility policy

Event consumers must safely process duplicate events.

==================================================
PRIVACY FINAL AUDIT
===================

Perform a complete privacy audit.

Verify:

- private accounts remain private
- blocked users cannot bypass restrictions
- restricted users cannot access protected data
- deleted accounts are correctly handled
- deleted content is removed from discovery paths
- message privacy is preserved
- analytics do not leak private content
- search does not expose protected content
- logs do not contain secrets
- logs do not contain unnecessary sensitive personal data
- event payloads do not contain forbidden private information
- moderation data is properly access-controlled
- export flows respect authorization
- deletion workflows cover derived stores

==================================================
SECURITY FINAL AUDIT
====================

Review:

- authentication
- authorization
- session management
- password handling
- token validation
- refresh-token handling
- CSRF where applicable
- CORS
- SSRF
- SQL injection
- command injection
- path traversal
- unsafe file processing
- malicious media
- MIME validation
- upload size limits
- rate limiting
- account enumeration
- brute-force protection
- webhook authentication
- signature validation
- secret management
- audit logging
- privilege escalation
- insecure direct object references
- WebSocket authorization
- queue poisoning
- event injection
- search injection
- open redirects where applicable

All user-controlled identifiers must be authorization-checked.

Never rely solely on obscurity of IDs.

==================================================
OBSERVABILITY FINAL AUDIT
=========================

Every important workflow must expose:

Metrics:

- request count
- latency
- errors
- throughput
- cache hits/misses
- queue depth
- queue lag
- event lag
- database latency
- search latency
- WebSocket connection count
- notification delivery success
- media processing latency
- moderation processing latency

Traces:

- HTTP requests
- async workflows
- queue processing
- event consumption
- critical database operations
- external provider calls

Logs:

- structured JSON
- correlation ID
- trace ID
- request ID
- user-safe context
- no secrets
- no unnecessary private content

==================================================
SLO/SLI DEFINITIONS
===================

Define measurable SLIs/SLOs for:

- authentication
- API availability
- API latency
- feed generation
- content publication
- media processing
- messaging send
- notification delivery
- search
- moderation processing
- queue processing
- event processing
- creator analytics
- commerce operations

Avoid arbitrary values unless the architecture has already established targets.

Where targets are not defined, create configurable operational thresholds rather than hard-coding assumptions into application logic.

==================================================
TESTING REQUIREMENTS
====================

Complete the backend test strategy.

Unit tests must cover:

- domain rules
- authorization decisions
- privacy policies
- visibility rules
- state transitions
- fraud decisions
- anti-abuse decisions
- financial calculations
- idempotency
- pagination
- validation

Integration tests must cover:

- PostgreSQL repositories
- Prisma transactions
- Redis coordination
- Kafka event publishing
- event consumers
- BullMQ processors
- search indexing
- storage integration boundaries
- WebSocket gateways
- push notification adapters
- webhook verification

End-to-end tests must cover:

- registration
- login
- profile creation
- private account follow request
- accept follow request
- publish post
- publish reel
- story workflow
- engagement workflow
- feed retrieval
- search
- messaging
- reporting
- moderation
- privacy export
- account deletion
- notification delivery
- creator monetization
- commerce workflow
- fraud rejection
- anti-abuse restrictions

==================================================
DISTRIBUTED SYSTEM TESTING
==========================

Add tests for:

- duplicate events
- duplicate jobs
- out-of-order events
- delayed events
- missing events
- consumer retries
- dead-letter recovery
- partial failures
- transaction rollback
- Redis race conditions
- cache inconsistency
- search lag
- eventual consistency
- provider timeout
- provider failure
- regional failover behavior where testable

==================================================
PERFORMANCE TESTS
=================

Add load/performance test definitions for:

- authentication
- feed
- Explore
- Reels
- search
- notifications
- messaging
- media upload initialization
- engagement endpoints
- moderation queues
- analytics ingestion

Do not generate meaningless benchmark tests.

Design scenarios around realistic read/write patterns and concurrency.

==================================================
DATABASE MIGRATION FINALIZATION
===============================

Review all migrations.

Ensure:

- deterministic ordering
- safe deployment
- backward compatibility
- rollback considerations
- indexes are intentional
- foreign keys are correct
- unique constraints are correct
- nullable fields have meaningful semantics
- soft-delete behavior is consistent
- audit fields exist where needed

Avoid destructive migrations that would cause production outages without an explicit migration strategy.

==================================================
CONFIGURATION FINALIZATION
==========================

Centralize configuration.

Required configuration categories include:

- application
- database
- Redis
- Kafka/Redpanda
- BullMQ
- storage
- CDN
- search
- push providers
- email
- payments
- commerce
- fraud
- anti-abuse
- observability
- feature flags
- regional settings

Validate configuration at startup.

Fail fast for missing required secrets/configuration.

Never log secret values.

==================================================
DOCUMENTATION FINALIZATION
==========================

Generate/update:

- README
- backend architecture overview
- domain map
- module map
- API documentation
- event catalog
- queue catalog
- WebSocket event catalog
- configuration documentation
- local development instructions
- testing instructions
- migration instructions
- troubleshooting guide
- production readiness checklist
- incident-response guidance
- data lifecycle documentation
- privacy/deletion documentation
- disaster recovery documentation

Documentation must match the actual implementation.

==================================================
BACKEND PROJECT INDEX
=====================

Create a final authoritative backend index.

The index must map:

Domain
→ Module
→ Folder
→ Main responsibility
→ Database models
→ APIs
→ Events
→ Queues
→ External dependencies
→ Redis usage
→ Search usage
→ Security boundaries
→ Tests

This index must make the repository navigable by another senior engineer without requiring inference.

==================================================
ARCHITECTURAL CONSISTENCY RULES
===============================

Across every module:

Do not duplicate business rules.

Do not duplicate authorization logic.

Do not duplicate visibility logic.

Do not duplicate privacy logic.

Do not duplicate idempotency logic inconsistently.

Do not introduce circular dependencies.

Do not put database queries directly inside controllers.

Do not put transport-specific logic inside domain entities.

Do not couple domain logic directly to AWS SDKs, payment vendors, push vendors, or search clients.

Use interfaces and adapters.

==================================================
FINAL CODE QUALITY BAR
======================

Every generated implementation must be:

- production-oriented
- typed
- validated
- tested
- observable
- secure
- maintainable
- horizontally scalable
- failure-aware
- idempotent where required
- backward-compatible

No TODOs.

No placeholders.

No pseudo-code.

No fake APIs.

No mock business logic in production modules.

No hard-coded credentials.

No unexplained magic constants where configuration is required.

No silent error swallowing.

No catch blocks that simply ignore failures.

No unnecessary rewrites.

==================================================
IMPLEMENTATION ORDER
====================

Execute the milestones in this exact sequence:

1. Milestone 41
2. Milestone 42
3. Milestone 43
4. Milestone 44
5. Milestone 45
6. Milestone 46
7. Milestone 47
8. Milestone 48
9. Milestone 49
10. Milestone 50

Within each milestone:

1. Inspect existing repository structure.
2. Reuse existing abstractions.
3. Identify dependencies.
4. Implement database changes.
5. Implement domain/application logic.
6. Implement repositories.
7. Implement API contracts.
8. Implement event publishers.
9. Implement event consumers.
10. Implement background jobs.
11. Implement cache behavior.
12. Implement security rules.
13. Implement observability.
14. Implement tests.
15. Update documentation.
16. Validate integration with previously implemented modules.

==================================================
BACKWARD COMPATIBILITY
======================

Never break already-implemented APIs without an explicit versioning strategy.

Never silently change event schemas.

Never silently change database semantics.

Never silently alter visibility behavior.

Never silently modify authorization behavior.

When extending an existing contract:

- preserve existing fields
- preserve existing semantics
- add optional fields when possible
- version breaking changes
- update tests

==================================================
NO FRONTEND WORK
================

This volume is BACKEND ONLY.

Do not implement:

- Next.js pages
- React components
- Tailwind UI
- React Native screens
- Expo UI
- mobile navigation
- frontend state management
- frontend styling

The backend must expose the contracts required by those future layers.

==================================================
NO INFRASTRUCTURE WORK
======================

Do not implement:

- Terraform
- Kubernetes manifests
- Helm charts
- AWS networking
- CI/CD pipelines
- production cloud provisioning

You may provide backend operational contracts and configuration requirements that the future infrastructure prompts will consume.

==================================================
FINAL ACCEPTANCE CRITERIA
=========================

The backend is considered complete only when:

- all domains are integrated;
- all critical workflows are implemented;
- privacy boundaries are enforced;
- authorization is enforced;
- event-driven workflows are idempotent;
- background jobs are retry-safe;
- feed/recommendation/search consistency is handled;
- anti-abuse infrastructure exists;
- fraud infrastructure exists;
- creator monetization foundations exist;
- commerce transaction foundations exist;
- analytics event boundaries exist;
- multi-region behavior is explicitly modeled;
- disaster-recovery mechanisms are documented and testable;
- performance bottlenecks have been addressed;
- observability is complete;
- security has been audited;
- tests cover critical paths and failure paths;
- APIs are documented;
- events are documented;
- queues are documented;
- migrations are valid;
- configuration is validated;
- repository structure is coherent;
- the backend can serve as the stable contract for the future frontend, mobile, infrastructure, and DevOps phases.

==================================================
OUTPUT FORMAT
=============

For every implementation step:

1. State the milestone being implemented.
2. Briefly state the affected domains.
3. Inspect the current repository before changing anything.
4. Create or modify only the files required.
5. Output complete file contents for every newly created or changed file.
6. Never output unchanged files.
7. Explain important architectural decisions briefly.
8. List migrations created or modified.
9. List API endpoints added or changed.
10. List events added or changed.
11. List queues/jobs added or changed.
12. List tests added.
13. Run validation/build/test commands where available.
14. Fix discovered issues before proceeding.
15. Maintain the repository in a buildable state after every milestone.

Do not stop at architectural discussion.

Implement the actual backend.

Begin with MILESTONE 41 — PLATFORM-WIDE DOMAIN ORCHESTRATION.
