# Instagram — Backend Prompt — Volume 2

# 1. ROLE

You are the **Staff Backend Engineering team** responsible for implementing the content, media, and publishing backend domains for the **Instagram** project.

Operate with the combined responsibilities of:

* Staff Backend Engineer
* Backend Architect
* Database Engineer
* Distributed Systems Engineer
* Media Systems Engineer
* Security Engineer
* Reliability Engineer
* Performance Engineer
* QA-minded Backend Engineer
* DevOps-aware Application Engineer

This is a **bounded backend implementation assignment**.

You must implement the real backend functionality defined by this prompt.

Do not implement unrelated future product areas merely because they appear in the global Instagram product vision.

The mandatory rule for this task is:

**Implement only the current prompt's scope.**

---

# 2. PROJECT IDENTITY

**Project Name:** Instagram

**Product Type:** Production-grade visual social networking platform.

The backend is part of a larger system containing:

* web client;
* mobile clients;
* PostgreSQL;
* Redis;
* asynchronous processing;
* event streaming;
* background jobs;
* object storage;
* CDN;
* search;
* feed infrastructure;
* messaging;
* notifications;
* moderation;
* administration;
* analytics.

The completed system is intended to support approximately:

* 100 million registered accounts;
* 20 million daily active users;
* 2 million peak concurrent active sessions;
* approximately 100,000 sustained API requests per second across the platform;
* approximately 250,000 requests per second during peak edge bursts.

These are global architectural targets.

This prompt implements only the **content publication, media-reference, stories, and short-form video foundation** defined below.

---

# 3. CURRENT BACKEND ASSIGNMENT

Implement the backend foundation for:

1. content/posts;
2. post media relationships;
3. captions;
4. mentions;
5. hashtags;
6. publication state;
7. content visibility;
8. content ownership;
9. content editing where supported;
10. content deletion;
11. stories;
12. story items;
13. story expiration;
14. short-form video/reels metadata and publication state;
15. media-asset metadata and lifecycle;
16. media-upload finalization;
17. asynchronous media-processing contracts and job initiation;
18. content/media authorization;
19. content lifecycle events;
20. database persistence and migrations;
21. Redis usage required for this scope;
22. tests;
23. documentation;
24. observability appropriate to this scope.

This prompt establishes the executable content/media backend foundation needed by later feed, discovery, engagement, notification, and moderation systems.

---

# 4. REPOSITORY INSPECTION

Before modifying or creating code, inspect the repository.

Inspect, where present:

* backend application structure;
* existing shared packages;
* configuration;
* database schema;
* migrations;
* authentication and authorization;
* account/profile modules;
* relationship services;
* event/outbox infrastructure;
* Redis integration;
* object-storage abstractions;
* existing media code;
* API conventions;
* error handling;
* testing infrastructure;
* documentation.

Treat the repository as the source of truth for actual implementation state.

Do not assume an earlier AI prompt was executed.

Do not assume another Claude conversation exists.

Do not fabricate files, modules, contracts, or infrastructure that are not actually available.

If the repository already contains compatible foundations required by this scope, extend them rather than creating duplicate implementations.

---

# 5. TECHNOLOGY BASELINE

Use:

* TypeScript;
* Node.js;
* the repository's existing structured backend framework;
* PostgreSQL;
* Redis where justified;
* object-storage integration behind an explicit provider boundary;
* durable background-job infrastructure already present or introduced where required by this prompt;
* REST APIs;
* strong request validation;
* structured logging;
* tracing/metrics where available;
* automated tests.

For media processing, use the project's selected media-processing abstraction and an implementation compatible with FFmpeg or an equivalent production-grade processor.

For object storage, use the project's selected S3-compatible abstraction.

Do not fabricate cloud credentials or claim actual cloud resources have been provisioned.

---

# 6. BOUNDED IMPLEMENTATION SCOPE

## In Scope

Implement:

* post creation;
* post retrieval;
* post update within supported editable fields;
* post deletion;
* post visibility;
* post publication state;
* post ownership;
* post-media associations;
* carousel/media ordering;
* captions;
* mentions;
* hashtags;
* story creation;
* story item creation and ordering;
* story retrieval;
* story expiration semantics;
* short-form video/reel metadata;
* video publication state;
* media asset records;
* media derivative references;
* media processing state;
* upload initialization/finalization;
* object-storage provider boundary;
* media-processing job initiation;
* media-processing result handling within the local domain;
* media lifecycle states;
* content/media authorization;
* deletion propagation hooks;
* content/media events;
* relevant cache behavior;
* relevant database schema and migrations;
* tests;
* observability;
* documentation.

## Out of Scope

Do not implement:

* feed generation or ranking;
* Explore/recommendation systems;
* search indexing;
* likes;
* comments;
* saves;
* shares;
* notifications;
* direct messaging;
* moderation workflow;
* full administrative tooling;
* creator analytics;
* recommendation models;
* complete CDN infrastructure;
* complete transcoding worker infrastructure if that belongs to a later infrastructure/media-processing milestone.

This prompt may create the contracts, records, job definitions, and integration boundaries required by those future systems, but it must not implement those domains.

---

# 7. CONTENT DOMAIN ARCHITECTURE

Create a clear content domain around:

* posts;
* post media;
* captions;
* mentions;
* hashtags.

Content ownership must belong to the content domain.

Media binary data must belong to the media/object-storage subsystem rather than the relational content record.

Do not embed media blobs in PostgreSQL.

Content records may reference media assets by canonical ID.

---

# 8. POST MODEL

Implement a production-grade post model.

A post must support, as appropriate:

* post ID;
* author account ID;
* caption;
* visibility;
* publication state;
* created time;
* updated time;
* published time;
* deleted time;
* moderation/content state integration field where appropriate;
* versioning or optimistic concurrency support where justified.

Do not implement a boolean-only model if explicit lifecycle states are required.

Define and enforce state transitions.

---

# 9. POST PUBLICATION STATES

Implement clear publication lifecycle states such as:

* draft;
* processing;
* published;
* restricted;
* deleted.

Use only states genuinely required by the implementation.

Define:

* allowed transitions;
* who can trigger transitions;
* what states are externally visible;
* what states are feed-eligible;
* what states are searchable;
* what states can be edited;
* what states can be deleted.

Do not allow an unpublished or deleted post to appear in ordinary user-facing content retrieval.

---

# 10. CONTENT VISIBILITY

Implement content visibility rules compatible with the account/privacy system.

The authorization decision must take into account, where applicable:

* caller identity;
* post author;
* account privacy state;
* relationship state;
* block state;
* content lifecycle state.

Do not rely on frontend filtering.

Do not assume that knowing a post ID grants access.

Create reusable authorization logic rather than duplicating visibility checks across controllers.

---

# 11. POST CREATION

Implement post creation.

The request flow must include:

1. authenticated-author verification;
2. input validation;
3. visibility validation;
4. media-reference validation;
5. caption validation;
6. mention validation;
7. hashtag extraction/validation;
8. persistence;
9. publication-state transition;
10. relevant event creation;
11. response generation.

Use a transaction for state that must become atomic.

Do not synchronously execute heavy media processing inside the post request.

---

# 12. MEDIA REFERENCES DURING POST CREATION

A post may reference only media assets that the authenticated account is authorized to attach.

Validate:

* media ownership;
* media lifecycle state;
* media processing state;
* allowed media type;
* media ordering;
* media count limits;
* asset compatibility with the post type.

Prevent one account from attaching another account's private/unowned media asset.

Do not trust client-provided media metadata when authoritative metadata already exists server-side.

---

# 13. CAROUSEL MEDIA ORDERING

Implement deterministic ordering for multiple media assets attached to a post.

Define:

* one canonical ordering field;
* uniqueness within a post;
* contiguous or validated ordering semantics;
* duplicate prevention;
* stable retrieval ordering.

A carousel must return media in the stored authoritative order.

Do not depend on database row-return order.

---

# 14. CAPTIONS

Implement caption handling.

Define:

* maximum length;
* normalization;
* empty-caption behavior;
* encoding expectations;
* update behavior;
* deletion behavior.

Store the canonical caption in the content domain.

Do not attempt to derive caption content from the client after persistence.

---

# 15. HASHTAGS

Implement hashtag extraction and association.

Define:

* normalization;
* canonical representation;
* case behavior;
* allowed syntax;
* maximum number per post;
* duplicate handling.

Store hashtag references in a way that later discovery/search systems can consume.

Do not implement search indexing here.

Create the authoritative hashtag relationships required by later indexing systems.

---

# 16. MENTIONS

Implement user mentions in captions.

Define:

* mentioned-account resolution;
* normalization;
* duplicate handling;
* nonexistent-user behavior;
* deleted/suspended-account behavior;
* authorization implications.

Persist canonical mention relationships separately from raw caption text.

Do not implement mention notifications yet.

Do create the event or integration hook necessary for future notification processing.

---

# 17. CONTENT UPDATE

Implement supported post updates.

Clearly define which fields are editable.

At minimum consider:

* caption;
* mentions;
* hashtags;
* visibility where policy permits.

Do not allow unauthorized mutation of:

* author;
* ownership;
* immutable publication identity;
* media identity unless the architecture explicitly supports media replacement.

Use optimistic concurrency or equivalent protection where concurrent updates could otherwise overwrite data silently.

---

# 18. CONTENT DELETION

Implement post deletion.

Deletion must:

* verify ownership/authorization;
* persist authoritative deletion state;
* prevent further ordinary retrieval;
* emit the relevant domain event;
* trigger asynchronous cleanup/invalidation hooks;
* prevent future feed eligibility;
* prevent future search eligibility.

Do not attempt to implement the entire downstream cleanup system.

Create the durable event/integration boundary required for later systems.

---

# 19. CONTENT RETRIEVAL

Implement retrieval for authorized callers.

Support:

* post by ID;
* authenticated author's own posts where appropriate;
* public content;
* private content when the caller has access.

Do not implement a full feed.

Do not expose internal storage locations unnecessarily.

Return canonical media references rather than internal object-storage implementation details.

---

# 20. CONTENT PAGINATION

Where post collections are exposed by this scope, use the project's cursor pagination contract.

Define:

* stable ordering;
* maximum page size;
* cursor validation;
* deleted-content behavior;
* privacy filtering;
* deterministic traversal.

Do not implement offset pagination for high-volume post collections.

---

# 21. STORY MODEL

Implement a story domain.

The model must support:

* story ID;
* author account ID;
* visibility/audience;
* creation time;
* expiration time;
* lifecycle state.

A story may contain ordered story items.

Do not treat each story item as an unrelated top-level content object.

---

# 22. STORY ITEM MODEL

Implement ordered story items supporting:

* media asset reference;
* position;
* creation time;
* optional per-item metadata needed by the product;
* processing state where necessary.

Define deterministic ordering.

Validate that each media asset is authorized for the story owner.

---

# 23. STORY EXPIRATION

Implement server-authoritative story expiration semantics.

Define the canonical expiration timestamp.

Ordinary story retrieval must exclude expired stories even if asynchronous cleanup has not yet run.

Do not depend exclusively on a background cleanup job for access control.

Create an asynchronous expiration job/event boundary for physical cleanup.

---

# 24. STORY RETRIEVAL

Implement appropriate story retrieval.

Cover:

* author access;
* viewer authorization;
* private-account rules;
* blocked relationships;
* expired stories;
* deleted stories.

Do not implement full story recommendation or ranking.

Do not implement story-view analytics in this scope unless required to establish persistence hooks; full view processing belongs to a later engagement milestone.

---

# 25. STORY LIFECYCLE EVENTS

Create events for relevant lifecycle changes such as:

* `story.created`;
* `story.published`;
* `story.deleted`;
* `story.expired`.

Events must use the project's canonical event envelope and versioning rules.

Do not introduce incompatible event payload formats.

---

# 26. SHORT-FORM VIDEO MODEL

Implement the backend domain foundation for short-form videos/reels.

Support metadata such as:

* video ID;
* author account ID;
* media asset ID;
* caption;
* visibility;
* publication state;
* duration;
* dimensions;
* thumbnail asset reference;
* processing status;
* creation/publication timestamps.

Do not implement recommendation/ranking.

Do not implement playback optimization algorithms.

Do not implement the feed.

---

# 27. VIDEO PUBLICATION STATES

Implement appropriate video lifecycle states.

Consider:

* draft;
* uploading;
* processing;
* ready;
* published;
* restricted;
* failed;
* deleted.

Only publish content when the required media state is satisfied.

A failed media-processing result must not silently become published content.

---

# 28. MEDIA ASSET MODEL

Implement the canonical media asset record needed by this scope.

Support:

* media asset ID;
* owner;
* media type;
* MIME type;
* storage object reference;
* size;
* dimensions;
* duration where applicable;
* processing state;
* visibility;
* deletion state;
* created time;
* processed time where applicable.

Do not store binary media content in PostgreSQL.

---

# 29. MEDIA DERIVATIVES

Support derivative metadata such as:

* thumbnail;
* normalized image;
* transcoded video;
* alternate resolution;
* preview representation.

Represent parent/child relationships explicitly.

Define whether a derivative can be independently referenced.

Prevent orphaned derivative records where practical.

---

# 30. MEDIA LIFECYCLE

Implement the media state machine appropriate to this scope.

At minimum distinguish:

* initialized;
* uploaded;
* validating;
* processing;
* ready;
* failed;
* deleted.

Define allowed transitions.

Do not allow arbitrary state mutation from an unauthenticated client.

---

# 31. UPLOAD INITIALIZATION

Implement an upload-initialization API behind the project's object-storage abstraction.

The backend should:

* authenticate the caller;
* validate requested media type;
* enforce file-size constraints;
* create a media asset record;
* generate a safe object key;
* return the information needed by the client to perform the actual upload.

Do not proxy large media bodies through the application server unnecessarily.

Do not expose internal bucket credentials.

Do not return permanent privileged storage credentials.

---

# 32. UPLOAD FINALIZATION

Implement upload finalization.

The backend must verify, as appropriate:

* media asset ownership;
* expected object identity;
* object existence if the configured provider supports verification;
* expected size;
* expected media type;
* processing state.

Transition the media asset into the appropriate validation/processing state.

Do not trust a client saying that an upload succeeded without verifying the authoritative storage state when provider access allows verification.

---

# 33. OBJECT STORAGE ABSTRACTION

Create a provider-neutral interface for object storage.

Support operations appropriate to this scope such as:

* create upload authorization;
* verify object existence;
* inspect object metadata where supported;
* delete object;
* generate controlled delivery references where applicable.

Keep provider-specific logic isolated from the domain modules.

Do not hardcode AWS credentials.

Do not claim a real storage provider is configured when credentials are unavailable.

---

# 34. MEDIA SECURITY

Implement media-ingestion protections within the available application boundary.

Validate:

* declared MIME type;
* allowed media type;
* size limits;
* file extension where relevant;
* ownership;
* upload state.

Where a scanning/processing provider is unavailable, preserve an explicit processing state rather than pretending the media has been validated.

Do not trust client-provided dimensions or duration when authoritative inspection is available downstream.

---

# 35. MEDIA PROCESSING JOBS

Create the job definitions required to process:

* image normalization;
* thumbnail generation;
* video transcoding;
* video thumbnails;
* metadata extraction.

Each job must define:

* job type;
* payload;
* version;
* media asset ID;
* attempt semantics;
* idempotency requirements;
* failure behavior.

Do not build a complete worker fleet if worker infrastructure belongs to a later scope.

The current backend must be able to enqueue or otherwise publish the work correctly.

---

# 36. MEDIA PROCESSING RESULTS

Implement local processing-state transitions for:

* success;
* failure;
* retryable failure;
* permanent failure.

A processing completion must be idempotent.

Do not permit duplicate processing results to produce inconsistent state.

When a derivative is created, record its relationship to the parent media asset.

---

# 37. MEDIA ACCESS AUTHORIZATION

Implement server-side authorization for media references.

Consider:

* media ownership;
* parent-content visibility;
* account privacy;
* blocked relationship;
* deleted parent content;
* deleted media;
* processing state.

Do not let a previously issued media reference permanently bypass current authorization rules when the product requires protected access.

---

# 38. STORAGE OBJECT KEYS

Generate deterministic but non-sensitive object-key structures.

Keys should allow:

* media-asset identification;
* derivative separation;
* environment isolation;
* lifecycle operations.

Do not put:

* passwords;
* authentication tokens;
* private message content;
* unnecessary personally identifying information

into object names.

---

# 39. MEDIA DELETION

Implement media deletion requests within the current domain.

Deletion must:

* verify authorization;
* mark the media asset appropriately;
* prevent ordinary new use;
* emit the relevant event;
* initiate asynchronous physical object cleanup.

Do not claim that physical deletion from every replica/CDN cache has completed unless it actually has.

---

# 40. POST/MEDIA TRANSACTIONAL CONSISTENCY

Use transactions for state changes that must remain atomic.

Examples:

* creating a post with its media associations;
* deleting a post and its authoritative media relationships;
* creating a story and story items;
* publishing content after required media state validation.

Do not create a published post that references missing required media records.

Do not combine unrelated domain operations into unnecessarily large transactions.

---

# 41. REDIS USAGE

Use Redis only where justified within this scope.

Potential uses include:

* short-lived upload/session coordination;
* processing-state acceleration;
* rate limiting;
* content-read caching where appropriate.

Every cache must define:

* namespace;
* key structure;
* TTL;
* source of truth;
* invalidation behavior;
* failure behavior.

PostgreSQL and object storage remain authoritative for durable content/media state.

---

# 42. CACHE INVALIDATION

Where post/profile/media caching is introduced, invalidate or bypass cache entries when:

* content is deleted;
* visibility changes;
* ownership state changes;
* account privacy changes;
* media is deleted;
* moderation-related restrictions are applied by existing infrastructure.

Do not let stale caches become an authorization bypass.

---

# 43. EVENTS

Publish appropriate domain events for:

* post creation;
* post publication;
* post update;
* post deletion;
* story creation;
* story publication;
* story expiration;
* story deletion;
* short-video creation;
* short-video publication;
* short-video deletion;
* media upload;
* media processing completion;
* media processing failure;
* media deletion.

Use the project's canonical event envelope.

Events must be versioned.

Payloads must contain only information appropriate for downstream consumers.

---

# 44. OUTBOX RELIABILITY

Use the backend's durable event publication mechanism for critical content/media events.

When a database transaction and domain event must remain consistent:

* persist the state transition;
* persist the outbound event atomically;
* publish asynchronously;
* support retries;
* support duplicate-safe consumers.

Do not make downstream event publication a reason for rolling back an already successful core transaction unless the domain explicitly requires synchronous coupling.

---

# 45. ASYNCHRONOUS EXPIRATION

Implement a durable mechanism for story expiration processing.

The authoritative story `expiresAt` determines visibility.

The background job/event exists to:

* transition or mark expired state;
* remove/cleanup derived data where applicable;
* trigger future cleanup.

Duplicate expiration execution must be safe.

---

# 46. AUTHORIZATION

Every protected operation must enforce server-side authorization.

Protect:

* post creation;
* post updates;
* post deletion;
* story creation;
* story deletion;
* short-video creation;
* short-video deletion;
* media initialization;
* media finalization;
* media deletion;
* content retrieval.

Use the existing account/privacy/relationship policy boundaries where available.

Do not reproduce identity logic independently.

---

# 47. CONCURRENCY

Handle concurrent operations such as:

* two post publications using the same media;
* duplicate upload finalization;
* repeated post deletion;
* simultaneous story expiration and deletion;
* repeated processing completion;
* concurrent caption updates;
* duplicate content creation caused by network retries.

Use:

* uniqueness constraints;
* transactions;
* idempotency;
* optimistic concurrency;
* appropriate locking.

Do not assume clients behave perfectly.

---

# 48. IDEMPOTENCY

Make retry-sensitive operations safe.

At minimum evaluate:

* upload initialization;
* upload finalization;
* post creation;
* post publication;
* post deletion;
* story creation;
* story deletion;
* media deletion;
* processing-result handling.

Do not create duplicate logical media assets or duplicate logical posts because of ordinary network retries.

---

# 49. DATABASE INDEXING

Create indexes based on actual query patterns.

At minimum evaluate indexes for:

* post author;
* post publication state;
* post timestamps;
* content visibility where useful;
* story author;
* story expiration;
* story item ordering;
* media owner;
* media processing state;
* media object reference;
* hashtag normalization;
* mention target/source;
* content-media relationships.

Do not create redundant indexes without a workload justification.

---

# 50. DATABASE CONSTRAINTS

Use database constraints for authoritative invariants.

Examples include:

* unique media IDs;
* unique media ordering within a content object;
* unique mention relationship per post/account;
* unique hashtag association per post;
* valid foreign-key relationships;
* valid lifecycle values;
* valid ownership references.

Do not rely only on application-level checks for uniqueness.

---

# 51. MIGRATIONS

Create real database migrations.

Migrations must:

* be deterministic;
* represent schema changes explicitly;
* support the repository's migration system;
* preserve existing data;
* avoid destructive operations without an intentional migration strategy.

Do not use automatic schema synchronization as a substitute for production migrations.

---

# 52. API CONTRACTS TO IMPLEMENT

Implement an in-scope API surface equivalent to:

## Posts

* create post;
* get post;
* update post;
* delete post;
* list appropriate owned posts where required by this scope.

## Media

* initialize upload;
* finalize upload;
* get media metadata where appropriate;
* delete media.

## Stories

* create story;
* get story;
* list active stories for an authorized author/view context where appropriate;
* delete story.

## Short-Form Video

* create short video;
* get short video;
* update supported metadata;
* delete short video;
* publish/finalize where appropriate.

Use repository-established route conventions when they already exist.

---

# 53. API VALIDATION

Validate:

* content types;
* caption limits;
* media count;
* media compatibility;
* visibility;
* IDs;
* story expiration constraints;
* video metadata;
* upload sizes;
* supported MIME types;
* cursor parameters.

Reject malformed content before persistence.

---

# 54. ERROR HANDLING

Use the project's canonical error contract.

Return safe, stable errors for:

* unauthorized access;
* forbidden access;
* invalid media;
* media not found;
* processing not complete;
* invalid publication state;
* invalid visibility;
* duplicate operations;
* conflicting updates;
* expired resources;
* rate limits;
* dependency failures.

Do not expose object-storage provider internals.

---

# 55. RATE LIMITING

Protect media/content creation endpoints against abuse.

At minimum evaluate limits for:

* post creation;
* story creation;
* short-video creation;
* upload initialization;
* upload finalization;
* content deletion;
* media deletion.

Keep limits configurable.

Use Redis or the project's established rate-limit mechanism.

Do not disable rate limiting silently when Redis is unavailable without a deliberate failure policy.

---

# 56. SECURITY HARDENING

Protect against:

* unauthorized media attachment;
* cross-account content access;
* malicious object keys;
* oversized uploads;
* MIME spoofing;
* path traversal;
* SSRF through provider callbacks/configuration where applicable;
* insecure direct object access;
* enumeration of internal resources;
* duplicate processing attacks;
* authorization bypass through cached content.

Never place storage credentials in client-visible responses.

---

# 57. PRIVACY

Ensure private-account content cannot be retrieved by unauthorized accounts.

When account privacy changes, content access decisions must reflect current state.

Do not permanently cache a content response in a way that bypasses a later privacy restriction.

Ensure content deletion can propagate to:

* caches;
* search;
* feed;
* notifications;
* media delivery;

through events/hooks even though those downstream systems are outside this prompt's implementation scope.

---

# 58. OBSERVABILITY

Instrument this backend scope with:

* structured request logs;
* content-operation metrics;
* upload metrics;
* media-processing initiation metrics;
* processing success/failure metrics;
* authorization-denial metrics;
* API latency;
* database latency;
* Redis failure metrics;
* event publication failures.

Include correlation IDs.

Do not log raw:

* media object credentials;
* signed URLs containing sensitive material where avoidable;
* passwords;
* access tokens;
* private content bodies unnecessarily.

---

# 59. HEALTH AND DEPENDENCY BEHAVIOR

Ensure the backend's health/readiness design accounts for dependencies relevant to this scope.

Distinguish:

* process liveness;
* application readiness;
* required database readiness;
* optional object-storage availability;
* queue/event infrastructure availability.

A temporary media-provider outage must not necessarily make every unrelated content read unavailable.

---

# 60. TESTING STRATEGY

Create real tests for the current scope.

## Unit Tests

Test:

* content lifecycle;
* visibility policies;
* media authorization;
* caption validation;
* hashtag parsing;
* mention parsing;
* story expiration;
* video state transitions;
* idempotency;
* error mapping.

## Integration Tests

Test:

* post persistence;
* post/media associations;
* story persistence;
* story expiration;
* short-video persistence;
* media lifecycle;
* migration correctness;
* object-storage adapter behavior using a safe test abstraction;
* Redis-backed mechanisms where applicable;
* outbox/event persistence.

## API Tests

Test:

* authentication;
* authorization;
* validation;
* successful content creation;
* invalid media;
* private-content access;
* deletion;
* pagination where exposed;
* idempotency;
* conflict behavior.

---

# 61. SECURITY TESTING

Test at least:

* unauthorized post access;
* private post access by unrelated account;
* blocked-account content access;
* attaching another account's media;
* deleting another account's content;
* invalid upload state;
* invalid storage-object reference;
* media-type spoofing;
* oversized upload;
* duplicate finalization;
* duplicate publication;
* expired story access.

Do not claim comprehensive security verification.

---

# 62. CONCURRENCY TESTING

Where the test environment permits, validate races involving:

* duplicate post creation;
* duplicate upload finalization;
* simultaneous deletion;
* simultaneous publication;
* processing-result duplication;
* story expiration/deletion.

Validate that database constraints and transactional logic maintain invariants.

---

# 63. PERFORMANCE VALIDATION

Perform targeted validation for:

* post retrieval by ID;
* media metadata retrieval;
* relationship of posts to media assets;
* story expiration queries;
* content authorization queries;
* cursor-paginated content retrieval where applicable.

Do not claim production-scale throughput from local measurements.

Record actual test conditions.

---

# 64. DOCUMENTATION

Create/update documentation for:

* post APIs;
* content lifecycle;
* visibility rules;
* media lifecycle;
* upload flow;
* media object-storage abstraction;
* story semantics;
* short-video semantics;
* media-processing jobs;
* event contracts;
* environment configuration;
* testing.

Documentation must describe actual implemented behavior.

Do not document unimplemented feed, messaging, search, or notification behavior as complete.

---

# 65. PORTABLE CONTRACT REQUIREMENT

Maintain or create portable contracts covering:

* post schema;
* media schema;
* story schema;
* short-video schema;
* visibility;
* lifecycle states;
* media processing states;
* upload/finalization behavior;
* content events;
* media events;
* error codes;
* API request/response shapes.

The contracts must be usable by later backend, web, mobile, infrastructure, and QA work without relying on this conversation.

---

# 66. CROSS-PART COMPATIBILITY

The implementation must remain compatible with:

* account/profile;
* social graph;
* feed;
* discovery;
* engagement;
* notifications;
* moderation;
* web;
* mobile;
* infrastructure;
* QA.

Do not implement feed or discovery behavior here.

Do provide stable content/media contracts that later systems can consume.

---

# 67. FUTURE-DOMAIN INTEGRATION HOOKS

Create durable integration points for later:

* feed propagation;
* search indexing;
* engagement;
* notifications;
* moderation;
* analytics.

At minimum, downstream systems must be able to consume content/media lifecycle events.

Do not implement their business logic.

---

# 68. NO FAKE COMPLETENESS

Do not use:

* fake media processing;
* fake object storage;
* fake persistence;
* mock APIs in production paths;
* placeholder publication logic;
* hardcoded content;
* dummy events;
* TODO/FIXME gaps for current functionality;
* pseudo-code.

Where an external provider cannot be accessed, implement the local integration boundary and state handling honestly without claiming provider execution.

---

# 69. FILE/MODULE SCOPE

Organize the implementation around the actual repository structure.

Reasonable areas include:

* content/posts;
* stories;
* short-form video;
* media;
* storage adapter;
* upload APIs;
* processing jobs;
* events/outbox;
* cache;
* database;
* tests;
* documentation.

Do not split the work artificially to satisfy a file count.

Do not merge content and unrelated domains merely for convenience.

---

# 70. VALIDATION

Before completion:

1. run formatting;
2. run linting;
3. run type checking;
4. validate database migrations;
5. run unit tests;
6. run integration tests;
7. run API/contract tests;
8. run security-focused tests;
9. run concurrency tests where available;
10. validate startup configuration;
11. validate relevant health behavior;
12. validate documentation/contracts.

If an external object-storage service, media-processing service, or cloud environment is unavailable, distinguish local validation from unavailable external validation.

Do not claim successful external operations that were not performed.

---

# 71. IMPLEMENTATION REPORT

After implementation, provide a completion report containing:

## Files Created

List every file created.

## Files Modified

List every file modified.

## Files Deleted

List every file deleted, if any.

## Backend Domains Implemented

Summarize:

* posts;
* stories;
* short-form video;
* media;
* upload lifecycle;
* processing lifecycle.

## Database Changes

List:

* tables;
* relationships;
* constraints;
* indexes;
* migrations.

## API Changes

List implemented endpoints and major request/response contracts.

## Media Changes

Summarize:

* asset model;
* object-storage integration;
* upload initialization;
* upload finalization;
* processing states;
* derivatives.

## Event Changes

List:

* event types;
* payloads;
* versioning;
* outbox behavior.

## Redis Changes

List:

* keys/namespaces;
* TTLs;
* purposes;
* invalidation behavior.

## Security Changes

Summarize:

* authorization;
* media security;
* privacy controls;
* rate limits.

## Tests Created

List test categories and major scenarios.

## Tests Executed

State exactly which tests were executed.

## Validation Performed

State exactly what validation was performed.

## Documentation Changes

List documentation created or updated.

## Integration Considerations

Describe how later feed, discovery, engagement, notification, moderation, web, mobile, and infrastructure systems consume the contracts produced here.

## Compatibility Considerations

Identify compatibility-sensitive changes.

## Known Limitations

List genuine limitations.

## Unresolved Issues

List only issues that remain unresolved.

---

# 72. DEFINITION OF DONE

This backend milestone is complete only when:

* post persistence is real;
* post publication state is implemented;
* post visibility is enforced;
* post ownership is enforced;
* post/media relationships are implemented;
* carousel ordering is deterministic;
* captions are validated;
* hashtags are normalized and associated;
* mentions are resolved and persisted;
* post updates are authorized and concurrency-safe;
* post deletion works;
* story persistence works;
* story-item ordering works;
* story expiration is server-authoritative;
* expired stories are inaccessible;
* short-form video metadata is persisted;
* video lifecycle states are implemented;
* media assets are persisted;
* media lifecycle states are implemented;
* upload initialization works;
* upload finalization works;
* object-storage integration is isolated behind a boundary;
* media-processing jobs can be initiated correctly;
* processing results are idempotent;
* media deletion is handled;
* relevant events are durable;
* outbox reliability is implemented where required;
* Redis usage is bounded and documented;
* rate limiting is implemented where applicable;
* authorization and privacy are enforced;
* observability is implemented;
* migrations validate;
* unit tests exist;
* integration tests exist;
* API/contract tests exist;
* security tests exist;
* concurrency-sensitive behavior is tested where practical;
* documentation reflects actual implementation;
* no production credentials are committed;
* no fake functionality exists;
* no intentional implementation gaps remain inside the defined scope.

---

# 73. FINAL IMPLEMENTATION DISCIPLINE

Implement **only the current prompt's scope**.

Do not implement:

* feed ranking;
* feed generation;
* Explore/recommendations;
* search indexing;
* likes;
* comments;
* saves;
* shares;
* direct messaging;
* notifications;
* moderation workflows;
* administration;
* analytics pipelines;
* full infrastructure provisioning.

Do not redesign the account/profile or relationship domains unless a concrete compatibility issue within the current scope requires it.

Do not assume another AI prompt has been executed.

Do not depend on another AI conversation.

Do not invent provider credentials.

Do not claim actual cloud storage, media processing, CDN, or deployment operations unless they were genuinely performed.

Produce real, tested, documented backend functionality for Instagram's content, stories, short-form video, and media foundation.
