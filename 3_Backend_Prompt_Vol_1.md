You are operating in Senior Engineering Team Mode.

The Master Prompt and both Architecture volumes have already been completed and approved.

The architecture is now the source of truth.

Your task in this phase is to begin the REAL BACKEND IMPLEMENTATION for the Instagram-like global visual-social platform.

This is implementation, not architecture discussion.

Inspect the existing repository before making changes.

Do not restart or replace existing work.

Do not regenerate unchanged files.

Do not invent architectural behavior that conflicts with the approved architecture.

==================================================
BACKEND VOLUME 1 SCOPE
======================

This volume establishes the backend foundation and implements the first core business domains.

Implement:

1. Backend project foundation
2. NestJS application architecture
3. Configuration management
4. Logging and request context
5. Error handling
6. Validation
7. Database and Prisma foundation
8. Redis foundation
9. Event/outbox foundation
10. BullMQ foundation
11. Authentication
12. Accounts
13. Profiles
14. Devices and sessions
15. Social graph foundation
16. Follow relationships
17. Follow requests
18. Blocks
19. Restrictions
20. Close Friends
21. Security and authorization foundation
22. API documentation
23. Initial automated tests

==================================================
IMPLEMENTATION RULES
====================

Every implementation must be production-grade.

Never generate:

- pseudo-code
- TODOs
- placeholders
- empty services
- fake implementations
- fake API responses
- unfinished methods
- commented-out "future" code

Every generated file must compile.

Every database migration must be valid.

Every API endpoint must be validated and authorized.

Every state-changing operation must define transaction boundaries.

Every important asynchronous side effect must use the approved event/outbox architecture.

Every implementation must preserve backward compatibility with previously existing repository code.

==================================================
BACKEND ARCHITECTURE
====================

Use:

- Node.js
- NestJS
- TypeScript
- PostgreSQL
- Prisma
- Redis
- Kafka or Redpanda
- BullMQ
- OpenSearch/Elasticsearch integration boundaries
- AWS S3 integration boundaries
- OpenTelemetry

Do not implement frontend, mobile, or infrastructure in this volume.

==================================================

1. PROJECT FOUNDATION
   ==================================================

Inspect the current repository and establish the backend application structure.

Use a maintainable organization separating:

- domain
- application
- infrastructure
- interfaces/API
- configuration
- shared kernel
- testing

Organize business modules by bounded context.

Avoid a flat directory containing every service and controller.

==================================================
2. NESTJS BOOTSTRAP
===================

Implement:

- application bootstrap
- global validation
- global exception handling
- configuration initialization
- structured logging
- security headers where appropriate
- request correlation
- graceful shutdown
- health infrastructure

Configure production-safe defaults.

==================================================
3. CONFIGURATION
================

Create strongly typed configuration for:

- application
- database
- Redis
- Kafka/Redpanda
- BullMQ
- storage
- search
- authentication
- security
- observability

Validate required configuration at startup.

Never silently continue with missing required configuration.

Never log secrets.

==================================================
4. REQUEST CONTEXT
==================

Implement request context containing where appropriate:

- request ID
- correlation ID
- authenticated user ID
- session ID
- trace context

The context must be available to:

- logs
- application services
- events
- background jobs

Do not place unnecessary sensitive information into logs.

==================================================
5. ERROR ARCHITECTURE
=====================

Create standardized backend error handling.

Support categories such as:

- validation
- authentication
- authorization
- not found
- conflict
- rate limiting
- dependency failure
- internal failure

API responses must use the approved error contract.

Do not expose stack traces in production responses.

==================================================
6. VALIDATION
=============

Implement request validation for:

- params
- query parameters
- request bodies
- headers where appropriate

Reject:

- unexpected fields where appropriate
- malformed identifiers
- invalid enums
- invalid pagination
- oversized values

==================================================
7. DATABASE FOUNDATION
======================

Configure Prisma.

Establish:

- datasource
- client lifecycle
- migrations
- transaction utilities
- repository conventions

Implement the foundational models required by this volume.

Do not attempt to create every model from the entire platform at once.

==================================================
8. DATABASE TRANSACTION PATTERN
===============================

Create reusable patterns for transactional use cases.

A use case performing:

- database mutation
- invariant validation
- outbox insertion

must be able to perform those operations atomically.

==================================================
9. REDIS FOUNDATION
===================

Create a Redis abstraction.

Support:

- get
- set
- delete
- TTL
- atomic operations
- distributed locking where required

Do not expose raw Redis clients throughout every domain.

Provide domain-appropriate abstractions over infrastructure access.

==================================================
10. REDIS KEY STRATEGY
======================

Create consistent namespacing.

Keys must identify:

- environment
- domain
- entity
- purpose

Temporary keys must have explicit TTL.

Do not create unbounded cache keys.

==================================================
11. EVENT / OUTBOX FOUNDATION
=============================

Implement the transactional outbox pattern.

Create:

- OutboxEvent
- event envelope
- publisher
- publishing worker/process
- retry handling
- dead-letter strategy

The transactional pattern must be:

Database transaction
→ domain state change
→ outbox record
→ publisher
→ Kafka/Redpanda

Never publish a critical domain event independently of the source transaction when atomicity is required.

==================================================
12. EVENT ENVELOPE
==================

Every integration event must contain:

- eventId
- eventType
- schemaVersion
- timestamp
- producer
- aggregateId
- correlationId
- causationId where applicable
- payload

==================================================
13. EVENT IDEMPOTENCY
=====================

Create infrastructure for idempotent event consumption.

Consumers must be able to safely handle duplicate delivery.

Do not assume exactly-once delivery.

==================================================
14. BULLMQ FOUNDATION
=====================

Create queue infrastructure for asynchronous work.

Establish:

- queue registration
- job configuration
- retries
- exponential backoff where appropriate
- timeout
- concurrency
- failure handling
- graceful shutdown

Do not create feature-specific queues unless this volume requires them.

==================================================
15. HEALTH CHECKS
=================

Implement health endpoints.

Separate:

- liveness
- readiness

Readiness may check required dependencies.

Liveness must not restart healthy instances merely because an external dependency is temporarily unavailable.

==================================================
16. SECURITY FOUNDATION
=======================

Implement shared security infrastructure for:

- authentication
- authorization
- guards
- roles/permissions where applicable
- request validation
- rate-limit integration
- secure headers
- audit context

==================================================
17. AUTHENTICATION
==================

Implement:

- registration
- login
- logout
- session creation
- session validation
- session revocation
- credential verification
- password hashing
- password change
- password reset architecture
- account verification architecture

Use secure password hashing.

Never store plaintext passwords.

==================================================
18. AUTHENTICATION SESSION MODEL
================================

Implement session state with:

- session ID
- user ID
- creation time
- expiration
- revocation
- device reference
- security metadata

Define session lifecycle explicitly.

==================================================
19. TOKEN/SESSION SECURITY
==========================

Use the authentication strategy defined by the architecture.

Protect against:

- session fixation
- replay
- expired sessions
- revoked sessions
- token misuse

Do not place sensitive tokens in logs.

==================================================
20. ACCOUNT DOMAIN
==================

Implement Account/User functionality.

Support:

- create account
- retrieve current account
- account status
- update allowed account data
- deactivate where supported
- deletion request foundation

Account states must follow the approved architecture.

==================================================
21. USER IDENTITY
=================

Implement globally unique user identifiers.

Do not use predictable public identifiers when the architecture requires opaque IDs.

==================================================
22. DEVICE DOMAIN
=================

Implement device registration.

Store only the device metadata required by the architecture.

Support:

- register device
- update device
- revoke device
- list authorized devices

Do not store unnecessary device-sensitive information.

==================================================
23. PROFILE DOMAIN
==================

Implement:

- profile creation
- profile retrieval
- profile update
- username
- display name
- biography
- links
- avatar metadata
- public/private state

Separate account identity from profile presentation.

==================================================
24. USERNAME MANAGEMENT
=======================

Implement:

- username validation
- uniqueness
- normalization
- safe lookup
- update

Define canonical username rules.

Prevent ambiguous representations where possible.

==================================================
25. PROFILE PRIVACY
===================

Implement public/private account behavior.

Profile visibility must integrate with authorization.

Private profiles must not expose protected data to unauthorized users.

==================================================
26. CREATOR/PROFESSIONAL PROFILE FOUNDATION
===========================================

Implement the foundational data model for:

- creator
- professional
- business

Do not implement full analytics, advertising, commerce, or monetization yet.

Create the domain extension points needed by later volumes.

==================================================
27. SOCIAL GRAPH FOUNDATION
===========================

Implement relationship infrastructure.

Support:

- follow
- follow request
- block
- restriction
- close friends

Define explicit relationship states.

==================================================
28. FOLLOW
==========

Implement:

- follow user
- unfollow user
- get follow state

For public accounts:

follow should create the appropriate relationship immediately.

For private accounts:

follow should create a follow request.

Use transaction boundaries.

==================================================
29. FOLLOW REQUESTS
===================

Implement:

- create request
- cancel request
- accept request
- decline request
- list incoming requests
- list outgoing requests where required

State transitions must be guarded.

==================================================
30. FOLLOW IDEMPOTENCY
======================

Repeated follow requests must not create duplicate relationship records.

Repeated unfollow operations must be safe.

Concurrent requests must resolve correctly according to the domain rules.

==================================================
31. BLOCK
=========

Implement:

- block
- unblock
- block status
- blocked-account listing

Blocking must have precedence over normal relationship-based access.

==================================================
32. BLOCK SIDE EFFECTS
======================

Define and implement the required immediate effects of blocking.

At minimum address:

- follow relationships
- pending follow requests
- interaction permissions
- messaging eligibility where applicable
- cached authorization state

Do not leave stale access accidentally available.

==================================================
33. RESTRICTION
===============

Implement:

- restrict
- unrestrict
- restriction state
- restricted-account listing where required

Use backend policy logic.

==================================================
34. CLOSE FRIENDS
=================

Implement:

- add close friend
- remove close friend
- list close friends
- membership state

Ensure close-friend lists are private to the owner.

==================================================
35. AUTHORIZATION POLICIES
==========================

Create reusable authorization policies for:

- account ownership
- profile editing
- following
- follow requests
- blocking
- restrictions
- close friends

Do not duplicate checks across controllers.

==================================================
36. PRIVACY POLICIES
====================

Implement reusable policy evaluation for:

- public profile
- private profile
- follower
- blocked user
- restricted user
- owner

This policy layer will be reused by content, stories, messaging, and discovery in later volumes.

==================================================
37. RATE LIMITING
=================

Apply rate-limit architecture to:

- login
- registration
- password reset
- username changes
- follow
- follow request
- block
- high-risk account operations

Use Redis-backed distributed state where required.

==================================================
38. SECURITY AUDIT LOGGING
==========================

Create audit events for security-sensitive actions:

- login
- logout
- password change
- session revocation
- account changes
- follow actions where required
- block
- privacy changes

Do not store credentials.

==================================================
39. API DESIGN
==============

Implement REST endpoints according to the approved API architecture.

Suggested groups:

/auth
/accounts
/profiles
/social
/sessions
/devices

Use consistent naming.

Every endpoint must define:

- authentication
- authorization
- validation
- success response
- error response

==================================================
40. API DOCUMENTATION
=====================

Integrate OpenAPI/Swagger documentation.

Document:

- authentication requirements
- request bodies
- responses
- errors
- pagination
- security requirements

Keep documentation synchronized with implementation.

==================================================
41. PAGINATION
==============

Use cursor pagination for:

- follow lists
- followers
- following
- follow requests
- blocked users
- restricted users
- close friends where large enough

Define opaque cursors.

==================================================
42. CACHE STRATEGY
==================

Cache only appropriate derived/read-heavy information.

Potential caches:

- profile summary
- follow state
- public profile data
- social counters where applicable

Never cache private information without explicit authorization-aware design.

==================================================
43. CACHE INVALIDATION
======================

A mutation must invalidate/update relevant cache state.

Examples:

Follow:

- target profile
- follower count
- current relationship

Block:

- relationship state
- authorization-related cached state

Privacy change:

- profile visibility
- affected derived caches

==================================================
44. EVENTS
==========

Define and publish appropriate events such as:

- UserRegistered
- UserLoggedIn
- SessionCreated
- SessionRevoked
- ProfileUpdated
- FollowCreated
- FollowRemoved
- FollowRequestCreated
- FollowRequestAccepted
- FollowRequestDeclined
- UserBlocked
- UserUnblocked
- UserRestricted
- UserUnrestricted
- CloseFriendAdded
- CloseFriendRemoved

Use the approved event envelope.

==================================================
45. ASYNC SIDE EFFECTS
======================

Where future domains depend on these events, publish them through the outbox.

Do not synchronously call unrelated future domains merely to simulate integration.

==================================================
46. SECURITY REQUIREMENTS
=========================

Test protection against:

- duplicate registration
- account enumeration
- username enumeration where inappropriate
- brute-force login
- session replay
- unauthorized profile update
- IDOR
- follow manipulation
- block bypass
- private profile access
- privilege escalation

==================================================
47. TESTING
===========

Implement tests for:

Unit:

- username normalization
- account state
- authorization
- privacy
- follow state
- block state
- restriction
- close friends
- session rules

Integration:

- PostgreSQL
- Redis
- authentication
- social graph
- outbox
- event publishing

E2E/API:

- registration
- login
- logout
- profile
- follow
- private-account request
- request acceptance
- block
- restrict
- close friends

==================================================
48. CONCURRENCY TESTING
=======================

Test concurrent:

- follow
- unfollow
- follow request
- accept request
- block
- unblock

Verify there are no duplicate or contradictory relationship states.

==================================================
49. EVENT TESTING
=================

Test:

- outbox creation
- successful publication
- publication failure
- retry
- duplicate delivery
- correlation IDs
- dead-letter behavior

==================================================
50. SECURITY TESTING
====================

Test:

- invalid credentials
- expired session
- revoked session
- unauthorized profile mutation
- private profile access
- block bypass
- restricted access
- rate-limit behavior

==================================================
51. MIGRATIONS
==============

All database changes must use Prisma migrations.

Migration names must be descriptive.

Do not manually modify production databases outside the established migration process.

==================================================
52. OBSERVABILITY
=================

Instrument:

- authentication
- profile operations
- relationship mutations
- database calls
- Redis operations
- event publishing
- queue operations

Expose:

- metrics
- structured logs
- traces

Never expose secrets in telemetry.

==================================================
53. GRACEFUL SHUTDOWN
=====================

Ensure the backend safely shuts down:

- HTTP server
- Prisma
- Redis
- Kafka producers/consumers
- BullMQ
- telemetry

==================================================
54. DOCUMENTATION
=================

Update backend documentation with:

- module map
- setup instructions
- environment variables
- database setup
- migrations
- authentication
- social graph
- API endpoints
- events
- local development
- testing

Documentation must match the actual implementation.

==================================================
55. IMPLEMENTATION DISCIPLINE
=============================

Before each change:

1. Inspect the current repository.
2. Identify existing files and abstractions.
3. Reuse existing code.
4. Determine dependencies.
5. Implement the smallest coherent change.
6. Add tests.
7. Validate.
8. Fix failures.
9. Continue.

Never overwrite unchanged files.

==================================================
56. VALIDATION
==============

Run the repository-supported:

- formatter
- lint
- typecheck
- unit tests
- integration tests
- API/E2E tests
- build

If a validation command fails:

1. determine whether the failure is caused by your changes;
2. fix the implementation;
3. rerun the validation.

Never suppress errors simply to obtain a passing result.

==================================================
FINAL ACCEPTANCE CRITERIA
=========================

Backend Volume 1 is complete when:

FOUNDATION

- NestJS application boots;
- configuration is validated;
- request context exists;
- errors are standardized;
- validation exists;
- health checks exist;
- graceful shutdown works.

DATABASE

- Prisma is configured;
- migrations work;
- repositories are organized;
- transactions are supported.

REDIS

- Redis abstraction exists;
- key conventions exist;
- TTLs are applied appropriately.

EVENTS

- transactional outbox exists;
- event envelope exists;
- publishing works;
- retry/idempotency foundations exist.

QUEUES

- BullMQ foundation exists;
- job lifecycle is defined.

AUTHENTICATION

- registration works;
- login works;
- logout works;
- sessions work;
- revocation works;
- password security works.

ACCOUNTS

- account lifecycle foundation works;
- devices work;
- profiles work;
- usernames work;
- privacy state works.

SOCIAL GRAPH

- follow works;
- unfollow works;
- private-account requests work;
- requests can be accepted/declined;
- block works;
- restriction works;
- close friends work.

SECURITY

- authorization works;
- privacy policies work;
- rate limiting is integrated;
- security events are auditable.

API

- endpoints are documented;
- validation works;
- errors are standardized;
- pagination is implemented where required.

TESTING

- unit tests exist;
- integration tests exist;
- critical API/E2E tests exist;
- concurrency cases are covered;
- security cases are covered.

The repository must remain buildable and testable at the end of this volume.

==================================================
DO NOT IMPLEMENT IN THIS VOLUME
===============================

Do not implement:

- posts
- carousels
- stories
- reels
- feed
- recommendations
- search
- messaging
- notifications
- advertising
- commerce
- monetization
- advanced analytics
- infrastructure
- Kubernetes
- Terraform
- frontend
- mobile application

Those systems must consume the foundation established here in later implementation volumes.

BEGIN WITH:

1. INSPECT THE EXISTING BACKEND REPOSITORY.
2. ESTABLISH THE NESTJS/BACKEND FOUNDATION.
3. IMPLEMENT THE DATABASE/PRISMA FOUNDATION.
4. IMPLEMENT AUTHENTICATION, ACCOUNTS, PROFILES, AND SOCIAL GRAPH FOUNDATION

You are operating in Senior Engineering Team Mode.

The Master Prompt and both Architecture volumes have already been completed and approved.

The architecture is now the source of truth.

Your task in this phase is to begin the REAL BACKEND IMPLEMENTATION for the Instagram-like global visual-social platform.

This is implementation, not architecture discussion.

Inspect the existing repository before making changes.

Do not restart or replace existing work.

Do not regenerate unchanged files.

Do not invent architectural behavior that conflicts with the approved architecture.

==================================================
BACKEND VOLUME 1 SCOPE
======================

This volume establishes the backend foundation and implements the first core business domains.

Implement:

1. Backend project foundation
2. NestJS application architecture
3. Configuration management
4. Logging and request context
5. Error handling
6. Validation
7. Database and Prisma foundation
8. Redis foundation
9. Event/outbox foundation
10. BullMQ foundation
11. Authentication
12. Accounts
13. Profiles
14. Devices and sessions
15. Social graph foundation
16. Follow relationships
17. Follow requests
18. Blocks
19. Restrictions
20. Close Friends
21. Security and authorization foundation
22. API documentation
23. Initial automated tests

==================================================
IMPLEMENTATION RULES
====================

Every implementation must be production-grade.

Never generate:

- pseudo-code
- TODOs
- placeholders
- empty services
- fake implementations
- fake API responses
- unfinished methods
- commented-out "future" code

Every generated file must compile.

Every database migration must be valid.

Every API endpoint must be validated and authorized.

Every state-changing operation must define transaction boundaries.

Every important asynchronous side effect must use the approved event/outbox architecture.

Every implementation must preserve backward compatibility with previously existing repository code.

==================================================
BACKEND ARCHITECTURE
====================

Use:

- Node.js
- NestJS
- TypeScript
- PostgreSQL
- Prisma
- Redis
- Kafka or Redpanda
- BullMQ
- OpenSearch/Elasticsearch integration boundaries
- AWS S3 integration boundaries
- OpenTelemetry

Do not implement frontend, mobile, or infrastructure in this volume.

==================================================

1. PROJECT FOUNDATION
   ==================================================

Inspect the current repository and establish the backend application structure.

Use a maintainable organization separating:

- domain
- application
- infrastructure
- interfaces/API
- configuration
- shared kernel
- testing

Organize business modules by bounded context.

Avoid a flat directory containing every service and controller.

==================================================
2. NESTJS BOOTSTRAP
===================

Implement:

- application bootstrap
- global validation
- global exception handling
- configuration initialization
- structured logging
- security headers where appropriate
- request correlation
- graceful shutdown
- health infrastructure

Configure production-safe defaults.

==================================================
3. CONFIGURATION
================

Create strongly typed configuration for:

- application
- database
- Redis
- Kafka/Redpanda
- BullMQ
- storage
- search
- authentication
- security
- observability

Validate required configuration at startup.

Never silently continue with missing required configuration.

Never log secrets.

==================================================
4. REQUEST CONTEXT
==================

Implement request context containing where appropriate:

- request ID
- correlation ID
- authenticated user ID
- session ID
- trace context

The context must be available to:

- logs
- application services
- events
- background jobs

Do not place unnecessary sensitive information into logs.

==================================================
5. ERROR ARCHITECTURE
=====================

Create standardized backend error handling.

Support categories such as:

- validation
- authentication
- authorization
- not found
- conflict
- rate limiting
- dependency failure
- internal failure

API responses must use the approved error contract.

Do not expose stack traces in production responses.

==================================================
6. VALIDATION
=============

Implement request validation for:

- params
- query parameters
- request bodies
- headers where appropriate

Reject:

- unexpected fields where appropriate
- malformed identifiers
- invalid enums
- invalid pagination
- oversized values

==================================================
7. DATABASE FOUNDATION
======================

Configure Prisma.

Establish:

- datasource
- client lifecycle
- migrations
- transaction utilities
- repository conventions

Implement the foundational models required by this volume.

Do not attempt to create every model from the entire platform at once.

==================================================
8. DATABASE TRANSACTION PATTERN
===============================

Create reusable patterns for transactional use cases.

A use case performing:

- database mutation
- invariant validation
- outbox insertion

must be able to perform those operations atomically.

==================================================
9. REDIS FOUNDATION
===================

Create a Redis abstraction.

Support:

- get
- set
- delete
- TTL
- atomic operations
- distributed locking where required

Do not expose raw Redis clients throughout every domain.

Provide domain-appropriate abstractions over infrastructure access.

==================================================
10. REDIS KEY STRATEGY
======================

Create consistent namespacing.

Keys must identify:

- environment
- domain
- entity
- purpose

Temporary keys must have explicit TTL.

Do not create unbounded cache keys.

==================================================
11. EVENT / OUTBOX FOUNDATION
=============================

Implement the transactional outbox pattern.

Create:

- OutboxEvent
- event envelope
- publisher
- publishing worker/process
- retry handling
- dead-letter strategy

The transactional pattern must be:

Database transaction
→ domain state change
→ outbox record
→ publisher
→ Kafka/Redpanda

Never publish a critical domain event independently of the source transaction when atomicity is required.

==================================================
12. EVENT ENVELOPE
==================

Every integration event must contain:

- eventId
- eventType
- schemaVersion
- timestamp
- producer
- aggregateId
- correlationId
- causationId where applicable
- payload

==================================================
13. EVENT IDEMPOTENCY
=====================

Create infrastructure for idempotent event consumption.

Consumers must be able to safely handle duplicate delivery.

Do not assume exactly-once delivery.

==================================================
14. BULLMQ FOUNDATION
=====================

Create queue infrastructure for asynchronous work.

Establish:

- queue registration
- job configuration
- retries
- exponential backoff where appropriate
- timeout
- concurrency
- failure handling
- graceful shutdown

Do not create feature-specific queues unless this volume requires them.

==================================================
15. HEALTH CHECKS
=================

Implement health endpoints.

Separate:

- liveness
- readiness

Readiness may check required dependencies.

Liveness must not restart healthy instances merely because an external dependency is temporarily unavailable.

==================================================
16. SECURITY FOUNDATION
=======================

Implement shared security infrastructure for:

- authentication
- authorization
- guards
- roles/permissions where applicable
- request validation
- rate-limit integration
- secure headers
- audit context

==================================================
17. AUTHENTICATION
==================

Implement:

- registration
- login
- logout
- session creation
- session validation
- session revocation
- credential verification
- password hashing
- password change
- password reset architecture
- account verification architecture

Use secure password hashing.

Never store plaintext passwords.

==================================================
18. AUTHENTICATION SESSION MODEL
================================

Implement session state with:

- session ID
- user ID
- creation time
- expiration
- revocation
- device reference
- security metadata

Define session lifecycle explicitly.

==================================================
19. TOKEN/SESSION SECURITY
==========================

Use the authentication strategy defined by the architecture.

Protect against:

- session fixation
- replay
- expired sessions
- revoked sessions
- token misuse

Do not place sensitive tokens in logs.

==================================================
20. ACCOUNT DOMAIN
==================

Implement Account/User functionality.

Support:

- create account
- retrieve current account
- account status
- update allowed account data
- deactivate where supported
- deletion request foundation

Account states must follow the approved architecture.

==================================================
21. USER IDENTITY
=================

Implement globally unique user identifiers.

Do not use predictable public identifiers when the architecture requires opaque IDs.

==================================================
22. DEVICE DOMAIN
=================

Implement device registration.

Store only the device metadata required by the architecture.

Support:

- register device
- update device
- revoke device
- list authorized devices

Do not store unnecessary device-sensitive information.

==================================================
23. PROFILE DOMAIN
==================

Implement:

- profile creation
- profile retrieval
- profile update
- username
- display name
- biography
- links
- avatar metadata
- public/private state

Separate account identity from profile presentation.

==================================================
24. USERNAME MANAGEMENT
=======================

Implement:

- username validation
- uniqueness
- normalization
- safe lookup
- update

Define canonical username rules.

Prevent ambiguous representations where possible.

==================================================
25. PROFILE PRIVACY
===================

Implement public/private account behavior.

Profile visibility must integrate with authorization.

Private profiles must not expose protected data to unauthorized users.

==================================================
26. CREATOR/PROFESSIONAL PROFILE FOUNDATION
===========================================

Implement the foundational data model for:

- creator
- professional
- business

Do not implement full analytics, advertising, commerce, or monetization yet.

Create the domain extension points needed by later volumes.

==================================================
27. SOCIAL GRAPH FOUNDATION
===========================

Implement relationship infrastructure.

Support:

- follow
- follow request
- block
- restriction
- close friends

Define explicit relationship states.

==================================================
28. FOLLOW
==========

Implement:

- follow user
- unfollow user
- get follow state

For public accounts:

follow should create the appropriate relationship immediately.

For private accounts:

follow should create a follow request.

Use transaction boundaries.

==================================================
29. FOLLOW REQUESTS
===================

Implement:

- create request
- cancel request
- accept request
- decline request
- list incoming requests
- list outgoing requests where required

State transitions must be guarded.

==================================================
30. FOLLOW IDEMPOTENCY
======================

Repeated follow requests must not create duplicate relationship records.

Repeated unfollow operations must be safe.

Concurrent requests must resolve correctly according to the domain rules.

==================================================
31. BLOCK
=========

Implement:

- block
- unblock
- block status
- blocked-account listing

Blocking must have precedence over normal relationship-based access.

==================================================
32. BLOCK SIDE EFFECTS
======================

Define and implement the required immediate effects of blocking.

At minimum address:

- follow relationships
- pending follow requests
- interaction permissions
- messaging eligibility where applicable
- cached authorization state

Do not leave stale access accidentally available.

==================================================
33. RESTRICTION
===============

Implement:

- restrict
- unrestrict
- restriction state
- restricted-account listing where required

Use backend policy logic.

==================================================
34. CLOSE FRIENDS
=================

Implement:

- add close friend
- remove close friend
- list close friends
- membership state

Ensure close-friend lists are private to the owner.

==================================================
35. AUTHORIZATION POLICIES
==========================

Create reusable authorization policies for:

- account ownership
- profile editing
- following
- follow requests
- blocking
- restrictions
- close friends

Do not duplicate checks across controllers.

==================================================
36. PRIVACY POLICIES
====================

Implement reusable policy evaluation for:

- public profile
- private profile
- follower
- blocked user
- restricted user
- owner

This policy layer will be reused by content, stories, messaging, and discovery in later volumes.

==================================================
37. RATE LIMITING
=================

Apply rate-limit architecture to:

- login
- registration
- password reset
- username changes
- follow
- follow request
- block
- high-risk account operations

Use Redis-backed distributed state where required.

==================================================
38. SECURITY AUDIT LOGGING
==========================

Create audit events for security-sensitive actions:

- login
- logout
- password change
- session revocation
- account changes
- follow actions where required
- block
- privacy changes

Do not store credentials.

==================================================
39. API DESIGN
==============

Implement REST endpoints according to the approved API architecture.

Suggested groups:

/auth
/accounts
/profiles
/social
/sessions
/devices

Use consistent naming.

Every endpoint must define:

- authentication
- authorization
- validation
- success response
- error response

==================================================
40. API DOCUMENTATION
=====================

Integrate OpenAPI/Swagger documentation.

Document:

- authentication requirements
- request bodies
- responses
- errors
- pagination
- security requirements

Keep documentation synchronized with implementation.

==================================================
41. PAGINATION
==============

Use cursor pagination for:

- follow lists
- followers
- following
- follow requests
- blocked users
- restricted users
- close friends where large enough

Define opaque cursors.

==================================================
42. CACHE STRATEGY
==================

Cache only appropriate derived/read-heavy information.

Potential caches:

- profile summary
- follow state
- public profile data
- social counters where applicable

Never cache private information without explicit authorization-aware design.

==================================================
43. CACHE INVALIDATION
======================

A mutation must invalidate/update relevant cache state.

Examples:

Follow:

- target profile
- follower count
- current relationship

Block:

- relationship state
- authorization-related cached state

Privacy change:

- profile visibility
- affected derived caches

==================================================
44. EVENTS
==========

Define and publish appropriate events such as:

- UserRegistered
- UserLoggedIn
- SessionCreated
- SessionRevoked
- ProfileUpdated
- FollowCreated
- FollowRemoved
- FollowRequestCreated
- FollowRequestAccepted
- FollowRequestDeclined
- UserBlocked
- UserUnblocked
- UserRestricted
- UserUnrestricted
- CloseFriendAdded
- CloseFriendRemoved

Use the approved event envelope.

==================================================
45. ASYNC SIDE EFFECTS
======================

Where future domains depend on these events, publish them through the outbox.

Do not synchronously call unrelated future domains merely to simulate integration.

==================================================
46. SECURITY REQUIREMENTS
=========================

Test protection against:

- duplicate registration
- account enumeration
- username enumeration where inappropriate
- brute-force login
- session replay
- unauthorized profile update
- IDOR
- follow manipulation
- block bypass
- private profile access
- privilege escalation

==================================================
47. TESTING
===========

Implement tests for:

Unit:

- username normalization
- account state
- authorization
- privacy
- follow state
- block state
- restriction
- close friends
- session rules

Integration:

- PostgreSQL
- Redis
- authentication
- social graph
- outbox
- event publishing

E2E/API:

- registration
- login
- logout
- profile
- follow
- private-account request
- request acceptance
- block
- restrict
- close friends

==================================================
48. CONCURRENCY TESTING
=======================

Test concurrent:

- follow
- unfollow
- follow request
- accept request
- block
- unblock

Verify there are no duplicate or contradictory relationship states.

==================================================
49. EVENT TESTING
=================

Test:

- outbox creation
- successful publication
- publication failure
- retry
- duplicate delivery
- correlation IDs
- dead-letter behavior

==================================================
50. SECURITY TESTING
====================

Test:

- invalid credentials
- expired session
- revoked session
- unauthorized profile mutation
- private profile access
- block bypass
- restricted access
- rate-limit behavior

==================================================
51. MIGRATIONS
==============

All database changes must use Prisma migrations.

Migration names must be descriptive.

Do not manually modify production databases outside the established migration process.

==================================================
52. OBSERVABILITY
=================

Instrument:

- authentication
- profile operations
- relationship mutations
- database calls
- Redis operations
- event publishing
- queue operations

Expose:

- metrics
- structured logs
- traces

Never expose secrets in telemetry.

==================================================
53. GRACEFUL SHUTDOWN
=====================

Ensure the backend safely shuts down:

- HTTP server
- Prisma
- Redis
- Kafka producers/consumers
- BullMQ
- telemetry

==================================================
54. DOCUMENTATION
=================

Update backend documentation with:

- module map
- setup instructions
- environment variables
- database setup
- migrations
- authentication
- social graph
- API endpoints
- events
- local development
- testing

Documentation must match the actual implementation.

==================================================
55. IMPLEMENTATION DISCIPLINE
=============================

Before each change:

1. Inspect the current repository.
2. Identify existing files and abstractions.
3. Reuse existing code.
4. Determine dependencies.
5. Implement the smallest coherent change.
6. Add tests.
7. Validate.
8. Fix failures.
9. Continue.

Never overwrite unchanged files.

==================================================
56. VALIDATION
==============

Run the repository-supported:

- formatter
- lint
- typecheck
- unit tests
- integration tests
- API/E2E tests
- build

If a validation command fails:

1. determine whether the failure is caused by your changes;
2. fix the implementation;
3. rerun the validation.

Never suppress errors simply to obtain a passing result.

==================================================
FINAL ACCEPTANCE CRITERIA
=========================

Backend Volume 1 is complete when:

FOUNDATION

- NestJS application boots;
- configuration is validated;
- request context exists;
- errors are standardized;
- validation exists;
- health checks exist;
- graceful shutdown works.

DATABASE

- Prisma is configured;
- migrations work;
- repositories are organized;
- transactions are supported.

REDIS

- Redis abstraction exists;
- key conventions exist;
- TTLs are applied appropriately.

EVENTS

- transactional outbox exists;
- event envelope exists;
- publishing works;
- retry/idempotency foundations exist.

QUEUES

- BullMQ foundation exists;
- job lifecycle is defined.

AUTHENTICATION

- registration works;
- login works;
- logout works;
- sessions work;
- revocation works;
- password security works.

ACCOUNTS

- account lifecycle foundation works;
- devices work;
- profiles work;
- usernames work;
- privacy state works.

SOCIAL GRAPH

- follow works;
- unfollow works;
- private-account requests work;
- requests can be accepted/declined;
- block works;
- restriction works;
- close friends work.

SECURITY

- authorization works;
- privacy policies work;
- rate limiting is integrated;
- security events are auditable.

API

- endpoints are documented;
- validation works;
- errors are standardized;
- pagination is implemented where required.

TESTING

- unit tests exist;
- integration tests exist;
- critical API/E2E tests exist;
- concurrency cases are covered;
- security cases are covered.

The repository must remain buildable and testable at the end of this volume.

==================================================
DO NOT IMPLEMENT IN THIS VOLUME
===============================

Do not implement:

- posts
- carousels
- stories
- reels
- feed
- recommendations
- search
- messaging
- notifications
- advertising
- commerce
- monetization
- advanced analytics
- infrastructure
- Kubernetes
- Terraform
- frontend
- mobile application

Those systems must consume the foundation established here in later implementation volumes.

BEGIN WITH:

1. INSPECT THE EXISTING BACKEND REPOSITORY.
2. ESTABLISH THE NESTJS/BACKEND FOUNDATION.
3. IMPLEMENT THE DATABASE/PRISMA FOUNDATION.
4. IMPLEMENT AUTHENTICATION, ACCOUNTS, PROFILES, AND SOCIAL GRAPH FOUNDATION

You are operating in Senior Engineering Team Mode.

Build the production-ready backend foundation for an enterprise-scale global visual-social platform comparable in architectural scope to Instagram.

The platform is an original implementation.

Do not copy proprietary source code, internal architecture, branding, confidential implementation details, proprietary algorithms, proprietary datasets, private implementation details, or internal systems from Instagram, Meta, or any other company.

This prompt is completely independent and may be executed in a separate conversation.

The backend must strictly follow the approved Instagram-like architecture, bounded contexts, service boundaries, database ownership, media architecture, feed architecture, recommendation architecture, search architecture, messaging architecture, moderation architecture, rights architecture, analytics architecture, privacy architecture, security model, event architecture, queue architecture, and Project Index.

Do not redesign the architecture.

Do not generate frontend code.

Do not generate mobile code.

Do not generate infrastructure implementation code.

Do not generate Terraform.

Do not generate Kubernetes manifests.

Do not generate CI/CD workflows.

────────────────────────────────────────

MISSION

Build the production-ready backend foundation required for:

• Application bootstrap
• Configuration
• Request context
• Logging
• Error handling
• Validation
• API versioning
• Authentication foundation
• Authorization foundation
• Accounts
• Profiles
• Creator profiles
• Business profiles
• Devices
• Sessions
• Social graph
• Follows
• Follow requests
• Blocks
• Restrictions
• Close friends
• PostgreSQL
• Prisma
• Redis
• Kafka/Redpanda
• BullMQ
• WebSockets
• Socket.IO
• OpenTelemetry
• Health checks
• Graceful shutdown
• API contracts
• Event contracts
• Queue contracts
• Transactional Outbox
• Security foundations
• Privacy foundations
• Testing foundations
• Local development

The backend must eventually support:

• Posts
• Carousels
• Reels
• Stories
• Story highlights
• Media
• Image processing
• Video processing
• Audio
• Music
• Hashtags
• Mentions
• Locations
• Likes
• Comments
• Replies
• Saves
• Collections
• Shares
• Reposts
• Feed
• Explore
• Recommendations
• Trending
• Search
• Messaging
• Notifications
• Moderation
• Safety
• Reporting
• Rights
• Advertising
• Commerce
• Analytics
• Administration
• Feature flags
• Dynamic configuration
• Audit
• Privacy

────────────────────────────────────────

PRIMARY TECHNOLOGY STACK

Backend:

• Node.js
• NestJS
• TypeScript

Database:

• PostgreSQL
• Prisma ORM

Cache:

• Redis

Event streaming:

• Kafka or Redpanda

Background processing:

• BullMQ

Search:

• Elasticsearch or OpenSearch

Object storage:

• AWS S3

CDN:

• CloudFront

Media:

• FFmpeg
• Image processing abstraction
• Video transcoding
• HLS

Real-time:

• WebSockets
• Socket.IO

Notifications:

• FCM
• APNS
• Email provider abstraction

Observability:

• OpenTelemetry
• Prometheus
• Grafana
• Loki
• Tempo

Testing:

• Jest
• Supertest
• Integration testing tools

────────────────────────────────────────

IMPLEMENTATION RULES

Never generate pseudo-code.

Never generate placeholders.

Never generate TODO comments.

Never omit implementations.

Never say:

- "implement similarly"
- "left as an exercise"
- "for brevity"
- "remaining code omitted"

Every generated file must be complete.

Every generated file must compile.

Never regenerate unchanged files.

Only modify existing files when required.

Use strict TypeScript.

Use dependency injection.

Keep controllers thin.

Keep business logic outside controllers.

Use repositories for persistence.

Use DTOs for external contracts.

Use centralized validation.

Use centralized error handling.

Use structured logging.

Use idempotency for retriable operations.

Use optimistic concurrency where appropriate.

Never trust client-supplied ownership.

Never trust client-supplied visibility.

Never trust client-supplied moderation state.

Never trust client-supplied creator/business authority.

────────────────────────────────────────

BACKEND ARCHITECTURE

Use:

• Clean Architecture
• Domain-Driven Design
• SOLID
• Repository Pattern
• Service Layer
• Dependency Injection
• Feature-first organization
• Explicit domain ownership
• Event-driven architecture
• Transactional Outbox
• Idempotent consumers
• Stateless services where possible
• Horizontal scalability
• Regional processing
• Provider abstraction
• Graceful degradation

Use CQRS where justified.

The backend should allow future extraction of:

• Social Graph
• Media
• Feed
• Recommendations
• Search
• Messaging
• Moderation
• Rights
• Notifications
• Analytics

────────────────────────────────────────

MONOREPO FOUNDATION

Prepare structure such as:

apps/

• api-gateway

services/

• identity
• accounts
• profiles
• creators
• businesses
• devices
• social-graph
• content
• media
• stories
• reels
• feed
• recommendations
• explore
• trending
• search
• hashtags
• audio
• engagement
• comments
• collections
• messaging
• notifications
• moderation
• safety
• reports
• rights
• advertising
• commerce
• analytics
• privacy
• administration
• audit
• feature-flags
• configuration

workers/

• media-validation
• image-processing
• video-processing
• hls-processing
• thumbnail-generation
• story-expiration
• search-indexing
• trending
• notifications
• moderation
• rights
• analytics
• advertising
• commerce
• privacy
• cleanup
• reconciliation

packages/

• configuration
• logging
• errors
• validation
• database
• redis
• events
• queues
• observability
• api-contracts
• auth
• security
• storage
• providers
• testing

────────────────────────────────────────

APPLICATION BOOTSTRAP

Implement:

• NestJS initialization
• Configuration bootstrap
• Global validation
• Global exception filter
• Structured logger
• Request ID
• Correlation ID
• Trace ID
• CORS
• Secure headers
• Body-size limits
• API versioning
• OpenAPI
• Graceful shutdown
• Health checks

Production behavior must be secure by default.

────────────────────────────────────────

CONFIGURATION

Create strongly typed configuration.

APPLICATION:

• Environment
• Service
• Version
• Region
• Host
• Port

DATABASE:

• URL
• Pool limits
• TLS
• Query timeout

REDIS:

• Host
• Port
• TLS
• Authentication

KAFKA:

• Brokers
• Client ID
• TLS
• Authentication
• Consumer groups

BULLMQ:

• Redis connection
• Concurrency defaults
• Retry defaults

S3:

• Region
• Bucket
• Endpoint when required

SEARCH:

• Endpoint
• Authentication
• Index prefix

MEDIA:

• Upload limits
• Processing profile
• Supported media types

AUTH:

• Token configuration
• Session configuration

OBSERVABILITY:

• Log level
• OTEL endpoint
• Metrics configuration

All configuration must be validated at startup.

Never call process.env directly inside domain services.

────────────────────────────────────────

REQUEST CONTEXT

Propagate:

• Request ID
• Correlation ID
• Trace ID
• User ID
• Session ID
• Device ID
• Platform
• App version
• Region
• Service
• Environment

Across:

• HTTP
• Kafka
• BullMQ
• WebSockets
• External provider calls
• Logs
• Metrics
• Traces

────────────────────────────────────────

LOGGING

Use structured logging.

Fields:

• Timestamp
• Level
• Service
• Environment
• Region
• Request ID
• Correlation ID
• Trace ID
• Operation
• Duration
• Result
• Safe error code

Never log:

• Passwords
• Access tokens
• Refresh tokens
• Private message content
• Signed media URLs
• Sensitive behavioral profiles
• Moderation evidence unnecessarily
• Advertising secrets

────────────────────────────────────────

ERROR MODEL

Define normalized errors:

• ValidationError
• AuthenticationError
• AuthorizationError
• NotFoundError
• ConflictError
• RateLimitError
• IdempotencyConflictError
• DependencyUnavailableError
• ProviderTimeoutError
• ProcessingError
• PrivacyError
• ModerationError
• RightsError
• InternalError

Public response:

• Error code
• Safe message
• Request ID
• Correlation ID
• Validation details where appropriate

Never expose stack traces in production.

────────────────────────────────────────

VALIDATION

Validate:

• IDs
• Usernames
• Visibility
• Content state
• Profile data
• Follow targets
• Social relationships
• Device data
• Pagination
• Cursor
• Idempotency keys
• Upload metadata
• Media metadata

Reject malformed identifiers and unsupported values.

────────────────────────────────────────

AUTHENTICATION FOUNDATION

Prepare:

• Registration
• Login
• Logout
• Session restoration
• Token refresh
• Password reset
• Password change
• Email verification
• Device registration

Authentication implementation must support future:

• OAuth
• MFA
• Passkeys

Never store plaintext passwords.

Use established password-hashing practices.

────────────────────────────────────────

AUTHORIZATION FOUNDATION

Implement:

• Authentication guards
• Role guards where relevant
• Resource ownership
• User-level authorization
• Creator authorization
• Business authorization
• Admin authorization

Authorization must evaluate server-side resource state.

────────────────────────────────────────

ACCOUNT DOMAIN

Implement:

• Account
• Account state
• Account security settings
• Session references

States:

• Pending
• Active
• Restricted
• Suspended
• Deactivated
• Deletion Requested
• Deleted

Define valid transitions.

────────────────────────────────────────

ACCOUNT STATE EFFECTS

Account state affects:

• Login
• Content creation
• Content visibility
• Messaging
• Follows
• Notifications
• Search
• Feed
• Advertising
• Analytics

────────────────────────────────────────

PROFILE DOMAIN

Implement:

• Username
• Display name
• Bio
• Avatar reference
• Links
• Profile visibility
• Category
• Public profile metadata

Separate:

• Authentication/account data
• Public profile data
• Private account metadata

────────────────────────────────────────

USERNAME SYSTEM

Support:

• Normalization
• Uniqueness
• Reserved names
• Rename rules
• Previous-name references
• Impersonation protection

Do not use username as the only identity key internally.

────────────────────────────────────────

PROFILE VISIBILITY

Support:

• Public
• Private

Private-account state must affect:

• Follow requests
• Content visibility
• Search
• Mentions
• Messaging
• Feed
• Explore

────────────────────────────────────────

CREATOR DOMAIN

Implement creator-profile foundation.

Support:

• Creator status
• Creator category
• Verification reference
• Professional profile
• Creator permissions
• Analytics eligibility

Keep creator metadata separate from normal authentication data.

────────────────────────────────────────

BUSINESS PROFILE FOUNDATION

Support:

• Business profile
• Business category
• Verification foundation
• Business administrators
• Business permissions

Business authorization must be scoped to the business entity.

────────────────────────────────────────

DEVICE DOMAIN

Implement:

• Device ID
• Platform
• App version
• Push-token reference
• Last active
• Security state

Do not treat device ID as sufficient authentication.

────────────────────────────────────────

SESSION DOMAIN

Support:

• Session creation
• Session rotation
• Session expiration
• Session revocation
• Device association

Prepare security events for:

• New login
• Password change
• Session revoke
• Suspicious login

────────────────────────────────────────

SOCIAL GRAPH

Implement the core relationship domain.

Support:

• Follow
• Unfollow
• Follow request
• Accept request
• Reject request
• Remove follower
• Block
• Unblock
• Restrict
• Close friends

────────────────────────────────────────

FOLLOW MODEL

Represent:

• Follower
• Followed
• State
• Created time
• Updated time
• Version

Prevent duplicate relationships.

────────────────────────────────────────

FOLLOW REQUESTS

States:

• Pending
• Accepted
• Rejected
• Canceled
• Expired where supported

Handle:

• Private → public
• Accept + block race
• Reject + cancel race
• Request + block
• Duplicate request

────────────────────────────────────────

BLOCKING

Implement blocking as authoritative graph state.

A block may affect:

• Follow
• Messaging
• Comments
• Mentions
• Notifications
• Search
• Feed
• Explore
• Stories
• Reels

Publish propagation events.

────────────────────────────────────────

RESTRICTION

Implement separate restriction state.

Possible scopes:

• Comments
• Messages
• Mentions
• Interaction visibility

Restriction must not be treated as block.

────────────────────────────────────────

CLOSE FRIENDS

Implement:

• Add member
• Remove member
• List members where owner-authorized

Close friends membership is private.

Prepare integration with stories.

────────────────────────────────────────

SOCIAL GRAPH AUTHORIZATION

Before displaying or modifying relationships evaluate:

• Account state
• Block
• Restriction
• Private/public status
• Target permissions

Never rely on client-side filtering.

────────────────────────────────────────

DATABASE FOUNDATION

Implement PostgreSQL/Prisma infrastructure.

Support:

• Transactions
• Connection pool
• Health checks
• Migration structure
• Error mapping
• Transaction helpers

────────────────────────────────────────

PRISMA CONVENTIONS

Define conventions for:

• Internal IDs
• Public IDs
• Timestamps
• Version fields
• Soft deletion where justified
• Unique constraints
• Foreign keys
• Composite indexes

Do not force identical patterns onto every model when domain requirements differ.

────────────────────────────────────────

DATABASE MODELS

Implement foundational models for:

IDENTITY

• User
• Account
• Session
• Device

PROFILE

• Profile
• CreatorProfile
• BusinessProfile

SOCIAL

• Follow
• FollowRequest
• Block
• Restriction
• CloseFriend

SECURITY

• SecurityEvent
• SessionRevocation

Maintain appropriate relations and indexes.

────────────────────────────────────────

DATABASE INDEXING

Identity:

• Email
• Username
• Account state

Social:

• Follower
• Following
• Follow state
• Follow request state
• Block source/target
• Restriction source/target
• Close-friend membership

Use composite indexes for common authorization and relationship queries.

────────────────────────────────────────

CURSOR PAGINATION

Implement reusable cursor pagination for:

• Followers
• Following
• Follow requests
• Blocks
• Restrictions
• Close friends where appropriate

Cursors must be opaque.

────────────────────────────────────────

REDIS FOUNDATION

Implement reusable Redis infrastructure.

Support:

• Connection lifecycle
• TLS
• Authentication
• Health checks
• Namespaces
• TTL
• Serialization
• Cache abstraction
• Rate limiting
• Session acceleration
• Idempotency
• Social-graph caching

────────────────────────────────────────

REDIS KEY NAMESPACES

Use namespaces such as:

• account:
• session:
• profile:
• creator:
• business:
• social:
• follow:
• block:
• restriction:
• close-friend:
• rate-limit:
• idempotency:

Keys should include:

• Environment
• Region where relevant
• Entity ID
• Version where applicable

────────────────────────────────────────

REDIS AUTHORITY

Redis may provide:

• Cache
• Ephemeral state
• Rate limiting
• Idempotency
• Short-lived session acceleration

Redis must never be authoritative for:

• User
• Account
• Profile
• Follow
• Block
• Restriction
• Creator
• Business ownership

────────────────────────────────────────

KAFKA / REDPANDA FOUNDATION

Implement:

• Producer
• Consumer
• Event envelope
• Serialization
• Validation
• Consumer groups
• Retry
• Dead-letter handling
• Graceful shutdown

Event envelope:

• Event ID
• Event type
• Version
• Aggregate type
• Aggregate ID
• Region
• Timestamp
• Producer
• Correlation ID
• Causation ID where appropriate
• Payload

────────────────────────────────────────

TRANSACTIONAL OUTBOX

Implement shared outbox infrastructure.

Fields:

• Outbox ID
• Event type
• Version
• Aggregate type
• Aggregate ID
• Payload
• Region
• Status
• Retry count
• Next retry
• Published time
• Error
• Created time

Ensure domain transaction and event creation are atomic.

────────────────────────────────────────

BULLMQ

Implement reusable queue infrastructure.

Support:

• Job schema
• Producer
• Worker
• Job ID
• Retry
• Backoff
• Timeout
• Concurrency
• Dead-letter
• Graceful shutdown
• Metrics

Prepare queues for:

• Media
• Search
• Feed
• Notifications
• Moderation
• Rights
• Analytics
• Privacy
• Cleanup
• Reconciliation

────────────────────────────────────────

WEBSOCKET FOUNDATION

Implement:

• Authentication
• Authorization
• Heartbeats
• Connection lifecycle
• Reconnection
• Rate limiting
• Room management
• Backpressure

Prepare channels for:

• Messaging
• Notifications
• Story/reel live updates where appropriate
• Moderation status where appropriate

Horizontal scaling must support Redis coordination.

────────────────────────────────────────

S3 STORAGE ABSTRACTION

Create a provider-neutral storage interface.

Support:

• Create upload authorization
• Put object reference
• Head object
• Delete object
• Generate temporary access
• Multipart upload foundation

Do not expose AWS credentials.

────────────────────────────────────────

MEDIA FOUNDATION

Create media-domain abstractions for:

• Media asset
• Media type
• Owner
• Original object
• Processing state
• Moderation state
• Rights state
• Version

Support:

• Image
• Video

────────────────────────────────────────

MEDIA UPLOAD AUTHORIZATION

Support:

• Signed upload
• Size limit
• MIME declaration
• Object-key namespace
• Owner binding
• Expiration

Actual media bytes should be uploaded directly to object storage where supported.

────────────────────────────────────────

MEDIA SECURITY

Validate server-side:

• File size
• Content signature
• MIME
• Container
• Metadata
• Owner
• Object location

Prepare integration with malware/safety scanning.

────────────────────────────────────────

MEDIA PROCESSING STATES

Define common states:

• Uploading
• Uploaded
• Validating
• Processing
• Moderating
• Ready
• Failed
• Deleted

Use version/revision semantics to prevent stale jobs from overwriting newer state.

────────────────────────────────────────

API FOUNDATION

Implement common API conventions:

• REST
• Versioning
• DTO validation
• Authentication
• Authorization
• Cursor pagination
• Error normalization
• Request ID
• Correlation ID
• Idempotency
• OpenAPI

────────────────────────────────────────

IDENTITY API

Prepare endpoints for:

• Register
• Login
• Logout
• Refresh
• Verify email
• Password reset
• Password change
• Session list
• Session revoke

────────────────────────────────────────

PROFILE API

Support:

• Get own profile
• Get public profile
• Update own profile
• Change username
• Change visibility

Verify authorization server-side.

────────────────────────────────────────

SOCIAL GRAPH API

Support:

• Follow
• Unfollow
• Request follow
• Accept request
• Reject request
• Remove follower
• Block
• Unblock
• Restrict
• Unrestrict
• Add close friend
• Remove close friend
• List followers
• List following
• List requests

────────────────────────────────────────

SOCIAL GRAPH IDEMPOTENCY

Use safe semantics for:

• Follow
• Unfollow
• Block
• Unblock
• Restrict
• Unrestrict

Prevent duplicate side effects under retries.

────────────────────────────────────────

FOLLOW / BLOCK INTERACTION

Blocking must immediately affect effective relationship state.

Examples:

• Existing follow → inaccessible/removed according to policy
• Pending request → invalidated
• Messaging → blocked
• Mentions → restricted
• Search → filtered

Define deterministic rules.

────────────────────────────────────────

ACCOUNT DELETION FOUNDATION

Prepare asynchronous deletion hooks for:

• Profile
• Social graph
• Content
• Media
• Messaging
• Notifications
• Search
• Recommendations
• Analytics

Actual full deletion belongs to later privacy implementation.

────────────────────────────────────────

PRIVACY FOUNDATION

Create interfaces for:

• Data access
• Data export
• Data deletion
• Retention
• Consent
• Personalization controls
• Advertising controls

Do not implement the complete privacy workflow in this milestone.

────────────────────────────────────────

EVENT CATALOG

Publish:

IDENTITY

• UserCreated
• UserLoggedIn
• SessionCreated
• SessionRevoked
• DeviceRegistered

PROFILE

• ProfileCreated
• ProfileUpdated
• UsernameChanged
• ProfileVisibilityChanged

SOCIAL

• FollowCreated
• FollowRemoved
• FollowRequestCreated
• FollowRequestAccepted
• FollowRequestRejected
• FollowerRemoved
• BlockCreated
• BlockRemoved
• RestrictionCreated
• RestrictionRemoved
• CloseFriendAdded
• CloseFriendRemoved

MEDIA

• MediaUploadAuthorized
• MediaUploaded
• MediaProcessingRequested

ACCOUNT

• AccountSuspended
• AccountReactivated
• AccountDeletionRequested

Every event must:

• Be versioned
• Be idempotent
• Include correlation metadata
• Minimize sensitive information

────────────────────────────────────────

AUTHORIZATION EVENTS

Do not expose private authorization details unnecessarily.

Consumers should receive only what they require.

────────────────────────────────────────

OBSERVABILITY

Instrument:

• Authentication
• Authorization
• Profile updates
• Social graph operations
• Media upload authorization
• Redis
• Kafka
• BullMQ
• WebSockets
• S3
• PostgreSQL

Track:

• Request latency
• Error rate
• Follow latency
• Block latency
• Login latency
• Session refresh
• Queue depth
• Kafka lag
• Redis latency
• WebSocket connections

Never log private content or sensitive credentials.

────────────────────────────────────────

HEALTH CHECKS

Provide:

• Liveness
• Readiness
• Startup

Health checks for:

• PostgreSQL
• Redis
• Kafka
• BullMQ
• S3

Liveness must not fail just because an optional external provider is unavailable.

────────────────────────────────────────

GRACEFUL SHUTDOWN

Gracefully close:

• HTTP
• WebSockets
• Kafka producers
• Kafka consumers
• BullMQ workers
• Redis
• Prisma

Stop accepting new work before terminating dependencies.

────────────────────────────────────────

SECURITY

Harden:

• Authentication
• Session handling
• Password reset
• Authorization
• IDOR
• Rate limiting
• Input validation
• Upload authorization
• WebSocket authentication
• Admin boundaries
• Private-profile access

────────────────────────────────────────

RATE LIMITING

Prepare rate limits for:

• Login
• Registration
• Password reset
• Follow
• Unfollow
• Block
• Search
• Upload initialization
• WebSocket connection
• API requests

Support:

• User
• IP
• Device
• Endpoint

Do not rely solely on IP.

────────────────────────────────────────

TESTING FOUNDATION

Implement utilities for:

• Unit tests
• Integration tests
• API tests
• Database fixtures
• Redis fixtures
• Kafka fixtures
• BullMQ fixtures
• WebSocket fixtures
• Authentication helpers
• Authorization helpers

Create deterministic factories for:

• User
• Account
• Profile
• Creator
• Business
• Device
• Follow
• FollowRequest
• Block
• Restriction
• CloseFriend
• MediaAsset

────────────────────────────────────────

TEST CASES

IDENTITY

• Registration
• Login
• Logout
• Refresh
• Password reset
• Session revoke
• Account suspension

PROFILES

• Update
• Username collision
• Visibility
• Authorization

SOCIAL GRAPH

• Follow
• Unfollow
• Request
• Accept
• Reject
• Remove follower
• Block
• Unblock
• Restrict
• Unrestrict
• Close friends

CONCURRENCY:

• Duplicate follow
• Follow/unfollow race
• Block/follow race
• Accept/block race
• Concurrent username changes

SECURITY:

• IDOR
• Cross-user access
• Cross-business access
• Private profile leakage
• Session replay
• Rate-limit bypass

────────────────────────────────────────

LOCAL DEVELOPMENT

Prepare Docker-compatible local dependencies:

• PostgreSQL
• Redis
• Kafka/Redpanda
• OpenSearch foundation
• MinIO/S3-compatible storage

Use local-only credentials.

────────────────────────────────────────

DOCUMENTATION

Generate:

• Backend architecture
• Monorepo structure
• Configuration
• Request context
• Logging
• Errors
• Validation
• Authentication
• Authorization
• Accounts
• Profiles
• Creators
• Businesses
• Devices
• Sessions
• Social graph
• Follow requests
• Blocking
• Restrictions
• Close friends
• PostgreSQL
• Prisma
• Redis
• Kafka
• Transactional Outbox
• BullMQ
• WebSockets
• S3 abstraction
• Media foundation
• Upload authorization
• Security
• Privacy foundation
• Observability
• Testing
• Local development

────────────────────────────────────────

PROJECT INDEX

Update the backend Project Index with:

• Applications
• Services
• Workers
• Shared packages
• Configuration
• Identity
• Accounts
• Profiles
• Creators
• Businesses
• Devices
• Sessions
• Social graph
• Follows
• Follow requests
• Blocks
• Restrictions
• Close friends
• PostgreSQL
• Prisma
• Redis
• Kafka
• BullMQ
• WebSockets
• S3
• Media foundation
• APIs
• Events
• Queues
• Redis keys
• Security
• Privacy
• Observability
• Tests
• Generated files
• Modified files
• Remaining work
• Current milestone
• Dependencies

────────────────────────────────────────

IMPLEMENTATION MILESTONES

BACKEND MILESTONE 1

NestJS bootstrap, configuration, request context, logging, errors, validation, API versioning, OpenAPI, health checks, graceful shutdown, security foundation, and test foundation.

BACKEND MILESTONE 2

Identity, accounts, sessions, authentication, password reset, email verification, devices, security events, authorization, and account lifecycle.

BACKEND MILESTONE 3

Profiles, usernames, public/private visibility, creator-profile foundation, business-profile foundation, profile authorization, and profile caching.

BACKEND MILESTONE 4

Social graph, follows, follow requests, blocking, restrictions, close friends, relationship APIs, concurrency controls, and event propagation.

BACKEND MILESTONE 5

PostgreSQL/Prisma hardening, Redis foundation, Kafka/Redpanda, Transactional Outbox, BullMQ, WebSockets, Socket.IO, S3 abstraction, and reusable infrastructure packages.

BACKEND MILESTONE 6

Media asset foundation, upload authorization, object ownership, media states, storage integration, security validation, and processing-event contracts.

BACKEND MILESTONE 7

Cross-domain authorization, rate limiting, privacy foundations, deletion hooks, audit hooks, security hardening, and observability.

BACKEND MILESTONE 8

Integration testing, concurrency testing, security testing, event testing, queue testing, WebSocket testing, and failure handling.

BACKEND MILESTONE 9

Performance hardening, database/index review, Redis review, Kafka review, API optimization, caching, fault isolation, and production diagnostics.

BACKEND MILESTONE 10

Full foundation integration, regression testing, documentation, Project Index completion, dependency validation, and production-readiness review before implementing higher-level content domains.

Each milestone should contain approximately 20–40 files where practical.

Every milestone must compile before proceeding.

────────────────────────────────────────

OUTPUT FORMAT

For every generated file provide:

1. Exact file path
2. Complete file contents

Never truncate code.

Never summarize source code instead of generating it.

Never generate pseudo-code.

Never generate placeholders.

Never generate TODO implementations.

When modifying an existing file:

1. Provide the exact file path.
2. State why it must change.
3. Provide the complete updated file.

Never regenerate unchanged files.

────────────────────────────────────────

SCOPE RESTRICTION

This volume covers the backend foundation for:

• Identity
• Accounts
• Profiles
• Creators
• Businesses
• Devices
• Sessions
• Social graph
• Follows
• Follow requests
• Blocking
• Restrictions
• Close friends
• PostgreSQL
• Prisma
• Redis
• Kafka
• Transactional Outbox
• BullMQ
• WebSockets
• Socket.IO
• S3 abstraction
• Media foundation
• Upload authorization
• Security
• Privacy foundations
• Observability
• Testing foundation
• Local development

Do not implement the full business logic for:

• Posts
• Stories
• Reels
• Feed
• Recommendations
• Explore
• Trending
• Search
• Messaging
• Notifications
• Moderation
• Rights
• Advertising
• Commerce
• Analytics
• Administration
• Privacy export/deletion

Those belong to later backend implementation volumes.

────────────────────────────────────────

QUALITY BAR

Treat identity, authorization, social graph, privacy foundations, and infrastructure primitives as mission-critical.

Assume:

• Hundreds of millions of users
• Millions of creators
• Massive follow graphs
• High authentication traffic
• High social-graph traffic
• Large media uploads
• Multiple regions
• High availability
• Strict privacy
• Strict security

Prioritize:

• Correct authorization
• Relationship integrity
• Idempotency
• Concurrency safety
• Low latency
• Data ownership
• Horizontal scalability
• Observability
• Fault isolation
• Privacy
• Security
• Maintainability
• Production readiness
