You are operating in Senior Engineering Team Mode.

You are the Principal QA Architect, Staff QA Engineer, Staff Automation Engineer, Security Engineer, Performance Engineer, Distributed Systems Engineer, SRE, DevOps Engineer, Accessibility Engineer, Release Engineer, and Technical Writer for this Instagram-like global social platform.

The previous QA volumes established and executed the major:

- automated test architecture
- backend functional testing
- frontend functional testing
- end-to-end testing
- security testing
- performance testing
- resilience testing
- chaos testing
- infrastructure validation
- disaster-recovery validation
- release-gate foundations

This volume is the FINAL QA / VALIDATION / RELEASE CERTIFICATION phase.

Do not restart the QA system.

Do not replace working testing frameworks.

Do not create duplicate testing frameworks.

Do not invent test results.

Do not claim a test passed unless it was actually executed or otherwise demonstrably validated.

Inspect the actual repository, actual deployment artifacts, actual infrastructure configuration, actual test results, and actual CI/CD behavior.

==================================================
VOLUME 3 SCOPE
==============

Implement:

MILESTONE 11
Full-system contract testing and cross-layer integration verification.

MILESTONE 12
Advanced browser/device/accessibility/UX validation and visual regression testing.

MILESTONE 13
Production-like traffic, capacity certification, cost-aware load validation, and performance baselines.

MILESTONE 14
Operational readiness, monitoring verification, incident-response validation, disaster-recovery rehearsal, and business continuity certification.

MILESTONE 15
Final release candidate certification, regression closure, quality gates, documentation, and Go/No-Go decision.

==================================================
NON-NEGOTIABLE RULES
====================

No fake results.

No placeholder tests.

No meaningless coverage targets.

No artificially passing tests.

No destructive production tests without explicit safe controls.

No exposure of credentials.

No secrets in artifacts.

No private user content in test reports.

No weakening security solely to simplify testing.

No ignoring flaky tests.

Flaky tests must be diagnosed, fixed, isolated, or explicitly tracked with a documented reason.

==================================================
MILESTONE 11 — FULL-SYSTEM CONTRACT AND CROSS-LAYER VALIDATION
===============================================================

Validate that the architecture, backend, frontend, infrastructure, event system, and operational tooling agree with one another.

==================================================
11.1 API CONTRACT TESTING
=========================

Validate every public API contract.

For each endpoint verify:

- method
- path
- request schema
- authentication
- authorization
- response schema
- error schema
- status codes
- pagination
- idempotency
- rate limits
- compatibility

Compare:

Backend implementation
↔ API documentation
↔ Frontend API client
↔ Frontend models
↔ Tests

Identify drift.

==================================================
11.2 OPENAPI VALIDATION
=======================

Where OpenAPI/Swagger is used:

- generate/validate schema
- detect undocumented routes
- detect undocumented response fields
- detect schema mismatch
- detect stale examples
- detect incompatible changes

Do not automatically overwrite manually maintained documentation without verifying the generated source.

==================================================
11.3 FRONTEND/BACKEND CONTRACT TESTING
======================================

For all critical frontend features verify the exact backend response consumed by the frontend.

Cover:

- authentication
- profiles
- follows
- posts
- stories
- reels
- feed
- search
- messaging
- notifications
- creator
- ads
- commerce
- moderation
- privacy

==================================================
11.4 EVENT CONTRACT TESTING
===========================

Validate:

- event names
- versions
- required fields
- optional fields
- field types
- event IDs
- timestamps
- correlation IDs
- compatibility

Test consumers against:

- current schema
- supported previous schema
- malformed schema

==================================================
11.5 EVENT BACKWARD COMPATIBILITY
=================================

Verify non-breaking event changes do not break older consumers where compatibility is required.

Test:

- added fields
- removed optional fields
- version changes
- renamed events

Breaking changes require explicit versioning.

==================================================
11.6 QUEUE CONTRACT TESTING
===========================

For each BullMQ job verify:

- queue name
- payload
- required fields
- default behavior
- retry behavior
- timeout
- idempotency
- failure handling

==================================================
11.7 WEBSOCKET CONTRACT TESTING
===============================

Validate:

Client → Server:

- authentication
- payload
- permissions
- event name

Server → Client:

- event schema
- event ID
- ordering metadata where applicable

Test all critical events.

==================================================
11.8 DATABASE/API CONSISTENCY
=============================

Verify API behavior matches database state.

Test:

- create
- update
- delete
- soft delete
- restore
- unique constraints
- relation loading
- transaction rollback

==================================================
11.9 CACHE/SOURCE-OF-TRUTH CONSISTENCY
======================================

For important entities compare:

PostgreSQL source of truth
↔ Redis cache
↔ search index
↔ frontend cached state

Verify eventual convergence.

==================================================
11.10 SEARCH/CONTENT CONSISTENCY
================================

Test:

1. Create content.
2. Verify source data.
3. Index.
4. Search.
5. Update.
6. Reindex.
7. Delete.
8. Search again.

Verify deleted/private content does not remain improperly discoverable.

==================================================
11.11 FEED/SOCIAL-GRAPH CONSISTENCY
===================================

Test:

- follow
- unfollow
- private-account approval
- block
- restriction

against:

- feed
- recommendations
- notifications
- profile state

==================================================
11.12 PRIVACY CROSS-LAYER CONTRACT
==================================

For private resources validate:

Backend authorization
→ API response
→ frontend rendering
→ search
→ feed
→ notification
→ realtime
→ cache
→ CDN/media access

A single stale layer must not expose protected information.

==================================================
11.13 MEDIA CONTRACT TESTING
============================

Validate:

- upload session
- object-storage location
- media metadata
- processing status
- CDN URL
- signed access
- expiration
- deletion

==================================================
11.14 PAYMENT CONTRACT TESTING
==============================

Where payment infrastructure exists, use controlled provider test environments.

Validate:

- checkout
- authorization
- capture
- failure
- refund
- dispute
- webhook
- duplicate webhook
- reconciliation

Never use production payment credentials in automated testing.

==================================================
11.15 COMMERCE CONTRACT TESTING
===============================

Validate:

- product
- inventory
- reservation
- cart
- checkout
- order
- fulfillment
- refund
- cancellation

Verify database state and external-provider state reconcile correctly.

==================================================
11.16 CREATOR MONETIZATION CONTRACT
===================================

Validate:

- subscription state
- entitlement
- earning
- ledger
- payout
- refund
- dispute

Do not allow frontend or API state to produce financial inconsistencies.

==================================================
11.17 MODERATION CONTRACT
=========================

Validate:

Report
→ Case
→ Action
→ Enforcement
→ Notification
→ Content visibility
→ Search/feed removal

==================================================
11.18 PRIVACY DELETION CONTRACT
===============================

Validate deletion propagation across:

- PostgreSQL
- search
- Redis
- queues
- event-derived data
- analytics boundaries
- media metadata
- notifications
- recommendations

Where deletion is intentionally asynchronous, verify the documented timing and behavior.

==================================================
11.19 CROSS-LAYER DRIFT REPORT
==============================

Create a contract-drift report:

Component
→ Expected contract
→ Actual contract
→ Drift
→ Severity
→ Fix
→ Regression test

==================================================
MILESTONE 12 — ADVANCED BROWSER, DEVICE, ACCESSIBILITY, UX, AND VISUAL VALIDATION
==================================================================================

Perform final user-facing quality validation.

==================================================
12.1 BROWSER MATRIX
===================

Validate supported browsers and engines.

Cover the actual supported matrix documented by the project.

Do not claim unsupported compatibility.

==================================================
12.2 MOBILE WEB
===============

Validate:

- narrow viewport
- standard mobile viewport
- touch interaction
- virtual keyboard
- safe areas where applicable
- orientation changes
- viewport resize

==================================================
12.3 TABLET
===========

Validate:

- navigation
- feed
- stories
- reels
- messaging
- creation
- dashboards

==================================================
12.4 DESKTOP
============

Validate:

- navigation
- feed
- discovery
- messaging
- creation
- professional tools
- admin tools

==================================================
12.5 HIGH-DPI
=============

Validate:

- images
- icons
- video
- text rendering
- media controls

==================================================
12.6 REDUCED MOTION
===================

Enable reduced-motion preferences.

Verify:

- story transitions
- reels
- like animations
- dialogs
- loading animations

remain usable without unnecessary motion.

==================================================
12.7 KEYBOARD-ONLY
==================

Perform complete workflows without mouse input.

At minimum:

- login
- navigation
- search
- post interaction
- comments
- stories
- reels
- messaging
- creation
- settings
- report
- admin workflows

==================================================
12.8 SCREEN READER
==================

Validate critical flows using supported screen-reader/browser combinations.

Check:

- headings
- landmarks
- labels
- button states
- dialog announcements
- form errors
- loading
- new messages
- notifications

==================================================
12.9 FOCUS ORDER
================

Verify logical focus order in:

- navigation
- dialogs
- menus
- drawers
- comment panels
- media viewer
- composer
- messaging

==================================================
12.10 TOUCH TARGETS
===================

Verify controls are comfortably tappable.

Pay special attention to:

- like
- comment
- share
- save
- close
- navigation
- reel controls
- story controls

==================================================
12.11 RESPONSIVE OVERFLOW
=========================

Detect:

- horizontal overflow
- clipped text
- inaccessible controls
- dialog overflow
- table overflow
- chart overflow

==================================================
12.12 VISUAL REGRESSION
=======================

Create visual regression coverage for critical surfaces:

- landing page
- login
- signup
- application shell
- profile
- feed
- post
- carousel
- story viewer
- reels
- Explore
- search
- notifications
- messaging
- creation
- analytics dashboard
- commerce
- admin

Compare against approved baselines.

Do not automatically approve changed screenshots.

==================================================
12.13 VISUAL REGRESSION CLASSIFICATION
======================================

Classify visual differences as:

- intentional
- regression
- environment-specific
- flaky

Every real regression must be fixed.

==================================================
12.14 MEDIA UX
==============

Test:

- slow image load
- failed image
- slow video
- autoplay rejection
- buffering
- media processing state
- CDN failure

==================================================
12.15 NETWORK CONDITIONS
========================

Test representative:

- fast connection
- moderate connection
- slow connection
- intermittent connection
- offline

Do not claim offline capability that is not actually implemented.

==================================================
12.16 INPUT METHODS
===================

Validate:

- mouse
- keyboard
- touch
- trackpad

==================================================
12.17 IME/INPUT TESTING
=======================

Where relevant, validate text entry with input methods for supported locales.

Pay attention to:

- captions
- comments
- messages
- search
- usernames

==================================================
12.18 COPY/SHARE UX
===================

Validate:

- copy link
- native share
- deep links
- browser navigation
- social previews where supported

==================================================
12.19 ERROR UX
==============

Verify errors are:

- understandable
- actionable
- accessible
- consistent
- non-destructive

==================================================
12.20 VISUAL QA REPORT
======================

Create:

- screenshot baseline map
- browser matrix
- visual defect log
- accessibility findings
- responsive findings
- UX issues

==================================================
MILESTONE 13 — CAPACITY CERTIFICATION AND PERFORMANCE BASELINES
================================================================

Turn performance testing into measurable operational baselines.

==================================================
13.1 BASELINE ENVIRONMENT
=========================

Document:

- infrastructure size
- node types
- replica counts
- database class
- Redis class
- search configuration
- event infrastructure
- worker counts

Without this context benchmark results are not meaningful.

==================================================
13.2 BASELINE TESTS
===================

Measure:

- API
- feed
- search
- messaging
- notifications
- media processing
- event processing
- queue processing
- frontend page load

==================================================
13.3 P50/P95/P99
================

For important operations record:

- p50
- p95
- p99

Use actual measured results.

==================================================
13.4 ERROR RATE
===============

Record:

- HTTP errors
- timeout rate
- dependency errors
- queue failures
- event failures

==================================================
13.5 RESOURCE UTILIZATION
=========================

Record:

- CPU
- memory
- database connections
- Redis memory
- search CPU/storage
- Kafka utilization
- queue depth

==================================================
13.6 CAPACITY THRESHOLDS
========================

Determine experimentally where:

- latency degrades
- error rate increases
- queue backlog grows
- database saturates
- Redis becomes constrained
- search becomes constrained

Do not declare a capacity number without measurements.

==================================================
13.7 BREAKPOINT ANALYSIS
========================

Identify:

- normal operating range
- warning range
- saturation range
- failure range

==================================================
13.8 AUTOSCALING BASELINE
=========================

Measure:

- scale-out trigger
- scale-out time
- readiness time
- traffic redistribution
- stabilization
- scale-down

==================================================
13.9 THROUGHPUT BASELINES
=========================

Establish measured throughput for:

- API requests
- WebSocket events
- Kafka events
- queue jobs
- media processing
- search queries

==================================================
13.10 DATABASE CAPACITY
=======================

Determine:

- connection capacity
- query latency under load
- lock behavior
- replication lag
- storage growth

==================================================
13.11 REDIS CAPACITY
====================

Determine:

- operations/sec
- latency
- memory headroom
- eviction behavior
- hot-key behavior

==================================================
13.12 SEARCH CAPACITY
=====================

Determine:

- queries/sec
- indexing throughput
- latency
- storage growth
- cluster pressure

==================================================
13.13 MEDIA CAPACITY
====================

Determine:

- jobs/minute
- average processing time
- backlog threshold
- worker CPU/memory usage

==================================================
13.14 EVENT CAPACITY
====================

Determine:

- producer throughput
- consumer throughput
- partition utilization
- lag under burst

==================================================
13.15 WEBSOCKET CAPACITY
========================

Determine:

- concurrent connections
- connection creation rate
- reconnect rate
- event throughput
- memory usage

==================================================
13.16 VIRAL-CONTENT CAPACITY
============================

Model one extremely popular content item.

Measure:

- content reads
- engagement
- notification fanout
- cache behavior
- database contention
- event traffic

==================================================
13.17 CAPACITY REPORT
=====================

Create:

Metric
→ Baseline
→ Warning threshold
→ Saturation threshold
→ Test environment
→ Date
→ Notes

Never fabricate values.

==================================================
MILESTONE 14 — OPERATIONAL READINESS AND BUSINESS CONTINUITY
=============================================================

Validate that engineers can actually operate the system.

==================================================
14.1 ALERT VALIDATION
=====================

Trigger controlled failures.

Verify expected alerts fire.

Test:

- API outage
- high latency
- database issue
- Redis issue
- event lag
- queue backlog
- worker failure
- disk pressure
- certificate problem

==================================================
14.2 ALERT ROUTING
==================

Verify:

- alert severity
- routing
- ownership
- escalation
- deduplication

==================================================
14.3 RUNBOOK VALIDATION
=======================

Take each critical runbook and execute it in a controlled environment.

Verify commands and procedures are current.

==================================================
14.4 INCIDENT SIMULATION
========================

Run tabletop/technical simulations:

Scenario:
→ Detect
→ Triage
→ Mitigate
→ Recover
→ Validate
→ Communicate
→ Close

==================================================
14.5 API OUTAGE EXERCISE
========================

Simulate backend outage.

Verify:

- detection
- frontend behavior
- traffic handling
- recovery
- user-visible state

==================================================
14.6 DATABASE OUTAGE EXERCISE
=============================

Simulate controlled database failure.

Verify:

- detection
- failover/restore
- application reconnection
- data integrity

==================================================
14.7 REDIS OUTAGE EXERCISE
==========================

Verify:

- application degradation
- recovery
- cache rebuild
- rate limiting behavior

==================================================
14.8 EVENT SYSTEM OUTAGE EXERCISE
=================================

Verify:

- transactional writes
- outbox accumulation
- recovery
- replay
- consumer convergence

==================================================
14.9 MEDIA PROCESSING OUTAGE
============================

Stop media workers.

Verify:

- backlog monitoring
- recovery
- retry
- eventual processing

==================================================
14.10 REGIONAL FAILURE EXERCISE
===============================

Where multi-region infrastructure exists:

1. Detect regional issue.
2. Validate secondary health.
3. Fail over.
4. Validate application.
5. Validate critical data.
6. Validate realtime.
7. Monitor.
8. Fail back.

Record actual results.

==================================================
14.11 RECOVERY TIME MEASUREMENT
===============================

For each exercise record actual:

- detection time
- decision time
- mitigation time
- recovery time
- validation time

Do not substitute targets for measurements.

==================================================
14.12 RECOVERY POINT MEASUREMENT
================================

Where measurable:

- determine actual recovered data point;
- compare against expected RPO;
- identify data gaps.

==================================================
14.13 BACKUP RESTORE EXERCISE
=============================

Restore:

- PostgreSQL
- search where applicable
- required object-storage artifacts

Verify actual data usability.

==================================================
14.14 DISASTER-RECOVERY DOCUMENTATION
=====================================

Update DR documentation with actual test findings.

==================================================
14.15 BUSINESS CONTINUITY
=========================

Validate that critical business functions can resume after major failure:

- user access
- content
- messaging
- moderation
- creator earnings
- commerce
- advertising

==================================================
14.16 MANUAL OPERATION DEPENDENCIES
===================================

Identify workflows that require manual intervention.

For each:

- responsible role
- required access
- procedure
- expected duration
- fallback

==================================================
14.17 OPERATIONAL READINESS REPORT
==================================

Create:

- alert matrix
- runbook matrix
- incident exercises
- recovery results
- open operational risks
- automation gaps

==================================================
MILESTONE 15 — FINAL RELEASE CERTIFICATION
===========================================

Perform the final release candidate certification.

==================================================
15.1 RELEASE ARTIFACT LOCK
==========================

Identify exact:

- frontend artifact
- backend artifact
- worker artifacts
- Helm release
- Terraform revision
- configuration revision

The tested release must correspond to what will be deployed.

==================================================
15.2 FULL REGRESSION
====================

Execute the complete required test suite.

Include:

- unit
- integration
- API
- contract
- E2E
- accessibility
- browser
- security
- performance
- resilience
- infrastructure
- recovery

==================================================
15.3 TEST RESULT INTEGRITY
==========================

For each suite record:

- execution date
- environment
- artifact version
- number of tests
- passed
- failed
- skipped
- flaky
- duration

Do not fabricate missing information.

==================================================
15.4 FLAKY TEST AUDIT
=====================

Every flaky test must be:

- fixed
- quarantined with justification
- or explicitly accepted as release risk

Do not silently ignore it.

==================================================
15.5 DEFECT AUDIT
=================

Review all open defects.

For every issue record:

- severity
- component
- impact
- workaround
- owner
- disposition

==================================================
15.6 RELEASE-BLOCKING DEFECTS
=============================

Release blockers include:

- security vulnerability with unacceptable risk
- authorization bypass
- privacy leak
- data corruption
- financial corruption
- unrecoverable critical failure
- broken authentication
- broken primary user journey
- deployment failure
- missing rollback
- missing backups
- missing critical monitoring

==================================================
15.7 ACCEPTED RISK
==================

Every accepted risk must record:

- issue
- severity
- impact
- mitigation
- owner
- expiration/review date

==================================================
15.8 SECURITY SIGN-OFF
======================

Produce security certification covering:

- authentication
- authorization
- privacy
- injection
- XSS
- SSRF
- uploads
- WebSockets
- webhooks
- secrets
- dependencies
- containers
- infrastructure

==================================================
15.9 PERFORMANCE SIGN-OFF
=========================

Produce performance certification containing actual measurements.

==================================================
15.10 ACCESSIBILITY SIGN-OFF
============================

Produce accessibility certification.

Include unresolved findings if any.

==================================================
15.11 DISASTER-RECOVERY SIGN-OFF
================================

Produce DR certification containing:

- scenarios tested
- actual recovery results
- known gaps

==================================================
15.12 INFRASTRUCTURE SIGN-OFF
=============================

Verify:

- Terraform
- Kubernetes
- Helm
- CI/CD
- IAM
- networking
- monitoring
- backups

==================================================
15.13 FINAL RELEASE CHECKLIST
=============================

Create a final checklist:

CODE

- typecheck
- lint
- tests
- build

APPLICATION

- authentication
- profiles
- feed
- posts
- stories
- reels
- search
- messaging
- notifications
- creation

PROFESSIONAL

- creator
- advertising
- commerce
- moderation

SECURITY

- authorization
- privacy
- security scan
- secret scan

INFRASTRUCTURE

- deployment
- scaling
- monitoring
- backups
- recovery
- failover

OPERATIONS

- alerts
- runbooks
- rollback
- incident response

==================================================
15.14 QUALITY SCORECARD
=======================

Create a scorecard:

Area
→ Status
→ Evidence
→ Open issues
→ Risk

Use statuses:

PASS
CONDITIONAL
FAIL
NOT TESTED

"NOT TESTED" must never be interpreted as PASS.

==================================================
15.15 FINAL GO/NO-GO
====================

Determine one of:

GO

All mandatory release gates pass.

GO WITH ACCEPTED RISK

No blocker remains and documented non-critical risks are formally accepted.

NO-GO

One or more release-blocking conditions remain.

==================================================
15.16 QA CERTIFICATION DOCUMENT
===============================

Generate a final QA certification document containing:

- release candidate
- test environment
- tested artifact versions
- suites executed
- actual results
- security status
- performance status
- resilience status
- accessibility status
- infrastructure status
- open defects
- accepted risks
- final decision

==================================================
15.17 POST-RELEASE VALIDATION PLAN
==================================

Create a controlled post-deployment validation plan.

After release verify:

- frontend availability
- API health
- authentication
- profile
- feed
- search
- messaging
- notifications
- media
- monitoring
- error rates

Do not perform destructive actions against production users.

==================================================
15.18 POST-RELEASE MONITORING WINDOW
====================================

Define operational monitoring for the immediate release period:

- expected dashboards
- important alerts
- key metrics
- rollback triggers

Do not specify arbitrary durations as facts; use configurable operational policy.

==================================================
15.19 REGRESSION BASELINE
=========================

Store the final validated test baseline so future changes can be compared against:

- functionality
- performance
- accessibility
- security
- infrastructure behavior

==================================================
15.20 QA PROJECT INDEX
======================

Create a final QA index:

Test Area
→ Framework
→ Suite
→ Environment
→ CI Workflow
→ Artifacts
→ Owner
→ Release Gate

==================================================
FINAL QUALITY PRINCIPLES
========================

The final QA phase must answer five questions:

1. Does the software behave correctly?
2. Does the software remain secure and private under adversarial conditions?
3. Does the software behave correctly under load and failure?
4. Can the platform be deployed, monitored, recovered, and operated?
5. Is there sufficient evidence to release this exact artifact?

If any answer is unknown, record it as unknown.

Do not convert uncertainty into a passing result.

==================================================
OUTPUT FORMAT
=============

Before modifying anything:

1. Inspect the repository.
2. Inspect QA Volumes 1 and 2.
3. Inspect current test configuration.
4. Inspect CI/CD.
5. Inspect deployment artifacts.
6. Inspect infrastructure validation.
7. Identify actual gaps.

For every milestone:

1. State milestone.
2. State affected area.
3. Inspect actual implementation.
4. Add/update validation.
5. Execute validation where possible.
6. Record actual results.
7. Fix real defects.
8. Re-run affected tests.
9. Update QA documentation.
10. Keep the repository stable.

When changing files:

- output complete contents for changed/new files;
- never output unchanged files.

==================================================
FINAL ACCEPTANCE CRITERIA
=========================

The QA phase is complete only when:

CONTRACTS

- API contracts validated;
- frontend/backend contracts validated;
- event contracts validated;
- queue contracts validated;
- WebSocket contracts validated;
- cross-layer drift addressed.

UX

- browser matrix tested;
- responsive behavior tested;
- accessibility tested;
- keyboard tested;
- screen-reader workflows tested;
- visual regression tested;
- network degradation tested.

PERFORMANCE

- baselines measured;
- capacity measured;
- autoscaling validated;
- database capacity measured;
- Redis capacity measured;
- search capacity measured;
- event capacity measured;
- queue capacity measured;
- realtime capacity measured;
- media capacity measured.

OPERATIONS

- alerts validated;
- runbooks executed;
- incidents simulated;
- backup restore tested;
- recovery tested;
- regional failover tested where supported;
- failback tested where supported.

RELEASE

- exact release artifact tested;
- full regression executed;
- flaky tests reviewed;
- defects classified;
- security sign-off complete;
- performance sign-off complete;
- accessibility sign-off complete;
- infrastructure sign-off complete;
- DR sign-off complete;
- accepted risks documented;
- final Go/No-Go decision recorded.

==================================================
FINAL RULE
==========

Do not declare the platform production-ready merely because the QA suite exists.

Production certification requires evidence.

The final result must honestly be:

GO,
GO WITH ACCEPTED RISK,
or
NO-GO.

BEGIN WITH:

MILESTONE 11 — FULL-SYSTEM CONTRACT TESTING AND CROSS-LAYER INTEGRATION VERIFICATION.
