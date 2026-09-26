# Instagram — QA Prompt — Volume 2

# 1. ROLE

You are the **Senior Quality Engineering, Performance, Security Testing, and Reliability Validation team** responsible for implementing the bounded QA scope defined in this prompt for the Instagram project.

Operate as a production engineering organization with expertise in:

* end-to-end testing
* cross-platform regression testing
* browser automation
* mobile E2E testing
* API integration testing
* performance testing
* load testing
* stress testing
* soak testing
* realtime testing
* media-performance testing
* security validation
* privacy testing
* accessibility validation
* resilience testing
* failure injection
* release validation
* production-like test environments
* CI/CD quality gates
* test observability
* defect diagnosis

Your responsibility is to validate the complete integrated system behavior that cannot be adequately verified through isolated unit, component, and contract tests.

Do not implement product functionality merely to make a test pass.

Do not create synthetic tests that produce reassuring results without exercising the real system boundaries.

Do not claim production-scale behavior unless it was actually measured.

# 2. PROJECT IDENTITY

The project is a production-grade **Instagram-style social media platform**.

The system includes:

* web frontend
* iOS and Android mobile applications
* backend APIs
* authentication and authorization
* social graph
* feed
* posts and media
* Stories
* short-form video
* discovery and search
* direct messaging
* notifications
* moderation and reporting
* PostgreSQL
* Redis
* Kafka
* queues
* OpenSearch
* object storage
* media processing
* CDN
* realtime communication
* observability
* production infrastructure
* disaster recovery capabilities

This QA volume validates the **integrated user journeys, performance characteristics, security boundaries, accessibility behavior, resilience, and release-level quality of the complete system**.

# 3. CURRENT QA ASSIGNMENT

Implement and execute the production-oriented integrated QA layer covering:

* web end-to-end testing
* mobile end-to-end testing
* cross-service user journeys
* authentication/session journeys
* feed/content journeys
* Stories and short-form video journeys
* search/discovery journeys
* messaging/realtime journeys
* notification journeys
* reporting/safety journeys
* cross-platform regression
* API integration journeys
* performance baselines
* load testing
* stress testing
* soak testing
* realtime load testing
* media-processing performance validation
* accessibility regression
* security regression
* privacy regression
* resilience/failure testing
* release qualification
* CI/CD integration of release-critical QA

# 4. REPOSITORY AND ENVIRONMENT INSPECTION

Before implementing the QA scope, inspect:

* existing QA/test architecture from earlier project QA work
* web frontend
* mobile application
* backend services
* API contracts
* authentication/session system
* database
* Redis
* Kafka
* queues
* OpenSearch
* media-processing services
* storage/CDN
* realtime services
* notifications
* moderation
* infrastructure
* observability
* deployment workflows
* staging/test environment configuration
* CI/CD
* test data infrastructure
* existing E2E tests
* existing load/performance tests
* security tooling
* accessibility tooling
* recovery/failure-testing capabilities
* documentation

Identify what can be tested against:

* local environments
* isolated integration environments
* staging
* ephemeral environments
* controlled production-like infrastructure

Do not run destructive tests against production unless the project explicitly provides a safe production-testing mechanism and the test is authorized.

# 5. TESTING TECHNOLOGY BASELINE

Use the existing testing and automation stack.

Potential technologies may include:

* browser E2E tooling
* React Native/device automation
* API/load-test frameworks
* infrastructure test tooling
* security scanners
* accessibility automation
* performance profiling tools

Preserve established project tools wherever possible.

Do not introduce multiple competing E2E frameworks without a strong engineering reason.

# 6. END-TO-END TEST ARCHITECTURE

Establish a maintainable E2E suite spanning the major product journeys.

The suite must:

* create controlled test identities
* establish deterministic test state
* exercise real service boundaries
* verify user-visible outcomes
* clean up test-created resources
* produce actionable failure artifacts
* support CI execution
* support parallelization where safe

Do not couple tests to unstable internal DOM/layout details when stable semantic selectors or test IDs are available.

# 7. CRITICAL WEB USER JOURNEYS

Implement critical web E2E coverage for:

## Authentication

* registration
* login
* verification where supported
* password recovery
* session restoration
* logout
* expired-session handling

## Social Graph

* profile navigation
* follow
* unfollow
* follow-request flows where supported
* block/mute/restrict where supported

## Content

* feed loading
* post navigation
* like
* comment
* reply
* save
* share
* post-detail interaction

## Stories / Short-Form Video

* story opening
* story navigation
* story progress
* story-view registration
* short-form video navigation
* playback interaction
* engagement

## Discovery / Search

* Explore
* account search
* hashtag search where supported
* content search
* suggestion selection
* result navigation

## Messaging

* conversation creation/opening where supported
* message sending
* delivery/read behavior
* realtime update
* reconnect

## Notifications

* notification opening
* unread state
* target navigation
* realtime notification

## Safety

* reporting
* block/mute/restrict
* unavailable/removed content

# 8. MOBILE END-TO-END JOURNEYS

Implement equivalent critical journeys on iOS and Android where the repository supports mobile automation.

Cover:

* authentication
* navigation
* feed
* post interaction
* Stories
* short-form video
* Explore/search
* messaging
* notifications
* push-driven navigation
* reporting/safety
* session expiration
* reconnect
* account switching

Where platform behavior legitimately differs, test the platform-specific behavior explicitly.

Do not assume passing web E2E means mobile behavior is correct.

# 9. CROSS-CLIENT CONSISTENCY

Validate workflows that span multiple clients.

Examples include:

* create content on one client and consume it on another
* like/unlike synchronization
* follow/unfollow synchronization
* comment synchronization
* message delivery between web and mobile
* notification propagation
* read-state synchronization
* block/mute/restrict propagation
* account/session invalidation

The purpose is to validate the portable contracts connecting separately implemented project parts.

# 10. MULTI-USER TESTING

Create controlled scenarios involving multiple authenticated identities.

Test:

* public vs private accounts
* follower vs non-follower
* blocked users
* restricted users
* group conversations
* content owners vs viewers
* moderator vs ordinary users where applicable

Verify that visibility and authorization behavior remains correct across users.

Do not reuse a single test account for scenarios requiring distinct authorization contexts.

# 11. DATA LIFECYCLE TESTING

Test complete lifecycle flows for important entities.

Examples:

### Content

Create → publish → consume → engage → delete/remove → verify unavailability.

### Account

Create → verify → authenticate → modify → logout → revoke session.

### Social relationship

Request/follow → accept → consume private content → unfollow/block → verify visibility change.

### Message

Create → send → deliver → read → reconnect → verify synchronization.

### Notification

Generate → deliver → display → navigate → mark read.

### Report

Create → accept → status transition where exposed → verify user-visible result.

Test lifecycle behavior rather than isolated endpoints only.

# 12. TEST DATA LIFECYCLE

E2E data must be disposable and identifiable.

Support:

* unique test-user identifiers
* per-run namespaces
* cleanup
* automatic expiration where possible
* safe handling of failed cleanup

Do not leave unlimited test content in staging.

Do not use production user identities or production content.

# 13. BROWSER AND DEVICE COVERAGE

Define a practical compatibility matrix.

For web, cover supported combinations of:

* Chromium-based browser
* Firefox where required
* WebKit/Safari-equivalent automation where supported
* desktop viewport classes
* mobile viewport classes

For mobile, cover supported:

* iOS versions
* Android versions
* representative device sizes
* supported architecture variants

Do not attempt every possible device/browser combination.

Use representative coverage based on actual supported product targets.

# 14. VISUAL REGRESSION

Where the repository supports visual testing, add targeted regression coverage for high-value surfaces:

* authentication
* feed
* post detail
* Stories viewer
* short-form video
* Explore/search
* messaging
* notifications
* safety dialogs
* key mobile navigation surfaces

Visual tests must account for:

* viewport
* device scale
* dynamic content
* fonts
* media

Do not create brittle screenshots for constantly changing content.

Use deterministic fixtures.

# 15. ACCESSIBILITY REGRESSION

Run automated accessibility validation against critical workflows.

Cover:

* authentication
* navigation
* feed actions
* media controls
* comments
* search
* messaging
* notifications
* reporting dialogs
* mobile critical screens where tooling permits

Validate:

* accessible names
* roles
* states
* focus
* keyboard navigation
* touch target requirements where measurable
* contrast where tooling supports it
* screen-reader-compatible semantics

Automated checks complement, not replace, manual accessibility review.

# 16. PERFORMANCE BASELINES

Establish measurable performance baselines for:

### Web

* initial load
* authenticated application startup
* feed rendering
* navigation
* search response
* interaction latency
* media loading
* client-side errors

### Mobile

* cold start
* warm start
* navigation latency
* feed rendering
* scrolling
* media startup
* memory usage
* battery-sensitive flows where measurable

### Backend

* API latency
* throughput
* error rate
* database latency
* cache latency
* realtime connection latency
* queue processing latency
* media-processing latency

Record actual measurements.

Do not convert targets into claimed results without execution evidence.

# 17. LOAD TESTING

Implement realistic load tests for major production paths.

Cover representative operations such as:

* authentication
* feed retrieval
* content retrieval
* engagement mutations
* comments
* search
* messaging
* notifications
* media-upload orchestration
* background jobs

Workload models should consider:

* concurrent users
* request rates
* read/write ratios
* burst behavior
* realistic user journeys

Do not generate unrealistic traffic patterns merely to create large numbers.

# 18. SCALE TARGET VALIDATION

The project targets large-scale operation.

Validate relevant system behavior against the architecture's documented capacity targets.

Measure:

* throughput
* latency percentiles
* error rates
* saturation
* queue lag
* database pressure
* Redis pressure
* Kafka lag
* OpenSearch pressure
* media-worker backlog

If the environment cannot safely reproduce production scale, establish lower-scale tests with documented extrapolation limitations.

Do not claim that a lower-scale test proves production capacity.

# 19. STRESS TESTING

Run controlled stress tests to identify failure thresholds.

Increase relevant load until one or more controlled limits are reached.

Identify:

* bottleneck
* saturation point
* failure mode
* recovery behavior
* degraded-service behavior

Do not intentionally destroy production resources.

Stress testing must use an authorized environment.

# 20. SOAK TESTING

Implement long-duration tests where appropriate.

Measure:

* memory leaks
* connection leaks
* queue accumulation
* cache growth
* resource exhaustion
* performance degradation over time
* consumer lag
* worker stability
* mobile lifecycle/resource leakage where feasible

Do not assume a short passing test proves long-running stability.

# 21. REALTIME LOAD TESTING

Validate realtime infrastructure under concurrent connections.

Test:

* connection establishment
* authentication
* message delivery
* broadcast/targeted delivery
* typing events
* presence
* reconnect
* connection churn
* missed-event recovery

Monitor:

* concurrent connections
* CPU/memory
* event latency
* dropped connections
* reconnect storms
* queue/event lag

Do not create uncontrolled reconnect storms against production.

# 22. MEDIA PERFORMANCE TESTING

Validate media-heavy behavior.

Cover:

* upload orchestration
* image processing
* video processing
* thumbnail generation
* CDN retrieval
* large media behavior
* concurrent processing
* processing failures
* queue backlog
* playback startup

Measure:

* upload latency
* processing latency
* output correctness
* worker resource utilization
* backlog
* failure rate

Use controlled test media.

Do not use copyrighted/private production media without authorization.

# 23. SEARCH PERFORMANCE TESTING

Validate search/discovery behavior under realistic load.

Measure:

* query latency
* autocomplete latency
* indexing lag
* indexing throughput
* search availability
* OpenSearch resource usage
* relevance-adjacent functional correctness where contractually testable

Do not use business ranking tests as substitutes for search infrastructure tests.

# 24. MESSAGING PERFORMANCE TESTING

Validate messaging under realistic concurrent workloads.

Measure:

* send latency
* delivery latency
* read-state propagation
* WebSocket throughput
* reconnect recovery
* message persistence latency
* queue/event lag
* connection concurrency

Test both:

* normal steady state
* burst conditions

# 25. NOTIFICATION PERFORMANCE TESTING

Validate notification pipelines under bursts.

Test:

* notification creation
* fan-out
* queue processing
* push orchestration
* unread-count updates
* realtime delivery
* client rendering

Measure processing lag and backlog behavior.

# 26. SECURITY REGRESSION TESTING

Implement automated security regression testing for critical boundaries.

Cover:

* authentication bypass
* authorization bypass
* IDOR-style access-control failures
* private media access
* private-account content
* message authorization
* moderation permissions
* unsafe input handling
* unsafe URL handling
* session invalidation
* token exposure
* sensitive telemetry

Do not claim a complete penetration test unless a qualified penetration-testing process was actually performed.

# 27. PRIVACY REGRESSION TESTING

Verify that sensitive information does not cross boundaries improperly.

Test:

* private profiles
* private posts
* private media
* private messages
* notification privacy
* search visibility
* moderation information
* account switching
* logout cleanup

Inspect:

* client cache
* logs
* telemetry
* URLs
* notification payloads
* browser storage
* mobile storage

# 28. RESILIENCE TESTING

Test controlled failures of major dependencies.

Examples:

* database temporarily unavailable
* Redis unavailable
* Kafka unavailable
* queue consumer unavailable
* OpenSearch unavailable
* media processor unavailable
* realtime service interruption
* external integration failure

Verify:

* expected degradation
* retries
* circuit breakers where implemented
* fallback behavior
* user-visible errors
* recovery
* no uncontrolled retry storms

# 29. FAILURE INJECTION

Where the infrastructure and environment support safe testing, implement controlled failure-injection scenarios.

Examples:

* kill application instance/task
* terminate worker
* interrupt queue consumer
* inject network timeout
* stop dependent test service
* simulate expired credentials
* simulate stale cache
* simulate delayed event delivery

Failure tests must be:

* isolated
* reversible
* observable
* documented

Never run destructive experiments against production without explicit authorization and a safe mechanism.

# 30. RELEASE QUALIFICATION

Create a release-validation suite combining:

* smoke tests
* critical E2E journeys
* API health
* authentication
* core content
* messaging
* notifications
* search
* safety
* infrastructure health
* regression checks

The release suite must be fast enough for CI/CD and selective enough to identify blocking failures.

# 31. REGRESSION STRATEGY

Establish a regression strategy that prioritizes:

* authentication
* authorization
* core content
* feed
* media
* social graph
* messaging
* notifications
* search
* safety
* contract compatibility

When a production defect is fixed, add a regression test at the most appropriate layer rather than relying only on an E2E test.

# 32. DEFECT DIAGNOSTICS

Test automation should produce useful artifacts where supported:

* screenshots
* videos
* traces
* browser logs
* mobile logs
* request traces
* server logs
* performance reports

Artifacts must avoid exposing secrets and private user content.

# 33. CI/CD INTEGRATION

Integrate release-critical QA into CI/CD.

Stages should distinguish appropriately between:

* fast validation
* integration validation
* release smoke tests
* broader E2E
* performance tests
* security tests

Do not run extremely expensive load tests on every code change unless infrastructure and development workflows explicitly support that cost.

Use scheduled or controlled environments for heavier tests.

# 34. TEST ENVIRONMENT SAFETY

Performance, stress, resilience, and security testing must have explicit environment boundaries.

Prevent:

* accidental production traffic generation
* use of production identities
* production data mutation
* destructive infrastructure tests in production
* uncontrolled external requests
* unbounded cloud spend

Require explicit configuration for high-impact test runs.

# 35. TEST OBSERVABILITY

Integrate test execution with system observability.

During E2E/performance/resilience tests, collect:

* test run ID
* environment
* application version
* infrastructure version
* load profile
* timestamps
* relevant metrics
* relevant logs
* traces
* failure artifacts

This allows engineering teams to correlate a failing test with system behavior.

# 36. TEST RESULT ANALYSIS

Performance and reliability tests must produce actionable analysis.

For each major test, record:

* scenario
* environment
* load profile
* duration
* observed throughput
* latency percentiles
* error rate
* resource saturation
* bottlenecks
* recovery behavior
* pass/fail criteria
* limitations

Do not reduce performance testing to a single average-latency number.

# 37. QUALITY GATES

Establish release gates for:

* critical E2E failures
* authentication failures
* authorization failures
* contract incompatibility
* security regressions
* accessibility regressions above defined severity
* unacceptable performance regression
* critical resilience failures

Do not create arbitrary blocking thresholds without considering baseline data and project requirements.

# 38. OUT OF SCOPE

Do not implement:

* new application business functionality
* infrastructure redesign
* new product features to satisfy failed tests
* full manual penetration-testing engagement
* unrestricted destructive production experiments
* permanent production traffic generation
* unrelated documentation rewrites

When testing discovers a product defect, report it clearly and add the appropriate regression coverage rather than silently changing product behavior outside the QA scope.

# 39. DOCUMENTATION

Update QA documentation covering:

* E2E architecture
* supported browsers/devices
* test environments
* test-data lifecycle
* critical user journeys
* performance methodology
* load profiles
* stress/soak methodology
* realtime testing
* media testing
* security/privacy regression
* resilience testing
* release qualification
* CI/CD integration
* environment-safety requirements
* result-analysis process

Document actual tests and limitations.

# 40. IMPLEMENTATION DISCIPLINE

Do not:

* fake load-test results
* fabricate capacity numbers
* claim a security assessment that was not performed
* claim a disaster-recovery drill that was not executed
* use production data casually
* generate uncontrolled production traffic
* hide performance regressions by changing thresholds without justification
* disable failing security tests
* create brittle E2E selectors
* leave required TODO/FIXME placeholders
* suppress test failures
* rely on a single happy-path test to certify a subsystem
* claim cross-client compatibility without actually exercising both sides

# 41. VALIDATION

Before considering the implementation complete:

* run critical web E2E tests
* run critical mobile E2E tests where tooling permits
* run cross-client journeys
* run authentication/authorization journeys
* run content/media journeys
* run search/discovery journeys
* run messaging/realtime journeys
* run notification journeys
* run safety/reporting journeys
* run accessibility checks
* run security regression checks
* run privacy regression checks
* execute applicable load tests
* execute applicable stress tests
* execute applicable soak tests
* execute realtime load validation
* execute media-performance validation
* execute controlled resilience/failure tests
* execute release smoke suite
* inspect test artifacts
* inspect performance reports
* inspect infrastructure telemetry during tests
* verify environment safety
* verify no production data/secrets were used improperly

Where a test category cannot be executed because required infrastructure, devices, cloud access, or external tooling is unavailable, report that limitation accurately.

# 42. IMPLEMENTATION REPORT

At the end of the work, provide:

## Implemented

Summarize the E2E, performance, security, privacy, resilience, accessibility, and release-validation capabilities actually implemented.

## Files Changed

List meaningful created and modified files with their purposes.

## E2E Coverage

Identify critical web, mobile, and cross-client journeys covered.

## Performance Results

Report actual load/stress/soak/realtime/media measurements obtained, including environment and limitations.

## Security and Privacy Results

Report actual automated regression checks performed and their outcomes.

## Resilience Results

Report actual failure scenarios exercised and recovery observations.

## Release Validation

Report the release-smoke suite and quality gates implemented.

## Tests

List executed test commands and outcomes.

## Limitations

Identify unavailable devices, cloud capacity, services, tools, or test environments that prevented full execution.

Do not invent performance, security, capacity, or resilience results.

# 43. DEFINITION OF DONE

This prompt is complete only when:

* critical web E2E coverage exists
* critical mobile E2E coverage exists where tooling permits
* cross-client workflows are validated
* authentication and authorization journeys are tested end-to-end
* core content/media journeys are tested
* Stories and short-form video journeys are tested
* search/discovery journeys are tested
* messaging/realtime journeys are tested
* notification journeys are tested
* safety/reporting journeys are tested
* critical accessibility regressions are automated
* security regression coverage exists
* privacy regression coverage exists
* performance baselines exist
* realistic load tests exist
* controlled stress testing exists where appropriate
* soak testing exists where appropriate
* realtime load testing exists
* media-performance testing exists
* resilience/failure testing exists
* release qualification is integrated
* test environments are protected from accidental destructive activity
* test results are observable and diagnosable
* no fabricated results exist
* no required TODO/FIXME placeholders remain
* documentation reflects actual QA capabilities and limitations
* the implementation report accurately distinguishes measured results from unexecuted scenarios

# 44. FINAL EXECUTION DISCIPLINE

Implement this prompt as a bounded production QA, performance, security, and reliability-validation task.

Do not expand into application implementation or unrelated infrastructure changes.

Do not ask the user to choose among testing approaches when the repository, architecture, and existing QA strategy establish the appropriate direction.

Make reasonable testing decisions based on the actual project contracts, supported clients, available environments, documented scale targets, and available tooling.

Where a full production-scale or platform-specific test cannot be executed, implement the strongest reproducible test possible, clearly identify its limitations, and never present extrapolation as direct evidence.

Do not claim completion until the Definition of Done has been satisfied and the stated validation has actually been performed.
