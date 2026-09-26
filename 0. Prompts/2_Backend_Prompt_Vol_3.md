# Instagram — Backend Prompt — Volume 3

# 1. ROLE

You are the **Staff Backend Engineering team** responsible for implementing the engagement and interaction backend domains for the **Instagram** project.

Operate with the combined responsibilities of:

* Staff Backend Engineer
* Backend Architect
* Database Engineer
* Distributed Systems Engineer
* Security Engineer
* Reliability Engineer
* Performance Engineer
* Data/Consistency Engineer
* QA-minded Backend Engineer
* Observability Engineer

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

* account and identity services;
* profiles;
* social graph;
* posts;
* stories;
* short-form video;
* media processing;
* feed;
* discovery/search;
* messaging;
* notifications;
* moderation;
* administration;
* analytics;
* web clients;
* mobile clients;
* infrastructure.

The completed platform is intended to support approximately:

* 100 million registered accounts;
* 20 million daily active users;
* 2 million peak concurrent active sessions;
* approximately 100,000 sustained API requests per second;
* approximately 250,000 requests per second during peak bursts;
* extremely high content and engagement volumes.

These are global architectural targets.

This prompt implements only the **engagement and interaction backend** defined below.

---

# 3. CURRENT BACKEND ASSIGNMENT

Implement the backend foundation for:

1. likes;
2. comments;
3. comment replies;
4. saves;
5. shares;
6. mention/hashtag interaction support where required by engagement;
7. engagement counters;
8. engagement state queries;
9. content interaction authorization;
10. idempotent engagement mutations;
11. concurrency-safe high-volume interaction handling;
12. cursor-paginated comments;
13. engagement-related events;
14. interaction cache structures where justified;
15. interaction-related Redis coordination;
16. persistence and migrations;
17. observability;
18. security;
19. privacy;
20. testing;
21. documentation.

This prompt must produce the authoritative engagement foundation consumed later by feed, notification, discovery, moderation, analytics, web, and mobile implementations.

---

# 4. REPOSITORY INSPECTION

Before modifying or creating code, inspect the repository.

Inspect, where present:

* backend application structure;
* account/profile modules;
* relationship modules;
* content/post modules;
* story/short-video modules;
* media modules;
* database schema;
* migrations;
* API conventions;
* event/outbox infrastructure;
* Redis integration;
* authorization policies;
* validation;
* error handling;
* test infrastructure;
* observability;
* documentation.

Treat the repository as the source of truth for what actually exists.

Do not assume previous AI prompts were executed.

Do not assume another Claude conversation exists.

Do not fabricate repository state.

Reuse compatible components already present.

---

# 5. TECHNOLOGY BASELINE

Use the repository's existing backend stack, with the project baseline of:

* TypeScript;
* Node.js;
* structured TypeScript backend architecture;
* PostgreSQL;
* Redis;
* REST APIs;
* durable event publication;
* strong validation;
* structured logging;
* tracing/metrics where available;
* automated tests.

Do not introduce a new framework or persistence technology merely for this milestone.

---

# 6. BOUNDED IMPLEMENTATION SCOPE

## In Scope

Implement:

* likes;
* like/unlike;
* comments;
* comment creation/update/deletion;
* comment replies;
* comment pagination;
* saves;
* unsave;
* shares;
* engagement state queries;
* engagement counters;
* counter consistency strategy;
* engagement events;
* interaction authorization;
* privacy-aware engagement;
* block/mute/restriction-aware behavior where applicable;
* concurrency-safe mutations;
* idempotency;
* database persistence;
* migrations;
* Redis usage where justified;
* event/outbox integration;
* metrics and logging;
* unit tests;
* integration tests;
* API/contract tests;
* security tests;
* documentation.

## Out of Scope

Do not implement:

* feed generation;
* feed ranking;
* Explore/recommendations;
* search indexing;
* direct messaging;
* notification delivery;
* moderation workflows;
* administration UI;
* creator analytics;
* recommendation models;
* full analytics pipelines;
* complete web UI;
* complete mobile UI;
* infrastructure provisioning.

Create the contracts needed by those systems, but do not implement their complete runtime functionality.

---

# 7. ENGAGEMENT DOMAIN ARCHITECTURE

Organize this milestone around clear engagement responsibilities:

* likes;
* comments;
* saves;
* shares;
* counters;
* interaction authorization;
* engagement events.

Do not duplicate content ownership logic.

The content/post domain remains authoritative for:

* post identity;
* authorship;
* content lifecycle;
* visibility;
* media.

The engagement domain owns interaction state and engagement-specific persistence.

---

# 8. INTERACTION AUTHORIZATION FOUNDATION

Every engagement operation must evaluate:

* authenticated caller;
* target content existence;
* target content lifecycle;
* content visibility;
* target account privacy;
* relationship state;
* block state;
* moderation state when already available.

Do not trust the client to determine whether an interaction is permitted.

Create centralized policy logic for engagement authorization.

Later notification, feed, and moderation systems must be able to consume engagement decisions consistently.

---

# 9. LIKE MODEL

Implement a production-grade like relationship.

A like must include, as appropriate:

* like ID;
* post/content ID;
* account ID;
* creation timestamp.

Enforce uniqueness for:

**one account + one target content object**

A user must not be able to create duplicate logical likes through concurrent or repeated requests.

---

# 10. LIKE API

Implement APIs equivalent to:

* like content;
* unlike content;
* determine whether the current user has liked content;
* retrieve a paginated list of likes where required by the product scope.

Use repository-established API naming conventions when present.

Return stable response models.

Do not expose unnecessary internal persistence details.

---

# 11. LIKE IDEMPOTENCY

Like/unlike operations must be safe under retries.

Examples:

* repeated like request;
* repeated unlike request;
* simultaneous like requests;
* like retry after a network timeout.

Use:

* database uniqueness;
* transactional state changes;
* appropriate idempotency semantics.

Do not rely on the client to prevent duplicate likes.

---

# 12. LIKE CONCURRENCY

Handle races such as:

* two requests liking the same content simultaneously;
* like and unlike arriving concurrently;
* retries after successful persistence but before response delivery.

The final database state must remain valid.

Do not use application-side "check then insert" logic without a database-level invariant.

---

# 13. COMMENT MODEL

Implement comments.

Each comment must support, as appropriate:

* comment ID;
* content/post ID;
* author account ID;
* parent comment ID;
* body;
* lifecycle state;
* creation timestamp;
* update timestamp;
* deletion timestamp.

Use `parentCommentId` or an equivalent explicit relation for replies.

Do not create separate incompatible persistence models for comments and replies unless the architecture requires it.

---

# 14. COMMENT CONTENT VALIDATION

Implement validation for comment bodies.

Define:

* maximum length;
* minimum meaningful content rules where appropriate;
* normalization;
* empty/comment-only-whitespace behavior;
* supported encoding;
* safe handling of malicious input.

Do not render or interpret HTML submitted as comment content unless explicitly required by the product.

Store canonical text safely.

---

# 15. COMMENT CREATION

Implement comment creation.

The request flow must include:

1. authentication;
2. target-content authorization;
3. parent-comment validation if replying;
4. text validation;
5. persistence;
6. event publication;
7. response creation.

Use a transaction when the comment and its authoritative related state must become atomic.

Do not invoke future notification delivery synchronously.

---

# 16. COMMENT REPLY AUTHORIZATION

A reply must verify:

* parent comment exists;
* parent comment belongs to the target content;
* target content is accessible to the caller;
* parent comment is not deleted/restricted in a state that prevents replies;
* the caller is authorized to interact with the content.

Do not accept arbitrary parent-comment/content combinations supplied by the client.

---

# 17. COMMENT HIERARCHY

Keep comment nesting bounded.

Use the architecture's defined reply model.

Do not create an unbounded recursive hierarchy that produces unpredictable database and API behavior.

If replies are single-level or otherwise bounded, enforce that rule server-side.

Do not allow clients to bypass hierarchy constraints by supplying crafted parent IDs.

---

# 18. COMMENT RETRIEVAL

Implement cursor-based comment retrieval.

Support:

* root comments;
* replies;
* stable ordering;
* pagination;
* deletion handling;
* privacy filtering;
* authorization;
* deterministic traversal.

Do not use large-offset pagination for high-volume comment collections.

Define the ordering explicitly.

---

# 19. COMMENT DELETION

Implement comment deletion.

At minimum support deletion by authorized:

* comment owner;
* content owner where the project's policy permits.

When deleted:

* prevent ordinary new retrieval;
* preserve the integrity of reply relationships where necessary;
* emit a deletion event;
* update relevant counters;
* invalidate applicable caches.

Do not physically destroy relational context in a way that makes downstream replies invalid unless that behavior is explicitly part of the chosen product semantics.

---

# 20. COMMENT UPDATE

Implement supported comment updates.

Verify:

* caller ownership;
* comment lifecycle;
* target-content state.

Protect against concurrent edits where necessary.

Do not allow arbitrary modification of:

* author;
* target content;
* parent relationship.

---

# 21. COMMENT COUNTERS

Implement comment-count behavior.

Define whether the authoritative count is:

* transactionally maintained;
* asynchronously aggregated;
* derived through a count query;
* maintained through a hybrid model.

The implementation must remain compatible with the high-scale target.

Avoid synchronous global counter rows becoming a hot-row bottleneck for extremely popular content.

---

# 22. SAVE MODEL

Implement saved-content relationships.

A save must support:

* save ID;
* account ID;
* target content ID;
* creation timestamp.

Enforce uniqueness for:

**one account + one target content object**

---

# 23. SAVE API

Implement APIs equivalent to:

* save content;
* unsave content;
* determine whether the current user has saved content.

Where a saved-content list is exposed by this backend scope, use cursor pagination.

Do not implement collections/folders unless they are part of this milestone's explicit product scope.

---

# 24. SAVE AUTHORIZATION

A user may save only content they are currently authorized to access.

Saving private content must not create a hidden authorization bypass.

If the user later loses access because of:

* account privacy change;
* block;
* content deletion;
* moderation;

saved-content retrieval must respect the current authorization state.

---

# 25. SHARE MODEL

Implement the authoritative share interaction required by the product.

A share record must identify:

* share ID;
* actor;
* target content;
* timestamp;
* share type where the product requires multiple share destinations.

Do not implement direct messaging merely to support shares.

Do not create a fake messaging system.

The share operation must expose a stable event and contract for later consumers.

---

# 26. SHARE SEMANTICS

Define whether a share is:

* an immutable event;
* a durable user action;
* an aggregated metric;
* a combination of durable interaction and event.

Preserve the chosen semantics consistently.

If repeat shares are allowed, model them intentionally.

Do not accidentally create a uniqueness constraint that prevents legitimate repeat share behavior unless the product explicitly requires unique share state.

---

# 27. ENGAGEMENT COUNTERS

Implement a scalable counter strategy for:

* likes;
* comments;
* shares;
* saves where the product needs a public count.

The system must clearly distinguish:

* authoritative interaction records;
* derived counters.

A counter must never become the sole source of truth for whether an individual like/save relationship exists.

---

# 28. COUNTER CONSISTENCY

Define acceptable consistency for counters.

For high-volume counts:

* exact transactional counts may be used where safe;
* asynchronous aggregation may be used where necessary;
* sharded counters may be used where justified;
* periodic reconciliation must be possible.

Do not create silently drifting counters with no correction mechanism.

Implement the most appropriate strategy for the repository's actual current scale while preserving the global architecture.

---

# 29. HOT-CONTENT PROTECTION

Design engagement writes for highly popular content.

Consider:

* hot rows;
* viral posts;
* high-volume likes;
* comment storms;
* share spikes.

Use appropriate techniques such as:

* unique relational constraints;
* sharded/partitioned aggregation;
* asynchronous counter updates;
* batching;
* Redis coordination;
* rate limiting.

Do not force every interaction through one globally contended row.

---

# 30. REDIS USAGE

Use Redis where it provides a concrete benefit.

Possible uses:

* short-lived engagement-state caching;
* idempotency coordination;
* rate limiting;
* hot-counter buffering;
* request coalescing where justified.

Every cache must define:

* namespace;
* key;
* TTL;
* source of truth;
* invalidation;
* acceptable staleness;
* failure behavior.

Redis must not replace durable interaction persistence.

---

# 31. ENGAGEMENT STATE QUERIES

Implement efficient queries to determine:

* whether the current account likes a post;
* whether the current account saved a post;
* engagement counts;
* comment count;
* share count where available.

Do not execute one database query per item in a large collection.

Where batch retrieval is appropriate, implement efficient batch query patterns that later feed implementations can consume.

Avoid N+1 patterns in engagement-state retrieval.

---

# 32. BATCH ENGAGEMENT LOOKUPS

Provide backend mechanisms for batch retrieval of engagement state for multiple content IDs.

At minimum support efficient retrieval of:

* liked-by-current-user;
* saved-by-current-user;
* counts where appropriate.

Define stable response semantics.

Do not require callers to issue one HTTP request for every post displayed in a feed.

---

# 33. EVENT CONTRACTS

Publish engagement lifecycle events such as:

* `like.created`;
* `like.removed`;
* `comment.created`;
* `comment.updated`;
* `comment.deleted`;
* `save.created`;
* `save.removed`;
* `share.created`.

Use the established canonical event envelope.

Each event must contain enough stable identifiers for later consumers without unnecessarily exposing sensitive content.

---

# 34. EVENT PAYLOAD DISCIPLINE

Events must distinguish:

* actor;
* target resource;
* target resource owner where necessary;
* event timestamp;
* event ID;
* schema version.

Do not place entire ORM entities into events.

Do not place unnecessary:

* passwords;
* session data;
* access tokens;
* private metadata;
* internal database fields

into event payloads.

---

# 35. OUTBOX RELIABILITY

Persist required domain events reliably with the corresponding engagement state transition.

Where the architecture uses a transactional outbox:

* engagement mutation;
* outbox event creation

must be transactionally coordinated.

Publishing to downstream infrastructure may happen asynchronously.

Duplicate downstream delivery must remain safe.

---

# 36. TRANSACTION BOUNDARIES

Use transactions for operations requiring atomicity.

Examples include:

* create like + outbox event;
* remove like + outbox event;
* create comment + outbox event;
* delete comment + outbox event;
* save + outbox event;
* unsave + outbox event.

Do not combine unrelated engagement operations into one giant transaction.

---

# 37. PRIVACY AND BLOCKING

Engagement must respect current relationship policy.

If a user is blocked or otherwise prohibited from interacting with content:

* mutation must fail safely;
* existing interactions must be handled according to the project's policy;
* retrieval must respect current visibility.

Do not let a pre-existing like/save/comment record bypass current privacy or blocking rules.

---

# 38. PRIVATE CONTENT

For private accounts, interactions must be possible only for authorized viewers.

Check current authorization when:

* liking;
* commenting;
* replying;
* saving;
* sharing.

Do not rely on the fact that an interaction record existed before the content became private.

---

# 39. DELETED CONTENT

When content is deleted:

* new engagement mutations must be rejected;
* existing engagement data must transition according to lifecycle rules;
* counts must no longer represent active accessible content where appropriate;
* caches must be invalidated;
* deletion events must be published.

Do not leave active interaction endpoints operating on deleted content.

---

# 40. DELETED COMMENTS

Define handling for comments whose parent content or parent comment is deleted.

Maintain enough relational integrity for API behavior and future moderation systems.

Possible behavior may include retaining a tombstone representation or deleting dependent records, but choose one explicit strategy and implement it consistently.

Do not leave orphaned replies without defined semantics.

---

# 41. RATE LIMITING

Implement rate limits appropriate to engagement.

Protect:

* like;
* unlike;
* comment creation;
* comment updates;
* comment deletion;
* save;
* unsave;
* share.

Make thresholds configurable.

Consider separate limits for:

* authenticated account;
* IP/network;
* content target where abuse spikes;
* endpoint.

Do not make rate-limit decisions dependent exclusively on client behavior.

---

# 42. ABUSE-RESISTANT ENGAGEMENT

The implementation must reduce obvious abuse patterns.

Consider:

* rapid like/unlike loops;
* comment flooding;
* share flooding;
* automated save churn;
* duplicate requests;
* high-frequency mutations.

Implement platform-level rate controls where required.

Do not build the complete fraud/abuse detection platform in this prompt.

Create observable signals for later abuse systems.

---

# 43. COMMENT TEXT SECURITY

Treat comment text as untrusted user input.

Protect against:

* injection;
* XSS when rendered by downstream clients;
* malformed Unicode;
* oversized payloads;
* dangerous control characters where applicable.

Store canonical text.

Do not interpret submitted HTML as trusted markup.

---

# 44. DATABASE SCHEMA

Implement real persistence for:

* likes;
* comments;
* saves;
* shares;
* any required counter/projection tables.

Use:

* foreign keys;
* appropriate uniqueness;
* indexes;
* timestamps;
* deletion semantics.

Evaluate whether comments require database partitioning in the current scope based on expected growth.

Do not introduce partitioning simply because the final product is large.

---

# 45. DATABASE INDEXING

Create indexes for real access paths.

At minimum evaluate:

## Likes

* account + content;
* content + timestamp;
* content + account.

## Comments

* content + creation order;
* parent comment + creation order;
* author + creation order.

## Saves

* account + content;
* account + creation order;
* content where required.

## Shares

* content + timestamp;
* actor + timestamp.

Avoid unnecessary duplicate indexes.

---

# 46. CONCURRENCY

Handle races such as:

* duplicate likes;
* like/unlike collisions;
* duplicate saves;
* save/unsave collisions;
* comment deletion during reply creation;
* comment update/delete collisions;
* share retries;
* counter update races.

Use:

* database constraints;
* transactions;
* optimistic concurrency;
* idempotency;
* appropriate locking.

Do not trust a preflight read to guarantee the final write's uniqueness or validity.

---

# 47. IDEMPOTENCY

Implement safe retry semantics for:

* like;
* unlike;
* save;
* unsave;
* comment creation where a client-generated idempotency key is supplied;
* share operations where applicable.

Repeated requests should produce deterministic results consistent with the domain's semantics.

Do not accidentally create duplicate comments because a client retried after a timeout.

---

# 48. COMMENT IDEMPOTENCY

Provide a client-safe way for comment creation to be retried without creating duplicates.

Use an idempotency key or equivalent request identity where appropriate.

Persist enough information to determine whether the same mutation has already been accepted.

Do not use unbounded idempotency storage.

Define retention/cleanup behavior.

---

# 49. PAGINATION

Implement cursor-based pagination for:

* comments;
* replies;
* relevant likes;
* relevant saves/shares if exposed.

Define:

* stable ordering;
* maximum page size;
* cursor validation;
* deleted-resource behavior;
* authorization filtering.

Do not use offset pagination for large comment tables.

---

# 50. COMMENT ORDERING

Define deterministic comment ordering.

Use an ordering policy consistent with the architecture.

The implementation must not rely on nondeterministic database ordering.

If ranking is not part of this milestone, use an explicit chronological ordering strategy rather than implementing an undeclared ranking system.

Do not build comment recommendation/ranking algorithms here.

---

# 51. API CONTRACTS

Implement APIs equivalent to:

## Likes

* like;
* unlike;
* current-user like state.

## Comments

* create;
* list;
* get where appropriate;
* update;
* delete;
* reply.

## Saves

* save;
* unsave;
* current-user saved state.

## Shares

* create share;
* retrieve relevant share state/count where required.

## Batch State

* retrieve current-user engagement state for multiple content IDs.

Use existing route/version conventions from the repository when available.

---

# 52. API RESPONSE MODELS

Return only fields appropriate to the authenticated caller.

Comment responses may include:

* comment ID;
* author summary;
* target content ID;
* parent ID;
* text;
* timestamps;
* lifecycle state required for rendering.

Do not expose:

* internal moderation metadata;
* database internals;
* private administrative data;
* security events.

---

# 53. ERROR CONTRACTS

Use the established API error contract.

Provide stable errors for:

* unauthorized;
* forbidden;
* content unavailable;
* comment unavailable;
* parent-comment unavailable;
* already liked;
* already saved where semantics require conflict;
* rate limited;
* invalid state;
* duplicate idempotency key;
* conflicting mutation.

Do not expose internal database messages.

---

# 54. OBSERVABILITY

Instrument:

* like latency;
* comment latency;
* save latency;
* share latency;
* engagement mutation counts;
* engagement rejection counts;
* rate-limit events;
* database latency;
* cache hit/miss where caching exists;
* counter update latency;
* event publication latency/failures.

Track high-cardinality operational signals carefully.

Do not place raw comment bodies in normal application logs.

---

# 55. METRICS

Create useful backend metrics such as:

* likes/sec;
* comments/sec;
* saves/sec;
* shares/sec;
* mutation success/failure;
* authorization denials;
* rate-limit rejections;
* duplicate/idempotent requests;
* comment query latency;
* counter reconciliation failures;
* outbox backlog.

Do not create meaningless metrics solely to increase observability volume.

---

# 56. COUNTER RECONCILIATION

Where counters are materialized, implement a mechanism that allows future reconciliation against authoritative interaction records.

The reconciliation mechanism may be:

* a service;
* a scheduled job;
* a database procedure;
* a diagnostic command.

The mechanism must identify mismatches.

It must not silently overwrite correct data without a controlled strategy.

If actual scheduled reconciliation is outside this scope, create the contract/interface required for later infrastructure.

---

# 57. TESTING STRATEGY

Create real tests.

## Unit Tests

Cover:

* like state;
* save state;
* comment policy;
* reply validation;
* visibility;
* block/privacy interactions;
* counter logic;
* idempotency;
* lifecycle transitions;
* error mapping.

## Integration Tests

Cover:

* like persistence;
* duplicate like protection;
* unlike;
* comment persistence;
* replies;
* comment deletion;
* saves;
* shares;
* pagination;
* counter updates;
* outbox persistence;
* Redis mechanisms where applicable.

## API/Contract Tests

Validate:

* authentication;
* authorization;
* request validation;
* response shape;
* errors;
* pagination;
* idempotency.

---

# 58. SECURITY TESTING

Test at minimum:

* unauthorized like;
* unauthorized comment;
* unauthorized reply;
* unauthorized delete;
* interaction with private content;
* interaction after blocking;
* cross-account mutation;
* duplicate requests;
* malformed comment input;
* excessive request rate;
* invalid parent-comment/content combination.

Do not claim complete application security testing.

---

# 59. CONCURRENCY TESTING

Where practical, test:

* simultaneous likes;
* simultaneous unlike/like;
* simultaneous save/unsave;
* comment creation against comment deletion;
* duplicate comment creation;
* concurrent deletion;
* duplicate outbox event prevention where applicable.

Verify database invariants.

---

# 60. PERFORMANCE VALIDATION

Perform targeted tests for:

* indexed like state lookup;
* batch engagement lookup;
* comment pagination;
* comment retrieval by content;
* relationship-aware authorization;
* counter access.

Do not claim production-scale benchmark results from a development machine.

Document actual conditions.

---

# 61. DOCUMENTATION

Create or update documentation for:

* engagement APIs;
* like semantics;
* comment semantics;
* reply semantics;
* save semantics;
* share semantics;
* counter behavior;
* pagination;
* idempotency;
* event contracts;
* rate limits;
* privacy behavior;
* testing.

Documentation must describe implemented behavior.

---

# 62. PORTABLE CONTRACTS

Maintain explicit contracts for:

* like;
* comment;
* reply;
* save;
* share;
* counters;
* engagement-state lookup;
* engagement events;
* pagination;
* idempotency.

These contracts must be understandable by later web, mobile, feed, notification, moderation, analytics, and QA implementations without requiring this conversation.

---

# 63. CROSS-PART COMPATIBILITY

Preserve compatibility with:

* content/posts;
* account/profile;
* relationship policy;
* feed;
* discovery;
* notifications;
* moderation;
* analytics;
* web;
* mobile;
* infrastructure.

Do not redesign content contracts arbitrarily.

Do not implement downstream consumers inside this milestone.

---

# 64. FUTURE INTEGRATION HOOKS

Provide durable event and API contracts for later systems to consume:

* engagement notifications;
* feed ranking signals;
* content discovery signals;
* moderation signals;
* analytics events.

Do not synchronously invoke future notification or analytics systems.

---

# 65. NO FAKE COMPLETENESS

Do not use:

* fake persistence;
* fake counters;
* dummy comments;
* hardcoded engagement state;
* placeholder APIs;
* mock production logic;
* pseudo-code;
* TODO/FIXME gaps for required work;
* fabricated event delivery.

All current-scope functionality must be implemented.

---

# 66. VALIDATION

Before completion:

1. run formatting;
2. run linting;
3. run type checking;
4. validate migrations;
5. run unit tests;
6. run integration tests;
7. run API/contract tests;
8. run security tests;
9. run concurrency tests where available;
10. validate relevant documentation/contracts;
11. validate startup and health behavior.

If a dependency prevents a test from executing, state the precise limitation.

Do not claim successful validation that did not occur.

---

# 67. IMPLEMENTATION REPORT

After implementation, provide a completion report containing:

## Files Created

List every file created.

## Files Modified

List every file modified.

## Files Deleted

List every file deleted, if any.

## Backend Domains Implemented

Summarize:

* likes;
* comments;
* replies;
* saves;
* shares;
* counters;
* engagement state.

## Database Changes

List:

* tables;
* constraints;
* indexes;
* migrations.

## API Changes

List implemented endpoints and major contracts.

## Redis Changes

List:

* key namespaces;
* TTLs;
* use cases;
* invalidation behavior.

## Event Changes

List:

* events;
* schemas;
* producers;
* outbox behavior.

## Security Changes

Summarize authorization, privacy, rate limiting, and abuse controls.

## Tests Created

List test categories and important scenarios.

## Tests Executed

State exactly which tests were executed.

## Validation Performed

State exact validation performed.

## Documentation Changes

List documentation created or updated.

## Integration Considerations

Explain how feed, notification, moderation, discovery, analytics, web, and mobile systems can consume the engagement contracts.

## Compatibility Considerations

Identify compatibility-sensitive changes.

## Known Limitations

List genuine limitations.

## Unresolved Issues

List only issues that remain unresolved.

---

# 68. DEFINITION OF DONE

This backend milestone is complete only when:

* like persistence works;
* like uniqueness is enforced;
* like/unlike operations are idempotent;
* comment persistence works;
* comment validation works;
* replies work;
* reply authorization works;
* comment pagination works;
* comment update works;
* comment deletion works;
* save persistence works;
* save uniqueness is enforced;
* save/unsave operations work;
* share persistence/event behavior works;
* engagement state queries work;
* batch engagement lookups work;
* counters are implemented with a defined consistency strategy;
* hot-content behavior has been considered;
* privacy and block rules are enforced;
* concurrency invariants are protected;
* relevant rate limits are implemented;
* engagement events are durable;
* Redis usage is bounded where used;
* database migrations exist;
* indexes and constraints exist;
* observability is implemented;
* security tests exist;
* unit tests exist;
* integration tests exist;
* API/contract tests exist;
* concurrency tests exist where practical;
* documentation reflects actual behavior;
* no production secrets are committed;
* no fake functionality exists;
* no intentional implementation gaps remain inside the defined scope.

---

# 69. FINAL IMPLEMENTATION DISCIPLINE

Implement **only the current prompt's scope**.

Do not implement:

* feed generation;
* feed ranking;
* Explore;
* recommendations;
* search;
* direct messaging;
* notifications;
* moderation;
* administration;
* creator analytics;
* complete product analytics;
* web UI;
* mobile UI;
* infrastructure provisioning.

Do not assume another AI prompt has been executed.

Do not depend on another AI conversation.

Do not silently redefine existing content, identity, or relationship contracts.

Do not claim downstream notification, analytics, moderation, or feed processing has been implemented.

Produce real, tested, documented backend functionality for Instagram's engagement and interaction systems.
