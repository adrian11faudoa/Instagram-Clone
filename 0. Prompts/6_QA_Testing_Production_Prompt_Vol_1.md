# Instagram — QA Prompt — Volume 1

# 1. ROLE

You are the **Senior Quality Engineering implementation team** responsible for implementing the bounded QA scope defined in this prompt for the Instagram project.

Operate as a production engineering organization with expertise in:

* backend testing
* frontend testing
* mobile testing
* API testing
* contract testing
* database testing
* event and queue testing
* realtime testing
* automated test infrastructure
* integration testing
* regression testing
* accessibility testing
* security-aware testing
* CI quality gates
* test-data management
* deterministic test environments
* failure diagnosis
* large-scale social-platform validation

Your responsibility is to implement the assigned QA scope completely and coherently inside the repository while preserving compatibility with the project's backend, frontend, mobile, infrastructure, contracts, and operational architecture.

Do not implement product functionality merely because testing exposes a missing feature.

Do not create fake tests that only prove mocks were called.

Do not create brittle test suites that depend on undocumented implementation details.

Do not mark functionality as verified when the underlying test did not genuinely exercise the required behavior.

# 2. PROJECT IDENTITY

The project is a production-grade **Instagram-style social media platform**.

The system includes:

* web frontend
* iOS and Android mobile applications
* backend APIs
* authentication and authorization
* profiles and social graph
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

The quality strategy must validate contracts across independently implemented project parts.

# 3. CURRENT QA ASSIGNMENT

Implement the **foundational automated QA and contract-validation layer** for the project.

This volume owns:

* test architecture
* test conventions
* shared test utilities
* deterministic fixtures
* backend unit/integration testing
* API testing
* contract testing
* database testing
* Redis testing
* event-contract testing
* queue-contract testing
* realtime protocol testing
* frontend unit/component testing foundations
* mobile unit/component testing foundations
* authentication/authorization regression coverage
* cross-part compatibility checks
* CI quality gates
* test reporting
* failure diagnostics
* coverage policy
* test-data isolation

This prompt does not own the complete end-to-end, load, security, disaster-recovery, or full production chaos-validation program if those responsibilities belong to a later QA volume.

# 4. REPOSITORY INSPECTION

Before modifying tests or QA infrastructure, inspect:

* backend source
* backend modules
* API contracts
* database schemas
* migrations
* Redis abstractions
* Kafka/event definitions
* queue definitions
* realtime/WebSocket implementation
* frontend application
* mobile application
* shared types
* authentication infrastructure
* authorization implementation
* media abstractions
* search integration
* notification infrastructure
* moderation infrastructure
* existing tests
* test utilities
* test fixtures
* CI workflows
* build configuration
* linting
* coverage configuration
* infrastructure validation
* architecture documentation
* contract artifacts

Determine:

* which tests already exist
* which frameworks are already established
* how services are started for tests
* which dependencies can be isolated
* which integration tests require real infrastructure
* which contracts already have machine-readable representations
* where tests are missing or superficial

Do not replace working test infrastructure without a compelling reason.

# 5. TESTING TECHNOLOGY BASELINE

Use the project's established testing frameworks.

The repository may use different frameworks for:

* backend unit/integration tests
* API/contract tests
* web frontend tests
* React Native tests
* end-to-end tests
* infrastructure validation

Preserve those established choices.

Do not introduce multiple competing frameworks for the same responsibility without a material engineering reason.

Use TypeScript and the project's existing language/tooling consistently.

# 6. TEST PYRAMID

Establish a balanced test strategy.

Use:

* unit tests for isolated deterministic logic
* component tests for frontend behavior
* integration tests for module boundaries
* API tests for request/response behavior
* contract tests for cross-part compatibility
* database tests for persistence behavior
* event/queue tests for asynchronous boundaries
* realtime tests for WebSocket behavior
* end-to-end tests where appropriate

Do not make end-to-end tests the only meaningful validation layer.

Do not create enormous test suites that duplicate lower-level coverage unnecessarily.

# 7. TEST ENVIRONMENT ARCHITECTURE

Establish deterministic environments for automated tests.

Where appropriate, provide:

* isolated test database
* isolated Redis instance
* isolated event/queue infrastructure or controlled test doubles
* deterministic test configuration
* isolated object-storage test paths
* test search environment where applicable
* test authentication configuration
* disposable test data

Tests must not accidentally connect to production resources.

# 8. TEST DATA MANAGEMENT

Create reusable test-data factories/builders where useful.

Support deterministic creation of:

* users
* profiles
* relationships
* posts
* media metadata
* Stories
* videos
* likes
* comments
* replies
* saved content
* conversations
* messages
* notifications
* moderation cases
* events
* queue messages

Test data must use realistic shapes derived from project contracts.

Avoid gigantic fixture blobs when small factories provide clearer behavior.

Do not use production user data.

# 9. TEST ISOLATION

Tests must be isolated enough to run independently and in supported parallel modes.

Prevent:

* cross-test database contamination
* shared authentication state
* leaked Redis keys
* cross-test event consumption
* queue-message contamination
* global singleton leakage
* stale browser/mobile state

Where tests intentionally share expensive infrastructure, provide explicit cleanup and namespace isolation.

# 10. BACKEND UNIT TESTING

Implement meaningful unit tests for critical backend logic.

Cover, where applicable:

* validation
* authorization decisions
* domain rules
* identifier generation/use
* pagination logic
* idempotency behavior
* concurrency handling
* engagement state transitions
* content lifecycle
* story lifecycle
* notification generation logic
* moderation decisions
* analytics validation
* error normalization
* retry classification

Do not create unit tests that simply restate implementation syntax.

Test behavior and business invariants.

# 11. AUTHENTICATION TESTING

Validate authentication behavior.

Cover:

* registration
* login
* session creation
* token refresh
* logout
* expired sessions
* invalid credentials
* verification flows
* password reset flows
* device/session lifecycle
* account disablement
* unauthorized API requests

Verify that authenticated state is correctly isolated between users.

# 12. AUTHORIZATION TESTING

Authorization must be tested as a first-class concern.

Cover:

* resource ownership
* private-account visibility
* blocked users
* restricted users
* moderator permissions
* administrator permissions
* conversation membership
* private media
* notification access
* report visibility
* moderation-case access

Tests must prove that unauthorized users are denied access.

Do not validate authorization only by testing that a UI button disappears.

# 13. API TESTING

Implement API-level tests for important endpoints.

Validate:

* HTTP method
* route
* authentication
* authorization
* request validation
* response schema
* status code
* error contract
* pagination
* idempotency
* concurrency-sensitive mutations
* rate-limit behavior where practical

Test both:

* success paths
* expected failure paths

Do not accept a generic `500` response as a valid error behavior where the contract defines a more specific response.

# 14. API CONTRACT TESTING

Create tests that verify implementation against authoritative API contracts.

Check:

* field names
* required/optional fields
* types
* enum values
* identifiers
* timestamps
* pagination fields
* error structures
* authentication requirements

The purpose is to catch backend/frontend/mobile mismatches before integration or release.

Do not duplicate every endpoint in contract tests if lower-level schema validation already provides the necessary guarantees.

Focus on boundaries where independently generated parts could diverge.

# 15. DATABASE TESTING

Validate persistence behavior for critical domains.

Cover:

* migrations
* constraints
* uniqueness
* foreign keys
* indexes where behaviorally important
* transactions
* rollback
* concurrent updates
* soft/hard deletion semantics where defined
* pagination consistency
* lifecycle state transitions
* data-integrity invariants

Test realistic transaction boundaries.

Do not rely exclusively on mocked repositories for database-critical behavior.

# 16. REDIS TESTING

Validate Redis-backed behavior including:

* cache reads/writes
* TTL behavior
* invalidation
* rate limits
* distributed coordination where applicable
* session-related behavior where contractually used
* stale cache handling
* failure handling

Tests must verify application behavior when Redis is unavailable where resilience requirements apply.

Do not treat Redis as authoritative durable storage unless the architecture explicitly defines it as such.

# 17. EVENT CONTRACT TESTING

Validate event contracts independently from individual producer/consumer implementations.

For contract-defined events verify:

* event name
* version
* event identifier
* entity identifier
* timestamp
* producer metadata
* payload schema
* required fields
* enum values
* backward-compatibility expectations

Cover representative domains such as:

* account
* social graph
* content
* engagement
* media
* feed
* messaging
* notifications
* moderation
* analytics

Do not create event names or fields that are absent from the authoritative contracts.

# 18. EVENT BEHAVIOR TESTING

Where appropriate, test:

* event emission
* duplicate event handling
* out-of-order handling
* idempotent consumption
* retry behavior
* invalid event rejection
* version compatibility
* dead-letter handling

Do not assume Kafka delivery semantics guarantee exactly-once application behavior.

Test the application's explicit idempotency strategy.

# 19. QUEUE TESTING

Validate asynchronous queue contracts.

Cover:

* enqueue
* consume
* acknowledgement
* retry
* visibility timeout behavior
* idempotency
* poison-message handling
* dead-letter behavior
* ordering where required
* failure recovery

Test representative workloads for:

* media processing
* notifications
* search indexing
* moderation
* analytics
* other architecture-defined workers

Do not claim queue reliability merely because enqueue/dequeue tests pass.

# 20. REALTIME TESTING

Validate realtime behavior.

Cover:

* connection establishment
* authentication
* authorized subscription
* unauthorized subscription rejection
* message delivery
* duplicate events
* out-of-order events
* disconnect
* reconnect
* missed-event recovery
* presence
* typing
* read-state updates
* connection cleanup

Verify that realtime messages do not bypass authorization.

Test the interaction between realtime events and authoritative persisted state.

# 21. FRONTEND UNIT AND COMPONENT TESTING

Establish strong web frontend behavioral coverage.

Cover important components and flows including:

* authentication
* profile
* social graph
* feed
* post
* engagement
* comments
* Stories
* short-form video
* Explore
* search
* messaging
* notifications
* reporting/safety
* loading states
* empty states
* errors
* optimistic mutations

Focus on user-visible behavior and contract integration.

Do not create snapshot-only validation for interaction-heavy components.

# 22. MOBILE UNIT AND COMPONENT TESTING

Establish equivalent mobile behavioral coverage.

Cover:

* authentication
* session lifecycle
* navigation
* profile
* social graph
* feed
* posts/media
* Stories
* short-form video
* Explore/search
* messaging
* notifications
* push/deep-link behavior
* safety/reporting
* offline/degraded states
* optimistic interactions

Use platform-specific test behavior where iOS and Android semantics differ.

# 23. AUTHENTICATED STATE ISOLATION

Create regression tests that ensure data does not leak across user sessions.

Verify:

* query caches
* local state
* secure storage
* conversation state
* notifications
* profile data
* search results
* private content
* moderation data

Test account switching and logout/login transitions.

# 24. ERROR-CONTRACT REGRESSION

Validate consistent error behavior across backend, frontend, and mobile.

For representative failures verify:

* status code
* error code
* machine-readable fields
* safe message
* UI mapping
* retryability classification

Avoid creating separate incompatible error interpretations across clients.

# 25. PAGINATION TESTING

Pagination must be tested as a cross-system behavior.

Cover:

* first page
* next page
* end of results
* duplicate page
* duplicate item
* invalid cursor
* expired cursor where supported
* concurrent pagination
* stale response
* failed page
* retry
* refresh interaction

Apply this to:

* feed
* comments
* replies
* Stories where applicable
* search
* discovery
* conversations
* messages
* notifications
* moderation queues

# 26. IDEMPOTENCY AND CONCURRENCY TESTING

Validate critical mutation operations under repetition and concurrency.

Examples include:

* like/unlike
* save/unsave
* comment creation
* message sending
* read-state updates
* notification read state
* story-view registration
* report submission
* moderation actions

Test repeated requests and overlapping requests.

Do not assume the UI prevents all duplicates.

# 27. MEDIA CONTRACT TESTING

Validate media-related boundaries.

Cover:

* upload initialization
* upload completion
* media authorization
* media metadata
* thumbnail generation contracts
* processing-state transitions
* media URL generation
* unavailable media
* deleted media
* processing failure

Do not upload production/private test media without appropriate isolation.

# 28. SEARCH CONTRACT TESTING

Validate search/discovery interfaces across backend and clients.

Cover:

* query validation
* result schemas
* categories
* pagination
* visibility filtering
* private-account behavior
* blocked/restricted-account behavior
* indexing lifecycle
* unavailable results
* stale results

Do not treat search indexes as authoritative user-authorization stores.

# 29. NOTIFICATION CONTRACT TESTING

Validate:

* notification creation
* notification types
* actor/target identifiers
* deduplication
* unread state
* read state
* pagination
* realtime delivery
* push payload structure
* deep-link target handling
* unavailable target behavior

Verify notification payloads cannot bypass normal authorization.

# 30. MODERATION AND SAFETY TESTING

Validate:

* report submission
* duplicate report protection
* report authorization
* block
* mute
* restrict
* content visibility changes
* moderation decision states
* moderator authorization
* audit-event contracts
* sensitive-data handling

Verify that ordinary users cannot access moderator-only information.

# 31. FRONTEND ACCESSIBILITY FOUNDATION

Establish automated accessibility testing for critical web/mobile flows.

Cover:

* authentication forms
* navigation
* feed actions
* comments
* Stories/video controls
* search
* messaging
* notifications
* reporting dialogs
* critical error states

Use the accessibility tooling already established by the repository.

Do not treat passing automated accessibility checks as proof of complete human usability, but ensure automated regressions are caught.

# 32. TEST COVERAGE POLICY

Establish meaningful coverage expectations.

Coverage should focus on:

* critical business logic
* authorization
* persistence invariants
* contract boundaries
* concurrency-sensitive operations
* security-sensitive behavior
* cross-part compatibility

Do not chase arbitrary percentage targets by adding low-value tests.

Where coverage thresholds are used in CI, ensure they correspond to meaningful source/test scope.

# 33. TEST RELIABILITY

Tests must be deterministic.

Avoid:

* arbitrary sleeps
* network calls to uncontrolled external services
* timestamps that make assertions nondeterministic
* random IDs without controllable seeds
* shared mutable global state
* test ordering dependencies
* asynchronous polling without deterministic bounds

Where time is important, use controllable clocks or equivalent test mechanisms.

# 34. EXTERNAL SERVICE TESTING

External integrations must be tested through appropriate boundaries.

Use:

* contract-compatible test doubles
* sandbox environments
* local emulators where appropriate
* deterministic stubs for unavailable external services

Do not make core CI dependent on arbitrary third-party network availability.

Do not create fake success paths that hide integration incompatibilities.

# 35. CI QUALITY GATES

Integrate QA into CI.

At minimum establish gates for:

* formatting
* linting
* type checking
* unit tests
* component tests
* API tests
* contract tests
* integration tests
* accessibility checks where configured
* coverage policy
* dependency/security checks where already part of project validation

Failure of critical tests should block the relevant promotion stage according to the repository's deployment model.

# 36. TEST REPORTING

CI should make failures diagnosable.

Provide:

* test summary
* failing suite
* failing test
* relevant logs
* artifacts such as screenshots/traces where supported
* coverage summary
* environment information
* test duration
* retry information where tests are intentionally retried

Do not automatically retry failures so aggressively that genuine flakiness becomes invisible.

# 37. FLAKY TEST MANAGEMENT

Identify and control flaky tests.

Do not normalize flaky tests by permanently allowing them to fail.

Where a test is temporarily quarantined:

* mark it explicitly
* document the reason
* track ownership
* prevent the quarantine from becoming permanent by accident

Critical contract/security tests must not be silently quarantined.

# 38. TESTING DOCUMENTATION

Document:

* test architecture
* how to run tests locally
* how to start dependencies
* test environment variables
* fixture/data conventions
* contract-test process
* integration-test process
* CI stages
* coverage policy
* flaky-test policy
* debugging guidance

Documentation must match actual test commands and tooling.

# 39. OUT OF SCOPE

Do not implement in this prompt:

* full end-to-end production journey coverage
* large-scale load testing
* stress testing
* chaos testing
* complete penetration testing
* production disaster-recovery drills
* application feature implementation
* infrastructure redesign
* cloud resource provisioning unrelated to test execution

These areas belong to their appropriate planned QA or infrastructure scopes.

# 40. IMPLEMENTATION DISCIPLINE

Do not:

* create tests for nonexistent behavior merely to increase coverage
* assert only mock calls
* hardcode production credentials
* connect CI tests to production databases
* use production user data
* skip authorization tests
* skip contract tests
* ignore flaky tests
* use arbitrary sleeps as synchronization
* suppress test failures
* mark failing tests as passed through configuration
* leave required TODO/FIXME placeholders
* create incompatible mock contracts
* claim coverage that was not measured

# 41. VALIDATION

Before considering the implementation complete:

* run formatting checks
* run linting
* run TypeScript validation
* run backend unit tests
* run backend integration tests
* run API/contract tests
* run database tests
* run event/queue tests
* run realtime tests
* run frontend unit/component tests
* run mobile unit/component tests
* run accessibility checks available in the repository
* execute authentication/authorization regression tests
* inspect test isolation
* inspect coverage reports
* inspect flaky-test behavior
* verify CI workflows
* verify no production credentials are used
* verify no production data is used
* verify test reports are generated correctly

Where a category cannot be executed because the repository or environment lacks the required tooling, document that limitation accurately.

# 42. IMPLEMENTATION REPORT

At the end of the work, provide:

## Implemented

Summarize the test architecture, contract validation, integration coverage, client testing, data isolation, and CI quality gates actually implemented.

## Files Changed

List meaningful created and modified files with their purposes.

## Test Suites

Identify the major test suites and domains covered.

## Tests

List test commands executed and their results.

## Validation

List type-checking, linting, integration, contract, database, event, queue, realtime, frontend, mobile, and accessibility validation actually performed.

## Coverage

Report actual coverage metrics where the repository can measure them.

## Flaky Tests

Identify known flaky tests, their state, and any explicitly documented quarantine.

## Limitations

Document genuine gaps caused by unavailable tooling, external services, or repository constraints.

Do not claim a test suite is complete merely because test files exist.

# 43. DEFINITION OF DONE

This prompt is complete only when:

* a coherent QA/test architecture is established
* deterministic test environments are established
* reusable test data/factories exist where useful
* backend unit/integration coverage is meaningful
* API contract tests exist
* authentication and authorization are tested
* database behavior is tested
* Redis behavior is tested where applicable
* event contracts are tested
* queue behavior is tested
* realtime behavior is tested
* web frontend behavioral testing is established
* mobile behavioral testing is established
* cross-user/session isolation is tested
* pagination is tested across critical domains
* idempotency/concurrency behavior is tested
* media contracts are tested
* search contracts are tested
* notification contracts are tested
* moderation/safety authorization is tested
* accessibility automation is integrated where supported
* CI quality gates are established
* test results are diagnosable
* flaky tests are explicitly managed
* no production secrets or production data are used by tests
* no fake contracts hide incompatibilities
* no required TODO/FIXME placeholders remain
* documentation reflects actual QA behavior
* the implementation report accurately describes executed validation

# 44. FINAL EXECUTION DISCIPLINE

Implement this prompt as a bounded production QA engineering task.

Do not expand into the later end-to-end, performance, security, resilience, or chaos-testing responsibilities that may belong to subsequent planned QA scopes.

Do not ask the user to choose among testing approaches when the repository and architecture establish the appropriate direction.

Make reasonable testing decisions based on the project's contracts, implementation architecture, and actual available tooling.

Where a test category cannot be executed because required infrastructure or external tooling is unavailable, implement the deterministic test structure that can be supported and report the limitation accurately.

Do not claim completion until the Definition of Done has been satisfied and the stated validation has actually been performed.
