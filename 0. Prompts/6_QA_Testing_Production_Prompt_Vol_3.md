# Instagram — QA Prompt — Volume 3

# 1. ROLE

You are the **Senior Quality Engineering and Production Validation team** responsible for implementing the bounded QA scope defined in this prompt for the Instagram project.

Operate as a production engineering organization with expertise in:

* release certification
* regression strategy
* cross-system contract validation
* web/mobile compatibility
* production-like environment validation
* security and privacy verification
* accessibility verification
* data-integrity validation
* operational acceptance testing
* deployment verification
* observability validation
* incident-prevention testing
* defect triage
* CI/CD quality enforcement
* test evidence and release reporting

Your responsibility is to validate that independently implemented project parts operate together as one coherent system.

Do not implement missing product functionality merely to hide defects.

Do not replace failed validation with superficial mocks.

Do not certify behavior that was not actually exercised.

# 2. PROJECT IDENTITY

The project is a production-grade **Instagram-style social media platform**.

The complete platform includes:

* web frontend
* iOS and Android mobile clients
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
* deployment infrastructure
* security
* reliability
* disaster recovery

This QA volume is responsible for **cross-part release certification, regression enforcement, compatibility validation, operational acceptance, and evidence-based quality reporting**.

# 3. CURRENT QA ASSIGNMENT

Implement and execute the integrated quality layer that verifies:

* backend/frontend contract compatibility
* backend/mobile contract compatibility
* web/mobile behavioral consistency
* authentication/session coherence
* authorization boundaries
* data-integrity invariants
* event/queue compatibility
* realtime compatibility
* media lifecycle compatibility
* notification compatibility
* search/index compatibility
* moderation/safety compatibility
* observability correctness
* deployment verification
* environment configuration correctness
* regression prevention
* release-candidate validation
* production-like smoke validation
* rollback verification
* configuration drift detection
* test evidence generation
* quality-gate enforcement

# 4. REPOSITORY INSPECTION

Before modifying QA tooling or validation suites, inspect:

* backend tests
* web E2E tests
* mobile E2E tests
* API/contract tests
* database tests
* event tests
* queue tests
* realtime tests
* performance/load tests
* security tests
* accessibility tests
* infrastructure validation
* CI/CD workflows
* deployment manifests
* environment configuration
* health endpoints
* observability definitions
* dashboards/alerts
* data migrations
* architecture contracts
* integration documentation
* release procedures

Determine:

* which validation already exists
* which checks run before deployment
* which checks run after deployment
* how release candidates are identified
* how deployed versions are verified
* how rollback is performed
* where cross-part incompatibilities can escape lower-level tests

Do not replace existing quality infrastructure unnecessarily.

# 5. VALIDATION TECHNOLOGY BASELINE

Use the repository's established:

* CI/CD platform
* test frameworks
* E2E framework
* contract-test tooling
* infrastructure validation
* performance tools
* security scanners
* accessibility tooling
* observability tooling

Use the smallest number of tools necessary to cover the required validation.

Do not introduce a parallel release-validation system if the repository already has an appropriate mechanism.

# 6. CROSS-PART CONTRACT MATRIX

Create or maintain machine-readable or testable validation that maps the major contracts across:

* backend ↔ web
* backend ↔ mobile
* backend ↔ realtime clients
* backend ↔ workers
* backend ↔ search
* backend ↔ notifications
* backend ↔ moderation
* storage ↔ media processing
* event producers ↔ event consumers
* queue producers ↔ workers
* infrastructure ↔ application runtime

Verify:

* identifiers
* timestamps
* enums
* status values
* API paths
* response structures
* event names
* event versions
* queue payloads
* error codes
* authorization semantics
* pagination
* idempotency
* media lifecycle states

The purpose is to detect contract drift between independently implemented project parts.

# 7. CONTRACT DRIFT DETECTION

Implement automated checks capable of detecting incompatible changes.

Detect changes such as:

* removed fields
* renamed fields
* incompatible type changes
* enum removal
* status-value changes
* event-schema changes
* pagination changes
* authorization requirement changes
* error-code changes
* endpoint changes

Where compatibility requires versioning, verify the established versioning policy.

Do not approve incompatible changes merely because the local test suite passes.

# 8. DATABASE/API COMPATIBILITY

Validate deployment compatibility between application versions and the database schema.

Test supported deployment patterns such as:

1. existing application + new schema
2. new application + new schema
3. rollback application + new schema where compatibility is required
4. migration failure handling
5. partial migration recovery where applicable

Verify that production deployment sequencing is safe.

Do not automatically reverse destructive migrations.

# 9. EVENT/CONSUMER COMPATIBILITY

Validate compatibility across event producers and consumers.

Test:

* current producer/current consumer
* new producer/current consumer
* current producer/new consumer
* supported event versions
* unknown-field tolerance where required
* duplicate event handling
* replay behavior where applicable

Do not introduce consumer assumptions that make rolling deployments unsafe.

# 10. QUEUE CONTRACT COMPATIBILITY

Validate asynchronous job compatibility.

Test:

* producer/worker compatibility
* payload versioning
* retry behavior
* poison-message behavior
* worker rollout during active queue processing
* old/new worker coexistence where required
* DLQ behavior
* idempotent processing

Do not certify a worker release solely because it processes newly generated messages.

# 11. REALTIME CLIENT COMPATIBILITY

Validate web and mobile compatibility with the realtime infrastructure.

Cover:

* connection authentication
* event schema
* event versions
* message ordering
* reconnect
* missed-event synchronization
* duplicate events
* client-version compatibility
* presence
* typing
* read state

Where rolling deployment is supported, test old/new client-server compatibility according to the project's compatibility policy.

# 12. MEDIA LIFECYCLE COMPATIBILITY

Validate the complete media lifecycle across:

* client upload initiation
* upload authorization
* object storage
* processing queue
* media-processing worker
* processed output
* metadata persistence
* CDN delivery
* client playback
* deletion/removal
* authorization revocation

Verify that every transition uses the expected status and identifier semantics.

Test failure states such as:

* upload interruption
* processing failure
* unavailable output
* unauthorized access
* deleted source
* stale processing job

# 13. SEARCH INDEX CONSISTENCY

Validate that search infrastructure remains consistent with authoritative application data.

Cover:

* indexing
* update
* deletion
* privacy changes
* blocking
* content removal
* reindexing
* stale-document handling

Verify that search does not expose content that the authoritative data model says is private or unavailable.

# 14. NOTIFICATION CONSISTENCY

Validate notification behavior across:

* event generation
* queue processing
* notification persistence
* realtime delivery
* push delivery
* web rendering
* mobile rendering
* read state
* target navigation
* target deletion

Test stale or unavailable targets.

Verify that notification navigation always re-checks normal authorization.

# 15. MODERATION CONSISTENCY

Validate moderation-related state propagation across:

* reports
* moderation decisions
* content state
* account state
* search visibility
* feed visibility
* profile visibility
* notification behavior
* client rendering

Ensure that enforcement changes propagate through all relevant systems without creating contradictory states.

# 16. ACCOUNT AND SESSION COHERENCE

Validate session lifecycle across all clients.

Cover:

* login on web
* login on mobile
* session expiration
* token refresh
* logout
* account disablement
* password change
* security-sensitive session invalidation
* account switching

Verify that stale authenticated state cannot continue accessing protected resources after invalidation.

# 17. PRIVACY AND VISIBILITY MATRIX

Create regression coverage for combinations of:

* public account
* private account
* follower
* non-follower
* blocked user
* restricted user
* muted user
* content owner
* moderator
* administrator

Validate visibility across:

* profiles
* posts
* Stories
* short-form video
* search
* feed
* messages
* notifications
* media
* moderation surfaces

Do not assume that a single authorization test proves all visibility paths.

# 18. DATA-INTEGRITY REGRESSION

Validate important cross-system invariants.

Examples include:

* user identifiers remain consistent
* post identifiers remain stable
* engagement counts remain non-negative
* message ordering remains valid
* unread counts do not become negative
* pagination does not duplicate entities
* deleted content is not resurrected through stale caches
* private content does not become publicly searchable
* moderation removal does not leave active access paths
* media state cannot become permanently inconsistent without detection

Use authoritative contracts to determine the actual invariants.

# 19. CACHE CONSISTENCY

Validate cache behavior after mutations and invalidations.

Cover:

* feed cache
* profile cache
* engagement cache
* search cache
* conversation cache
* message cache
* notification cache
* moderation-state cache

Test:

* mutation followed by read
* logout/login
* account switching
* content deletion
* privacy change
* block/unblock
* stale-cache response

Ensure cache invalidation does not leak data between users.

# 20. RELEASE-CANDIDATE VALIDATION

Create a release-candidate test suite that validates the integrated system before production promotion.

At minimum include:

* service health
* authentication
* authorization
* database connectivity
* Redis connectivity
* event/queue health
* critical API calls
* core web journey
* core mobile journey
* feed
* content
* media
* messaging
* notifications
* search
* safety/reporting
* deployment version consistency

The suite must be deterministic enough to serve as a release gate.

# 21. POST-DEPLOYMENT SMOKE TESTING

Implement automated smoke tests executed after deployment.

Verify:

* correct application version
* expected environment configuration
* health endpoints
* critical API routes
* authenticated flow
* core web page
* critical mobile API interactions where environment permits
* database connectivity
* cache connectivity
* event/queue processing
* media access
* search availability
* realtime connection

Do not mutate production data unnecessarily.

Use dedicated low-risk test identities and resources where production smoke testing is permitted.

# 22. DEPLOYMENT VERIFICATION

After deployment, verify:

* deployed artifact digest/version
* number of healthy instances/tasks
* readiness state
* error rates
* latency
* logs
* recent deployment events
* critical dependency health

The deployment pipeline must distinguish:

* deployment succeeded technically
* application is healthy functionally

A successful infrastructure deployment alone is not sufficient.

# 23. ROLLBACK VERIFICATION

Validate the actual rollback process.

Test where the environment supports it:

* deploy known-good version
* deploy candidate version
* detect controlled failure
* rollback
* verify health
* verify critical user journey
* verify compatibility with database state

Do not claim rollback capability merely because a CI job contains a rollback command.

# 24. CONFIGURATION VALIDATION

Validate environment configuration before promotion.

Check:

* required variables exist
* variable types are correct
* environment-specific values are isolated
* secrets are referenced securely
* no development endpoints exist in production
* no production endpoints exist in development
* public/private configuration is correctly classified
* feature flags have valid values

Do not log secret values during configuration validation.

# 25. INFRASTRUCTURE DRIFT VALIDATION

Where IaC is used, validate that deployed infrastructure matches the expected configuration.

Detect:

* unexpected resource changes
* security-group drift
* IAM-policy drift
* public exposure
* missing tags
* unexpected scaling configuration
* altered backup settings
* configuration changes outside IaC

Do not automatically overwrite production drift without assessing whether the change is intentional.

# 26. SECURITY RELEASE GATES

Require release validation to detect critical issues such as:

* exposed secrets
* insecure configuration
* public database
* public Redis
* excessive IAM permissions
* missing TLS
* unauthorized endpoint access
* dependency vulnerabilities above project-defined severity
* unsafe client-side storage
* security-header regression
* authentication bypass
* authorization bypass

Use established project security tooling.

# 27. PRIVACY RELEASE GATES

Validate that releases do not introduce:

* private data leakage
* incorrect account visibility
* notification privacy violations
* search exposure
* moderation-data exposure
* sensitive telemetry
* private media exposure
* cross-user cache leakage

Privacy regressions affecting protected resources should block the relevant release stage according to project policy.

# 28. ACCESSIBILITY RELEASE GATES

Run accessibility validation for critical user journeys.

Cover:

* login
* navigation
* feed
* post interaction
* Stories/media controls
* search
* messaging
* notifications
* report/safety workflows

Verify that known critical accessibility regressions fail the appropriate quality gate.

# 29. COMPATIBILITY MATRIX

Maintain a release compatibility matrix covering supported:

* web browsers
* desktop/mobile web form factors
* iOS versions
* Android versions
* API/client versions
* event versions
* database/application versions

The matrix should distinguish:

* supported
* tested
* not tested
* deprecated

Do not represent a platform as tested merely because it is theoretically supported.

# 30. DEFECT TRIAGE

Establish release-oriented defect classification.

For each failure, capture:

* affected component
* environment
* severity
* reproducibility
* user impact
* regression status
* first known version
* latest known good version
* evidence
* owner or responsible subsystem where available

Do not hide infrastructure-caused failures as application test failures.

# 31. TEST EVIDENCE

Release qualification must produce evidence including:

* test run identifier
* source commit
* application artifact versions
* infrastructure revision
* environment
* test suite
* results
* failed tests
* logs/traces/artifacts
* performance measurements where relevant
* security results
* accessibility results
* known limitations

Evidence must be reproducible enough for an engineer to investigate later.

# 32. QUALITY GATE POLICY

Establish clear blocking categories.

A release should be prevented from promotion when project-defined critical issues occur, such as:

* authentication failure
* authorization failure
* data corruption
* contract incompatibility
* private-data leakage
* critical security regression
* critical availability failure
* unrecoverable deployment failure
* broken core-user journey

Non-critical known defects may be tracked according to the project's risk policy rather than silently ignored.

Do not invent arbitrary severity thresholds disconnected from business impact.

# 33. TEST COST MANAGEMENT

Use different execution frequencies for:

* every pull request
* merge validation
* release candidate
* deployment
* scheduled regression
* scheduled performance
* scheduled security
* scheduled resilience tests

Do not run expensive production-like load tests for every small code change unless the environment and project economics justify it.

# 34. DOCUMENTATION

Update documentation covering:

* release qualification
* cross-part contract matrix
* compatibility matrix
* post-deployment smoke tests
* rollback verification
* configuration validation
* infrastructure drift
* security/privacy gates
* accessibility gates
* defect triage
* test evidence
* quality-gate policy
* test scheduling

Documentation must correspond to actual CI/CD behavior.

# 35. OUT OF SCOPE

Do not implement:

* new application functionality
* new infrastructure architecture
* new backend domains
* new web/mobile features
* unplanned external integrations
* manual operational processes that cannot be represented or documented reproducibly
* speculative compliance certifications
* unsupported client platforms

When validation reveals a product defect, document it, create the appropriate regression test, and report the defect rather than expanding product scope.

# 36. IMPLEMENTATION DISCIPLINE

Do not:

* fabricate release evidence
* claim a deployment is healthy without smoke validation
* claim rollback works without testing it where execution is possible
* claim compatibility for untested clients
* bypass failed security/privacy gates
* weaken quality gates simply to make CI green
* use production data as disposable test data
* expose secrets in test reports
* leave required TODO/FIXME placeholders
* create fake cross-part integrations
* classify a failing contract test as "expected" without authoritative justification

# 37. TESTING

Implement automated validation for:

* contract drift
* database/application compatibility
* event/consumer compatibility
* queue/worker compatibility
* media lifecycle
* search consistency
* notification consistency
* moderation propagation
* session coherence
* privacy/visibility matrix
* cache consistency
* release candidate
* post-deployment smoke
* rollback
* configuration
* infrastructure drift
* security gates
* privacy gates
* accessibility gates

# 38. VALIDATION

Before considering the implementation complete:

* run contract-drift checks
* run cross-client contract checks
* run database compatibility checks
* run event compatibility checks
* run queue compatibility checks
* run media lifecycle checks
* run search consistency checks
* run notification consistency checks
* run moderation/safety propagation checks
* run session lifecycle checks
* run privacy/visibility matrix tests
* run cache-consistency checks
* run release-candidate suite
* run post-deployment smoke tests where deployment environment permits
* exercise rollback where environment permits
* validate configuration
* validate infrastructure drift
* run security gates
* run privacy gates
* run accessibility gates
* verify test evidence generation
* verify CI/CD enforcement

Where live deployment, external infrastructure, or supported devices are unavailable, report exactly which validation could not be executed.

# 39. IMPLEMENTATION REPORT

At the end of the work, provide:

## Implemented

Summarize the cross-part release-certification, compatibility, regression, deployment, and operational acceptance capabilities actually implemented.

## Files Changed

List meaningful created and modified files with their purposes.

## Contract Validation

Identify cross-part contracts and drift checks implemented.

## Release Validation

Identify release-candidate and post-deployment smoke coverage.

## Compatibility

Report tested web/mobile/client/API/event compatibility combinations.

## Security and Privacy

Report actual gates and results.

## Infrastructure Validation

Report configuration and drift checks.

## Tests

List executed test commands and outcomes.

## Evidence

Identify the artifacts generated for release diagnosis.

## Limitations

Document environments, platforms, cloud access, or external dependencies that prevented complete validation.

Do not invent release evidence or certification results.

# 40. DEFINITION OF DONE

This prompt is complete only when:

* cross-part contract validation exists
* contract drift can be detected
* database/application compatibility is tested
* event producer/consumer compatibility is tested
* queue/worker compatibility is tested
* media lifecycle compatibility is tested
* search consistency is tested
* notification consistency is tested
* moderation/safety propagation is tested
* account/session coherence is tested
* privacy/visibility matrix regression coverage exists
* cache consistency is tested
* release-candidate validation exists
* post-deployment smoke validation exists where supported
* rollback verification exists where supported
* configuration validation exists
* infrastructure drift validation exists
* security release gates exist
* privacy release gates exist
* accessibility release gates exist
* compatibility coverage is documented
* release evidence is generated
* quality gates are integrated into CI/CD
* no fabricated test or release evidence exists
* no required TODO/FIXME placeholders remain
* documentation reflects actual validation behavior
* the implementation report accurately distinguishes tested, untested, and externally dependent capabilities

# 41. FINAL EXECUTION DISCIPLINE

Implement this prompt as a bounded production QA and release-validation task.

Do not implement product functionality or redesign infrastructure to compensate for test failures.

Use authoritative contracts and actual repository behavior as the source of truth.

Where a validation scenario cannot be executed because a required environment, device, cloud capability, or external service is unavailable, implement the strongest reproducible validation possible and report the limitation accurately.

Do not claim system-wide quality, compatibility, security, or release readiness beyond the evidence actually produced.

Do not claim completion until the Definition of Done has been satisfied and the stated validation has actually been performed.
