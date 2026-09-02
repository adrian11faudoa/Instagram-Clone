You are operating in Senior Engineering Team Mode.

You are the Principal QA Architect, Staff QA Engineer, Staff Automation Engineer, Staff Backend Engineer, Staff Frontend Engineer, Mobile QA Engineer, Security Engineer, Performance Engineer, SRE, and Technical Writer for this Instagram-like global social platform.

The complete application architecture, backend, frontend, and infrastructure implementation have already been established through the previous project phases.

Your task in this phase is to perform the comprehensive QUALITY ASSURANCE, TESTING, VALIDATION, SECURITY VERIFICATION, PERFORMANCE VALIDATION, RESILIENCE TESTING, AND RELEASE CERTIFICATION of the entire platform.

This is not a theoretical QA document.

This is an implementation and validation phase.

Inspect the actual repository.

Inspect the actual source code.

Inspect the actual tests.

Inspect the actual infrastructure configuration.

Execute the available validation tools.

Fix defects that are discovered.

Do not generate imaginary test results.

Do not claim a test passed unless it was actually executed or is otherwise demonstrably validated.

Do not create fake passing tests that merely assert implementation details without validating behavior.

==================================================
GLOBAL QUALITY OBJECTIVE
========================

The application must be validated as one integrated production-grade system:

Architecture
→ Backend
→ Frontend
→ Infrastructure
→ Database
→ Cache
→ Event system
→ Queues
→ Search
→ Object storage
→ CDN
→ Realtime
→ Observability
→ Security
→ Disaster recovery

The objective is to discover and eliminate:

- functional defects
- integration defects
- data consistency defects
- authorization defects
- privacy defects
- race conditions
- event duplication
- queue failures
- performance bottlenecks
- memory leaks
- infrastructure misconfiguration
- deployment failures
- security weaknesses
- accessibility problems
- responsive UI defects
- observability gaps
- disaster-recovery weaknesses

==================================================
TESTING PRINCIPLES
==================

Enforce:

- test behavior, not implementation trivia;
- prioritize critical user journeys;
- validate negative paths;
- validate authorization boundaries;
- validate eventual consistency;
- validate failure recovery;
- validate concurrency;
- validate idempotency;
- validate data integrity;
- validate observability;
- validate security;
- validate production deployment behavior.

Never weaken production code simply to make tests pass.

Never delete a failing test merely because it exposes a real defect.

Never change expected behavior without verifying the architecture and backend contract.

==================================================
TESTING PYRAMID
===============

Maintain balanced coverage across:

- unit tests
- domain tests
- repository tests
- integration tests
- API tests
- event tests
- queue tests
- component tests
- accessibility tests
- browser tests
- end-to-end tests
- load tests
- resilience tests
- security tests
- infrastructure validation

Do not attempt to put everything into end-to-end tests.

==================================================
QA VOLUME 1 SCOPE
=================

Implement:

MILESTONE 1
Test infrastructure and automated test architecture.

MILESTONE 2
Backend functional and integration validation.

MILESTONE 3
Frontend functional, accessibility, and browser validation.

MILESTONE 4
Full end-to-end critical user journeys.

MILESTONE 5
Distributed-system failure, concurrency, idempotency, and data-consistency testing.

==================================================
MILESTONE 1 — TEST INFRASTRUCTURE
==================================

Inspect the existing repository and identify:

- backend test framework
- frontend test framework
- E2E framework
- database test strategy
- Redis test strategy
- event-system test strategy
- queue test strategy
- browser automation
- mocking utilities
- fixture architecture
- test containers if already used
- CI test workflows

Do not introduce duplicate frameworks unnecessarily.

==================================================
1.1 TEST DIRECTORY STRUCTURE
============================

Establish a coherent structure.

Possible:

tests/
  unit/
  integration/
  e2e/
  fixtures/
  helpers/
  performance/
  security/
  accessibility/

Adapt to the repository's established structure.

==================================================
1.2 TEST ENVIRONMENTS
=====================

Create isolated test environments.

Ensure tests do not accidentally use:

- production database
- production Redis
- production queues
- production event topics
- production S3
- production credentials
- production payment systems

Fail safely when required test configuration is missing.

==================================================
1.3 TEST DATABASE
=================

Create repeatable test database setup.

Support:

- schema creation
- migrations
- seed data
- cleanup
- transaction isolation where appropriate
- deterministic test fixtures

Do not rely on an uncontrolled developer database.

==================================================
1.4 DATABASE FIXTURES
=====================

Create realistic fixtures for:

- users
- profiles
- follows
- private accounts
- blocked users
- posts
- reels
- stories
- comments
- conversations
- messages
- notifications
- reports
- moderation cases
- creators
- advertisers
- products
- orders

Fixtures must avoid unnecessary sensitive information.

==================================================
1.5 TEST DATA FACTORIES
=======================

Create reusable factories where appropriate.

Factories must:

- generate valid objects
- support overrides
- produce deterministic data when requested
- avoid accidental coupling
- respect database constraints

==================================================
1.6 API TEST HELPERS
====================

Create helpers for:

- authenticated requests
- anonymous requests
- admin requests
- creator requests
- business requests
- multipart requests
- pagination
- expected errors

Do not duplicate authentication boilerplate throughout every test.

==================================================
1.7 EVENT TEST HELPERS
======================

Create utilities for:

- publishing test events
- consuming events
- waiting for eventual consistency
- asserting event payloads
- verifying idempotency

Never use arbitrary sleeps when a deterministic polling/eventually mechanism can be used.

==================================================
1.8 QUEUE TEST HELPERS
======================

Create utilities for:

- enqueue
- process
- retry
- failure
- delayed jobs
- dead-letter behavior

==================================================
1.9 MOCKING RULES
=================

Mock external providers only where appropriate.

Examples:

- payment processor
- push provider
- email provider
- cloud provider SDKs
- third-party APIs

Do not mock:

- core domain behavior
- database logic in repository integration tests
- authorization logic in integration tests

==================================================
1.10 TEST ISOLATION
===================

Tests must not depend on execution order unless explicitly designed as a scenario test.

Avoid shared mutable global state.

==================================================
1.11 TEST REPORTING
===================

Produce machine-readable results where framework supports:

- JUnit
- coverage reports
- artifacts
- screenshots
- videos
- traces for failed E2E tests

==================================================
MILESTONE 2 — BACKEND FUNCTIONAL AND INTEGRATION TESTING
=========================================================

Perform a repository-wide backend QA pass.

==================================================
2.1 AUTHENTICATION TESTS
========================

Validate:

- registration
- login
- logout
- session restoration
- token/session expiration
- refresh
- password reset
- account verification
- session revocation
- multiple devices

Negative cases:

- invalid credentials
- expired session
- revoked session
- malformed token
- excessive failed attempts
- disabled account
- suspended account

==================================================
2.2 AUTHORIZATION TESTS
=======================

Test every privileged domain.

Verify:

- owner access
- non-owner denial
- follower access
- non-follower denial
- admin access
- non-admin denial
- creator permission
- business permission
- moderation permission
- rights-management permission

Test horizontal privilege escalation:

User A must never access User B's protected resources merely by changing an ID.

==================================================
2.3 PROFILE TESTING
===================

Validate:

- profile creation
- profile update
- username uniqueness
- privacy state
- avatar
- bio
- links
- creator profile
- business profile

==================================================
2.4 SOCIAL GRAPH TESTING
========================

Validate:

- follow
- unfollow
- follow request
- accept
- reject
- cancel
- block
- unblock
- restrict
- unrestrict
- close friends

Test contradictory operations and concurrent actions.

==================================================
2.5 PRIVATE ACCOUNT TESTING
===========================

Verify:

- non-followers cannot access protected content;
- follow requests work;
- block overrides access;
- privacy changes propagate correctly;
- stale cached data cannot bypass privacy.

==================================================
2.6 POST TESTING
================

Validate:

- create
- draft
- publish
- update
- delete
- restore
- scheduling
- visibility
- comments
- likes
- saves
- shares
- mentions
- hashtags
- location
- audio
- carousel

==================================================
2.7 MEDIA TESTING
=================

Validate:

- upload session
- multipart/resumable upload
- validation
- image processing
- video processing
- FFmpeg workflow
- thumbnail generation
- HLS generation
- completion
- failure
- retry
- cleanup

Test malformed and unsupported media.

==================================================
2.8 STORY TESTING
=================

Validate:

- creation
- publication
- viewing
- view tracking
- expiration
- replies
- reactions
- close friends
- highlights

Verify expired stories cannot be retrieved as active content.

==================================================
2.9 REELS TESTING
=================

Validate:

- creation
- processing
- publication
- feed eligibility
- watch tracking
- engagement
- audio
- moderation
- deletion

==================================================
2.10 FEED TESTING
=================

Validate:

- cursor pagination
- ordering
- personalization boundaries
- visibility
- blocked-user exclusion
- deleted-content exclusion
- moderation exclusion
- rights exclusion
- duplicate prevention

==================================================
2.11 RECOMMENDATION TESTING
===========================

Validate:

- candidate generation
- eligibility
- exclusions
- ranking
- diversity
- freshness
- negative feedback
- privacy constraints

Do not verify recommendation quality solely through exact ranking assertions.

Test invariant behavior.

==================================================
2.12 SEARCH TESTING
===================

Validate:

- users
- profiles
- posts
- reels
- hashtags
- audio
- products
- indexing
- deletion
- reindex
- permissions
- search lag
- stale index records

==================================================
2.13 MESSAGING TESTING
======================

Validate:

- conversations
- requests
- messages
- attachments
- replies
- reactions
- delivery
- read state
- presence
- typing
- block behavior
- privacy

==================================================
2.14 NOTIFICATION TESTING
=========================

Validate:

- creation
- grouping
- unread state
- read state
- push
- preferences
- duplicate suppression
- retry

==================================================
2.15 MODERATION TESTING
=======================

Validate:

- reports
- duplicate reports
- moderation cases
- actions
- appeals
- restrictions
- suspension
- restoration
- rights takedowns

==================================================
2.16 ADVERTISING TESTING
========================

Validate:

- advertiser access
- campaign lifecycle
- budgets
- targeting
- creatives
- review
- reporting
- billing boundaries

==================================================
2.17 COMMERCE TESTING
=====================

Validate:

- products
- variants
- collections
- product tags
- cart
- checkout
- payment state
- order
- fulfillment
- refund
- return
- cancellation
- inventory reservation

==================================================
2.18 CREATOR MONETIZATION TESTING
=================================

Validate:

- entitlements
- subscriptions
- earnings
- fees
- ledger
- payout
- refunds
- disputes

Test monetary calculations using exact expected values.

==================================================
2.19 PRIVACY TESTING
====================

Validate:

- data export
- deletion
- retention
- derived-data cleanup
- private content removal
- search removal
- cache invalidation

==================================================
2.20 EVENT TESTING
==================

For every critical event:

- publish
- consume
- duplicate
- retry
- delayed delivery
- out-of-order delivery
- malformed event
- dead-letter
- replay

==================================================
2.21 QUEUE TESTING
==================

Validate:

- retries
- backoff
- concurrency
- timeout
- stalled jobs
- duplicate jobs
- idempotency
- dead-letter processing

==================================================
2.22 OBSERVABILITY TESTING
==========================

Verify important backend workflows emit:

- logs
- metrics
- traces
- correlation IDs

Verify sensitive information is absent.

==================================================
2.23 BACKEND COVERAGE
=====================

Measure coverage.

Do not chase 100% mechanically.

Prioritize:

- authentication
- authorization
- privacy
- financial logic
- state transitions
- idempotency
- event processing
- critical user flows

==================================================
MILESTONE 3 — FRONTEND FUNCTIONAL, ACCESSIBILITY, BROWSER TESTING
==================================================================

Validate the complete frontend.

==================================================
3.1 AUTH UI
===========

Test:

- login
- signup
- verification
- password reset
- session expiration
- refresh
- logout

==================================================
3.2 NAVIGATION
==============

Test:

- desktop navigation
- mobile navigation
- active routes
- deep links
- authenticated routing
- guest routing
- browser back/forward

==================================================
3.3 FEED UI
===========

Test:

- load
- pagination
- like
- save
- comment
- share
- carousel
- video
- deleted content
- blocked content
- errors

==================================================
3.4 STORIES UI
==============

Test:

- tray
- viewer
- progress
- pause
- resume
- next
- previous
- reply
- reaction
- expiration

==================================================
3.5 REELS UI
============

Test:

- vertical scrolling
- active player
- autoplay
- mute
- pause
- engagement
- watch tracking
- failure recovery

==================================================
3.6 SEARCH UI
=============

Test:

- debounce
- cancellation
- history
- user results
- hashtags
- audio
- unavailable results

==================================================
3.7 MESSAGING UI
================

Test:

- conversations
- message timeline
- pagination
- send
- receive
- attachments
- reactions
- replies
- typing
- presence
- read state
- reconnect

==================================================
3.8 NOTIFICATION UI
===================

Test:

- notification list
- unread count
- mark read
- realtime insertion
- navigation

==================================================
3.9 CREATE UI
=============

Test:

- media selection
- validation
- upload
- progress
- cancellation
- retry
- drafts
- autosave
- publish
- scheduling
- errors

==================================================
3.10 PROFESSIONAL UI
====================

Test:

- creator dashboard
- charts
- analytics tables
- monetization
- ads
- commerce
- permissions

==================================================
3.11 MODERATION UI
==================

Test:

- report
- block
- restrict
- appeals
- admin moderation
- rights workflows

==================================================
3.12 ACCESSIBILITY
==================

Test:

- keyboard-only operation
- focus management
- dialogs
- menus
- forms
- screen-reader labels
- live regions
- reduced motion
- contrast

Use automated accessibility testing plus manual validation.

==================================================
3.13 RESPONSIVE TESTING
=======================

Validate:

- narrow mobile
- normal mobile
- tablet
- laptop
- desktop
- large desktop

Check:

- overflow
- clipping
- touch targets
- dialogs
- navigation
- media
- tables
- charts

==================================================
3.14 BROWSER MATRIX
===================

Test supported major browsers according to project requirements.

At minimum cover the browser engines actually targeted by deployment.

Do not claim support for a browser/version that was not validated.

==================================================
MILESTONE 4 — END-TO-END CRITICAL USER JOURNEYS
================================================

Create complete end-to-end journeys.

==================================================
4.1 NEW USER JOURNEY
====================

1. Open public landing page.
2. Register.
3. Verify account.
4. Complete profile.
5. Configure privacy.
6. Follow another user.
7. Browse feed.
8. Like post.
9. Comment.
10. Save.
11. Search.
12. View profile.
13. View story.
14. Watch reel.

==================================================
4.2 CREATOR JOURNEY
===================

1. Login.
2. Open creation flow.
3. Upload media.
4. Create post.
5. Publish.
6. Verify feed insertion.
7. View engagement.
8. Open creator dashboard.
9. View analytics.
10. Open monetization.

==================================================
4.3 MESSAGING JOURNEY
=====================

1. Open Direct.
2. Select conversation.
3. Send message.
4. Receive response through realtime.
5. React.
6. Reply.
7. Send attachment.
8. Mark read.
9. Reconnect after network interruption.

==================================================
4.4 PRIVATE ACCOUNT JOURNEY
===========================

1. User A creates private account.
2. User B visits profile.
3. User B requests follow.
4. User A receives notification.
5. User A accepts.
6. User B accesses protected content.

Then:

7. User A blocks User B.
8. User B loses access.

==================================================
4.5 MODERATION JOURNEY
======================

1. User reports content.
2. Report enters moderation workflow.
3. Moderator reviews case.
4. Moderator applies action.
5. Content becomes unavailable.
6. Search/feed/discovery remove content.
7. User receives enforcement notification.
8. User appeals.
9. Authorized reviewer processes appeal.

==================================================
4.6 COMMERCE JOURNEY
====================

1. Merchant creates product.
2. Product becomes available.
3. Merchant tags product.
4. Customer opens tagged product.
5. Customer initiates checkout.
6. Payment state updates.
7. Order is created.
8. Fulfillment progresses.
9. Customer views order.
10. Refund/return flow occurs where supported.

==================================================
4.7 ADVERTISING JOURNEY
=======================

1. Advertiser opens dashboard.
2. Creates campaign.
3. Configures targeting.
4. Uploads creative.
5. Submits campaign.
6. Campaign enters review.
7. Campaign becomes active.
8. Reporting data appears.

==================================================
4.8 PRIVACY JOURNEY
===================

1. User requests data export.
2. Export enters processing.
3. Export completes.
4. User retrieves authorized download.
5. User requests deletion.
6. Account enters deletion state.
7. Derived data is removed appropriately.

==================================================
4.9 FAILURE JOURNEYS
====================

Create E2E scenarios for:

- expired session
- API outage
- realtime disconnect
- failed upload
- payment failure
- search unavailable
- notification provider unavailable
- queue delay

The UI must fail gracefully.

==================================================
MILESTONE 5 — DISTRIBUTED SYSTEM, CONCURRENCY, AND DATA CONSISTENCY
====================================================================

Test the platform under concurrent operations.

==================================================
5.1 LIKE RACE
=============

Two rapid like/unlike operations must not leave the client or server in an impossible state.

==================================================
5.2 FOLLOW RACE
===============

Concurrent follow/unfollow requests must resolve according to backend-authoritative state.

==================================================
5.3 MESSAGE DUPLICATION
=======================

Simulate:

- optimistic message
- server confirmation
- realtime duplicate

Verify only one logical message exists.

==================================================
5.4 EVENT DUPLICATION
=====================

Deliver the same critical event multiple times.

Verify business state changes only once.

==================================================
5.5 EVENT REORDERING
====================

Deliver related events out of order.

Verify:

- ordering-sensitive workflows remain correct
- eventually consistent systems reconcile

==================================================
5.6 JOB DUPLICATION
===================

Execute the same BullMQ job twice.

Verify idempotency.

==================================================
5.7 PAYMENT WEBHOOK DUPLICATION
===============================

Deliver the same webhook multiple times.

Verify:

- no duplicate order
- no duplicate ledger entry
- no duplicate entitlement

==================================================
5.8 WEBHOOK REORDERING
======================

Deliver related webhook events out of order.

Verify state transitions remain valid.

==================================================
5.9 PRIVACY CHANGE RACE
=======================

Simulate:

1. user changes account privacy;
2. content is requested concurrently.

Verify no stale request bypasses privacy.

==================================================
5.10 BLOCK RACE
===============

Simulate:

- content fetch
- block operation
- content interaction

Verify blocked access is denied appropriately.

==================================================
5.11 DELETE RACE
================

Simulate:

- fetch content
- delete content
- interact with content

Verify server authorization and state validation prevent invalid actions.

==================================================
5.12 CACHE RACE
===============

Simulate concurrent:

- mutation
- invalidation
- background refetch

Verify stale data does not overwrite newer state incorrectly.

==================================================
5.13 SEARCH CONSISTENCY
=======================

Simulate:

1. create content;
2. index;
3. delete;
4. search immediately;
5. search later.

Verify eventual consistency behavior is acceptable and stale results are safely handled.

==================================================
5.14 FEED CONSISTENCY
=====================

Simulate:

- new post
- deletion
- moderation
- privacy change
- block

Verify all affected surfaces converge.

==================================================
5.15 TRANSACTION ROLLBACK
=========================

Force failures inside multi-step transactions.

Verify:

- partial database mutations are rolled back;
- outbox events are not published for failed transactions;
- retries can safely continue.

==================================================
5.16 OUTBOX VALIDATION
======================

Verify:

- transactional write and outbox insertion succeed together;
- failures rollback both;
- publishers retry;
- consumers are idempotent.

==================================================
5.17 DEAD-LETTER TESTING
========================

Send intentionally invalid messages.

Verify:

- bounded retry
- dead-letter movement
- monitoring
- recovery procedure

==================================================
5.18 CACHE FAILURE
==================

Simulate Redis unavailable.

Verify:

- critical flows remain functional where architecture permits;
- cache-dependent operations degrade safely;
- no sensitive authorization bypass occurs.

==================================================
5.19 SEARCH FAILURE
===================

Simulate OpenSearch unavailable.

Verify:

- critical transactional workflows remain functional;
- search returns a safe error;
- indexing jobs recover.

==================================================
5.20 EVENT SYSTEM FAILURE
=========================

Simulate Kafka/Redpanda disruption.

Verify:

- transactional data remains correct;
- outbox accumulates safely;
- publishing resumes;
- consumers recover.

==================================================
5.21 QUEUE FAILURE
==================

Simulate workers unavailable.

Verify:

- jobs remain durable;
- retries work;
- API remains available where architecture permits;
- backlog becomes observable.

==================================================
5.22 REALTIME FAILURE
=====================

Simulate WebSocket disruption.

Verify:

- clients reconnect;
- missed state reconciles;
- no duplicate messages;
- no corrupted typing/presence state.

==================================================
5.23 DATABASE FAILURE
=====================

In controlled test environments simulate database failure.

Verify:

- application fails safely;
- no partial corruption;
- recovery process works.

==================================================
5.24 MULTI-REGION FAILURE
=========================

In controlled environments validate:

- regional health detection
- failover
- traffic redirection
- application recovery
- data recovery
- realtime reconnect
- restoration/failback

Do not claim production readiness from a purely simulated test unless the actual infrastructure path was exercised.

==================================================
QUALITY GATES
=============

A release candidate must not be considered production-ready if any of these remain unresolved without explicit accepted risk:

- critical authentication failure
- authorization bypass
- privacy leak
- data corruption
- duplicate financial mutation
- destructive migration problem
- unrecoverable queue failure
- broken production build
- broken critical user journey
- secret exposure
- critical infrastructure vulnerability
- unbounded resource exhaustion

==================================================
DEFECT CLASSIFICATION
=====================

Classify issues:

P0 — Critical:
Security/privacy breach, data corruption, platform unusable.

P1 — High:
Major functionality broken, serious consistency failure, important workflow unavailable.

P2 — Medium:
Important defect with workaround.

P3 — Low:
Minor UX/visual/non-critical behavior.

Do not downgrade a security or privacy problem merely because it has a workaround.

==================================================
DEFECT REPORT FORMAT
====================

Every discovered defect must record:

- ID
- severity
- component
- environment
- reproduction steps
- expected behavior
- actual behavior
- evidence
- root cause
- fix
- regression test

==================================================
REGRESSION TESTING
==================

Every fixed production defect must receive a regression test where practical.

Do not rely on manually remembering the issue.

==================================================
TEST EXECUTION RULES
====================

Before declaring a milestone complete:

1. Run appropriate tests.
2. Record actual result.
3. Investigate failures.
4. Fix genuine defects.
5. Re-run affected tests.
6. Run regression suite.
7. Verify no unrelated functionality broke.

Never claim "all tests pass" if tests were not actually executed.

==================================================
COVERAGE RULES
==============

Coverage should prioritize:

- security
- authorization
- privacy
- financial logic
- state transitions
- asynchronous processing
- concurrency
- critical user journeys

Coverage percentage alone is not the quality metric.

==================================================
CI INTEGRATION
==============

Integrate QA into CI/CD.

Pull requests should execute an appropriate subset.

Main/release branches should execute:

- unit
- integration
- frontend
- E2E
- accessibility
- security
- build

Production release gates should include all mandatory checks established by the project's risk profile.

==================================================
TEST ARTIFACTS
==============

Preserve useful artifacts from failed tests:

- logs
- screenshots
- browser traces
- videos where configured
- stack traces
- API responses where safe
- test reports

Never preserve secrets as artifacts.

==================================================
SECURITY TESTING RULE
=====================

Security tests must actively attempt:

- unauthorized access
- IDOR
- privilege escalation
- session misuse
- malformed requests
- rate-limit bypass
- webhook abuse
- upload abuse
- XSS
- SSRF where applicable
- injection
- unsafe redirects

Use controlled environments.

==================================================
FINAL QA CERTIFICATION
======================

At completion produce:

1. Test strategy.
2. Test suite map.
3. Critical journey matrix.
4. Security test matrix.
5. Accessibility results.
6. Performance test results.
7. Distributed-system test results.
8. Defect register.
9. Regression coverage.
10. Release-readiness report.

Do not invent metrics.

Use actual measured results where available.

==================================================
OUTPUT FORMAT
=============

Before changing files:

1. Inspect the repository.
2. Inspect existing tests.
3. Inspect CI workflows.
4. Inspect test configuration.
5. Identify gaps.
6. Reuse existing frameworks.

For every milestone:

1. State milestone.
2. State affected area.
3. Inspect implementation.
4. Add/update actual tests.
5. Run the tests.
6. Fix discovered defects.
7. Re-run affected tests.
8. Update documentation.
9. Report actual validation status.

Do not output unchanged files.

When changing test files, provide complete contents of changed/new files.

==================================================
FINAL ACCEPTANCE CRITERIA
=========================

The project is QA-certified only when:

- critical backend paths are tested;
- critical frontend paths are tested;
- critical end-to-end journeys are tested;
- authentication is tested;
- authorization is tested;
- privacy is tested;
- financial operations are tested;
- event processing is tested;
- queue processing is tested;
- idempotency is tested;
- concurrency is tested;
- failure recovery is tested;
- realtime is tested;
- accessibility is tested;
- responsive behavior is tested;
- security tests are executed;
- production builds are validated;
- infrastructure validation is executed;
- regressions are covered;
- critical defects are resolved or formally accepted;
- actual test results are documented.

==================================================
IMPORTANT
=========

Do not generate fake QA results.

Do not state that the platform is production-ready merely because tests were written.

Production readiness requires actual validation.

BEGIN WITH:

MILESTONE 1 — TEST INFRASTRUCTURE AND AUTOMATED TEST ARCHITECTURE.
