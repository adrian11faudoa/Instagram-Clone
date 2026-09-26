# Instagram — Backend Prompt — Volume 7

# 1. ROLE

You are the **Staff Backend Engineering team** responsible for implementing the cross-cutting backend platform hardening, reliability, observability, integration, performance, and operational foundations for the **Instagram** project.

Operate with the combined responsibilities of:

* Staff Backend Engineer
* Backend Architect
* Distributed Systems Engineer
* SRE / Reliability Engineer
* Security Engineer
* Performance Engineer
* Database Reliability Engineer
* Observability Engineer
* Platform Integration Engineer
* QA-minded Backend Engineer
* DevOps-aware Application Engineer

This is a **bounded backend implementation assignment**.

You must implement the real backend functionality defined by this prompt.

Do not implement unrelated product functionality merely because it appears in the global Instagram product vision.

The mandatory rule for this task is:

**Implement only the current prompt's scope.**

---

# 2. PROJECT IDENTITY

**Project Name:** Instagram

**Product Type:** Production-grade visual social networking platform.

The backend includes:

* identity;
* accounts and profiles;
* social graph;
* content;
* media;
* engagement;
* feed;
* discovery/search;
* messaging;
* realtime;
* notifications;
* moderation;
* administration;
* analytics.

The completed platform is intended to support approximately:

* 100 million registered accounts;
* 20 million daily active users;
* 2 million peak concurrent active sessions;
* approximately 100,000 sustained API requests per second;
* approximately 250,000 requests per second during peak bursts;
* high-volume media traffic;
* high event throughput;
* large realtime connection volumes;
* distributed asynchronous processing.

These are global architectural targets.

This prompt implements the **cross-cutting backend platform foundations** required to make the previously implemented backend domains operationally coherent, resilient, observable, secure, and integration-ready.

---

# 3. CURRENT BACKEND ASSIGNMENT

Implement the backend platform hardening and cross-cutting infrastructure required by the completed backend surface.

This includes:

1. centralized dependency management;
2. service-to-service boundaries;
3. shared request context;
4. structured logging;
5. distributed tracing;
6. metrics;
7. health/readiness/liveness;
8. graceful shutdown;
9. timeout policies;
10. retry policies;
11. circuit-breaking where justified;
12. resilience wrappers;
13. idempotency infrastructure refinement;
14. background worker reliability;
15. queue and event observability;
16. database connection management;
17. database performance protections;
18. Redis reliability and failure behavior;
19. cache consistency safeguards;
20. API performance protections;
21. request-size and payload protections;
22. centralized rate-limit infrastructure;
23. security hardening;
24. dependency/security configuration;
25. audit-safe logging;
26. operational diagnostics;
27. configuration hardening;
28. backend integration contracts;
29. contract-generation/validation infrastructure where appropriate;
30. CI-oriented backend validation;
31. performance instrumentation;
32. failure testing support;
33. backend operational documentation;
34. tests.

This prompt is not another product-feature milestone.

It hardens and connects the backend systems already covered by the project-specific implementation scope.

---

# 4. REPOSITORY INSPECTION

Before modifying or creating code, inspect the repository.

Inspect:

* all backend applications;
* shared libraries/packages;
* domain modules;
* API infrastructure;
* event infrastructure;
* queue infrastructure;
* worker applications;
* PostgreSQL configuration;
* Redis configuration;
* OpenSearch integration;
* WebSocket/realtime infrastructure;
* media integration;
* authentication;
* authorization;
* logging;
* metrics;
* tracing;
* health checks;
* tests;
* linting;
* formatting;
* CI configuration;
* environment configuration;
* Docker/container definitions;
* operational documentation.

Treat the repository as the source of truth for actual implementation state.

Do not assume previous AI prompts were executed.

Do not assume another Claude conversation exists.

Do not fabricate missing infrastructure.

Where equivalent hardening already exists, strengthen or complete it rather than creating competing implementations.

---

# 5. TECHNOLOGY BASELINE

Remain compatible with the repository's established stack.

The project baseline includes:

* TypeScript;
* Node.js;
* PostgreSQL;
* Redis;
* durable event infrastructure;
* background jobs;
* OpenSearch;
* realtime transport;
* REST APIs;
* structured logging;
* distributed tracing;
* metrics;
* automated testing.

Use the repository's existing observability and infrastructure libraries when they are sound.

Do not replace the entire backend framework merely to introduce a preferred library.

---

# 6. BOUNDED IMPLEMENTATION SCOPE

## In Scope

Implement or harden:

* shared request context;
* correlation IDs;
* trace propagation;
* structured logging;
* sensitive-field redaction;
* metrics conventions;
* health endpoints;
* dependency health;
* readiness/liveness;
* graceful shutdown;
* timeout middleware/interceptors;
* retry utilities;
* circuit breakers where justified;
* resilience policies;
* DB connection pools;
* Redis connection behavior;
* queue worker resilience;
* event-consumer resilience;
* background-job observability;
* centralized rate limiting;
* request-size limits;
* response-size protections where appropriate;
* API performance instrumentation;
* database query instrumentation;
* cache observability;
* security middleware;
* dependency security configuration;
* secret/configuration handling;
* operational diagnostics;
* contract validation infrastructure;
* backend CI validation;
* failure-oriented tests;
* performance instrumentation;
* operational documentation.

## Out of Scope

Do not implement:

* new product-domain functionality;
* web UI;
* mobile UI;
* new feed algorithms;
* new messaging features;
* new content features;
* new moderation workflows;
* cloud infrastructure provisioning;
* Kubernetes production deployment;
* complete CI/CD infrastructure;
* data warehouse construction;
* full-scale load-generation infrastructure.

This prompt may prepare repository-level configuration and validation needed by future infrastructure work, but must not claim that external infrastructure has been provisioned.

---

# 7. SHARED REQUEST CONTEXT

Implement a standardized backend request context.

It should carry, where applicable:

* request ID;
* correlation ID;
* trace ID;
* authenticated principal reference;
* client/application identifier;
* request start time;
* operation name.

The context must be safe to propagate into:

* logs;
* traces;
* metrics;
* events;
* background-job metadata.

Do not include:

* passwords;
* access tokens;
* raw message bodies;
* private media;
* unnecessary personal information.

---

# 8. CORRELATION ID POLICY

Define one canonical correlation/request-ID strategy.

Requirements:

* accept a valid inbound identifier when policy permits;
* generate one when absent;
* validate length/format;
* propagate downstream;
* include it in safe error responses;
* include it in structured logs;
* include it in relevant event/job context.

Do not allow arbitrary unbounded client strings to become logging or tracing identifiers.

---

# 9. DISTRIBUTED TRACING

Implement distributed tracing integration.

Instrument major backend boundaries including:

* HTTP requests;
* database calls;
* Redis;
* event publication;
* event consumption;
* background jobs;
* OpenSearch requests;
* object-storage operations where applicable;
* realtime operations where technically supported.

Propagate trace context across:

* synchronous service calls;
* events where appropriate;
* background jobs.

Do not place sensitive data into span attributes.

---

# 10. STRUCTURED LOGGING

Standardize structured logging.

Log records should include, where appropriate:

* timestamp;
* severity;
* service/module;
* environment;
* operation;
* request ID;
* correlation ID;
* trace ID;
* outcome;
* duration;
* error classification.

Support safe metadata.

Do not log:

* passwords;
* raw authentication credentials;
* refresh tokens;
* recovery tokens;
* private message bodies;
* private media contents;
* secrets.

---

# 11. LOG REDACTION

Implement centralized redaction for known sensitive fields.

At minimum evaluate:

* passwords;
* access tokens;
* refresh tokens;
* API keys;
* authorization headers;
* cookies;
* push tokens;
* signed media URLs;
* recovery tokens.

Redaction must occur before structured data reaches the logging sink.

Do not rely on every individual developer remembering to redact fields manually.

---

# 12. METRICS FOUNDATION

Implement standardized metrics for:

* request count;
* request latency;
* error count;
* dependency latency;
* database query duration;
* Redis operations;
* cache hits/misses;
* event publication;
* event-consumer lag/failure;
* queue depth;
* job success/failure;
* realtime connection counts;
* media-processing initiation;
* search requests;
* feed requests;
* notification processing;
* moderation processing.

Avoid unbounded metric labels.

Do not use user IDs, content IDs, or arbitrary request values as high-cardinality metric labels.

---

# 13. BUSINESS VS OPERATIONAL METRICS

Separate:

**business/product events**

from:

**operational metrics**.

Business events belong to the analytics/event architecture.

Operational metrics must remain focused on system health and performance.

Do not use database writes to analytics events as a substitute for Prometheus/OpenTelemetry-style operational metrics.

---

# 14. HEALTH MODEL

Implement standardized:

* liveness;
* readiness;
* startup/initialization health where useful.

Health responses must distinguish:

**process is alive**

from:

**application is ready to serve traffic**.

Do not expose internal credentials, database names, secret configuration, or detailed dependency errors publicly.

---

# 15. DEPENDENCY HEALTH

Define dependency-aware readiness for:

* PostgreSQL;
* Redis;
* event infrastructure;
* queue infrastructure;
* OpenSearch;
* required object storage integrations.

Optional dependencies must not unnecessarily prevent unrelated application functionality from becoming ready.

Differentiate:

* critical dependency;
* degraded-but-operational dependency;
* optional dependency.

---

# 16. GRACEFUL SHUTDOWN

Implement standardized graceful shutdown.

The application must:

1. stop accepting new work;
2. allow safe in-flight requests to finish;
3. close realtime connections appropriately;
4. stop accepting new background jobs;
5. finish or safely requeue active work;
6. flush required telemetry;
7. close Redis connections;
8. close database pools;
9. close event/queue connections;
10. exit within a bounded timeout.

Shutdown must be observable.

---

# 17. TIMEOUT POLICY

Create centralized timeout policies.

At minimum distinguish:

* incoming HTTP request timeout;
* database timeout;
* Redis timeout;
* OpenSearch timeout;
* object-storage timeout;
* external-provider timeout;
* event publication timeout;
* background-job execution timeout.

Do not allow requests to wait indefinitely on dependencies.

Avoid setting every timeout to one global value.

Timeouts must reflect the operation being protected.

---

# 18. RETRY POLICY

Create reusable retry behavior for transient failures.

Requirements:

* bounded attempts;
* exponential backoff;
* jitter;
* retry classification;
* cancellation support;
* timeout integration;
* observability.

Do not retry:

* validation errors;
* authentication failures;
* authorization failures;
* deterministic conflicts;
* non-idempotent operations without appropriate idempotency protection.

---

# 19. CIRCUIT BREAKING

Implement circuit breakers only for dependencies where they provide concrete value.

Potential candidates include:

* external notification providers;
* search;
* object storage;
* external moderation providers;
* other remote integrations.

A circuit breaker must define:

* failure threshold;
* open duration;
* half-open behavior;
* fallback;
* telemetry.

Do not wrap every internal function in a circuit breaker.

---

# 20. BULKHEADS AND FAILURE ISOLATION

Where justified, isolate resource pools for:

* realtime;
* API traffic;
* background workers;
* media processing;
* search;
* notifications.

Prevent one overloaded subsystem from exhausting all database or worker resources.

Use bounded concurrency.

Do not create unnecessary process fragmentation.

---

# 21. DATABASE CONNECTION MANAGEMENT

Harden PostgreSQL access.

Implement:

* bounded pool size;
* connection acquisition timeout;
* query timeout;
* idle behavior;
* graceful pool shutdown;
* instrumentation;
* appropriate transaction timeout.

Avoid creating one database connection per request.

Prevent accidental connection-pool multiplication across worker processes.

---

# 22. DATABASE PERFORMANCE PROTECTION

Implement safeguards against:

* unbounded queries;
* missing pagination;
* excessive result sets;
* accidental full-table operations;
* N+1 patterns where detectable;
* expensive queries without timeouts.

Where appropriate, add instrumentation to identify slow queries.

Do not automatically kill every query above an arbitrary threshold without understanding legitimate workloads.

---

# 23. DATABASE TRANSACTION SAFETY

Standardize transaction helpers.

Transaction helpers must:

* enforce bounded execution time;
* preserve tracing;
* surface errors safely;
* cooperate with retries;
* prevent accidental retries of unsafe transactions.

Document which operations require explicit idempotency.

Do not retry an entire transaction blindly when the transaction contains non-idempotent external side effects.

---

# 24. REDIS RELIABILITY

Harden Redis integration.

Support:

* connection retry;
* bounded retry;
* command timeout;
* reconnection;
* graceful shutdown;
* instrumentation;
* failure classification.

Redis failures must have explicit behavior per use case.

Examples:

* cache read failure → authoritative read where safe;
* rate limiter failure → safe configurable policy;
* realtime ephemeral-state failure → degraded realtime behavior;
* durable database data → never replaced by Redis.

---

# 25. CACHE SAFETY

Review implemented Redis caches.

Ensure:

* keys have namespaces;
* TTLs exist where appropriate;
* values cannot grow unbounded;
* invalidation is defined;
* cache failure is survivable where possible;
* sensitive data is not accidentally cached globally;
* authorization-sensitive data is properly scoped.

Do not cache protected resources under keys that omit the authorization context when that could leak data.

---

# 26. EVENT INFRASTRUCTURE RESILIENCE

Harden event publication and consumption.

Support:

* retry;
* backoff;
* dead-letter behavior;
* consumer idempotency;
* lag metrics;
* processing-time metrics;
* poison-message handling;
* graceful shutdown;
* replay-safe behavior.

Do not claim exactly-once processing without a genuine guarantee.

---

# 27. EVENT VERSIONING ENFORCEMENT

Where event schemas have versions:

* validate version;
* reject unsupported versions safely;
* support backward-compatible consumers where required;
* instrument version failures.

Do not silently accept malformed event payloads.

---

# 28. QUEUE WORKER RESILIENCE

Harden background workers.

Workers must support:

* bounded concurrency;
* graceful shutdown;
* retry;
* backoff;
* dead-letter;
* visibility/lease handling where relevant;
* job timeout;
* idempotency;
* metrics.

A worker crash must not permanently lose a durable job.

---

# 29. JOB OBSERVABILITY

Instrument:

* queue depth;
* active workers;
* job latency;
* retry count;
* failure count;
* dead-letter count;
* processing throughput;
* oldest queued job.

Use low-cardinality labels.

Do not include arbitrary resource IDs as metric dimensions.

---

# 30. RATE LIMITING FOUNDATION

Standardize backend rate limiting.

Support configurable dimensions such as:

* authenticated account;
* IP/network source;
* endpoint;
* device/session;
* application/client.

Define rate-limit responses consistently.

Where practical, return retry metadata.

Avoid exposing detailed internal abuse-detection logic to clients.

---

# 31. RATE-LIMIT FAILURE POLICY

Define what happens when the rate-limit store is unavailable.

Policies may differ by endpoint.

For example:

* authentication abuse controls may fail closed;
* low-risk read caching may fail open;
* sensitive administrative endpoints should prefer conservative behavior.

Do not silently disable critical abuse protection because Redis is unavailable.

---

# 32. REQUEST-SIZE PROTECTION

Implement limits for:

* HTTP body size;
* JSON payload size;
* query-string size;
* header size where configurable;
* file metadata payload;
* WebSocket message size.

Large media binaries must use the media/object-storage upload path rather than ordinary JSON APIs.

---

# 33. RESPONSE-SIZE PROTECTION

Prevent accidentally returning unbounded result sets.

Require:

* pagination;
* maximum page sizes;
* bounded batch requests;
* response limits where appropriate.

Do not permit an API client to request millions of rows in one response.

---

# 34. SECURITY MIDDLEWARE

Harden the API with appropriate:

* secure headers;
* request validation;
* content-type validation;
* CORS policy where applicable;
* CSRF protection where applicable;
* authentication enforcement;
* authorization integration;
* request-size limits;
* rate limiting.

Do not enable permissive security policies merely to make development easier.

---

# 35. SECRET HANDLING

Review backend configuration to ensure secrets are loaded only through appropriate secure configuration mechanisms.

Secrets include:

* database credentials;
* JWT/signing keys;
* session secrets;
* Redis credentials;
* Kafka credentials;
* OpenSearch credentials;
* cloud credentials;
* push provider secrets;
* external-service credentials.

Never commit real secrets.

Never print them during startup.

Never include them in exception messages.

---

# 36. DEPENDENCY SECURITY

Review project dependencies relevant to the backend.

Implement repository-compatible controls for:

* lockfile integrity;
* dependency vulnerability scanning;
* outdated critical dependencies where actionable;
* unsafe package configuration;
* secret scanning.

Do not blindly upgrade major frameworks if doing so destabilizes the current implementation.

---

# 37. API SECURITY HARDENING

Review all implemented backend domains for:

* authorization gaps;
* IDOR-style resource access;
* missing validation;
* oversized inputs;
* unsafe error exposure;
* rate-limit gaps;
* insecure direct object references;
* missing ownership checks.

Focus on current repository behavior.

Do not pretend an automated scanner proves complete security.

---

# 38. AUTHENTICATION HARDENING

Review the existing authentication implementation.

Validate:

* password hashing;
* token/session expiry;
* refresh rotation;
* revocation;
* account state;
* failed-login handling;
* credential reset;
* verification;
* administrative authentication.

Do not redesign authentication unnecessarily.

Fix concrete weaknesses found within the current backend scope.

---

# 39. AUTHORIZATION HARDENING

Review protected operations across:

* accounts;
* profiles;
* content;
* engagement;
* feed;
* discovery;
* messaging;
* notifications;
* moderation;
* administration.

Verify:

* principal is established correctly;
* resource ownership is checked;
* relationship policies are applied;
* privileged actions require explicit permission.

Do not rely on client-provided role information.

---

# 40. ERROR-EXPOSURE REVIEW

Ensure public error responses do not expose:

* SQL statements;
* stack traces;
* file paths;
* internal hostnames;
* credentials;
* provider secrets;
* infrastructure topology unnecessary to the caller.

Internal logs may retain safe diagnostic context subject to privacy/redaction rules.

---

# 41. OPERATIONAL DIAGNOSTICS

Implement safe diagnostic capabilities such as:

* dependency status;
* queue status;
* event lag;
* database pool status;
* Redis health;
* configuration validation;
* build/version metadata.

Protect operational diagnostics from ordinary users.

Do not expose secret configuration values.

---

# 42. VERSION AND BUILD INFORMATION

Expose safe application metadata for operational use where appropriate:

* application version;
* build identifier;
* environment;
* release timestamp.

Do not expose:

* Git credentials;
* environment secrets;
* internal source paths.

---

# 43. BACKEND CONTRACT VALIDATION

Create a repeatable mechanism to validate important backend contracts.

Where the repository supports it, validate:

* API schemas;
* event schemas;
* request/response models;
* database migrations;
* generated types;
* configuration schemas.

Contract validation should be executable in CI.

---

# 44. API SCHEMA GENERATION

Where appropriate, generate an authoritative API specification such as OpenAPI from the implemented backend contracts.

Ensure:

* routes are represented;
* authentication requirements are documented;
* request schemas are documented;
* response schemas are documented;
* error models are documented.

Do not document endpoints that do not exist.

---

# 45. EVENT SCHEMA VALIDATION

Where event schemas are machine-readable, validate:

* required fields;
* versions;
* payload types;
* compatibility rules.

Do not allow undocumented schema drift.

---

# 46. CI VALIDATION FOUNDATION

Create/update repository-level backend validation that can execute in CI.

Include, where supported:

* formatting;
* linting;
* type checking;
* unit tests;
* integration tests;
* migration validation;
* API contract validation;
* event contract validation;
* dependency/security scanning.

Do not build an entire cloud CI/CD platform in this prompt.

Create the repository-level validation necessary for future infrastructure pipelines.

---

# 47. TEST ENVIRONMENT SUPPORT

Improve backend tests so they can run deterministically.

Where appropriate provide:

* isolated test configuration;
* test database handling;
* migration setup;
* test data factories;
* Redis test setup;
* event/queue test adapters;
* cleanup.

Do not make tests depend on a developer's production credentials.

---

# 48. FAILURE-INJECTION SUPPORT

Where practical, create test seams for:

* database failure;
* Redis failure;
* event failure;
* queue failure;
* search failure;
* external-provider failure.

Do not build a complete chaos-engineering platform.

The goal is deterministic resilience testing of critical backend paths.

---

# 49. RETRY-SAFETY REVIEW

Review all existing retry paths.

Identify operations where retries could create duplicate:

* account creation;
* relationships;
* content;
* engagement;
* messages;
* notifications;
* moderation actions;
* analytics events.

Ensure retry-sensitive mutations have idempotency or safe transaction semantics.

---

# 50. OUTBOX/INBOX RELIABILITY REVIEW

Review event publication and consumption mechanisms.

Where an outbox exists:

* verify atomicity with the source transaction;
* verify retry;
* verify cleanup;
* verify observability.

Where consumer idempotency exists:

* identify the deduplication key;
* bound retention;
* handle duplicates safely.

Do not introduce a second competing outbox implementation.

---

# 51. CROSS-DOMAIN INTEGRATION REVIEW

Verify integration among:

* identity;
* social graph;
* content;
* media;
* engagement;
* feed;
* discovery;
* messaging;
* notifications;
* moderation;
* administration;
* analytics.

Check that:

* entity identifiers match;
* timestamps match;
* authorization semantics match;
* event names match;
* event versions match;
* API errors match;
* pagination matches;
* configuration names match.

Correct concrete incompatibilities found within this scope.

---

# 52. DATA CONSISTENCY REVIEW

Review derived data such as:

* counters;
* feed candidates;
* search documents;
* notification aggregates;
* realtime state;
* analytics ingestion state.

Verify each has:

* authoritative source;
* update mechanism;
* failure behavior;
* reconciliation strategy where required.

Do not allow derived data to silently become authoritative.

---

# 53. PERFORMANCE REVIEW

Instrument and review:

* API latency;
* database latency;
* cache latency;
* search latency;
* event latency;
* queue latency;
* realtime operations;
* feed retrieval;
* messaging;
* notifications.

Identify high-risk N+1 queries.

Identify unbounded loops.

Identify unbounded payloads.

Identify likely database hot spots.

Do not perform broad rewrites solely for theoretical future scale.

---

# 54. CONNECTION MANAGEMENT REVIEW

Review:

* PostgreSQL pool configuration;
* Redis connections;
* event-stream connections;
* queue workers;
* OpenSearch clients;
* WebSocket connections.

Ensure resources are:

* bounded;
* reused appropriately;
* closed gracefully;
* observable.

Avoid per-request client creation for long-lived dependencies.

---

# 55. MEMORY SAFETY

Review backend code for:

* unbounded arrays;
* unbounded cache values;
* full-table reads;
* large event payloads;
* large API responses;
* unbounded worker concurrency;
* large in-memory aggregation.

Use streaming/batching/pagination where appropriate.

Do not load entire high-volume datasets into memory.

---

# 56. SECURITY-SAFE OBSERVABILITY

Ensure observability itself does not become a privacy/security vulnerability.

Review:

* logs;
* traces;
* metrics;
* error tracking;
* debug endpoints;
* diagnostic endpoints.

Remove or redact sensitive user content where unnecessary.

---

# 57. OPERATIONAL RUNBOOKS

Create concise operational documentation covering:

* backend startup failure;
* database unavailable;
* Redis unavailable;
* queue backlog;
* event lag;
* search unavailable;
* realtime degradation;
* notification backlog;
* media-processing backlog;
* authentication degradation.

Runbooks should describe:

* symptoms;
* relevant telemetry;
* safe diagnostics;
* likely causes;
* recovery actions;
* escalation boundaries.

Do not document commands that require credentials unavailable to the execution environment.

---

# 58. CONFIGURATION VALIDATION

Review all backend configuration.

Ensure:

* required values are validated;
* optional values have safe defaults;
* invalid values fail startup;
* environment-specific behavior is explicit;
* secret values are not printed;
* configuration names are consistent across applications/workers.

Do not silently accept malformed configuration.

---

# 59. DEPLOYMENT-SAFE BACKEND CHANGES

Ensure cross-cutting changes are compatible with rolling deployments.

Avoid introducing:

* schema changes that require every instance to deploy simultaneously;
* event versions that break mixed-version consumers;
* API changes that break current clients.

Where changes require ordering, document the deployment order.

---

# 60. BACKWARD COMPATIBILITY REVIEW

Review:

* API versions;
* error codes;
* event versions;
* database migrations;
* realtime event envelopes;
* message schemas;
* notification schemas.

Do not casually rename shared fields.

Where a breaking change is genuinely required, document the migration path.

---

# 61. RATE-LIMIT POLICY REVIEW

Audit the rate-limit configuration across backend domains.

Ensure there are controls for high-risk operations without creating unreasonable restrictions for legitimate use.

Review:

* account creation;
* login;
* password recovery;
* relationships;
* content creation;
* engagement;
* feed;
* search;
* messaging;
* notifications;
* moderation;
* analytics.

Keep thresholds centrally configurable.

---

# 62. RESOURCE QUOTA REVIEW

Implement or document configurable limits for:

* request payloads;
* batch sizes;
* comments;
* attachments;
* message payloads;
* search result size;
* background-job concurrency;
* media metadata;
* API pagination.

Prevent a single request from consuming disproportionate resources.

---

# 63. BACKEND INTEGRATION CHECKS

Create integration checks that verify major runtime boundaries.

At minimum validate, where environment support exists:

* API → PostgreSQL;
* API → Redis;
* API → event publisher;
* worker → database;
* worker → queue;
* search integration;
* realtime infrastructure;
* notification integration boundary;
* object-storage boundary.

Do not require unavailable external production services for local CI tests.

---

# 64. CONTRACT COMPATIBILITY TESTING

Where possible, add tests that ensure:

* frontend-consumable API schemas remain stable;
* mobile-consumable API schemas remain stable;
* event consumers accept published event versions;
* realtime envelopes match server contracts;
* notification schemas remain compatible.

Do not require the web or mobile clients to be implemented for contract-level validation.

---

# 65. FAILURE TESTING

Add deterministic tests for critical degraded scenarios:

* Redis timeout;
* database timeout;
* event publication failure;
* queue failure;
* search failure;
* notification provider failure.

Verify:

* correct fallback;
* correct error;
* correct telemetry;
* no silent data loss.

---

# 66. PERFORMANCE REGRESSION GUARDRAILS

Add reasonable backend checks to catch regressions in:

* pagination;
* query counts;
* request latency;
* payload sizes;
* connection usage.

Do not turn development CI into an unreliable benchmark suite.

Only enforce performance thresholds that can run deterministically in the repository's test environment.

---

# 67. DOCUMENTATION

Update or create:

* backend operational guide;
* observability guide;
* resilience guide;
* configuration guide;
* CI validation guide;
* API contract validation guide;
* event contract validation guide;
* troubleshooting runbooks;
* security-hardening documentation;
* performance considerations.

Documentation must describe the actual repository implementation.

---

# 68. PORTABLE CONTRACTS

Maintain/update portable contracts for:

* error structure;
* correlation IDs;
* observability fields;
* configuration;
* resilience behavior;
* API validation;
* event validation;
* operational health;
* dependency behavior.

These contracts must be usable by infrastructure and QA engineers without relying on this conversation.

---

# 69. CROSS-PART COMPATIBILITY

Preserve compatibility with:

* web;
* mobile;
* backend domains;
* infrastructure;
* QA;
* monitoring/observability;
* external integrations.

Do not introduce backend-only conventions that client teams cannot consume.

Do not require production cloud resources merely to run repository-level contract validation.

---

# 70. NO FAKE COMPLETENESS

Do not:

* claim distributed tracing is operational when only configuration exists;
* claim production alerts exist when only metric instrumentation exists;
* claim cloud infrastructure is provisioned;
* fabricate load-test results;
* fabricate chaos-test results;
* create fake external integrations;
* use placeholder resilience behavior for current scope;
* leave TODO/FIXME gaps for required hardening;
* claim a dependency is highly available without actual infrastructure supporting it.

Implement the actual repository-level behavior covered by this prompt.

---

# 71. VALIDATION

Before completion:

1. run formatting;
2. run linting;
3. run type checking;
4. run unit tests;
5. run integration tests;
6. run API/contract validation;
7. run event-schema validation;
8. run migration validation;
9. run security/dependency scans available in the repository;
10. run failure-oriented tests;
11. run relevant performance/regression checks;
12. validate configuration;
13. validate health/readiness behavior;
14. validate documentation links or generated artifacts where tooling permits.

If an external environment is unavailable, clearly distinguish repository-level validation from unavailable infrastructure validation.

Do not claim validation that was not performed.

---

# 72. IMPLEMENTATION REPORT

After implementation, provide a completion report containing:

## Files Created

List every file created.

## Files Modified

List every file modified.

## Files Deleted

List every file deleted, if any.

## Platform Hardening Implemented

Summarize:

* request context;
* logging;
* metrics;
* tracing;
* health;
* shutdown;
* timeouts;
* retries;
* rate limiting;
* resilience.

## Database/Cache Hardening

Summarize:

* pool behavior;
* query protections;
* Redis behavior;
* cache safeguards.

## Event/Queue Hardening

Summarize:

* retries;
* idempotency;
* dead letters;
* worker behavior;
* observability.

## Security Hardening

Summarize:

* secret handling;
* request protections;
* authorization review;
* dependency security;
* logging redaction.

## Contract Validation

Summarize:

* API contracts;
* event contracts;
* generated specifications;
* CI checks.

## Tests Created

List test categories.

## Tests Executed

State exactly which tests were executed.

## Validation Performed

State exact validation performed.

## Operational Documentation

List runbooks and operational documentation created/updated.

## Integration Considerations

Explain how the hardened backend interfaces with web, mobile, infrastructure, and QA.

## Compatibility Considerations

Identify compatibility-sensitive changes.

## Known Limitations

List genuine limitations.

## Unresolved Issues

List only issues that remain unresolved.

---

# 73. DEFINITION OF DONE

This backend milestone is complete only when:

* request/correlation context is standardized;
* structured logging is implemented;
* sensitive log fields are redacted;
* tracing is implemented where supported;
* operational metrics are implemented;
* health/readiness/liveness behavior is consistent;
* graceful shutdown is implemented;
* timeout policies exist;
* retry policies exist;
* circuit breaking exists where justified;
* database pools are bounded;
* Redis failure behavior is explicit;
* cache safety is reviewed;
* event resilience is implemented;
* worker resilience is implemented;
* queue observability exists;
* centralized rate limiting is implemented;
* request-size protections exist;
* security middleware is hardened;
* secret handling is secure;
* backend dependency security checks are integrated where supported;
* API contract validation exists;
* event contract validation exists;
* CI-level backend validation exists;
* deterministic test infrastructure exists;
* failure-oriented tests exist;
* performance/regression guardrails exist where practical;
* operational runbooks exist;
* backend integration contracts are consistent;
* no secret values are committed;
* no fake operational claims are made;
* no intentional implementation gaps remain inside the defined scope.

---

# 74. FINAL IMPLEMENTATION DISCIPLINE

Implement **only the current prompt's scope**.

Do not implement:

* new product features;
* web UI;
* mobile UI;
* cloud infrastructure provisioning;
* Kubernetes deployment;
* a full CI/CD cloud platform;
* data warehouse infrastructure;
* full chaos engineering;
* new recommendation algorithms;
* new moderation models.

Do not redesign domain functionality unnecessarily.

Do not assume another AI prompt has been executed.

Do not depend on another AI conversation.

Do not claim production availability, cloud provisioning, or operational performance without actual infrastructure and validation.

Produce real, tested, documented backend hardening and operational integration for the Instagram backend.
