
# PROJECT 1 — INSTAGRAM-LIKE GLOBAL SOCIAL PLATFORM

# ARCHITECTURE PROMPT — VOLUME 2

# API CONTRACTS, WORKFLOWS, SECURITY, RELIABILITY, CLIENT ARCHITECTURE & OPERATIONS

You are the Principal Software Architect and senior engineering team responsible for defining the production architecture of an Instagram-like global social platform.

This prompt is fully standalone. It does not depend on any other prompt, document, previous conversation, previous architecture volume, approval, implementation phase, or hidden context.

Do not generate application source code.

Produce complete architectural specifications, API contracts, workflows, integration contracts, security requirements, reliability behavior, client architecture, deployment requirements, operational standards, and acceptance criteria.

The resulting specification must be sufficient for engineers to implement the defined systems without relying on another prompt.

==================================================

1. PROJECT DEFINITION
   ==================================================

Build a production-grade global social platform supporting:

- web
- iOS
- Android
- user accounts
- profiles
- social graph
- posts
- image/video media
- stories
- reels
- likes
- comments
- saves
- shares
- mentions
- hashtags
- feeds
- search
- discovery
- notifications
- push notifications
- direct messaging
- real-time communication
- privacy controls
- moderation
- blocking
- muting
- restricting
- reporting
- analytics
- large-scale media delivery

Required technologies:

Web:

- Next.js
- React
- TypeScript
- Tailwind CSS
- shadcn/ui
- TanStack Query
- Zustand

Mobile:

- React Native
- Expo
- TypeScript
- TanStack Query
- Zustand
- React Navigation

Backend:

- Node.js
- NestJS
- TypeScript

Data:

- PostgreSQL
- Prisma
- Redis
- Kafka or Redpanda
- BullMQ
- OpenSearch or Elasticsearch

Media:

- AWS S3
- CloudFront
- FFmpeg

Real-time:

- Socket.IO
- WebSockets

Push:

- Firebase Cloud Messaging
- Apple Push Notification service

Infrastructure:

- Docker
- Kubernetes
- Helm
- Terraform
- AWS
- GitHub Actions

Observability:

- OpenTelemetry
- Prometheus
- Grafana
- Loki
- Tempo

==================================================
2. EXTERNAL API CONTRACT
========================

Design the public API around stable resource-oriented contracts.

The API must define:

- authentication
- authorization
- versioning
- validation
- pagination
- error handling
- idempotency
- rate limiting
- request IDs
- response metadata

Use a consistent API envelope where appropriate, but avoid unnecessary wrapper complexity.

Every endpoint must clearly identify:

- HTTP method
- route
- authentication requirement
- authorization rules
- request body
- query parameters
- path parameters
- response structure
- error conditions
- pagination behavior
- idempotency behavior

==================================================
3. API DOMAIN GROUPS
====================

Define API groups for:

Authentication:

- registration
- login
- logout
- refresh
- verification
- password reset
- session management
- device management

Profile:

- current user
- profile retrieval
- profile update
- username update
- avatar update
- privacy settings

Social graph:

- follow
- unfollow
- follow request
- approve request
- reject request
- followers
- following
- block
- unblock
- mute
- unmute
- restrict
- unrestrict

Posts:

- create post
- retrieve post
- update post
- delete post
- list posts
- save post
- unsave post
- share post

Engagement:

- like
- unlike
- comments
- replies
- delete comment
- comment likes where supported

Stories:

- create story
- retrieve active stories
- story viewers
- mark viewed
- delete story

Reels:

- publish reel
- retrieve reel
- feed/discovery
- engagement
- save/share

Search:

- user search
- hashtag search
- content search
- autocomplete

Notifications:

- notification list
- unread count
- mark read
- preferences
- device registration

Messaging:

- conversations
- messages
- attachments
- read receipts
- conversation state

Moderation:

- report content
- report account
- moderation state
- block
- restriction

==================================================
4. ERROR CONTRACT
=================

All API errors must follow a predictable structure.

Errors should contain fields such as:

- stable error code
- human-readable message
- request ID
- optional structured validation details

Do not expose:

- stack traces
- SQL errors
- internal service names
- infrastructure credentials
- secret configuration

Define categories for:

- authentication failure
- authorization failure
- validation failure
- conflict
- not found
- rate limiting
- dependency failure
- transient failure
- internal failure

HTTP status codes must be used consistently.

==================================================
5. PAGINATION CONTRACT
======================

Use cursor pagination for high-volume collections.

Cursor pagination is required for:

- feed
- posts
- comments
- followers
- following
- notifications
- messages
- story viewers
- search results where appropriate

Cursors must be opaque.

Clients must not be able to modify ordering semantics through cursor tampering.

Define stable ordering.

For message history, define whether ordering is:

- newest-first
- oldest-first
- bidirectional

and document synchronization behavior.

==================================================
6. IDEMPOTENCY
==============

Use idempotency mechanisms for operations that may be retried safely.

Examples:

- media upload initialization
- post creation when retries could duplicate content
- payment-related operations
- message submission where duplicate delivery is possible
- moderation actions
- notification delivery

Define:

- idempotency-key format
- scope
- TTL
- storage
- conflict behavior
- replay behavior

==================================================
7. AUTHENTICATION ARCHITECTURE
==============================

Authentication must support:

- short-lived access tokens
- refresh tokens
- session tracking
- device tracking
- revocation
- account security events

Refresh tokens must be protected against replay and theft.

Support refresh-token rotation where appropriate.

Every session should be associated with enough metadata to support:

- device identification
- suspicious-session detection
- revocation
- user-visible session management

Never place credentials in URLs.

Never expose secure tokens to logs.

==================================================
8. AUTHORIZATION MODEL
======================

Authorization must be enforced on the server.

At minimum distinguish:

- unauthenticated users
- authenticated users
- account owner
- ordinary users
- blocked relationships
- restricted relationships
- moderators
- administrators

Authorization rules must consider:

- target ownership
- account visibility
- follow relationship
- block state
- restriction state
- content visibility
- moderation status
- account status

A client-provided user ID must never determine the acting identity.

==================================================
9. PRIVACY ENFORCEMENT
======================

Every content retrieval path must evaluate privacy requirements.

Apply visibility rules to:

- profile
- post
- reel
- story
- comment
- search result
- feed candidate
- notification
- message
- media object

A content object must not become accessible solely because its identifier is known.

Private content must not leak through:

- search indexes
- CDN URLs
- caches
- notifications
- recommendations
- feed caches
- background processing outputs

==================================================
10. SIGNED MEDIA ACCESS
=======================

Object-storage access must use controlled authorization.

For private media:

- generate short-lived signed access
- enforce ownership/visibility checks before authorization
- avoid permanent public URLs

For public CDN content:

- ensure only content intended for public distribution is publicly accessible

Media URLs must not themselves become authorization mechanisms.

Authorization must happen before generating protected access.

==================================================
11. MEDIA UPLOAD WORKFLOW
=========================

Define a robust workflow:

Client
→ request upload authorization
→ backend validates request
→ backend creates upload session
→ client uploads directly to S3
→ client/backend signals completion
→ processing job created
→ validation
→ FFmpeg/image processing
→ moderation
→ variants stored
→ metadata persisted
→ search/event propagation
→ content becomes available

Handle:

- interrupted uploads
- duplicate completion requests
- abandoned uploads
- unsupported media
- oversized media
- corrupted media
- malicious media
- processing timeout
- processing failure

Temporary upload objects must be cleaned up.

==================================================
12. MEDIA VARIANT MODEL
=======================

Media assets should be represented independently from their source upload.

Support variant attributes such as:

- type
- format
- resolution
- bitrate
- width
- height
- duration
- object key
- file size
- checksum
- processing status

For video, define delivery-oriented variants appropriate for CDN playback.

For images, generate optimized formats and dimensions appropriate for:

- feed
- profile
- story
- full-size view
- thumbnails

==================================================
13. VIDEO PROCESSING
====================

FFmpeg processing must run in worker infrastructure, not in ordinary synchronous request handlers.

Pipeline requirements:

- input validation
- codec inspection
- metadata extraction
- normalization where required
- resolution variants
- thumbnails
- poster frames
- streaming-oriented packaging where applicable
- content safety preprocessing

Workers must enforce:

- CPU/memory limits
- execution timeouts
- bounded concurrency
- retry limits

Never permit user-provided media metadata to control unsafe command execution.

==================================================
14. STORY WORKFLOW
==================

Story creation must validate:

- ownership
- account state
- media state
- privacy
- supported duration
- supported format

Viewing must validate:

- story not expired
- viewer authorization
- block/restriction/privacy state

Story expiration must be enforced independently of asynchronous cleanup.

The system must be correct even if an expiration job is delayed.

==================================================
15. FOLLOW WORKFLOW
===================

For a public account:

User
→ follow request
→ validate relationship
→ create follow
→ emit event
→ asynchronously update counters/indexes/feed
→ optionally create notification

For a private account:

User
→ follow request
→ validate permissions
→ create pending request
→ notify owner
→ owner approves/rejects
→ relationship becomes active only after approval

Handle race conditions such as:

- simultaneous follow/unfollow
- duplicate requests
- block during request
- account privacy change during request
- account deletion during request

==================================================
16. BLOCKING WORKFLOW
=====================

Blocking must have strong enforcement.

Once user A blocks user B:

- B must not be able to interact in unauthorized ways
- private content must remain inaccessible
- appropriate existing relationships must be invalidated
- messaging access must follow product rules
- feed candidates must be filtered
- search exposure must be adjusted
- notifications must not leak protected interactions

Block state must be checked using authoritative data where required.

==================================================
17. POST CREATION WORKFLOW
==========================

A post may consist of:

- metadata
- caption
- one or more media assets
- mentions
- hashtags
- location metadata

Post creation must validate:

- authenticated owner
- account state
- media ownership
- media readiness
- content policy
- caption limits
- tag limits
- visibility settings

Creation should use transactional semantics for the authoritative record.

Derived operations should use asynchronous events.

==================================================
18. POST DELETION WORKFLOW
==========================

Deletion must immediately prevent normal user access through authoritative state.

Then asynchronously propagate deletion to:

- caches
- search indexes
- feed stores
- notifications where appropriate
- derived engagement
- object storage
- CDN
- analytics

A stale derived system must never re-enable access to deleted content.

==================================================
19. ENGAGEMENT WORKFLOWS
========================

Likes:

- enforce uniqueness
- handle concurrent requests
- persist authoritative state
- update counters asynchronously if desired
- emit events

Comments:

- validate visibility
- validate content
- persist author and content
- emit event
- support moderation

Saves:

- enforce uniqueness
- preserve user-specific state

Shares:

- define whether sharing creates a new object or an event
- prevent privacy bypass

==================================================
20. NOTIFICATION WORKFLOW
=========================

Use domain events to trigger notifications.

Example:

PostLiked
→ notification policy
→ preference evaluation
→ deduplication/aggregation
→ notification persistence
→ push job
→ provider
→ delivery result

Push delivery failure must not delete the durable in-app notification.

The system must handle:

- invalid tokens
- revoked devices
- provider outages
- duplicate events
- notification storms

==================================================
21. REAL-TIME WORKFLOW
======================

Socket.IO connections must be authenticated.

Connection flow:

Client
→ establish connection
→ authenticate
→ validate session
→ establish authorized channels
→ subscribe to permitted events

For real-time messaging:

message persisted
→ message event produced
→ target connection(s) receive event
→ delivery acknowledgement where applicable

Real-time delivery must not be the only persistence mechanism.

==================================================
22. WEBSOCKET AUTHORIZATION
===========================

Every protected channel must validate:

- authenticated user
- conversation membership
- resource ownership
- relationship state
- account status

Do not allow arbitrary channel subscription based solely on client-supplied IDs.

Handle:

- reconnect
- stale sessions
- token expiration
- unauthorized subscription
- duplicate events
- connection storms

==================================================
23. MESSAGING SYNCHRONIZATION
=============================

Clients must be able to recover after disconnection.

Define:

- message IDs
- server timestamps
- ordering
- pagination
- unread state
- read state
- synchronization cursors

A reconnecting client must be able to request messages after a known synchronization point.

Do not assume that WebSocket delivery is lossless.

==================================================
24. SEARCH WORKFLOW
===================

Search indexing should be event-driven.

Example:

ProfileUpdated
→ search indexing event
→ OpenSearch document update

PostCreated
→ indexing event
→ visibility-aware index document

PostDeleted
→ delete/update search document

Search results must be filtered according to:

- account status
- visibility
- block state
- moderation state
- deletion state

Search index rebuilds must be possible.

==================================================
25. FEED WORKFLOW
=================

A feed request should follow approximately:

request
→ authenticate
→ validate cursor
→ retrieve candidates
→ filter unauthorized/ineligible content
→ rank
→ hydrate required metadata
→ remove unavailable objects
→ return bounded result set

Do not make one network request per feed item.

Use batching.

Do not allow stale cached candidates to bypass privacy checks.

==================================================
26. FEED RANKING FAILURE
========================

If ranking infrastructure fails:

- return a safe fallback feed
- preserve authorization
- preserve privacy rules
- avoid exposing deleted/private content
- record telemetry

Feed unavailability should not prevent:

- posting
- messaging
- profile viewing
- basic social interactions

==================================================
27. RECOMMENDATION ARCHITECTURE
===============================

Recommendation signals may include:

- relationship strength
- engagement
- freshness
- content similarity
- interests
- viewing history
- saves
- shares
- creator affinity

Do not allow recommendation systems to become the authoritative source for privacy decisions.

Recommendations must respect:

- block
- mute
- private accounts
- moderation state
- deleted content
- restricted content

==================================================
28. MODERATION WORKFLOW
=======================

A report should create an auditable moderation object.

Support:

- user report
- content report
- spam detection
- abuse detection
- automated classification
- human review
- moderation decisions
- appeal workflow where required

Moderation decisions should emit events for downstream systems.

==================================================
29. ABUSE PREVENTION
====================

Implement controls for:

- credential stuffing
- brute force
- spam follows
- mass commenting
- automated likes
- abusive messaging
- malicious uploads
- report abuse
- account creation abuse

Use:

- Redis rate limiting
- behavioral controls
- request throttling
- device/IP intelligence where appropriate
- progressive restrictions
- audit logs

Avoid relying solely on IP addresses because legitimate users may share addresses.

==================================================
30. DATABASE TRANSACTION BOUNDARIES
===================================

Transactions should protect business invariants.

Use transactions for operations such as:

- account creation
- relationship creation
- relationship deletion
- post creation
- comment creation
- message persistence
- moderation decisions
- sensitive account changes

Do not hold database transactions open while waiting for:

- Kafka
- S3
- FFmpeg
- push providers
- third-party APIs

Persist the transactional state first.

Publish asynchronous work afterward using a reliable event strategy.

==================================================
31. EVENT DELIVERY RELIABILITY
==============================

Avoid the dual-write problem where a database transaction succeeds but event publication silently fails.

Use an outbox-style architecture where appropriate.

The durable transaction should record the event intent.

A publisher should then deliver it to Kafka/Redpanda.

Consumers must be idempotent.

==================================================
32. EVENT CONSUMER DESIGN
=========================

Every consumer must consider:

- duplicate delivery
- retry
- ordering
- poison messages
- schema evolution
- dead-letter handling
- replay

Consumer operations must not assume exactly-once execution unless a specific mechanism guarantees it.

Prefer idempotent effects.

==================================================
33. QUEUE ARCHITECTURE
======================

BullMQ should handle task-oriented asynchronous jobs.

Separate queues by workload where useful:

- media processing
- notifications
- search indexing
- feed updates
- moderation
- cleanup
- analytics

Each job must define:

- retry policy
- backoff
- timeout
- concurrency
- idempotency
- dead-letter behavior
- observability

Avoid one giant queue for unrelated workloads.

==================================================
34. BACKPRESSURE
================

When workload exceeds processing capacity:

- queues must grow predictably
- workers must not exhaust infrastructure
- retries must not amplify overload
- high-priority work must remain serviceable
- low-priority work may be delayed or throttled

Monitor:

- queue depth
- processing latency
- retry rate
- dead-letter rate
- oldest waiting job

==================================================
35. DATABASE SCALABILITY
========================

Prepare PostgreSQL for:

- read replicas
- connection pooling
- partitioning of very large tables
- archival
- hot-index management
- query optimization

High-growth tables likely include:

- follows
- likes
- comments
- messages
- notifications
- feed state
- media records
- audit records

Do not add partitioning solely for theoretical scale; define concrete partitioning criteria and migration strategy.

==================================================
36. REDIS SCALABILITY
=====================

Redis usage must distinguish:

- cache
- ephemeral state
- coordination
- rate limiting
- queues/presence where appropriate

Define TTLs.

Prevent:

- cache stampedes
- unlimited key growth
- oversized values
- accidental durable-data dependency

Use distributed locking only for operations that genuinely require coordination.

==================================================
37. DATABASE QUERY REQUIREMENTS
===============================

All high-traffic queries should be evaluated for:

- index coverage
- cardinality
- sort strategy
- pagination behavior
- join explosion
- N+1 behavior

Never allow endpoints to accept arbitrary unrestricted page sizes.

Set hard limits.

Reject unreasonable requests.

==================================================
38. CLIENT ARCHITECTURE
=======================

Web and mobile clients should use:

TanStack Query for:

- server state
- remote cache
- request lifecycle
- invalidation

Zustand for:

- UI/application state
- transient local state
- selected session-independent state

Do not duplicate the complete server database inside Zustand.

==================================================
39. CLIENT CACHE POLICY
=======================

Define cache behavior for:

- profiles
- feeds
- posts
- stories
- reels
- comments
- notifications
- conversations

Clients must invalidate or refetch after mutations where required.

Do not trust stale client cache for:

- permissions
- visibility
- blocked state
- account security

==================================================
40. OFFLINE AND NETWORK FAILURE
===============================

Mobile applications must handle:

- temporary network loss
- request retries
- app backgrounding
- reconnect
- stale data
- token expiration

Mutations requiring retry must have deterministic/idempotent semantics.

Do not blindly replay all mutations.

==================================================
41. PUSH NOTIFICATION ARCHITECTURE
==================================

Each mobile device should have a managed push registration.

Track:

- user
- device
- platform
- push token
- app version where useful
- last seen
- status

When providers return invalid-token responses:

- mark token invalid
- stop sending to it
- clean it asynchronously

Push notifications must respect:

- notification preferences
- account privacy
- user blocking
- quiet settings where supported

==================================================
42. DEPLOYMENT ARCHITECTURE
===========================

Kubernetes workloads should define:

- Deployments
- Services
- ConfigMaps where appropriate
- Secrets references
- Horizontal Pod Autoscalers
- readiness probes
- liveness probes
- startup probes where required
- resource requests
- resource limits
- Pod disruption strategy

Use Helm for templated deployment configuration.

Use Terraform for infrastructure provisioning.

==================================================
43. ENVIRONMENT MODEL
=====================

Support at minimum:

- development
- staging
- production

Environment-specific configuration must be externalized.

Production credentials must never be committed to source control.

==================================================
44. CI/CD
=========

GitHub Actions should support:

- dependency installation
- linting
- type checking
- unit testing
- integration testing
- build validation
- container image creation
- security scanning
- artifact publication
- deployment workflows

Production deployment must include:

- validation
- controlled rollout
- health verification
- rollback strategy

==================================================
45. OBSERVABILITY
=================

Use OpenTelemetry for distributed tracing.

Collect metrics using Prometheus.

Visualize with Grafana.

Aggregate logs using Loki.

Use Tempo for tracing storage/analysis where appropriate.

Critical trace propagation should cover:

HTTP
→ application
→ PostgreSQL
→ Redis
→ Kafka/Redpanda
→ BullMQ
→ external providers

==================================================
46. SERVICE LEVEL OBJECTIVES
============================

Define measurable operational objectives for:

- API availability
- API latency
- feed latency
- search latency
- message delivery
- media processing
- notification delivery
- database availability
- background-job completion

SLOs must be measurable from telemetry.

==================================================
47. ALERTING
============

Create alerts for:

- elevated error rate
- latency degradation
- database saturation
- Redis saturation
- Kafka lag
- queue backlog
- worker failure
- media-processing failure rate
- push-provider failure
- WebSocket connection failures
- storage failures

Avoid alerts that only report symptoms without actionable context.

==================================================
48. DISASTER RECOVERY
=====================

Define:

- PostgreSQL backups
- backup verification
- restore testing
- object-storage durability strategy
- infrastructure recreation
- secret recovery
- event replay strategy
- search-index reconstruction

OpenSearch/Elasticsearch must be reconstructible.

Caches must not be treated as irreplaceable data.

==================================================
49. DATA RETENTION
==================

Define retention policies for:

- application records
- audit records
- events
- logs
- traces
- metrics
- expired media
- deleted accounts
- moderation records

Retention should balance:

- operational needs
- security
- privacy
- legal requirements
- storage cost

==================================================
50. SECURITY OPERATIONS
=======================

Production environments must support:

- secret rotation
- dependency updates
- vulnerability scanning
- least-privilege IAM
- network segmentation
- encrypted transport
- encrypted storage
- audit logging
- security monitoring

==================================================
51. PERFORMANCE TESTING
=======================

Critical load scenarios must include:

- feed reads
- viral post engagement
- high-follower account activity
- concurrent video playback
- mass notification generation
- high-volume comments
- messaging bursts
- search spikes
- media upload bursts
- WebSocket connection spikes

Test realistic failure and recovery behavior rather than only happy-path throughput.

==================================================
52. ARCHITECTURAL TRADEOFFS
===========================

Explicitly document tradeoffs involving:

- modular monolith vs microservices
- synchronous vs asynchronous processing
- PostgreSQL vs derived data stores
- fanout-on-write vs fanout-on-read
- cache consistency
- strong vs eventual consistency
- event-driven architecture
- object storage/CDN architecture
- real-time delivery
- search indexing
- database partitioning

Every major choice must identify:

- benefit
- cost
- operational complexity
- failure mode
- reason for selection

==================================================
53. ACCEPTANCE CRITERIA
=======================

The architecture is complete only when it defines:

- complete API boundary
- request/response contract strategy
- authentication
- authorization
- privacy enforcement
- media workflow
- story expiration
- follow workflow
- blocking
- content lifecycle
- deletion propagation
- engagement semantics
- notifications
- real-time communication
- messaging synchronization
- search synchronization
- feed retrieval
- event reliability
- queue behavior
- backpressure
- database scalability
- caching
- client state management
- push notifications
- Kubernetes architecture
- CI/CD
- observability
- alerting
- backups
- disaster recovery
- data retention
- operational security
- performance testing

==================================================
54. FINAL ARCHITECTURAL STANDARD
================================

The architecture must be internally coherent.

Do not create conflicting definitions.

Do not depend on client behavior for server-side security.

Do not allow derived data systems to override authoritative state.

Do not assume reliable delivery where infrastructure provides at-least-once semantics.

Do not treat eventual consistency as acceptable for authorization decisions.

Do not make media processing synchronous with normal API request execution.

Do not make real-time connections the authoritative storage mechanism.

Do not create unnecessary microservices.

Do not leave critical architecture decisions unresolved.

The resulting architecture must be realistic for a serious global social platform and directly usable as an implementation specification.
