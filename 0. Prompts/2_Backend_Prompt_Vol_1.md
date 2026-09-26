
# Instagram — Backend Prompt — Volume 1

# 1. ROLE

You are the **Staff Backend Engineering team** responsible for implementing the foundational backend platform for the **Instagram** project.

Operate with the combined responsibilities of:

* Staff Backend Engineer
* Backend Architect
* Database Engineer
* Distributed Systems Engineer
* Security Engineer
* Reliability Engineer
* Performance Engineer
* DevOps-aware Application Engineer
* QA-minded Backend Engineer

This is a **bounded backend implementation assignment**.

You must implement the real backend functionality defined by this prompt.

Do not implement unrelated future product areas merely because they appear in the global Instagram product vision.

The mandatory rule for this task is:

**Implement only the current prompt's scope.**

---

# 2. PROJECT IDENTITY

**Project Name:** Instagram

**Product Type:** Production-grade visual social networking platform.

The backend is part of a larger system that includes:

* web client;
* mobile clients;
* relational persistence;
* Redis;
* asynchronous event processing;
* job queues;
* media processing;
* search;
* realtime messaging;
* notifications;
* moderation;
* administration;
* analytics;
* cloud infrastructure.

The completed system is intended to support approximately:

* 100 million registered accounts;
* 20 million daily active users;
* 2 million peak concurrent active sessions;
* approximately 100,000 sustained API requests per second across the platform;
* approximately 250,000 requests per second during peak edge bursts.

These are global architectural targets.

This prompt implements only the foundational backend scope defined below.

---

# 3. TECHNOLOGY BASELINE

Use the following technology direction unless an actual repository constraint requires a compatible alternative:

* TypeScript;
* Node.js;
* NestJS or an equivalent structured TypeScript backend framework;
* PostgreSQL;
* Redis;
* Prisma, TypeORM, Drizzle, or an existing repository-compatible ORM/data-access layer;
* REST APIs;
* structured validation;
* structured logging;
* OpenTelemetry-compatible tracing/metrics where practical;
* automated unit and integration testing.

Do not replace an existing sound repository technology stack without a concrete compatibility reason.

If the repository already contains a backend framework or ORM, inspect it first and preserve it unless a necessary correction falls within this prompt's scope.

---

# 4. CURRENT BACKEND ASSIGNMENT

Implement the backend foundation for these domains:

1. application/bootstrap foundation;
2. configuration;
3. database infrastructure;
4. shared API conventions;
5. error handling;
6. request correlation;
7. authentication;
8. sessions/devices;
9. account lifecycle;
10. profiles;
11. social relationships.

This prompt establishes the executable backend foundation required for later backend domains.

The implementation must be production-grade within this scope.

---

# 5. REPOSITORY INSPECTION

Before modifying or creating code, inspect the repository.

Inspect, where present:

* workspace/package structure;
* backend applications;
* shared packages;
* package manager and lockfile;
* TypeScript configuration;
* linting;
* formatting;
* test configuration;
* environment configuration;
* database schema;
* migrations;
* seed infrastructure;
* existing authentication code;
* existing controllers/routes;
* middleware;
* guards;
* interceptors;
* exception handling;
* Redis integration;
* logging;
* tracing;
* health checks;
* documentation;
* CI configuration.

Treat the repository as the source of truth for actual implementation state.

Do not assume another AI prompt was executed.

Do not assume any specific architecture file exists.

Do not fabricate repository state.

If compatible components already exist, reuse and extend them rather than duplicating equivalent systems.

---

# 6. BOUNDED IMPLEMENTATION SCOPE

## In Scope

Implement:

* backend application bootstrap;
* environment/configuration validation;
* application module organization;
* shared API infrastructure;
* request IDs/correlation IDs;
* structured error handling;
* authentication;
* credential security;
* account creation;
* account lifecycle;
* session management;
* device/session management;
* password recovery;
* verification architecture and implementation where provider-independent behavior can be implemented locally;
* profiles;
* usernames;
* public/private account state;
* follow relationships;
* follow requests for private accounts;
* block relationships;
* mute relationships;
* restrict relationships;
* relevant authorization guards/policies;
* PostgreSQL persistence;
* migrations;
* relevant Redis support;
* relevant events/outbox infrastructure for the implemented domains;
* unit tests;
* integration tests;
* API contract tests appropriate to this scope;
* documentation required for the implemented backend foundation.

## Out of Scope

Do not implement:

* posts;
* stories;
* reels/short-form video;
* media processing;
* feed ranking;
* discovery;
* search;
* comments;
* likes;
* saves;
* shares;
* direct messaging;
* notifications;
* moderation workflows;
* administration console functionality;
* analytics pipelines;
* full cloud infrastructure;
* Kubernetes deployment;
* CDN configuration;
* production object-storage processing pipelines.

Create extension points and contracts where necessary, but do not implement those future domains.

---

# 7. BACKEND ARCHITECTURE

Create a maintainable backend structure organized around domain ownership.

The implementation should separate concerns for:

* configuration;
* HTTP/API infrastructure;
* identity/authentication;
* sessions/devices;
* accounts/profiles;
* social graph;
* database access;
* cache;
* events;
* observability;
* health/diagnostics.

Avoid an unstructured "everything in controllers/services" design.

Do not create a microservice fleet merely to satisfy the target scale.

The codebase may be a modular monolith at this stage if that is the most operationally appropriate implementation, provided domain boundaries remain explicit and future extraction is feasible.

---

# 8. APPLICATION BOOTSTRAP

Implement a production-grade application bootstrap.

Include, as appropriate:

* process initialization;
* environment loading;
* configuration validation;
* dependency initialization;
* HTTP server setup;
* global validation;
* global error handling;
* request correlation;
* security headers;
* graceful shutdown;
* readiness handling;
* liveness handling.

Do not allow malformed configuration to produce a partially functioning application.

Startup must fail clearly when required configuration is missing or invalid.

---

# 9. CONFIGURATION

Implement typed configuration management.

Configuration must support:

* application settings;
* environment;
* HTTP settings;
* database;
* Redis;
* authentication;
* sessions;
* password hashing;
* rate limits relevant to this scope;
* email/verification integration boundary where applicable;
* observability.

Separate:

* non-secret configuration;
* secrets;
* runtime-generated state.

Validate configuration at startup.

Never log secret values.

Never commit real secrets.

Create a documented environment-variable contract.

---

# 10. API FOUNDATION

Implement the shared API foundation.

Define:

* API versioning convention;
* route naming;
* JSON serialization;
* content-type handling;
* request validation;
* response conventions;
* status-code conventions;
* request/correlation IDs;
* error format.

The implementation must use one consistent error model.

Error responses should support machine-readable error codes and safe human-readable messages.

Do not expose:

* stack traces;
* internal database errors;
* credentials;
* security-sensitive implementation details.

---

# 11. REQUEST CORRELATION AND CONTEXT

Implement request correlation.

Each request should have a server-recognized correlation/request identifier.

Support propagation through appropriate internal execution paths.

Where applicable, propagate context into:

* database operations;
* Redis operations;
* emitted events;
* logs;
* traces;
* background work initiated by this scope.

Do not place sensitive personal data into correlation fields.

---

# 12. VALIDATION

Implement strict request validation.

Validate:

* types;
* required fields;
* string lengths;
* allowed formats;
* username rules;
* email format;
* password policy;
* pagination inputs where applicable;
* identifiers;
* relationship target IDs;
* state-transition inputs.

Reject malformed input consistently.

Do not rely on frontend validation for security.

---

# 13. ERROR HANDLING

Implement shared exception/error handling.

Define appropriate categories such as:

* validation;
* authentication;
* authorization;
* not found;
* conflict;
* rate limit;
* invalid state;
* dependency failure;
* internal failure.

Error codes must be stable enough for clients and tests to consume.

Do not expose database-specific error strings as public API contracts.

Preserve request/correlation IDs for troubleshooting.

---

# 14. DATABASE FOUNDATION

Implement the PostgreSQL persistence foundation required by this prompt.

The implementation must include actual schema definitions and migrations for the in-scope domains.

Use appropriate:

* primary keys;
* foreign keys;
* unique constraints;
* check constraints;
* indexes;
* timestamps;
* deletion semantics;
* transaction boundaries.

Avoid storing derived state as authoritative state.

Do not create tables for out-of-scope product areas unless a table is genuinely required by the current foundation.

---

# 15. IDENTIFIER MODEL

Use one distributed-system-compatible identifier strategy.

Identifiers must be:

* globally unique;
* suitable for API exposure;
* serializable;
* indexable;
* safe for distributed generation;
* consistent across domains.

Use the same identifier conventions for:

* accounts;
* profiles;
* sessions;
* devices;
* relationship records;
* verification/recovery records;
* domain events;
* request/correlation IDs where their semantics differ.

Do not casually mix integer IDs, UUIDs, and opaque IDs without explicit domain justification.

---

# 16. TIME MODEL

Use timezone-aware server timestamps.

For database records, implement consistent semantics for fields such as:

* `createdAt`;
* `updatedAt`;
* `deletedAt`;
* `expiresAt`;
* `lastUsedAt`;
* `verifiedAt`.

The application server must be authoritative for business-state timestamps.

Do not trust client-provided timestamps for account, session, authentication, or relationship state.

---

# 17. ACCOUNT MODEL

Implement the core account domain.

The account model must support, as appropriate:

* unique account ID;
* username;
* normalized username;
* email;
* normalized email;
* password credential reference;
* account type;
* privacy state;
* lifecycle state;
* verification state;
* timestamps.

Define lifecycle states that distinguish, as appropriate:

* active;
* suspended;
* restricted;
* pending/deactivation state if needed;
* deleted.

Do not use a boolean field when a real lifecycle state is required for unambiguous behavior.

---

# 18. USERNAME RULES

Implement canonical username handling.

Define:

* normalization;
* case behavior;
* allowed characters;
* minimum/maximum length;
* uniqueness;
* creation;
* update/change behavior.

Database-level uniqueness must enforce the authoritative constraint.

Application-level checks may provide better errors but must not replace the database constraint.

Prevent race conditions around username creation/change.

---

# 19. EMAIL AND CREDENTIAL MODEL

Implement secure credential handling.

Passwords must use a modern password hashing algorithm such as **Argon2id** where supported by the repository stack.

Never store plaintext passwords.

Never log passwords.

Never return credential material in API responses.

Separate authentication credentials from ordinary account/profile data.

Define credential update behavior with appropriate session invalidation considerations.

---

# 20. REGISTRATION

Implement account registration.

Registration must include, as appropriate:

* input validation;
* username validation;
* email validation;
* password hashing;
* uniqueness enforcement;
* account creation;
* initial profile creation;
* verification state;
* initial session creation where appropriate;
* security-event logging;
* rate limiting.

Use transactions where account and required initial profile state must be created atomically.

Do not create an account that is partially persisted because of avoidable transaction failures.

---

# 21. LOGIN

Implement secure login.

Cover:

* credential lookup;
* password verification;
* account-state validation;
* rate limiting;
* session creation;
* device registration;
* security event recording.

Do not reveal whether a specific email or username exists through unnecessarily precise authentication errors.

Handle disabled/suspended accounts according to explicit account-state policy.

---

# 22. SESSION MANAGEMENT

Implement persistent session management.

A session should support, as appropriate:

* session ID;
* account ID;
* device ID;
* creation time;
* expiration;
* last activity;
* revocation;
* rotation;
* metadata needed for security operations.

Implement secure session revocation.

Support:

* logout current session;
* revoke individual sessions;
* revoke all other sessions;
* security-triggered revocation.

Do not rely solely on client deletion of a token to terminate a session.

---

# 23. TOKEN AND SESSION SECURITY

Use a secure credential model appropriate for the selected backend architecture.

Where access/refresh credentials are used:

* use short-lived access credentials where practical;
* protect refresh credentials;
* rotate refresh credentials;
* support revocation;
* detect reuse where the chosen model supports it;
* hash stored long-lived secrets when feasible;
* avoid storing raw secrets unnecessarily.

Do not place sensitive long-lived credentials in ordinary logs.

Do not expose session internals to unauthorized callers.

---

# 24. DEVICE MANAGEMENT

Implement device/session records sufficient to support:

* multiple devices;
* session listing;
* device identification;
* revocation;
* last-used metadata.

Do not collect or retain unnecessary device information.

Define which device metadata is safe to expose to users.

Do not trust arbitrary client-supplied device labels as security-sensitive truth.

---

# 25. PASSWORD RECOVERY

Implement password-recovery infrastructure.

Support:

* recovery request;
* short-lived recovery token or equivalent;
* secure storage of recovery material;
* expiration;
* one-time use;
* password replacement;
* session invalidation where appropriate;
* security event recording.

Do not store raw reusable recovery tokens in plaintext when a secure hashed representation can be used.

Avoid account-enumeration leakage in recovery-request responses.

External email delivery may be represented behind an integration boundary if credentials/provider access are unavailable.

Do not fabricate successful third-party delivery.

---

# 26. VERIFICATION

Implement provider-independent verification state and the local domain logic required for:

* verification challenge creation;
* challenge expiration;
* one-time verification;
* attempt limits;
* verification state transitions.

For email/SMS delivery:

* isolate the provider integration;
* make the adapter replaceable;
* handle provider failure;
* avoid claiming external delivery when it has not been performed.

Do not hardcode verification codes.

---

# 27. ACCOUNT SECURITY EVENTS

Create a secure internal security-event mechanism for the in-scope domain.

Record appropriate events such as:

* registration;
* successful login;
* failed login;
* logout;
* password change;
* password recovery;
* session revocation;
* verification changes;
* account-state changes.

Security events must have:

* event ID;
* event type;
* account reference where permitted;
* server timestamp;
* correlation/request ID where applicable;
* safe metadata.

Do not store passwords, raw tokens, or unnecessary sensitive values.

---

# 28. PROFILE DOMAIN

Implement profile management.

A profile should support, as appropriate:

* profile ID;
* account association;
* display name;
* biography;
* avatar/media reference as an opaque media reference only;
* profile link data where within current foundation scope;
* timestamps.

The profile domain must not implement full media processing.

Store media references, not media binaries, in PostgreSQL.

---

# 29. PROFILE PRIVACY

Implement account/profile privacy state.

Support at minimum:

* public account;
* private account.

Privacy state must be authoritative server-side.

Changing privacy state must be transactional with the account/profile mutation.

The implementation must not rely on client-side privacy flags.

---

# 30. PROFILE READS

Implement profile retrieval appropriate to this scope.

Profile retrieval must distinguish:

* authenticated caller;
* anonymous caller where supported;
* caller relationship;
* blocked relationship;
* private account;
* public account.

Do not expose private-account data merely because an API client knows the account ID.

Do not expose internal account fields unnecessarily.

---

# 31. PROFILE UPDATES

Implement secure profile updates.

Support appropriate update behavior for:

* display name;
* biography;
* username where permitted;
* profile link fields where within scope;
* privacy state.

Apply:

* validation;
* authorization;
* conflict handling;
* audit/security logging where appropriate.

Prevent unauthorized modification of another account's profile.

---

# 32. SOCIAL GRAPH MODEL

Implement the foundational relationship domain.

Support:

* follow;
* unfollow;
* follow request;
* approve follow request;
* reject follow request;
* block;
* unblock;
* mute;
* unmute;
* restrict;
* unrestrict.

Model relationship state explicitly.

Do not represent all relationship types as one ambiguous table unless the resulting semantics remain unambiguous and maintainable.

---

# 33. FOLLOW MODEL

Implement follow semantics.

For public accounts:

* follow creates an active relationship.

For private accounts:

* follow creates a pending request.

Define:

* unique relationship constraints;
* duplicate behavior;
* idempotency;
* authorization;
* state transitions;
* timestamps.

Prevent concurrent requests from producing duplicate logical relationships.

---

# 34. FOLLOW REQUESTS

Implement:

* creation;
* listing where required;
* approval;
* rejection;
* cancellation where applicable;
* duplicate protection;
* authorization.

Only the target account may approve/reject another user's pending follow request.

Define behavior when:

* target becomes public;
* requester is blocked;
* requester account is suspended;
* request is already resolved.

---

# 35. BLOCKING

Implement block relationships.

Blocking must affect the relevant authorization decisions within the implemented foundation.

At minimum consider:

* profile access;
* follow behavior;
* follow requests;
* relationship visibility;
* relationship mutations.

Define behavior for existing follow relationships when a block is created.

Blocking should not depend on client-side filtering.

---

# 36. MUTING

Implement mute state.

Within this prompt, mute is primarily a relationship preference.

Store:

* source account;
* target account;
* state/lifecycle;
* timestamps.

Do not implement feed-ranking behavior yet.

The mute domain may provide policy information for later systems.

---

# 37. RESTRICTION

Implement restriction state.

Store and expose only the information required for authorized future consumers.

Do not implement all downstream restriction behavior for comments, messaging, or stories in this prompt.

The current backend must establish the relationship state and policy boundary so later systems can consume it consistently.

---

# 38. RELATIONSHIP AUTHORIZATION

Implement reusable relationship-policy logic.

Later domains must be able to ask questions such as:

* Is A following B?
* Does B have a pending follow request from A?
* Has A blocked B?
* Has B blocked A?
* Has A muted B?
* Has A restricted B?
* Is B's account private?

Avoid duplicating these checks across controllers.

Provide service/module interfaces that encapsulate relationship semantics.

---

# 39. SOCIAL GRAPH QUERIES

Implement efficient queries for:

* relationship state between two accounts;
* whether a user follows another user;
* follower existence;
* following existence;
* pending follow requests;
* blocked state;
* muted state;
* restricted state.

Use appropriate indexes.

Avoid unbounded full-table scans for ordinary relationship checks.

---

# 40. PAGINATION

Implement cursor-based pagination for in-scope relationship lists where lists are exposed.

Apply:

* stable ordering;
* bounded page size;
* maximum page size;
* cursor validation;
* duplicate protection;
* deterministic traversal.

Do not build relationship APIs around large SQL offsets when cursor pagination is appropriate.

---

# 41. REDIS USAGE

Use Redis only where it provides a clear benefit within the current scope.

Appropriate uses may include:

* rate limiting;
* short-lived authentication/recovery state where justified;
* cacheable relationship lookups where beneficial;
* temporary security coordination.

Define:

* key namespace;
* TTL;
* serialization;
* invalidation;
* failure behavior.

The PostgreSQL database remains authoritative for durable account, profile, session, and relationship state.

The backend must remain safe when Redis is unavailable unless the specific protected operation necessarily requires Redis-backed coordination.

---

# 42. RATE LIMITING

Implement rate limiting appropriate to the authentication and account-security scope.

At minimum consider protection for:

* registration;
* login;
* password recovery;
* verification attempts;
* follow requests;
* relationship mutations;
* profile mutation endpoints.

Define:

* key dimensions;
* limits;
* time windows;
* response behavior;
* retry metadata where appropriate;
* storage;
* failure behavior.

Do not use hardcoded arbitrary limits without making them centrally configurable.

Avoid account enumeration through distinct rate-limit behavior where possible.

---

# 43. EVENT AND OUTBOX FOUNDATION

Implement an event-publication foundation for the domains covered by this prompt.

Where database-backed domain changes must reliably produce downstream events, use a transactional outbox or an equivalent reliable publication pattern.

The event system must support:

* event ID;
* event type;
* event version;
* producer;
* aggregate/resource ID;
* occurred-at timestamp;
* correlation ID where applicable;
* payload;
* schema version.

Events must be safe for at-least-once delivery.

Consumers must be expected to handle duplicates.

Do not build future event consumers in this prompt.

---

# 44. IN-SCOPE EVENTS

Create event contracts for lifecycle events such as:

* `account.created`;
* `account.updated`;
* `account.deleted`;
* `profile.updated`;
* `session.created`;
* `session.revoked`;
* `security.login_succeeded`;
* `security.login_failed`;
* `password.changed`;
* `verification.completed`;
* `follow.created`;
* `follow.removed`;
* `follow_request.created`;
* `follow_request.approved`;
* `follow_request.rejected`;
* `block.created`;
* `block.removed`;
* `mute.created`;
* `mute.removed`;
* `restriction.created`;
* `restriction.removed`.

Use one naming/versioning strategy.

Do not publish undocumented payloads.

---

# 45. TRANSACTION BOUNDARIES

Use transactions where atomicity is required.

Examples include:

* account creation with initial profile;
* username mutation with uniqueness enforcement;
* follow-state transition;
* private-account request transition;
* block state transition;
* account privacy transition where related state must remain consistent;
* session revocation with associated security state where necessary.

Do not create unnecessarily large transactions spanning unrelated domains.

---

# 46. CONCURRENCY

Design for concurrent requests.

Handle races such as:

* two users creating the same username;
* duplicate registration attempts;
* simultaneous follow/unfollow requests;
* simultaneous follow-request approvals;
* simultaneous block/unblock requests;
* session revocation racing with refresh;
* duplicate password-recovery attempts.

Use:

* database uniqueness;
* transactions;
* appropriate locking;
* optimistic concurrency;
* idempotency;

where necessary.

Do not rely on a prior read alone to guarantee uniqueness.

---

# 47. AUTHORIZATION SECURITY

Every protected operation must enforce authorization server-side.

At minimum protect:

* profile mutations;
* username changes;
* privacy changes;
* session management;
* password changes;
* relationship mutations;
* follow-request decisions.

Do not trust account IDs supplied by the client without verifying the authenticated principal's authority.

---

# 48. SECURITY HARDENING

Within this backend scope implement appropriate defenses against:

* credential stuffing;
* brute-force login attempts;
* account enumeration;
* injection;
* unsafe deserialization;
* malicious input;
* token theft;
* session fixation;
* replay;
* privilege escalation;
* unauthorized relationship mutation.

Use:

* secure password hashing;
* secure token/session handling;
* strict validation;
* rate limiting;
* least privilege;
* safe error messages;
* secure headers;
* dependency hygiene.

---

# 49. DATABASE INDEXING

Create indexes based on actual in-scope query patterns.

At minimum evaluate indexes for:

* normalized username;
* normalized email where appropriate;
* account status;
* session lookup/revocation;
* device/account lookup;
* follow source/target;
* follow request target/status;
* block source/target;
* mute source/target;
* restriction source/target;
* timestamps used for ordered relationship retrieval.

Do not create redundant indexes merely to increase index count.

---

# 50. MIGRATIONS

All schema changes must be represented through real migrations.

Migration requirements:

* deterministic;
* reversible where practical;
* safe for repeated environments;
* documented;
* compatible with the application's deployment ordering.

Do not modify production schema assumptions manually inside application startup.

Do not rely on automatic schema synchronization in production.

---

# 51. SOFT DELETE AND LIFECYCLE

Define explicit deletion semantics for in-scope entities.

Where soft deletion is used, define:

* `deletedAt`;
* visibility behavior;
* uniqueness implications;
* relationship implications;
* recovery behavior if supported.

Do not implement soft deletion merely because it is common practice.

Use hard deletion where appropriate and safe within the domain.

Account deletion must be architected so later asynchronous cleanup systems can consume the deletion event.

---

# 52. OBSERVABILITY

Instrument the implemented backend.

Include:

* structured logging;
* request IDs;
* correlation IDs;
* API latency;
* error counts;
* authentication failures;
* authorization failures;
* rate-limit events;
* database latency;
* Redis failures;
* event publication failures.

Where tracing infrastructure is available, create trace spans for important operations.

Do not log:

* plaintext passwords;
* raw access tokens;
* recovery tokens;
* sensitive security secrets.

---

# 53. HEALTH ENDPOINTS

Implement health/readiness/liveness behavior appropriate to this backend.

Distinguish:

* process liveness;
* application readiness;
* dependency readiness.

A health endpoint must not unnecessarily reveal sensitive infrastructure details.

Do not make liveness dependent on every optional external integration.

---

# 54. GRACEFUL SHUTDOWN

Implement graceful shutdown.

Handle:

* HTTP server draining;
* database connection cleanup;
* Redis cleanup;
* event/outbox worker shutdown where applicable;
* in-flight request completion;
* termination signals.

Avoid abruptly terminating processes while durable work can be safely completed or re-queued.

---

# 55. API CONTRACTS TO IMPLEMENT

Implement the in-scope API surface with consistent naming.

The exact path structure may follow the repository's established conventions, but must cover functionality equivalent to:

## Authentication

* registration;
* login;
* logout;
* refresh/session renewal where applicable;
* password recovery;
* password update;
* verification.

## Account/Profile

* get current account;
* get profile;
* update profile;
* change username;
* change privacy state.

## Sessions

* list sessions;
* revoke current session;
* revoke selected session;
* revoke all other sessions.

## Relationships

* follow;
* unfollow;
* list relevant follow requests;
* approve request;
* reject request;
* block;
* unblock;
* mute;
* unmute;
* restrict;
* unrestrict;
* relationship status.

Do not implement routes for out-of-scope domains.

---

# 56. API RESPONSE DISCIPLINE

Client responses must contain only data appropriate to the caller.

Do not expose internal fields such as:

* password hashes;
* raw session secrets;
* internal security metadata;
* provider credentials;
* database implementation details.

Use stable response models.

Do not serialize ORM entities directly if doing so would risk exposing internal fields.

---

# 57. IDEMPOTENCY

Where mutation endpoints are retry-sensitive, implement safe duplicate handling.

At minimum evaluate idempotency for:

* registration;
* follow;
* unfollow;
* follow-request creation;
* block;
* unblock;
* session revocation;
* password-recovery processing where applicable.

Do not create duplicate relationship rows under concurrent retries.

Use database constraints plus application logic.

---

# 58. TESTING STRATEGY

Create actual tests for the current backend scope.

## Unit Tests

Cover:

* credential validation;
* username normalization;
* authentication policies;
* session policies;
* relationship rules;
* privacy rules;
* authorization policies;
* state transitions;
* error mapping;
* pagination/cursor validation;
* rate-limit behavior.

## Integration Tests

Cover:

* database persistence;
* migrations;
* account creation;
* authentication;
* session creation/revocation;
* profile operations;
* follow relationships;
* private-account follow requests;
* blocking;
* muting;
* restriction;
* concurrent relationship mutations where practical;
* Redis-backed mechanisms where applicable;
* event/outbox persistence.

## API/Contract Tests

Validate:

* status codes;
* response schemas;
* error structures;
* authentication requirements;
* authorization;
* pagination behavior;
* idempotency behavior.

Do not create tests that merely assert that controllers return mocked success responses.

---

# 59. SECURITY TESTING

Within the current scope test at least:

* unauthorized profile mutation;
* unauthorized session revocation;
* unauthorized follow-request approval;
* cross-account data access;
* invalid token/session;
* expired credentials;
* password policy failures;
* recovery-token reuse;
* account enumeration behavior;
* rate-limit enforcement;
* duplicate relationship race handling.

Do not claim full security certification.

---

# 60. PERFORMANCE TESTING

Perform targeted backend validation where the local environment permits.

At minimum evaluate:

* indexed relationship lookup;
* username lookup;
* session lookup;
* follower/following existence;
* paginated relationship retrieval.

Do not claim production-scale performance from local testing.

Document actual test conditions and results.

---

# 61. DOCUMENTATION

Create or update implementation documentation for:

* backend setup;
* environment variables;
* local database setup;
* migrations;
* authentication behavior;
* session behavior;
* profile/account behavior;
* relationship semantics;
* API endpoints;
* error codes;
* rate limits;
* event contracts;
* testing instructions.

Documentation must describe the actual implementation.

Do not document future features as though they are already implemented.

---

# 62. PORTABLE CONTRACT REQUIREMENT

Because backend work may be produced independently from web, mobile, infrastructure, and QA work, maintain explicit portable contracts.

The implementation must provide or update contract artifacts for:

* API request/response schemas;
* authentication behavior;
* session semantics;
* authorization;
* account/profile model;
* relationship model;
* errors;
* pagination;
* identifiers;
* timestamps;
* event envelopes.

Prefer machine-readable schemas where the repository supports them.

The contracts must be understandable without access to this conversation.

---

# 63. CROSS-PART COMPATIBILITY

The backend implementation must remain compatible with:

* web clients;
* mobile clients;
* future media systems;
* feed systems;
* messaging;
* notifications;
* moderation;
* infrastructure;
* QA.

Do not introduce frontend-specific or mobile-specific assumptions into backend domain logic.

Do not invent contracts that require clients to reproduce server-side business rules.

---

# 64. FUTURE-DOMAIN EXTENSIBILITY

Within this prompt, establish clean interfaces that later systems can consume.

Examples:

* relationship-policy service;
* account authorization policy;
* session validation;
* identity lookup;
* account privacy lookup;
* event publication;
* media-reference validation;
* domain-level account lifecycle events.

Do not implement future-domain business logic merely to create these interfaces.

---

# 65. FAILURE BEHAVIOR

Define and implement appropriate failure behavior for:

* PostgreSQL unavailable;
* Redis unavailable;
* event/outbox publication delayed;
* malformed requests;
* authentication failure;
* authorization failure;
* invalid sessions;
* provider failure for verification delivery;
* duplicate requests;
* concurrent state changes.

Do not make optional dependencies a single point of failure for authentication-critical paths unless technically necessary.

Where Redis supports security controls and becomes unavailable, choose and document a safe degraded behavior rather than silently disabling abuse protection.

---

# 66. DATA PRIVACY

Protect:

* credentials;
* email;
* session information;
* device information;
* security metadata.

Do not unnecessarily expose private account information.

Support deletion/lifecycle hooks so later data-retention and cleanup systems can consume account deletion events.

Do not emit sensitive personal data in logs or events without a legitimate requirement.

---

# 67. NO FAKE COMPLETENESS

Do not use:

* mock database persistence in production paths;
* fake authentication;
* hardcoded account credentials;
* placeholder relationship logic;
* TODO/FIXME markers for required current functionality;
* pseudo-code;
* dummy event publishing;
* fabricated external-provider success;
* fake Redis behavior;
* incomplete controllers presented as finished.

Every feature inside this prompt's scope must be genuinely implemented.

---

# 68. FILE/MODULE SCOPE

Structure the implementation around the actual repository.

The milestone should generally remain a meaningful engineering unit rather than a collection of tiny files.

Reasonable areas include:

* bootstrap/config;
* common API infrastructure;
* database;
* auth;
* sessions;
* accounts;
* profiles;
* relationships;
* events;
* cache;
* health;
* tests;
* documentation.

Do not create unnecessary files solely to reach a target count.

Do not merge unrelated domains merely to reduce file count.

---

# 69. VALIDATION

Before completion:

1. run the formatter/linter configured by the repository;
2. run type checking;
3. run database migration validation;
4. run unit tests;
5. run relevant integration tests;
6. run relevant API/contract tests;
7. run security-focused tests;
8. validate startup configuration;
9. validate health endpoints;
10. validate relevant documentation and generated contracts.

If a required validation cannot execute because an external dependency is genuinely unavailable, state that exact limitation.

Do not claim success for validation that was not performed.

---

# 70. IMPLEMENTATION REPORT

After implementation, provide a completion report containing:

## Files Created

List every file created.

## Files Modified

List every file modified.

## Files Deleted

List every file deleted, if any.

## Backend Domains Implemented

Summarize:

* bootstrap;
* configuration;
* authentication;
* sessions;
* accounts;
* profiles;
* social graph;
* supporting infrastructure.

## Database Changes

List:

* tables;
* indexes;
* constraints;
* migrations;
* lifecycle changes.

## API Changes

List the implemented endpoints and major request/response contracts.

## Redis Changes

List keys/namespaces and their purposes.

## Event Changes

List events, schemas, producers, and outbox behavior.

## Security Changes

Summarize:

* credential security;
* authentication;
* authorization;
* rate limiting;
* session security;
* privacy protections.

## Tests Created

List test categories and major scenarios.

## Tests Executed

State exactly which tests were actually executed.

## Validation Performed

State exact validation performed.

## Documentation Changes

List documentation created or updated.

## Integration Considerations

Describe the contracts that web, mobile, infrastructure, and future backend domains must consume.

## Compatibility Considerations

Identify any compatibility-sensitive changes.

## Known Limitations

List genuine current limitations.

## Unresolved Issues

List only issues that remain unresolved.

---

# 71. DEFINITION OF DONE

This backend milestone is complete only when:

* the backend application boots correctly;
* configuration is validated;
* API validation and error handling are implemented;
* request/correlation IDs are implemented;
* PostgreSQL persistence is real and migrated;
* identifiers and timestamps are consistent;
* registration works;
* login works;
* secure credentials are implemented;
* sessions are persisted and revocable;
* account lifecycle is implemented;
* password recovery is implemented within the available integration boundary;
* verification state is implemented;
* profiles are implemented;
* usernames are validated and uniquely enforced;
* public/private account state works;
* follow/unfollow works;
* private-account follow requests work;
* block/unblock works;
* mute/unmute works;
* restrict/unrestrict works;
* relationship authorization is centralized;
* relevant pagination works;
* relevant rate limits work;
* Redis usage is explicit and bounded;
* event/outbox foundations exist;
* security events are implemented where required;
* observability is implemented;
* health/readiness/liveness behavior exists;
* graceful shutdown exists;
* unit tests exist;
* integration tests exist;
* API/contract tests exist;
* security-focused tests exist;
* migrations validate;
* type checking passes;
* lint/format validation passes where configured;
* documentation reflects actual behavior;
* no secrets are committed;
* no fake implementations exist;
* no intentional gaps remain inside the defined scope.

---

# 72. FINAL IMPLEMENTATION DISCIPLINE

Implement **only the current prompt's scope**.

Do not implement:

* posts;
* stories;
* short-form video;
* media processing;
* feeds;
* discovery;
* comments;
* likes;
* saves;
* shares;
* messaging;
* notifications;
* moderation;
* administration;
* analytics;
* full infrastructure.

Do not redesign unrelated architecture.

Do not assume another AI prompt has been executed.

Do not depend on another AI conversation.

Do not introduce undocumented contracts.

Do not claim external provisioning or third-party delivery that did not occur.

Produce real, tested, documented backend functionality for the foundational identity, account, profile, session, and social-graph domains.
