# PROJECT 1 — INSTAGRAM-LIKE GLOBAL SOCIAL PLATFORM

# BACKEND PROMPT — VOLUME 1

# IDENTITY, AUTHENTICATION, USERS, PROFILES, SOCIAL GRAPH & SECURITY

You are the Staff Backend Engineering team responsible for implementing the backend of a production-grade Instagram-like global social platform.

This prompt is fully standalone. It does not depend on any other prompt, document, previous conversation, previous implementation, architecture volume, approval, or hidden context.

You must inspect the current repository before making changes and integrate with existing compatible code. Repository state is the source of truth for existing implementation.

Implement real production functionality.

Do not generate pseudo-code.

Do not create placeholders.

Do not use TODO/FIXME stubs instead of implementation.

Do not fabricate completed functionality.

Do not regenerate unchanged files.

Preserve working behavior unless a change is required by this implementation.

==================================================

1. PROJECT IDENTITY
   ==================================================

Build the backend foundation for a global social platform supporting:

- user registration
- authentication
- account verification
- sessions
- device management
- profiles
- username management
- privacy settings
- follow relationships
- follow requests
- blocking
- muting
- restricting
- account states
- security auditing
- rate limiting
- authorization

The backend must be production-grade, secure, observable, testable, and horizontally scalable.

==================================================
2. TECHNOLOGY STACK
===================

Use:

- Node.js
- NestJS
- TypeScript
- PostgreSQL
- Prisma ORM
- Redis
- Kafka or Redpanda
- BullMQ
- OpenSearch/Elasticsearch where integration is relevant
- Socket.IO/WebSockets where integration is relevant
- AWS S3 where integration is relevant
- OpenTelemetry
- Prometheus
- Grafana
- Loki
- Tempo

Use modern TypeScript with strict typing.

==================================================
3. BACKEND ARCHITECTURE
=======================

Use a modular NestJS architecture with clear domain boundaries.

At minimum establish modules for:

- identity
- authentication
- users
- profiles
- social graph
- privacy
- sessions/devices
- security/audit
- notifications integration
- event publishing
- infrastructure

Use separation between:

- controllers
- application services
- domain logic
- repositories
- persistence
- infrastructure adapters

Do not place substantial business logic inside controllers.

==================================================
4. DATABASE FOUNDATION
======================

Use PostgreSQL with Prisma.

Create production-ready data models for:

- User
- Credential
- Session
- Device
- Profile
- PrivacySettings
- Follow
- FollowRequest
- Block
- Mute
- Restriction
- AuditRecord
- VerificationToken
- PasswordResetToken

Use:

- primary keys
- foreign keys where appropriate
- unique constraints
- composite indexes
- timestamps
- appropriate nullable semantics
- explicit enum modeling

Avoid storing derived counters as authoritative facts unless there is a deliberate consistency strategy.

==================================================
5. USER MODEL
=============

The User entity must represent account identity independently from public profile information.

Support:

- immutable internal user identifier
- account status
- verification state
- created timestamp
- updated timestamp
- deleted timestamp where soft deletion applies

Account states should include at least:

- pending
- active
- restricted
- suspended
- disabled
- deleted

Do not expose internal database implementation details through public APIs.

==================================================
6. USERNAME SYSTEM
==================

Implement globally unique usernames.

Requirements:

- normalize usernames consistently
- enforce uniqueness at database level
- prevent race-condition duplicates
- validate allowed characters
- validate length
- reject reserved names
- handle case normalization consistently

Do not rely solely on application-level uniqueness checks.

The database must enforce the invariant.

==================================================
7. REGISTRATION
===============

Implement secure account registration.

The flow must:

1. validate input
2. normalize appropriate fields
3. detect conflicts
4. securely hash the password
5. create account and profile data transactionally
6. create verification state
7. create security/audit event
8. publish appropriate asynchronous event after persistence
9. return a safe response

Do not leak whether sensitive account information exists where enumeration prevention is required.

==================================================
8. PASSWORD SECURITY
====================

Use a modern adaptive password hashing algorithm supported by the chosen secure library.

Never store plaintext passwords.

Never log passwords.

Password validation must include:

- minimum length
- maximum safe length
- Unicode considerations
- common-password protections where appropriate
- credential reuse considerations if supported

Password comparison must be timing-safe through the selected password library.

==================================================
9. LOGIN
========

Implement secure login.

Validate:

- account state
- credentials
- verification/security conditions
- rate limits
- suspicious login controls

On successful authentication:

- create or rotate session state
- issue access token
- issue refresh token
- register device metadata
- record security event

Do not expose sensitive account state through distinguishable error responses when doing so would enable enumeration.

==================================================
10. TOKEN ARCHITECTURE
======================

Use short-lived access tokens and protected refresh tokens.

Define:

- token lifetime
- issuer
- audience
- signing configuration
- token claims
- refresh strategy
- revocation strategy

Do not place unnecessary personal information into tokens.

Access tokens should contain only claims required by the authorization system.

Refresh tokens must support revocation and replay protection.

Never store raw long-lived refresh tokens where hashing/token-family storage provides stronger protection.

==================================================
11. REFRESH TOKEN ROTATION
==========================

Implement secure refresh behavior.

A refresh request must:

1. validate the presented refresh token
2. verify session state
3. detect replay/reuse conditions
4. rotate the refresh credential
5. invalidate the previous refresh credential
6. issue a new access token
7. issue replacement refresh credential
8. update session metadata

If a refresh-token reuse attack is detected, invalidate the affected session/token family according to the security model.

==================================================
12. LOGOUT
==========

Support:

- logout current session
- logout selected session
- logout all sessions

Revocation must be server-side.

Do not merely delete client-side tokens and consider the session terminated.

Where required:

- invalidate refresh credentials
- revoke session state
- propagate security events
- clear relevant caches

==================================================
13. SESSION MANAGEMENT
======================

Sessions must contain appropriate metadata such as:

- session ID
- user ID
- device ID
- creation time
- last-used time
- expiration
- revocation state
- security metadata

Do not store unnecessary sensitive device data.

Implement APIs allowing users to inspect and revoke active sessions.

==================================================
14. DEVICE MANAGEMENT
=====================

Support registered devices for:

- mobile applications
- web sessions where appropriate
- push notification integration

Track:

- device ID
- platform
- app version where useful
- push token reference where applicable
- last active time
- status

Avoid treating device metadata as a trusted security identity by itself.

==================================================
15. EMAIL VERIFICATION
======================

Implement account verification architecture.

Support:

- verification token generation
- expiration
- one-time usage
- secure token storage
- verification completion
- resend controls
- rate limiting

Verification tokens must not be reusable.

Do not expose raw verification tokens in database logs.

==================================================
16. PASSWORD RESET
==================

Implement secure password-reset workflow.

Support:

- request reset
- generic response to reduce enumeration
- short-lived reset credential
- one-time use
- password replacement
- session revocation after successful reset

A successful password reset should invalidate active authentication sessions where appropriate.

==================================================
17. PROFILE MODEL
=================

Implement profile functionality for:

- display name
- biography
- avatar reference
- website
- public metadata
- creator metadata where supported
- profile visibility

Profile and credential information must remain separated conceptually.

A public profile response must never accidentally expose:

- password information
- session data
- private account metadata
- internal security fields

==================================================
18. PROFILE UPDATE
==================

Support secure profile updates.

Operations must:

- authenticate user
- authorize ownership
- validate fields
- enforce length limits
- sanitize supported rich/text data where necessary
- persist transactionally
- invalidate relevant cache
- emit profile update event

Username changes must enforce uniqueness and race safety.

==================================================
19. PRIVACY SETTINGS
====================

Implement account privacy state.

At minimum:

- public account
- private account

Privacy configuration must be server-authoritative.

Do not allow clients to bypass privacy rules by calling another endpoint.

Privacy must be evaluated consistently across future:

- posts
- stories
- reels
- search
- followers
- messaging
- notifications
- recommendations

==================================================
20. FOLLOW RELATIONSHIP
=======================

Implement Follow as a durable relationship.

For public accounts:

authenticated user
→ validate target
→ validate block/restriction rules
→ create relationship
→ emit event

For private accounts:

authenticated user
→ validate target
→ create pending request
→ owner receives notification/event
→ owner accepts
→ relationship becomes active

Enforce uniqueness at database level.

==================================================
21. FOLLOW REQUESTS
===================

Implement:

- create request
- cancel request
- approve request
- reject request

Handle:

- duplicate requests
- already-following state
- blocked users
- privacy changes
- target account deletion
- requester account deletion

Do not permit authorization races to create unauthorized relationships.

==================================================
22. SOCIAL GRAPH QUERIES
========================

Implement paginated queries for:

- followers
- following
- pending requests
- relationship state

Use cursor pagination for potentially large collections.

Never allow unrestricted page sizes.

Design indexes for:

- user → followers
- user → following
- relationship existence
- pending requests

==================================================
23. BLOCKING
============

Implement durable blocking.

A block must be enforceable across current and future domains.

When A blocks B:

- B must be prevented from unauthorized interaction with A
- protected content must remain inaccessible
- follow relationships must be handled according to product rules
- pending requests must be invalidated as required
- messaging authorization must reject prohibited access
- feed/search integration must be informed through events

The block relation must be checked server-side.

==================================================
24. MUTING
==========

Implement user-level muting.

Mute must be distinct from block.

A muted user may remain socially connected while their content is suppressed from applicable surfaces.

The relationship should be represented as durable user-specific state.

Emit appropriate events when mute state changes if downstream feed/recommendation systems depend on it.

==================================================
25. RESTRICTING
===============

Implement restriction as a distinct privacy/social state.

Restriction must not be treated as a synonym for blocking.

Define behavior for future domains including:

- comments
- messaging
- notifications
- activity visibility

Do not allow frontend-only restriction enforcement.

==================================================
26. AUTHORIZATION LAYER
=======================

Implement reusable authorization mechanisms.

Authorization must evaluate:

- authenticated principal
- target resource
- ownership
- account status
- social relationship
- privacy state
- block state
- restriction state

Controllers must not implement authorization by trusting request body fields.

==================================================
27. REQUEST VALIDATION
======================

All externally supplied input must be validated.

Validate:

- body
- path parameters
- query parameters
- headers where relevant

Reject malformed input before business logic executes.

Set bounded limits on:

- strings
- arrays
- pagination
- request payloads

==================================================
28. RATE LIMITING
=================

Implement distributed Redis-backed rate limiting for sensitive operations.

At minimum protect:

- registration
- login
- password reset
- verification resend
- follow
- follow request
- profile updates
- username changes

Rate limits should consider:

- user
- IP
- endpoint
- device where appropriate

Avoid using only IP address as the security boundary.

==================================================
29. REDIS USAGE
===============

Use Redis for:

- rate limiting
- session lookup acceleration where appropriate
- temporary security state
- cache
- idempotency support where appropriate

Do not use Redis as the sole durable source of truth for:

- users
- credentials
- follows
- blocks
- privacy settings

Every cache must have:

- purpose
- TTL
- invalidation behavior

==================================================
30. EVENT ARCHITECTURE
======================

Use Kafka or Redpanda for asynchronous domain event propagation.

Events to support include:

- UserRegistered
- UserVerified
- PasswordChanged
- SessionCreated
- SessionRevoked
- ProfileUpdated
- FollowCreated
- FollowRemoved
- FollowRequestCreated
- FollowRequestApproved
- FollowRequestRejected
- UserBlocked
- UserUnblocked
- UserMuted
- UserUnmuted
- UserRestricted
- UserUnrestricted

Each event must have:

- event ID
- event type
- version
- aggregate ID
- timestamp
- producer
- correlation ID
- payload

Do not put unnecessary secrets or sensitive credentials into events.

==================================================
31. OUTBOX RELIABILITY
======================

Avoid unsafe database/event dual writes.

For important domain events:

database transaction
→ durable state + outbox record
→ asynchronous publisher
→ Kafka/Redpanda

Events must not depend on an HTTP request remaining alive after the database transaction finishes.

Consumers must be idempotent.

==================================================
32. BULLMQ
==========

Use BullMQ for appropriate asynchronous jobs such as:

- verification email delivery
- password-reset communication
- cache cleanup
- stale session cleanup
- security notifications
- relationship-maintenance work

Jobs must specify:

- retries
- exponential backoff where appropriate
- timeout
- concurrency
- idempotency
- failure handling

Do not retry permanently invalid jobs indefinitely.

==================================================
33. NOTIFICATION INTEGRATION
============================

Do not tightly couple authentication/profile transactions to notification-provider delivery.

For example:

FollowCreated
→ event
→ notification policy
→ notification subsystem

Identity/profile modules should only produce authoritative events and contracts.

==================================================
34. SEARCH INTEGRATION
======================

Profile updates should emit events that can later update OpenSearch/Elasticsearch.

Search indexing is derived state.

The PostgreSQL profile remains authoritative.

Search failures must not prevent profile updates.

==================================================
35. AUDIT LOGGING
=================

Create audit records for security-sensitive operations such as:

- login
- logout
- failed authentication where useful
- password change
- password reset
- email verification
- username change
- privacy change
- session revocation
- account status changes
- administrative actions

Do not log plaintext credentials or sensitive secrets.

==================================================
36. SECURITY EVENTS
===================

Support security telemetry for:

- suspicious login
- repeated failed login
- refresh-token reuse
- session revocation
- password reset
- unusual authentication patterns

Security events must be observable without exposing sensitive user data unnecessarily.

==================================================
37. ACCOUNT SUSPENSION
======================

The backend must enforce suspended/disabled accounts.

A suspended account must not continue authenticating normally.

Existing sessions must be revocable.

Sensitive account-state transitions must be auditable.

Do not rely on clients to detect account suspension.

==================================================
38. SOFT DELETION
=================

Where soft deletion is used:

- mark account deleted
- immediately prevent normal authentication
- invalidate sessions
- stop new interactions
- hide profile from applicable user-facing APIs
- emit deletion event
- initiate asynchronous cleanup

Cleanup must include future derived systems such as search/cache/event consumers where applicable.

==================================================
39. API STRUCTURE
=================

Use versioned API routing such as:

/api/v1/auth
/api/v1/users
/api/v1/profiles
/api/v1/social

Do not unnecessarily expose database-oriented routes.

Resources should reflect domain concepts.

==================================================
40. RESPONSE CONTRACTS
======================

Use stable response DTOs.

Never return Prisma models directly from controllers.

Map internal entities to externally controlled DTOs.

This prevents accidental leakage of:

- internal IDs
- security fields
- internal metadata
- database implementation details

==================================================
41. ERROR HANDLING
==================

Create consistent application error classes and HTTP mappings.

Support:

- validation errors
- authentication errors
- authorization errors
- not found
- conflict
- rate limiting
- dependency failures
- internal errors

Do not return raw exceptions.

Do not expose stack traces.

Include correlation/request identifiers where appropriate.

==================================================
42. DATABASE MIGRATIONS
=======================

All schema modifications must use Prisma migrations.

Migrations must:

- be deterministic
- be reviewable
- avoid destructive operations when unnecessary
- support safe rollout

Do not manipulate production schema manually through application startup.

==================================================
43. TRANSACTION RULES
=====================

Use database transactions when multiple writes must preserve a business invariant.

Do not keep transactions open while performing:

- network calls
- Kafka publication
- email sending
- external API calls
- expensive processing

Persist authoritative state first and trigger asynchronous work afterward.

==================================================
44. CONCURRENCY CONTROL
=======================

Handle concurrent requests for:

- username registration
- username changes
- follow creation
- block creation
- session refresh
- password reset
- privacy changes

Use:

- unique database constraints
- transactions
- optimistic concurrency
- atomic operations
- appropriate locks

Do not rely on application checks alone.

==================================================
45. OBSERVABILITY
=================

Instrument the backend with OpenTelemetry.

Trace:

- HTTP requests
- PostgreSQL
- Prisma
- Redis
- Kafka/Redpanda
- BullMQ
- important authentication workflows

Emit metrics for:

- login success/failure
- registration
- token refresh
- rate-limit rejection
- follow operations
- block operations
- request latency
- database latency
- queue latency
- errors

Use structured logging.

==================================================
46. HEALTH ENDPOINTS
====================

Provide:

- liveness endpoint
- readiness endpoint

Liveness should indicate whether the process is alive.

Readiness should indicate whether the service can safely receive traffic.

Do not make liveness dependent on every external dependency.

==================================================
47. CONFIGURATION
=================

All sensitive or environment-specific values must come from configuration.

Examples:

- DATABASE_URL
- REDIS_URL
- KAFKA/REDPANDA configuration
- JWT signing configuration
- token expiration settings
- email provider configuration
- S3 configuration
- OpenTelemetry configuration

Never hard-code secrets.

Validate required configuration at startup.

==================================================
48. TESTING
===========

Implement automated tests for:

- registration
- duplicate username prevention
- login
- invalid credentials
- account-state restrictions
- refresh rotation
- refresh-token replay detection
- logout
- session revocation
- password reset
- verification
- profile updates
- username uniqueness
- private/public privacy
- follow
- follow request
- follow approval
- follow rejection
- block
- mute
- restriction
- authorization bypass attempts
- rate limiting

Test database constraints and race-sensitive behavior.

==================================================
49. SECURITY TESTING
====================

Include tests for:

- IDOR
- unauthorized profile modification
- unauthorized relationship modification
- token misuse
- refresh replay
- session revocation
- brute-force protection
- enumeration behavior
- malformed input
- privilege escalation
- blocked-user bypass
- private-account bypass

==================================================
50. API DOCUMENTATION
=====================

Generate and maintain OpenAPI/Swagger documentation.

Document:

- endpoints
- request schemas
- response schemas
- authentication
- errors
- pagination
- rate limits where practical

Documentation must represent actual implementation.

Do not document endpoints that do not exist.

==================================================
51. ACCEPTANCE CRITERIA
=======================

This implementation is complete only when:

- NestJS backend architecture is established
- PostgreSQL/Prisma schema is implemented
- migrations are functional
- registration works
- login works
- secure password storage works
- token lifecycle works
- refresh rotation works
- session management works
- logout/revocation works
- profile management works
- username uniqueness is enforced
- privacy state works
- follows work
- follow requests work
- blocking works
- muting works
- restricting works
- authorization is enforced
- Redis-backed rate limiting works
- domain events are reliably published
- asynchronous jobs work where required
- audit records exist
- observability exists
- health checks exist
- OpenAPI documentation is maintained
- automated tests cover critical behavior
- the code compiles and type-checks
- no placeholder implementation remains

==================================================
52. IMPLEMENTATION FINISHING RULE
=================================

Do not stop after creating database models or module skeletons.

Complete the actual backend behavior for the scope above.

Inspect the repository and integrate with any existing compatible infrastructure.

Only modify files required to implement the functionality.

Preserve working unrelated code.

At the end, validate:

- formatting
- linting
- TypeScript compilation
- Prisma validation
- migrations
- unit tests
- integration tests
- critical security tests

The result must be a real production-ready backend foundation for the platform.
