# PROJECT 1 — INSTAGRAM-LIKE GLOBAL SOCIAL PLATFORM

# BACKEND PROMPT — VOLUME 3

# FEEDS, DISCOVERY, SEARCH, RECOMMENDATIONS, NOTIFICATIONS & ASYNCHRONOUS PROCESSING

You are the Staff Backend Engineering team responsible for implementing the feed, discovery, search, recommendation, notification, event-processing, and related backend systems of a production-grade Instagram-like global social platform.

This prompt is fully standalone. It does not depend on any other prompt, document, previous conversation, previous implementation, previous architecture, previous volume, approval, or hidden context.

You must inspect the current repository before making changes and integrate with compatible existing implementation.

Repository state is the source of truth for existing code.

Implement real production functionality.

Do not generate pseudo-code.

Do not create placeholder implementations.

Do not use TODO/FIXME as substitutes for required behavior.

Do not claim functionality exists when it has not been implemented.

Do not regenerate unchanged files.

Preserve working unrelated functionality.

==================================================

1. BACKEND SCOPE
   ==================================================

Implement the backend systems required for:

- home feed
- following feed
- feed candidate generation
- feed fanout
- feed ranking
- feed hydration
- personalized discovery
- recommendation signals
- user search
- hashtag search
- content search
- autocomplete
- trending discovery
- notification persistence
- notification aggregation
- push-notification orchestration
- asynchronous domain-event processing
- Kafka/Redpanda integration
- BullMQ workers
- OpenSearch/Elasticsearch synchronization
- distributed caching
- high-volume background processing
- feed consistency and privacy enforcement
- observability of all critical asynchronous workflows

==================================================
2. REQUIRED TECHNOLOGY
======================

Backend:

- Node.js
- NestJS
- TypeScript

Persistence:

- PostgreSQL
- Prisma ORM

Caching:

- Redis

Event streaming:

- Kafka or Redpanda

Background jobs:

- BullMQ

Search:

- OpenSearch or Elasticsearch

Media integration:

- AWS S3
- CloudFront

Push notifications:

- Firebase Cloud Messaging
- Apple Push Notification service

Real-time integration:

- Socket.IO
- WebSockets

Observability:

- OpenTelemetry
- Prometheus
- Grafana
- Loki
- Tempo

==================================================
3. DOMAIN MODULES
=================

Create or integrate modules for:

- feed
- feed-candidates
- feed-ranking
- discovery
- recommendations
- search
- hashtags
- trending
- notifications
- push-notifications
- events
- event-consumers
- background-jobs
- cache
- moderation integration

Maintain clear domain boundaries.

Do not move unrelated business logic into these modules.

==================================================
4. EVENT-DRIVEN FOUNDATION
==========================

Use Kafka or Redpanda for asynchronous domain-event propagation.

Support events including:

- UserRegistered
- ProfileUpdated
- FollowCreated
- FollowRemoved
- UserBlocked
- UserUnblocked
- UserMuted
- UserUnmuted
- UserRestricted
- PostCreated
- PostUpdated
- PostDeleted
- ReelPublished
- StoryCreated
- StoryExpired
- PostLiked
- PostUnliked
- CommentCreated
- CommentDeleted
- PostSaved
- PostUnsaved
- PostShared
- MessageCreated
- ReportCreated
- ModerationDecisionApplied

Events must support:

- event ID
- event type
- event version
- aggregate ID
- actor ID where appropriate
- timestamp
- correlation ID
- trace ID
- payload

Never publish:

- passwords
- access tokens
- refresh tokens
- raw credentials
- unnecessary private message contents

==================================================
5. OUTBOX PROCESSING
====================

Use an outbox-style pattern for critical domain events.

The transactional workflow should be:

database transaction
→ authoritative state mutation
→ outbox record

Then:

outbox
→ Kafka/Redpanda
→ consumers

Publishing failure must not cause the original transaction to be rolled back after the business operation has succeeded.

Outbox processing must support:

- retry
- backoff
- monitoring
- replay
- duplicate protection
- failure classification

==================================================
6. EVENT CONSUMER IDEMPOTENCY
=============================

Consumers must assume at-least-once delivery.

Every side effect should be idempotent where practical.

Use:

- event IDs
- consumer checkpoints
- unique constraints
- deduplication records
- deterministic writes

Consumers must not create duplicate:

- notifications
- feed entries
- search documents
- recommendation events
- analytics records

==================================================
7. FEED ARCHITECTURE
====================

Implement a scalable hybrid feed.

The feed should combine:

- followed-account content
- relationship signals
- freshness
- engagement
- content quality
- personalized relevance

Use an architecture that can combine:

- fanout-on-write
- fanout-on-read
- candidate generation
- ranking

Do not force every followed user into synchronous fanout.

==================================================
8. FOLLOWED-CONTENT FANOUT
==========================

When a user creates eligible content:

PostCreated
→ determine distribution strategy
→ generate candidate feed updates
→ process asynchronously

For normal accounts, asynchronous fanout may be appropriate.

For extremely high-follower accounts, avoid creating a huge synchronous write amplification event.

Use read-time candidate expansion or specialized treatment where appropriate.

==================================================
9. CELEBRITY / HIGH-DEGREE ACCOUNTS
===================================

Support users with very large follower counts.

Do not create a workflow such as:

new post
→ synchronous write to millions of feed rows

Instead use a strategy where high-degree creators are incorporated at read time or through controlled asynchronous fanout.

The threshold for high-degree treatment must be configuration-driven.

==================================================
10. FEED CANDIDATE MODEL
========================

A feed candidate should contain enough information for efficient ranking without duplicating entire posts.

Potential information:

- content ID
- author ID
- candidate source
- creation time
- relationship signal
- preliminary engagement signal
- relevance metadata
- eligibility state
- ranking features

Do not store sensitive private content directly inside feed caches when it can create privacy risk.

==================================================
11. FEED ELIGIBILITY
====================

Before returning a feed item, verify eligibility based on:

- content existence
- content deletion
- author account state
- visibility
- follow relationship
- blocked relationship
- muted author
- restriction rules
- moderation state
- story/reel/post state
- media availability

Stale candidates must be filtered.

Feed caches must never override authoritative privacy decisions.

==================================================
12. FEED RANKING
================

Ranking may consider:

- freshness
- user-author affinity
- previous engagement
- content engagement quality
- relationship strength
- content type
- historical interaction
- negative feedback
- frequency controls

Ranking logic must remain deterministic enough for debugging and experimentation.

Feature computation must have bounded latency.

==================================================
13. RANKING FAILURE
===================

If ranking dependencies fail or exceed their latency budget:

- return a safe fallback feed
- preserve authorization
- preserve privacy
- avoid blocking the entire application
- record telemetry

A ranking failure must not result in exposing unauthorized content.

==================================================
14. FEED HYDRATION
==================

Avoid N+1 database requests.

Given a set of ranked content IDs:

- batch-load posts
- batch-load authors
- batch-load media metadata
- batch-load engagement summaries
- batch-load relationship state

Assemble response DTOs efficiently.

Limit database round trips.

==================================================
15. FEED PAGINATION
===================

Use cursor pagination.

A cursor should encode enough information to maintain stable retrieval semantics without exposing internal database structure.

Protect against:

- modified cursors
- invalid cursors
- cursor expiration where required
- duplicate items across pages

Define deterministic tie-breakers for items with identical timestamps.

==================================================
16. FEED DEDUPLICATION
======================

Prevent duplicated content in one feed page.

Deduplicate by logical content identity.

Handle cases where one content item appears through multiple candidate sources.

Prefer deterministic prioritization of candidate sources.

==================================================
17. FEED CACHE
==============

Redis may cache:

- candidate feed items
- recent feed pages where appropriate
- ranking features
- relationship-derived signals

Do not cache complete private responses indefinitely.

Use short TTLs or invalidation where necessary.

Cache design must account for:

- stampede prevention
- bounded memory
- hot keys
- expiration
- versioning

==================================================
18. CACHE STAMPEDE PROTECTION
=============================

When a hot feed or profile cache expires:

do not allow every concurrent request to regenerate the same expensive result.

Use suitable mechanisms such as:

- request coalescing
- short locking
- stale-while-revalidate
- jittered TTLs

Do not create distributed lock deadlocks.

==================================================
19. FOLLOWING FEED
==================

Provide an explicit following-content feed.

It should support chronological or controlled ranking behavior.

Respect:

- privacy
- block
- mute
- restriction
- content deletion
- account suspension

Use cursor pagination.

==================================================
20. DISCOVERY FEED
==================

Implement discovery mechanisms for content outside the direct social graph.

Candidate sources may include:

- popular content
- similar content
- creator affinity
- hashtags
- trending content
- engagement patterns
- user interests

Discovery must be privacy-aware.

Do not recommend blocked or inaccessible content.

==================================================
21. RECOMMENDATION SIGNALS
==========================

Capture useful signals such as:

- impressions
- opens
- likes
- comments
- saves
- shares
- follows after viewing
- dwell or watch duration where product policy permits
- hides
- not-interested feedback
- profile visits

Store raw high-volume analytics through asynchronous pipelines rather than slowing user requests.

==================================================
22. RECOMMENDATION SAFETY
=========================

Recommendations must not expose:

- deleted content
- private content to unauthorized users
- blocked users
- moderation-rejected content
- suspended accounts
- content the viewer is prohibited from accessing

Recommendation systems are derived systems.

Authorization remains authoritative.

==================================================
23. SEARCH ARCHITECTURE
=======================

Use OpenSearch or Elasticsearch.

Create appropriate indexes for:

- users/profiles
- hashtags
- posts
- reels
- creators

Search documents must contain only data intended for indexing.

==================================================
24. PROFILE INDEXING
====================

Index appropriate public profile data such as:

- user ID
- normalized username
- display name
- searchable biography fields where appropriate
- creator metadata
- profile status

Do not index:

- password-related fields
- session information
- private contact details
- security metadata

==================================================
25. CONTENT INDEXING
====================

Posts and reels may be indexed with:

- content ID
- author
- caption
- hashtags
- searchable metadata
- content type
- moderation state
- publication timestamp

Search documents must not become authoritative for visibility.

==================================================
26. INDEX UPDATE EVENTS
=======================

Use events such as:

ProfileUpdated
PostCreated
PostUpdated
PostDeleted
ReelPublished
ModerationDecisionApplied
UserBlocked
UserUnblocked

Consumers should update search indexes asynchronously.

==================================================
27. INDEX CONSISTENCY
=====================

Search is eventually consistent.

A profile or post update must succeed even if OpenSearch is temporarily unavailable.

Indexing failures must:

- retry
- back off
- enter dead-letter handling if necessary
- be observable
- remain replayable

==================================================
28. INDEX REBUILD
=================

Provide a rebuild strategy.

The search index must be reconstructible from authoritative data.

Do not design a system where a corrupted search index permanently loses searchable content.

Rebuild workflows must be:

- resumable
- observable
- bounded
- rate-limited
- safe to run alongside production traffic

==================================================
29. SEARCH PRIVACY
==================

Before returning a search result, ensure the result remains eligible.

Search results must account for:

- account visibility
- private accounts
- blocked users
- deleted content
- suspended users
- moderation state

A stale search result must not become a privacy bypass.

==================================================
30. SEARCH PAGINATION
=====================

Use search-engine-compatible cursor/search-after pagination for large result sets where appropriate.

Avoid deep unrestricted pagination.

Bound:

- query size
- requested page size
- expensive sort operations

==================================================
31. AUTOCOMPLETE
================

Implement autocomplete for suitable entities such as:

- usernames
- hashtags

Autocomplete must:

- be latency-sensitive
- have bounded query length
- support normalization
- prevent abuse
- avoid returning unauthorized/deleted accounts

Cache popular safe results where appropriate.

==================================================
32. TRENDING HASHTAGS
=====================

Design trending calculations as asynchronous aggregation.

Signals may include:

- post volume
- growth rate
- engagement
- recency

Do not calculate expensive global trends synchronously during user requests.

Define abuse-resistant aggregation rules to reduce spam manipulation.

==================================================
33. NOTIFICATION DOMAIN
=======================

Implement durable Notification records.

Support categories including:

- follows
- follow requests
- likes
- comments
- replies
- mentions
- story interactions
- system events
- messages

Notifications must identify:

- recipient
- notification type
- actor where applicable
- target content where applicable
- created timestamp
- read state
- aggregation/group state

==================================================
34. NOTIFICATION CREATION
=========================

Notification flow:

domain event
→ notification policy
→ authorization/privacy check
→ preference check
→ deduplication/aggregation
→ notification persistence
→ push job
→ optional real-time event

Notification persistence should not depend on push-provider availability.

==================================================
35. NOTIFICATION AGGREGATION
============================

Support aggregation for high-volume events.

Example:

multiple likes on the same content
→ grouped notification state

Do not generate unlimited notifications for rapid automated interaction.

Aggregation rules must be deterministic.

==================================================
36. NOTIFICATION DEDUPLICATION
==============================

Avoid duplicate notifications caused by:

- duplicate Kafka events
- worker retries
- API retries
- consumer restarts

Use durable idempotency keys derived from event identity and notification semantics.

==================================================
37. NOTIFICATION PREFERENCES
============================

Support user-configurable preferences for categories such as:

- likes
- comments
- follows
- mentions
- messages
- system notifications

Preference changes must be evaluated before push dispatch.

==================================================
38. PUSH DEVICE MODEL
=====================

Track push-capable devices.

Store:

- user ID
- device ID
- platform
- push token
- token status
- app version where useful
- last active timestamp

Avoid treating push tokens as permanent.

==================================================
39. PUSH NOTIFICATION PIPELINE
==============================

Use BullMQ for push delivery jobs.

Workflow:

notification
→ eligibility/preferences
→ push job
→ provider
→ provider result
→ token state update

Implement:

- retry
- exponential backoff
- invalid-token handling
- provider outage handling
- rate limits
- delivery metrics

==================================================
40. FCM / APNS INTEGRATION
==========================

Use provider adapters.

Business logic should not depend directly on provider-specific request formats.

Define an abstraction for:

- send
- failure mapping
- invalid token
- retryable error
- permanent error

Provider credentials must remain server-side.

==================================================
41. PUSH DELIVERY FAILURE
=========================

If FCM/APNS fails:

- preserve durable notification
- classify error
- retry transient failures
- stop sending to invalid devices
- emit telemetry

Do not delete notifications merely because push failed.

==================================================
42. REAL-TIME NOTIFICATIONS
===========================

Where supported, new notifications may also be delivered through authenticated WebSocket connections.

Real-time delivery is supplemental.

The durable Notification record remains authoritative.

A reconnecting client must retrieve missed notifications through the API.

==================================================
43. BACKGROUND JOB QUEUES
=========================

Use separate BullMQ queues where workload characteristics differ.

Recommended categories:

- feed-fanout
- feed-ranking-support
- search-indexing
- notification
- push-notification
- trending
- analytics
- cleanup

Each queue requires:

- concurrency limits
- retry policy
- timeout
- backoff
- dead-letter handling
- metrics

==================================================
44. QUEUE PRIORITIES
====================

Prioritize user-visible operations appropriately.

Examples:

Higher priority:

- push notifications
- critical feed updates
- security events

Lower priority:

- historical analytics aggregation
- long-running index rebuilds
- non-critical cleanup

Do not starve lower-priority work indefinitely.

==================================================
45. EVENT RETRIES
=================

Retries must be bounded.

Use exponential backoff where useful.

Differentiate:

- transient dependency failure
- invalid payload
- authorization failure
- permanently invalid event
- infrastructure failure

Permanent failures should not loop forever.

==================================================
46. DEAD-LETTER HANDLING
========================

Persist failed messages/jobs in a recoverable dead-letter system.

Dead-letter records should include:

- original identifier
- failure category
- attempt count
- last error classification
- timestamps
- relevant safe metadata

Provide operational procedures for inspection and replay.

Never store secrets in dead-letter payloads.

==================================================
47. EVENT ORDERING
==================

Where ordering matters, preserve ordering by appropriate aggregate key.

Examples:

- content lifecycle
- relationship lifecycle
- message lifecycle

Do not assume global event ordering across all users and domains.

==================================================
48. ANALYTICS EVENTS
====================

Capture asynchronous events for:

- feed impressions
- content views
- reel plays
- story views
- likes
- comments
- saves
- shares
- profile visits
- follows
- searches
- notification interactions

Analytics must not block the main user request path.

==================================================
49. ANALYTICS DATA PROTECTION
=============================

Analytics events must:

- minimize unnecessary personal data
- avoid raw credentials
- avoid secrets
- use stable identifiers where appropriate
- support retention policies

Do not log sensitive private message content merely for analytics.

==================================================
50. REDIS DESIGN
================

Use Redis for suitable high-speed state such as:

- feed candidate caches
- ranking feature caches
- autocomplete caches
- trending caches
- notification unread counts
- rate limiting
- deduplication
- short-lived locks
- job coordination

Define TTL and invalidation for every cache class.

==================================================
51. UNREAD NOTIFICATION COUNT
=============================

Support an efficient unread count.

The count may be cached/derived.

Authoritative notification state remains durable.

Handle concurrent:

- notification creation
- notification read
- bulk mark-read

without producing negative or impossible counts.

==================================================
52. MARK NOTIFICATIONS READ
===========================

Support:

- mark one read
- mark multiple read
- mark all read

Operations must be idempotent.

Do not allow users to mark another user's notifications.

==================================================
53. SEARCH RATE LIMITING
========================

Protect search and autocomplete against abuse.

Use limits based on:

- user
- IP
- device where appropriate

Prevent expensive queries by enforcing:

- minimum query quality
- maximum query length
- bounded filters
- bounded result size

==================================================
54. FEED RATE LIMITING
======================

Protect feed endpoints against:

- rapid refresh
- scraping
- automated pagination
- cursor abuse

Use cache-friendly request policies where possible.

Do not allow limits to prevent ordinary user refresh behavior unnecessarily.

==================================================
55. HIGH-TRAFFIC CONTENT
========================

For viral content, avoid making one database object the bottleneck.

Use:

- cached content summaries
- asynchronous counter aggregation
- distributed cache
- batched ranking signals
- rate-limited secondary processing

Do not make every impression synchronously update one database row.

==================================================
56. COUNTER AGGREGATION
=======================

High-volume counters may use:

- Redis atomic increments
- sharded counters
- event streams
- periodic durable aggregation

The displayed count may be eventually consistent.

The underlying interaction records must remain correct.

==================================================
57. FEED INVALIDATION
=====================

Content state changes should invalidate or suppress relevant feed candidates.

Examples:

PostDeleted
→ remove/invalidate candidate

UserBlocked
→ suppress blocked-user content

PrivacyChange
→ recompute eligibility

ModerationDecisionApplied
→ suppress prohibited content

Do not depend on eventual invalidation alone for authorization.

==================================================
58. USER MUTE INTEGRATION
=========================

When a user mutes another user:

- feed candidate generation must suppress applicable content
- discovery should suppress where appropriate
- recommendations should incorporate the negative signal
- existing cached results must expire/invalidate

Mute state is user-specific.

==================================================
59. BLOCK INTEGRATION
=====================

When a block is created:

- feed candidates must be filtered
- search results must be filtered
- recommendations must be filtered
- notification generation must avoid prohibited interactions
- messaging access must remain blocked where applicable

Block state must be authoritative.

==================================================
60. PRIVATE ACCOUNT INTEGRATION
===============================

Feed/discovery/search pipelines must respect private accounts.

Private content must not leak through:

- cached candidates
- search documents
- recommendations
- notifications
- trending systems

==================================================
61. MODERATION INTEGRATION
==========================

Moderation state must affect:

- feed eligibility
- search eligibility
- recommendations
- notifications
- trending
- content discovery

Moderated content must be removed from derived systems asynchronously.

Until derived systems update, request-time authorization and moderation checks must protect access.

==================================================
62. OBSERVABILITY
=================

Instrument:

- Kafka/Redpanda producers
- Kafka/Redpanda consumers
- BullMQ jobs
- feed generation
- ranking
- search
- notification creation
- push delivery
- Redis
- PostgreSQL
- OpenSearch/Elasticsearch

Measure:

- feed latency
- ranking latency
- candidate generation latency
- queue depth
- queue wait time
- consumer lag
- search latency
- push success/failure
- notification creation rate
- duplicate-event rate
- dead-letter volume

==================================================
63. DISTRIBUTED TRACING
=======================

Propagate correlation and trace context across:

HTTP
→ application
→ database
→ outbox
→ Kafka/Redpanda
→ consumer
→ BullMQ
→ external provider

A production incident must be traceable across asynchronous boundaries.

==================================================
64. FAILURE ISOLATION
=====================

The following failures must not unnecessarily prevent core user operations:

Search failure must not prevent post creation.

Notification provider failure must not prevent notification persistence.

Ranking failure must not prevent content creation.

Kafka consumer lag must not make profile APIs unusable.

OpenSearch failure must not become the source of truth for access.

Push-provider outage must not destroy durable notifications.

==================================================
65. RECOVERY
============

All derived systems must be reconstructible.

Feed candidates may be rebuilt.

Search indexes may be rebuilt.

Recommendation caches may be rebuilt.

Notification push state may be retried.

Redis caches may be discarded and regenerated.

Do not make Redis-only data authoritative for critical durable business state.

==================================================
66. TESTING
===========

Implement automated tests covering:

Feed:

- pagination
- candidate generation
- ranking
- privacy
- deletion
- block
- mute
- private account
- duplicate prevention
- fallback behavior

Search:

- indexing
- deletion
- privacy
- autocomplete
- pagination
- index rebuild

Notifications:

- creation
- deduplication
- aggregation
- preferences
- unread counts
- mark read
- provider failure

Events:

- publication
- duplicate delivery
- consumer retries
- ordering
- dead-letter handling

Queues:

- retry
- timeout
- failure
- idempotency
- concurrency limits

==================================================
67. SECURITY TESTING
====================

Test:

- private-content search bypass
- deleted-content search bypass
- blocked-user discovery bypass
- muted-user suppression
- unauthorized notification access
- push-token abuse
- cursor manipulation
- oversized search queries
- feed scraping
- event replay
- duplicate job execution
- unauthorized ranking-data access

==================================================
68. PERFORMANCE TESTING
=======================

Test realistic scenarios:

- large follow graphs
- high-degree creators
- viral post
- large feed page
- concurrent feed requests
- concurrent search
- mass notifications
- notification bursts
- Kafka lag
- queue backlog
- OpenSearch latency
- Redis cache loss
- ranking dependency failure

==================================================
69. ACCEPTANCE CRITERIA
=======================

This implementation is complete only when:

- feed architecture is implemented
- following feed works
- candidate generation works
- hybrid fanout strategy works
- high-degree accounts are handled safely
- ranking is implemented
- ranking fallback exists
- feed hydration avoids N+1 behavior
- cursor pagination works
- feed deduplication works
- cache strategy works
- discovery works
- recommendations work
- search works
- profile indexing works
- content indexing works
- search privacy is enforced
- autocomplete works
- trending aggregation exists
- notifications persist correctly
- notification aggregation works
- notification deduplication works
- notification preferences work
- unread counts work
- push device management works
- FCM/APNS adapters work
- push retries and invalid-token handling work
- real-time notification integration works where applicable
- Kafka/Redpanda event processing works
- BullMQ queues/workers work
- retry and dead-letter handling works
- analytics events are processed asynchronously
- Redis caching is implemented
- block/mute/privacy integration works
- moderation integration works
- observability exists
- tests cover critical paths
- TypeScript compiles
- database migrations succeed
- no required functionality remains a placeholder

==================================================
70. IMPLEMENTATION FINISHING RULE
=================================

Do not stop after creating module structures, schemas, or interfaces.

Implement the actual working behavior.

Inspect the repository first.

Reuse compatible components.

Integrate with existing backend infrastructure.

Modify only the files needed.

Validate:

- formatting
- linting
- type checking
- Prisma schema/migrations
- API behavior
- event publication
- event consumers
- BullMQ workers
- search integration
- Redis behavior
- unit tests
- integration tests
- security tests
- performance-critical paths

The resulting backend must provide a real, scalable feed, discovery, search, recommendation, notification, and asynchronous-processing subsystem.
