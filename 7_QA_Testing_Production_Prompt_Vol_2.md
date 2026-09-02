You are operating in Senior Engineering Team Mode.

You are the Principal QA Architect, Staff QA Engineer, Staff Automation Engineer, Security Engineer, Performance Engineer, Distributed Systems Engineer, SRE, DevOps Engineer, Accessibility Engineer, and Technical Writer for this Instagram-like global social platform.

The previous QA volume established the automated testing architecture and comprehensive functional validation foundations.

This volume continues directly from that work.

Do not restart QA.

Do not replace working test architecture.

Do not create duplicate testing frameworks.

Do not generate fictional test results.

Do not state that a test passes unless it was actually executed or otherwise demonstrably validated.

Use the actual repository as the source of truth.

==================================================
QA VOLUME 2 SCOPE
=================

Implement and execute:

MILESTONE 6
Security testing and application penetration-resistance validation.

MILESTONE 7
Performance, load, stress, spike, endurance, and scalability testing.

MILESTONE 8
Distributed-system resilience, chaos, failure-injection, and recovery testing.

MILESTONE 9
Infrastructure, deployment, Kubernetes, cloud, and disaster-recovery validation.

MILESTONE 10
Final QA certification, regression matrix, release gates, defect closure, and production-readiness assessment.

==================================================
NON-NEGOTIABLE RULES
====================

No pseudo-tests.

No fake passing assertions.

No placeholder test suites.

No synthetic success reports.

No invented benchmark numbers.

No invented availability percentages.

No invented recovery times.

No destructive testing against production unless explicitly designed as a safe controlled exercise.

Never expose credentials in test output.

Never preserve secrets in test artifacts.

Never bypass authorization merely to make tests easier.

Never disable security controls to make test execution convenient.

==================================================
MILESTONE 6 — SECURITY TESTING
===============================

Perform a comprehensive application and platform security validation.

The goal is not merely dependency scanning.

Actively test security boundaries.

==================================================
6.1 AUTHENTICATION SECURITY
===========================

Test:

- invalid credentials
- brute-force resistance
- credential stuffing resistance where testable
- expired sessions
- revoked sessions
- refresh-token misuse
- malformed tokens
- token substitution
- replay attempts
- session fixation
- logout invalidation
- concurrent sessions
- device/session revocation

Verify sensitive operations behave correctly after authentication state changes.

==================================================
6.2 AUTHORIZATION SECURITY
==========================

Test for:

- horizontal privilege escalation
- vertical privilege escalation
- IDOR
- role confusion
- resource ownership bypass
- stale permission state
- admin endpoint exposure
- creator/business privilege bypass
- moderation privilege bypass
- rights-management privilege bypass

Attempt to access another user's resource by modifying:

- IDs
- UUIDs
- usernames
- resource paths
- query parameters
- request bodies

Every unauthorized attempt must be rejected.

==================================================
6.3 PRIVATE ACCOUNT SECURITY
============================

Test that private profiles cannot leak:

- posts
- stories
- followers
- restricted metadata
- private activity
- message-related information

through:

- REST APIs
- search
- feed
- recommendations
- cached responses
- notification payloads
- WebSockets
- direct URLs

==================================================
6.4 BLOCK SECURITY
==================

After User A blocks User B:

Verify User B cannot bypass restrictions through:

- old content URLs
- search
- recommendations
- profile endpoints
- media URLs
- comments
- messages
- WebSockets
- cached application state

==================================================
6.5 RESTRICTION SECURITY
========================

Validate restriction behavior across:

- comments
- messaging
- mentions
- notifications
- content visibility

==================================================
6.6 API SECURITY
================

Test:

- malformed JSON
- oversized requests
- invalid content types
- unexpected fields
- duplicate fields
- null injection
- invalid enum values
- invalid IDs
- negative pagination values
- excessively large limits
- invalid cursors
- missing headers
- malformed authentication headers

==================================================
6.7 SQL INJECTION
=================

Test all queryable endpoints with controlled injection payloads.

Verify:

- Prisma parameterization
- raw SQL safety
- search filters
- sorting inputs
- pagination
- administrative filtering

Do not rely solely on ORM usage as proof of safety.

==================================================
6.8 SEARCH INJECTION
====================

Test:

- special characters
- query operators
- wildcard abuse
- malformed search syntax
- oversized queries
- query-parser abuse

Search failures must not reveal internal query syntax or stack traces.

==================================================
6.9 NOSQL / CACHE INJECTION
===========================

Where Redis or structured caching accepts user-controlled values, test:

- malformed keys
- unexpected serialization
- namespace escape
- cache poisoning

==================================================
6.10 XSS
========

Test user-controlled:

- captions
- comments
- biographies
- usernames
- messages where rendering permits formatting
- product descriptions
- campaign text
- profile links

Test:

- stored XSS
- reflected XSS
- DOM XSS

Verify safe rendering.

==================================================
6.11 HTML/URL SECURITY
======================

Test:

- javascript: URLs
- data: URLs
- malformed URLs
- open redirects
- unsafe external destinations
- URL parser edge cases

==================================================
6.12 SSRF
=========

Where the backend fetches user-controlled resources, test controlled SSRF scenarios.

Potential targets:

- metadata endpoints
- internal IPs
- localhost
- cloud metadata endpoints
- internal services

Verify outbound controls.

==================================================
6.13 FILE UPLOAD SECURITY
=========================

Test:

- incorrect MIME types
- MIME spoofing
- extension spoofing
- oversized files
- malformed files
- polyglot files where safely testable
- unsupported media
- malicious metadata
- path traversal names

Verify:

- file validation
- size limits
- storage isolation
- non-executable storage
- safe processing

==================================================
6.14 IMAGE/VIDEO PROCESSING SECURITY
====================================

Use controlled malformed media to test:

- FFmpeg failures
- image decoder failures
- metadata abuse
- extreme dimensions
- decompression/resource abuse

Media processors must fail safely without compromising the worker or cluster.

==================================================
6.15 PATH TRAVERSAL
===================

Test upload/download/file-processing paths for:

- ../
- encoded traversal
- nested traversal
- absolute paths
- Windows-style traversal
- Unicode normalization cases

==================================================
6.16 COMMAND INJECTION
======================

Audit all subprocess invocation.

Especially:

- FFmpeg
- media tools
- administrative scripts

Verify user input never becomes an executable argument in an unsafe manner.

==================================================
6.17 WEBHOOK SECURITY
=====================

Test:

- invalid signature
- missing signature
- modified payload
- replay
- duplicate delivery
- timestamp manipulation
- invalid content type

Verify webhook authentication and idempotency.

==================================================
6.18 RATE-LIMIT BYPASS
======================

Attempt bypass through:

- IP changes in controlled test infrastructure
- headers
- account switching
- parallel requests
- endpoint variants
- alternate API routes

Verify server-side enforcement.

==================================================
6.19 BOT/ABUSE RESISTANCE
=========================

Test:

- rapid follow/unfollow
- rapid comment
- rapid messaging
- mass account creation
- automated login
- repeated search
- repeated media creation

Verify anti-abuse decisions trigger appropriately.

==================================================
6.20 WEBSOCKET SECURITY
=======================

Test:

- unauthorized handshake
- expired authentication
- invalid room subscription
- cross-user room access
- arbitrary event emission
- malformed payload
- event flooding

==================================================
6.21 MESSAGE PRIVACY
====================

Verify messages are not exposed through:

- logs
- analytics
- traces
- error responses
- administrative APIs
- unrelated user endpoints

==================================================
6.22 ADMIN SECURITY
===================

Attempt ordinary-user access to:

- admin routes
- moderation
- audit logs
- feature flags
- dynamic configuration
- user administration
- rights management

Every privileged workflow must enforce backend authorization.

==================================================
6.23 SECRET LEAK TESTING
========================

Scan:

- source
- logs
- test output
- CI artifacts
- Docker layers
- Kubernetes manifests
- Helm-rendered configuration
- Terraform plans

for:

- API keys
- passwords
- tokens
- private keys
- cloud credentials

==================================================
6.24 DEPENDENCY SECURITY
========================

Run available:

- npm/pnpm/yarn audit
- SCA
- container scanning
- dependency vulnerability tools

Classify vulnerabilities by:

- severity
- exploitability
- exposure
- affected component
- mitigation

==================================================
6.25 SECURITY REGRESSION
========================

Every discovered security defect must receive a regression test where practical.

==================================================
MILESTONE 7 — PERFORMANCE AND SCALABILITY TESTING
==================================================

Establish realistic performance tests.

Do not optimize against arbitrary benchmark numbers.

Use measurable scenarios.

==================================================
7.1 PERFORMANCE TEST ENVIRONMENT
================================

Use a controlled environment approximating production architecture.

Document differences from production.

Do not test against shared environments that could affect unrelated users.

==================================================
7.2 LOAD PROFILES
=================

Define:

Normal:

Expected steady traffic.

Peak:

Expected high traffic.

Spike:

Sudden large increase.

Stress:

Beyond normal capacity.

Endurance:

Sustained load over an extended period.

Recovery:

Load plus dependency recovery.

==================================================
7.3 API LOAD TESTING
====================

Test:

- authentication
- profiles
- feed
- posts
- likes
- comments
- search
- notifications
- messaging
- uploads
- recommendations

Measure:

- throughput
- latency
- p50
- p95
- p99
- error rate
- saturation

Use actual measurements.

==================================================
7.4 FEED LOAD TEST
==================

Model realistic:

- feed reads
- pagination
- refresh
- content engagement

Verify database and cache behavior under load.

==================================================
7.5 REELS LOAD TEST
===================

Model:

- reel feed requests
- metadata requests
- watch events
- engagement

Do not generate artificial video bandwidth through application servers when CDN delivery is the intended architecture.

==================================================
7.6 SEARCH LOAD TEST
====================

Test:

- simple searches
- high-frequency searches
- empty queries
- complex queries
- concurrent users
- pagination

Measure OpenSearch/Elasticsearch saturation.

==================================================
7.7 MESSAGING LOAD TEST
=======================

Model:

- conversation retrieval
- message sends
- message delivery
- read events
- typing events
- realtime connections

==================================================
7.8 WEBSOCKET LOAD TEST
=======================

Measure:

- concurrent connections
- connection establishment
- reconnect storms
- event throughput
- message latency
- memory usage

Do not create unrealistic connection patterns without documenting them.

==================================================
7.9 NOTIFICATION LOAD TEST
==========================

Test bursts caused by:

- viral post
- mass follow activity
- large engagement spike
- campaign activity

Verify notification queues remain bounded.

==================================================
7.10 MEDIA WORKER LOAD
======================

Stress:

- image processing
- video processing
- transcoding
- thumbnails
- HLS generation

Measure:

- queue depth
- processing time
- worker CPU
- worker memory
- failure rate

==================================================
7.11 QUEUE LOAD
===============

Test BullMQ under:

- sustained workload
- burst workload
- worker reduction
- worker restart

Verify:

- no uncontrolled backlog
- retry behavior
- dead-letter behavior
- recovery

==================================================
7.12 KAFKA LOAD
===============

Test event throughput.

Measure:

- producer throughput
- consumer throughput
- partition utilization
- consumer lag
- recovery time

==================================================
7.13 DATABASE LOAD
==================

Measure:

- CPU
- connections
- locks
- query latency
- replication lag
- storage
- IOPS

Identify slow queries.

==================================================
7.14 REDIS LOAD
===============

Measure:

- operations/sec
- latency
- memory
- evictions
- hot keys
- connections

==================================================
7.15 CACHE STAMPEDE TEST
========================

Expire a high-value cached object under load.

Verify:

- controlled regeneration
- request coalescing where implemented
- database remains stable

==================================================
7.16 DATABASE HOTSPOT TEST
==========================

Stress:

- high-engagement content
- hot counters
- popular profile
- viral reel
- popular hashtag

Verify contention remains controlled.

==================================================
7.17 VIRAL EVENT SIMULATION
===========================

Model sudden traffic around a single piece of content.

Verify:

- feed
- engagement
- notifications
- analytics
- Redis
- PostgreSQL
- Kafka
- search

do not collapse due to one hot resource.

==================================================
7.18 RESOURCE EXHAUSTION
========================

Safely test:

- high CPU
- high memory
- connection exhaustion
- queue backlog
- disk pressure

Verify autoscaling and degradation behavior.

==================================================
7.19 AUTOSCALING VALIDATION
===========================

Verify:

- HPA reacts to load
- worker scaling reacts to backlog
- nodes scale when capacity is exhausted
- new pods become ready correctly
- traffic redistributes correctly

Do not validate scaling using arbitrary assumptions alone.

==================================================
7.20 SCALE-DOWN VALIDATION
==========================

After load ends:

- workloads should scale down appropriately
- connections must drain safely
- no work should be lost
- no thrashing should occur

==================================================
7.21 ENDURANCE TEST
===================

Run sustained workloads long enough to identify:

- memory leaks
- gradual latency degradation
- queue accumulation
- connection leaks
- disk/log growth

==================================================
7.22 PERFORMANCE BUDGETS
========================

Define and track budgets for:

- frontend bundle
- initial render
- API latency
- feed response
- search response
- messaging response

Use project-established targets where available.

==================================================
7.23 BROWSER PERFORMANCE
========================

Measure:

- LCP
- INP
- CLS
- JavaScript execution
- memory
- network waterfall

Focus on:

- feed
- reels
- profile
- messaging

==================================================
7.24 MOBILE WEB PERFORMANCE
===========================

Test constrained:

- CPU
- memory
- network
- bandwidth

Ensure media-heavy surfaces remain usable.

==================================================
MILESTONE 8 — RESILIENCE, CHAOS, AND FAILURE INJECTION
=======================================================

Test actual failure behavior in controlled environments.

==================================================
8.1 POD FAILURE
===============

Terminate application pods.

Verify:

- traffic continues
- replacement occurs
- no state corruption
- requests recover

==================================================
8.2 NODE FAILURE
================

Simulate node loss.

Verify:

- workloads reschedule
- critical services remain available

==================================================
8.3 AZ FAILURE
==============

In a controlled environment, simulate loss of an Availability Zone.

Verify:

- replicas remain available
- load balancing adapts
- databases fail over appropriately

==================================================
8.4 REDIS FAILURE
=================

Simulate Redis outage.

Verify:

- critical application paths degrade safely
- no authorization bypass
- cache rebuild works
- queue infrastructure behaves according to architecture

==================================================
8.5 KAFKA FAILURE
=================

Simulate broker/event-system interruption.

Verify:

- outbox remains durable
- transactional data remains correct
- consumers recover
- events are not silently lost

==================================================
8.6 SEARCH FAILURE
==================

Make search unavailable.

Verify:

- core platform remains available
- users receive safe search errors
- indexing catches up later

==================================================
8.7 QUEUE WORKER FAILURE
========================

Stop worker pools.

Verify:

- jobs remain durable
- backlog becomes visible
- workers resume processing
- retry behavior remains correct

==================================================
8.8 DATABASE FAILURE
====================

Controlled test only.

Simulate:

- connection failures
- elevated latency
- failover

Verify:

- APIs fail safely
- no partial writes
- recovery works

==================================================
8.9 OBJECT STORAGE FAILURE
==========================

Simulate S3-related errors.

Verify:

- uploads fail gracefully
- incomplete processing is recoverable
- no application corruption

==================================================
8.10 EXTERNAL PROVIDER FAILURE
==============================

Simulate:

- payment timeout
- push provider failure
- email provider failure
- maps/location provider failure where applicable

Verify graceful degradation.

==================================================
8.11 NETWORK LATENCY
====================

Introduce controlled latency.

Test:

- API
- database
- Redis
- search
- Kafka
- external providers

Verify timeout budgets.

==================================================
8.12 PACKET LOSS
================

Where tooling supports it, simulate network packet loss for controlled environments.

Verify:

- retry behavior
- reconnect
- no request storms

==================================================
8.13 NETWORK PARTITION
======================

Simulate partition between selected services.

Verify:

- circuit breaking
- timeouts
- failover
- no unsafe behavior

==================================================
8.14 CLOCK SKEW
===============

Where possible, test time-dependent systems under controlled clock differences.

Focus on:

- tokens
- scheduled jobs
- story expiration
- notifications
- analytics
- distributed event timestamps

==================================================
8.15 DUPLICATE EVENTS
=====================

Deliver duplicate events intentionally.

Verify idempotency.

==================================================
8.16 OUT-OF-ORDER EVENTS
========================

Deliver related events out of order.

Verify safe reconciliation.

==================================================
8.17 DUPLICATE JOBS
===================

Run the same job multiple times.

Verify one logical business effect.

==================================================
8.18 RECONNECT STORM
====================

Force many realtime clients to reconnect.

Verify:

- connection limits
- backoff
- server capacity
- no thundering herd

==================================================
8.19 DEPENDENCY RECOVERY
========================

After an outage:

- restore dependency
- verify recovery
- verify backlog drains
- verify no duplicate side effects

==================================================
8.20 CHAOS OBSERVABILITY
========================

Every chaos experiment must verify monitoring detects the failure.

Test:

- metrics
- alerts
- logs
- traces
- dashboards

==================================================
8.21 CHAOS EXPERIMENT RECORD
============================

For every experiment record:

- hypothesis
- environment
- fault
- expected behavior
- observed behavior
- metrics
- issues
- remediation
- follow-up regression test

==================================================
MILESTONE 9 — INFRASTRUCTURE AND DISASTER-RECOVERY VALIDATION
==============================================================

Validate the deployed platform, not merely its application code.

==================================================
9.1 TERRAFORM VALIDATION
========================

Run:

- fmt
- validate
- plan

Inspect for:

- destructive changes
- unexpected resource replacement
- security regressions
- missing dependencies

==================================================
9.2 HELM VALIDATION
===================

Run:

- helm lint
- helm template

Validate:

- environment values
- image references
- secrets references
- probes
- resources
- RBAC

==================================================
9.3 KUBERNETES VALIDATION
=========================

Verify:

- deployments
- services
- ingress
- NetworkPolicies
- RBAC
- HPA
- PDB
- topology spread
- security contexts

==================================================
9.4 DEPLOYMENT VALIDATION
=========================

Perform deployment rehearsal.

Verify:

- rollout
- readiness
- migration
- smoke tests
- rollback

==================================================
9.5 ROLLBACK TEST
=================

Deploy a controlled version.

Roll it back.

Verify:

- services recover
- no data corruption
- compatible database state
- traffic restored

==================================================
9.6 MIGRATION SAFETY
====================

Test:

- forward migration
- application compatibility
- failure
- retry
- recovery

Where safe, test representative rollback strategies.

==================================================
9.7 DATABASE BACKUP TEST
========================

Perform controlled restore from backup.

Verify:

- database starts
- schema valid
- important records available
- application can connect

Record actual restoration duration.

==================================================
9.8 PITR TEST
=============

Perform point-in-time recovery in controlled infrastructure.

Verify data state at the selected recovery point.

==================================================
9.9 REDIS RECOVERY
==================

Validate recovery/failover.

Verify application correctness after cache loss or failover.

==================================================
9.10 SEARCH RECOVERY
====================

Test:

- snapshot restore
- index recreation
- full reindex

Verify source-of-truth data remains authoritative.

==================================================
9.11 KAFKA RECOVERY
===================

Test:

- broker failure
- consumer restart
- replay
- lag recovery

==================================================
9.12 OBJECT STORAGE RECOVERY
============================

Verify:

- replicated media where configured
- restore path
- CloudFront recovery

==================================================
9.13 REGION FAILOVER
====================

In controlled production-like infrastructure:

1. Validate primary.
2. Introduce regional failure.
3. Detect.
4. Promote secondary.
5. Redirect traffic.
6. Reconnect realtime.
7. Validate critical user flows.
8. Verify data consistency.
9. Monitor.

Record actual outcomes.

==================================================
9.14 REGION FAILBACK
====================

After primary recovery:

- synchronize state
- verify
- restore routing
- validate
- continue monitoring

Do not perform blind DNS switching.

==================================================
9.15 DATA CONSISTENCY AFTER FAILOVER
====================================

Compare:

- accounts
- profiles
- social graph
- content metadata
- messages
- notifications
- financial records

where the architecture requires the comparison.

==================================================
9.16 MEDIA CONSISTENCY
======================

Verify public and private media remain accessible according to policy after region failover.

==================================================
9.17 SECRETS/CREDENTIAL RECOVERY
================================

Validate that services can recover after:

- secret rotation
- credential invalidation
- regional secret access changes

==================================================
9.18 CERTIFICATE RECOVERY
=========================

Test certificate renewal/rotation in controlled infrastructure.

==================================================
9.19 DNS FAILOVER
=================

Validate health-aware routing.

Test false-positive/false-negative health checks.

==================================================
9.20 DISASTER-RECOVERY REPORT
=============================

Record:

- scenario
- planned RTO
- actual RTO
- planned RPO
- actual RPO
- data integrity result
- unresolved issues

Never replace measured results with target numbers.

==================================================
MILESTONE 10 — FINAL QA CERTIFICATION
======================================

Perform the final quality gate.

==================================================
10.1 FULL REGRESSION
====================

Execute the complete test suite.

Include:

- unit
- integration
- API
- component
- accessibility
- E2E
- security
- performance
- resilience
- infrastructure

==================================================
10.2 CRITICAL PATH MATRIX
=========================

Create a matrix:

Feature
→ Test suites
→ Environment
→ Latest execution
→ Result
→ Defects
→ Risk

Critical features:

- authentication
- authorization
- privacy
- profiles
- social graph
- posts
- stories
- reels
- feed
- search
- messaging
- notifications
- moderation
- rights
- creator monetization
- advertising
- commerce
- data export/deletion

==================================================
10.3 SECURITY MATRIX
====================

Document:

- attack class
- tested endpoint/component
- expected control
- result
- severity
- remediation

==================================================
10.4 PERFORMANCE REPORT
=======================

Record actual:

- throughput
- latency
- p50
- p95
- p99
- error rate
- resource utilization
- scaling behavior

Do not invent missing measurements.

==================================================
10.5 RESILIENCE REPORT
======================

Record:

- experiment
- fault
- result
- detection
- recovery
- data integrity
- remediation

==================================================
10.6 ACCESSIBILITY REPORT
=========================

Record:

- automated findings
- manual findings
- severity
- affected routes
- remediation

==================================================
10.7 DEFECT CLOSURE
===================

Review every:

- P0
- P1
- P2
- P3

P0 and P1 issues require resolution or explicit formal risk acceptance before release.

==================================================
10.8 REGRESSION CONFIRMATION
============================

Re-run all tests affected by fixed defects.

==================================================
10.9 RELEASE CANDIDATE TEST
===========================

Test the exact release artifact intended for deployment.

Do not certify source code while deploying a different artifact.

Use:

- exact container images
- exact Helm release
- exact configuration

where practical.

==================================================
10.10 PRODUCTION SMOKE TEST
===========================

After controlled deployment, validate only safe critical functionality.

Examples:

- public homepage
- API health
- authentication
- profile
- feed
- search
- realtime handshake

Do not perform destructive tests against real user data.

==================================================
10.11 RELEASE GATES
===================

Define mandatory gates.

Code:

- typecheck
- lint
- tests
- build

Security:

- vulnerability scan
- secret scan
- critical security issues resolved

Application:

- critical E2E pass
- authorization tests pass
- privacy tests pass

Infrastructure:

- Terraform valid
- Helm valid
- deployment successful

Operations:

- observability active
- alerts active
- rollback available
- backup verified

==================================================
10.12 QA DASHBOARD
==================

Create a final QA dashboard/report summarizing:

- test counts
- pass/fail
- coverage
- vulnerabilities
- performance
- resilience
- accessibility
- open defects
- release status

Use actual values.

==================================================
10.13 RISK REGISTER
===================

Record accepted risks:

- risk
- likelihood
- impact
- mitigation
- owner
- acceptance date

Do not disguise known risks as test limitations.

==================================================
10.14 FINAL CERTIFICATION STATES
================================

Use explicit states:

READY

All mandatory gates pass.

READY WITH ACCEPTED RISK

Mandatory gates pass with formally accepted non-critical risks.

NOT READY

One or more release-blocking issues remain.

==================================================
10.15 QA SIGN-OFF
=================

Generate a QA sign-off document containing:

- release candidate
- test environment
- execution date
- suites executed
- actual results
- open defects
- security status
- performance status
- resilience status
- accessibility status
- infrastructure status
- final certification state

Never sign off based on assumptions.

==================================================
FINAL QUALITY PRINCIPLES
========================

Do not confuse:

"tests exist"

with:

"the system is validated."

Do not confuse:

"test suite passes"

with:

"the system is production-safe."

Do not confuse:

"no defects found"

with:

"no defects exist."

Use evidence.

==================================================
OUTPUT FORMAT
=============

Before modifying anything:

1. Inspect the current repository.
2. Inspect QA Volume 1 implementation.
3. Inspect existing CI test workflows.
4. Identify available test tooling.
5. Reuse existing frameworks.
6. Identify actual gaps.

For every milestone:

1. State milestone.
2. State test domain.
3. Inspect actual implementation.
4. Add/update tests and validation tooling.
5. Execute tests where possible.
6. Capture actual results.
7. Fix discovered defects.
8. Re-run affected tests.
9. Update documentation and QA artifacts.
10. Keep the repository stable.

When changing files:

- output complete contents of changed/new files;
- never output unchanged files.

==================================================
FINAL ACCEPTANCE CRITERIA
=========================

At the end of this volume:

SECURITY

- authentication security tested;
- authorization security tested;
- IDOR tested;
- privacy boundaries tested;
- XSS tested;
- injection tested;
- SSRF tested where applicable;
- upload security tested;
- webhook security tested;
- WebSocket security tested;
- rate-limit bypass tested;
- secret scanning executed;
- dependency scanning executed.

PERFORMANCE

- normal load tested;
- peak load tested;
- spike tested;
- stress tested;
- endurance tested;
- browser performance tested;
- database performance tested;
- Redis performance tested;
- search performance tested;
- event/queue performance tested;
- realtime performance tested;
- autoscaling validated.

RESILIENCE

- pod failure tested;
- node failure tested;
- dependency failure tested;
- queue failure tested;
- event-system failure tested;
- database failure tested;
- cache failure tested;
- search failure tested;
- network degradation tested;
- duplicate/out-of-order events tested;
- duplicate jobs tested;
- recovery tested.

INFRASTRUCTURE

- Terraform validated;
- Helm validated;
- Kubernetes validated;
- deployment tested;
- rollback tested;
- migration strategy tested;
- backup restore tested;
- PITR tested;
- search recovery tested;
- event recovery tested;
- regional failover tested where infrastructure permits;
- failback tested where infrastructure permits.

FINAL QA

- full regression executed;
- critical-path matrix complete;
- defect register complete;
- security report complete;
- performance report complete;
- resilience report complete;
- accessibility report complete;
- risk register complete;
- release gates defined;
- final QA certification generated.

==================================================
CRITICAL RULE
=============

Never state that the project is "production-ready" simply because this prompt has been executed.

Production readiness requires evidence from actual test execution and validation.

The final certification state must reflect reality:

READY,
READY WITH ACCEPTED RISK,
or
NOT READY.

BEGIN WITH:

MILESTONE 6 — SECURITY TESTING AND APPLICATION PENETRATION-RESISTANCE VALIDATION.
