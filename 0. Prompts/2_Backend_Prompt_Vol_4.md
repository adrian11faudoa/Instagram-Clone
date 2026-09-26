# Instagram — Backend Prompt — Volume 4

# 1. ROLE

You are the **Staff Backend Engineering team** responsible for implementing the feed, discovery, recommendation, and search backend domains for the **Instagram** project.

Operate with the combined responsibilities of:

* Staff Backend Engineer
* Backend Architect
* Distributed Systems Engineer
* Feed/Ranking Engineer
* Search Engineer
* Database Engineer
* Caching Engineer
* Performance Engineer
* Security Engineer
* Reliability Engineer
* Observability Engineer
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

The backend is part of a larger system containing:

* identity and accounts;
* profiles;
* social graph;
* posts;
* stories;
* short-form video;
* media;
* engagement;
* feed;
* discovery/search;
* direct messaging;
* notifications;
* moderation;
* administration;
* analytics;
* web;
* mobile;
* infrastructure.

The completed platform is intended to support approximately:

* 100 million registered accounts;
* 20 million daily active users;
* 2 million peak concurrent active sessions;
* approximately 100,000 sustained API requests per second;
* approximately 250,000 requests per second during peak bursts;
* high-fan-out social relationships;
* high-volume content;
* large search workloads;
* large recommendation workloads.

These are global architectural targets.

This prompt implements the **feed, discovery, recommendation, and search backend foundation** required by the current project scope.

---

# 3. CURRENT BACKEND ASSIGNMENT

Implement:

1. home-feed candidate generation;
2. home-feed persistence/materialization where appropriate;
3. feed retrieval;
4. feed pagination;
5. feed eligibility filtering;
6. social-graph-aware feed candidate generation;
7. high-fan-out account handling;
8. feed cache;
9. feed invalidation;
10. feed freshness behavior;
11. discovery candidate generation;
12. recommended-account retrieval;
13. recommended-content retrieval;
14. search architecture implementation;
15. user/account search;
16. username search;
17. hashtag search;
18. content search where appropriate;
19. search indexing pipeline;
20. search deletion propagation;
21. search consistency behavior;
22. recommendation signals required by this scope;
23. asynchronous feed/search jobs;
24. relevant Redis structures;
25. relevant OpenSearch integration;
26. event consumers/producers needed by this scope;
27. authorization and privacy filtering;
28. observability;
29. security;
30. performance protections;
31. persistence and migrations;
32. tests;
33. documentation.

This milestone must create a scalable backend foundation without implementing machine-learning recommendation infrastructure that is not actually required for the current scope.

---

# 4. REPOSITORY INSPECTION

Before modifying or creating code, inspect the repository.

Inspect, where present:

* feed/content modules;
* engagement modules;
* social-graph modules;
* account/profile modules;
* media modules;
* event/outbox infrastructure;
* Kafka/event streaming;
* queue/job infrastructure;
* Redis integration;
* database schemas;
* migrations;
* OpenSearch/search infrastructure;
* API conventions;
* authorization policies;
* observability;
* test infrastructure;
* configuration;
* documentation.

Treat the repository as the source of truth for actual implementation state.

Do not assume previous prompts were executed.

Do not assume another Claude conversation exists.

Do not fabricate feed/search infrastructure that is not available.

Reuse compatible infrastructure already present.

---

# 5. TECHNOLOGY BASELINE

Use the repository's existing backend stack with the project baseline of:

* TypeScript;
* Node.js;
* PostgreSQL;
* Redis;
* durable event streaming;
* background jobs;
* OpenSearch or equivalent search engine;
* REST APIs;
* structured validation;
* structured logging;
* tracing/metrics;
* automated tests.

Do not introduce a search engine, queue system, or new database solely because it sounds appropriate if an equivalent compatible system already exists.

---

# 6. BOUNDED IMPLEMENTATION SCOPE

## In Scope

Implement:

* home feed;
* feed candidate generation;
* feed eligibility;
* feed ranking foundation;
* feed materialization where appropriate;
* feed retrieval;
* cursor pagination;
* feed caching;
* feed invalidation;
* high-fan-out/celebrity handling;
* discovery candidates;
* recommended accounts;
* recommended content;
* search index management;
* account/user search;
* username search;
* hashtag search;
* content search;
* search suggestions where supported;
* search deletion;
* event-driven indexing;
* feed/search background jobs;
* Redis structures;
* OpenSearch integration;
* privacy filtering;
* block/mute/restriction filtering;
* moderation-state filtering where current repository contracts support it;
* relevant migrations;
* API contracts;
* observability;
* performance protections;
* tests;
* documentation.

## Out of Scope

Do not implement:

* direct messaging;
* message search;
* notification delivery;
* notification preferences;
* full recommendation-machine-learning training systems;
* creator analytics;
* advertising;
* moderation operations UI;
* administrative dashboards;
* web UI;
* mobile UI;
* full cloud deployment;
* production infrastructure provisioning.

Create interfaces and event contracts needed by those future systems, but do not implement their complete functionality.

---

# 7. FEED ARCHITECTURE

The feed implementation must distinguish:

* authoritative content;
* feed candidates;
* ranked feed entries;
* cached feed pages;
* stale feed entries.

The feed must never become the authoritative owner of posts.

The feed must consume content and relationship data through defined interfaces/contracts.

---

# 8. HOME FEED MODEL

Implement a home-feed domain model supporting:

* viewer account;
* source content;
* candidate timestamp;
* ranking metadata;
* eligibility state;
* materialization timestamp;
* freshness state;
* optional score metadata.

Do not expose internal ranking features unnecessarily to clients.

Do not make the feed entry itself the source of truth for content.

---

# 9. FEED CANDIDATE GENERATION

Generate candidates from relevant sources such as:

* accounts the viewer follows;
* content from eligible followed accounts;
* appropriate discovery candidates where explicitly supported;
* content selected by future ranking infrastructure.

The first implementation should use deterministic, explainable signals rather than a fake machine-learning model.

Candidate generation must respect:

* account privacy;
* block relationships;
* mute relationships;
* content lifecycle;
* moderation state where available;
* deleted content;
* visibility restrictions.

---

# 10. FAN-OUT STRATEGY

Implement a hybrid feed architecture.

Use fan-out patterns appropriate to account characteristics.

For ordinary accounts, candidate propagation may be materialized asynchronously.

For extremely high-fan-out accounts, avoid synchronously generating enormous per-follower write amplification.

Support a strategy where high-fan-out sources can be incorporated at read/ranking time or through a specialized candidate path.

Define a configurable threshold rather than hardcoding an unexplained business constant.

---

# 11. FEED WRITE PATH

When eligible content is published, process the feed impact asynchronously where appropriate.

The system must be able to:

* receive the publication event;
* identify affected followers/candidates;
* create or update feed candidates;
* apply eligibility requirements;
* avoid duplicate candidate creation;
* handle retries;
* observe processing latency.

Do not make the successful publication API dependent on processing the entire follower graph synchronously.

---

# 12. FEED READ PATH

Implement feed retrieval.

The read flow must:

1. authenticate the viewer where required;
2. obtain feed candidates;
3. apply current authorization/privacy checks;
4. remove deleted/restricted content;
5. filter blocked relationships;
6. apply mute semantics;
7. apply current content eligibility;
8. rank available candidates;
9. deduplicate results;
10. return stable pagination;
11. populate/update cache where appropriate.

Feed reads must tolerate stale derived state.

---

# 13. FEED AUTHORIZATION

Feed candidate state must never override current authorization.

Before returning a feed item, re-evaluate or otherwise safely enforce:

* account visibility;
* follow relationship;
* block state;
* content lifecycle;
* moderation restrictions;
* deletion;
* privacy changes.

A cached feed entry created yesterday must not allow an otherwise unauthorized viewer to see content today.

---

# 14. FEED RANKING FOUNDATION

Implement a deterministic ranking foundation.

The initial ranking model may use signals such as:

* relationship proximity;
* recency;
* prior engagement;
* content type;
* freshness;
* viewer interaction history available from current backend systems.

Do not build a fake "AI recommendation model."

Do not create machine-learning infrastructure unless the repository already contains a real compatible foundation and it belongs to this prompt.

Create a ranking abstraction so future ranking implementations can replace the initial deterministic strategy without changing the feed API.

---

# 15. FEED RANKING INTERFACE

Create a clear interface between:

**candidate generation**

and:

**ranking**

The ranking layer should receive normalized candidate information rather than coupling directly to database tables.

Define stable input/output structures.

Avoid returning raw internal database entities from ranking logic.

---

# 16. FEED PAGINATION

Implement cursor-based feed pagination.

Define:

* cursor contents;
* stable ordering;
* page size;
* maximum page size;
* cursor validation;
* duplicate avoidance;
* stale-candidate behavior;
* missing/deleted-content behavior.

Feed pagination must remain stable enough that clients do not repeatedly receive the same content across adjacent pages under normal conditions.

---

# 17. FEED DEDUPLICATION

Prevent duplicates caused by:

* multiple candidate sources;
* retries;
* repeated fan-out;
* high-fan-out source merging;
* ranking-stage overlap.

Deduplication must occur before client response generation.

Do not rely on the client to deduplicate feed items.

---

# 18. FEED FRESHNESS

Define feed freshness semantics.

Distinguish:

* fresh candidate;
* stale candidate;
* expired candidate;
* deleted candidate;
* ineligible candidate.

A stale cache is not automatically invalid.

The backend must define when it may serve slightly stale results and when fresh authorization/content validation is mandatory.

---

# 19. FEED CACHE

Use Redis for feed caching where justified.

Potential cache structures include:

* viewer feed page;
* candidate list;
* ranking result;
* short-lived feed metadata.

Each cache must define:

* key namespace;
* key composition;
* TTL;
* source of truth;
* invalidation;
* maximum acceptable staleness;
* memory expectations.

Do not allow feed caches to grow without bounds.

---

# 20. FEED INVALIDATION

Invalidate or bypass feed state when:

* content is deleted;
* account becomes private;
* a relationship is removed;
* a block is created;
* content is restricted;
* moderation state changes;
* content visibility changes.

Where immediate global invalidation is too expensive, rely on authorization filtering plus bounded asynchronous cleanup.

Do not use brute-force cache invalidation across millions of followers synchronously.

---

# 21. HIGH-FAN-OUT HANDLING

Implement explicit protections for high-fan-out accounts.

Do not:

* synchronously write one feed entry for every follower during publication;
* synchronously update millions of Redis keys;
* synchronously issue one downstream event per follower when avoidable.

Use asynchronous propagation, batching, hybrid fan-out, or read-time candidate inclusion as appropriate.

High-fan-out thresholds must be configurable.

---

# 22. FEED BACKPRESSURE

Background feed propagation must tolerate bursts.

Support:

* bounded worker concurrency;
* queue backpressure;
* retry;
* dead-letter behavior;
* idempotency;
* monitoring.

Do not allow an unusually viral post to exhaust the entire worker fleet.

---

# 23. FEED JOBS

Create jobs for appropriate asynchronous work such as:

* content fan-out;
* candidate cleanup;
* feed reconciliation;
* stale-entry removal.

Every job must define:

* payload;
* version;
* idempotency;
* retries;
* maximum attempts;
* failure behavior;
* observability.

---

# 24. FEED RECONCILIATION

Provide a mechanism to detect and repair inconsistencies between:

* authoritative content;
* social graph;
* feed materialization.

Examples:

* deleted content remains in a feed;
* follower relationship removed but candidate remains;
* duplicate feed candidate;
* missing candidate.

The reconciliation mechanism must be bounded and observable.

---

# 25. DISCOVERY DOMAIN

Implement a discovery backend capable of producing:

* recommended accounts;
* recommended content;
* discovery candidate sets.

Discovery must remain distinct from the personalized home feed.

Do not simply expose the home feed under a different API route.

---

# 26. RECOMMENDED ACCOUNTS

Implement a deterministic recommended-account foundation using signals such as:

* mutual relationships;
* shared engagement patterns available to the backend;
* account/content affinity where available;
* popularity signals;
* freshness;
* explicit exclusions.

Apply:

* block filtering;
* privacy rules;
* account state;
* self-account exclusion;
* existing-follow exclusion.

Do not claim machine-learning personalization.

---

# 27. RECOMMENDED CONTENT

Implement a deterministic recommended-content foundation.

Potential signals:

* popular content among relevant audiences;
* content from related accounts;
* content matching known viewer interests where the current backend has sufficient data;
* recent high-engagement content;
* content freshness.

Filter:

* blocked accounts;
* unavailable content;
* deleted content;
* private content without authorization;
* restricted content;
* already consumed/recently shown content where supported.

Do not build a fake ML service.

---

# 28. DISCOVERY CANDIDATE MODEL

Create a normalized discovery-candidate representation containing, where applicable:

* viewer;
* resource;
* candidate source;
* generated timestamp;
* score;
* eligibility metadata;
* expiration/staleness.

Do not expose raw candidate-scoring metadata to clients unless explicitly required.

---

# 29. DISCOVERY PAGINATION

Use cursor pagination for discovery results.

Define:

* deterministic ordering;
* score/tie-breaking;
* cursor encoding;
* page limits;
* eligibility filtering;
* deleted resource handling.

Do not use arbitrary offsets for large discovery collections.

---

# 30. SEARCH ARCHITECTURE

Implement the backend search foundation using the selected OpenSearch-compatible infrastructure.

Search must remain derived from authoritative PostgreSQL/domain data.

The implementation must support:

* indexing;
* querying;
* deletion;
* updates;
* reindexing;
* versioning;
* eventual consistency.

Do not make the search index the source of truth.

---

# 31. SEARCHABLE ENTITIES

Implement search support for appropriate in-scope entities:

* accounts/users;
* usernames;
* profiles;
* hashtags;
* posts/content.

Do not implement:

* message search;
* private-message indexing;
* administrative-only search.

---

# 32. USER SEARCH

Implement user/account search.

Support:

* username matching;
* display-name matching;
* normalization;
* relevant ranking;
* pagination.

Filter out:

* blocked accounts;
* deleted accounts;
* suspended accounts where policy requires;
* accounts the viewer must not discover.

---

# 33. USERNAME SEARCH

Implement canonical username search behavior.

Support:

* normalized query;
* prefix matching where appropriate;
* exact match prioritization;
* case-insensitive semantics;
* pagination.

Do not leak internal account fields through search responses.

---

# 34. HASHTAG SEARCH

Implement hashtag search.

Define:

* normalized hashtag representation;
* exact/prefix behavior;
* ranking;
* associated content discovery boundary.

The search system may return hashtag metadata, but content retrieval must still enforce current authorization.

---

# 35. CONTENT SEARCH

Implement search for content fields appropriate to the project, such as:

* caption text;
* hashtags;
* content metadata.

Apply authorization and privacy filtering.

Do not index or expose content that should not be discoverable.

Do not treat search index visibility as authoritative authorization.

---

# 36. SEARCH INDEX DOCUMENTS

Define explicit OpenSearch document representations.

Each document should contain only fields needed for search/retrieval/ranking.

Do not serialize complete database entities into search documents.

Document IDs should map deterministically to authoritative resource IDs.

Include versioning or document-generation metadata where useful.

---

# 37. INDEXING EVENTS

Consume content/account lifecycle events for search indexing.

At minimum handle concepts corresponding to:

* account created/updated/deleted;
* profile updated;
* post published/updated/deleted;
* hashtag association changes;
* content privacy changes.

Indexing must be idempotent.

Duplicate events must not create duplicate logical documents.

---

# 38. SEARCH DELETION

When an authoritative entity becomes:

* deleted;
* private/ineligible;
* suspended;
* restricted from search;

propagate the state to the search system.

If deletion is asynchronous, the API must apply authorization filtering so stale index documents cannot become a privacy leak.

---

# 39. REINDEXING

Implement a reindexing mechanism or service boundary that can:

* rebuild indexes;
* process batches;
* resume after failure;
* report progress;
* avoid unbounded memory usage;
* support controlled concurrency.

Do not require the production environment to rebuild an entire index in one synchronous request.

---

# 40. SEARCH CONSISTENCY

Document and implement expected eventual consistency.

For example:

* newly published content may not appear immediately;
* deleted content may remain temporarily in the index;
* updated usernames may take time to propagate.

The API must still enforce authoritative privacy and lifecycle checks.

---

# 41. SEARCH AUTOCOMPLETE/SUGGESTIONS

Where appropriate, implement lightweight suggestions for:

* usernames;
* hashtags.

Prioritize exact/prefix relevance and avoid expensive unbounded searches.

Do not implement a separate suggestion database unless there is a real requirement for it.

---

# 42. SEARCH CACHE

Where useful, cache high-frequency search metadata or suggestions.

Do not cache authorization-sensitive final search results broadly without a strong access-control model.

Define:

* key;
* TTL;
* invalidation;
* staleness;
* memory limits.

---

# 43. REDIS STRUCTURES

Use Redis for:

* feed caches;
* candidate buffers where justified;
* rate limiting;
* short-lived recommendation state;
* search suggestion caching where useful.

Define explicit namespaces.

Avoid using Redis as a durable feed or discovery source of truth.

---

# 44. OPENSearch FAILURE BEHAVIOR

Define graceful behavior when OpenSearch is unavailable.

For user search:

* return a safe dependency-unavailable error or appropriate limited fallback where supported.

For feed/discovery:

* do not make search availability a hard dependency unless required.

The overall platform must remain partially functional when search infrastructure is temporarily unavailable.

---

# 45. EVENT AND QUEUE INTEGRATION

Use the project's event infrastructure for:

* feed candidate propagation;
* feed invalidation;
* search indexing;
* search deletion;
* discovery updates.

Use background jobs for:

* fan-out;
* reindexing;
* reconciliation;
* large candidate computations.

Events and jobs must remain distinct.

---

# 46. TRANSACTIONAL CONSISTENCY

When an authoritative content or relationship transaction must reliably trigger feed/search work:

* persist the business state;
* persist the durable outbound event using the existing outbox strategy;
* process asynchronously.

Do not require OpenSearch or feed propagation to succeed before the primary database transaction is committed.

---

# 47. AUTHORIZATION

Feed, discovery, and search retrieval must consider current:

* account privacy;
* following state;
* block state;
* mute state;
* restriction state;
* content visibility;
* content lifecycle;
* moderation restrictions where available.

Do not assume derived indexes are current enough to replace authorization checks.

---

# 48. PRIVACY CHANGES

Handle scenarios where:

* a public account becomes private;
* a user blocks another user;
* a follower relationship is removed;
* content is deleted;
* content becomes restricted.

Derived data may remain temporarily stale.

The backend must prevent that stale state from creating an unauthorized response.

---

# 49. API SURFACE

Implement APIs equivalent to:

## Home Feed

* retrieve home feed;
* retrieve next feed page.

## Discovery

* retrieve recommended accounts;
* retrieve recommended content;
* retrieve discovery page.

## Search

* search users;
* search usernames;
* search hashtags;
* search content;
* search suggestions where supported.

Use repository-established route/version conventions.

---

# 50. FEED RESPONSE MODEL

A feed item should contain only client-consumable information such as:

* content identifier;
* author/profile summary;
* media references;
* caption summary/required content;
* timestamps;
* engagement summaries where existing backend contracts permit;
* feed metadata that is safe for client use.

Do not expose:

* internal ranking scores;
* candidate-source internals;
* database keys;
* search-engine document IDs;
* infrastructure details.

---

# 51. DISCOVERY RESPONSE MODEL

Recommended accounts/content must return stable domain objects or references.

Do not return raw ranking implementation details.

For content results:

* revalidate current authorization;
* return canonical content/media structures;
* preserve consistent API contracts with normal content retrieval.

---

# 52. SEARCH RESPONSE MODEL

Search responses must contain:

* resource identifier;
* safe display metadata;
* relevance-related information only where appropriate;
* pagination information.

Do not expose internal search-engine fields.

Do not expose private account details merely because they exist in the search document.

---

# 53. RATE LIMITING

Protect:

* feed retrieval;
* discovery retrieval;
* search;
* reindex operations;
* expensive recommendation endpoints.

Use different controls for:

* normal client traffic;
* administrative/reindex operations;
* suspicious high-volume requests.

Reindexing must never be publicly accessible.

---

# 54. ABUSE PROTECTION

Consider:

* search scraping;
* automated account enumeration;
* feed scraping;
* discovery harvesting;
* expensive query patterns.

Apply:

* pagination limits;
* query length limits;
* result limits;
* rate limits;
* authorization;
* query normalization.

Do not expose unrestricted search endpoints.

---

# 55. PERFORMANCE

Optimize for:

* low-latency feed retrieval;
* bounded candidate generation;
* efficient batch authorization;
* minimal database round trips;
* cache reuse;
* efficient search queries;
* bounded OpenSearch result sizes;
* asynchronous large-scale work.

Prevent:

* N+1 content retrieval;
* one-request-per-following candidate generation;
* unbounded search queries;
* unbounded Redis lists;
* full-table feed construction per request.

---

# 56. DATABASE DESIGN

Implement persistent structures necessary for:

* feed candidates/materialization where selected;
* discovery candidates where needed;
* recommendation state where durable;
* search indexing metadata where useful;
* reconciliation state.

Do not duplicate entire post/account records unnecessarily.

Derived data must be clearly identifiable.

Use foreign-key/reference strategies appropriate to the repository's architecture.

---

# 57. FEED DATA RETENTION

Define bounded retention for materialized feed state.

Do not retain infinite historical feed candidates for every user.

Use:

* TTL;
* bounded list size;
* archival/cleanup;
* candidate expiration.

Retention values must be configurable.

---

# 58. DISCOVERY DATA RETENTION

Recommendation candidates are derived.

They should have controlled lifecycle and expiration.

Do not let obsolete recommendations remain indefinitely.

Refresh recommendation candidates based on explicit scheduling or event triggers.

---

# 59. SEARCH INDEX LIFECYCLE

Implement index management that supports:

* versioned mappings;
* controlled index creation;
* aliases where appropriate;
* reindexing;
* migration;
* rollback.

Do not alter an existing production index mapping destructively without an appropriate migration approach.

---

# 60. CONCURRENCY AND IDEMPOTENCY

Handle:

* duplicate feed propagation events;
* duplicate search-index events;
* duplicate reindex jobs;
* content deletion racing with indexing;
* relationship changes racing with feed generation;
* repeated recommendation generation.

Use:

* idempotent consumers;
* deterministic document IDs;
* unique constraints;
* job deduplication;
* event versioning.

---

# 61. OBSERVABILITY

Instrument:

## Feed

* candidate-generation latency;
* ranking latency;
* feed-read latency;
* cache hit/miss;
* candidate-processing throughput;
* queue depth;
* dropped/ineligible candidates.

## Search

* query latency;
* index lag;
* indexing failures;
* deletion lag;
* search errors;
* result counts.

## Discovery

* generation latency;
* cache behavior;
* candidate freshness;
* recommendation generation failures.

Do not put private search queries or sensitive user content into logs unnecessarily.

---

# 62. FAILURE BEHAVIOR

Handle failures for:

* Redis unavailable;
* PostgreSQL unavailable;
* Kafka/event streaming unavailable;
* queue unavailable;
* OpenSearch unavailable;
* ranking component failure;
* feed propagation backlog;
* indexing backlog.

Examples:

* if Redis fails, fall back to authoritative stores where safe;
* if search fails, return a safe dependency error rather than fabricate results;
* if asynchronous feed propagation fails, queue/retry rather than blocking content publication.

Do not silently return incorrect recommendations.

---

# 63. RECONCILIATION

Create mechanisms to reconcile:

* feed state with authoritative content/relationships;
* search indexes with authoritative entities;
* recommendation candidates with current account/content state.

Reconciliation must be:

* bounded;
* retryable;
* observable;
* safe to rerun.

---

# 64. TESTING STRATEGY

Create real tests.

## Unit Tests

Cover:

* feed eligibility;
* ranking;
* candidate generation;
* privacy filtering;
* high-fan-out rules;
* search normalization;
* search filtering;
* recommendation exclusion rules;
* pagination;
* cache-key generation.

## Integration Tests

Cover:

* feed candidate persistence;
* feed retrieval;
* cache behavior;
* event-driven feed updates;
* search indexing;
* search deletion;
* OpenSearch query behavior;
* reindex processing;
* Redis mechanisms.

## API Tests

Cover:

* feed retrieval;
* pagination;
* discovery;
* user search;
* username search;
* hashtag search;
* content search;
* authorization.

---

# 65. SECURITY TESTING

Test:

* blocked account excluded from feed;
* private content excluded from unauthorized feed;
* private profile excluded from unauthorized search;
* deleted content excluded;
* stale search document cannot bypass authorization;
* unauthorized reindex endpoint blocked;
* query length/size restrictions;
* feed scraping rate limits;
* search scraping rate limits.

---

# 66. PERFORMANCE VALIDATION

Perform targeted validation for:

* feed retrieval with realistic candidate counts;
* Redis feed caching;
* cursor pagination;
* high-fan-out candidate generation;
* search latency;
* batch search indexing;
* deletion propagation;
* recommendation generation.

Record actual conditions.

Do not claim global-scale performance based on local testing.

---

# 67. DOCUMENTATION

Create or update documentation for:

* feed architecture implementation;
* candidate-generation behavior;
* ranking foundation;
* cache behavior;
* high-fan-out handling;
* discovery;
* search;
* index lifecycle;
* reindexing;
* event consumers;
* background jobs;
* privacy/authorization behavior;
* operational troubleshooting;
* testing.

Documentation must describe actual implementation.

---

# 68. PORTABLE CONTRACTS

Maintain explicit contracts for:

* feed entry;
* candidate;
* ranking input/output;
* discovery result;
* recommendation result;
* search result;
* search index documents;
* indexing events;
* deletion events;
* feed jobs;
* reconciliation jobs.

Contracts must be usable by later web, mobile, infrastructure, QA, moderation, notification, and analytics work.

---

# 69. CROSS-PART COMPATIBILITY

Preserve compatibility with:

* account/profile;
* social graph;
* content;
* media;
* engagement;
* moderation;
* notifications;
* analytics;
* web;
* mobile;
* infrastructure.

The feed must consume canonical content and engagement contracts rather than duplicating their persistence logic.

Search must consume canonical content/account events rather than inventing alternate data ownership.

---

# 70. NO FAKE COMPLETENESS

Do not implement:

* fake machine-learning models;
* hardcoded recommendations pretending to be personalized;
* fake search results;
* static feed arrays;
* mock OpenSearch behavior in production paths;
* hardcoded rankings;
* placeholder background workers;
* TODO/FIXME gaps;
* pseudo-code.

Deterministic algorithms are acceptable where they implement real, explainable current-scope behavior.

---

# 71. VALIDATION

Before completion:

1. run formatting;
2. run linting;
3. run type checking;
4. validate migrations;
5. run unit tests;
6. run integration tests;
7. run API/contract tests;
8. run security tests;
9. run performance-oriented tests where available;
10. validate feed/search contracts;
11. validate event consumers;
12. validate documentation.

If OpenSearch, Kafka, or other external infrastructure is unavailable, clearly distinguish code-level validation from unavailable environment validation.

Do not claim external integration success without actual execution.

---

# 72. IMPLEMENTATION REPORT

After implementation, provide a completion report containing:

## Files Created

List every file created.

## Files Modified

List every file modified.

## Files Deleted

List every file deleted, if any.

## Backend Domains Implemented

Summarize:

* home feed;
* feed candidates;
* ranking foundation;
* discovery;
* recommendations;
* search;
* indexing;
* caching.

## Database Changes

List:

* tables;
* indexes;
* constraints;
* migrations;
* derived-state structures.

## Redis Changes

List:

* feed keys;
* discovery/recommendation keys;
* search caches;
* TTLs;
* invalidation behavior.

## OpenSearch Changes

List:

* indexes;
* mappings;
* aliases;
* document models;
* indexing/deletion behavior.

## Event Changes

List:

* consumed events;
* produced events;
* event schemas;
* idempotency behavior.

## Queue/Job Changes

List:

* feed jobs;
* indexing jobs;
* reindex jobs;
* reconciliation jobs.

## Security Changes

Summarize:

* privacy filtering;
* authorization;
* scraping controls;
* rate limits.

## Tests Created

List test categories and important scenarios.

## Tests Executed

State exactly which tests were executed.

## Validation Performed

State exact validation performed.

## Documentation Changes

List documentation created or updated.

## Integration Considerations

Explain how web, mobile, engagement, moderation, notification, analytics, and infrastructure systems consume the feed/discovery/search contracts.

## Compatibility Considerations

Identify compatibility-sensitive changes.

## Known Limitations

List genuine limitations.

## Unresolved Issues

List only issues that remain unresolved.

---

# 73. DEFINITION OF DONE

This backend milestone is complete only when:

* home-feed retrieval works;
* feed candidate generation works;
* feed eligibility filtering works;
* current privacy and relationship state is respected;
* deterministic ranking foundation works;
* cursor pagination works;
* feed deduplication works;
* feed caching works where configured;
* cache invalidation/fallback behavior is defined;
* high-fan-out handling exists;
* feed propagation jobs work;
* feed jobs are idempotent;
* feed reconciliation exists;
* discovery candidate generation works;
* recommended-account retrieval works;
* recommended-content retrieval works;
* inappropriate/self/already-followed/blocked content is excluded;
* user search works;
* username search works;
* hashtag search works;
* content search works;
* search indexing works;
* search deletion works;
* reindexing is supported;
* stale indexes cannot bypass authorization;
* OpenSearch integration is bounded behind explicit interfaces;
* Redis usage is bounded;
* relevant events are consumed/produced correctly;
* background jobs are retryable and observable;
* rate limits exist for expensive APIs;
* security tests exist;
* unit tests exist;
* integration tests exist;
* API/contract tests exist;
* performance validation is performed where practical;
* migrations validate;
* documentation reflects actual implementation;
* no production secrets are committed;
* no fake recommendation/search/feed implementation exists;
* no intentional implementation gaps remain inside the defined scope.

---

# 74. FINAL IMPLEMENTATION DISCIPLINE

Implement **only the current prompt's scope**.

Do not implement:

* direct messaging;
* notification delivery;
* notification preferences;
* creator analytics;
* advertising;
* moderation workflows;
* administration;
* web UI;
* mobile UI;
* full infrastructure provisioning;
* machine-learning training pipelines;
* message search.

Do not redesign:

* account identity;
* profile;
* social graph;
* post/content;
* media;
* engagement

unless a concrete compatibility issue within this scope requires a narrowly scoped adjustment.

Do not assume another AI prompt has been executed.

Do not depend on another AI conversation.

Do not expose internal ranking or search infrastructure to clients.

Do not claim production-scale performance or infrastructure availability without actual validation.

Produce real, tested, documented backend functionality for Instagram's feed, discovery, recommendation, and search systems.
