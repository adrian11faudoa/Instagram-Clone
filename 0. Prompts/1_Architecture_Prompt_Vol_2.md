# Instagram — Architecture Prompt — Volume 2

# 1. ROLE

You are the **Principal Architect and senior architecture team** responsible for defining the detailed technical contracts and implementation-facing architectural specifications for the **Instagram** project.

Operate with the combined responsibilities of:

* Principal Architect
* Backend Architect
* Distributed Systems Architect
* Database Architect
* API Architect
* Realtime Systems Architect
* Media Systems Architect
* Security Architect
* Privacy Architect
* Cloud Architect
* SRE / Reliability Architect
* Data / Analytics Architect
* QA Architect
* Technical Writer

This is an **architecture and contract-definition assignment**.

Do not implement the complete Instagram application in this task.

Do not treat architecture documentation as a substitute for runtime implementation.

Create the detailed, portable artifacts needed for independently generated backend, web, mobile, infrastructure, and QA work to remain compatible when later assembled by a final integration environment.

---

# 2. PROJECT IDENTITY

**Project Name:** Instagram

**Product Type:** Production-grade visual social networking platform.

**Primary Product Model:** A large-scale social platform centered on identity, social graph, visual media, short-form video, stories, personalized feeds, discovery, engagement, direct messaging, notifications, moderation, and creator/professional capabilities.

The completed system is architected toward approximately:

* 100 million registered accounts;
* 20 million daily active users;
* 2 million peak concurrent active sessions;
* approximately 100,000 sustained API requests per second across the platform;
* approximately 250,000 requests per second during peak edge bursts;
* high-volume media ingestion and delivery;
* very high social-graph fan-out;
* large realtime workloads;
* geographically distributed traffic;
* multi-region resilience where justified.

These are architectural target conditions.

They do not require this task to provision, deploy, or implement the complete production platform.

---

# 3. CURRENT ARCHITECTURE ASSIGNMENT

Create the **detailed contract and operational architecture layer** for Instagram.

This volume must establish the concrete rules that implementation teams will use when implementing the system.

The artifacts must resolve ambiguities around:

* identifiers;
* timestamps;
* API contracts;
* errors;
* pagination;
* authentication;
* sessions;
* authorization;
* privacy;
* relationships;
* posts;
* stories;
* short-form video;
* engagement;
* feeds;
* discovery;
* media;
* messaging;
* notifications;
* events;
* queues;
* caching;
* configuration;
* environments;
* reliability;
* deployment;
* disaster recovery;
* observability;
* security;
* cross-part integration.

The artifacts produced by this prompt must be portable.

They must not require access to this conversation to be understood.

---

# 4. REPOSITORY INSPECTION

If a repository is available:

1. Inspect the current repository structure.
2. Inspect all architecture documentation that actually exists.
3. Inspect existing schemas.
4. Inspect existing API specifications.
5. Inspect existing configuration contracts.
6. Inspect existing event definitions.
7. Inspect existing queue definitions.
8. Inspect database migrations.
9. Inspect existing application modules.
10. Inspect existing infrastructure definitions.
11. Inspect tests and validation tooling.
12. Identify concrete implementation constraints already present.

Treat repository state as authoritative for what actually exists.

Do not assume a prior AI response exists.

Do not assume another Claude conversation exists.

Do not assume any architecture document exists unless it is present in the repository or explicitly supplied.

When compatible architectural artifacts already exist, extend or refine them without silently creating incompatible duplicate contracts.

When a repository artifact conflicts with this prompt, determine whether the conflict is an actual implementation constraint or an incorrect/incomplete contract. Resolve it explicitly within this scope and document the decision.

---

# 5. TECHNOLOGY BASELINE

The architecture must remain compatible with the following project-wide technology direction unless the repository contains a concrete compatibility constraint requiring an equivalent alternative:

* TypeScript;
* Next.js / React for web;
* React Native for mobile;
* Node.js / TypeScript backend;
* NestJS or equivalent structured backend framework;
* PostgreSQL for transactional relational data;
* Redis for cache and ephemeral coordination;
* Kafka or compatible durable event streaming;
* durable job-queue infrastructure;
* OpenSearch or equivalent search infrastructure;
* Amazon S3 or compatible object storage;
* CloudFront or equivalent CDN;
* FFmpeg or equivalent media processing;
* AWS as the default cloud target;
* infrastructure as code.

Do not invent technology merely because it could be useful.

Every major platform dependency must have a clearly defined responsibility.

---

# 6. REQUIRED ARTIFACT SET

Create or update a portable contract set under an appropriate architecture documentation hierarchy.

At minimum create:

1. `docs/architecture/contracts/01-identifier-and-time-model.md`
2. `docs/architecture/contracts/02-api-contract.md`
3. `docs/architecture/contracts/03-error-and-status-contract.md`
4. `docs/architecture/contracts/04-pagination-and-list-contract.md`
5. `docs/architecture/contracts/05-idempotency-contract.md`
6. `docs/architecture/contracts/06-authentication-and-session-contract.md`
7. `docs/architecture/contracts/07-authorization-and-privacy-contract.md`
8. `docs/architecture/contracts/08-social-graph-contract.md`
9. `docs/architecture/contracts/09-content-contract.md`
10. `docs/architecture/contracts/10-story-and-short-video-contract.md`
11. `docs/architecture/contracts/11-engagement-contract.md`
12. `docs/architecture/contracts/12-feed-contract.md`
13. `docs/architecture/contracts/13-discovery-and-search-contract.md`
14. `docs/architecture/contracts/14-media-contract.md`
15. `docs/architecture/contracts/15-messaging-and-realtime-contract.md`
16. `docs/architecture/contracts/16-notification-contract.md`
17. `docs/architecture/contracts/17-event-contract.md`
18. `docs/architecture/contracts/18-queue-and-job-contract.md`
19. `docs/architecture/contracts/19-cache-contract.md`
20. `docs/architecture/contracts/20-configuration-contract.md`
21. `docs/architecture/contracts/21-observability-contract.md`
22. `docs/architecture/contracts/22-reliability-and-failure-contract.md`
23. `docs/architecture/contracts/23-security-and-audit-contract.md`
24. `docs/architecture/contracts/24-data-lifecycle-and-deletion-contract.md`
25. `docs/architecture/contracts/25-administration-and-moderation-contract.md`
26. `docs/architecture/contracts/26-analytics-event-contract.md`
27. `docs/architecture/contracts/27-external-integration-contract.md`
28. `docs/architecture/contracts/28-deployment-and-environment-contract.md`
29. `docs/architecture/contracts/29-cross-part-contract-matrix.md`

You may create additional artifacts where the architecture genuinely requires them.

Do not create documents that merely restate the same content without adding engineering value.

---

# 7. IDENTIFIER AND TIME CONTRACT

Create a single project-wide contract covering:

* internal entity IDs;
* externally exposed IDs;
* event IDs;
* message IDs;
* media IDs;
* session IDs;
* request/correlation IDs;
* idempotency keys;
* pagination cursors;
* moderation-case IDs;
* analytics event IDs.

Define:

* format;
* generation strategy;
* uniqueness expectations;
* ordering expectations;
* serialization;
* allowed character representation;
* client visibility;
* logging representation;
* database representation.

Choose a strategy appropriate for distributed systems and high-scale workloads.

Do not introduce different ID systems for different domains without an explicit reason.

Define canonical timestamp behavior for:

* `createdAt`;
* `updatedAt`;
* `deletedAt`;
* `publishedAt`;
* `expiresAt`;
* `processedAt`;
* `occurredAt`;
* `receivedAt`.

Define:

* timezone behavior;
* precision;
* serialization;
* clock-source expectations;
* client/server authority.

Server-side timestamps must be authoritative for business state.

---

# 8. API CONTRACT

Create the project's API contract.

Define:

* API style;
* base path conventions;
* versioning;
* resource naming;
* HTTP methods;
* content types;
* authentication headers or credential transport;
* request IDs;
* correlation IDs;
* validation;
* serialization;
* response envelope conventions where applicable;
* status codes;
* error representation;
* pagination;
* idempotency;
* rate limiting;
* conditional requests where applicable;
* caching semantics where applicable.

Establish a canonical resource naming vocabulary.

At minimum cover the conceptual API areas:

* auth;
* accounts;
* profiles;
* relationships;
* posts;
* stories;
* short-form video;
* comments;
* likes;
* saves;
* shares;
* feed;
* discovery;
* search;
* messaging;
* notifications;
* media;
* moderation;
* administration;
* analytics.

Do not invent every endpoint in this artifact unless necessary for defining a contract.

The API architecture must, however, establish enough concrete rules that later implementation prompts can create endpoints without independently inventing conventions.

---

# 9. ERROR AND STATUS CONTRACT

Define the canonical error model.

Every API error must have an explicit machine-readable structure.

Define fields such as:

* error code;
* human-readable message;
* request/correlation ID;
* field-level validation details where applicable;
* retryability;
* metadata where appropriate.

Define standard categories for:

* authentication errors;
* authorization errors;
* validation errors;
* not-found errors;
* conflict errors;
* rate-limit errors;
* idempotency conflicts;
* dependency failures;
* internal errors;
* unavailable services;
* moderation restrictions;
* privacy restrictions.

Define which failures are safe to expose to clients and which must remain internal.

Never expose stack traces, secrets, internal credentials, or sensitive infrastructure details.

---

# 10. PAGINATION CONTRACT

Define one canonical pagination model for list APIs.

Prefer cursor-based pagination for high-volume resources.

Define:

* cursor encoding;
* cursor contents;
* cursor expiration behavior;
* sort ordering;
* stable traversal;
* forward/backward behavior if supported;
* page-size limits;
* default limits;
* maximum limits;
* duplicate handling;
* deleted-item behavior;
* authorization filtering;
* stale-cursor handling.

Establish rules for pagination of:

* followers;
* following;
* posts;
* comments;
* feed entries;
* search results;
* conversations;
* messages;
* notifications;
* moderation queues.

Do not use offset pagination for workloads where large offsets would create an unacceptable scaling problem.

---

# 11. IDEMPOTENCY CONTRACT

Define idempotency behavior for mutation operations that may be retried.

Identify operations where idempotency is required, including as appropriate:

* content publication;
* media finalization;
* follow/unfollow transitions;
* engagement mutations;
* message sending;
* notification commands;
* moderation actions;
* administrative operations;
* external provider requests.

Define:

* idempotency-key format;
* scope;
* retention;
* collision handling;
* replay behavior;
* response reuse;
* conflict behavior;
* storage;
* cleanup.

Do not assume network retries are rare.

Do not require exactly-once processing when at-least-once delivery plus idempotency is more realistic.

---

# 12. AUTHENTICATION AND SESSION CONTRACT

Define:

* registration;
* login;
* logout;
* password reset;
* email/phone verification;
* session creation;
* session rotation;
* refresh behavior;
* device registration;
* session revocation;
* suspicious-session handling;
* optional MFA;
* account lockout/rate-limit behavior.

Define the responsibility of:

* identity subsystem;
* credential service;
* session store;
* API gateway;
* client applications.

Define:

* access credential lifetime;
* refresh/session lifetime;
* revocation behavior;
* rotation rules;
* device binding where appropriate.

Web and mobile clients must not use incompatible authentication models without a documented reason.

---

# 13. AUTHORIZATION AND PRIVACY CONTRACT

Create a concrete authorization model.

Define authorization for:

* public profiles;
* private profiles;
* posts;
* stories;
* short-form video;
* comments;
* media;
* saved content;
* followers/following;
* messaging;
* moderation;
* administration.

Define decision inputs such as:

* authenticated principal;
* account status;
* resource ownership;
* relationship state;
* privacy state;
* content visibility;
* block relationship;
* mute relationship;
* restriction relationship;
* moderation state;
* administrative role;
* platform policy state.

Define the authoritative authorization boundary.

Client-side state must never be treated as authoritative authorization.

Derived caches, feed entries, search indexes, notifications, and realtime events must not bypass authorization.

---

# 14. ACCOUNT AND PROFILE CONTRACT

Define canonical account/profile semantics.

Establish entities and relationships for:

* account;
* profile;
* username;
* display name;
* biography;
* avatar;
* profile links;
* account type;
* privacy state;
* account lifecycle state.

Define allowed states such as:

* active;
* restricted;
* suspended;
* deleted;
* pending verification where applicable.

Define username rules:

* uniqueness;
* normalization;
* case handling;
* allowed characters;
* change behavior;
* reservation;
* historical references.

Do not allow clients to establish uniqueness independently.

---

# 15. SOCIAL GRAPH CONTRACT

Define canonical semantics for:

* follow;
* unfollow;
* follow request;
* approve;
* reject;
* block;
* unblock;
* mute;
* unmute;
* restrict;
* unrestrict.

For each relationship define:

* source;
* target;
* ownership;
* state;
* creation;
* mutation;
* deletion;
* authorization effects;
* event behavior;
* notification behavior.

Define how relationship state affects:

* profile visibility;
* content eligibility;
* messaging;
* feed construction;
* notifications;
* search/discovery.

Explicitly define high-fan-out behavior.

Avoid designs that require scanning an entire relationship graph synchronously during ordinary user requests.

---

# 16. CONTENT CONTRACT

Create the canonical content model.

Cover:

* posts;
* post media;
* captions;
* mentions;
* hashtags;
* visibility;
* publication state;
* edits;
* deletions;
* moderation state;
* ownership;
* creation/publication timestamps.

Define content states such as:

* draft;
* processing;
* published;
* restricted;
* removed;
* deleted.

Clarify whether each state is:

* client-visible;
* API-visible;
* searchable;
* feed-eligible;
* shareable.

Define content ownership and lifecycle.

Do not allow a deleted or restricted item to remain eligible for newly generated feeds.

---

# 17. STORY AND SHORT-FORM VIDEO CONTRACT

Create detailed contracts for:

## Stories

Define:

* story;
* story item;
* ordering;
* expiration;
* audience;
* visibility;
* views;
* interactions;
* replies where supported;
* deletion;
* expiration cleanup.

## Short-Form Video

Define:

* video asset;
* processing state;
* derivatives;
* duration;
* dimensions;
* playback representations;
* thumbnail;
* visibility;
* moderation status;
* recommendation eligibility.

Define how each media type interacts with the general media contract.

Do not duplicate media lifecycle rules inconsistently between posts, stories, and short-form video.

---

# 18. ENGAGEMENT CONTRACT

Define canonical behavior for:

* likes;
* comments;
* comment replies;
* saves;
* shares;
* mentions;
* hashtags.

For each operation define:

* request identity;
* authorization;
* persistence;
* duplicate behavior;
* idempotency;
* event emission;
* notification effects;
* counter effects;
* deletion behavior.

Define counter semantics.

Distinguish:

* authoritative relationship state;
* exact counts where required;
* eventually consistent counters.

Avoid hot-row update strategies that cannot scale to highly popular content.

---

# 19. FEED CONTRACT

Define the canonical feed entry model.

A feed entry must identify, as appropriate:

* viewer;
* source/candidate;
* content;
* ranking metadata;
* generation timestamp;
* eligibility state;
* expiry/staleness state.

Define:

* candidate generation;
* ranking inputs;
* eligibility rules;
* privacy filtering;
* block filtering;
* mute filtering;
* moderation filtering;
* freshness;
* deduplication;
* pagination;
* cache behavior.

Define how feed entries react to:

* content deletion;
* privacy changes;
* blocking;
* account suspension;
* moderation decisions.

Feed materialization must never become a second source of truth for content ownership or privacy.

---

# 20. DISCOVERY AND SEARCH CONTRACT

Define contracts for:

* user search;
* username search;
* hashtag search;
* content discovery;
* search suggestions;
* recommended accounts;
* recommended content.

For each search representation define:

* source of truth;
* index owner;
* indexing trigger;
* deletion trigger;
* expected consistency;
* searchable fields;
* authorization filtering;
* moderation filtering;
* reindexing.

Search results must never expose content or accounts that are no longer eligible for the requesting principal.

---

# 21. MEDIA CONTRACT

Define the canonical `MediaAsset` and derivative model.

Every media record must establish, as appropriate:

* owner;
* asset ID;
* object storage location;
* media type;
* MIME type;
* byte size;
* dimensions;
* duration;
* processing state;
* moderation state;
* visibility;
* derivative relationships;
* created time;
* deletion state.

Define lifecycle states such as:

* uploaded;
* validating;
* scanning;
* processing;
* ready;
* failed;
* restricted;
* deleted.

Define upload behavior:

* pre-signed upload;
* upload validation;
* finalization;
* ownership verification;
* size validation;
* type validation;
* security scanning.

Define delivery behavior:

* CDN;
* signed URLs where appropriate;
* authorization;
* cache behavior;
* expiration;
* deletion propagation.

---

# 22. MEDIA PROCESSING CONTRACT

Define media jobs for:

* image normalization;
* thumbnail generation;
* video transcoding;
* video thumbnail generation;
* metadata extraction;
* content scanning;
* derivative creation.

For every job define:

* input;
* output;
* state transition;
* retry behavior;
* idempotency;
* failure state;
* dead-letter behavior;
* observability;
* maximum retry assumptions.

Define what happens when:

* processing succeeds;
* processing fails permanently;
* media is deleted while processing;
* moderation blocks the asset during processing.

Avoid orphaned media derivatives.

---

# 23. MESSAGING AND REALTIME CONTRACT

Define canonical contracts for:

* conversation;
* participant;
* message;
* message attachment;
* delivery state;
* read state;
* typing;
* presence where supported.

Define message states such as:

* accepted;
* persisted;
* delivered;
* read;
* failed;
* deleted where applicable.

Establish:

* message IDs;
* conversation IDs;
* sequencing;
* client-generated identifiers;
* idempotency;
* ordering;
* realtime event envelope;
* acknowledgement;
* reconnection;
* synchronization.

Explicitly separate:

**durable persistence**

from:

**realtime transport**

A WebSocket acknowledgement must not be treated as proof of durable persistence unless the contract explicitly guarantees the persistence state it represents.

---

# 24. OFFLINE SYNCHRONIZATION CONTRACT

Define how clients recover from:

* intermittent connectivity;
* application restarts;
* expired sessions;
* realtime disconnections;
* duplicate delivery;
* missed events.

Establish:

* synchronization cursor;
* event sequence;
* replay window;
* gap detection;
* resynchronization;
* duplicate handling;
* conflict resolution;
* stale-client behavior.

The architecture must allow mobile clients to recover without requiring a complete local database reset for ordinary synchronization gaps.

---

# 25. NOTIFICATION CONTRACT

Define:

* notification identity;
* notification type;
* actor;
* recipient;
* related resource;
* aggregation key;
* timestamp;
* read state;
* delivery state;
* deep-link target.

Cover notifications generated by:

* follows;
* follow requests;
* likes;
* comments;
* mentions;
* shares;
* messages;
* story interactions;
* moderation/security events where appropriate.

Define:

* in-app persistence;
* push delivery;
* preference filtering;
* deduplication;
* aggregation;
* retry;
* expiration.

Notification delivery failure must not roll back the originating business operation.

---

# 26. EVENT CONTRACT

Define one canonical event envelope.

At minimum include conceptual fields for:

* event ID;
* event type;
* event version;
* occurred-at timestamp;
* producer;
* entity/resource ID;
* correlation ID;
* causation ID where useful;
* schema version;
* payload;
* metadata.

Define naming conventions.

Define event versioning.

Define compatibility expectations.

Define whether events are:

* durable;
* replayable;
* ordered only within a partition/key;
* best-effort;
* authoritative;
* derived.

Do not allow a client-facing API response to depend on an event consumer completing successfully unless explicitly required.

---

# 27. CORE DOMAIN EVENTS

Establish canonical event names or event-name conventions for important lifecycle changes.

Cover events conceptually corresponding to:

* account created;
* account updated;
* account deleted;
* session created;
* session revoked;
* follow created;
* follow removed;
* follow request created;
* follow request resolved;
* block created;
* block removed;
* post published;
* post updated;
* post deleted;
* story published;
* story expired;
* short video published;
* comment created;
* comment deleted;
* like created;
* like removed;
* save created;
* save removed;
* share created;
* media uploaded;
* media processed;
* media failed;
* conversation created;
* participant changed;
* message persisted;
* message read;
* notification created;
* moderation decision applied.

Define producers and likely consumers at the architecture level.

---

# 28. QUEUE AND JOB CONTRACT

Define the canonical background-job envelope.

At minimum specify:

* job ID;
* job type;
* version;
* created time;
* scheduled time;
* attempt count;
* payload;
* correlation ID;
* priority where used.

Define:

* retry policy;
* exponential backoff;
* jitter;
* visibility timeout or lease behavior where relevant;
* maximum attempts;
* dead-letter handling;
* worker concurrency;
* cancellation;
* idempotency.

Define job classes for:

* media processing;
* notifications;
* search indexing;
* feed propagation;
* moderation;
* analytics;
* story expiration;
* cleanup;
* reconciliation.

Distinguish jobs from events.

---

# 29. CACHE CONTRACT

Define canonical Redis key namespaces.

At minimum establish conceptual namespaces for:

* rate limits;
* sessions where applicable;
* profiles;
* relationship lookups;
* feed pages;
* notification state;
* realtime ephemeral state.

Each cache contract must specify:

* key namespace;
* key components;
* TTL;
* source of truth;
* invalidation mechanism;
* maximum staleness;
* failure behavior.

Define what happens when Redis is unavailable.

No critical durable business state may exist only in cache unless explicitly justified and modeled as ephemeral state.

---

# 30. CONFIGURATION CONTRACT

Create a canonical configuration specification.

Separate:

**non-secret configuration**

from:

**secrets**

from:

**runtime-generated state**

from:

**infrastructure state**.

Define naming conventions for:

* environment variables;
* service configuration;
* feature flags;
* resource identifiers;
* provider configuration.

Define configuration categories for:

* database;
* Redis;
* Kafka;
* queues;
* object storage;
* CDN;
* search;
* authentication;
* external services;
* observability.

Never create example secrets resembling real credentials.

Use explicit placeholders only where a configuration example requires a non-secret illustrative value, and clearly distinguish it from real production configuration.

---

# 31. OBSERVABILITY CONTRACT

Define canonical telemetry fields:

* timestamp;
* severity;
* service/module;
* environment;
* request ID;
* correlation ID;
* trace ID;
* user-safe actor reference where permitted;
* operation;
* result;
* latency;
* error classification.

Define:

* log conventions;
* metric naming conventions;
* trace conventions;
* dashboard ownership;
* alert categories;
* SLI/SLO measurement boundaries.

Do not place sensitive content into logs.

Define telemetry behavior for:

* APIs;
* database operations;
* Redis;
* Kafka;
* queues;
* workers;
* realtime connections;
* media processing;
* search;
* CDN interactions where observable.

---

# 32. RELIABILITY AND FAILURE CONTRACT

Create standard reliability policies.

Define default expectations for:

* timeouts;
* retryability;
* retry limits;
* exponential backoff;
* jitter;
* circuit breaking;
* idempotency;
* graceful degradation;
* graceful shutdown.

Create dependency failure classifications for:

* transient;
* persistent;
* overload;
* authorization;
* validation;
* data corruption;
* unavailable;
* timeout.

For major dependencies, define:

* caller behavior;
* user-visible behavior;
* retry policy;
* fallback;
* telemetry;
* recovery.

Do not retry non-idempotent operations blindly.

---

# 33. DATA LIFECYCLE AND DELETION CONTRACT

Define data lifecycle rules for:

* accounts;
* profiles;
* posts;
* stories;
* short-form video;
* comments;
* relationships;
* messages;
* notifications;
* media;
* search indexes;
* feed projections;
* analytics;
* moderation records;
* audit records.

For deletion, establish:

* authoritative deletion;
* asynchronous propagation;
* cache invalidation;
* search deletion;
* media deletion;
* feed invalidation;
* event behavior;
* retention exceptions.

Distinguish:

* user-visible deletion;
* physical deletion;
* retention required for security/audit/compliance where applicable.

Do not claim jurisdiction-specific legal requirements unless they are explicitly part of the project requirements.

---

# 34. MODERATION AND ADMINISTRATION CONTRACT

Define canonical structures for:

* report;
* moderation case;
* moderation decision;
* enforcement action;
* administrative action;
* audit record.

Define:

* state transitions;
* actor roles;
* evidence references;
* target resource;
* reason codes;
* timestamps;
* reversibility;
* auditability.

Administrative actions must be authenticated, authorized, attributable, and auditable.

Define how moderation state propagates to:

* content;
* search;
* feed;
* notifications;
* media;
* user profiles.

---

# 35. ANALYTICS EVENT CONTRACT

Define a separate analytics event model.

Differentiate it from operational domain events.

Establish:

* event identity;
* event name;
* event schema version;
* actor/account reference;
* anonymous/session reference where appropriate;
* resource reference;
* timestamp;
* client/platform;
* source;
* properties.

Define:

* privacy boundaries;
* retention;
* sampling;
* ingestion;
* asynchronous processing.

Do not put passwords, tokens, message bodies, raw private content, or unnecessary sensitive data into analytics events.

---

# 36. EXTERNAL INTEGRATION CONTRACT

Define a common integration pattern for providers.

For each integration category specify:

* adapter boundary;
* authentication/configuration boundary;
* timeout;
* retry;
* idempotency;
* failure classification;
* observability;
* privacy considerations.

Cover likely categories:

* email;
* SMS;
* push notifications;
* object storage;
* CDN;
* search;
* moderation;
* observability;
* analytics.

Do not hardcode a provider-specific implementation where a boundary is sufficient.

Do not pretend provider connectivity exists without credentials and actual validation.

---

# 37. DEPLOYMENT AND ENVIRONMENT CONTRACT

Define environment expectations:

* local;
* test;
* development;
* staging;
* production.

For each, define:

* configuration source;
* secret source;
* telemetry expectations;
* database expectations;
* external integration mode;
* deployment strategy.

Define deployment principles for:

* stateless API services;
* realtime services;
* background workers;
* media processors;
* web applications;
* scheduled jobs.

Establish:

* rolling deployment expectations;
* backward compatibility;
* migration ordering;
* health checks;
* readiness;
* liveness;
* rollback.

---

# 38. DATABASE CONTRACT

Define project-wide database conventions for:

* table naming;
* column naming;
* primary keys;
* foreign keys;
* timestamps;
* soft-delete semantics where used;
* indexes;
* unique constraints;
* enums;
* JSON fields;
* migration naming;
* transaction boundaries.

Define when denormalization is acceptable.

Define how high-volume tables should be evaluated for:

* partitioning;
* archive/retention;
* hot-key patterns;
* index growth;
* write amplification.

Do not dictate one physical database topology for every future deployment if scaling conditions may require decomposition.

---

# 39. DATABASE TRANSACTION BOUNDARIES

Define transaction principles for key operations such as:

* account creation;
* follow state change;
* post publication state transition;
* comment creation;
* engagement mutation;
* message persistence;
* moderation enforcement.

Explicitly distinguish:

**must be atomic**

from:

**may be eventually consistent**.

Cross-domain asynchronous updates should not be forced into one giant distributed transaction.

Use durable events or outbox-style patterns where appropriate.

---

# 40. OUTBOX / EVENT PUBLICATION STRATEGY

Define how authoritative database mutations become durable domain events.

Establish whether and where an outbox pattern is appropriate.

Define:

* outbox ownership;
* transaction relationship;
* event persistence;
* publication;
* retries;
* deduplication;
* cleanup;
* replay;
* observability.

Prevent the following failure:

**database transaction succeeds → event silently disappears**

when the event is required for downstream correctness.

Also prevent:

**event published → database transaction rolled back**

from creating invalid downstream state.

---

# 41. HIGH-FAN-OUT DESIGN CONTRACT

Define architecture rules for accounts with unusually large follower counts.

Cover:

* feed fan-out;
* notifications;
* relationship changes;
* content propagation;
* cache invalidation;
* event volume;
* hot keys.

Define hybrid strategies where appropriate.

Do not force the system into a single fan-out model for every account.

---

# 42. HOT-KEY AND HOT-ROW PROTECTION

Identify potential hot resources such as:

* highly popular posts;
* major creator profiles;
* viral videos;
* popular hashtags;
* large follower relationships;
* engagement counters.

Define mitigation strategies including, where appropriate:

* sharded counters;
* asynchronous aggregation;
* cache replication;
* request coalescing;
* partitioning;
* rate limits;
* write distribution.

Do not use synchronous global counters for workloads where they would become a systemic bottleneck.

---

# 43. SECURITY CONTRACT MATRIX

Create a security matrix covering:

* authentication;
* authorization;
* input validation;
* output encoding;
* session management;
* token management;
* password storage;
* rate limiting;
* media upload security;
* SSRF;
* XSS;
* CSRF where applicable;
* injection;
* credential stuffing;
* bot abuse;
* secret management;
* service-to-service trust;
* admin access.

For each threat category document:

* affected boundary;
* primary control;
* secondary control;
* telemetry;
* failure behavior.

---

# 44. PRIVACY CONTRACT MATRIX

Create a matrix describing how privacy state propagates through:

* profile reads;
* feed generation;
* search;
* media delivery;
* notifications;
* messaging;
* cache;
* moderation;
* analytics.

Explicitly evaluate the following scenario:

**A user becomes private or blocks another user after derived data has already been created.**

Define which derived systems must invalidate, recalculate, or filter the old state.

---

# 45. CROSS-PART INTEGRATION CONTRACT

Create or update:

`docs/architecture/contracts/29-cross-part-contract-matrix.md`

This artifact is a central portability document.

It must map:

| Contract Area | Authoritative Owner    | Main Consumers                           | Source of Truth             | Consistency                    | Change/Version Strategy |
| ------------- | ---------------------- | ---------------------------------------- | --------------------------- | ------------------------------ | ----------------------- |
| Identity      | Identity domain        | Web, Mobile, Backend                     | Defined authoritative store | Strong/defined                 | Explicit                |
| Profile       | Account/Profile        | Web, Mobile, Feed, Search                | Defined authoritative store | Defined                        | Explicit                |
| Social Graph  | Social Graph           | Feed, Messaging, Profiles, Notifications | Defined authoritative store | Defined                        | Explicit                |
| Content       | Content domain         | Feed, Search, Media, Clients             | Defined authoritative store | Defined                        | Explicit                |
| Media         | Media domain           | Content, Clients, CDN                    | Object/media metadata model | Defined                        | Explicit                |
| Messaging     | Messaging domain       | Web, Mobile, Notifications               | Messaging persistence       | Defined                        | Explicit                |
| Events        | Event platform         | Consumers                                | Durable event stream        | Defined                        | Versioned               |
| Jobs          | Queue/workers          | Background systems                       | Job state/queue             | At-least-once where applicable | Versioned               |
| Configuration | Platform configuration | Runtime components                       | Configuration source        | Defined                        | Explicit                |
| Observability | Platform operations    | All production components                | Telemetry systems           | Eventual                       | Versioned               |

Expand the matrix with the real contracts created by this prompt.

Do not leave generic rows when a specific contract exists.

---

# 46. CONTRACT CHANGE MANAGEMENT

Define how future implementation work must handle a contract change.

For changes to:

* APIs;
* schemas;
* events;
* queues;
* database structures;
* authentication;
* authorization;
* realtime protocols;

require:

1. identify consumers;
2. determine backward compatibility;
3. determine migration needs;
4. update documentation;
5. update relevant tests;
6. define deployment ordering;
7. define rollback implications.

Do not silently break independent project parts.

---

# 47. APPROVAL AND DECISION POLICY

Do not make later implementation teams dependent on a human approval message in a Claude conversation.

Architectural decisions that matter to implementation must be represented in portable artifacts.

When an assumption remains provisional, label it explicitly within the artifact.

Do not fabricate approval history.

Do not state that a decision was "approved" unless the repository or supplied project documentation demonstrates that approval.

---

# 48. REQUIRED ARCHITECTURE CROSS-CHECK

Cross-check all newly created contracts against the project architecture.

Verify consistency among:

* domain boundaries;
* data ownership;
* API ownership;
* identifier model;
* timestamps;
* authentication;
* authorization;
* content;
* social graph;
* feed;
* discovery;
* media;
* messaging;
* notifications;
* events;
* queues;
* caching;
* configuration;
* infrastructure;
* observability;
* reliability.

Resolve contradictions before completion.

Do not preserve two competing definitions of the same contract.

---

# 49. FAILURE SCENARIO MATRIX

Create a failure scenario matrix covering at least:

* PostgreSQL unavailable;
* PostgreSQL read degradation;
* Redis unavailable;
* Kafka unavailable;
* job queue unavailable;
* search unavailable;
* object storage unavailable;
* CDN degradation;
* media processor unavailable;
* push provider unavailable;
* email/SMS provider unavailable;
* realtime infrastructure unavailable;
* worker crash;
* duplicate event delivery;
* duplicate job delivery;
* stale cache;
* deleted resource referenced by derived data.

For each scenario document:

* affected subsystem;
* expected behavior;
* retry;
* fallback;
* user impact;
* telemetry;
* recovery;
* data-consistency implications.

---

# 50. SECURITY AND PRIVACY REVIEW

Perform an architecture-level review for:

* privilege escalation;
* account takeover;
* unauthorized private-content access;
* cache authorization leaks;
* search privacy leaks;
* media URL abuse;
* realtime authorization leaks;
* notification privacy leaks;
* message exposure;
* administrative abuse;
* insecure file uploads;
* event payload leakage;
* telemetry leakage.

Document identified risks and architectural controls.

Do not claim that implementation-level security vulnerabilities have been eliminated because implementation has not yet been completed.

---

# 51. SCALE REVIEW

Evaluate each major subsystem against:

* normal load;
* peak load;
* high-fan-out load;
* high-write load;
* high-read load;
* concurrent connections;
* storage growth;
* bandwidth growth.

At minimum review:

* identity;
* social graph;
* content;
* feed;
* discovery;
* media;
* messaging;
* notifications;
* moderation;
* database;
* Redis;
* event streaming;
* queues.

Identify:

* likely bottlenecks;
* mitigation;
* scaling trigger;
* whether scaling is synchronous or asynchronous.

Do not claim the system has been load tested.

---

# 52. OPERATIONAL COST REVIEW

For major architecture choices, document the operational tradeoffs among:

* managed services;
* self-managed services;
* storage;
* database;
* cache;
* event streaming;
* queues;
* search;
* media processing;
* observability;
* CDN/bandwidth.

Avoid adding services whose operational and financial cost cannot be justified.

The objective is commercial realism, not maximal infrastructure complexity.

---

# 53. ARTIFACT QUALITY REQUIREMENTS

Every created artifact must:

* be self-contained;
* use canonical project terminology;
* identify authoritative ownership;
* identify derived state where applicable;
* identify consistency behavior;
* identify lifecycle behavior;
* identify failure behavior where relevant;
* identify security and privacy implications where relevant;
* be implementable by another engineering team;
* avoid undocumented dependencies;
* avoid pseudo-contracts;
* avoid vague future-work statements.

Do not write:

* "handle errors appropriately";
* "scale as needed";
* "use caching where useful";
* "secure the API";
* "process media asynchronously."

Instead define the actual intended contract and boundaries.

---

# 54. NO APPLICATION IMPLEMENTATION

This volume must not implement:

* complete backend modules;
* complete API controllers;
* complete web pages;
* complete mobile screens;
* complete database migrations;
* complete workers;
* complete media processing;
* complete search;
* complete realtime infrastructure;
* complete cloud infrastructure;
* complete QA suites.

Creating contract artifacts, schema definitions, interface specifications, diagrams, and architectural documentation is in scope.

Runtime implementation is not.

---

# 55. NO FAKE COMPLETENESS

Do not:

* create dummy production behavior;
* create fake third-party integrations;
* claim APIs are functional merely because contracts exist;
* claim infrastructure is deployed;
* claim external services are connected;
* claim load testing occurred;
* claim failover testing occurred;
* create implementation placeholders disguised as completed functionality.

Architecture artifacts must accurately describe intended system behavior.

---

# 56. VALIDATION REQUIREMENTS

Before completion, validate:

* markdown syntax where tooling permits;
* internal documentation links;
* duplicate contract names;
* duplicate entity names;
* conflicting API conventions;
* conflicting event conventions;
* identifier consistency;
* timestamp consistency;
* state-machine consistency;
* data ownership consistency;
* authorization consistency;
* privacy consistency;
* retry/idempotency consistency;
* event/job distinction;
* cache/source-of-truth distinction.

Where the repository contains schemas or contracts, compare them against the architecture artifacts.

Document any existing incompatibility that could not reasonably be resolved within this architecture task.

---

# 57. DOCUMENTATION STRUCTURE

Organize documentation so implementation teams can quickly find:

* identity rules;
* API rules;
* domain contracts;
* media rules;
* messaging rules;
* event rules;
* job rules;
* cache rules;
* security rules;
* reliability rules;
* deployment rules;
* integration matrix.

Avoid excessively large single documents when splitting produces clearer ownership.

Avoid hundreds of tiny documents without meaningful boundaries.

---

# 58. PORTABILITY REQUIREMENT

Every artifact created by this prompt must remain useful when copied into:

* another Claude conversation;
* a backend implementation workspace;
* a frontend implementation workspace;
* a mobile implementation workspace;
* an infrastructure workspace;
* a QA workspace;
* a final Codex integration environment.

Do not require the reader to know:

* what was discussed in this conversation;
* what another AI said;
* which prompt produced the artifact;
* which Claude conversation generated it.

The artifact itself must carry the necessary information.

---

# 59. IMPLEMENTATION HANDOFF MATRIX

Create a matrix assigning contracts to future engineering consumers.

At minimum identify:

* backend;
* web;
* mobile;
* infrastructure;
* QA;
* security;
* operations.

For each contract identify:

* primary consumer;
* secondary consumers;
* implementation sensitivity;
* testing implications;
* versioning sensitivity.

Do not make the matrix a project-management schedule.

Its purpose is contract ownership and integration visibility.

---

# 60. DEFINITION OF DONE

This architecture volume is complete only when:

* the project-wide identifier model is defined;
* timestamp semantics are defined;
* API conventions are concrete;
* error behavior is concrete;
* pagination is defined;
* idempotency is defined;
* authentication/session behavior is defined;
* authorization/privacy behavior is defined;
* account/profile contracts are defined;
* social graph semantics are defined;
* content contracts are defined;
* story and short-form video contracts are defined;
* engagement semantics are defined;
* feed contracts are defined;
* discovery/search contracts are defined;
* media contracts are defined;
* media processing contracts are defined;
* messaging/realtime contracts are defined;
* offline synchronization behavior is defined;
* notification contracts are defined;
* event envelopes and versioning are defined;
* queue/job semantics are defined;
* cache conventions are defined;
* configuration conventions are defined;
* observability contracts are defined;
* reliability/failure behavior is defined;
* data lifecycle/deletion behavior is defined;
* moderation and administration contracts are defined;
* analytics contracts are defined;
* external integration boundaries are defined;
* deployment/environment contracts are defined;
* database conventions are defined;
* transaction boundaries are defined;
* event publication strategy is defined;
* hot-key/high-fan-out behavior is defined;
* security and privacy matrices are created;
* cross-part contract matrix is complete;
* failure scenarios are documented;
* scalability has been architecturally reviewed;
* operational cost implications have been considered;
* validation has been performed;
* no contradictory contract definitions remain;
* no production secrets are present;
* no claims of runtime deployment or unperformed testing are made.

---

# 61. COMPLETION REPORT

After completing the architecture work, provide a completion report containing:

## Files Created

List every file created.

## Files Modified

List every file modified.

## Files Deleted

List every file deleted, if any.

## Contract Systems Established

Summarize:

* identity/time;
* API;
* errors;
* pagination;
* idempotency;
* auth;
* authorization;
* content;
* feed;
* media;
* messaging;
* notifications;
* events;
* queues;
* caching;
* configuration.

## Data and Lifecycle Decisions

Summarize ownership, consistency, deletion, retention, and derived-data behavior.

## Reliability and Failure Decisions

Summarize major timeout, retry, fallback, and degradation policies.

## Security and Privacy Decisions

Summarize major architectural boundaries and protections.

## Scalability Decisions

Summarize high-fan-out, hot-key, feed, messaging, media, search, and database decisions.

## Integration Contract

Summarize the portable cross-part contract and the engineering consumers it serves.

## Validation Performed

State exactly what was checked.

Do not claim runtime validation that was not performed.

## Repository Compatibility

State what repository artifacts were actually inspected and whether any existing implementation constraints affected the architecture.

## Known Limitations

List genuine remaining architectural limitations.

## Unresolved Issues

List only issues that truly remain unresolved after this task.

---

# 62. FINAL ARCHITECTURE DISCIPLINE

This prompt creates detailed architectural contracts.

It does not authorize implementation of the complete Instagram application.

Do not invent an additional architecture phase merely because further documentation could be created.

Do not create hidden dependencies on previous AI responses.

Do not create contracts that conflict with the system architecture.

Do not leave critical implementation-facing contracts implicit.

All major interfaces required for later independently generated project parts must be represented explicitly in portable artifacts.

The resulting contract set must be concrete enough that backend, web, mobile, infrastructure, QA, security, and final integration engineers can implement against the same definitions without relying on undocumented conversation history.
