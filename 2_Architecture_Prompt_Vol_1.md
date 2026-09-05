# PROJECT 1 — INSTAGRAM-LIKE GLOBAL SOCIAL PLATFORM

# ARCHITECTURE PROMPT — VOLUME 1

# SYSTEM ARCHITECTURE, DOMAIN MODEL, DATA ARCHITECTURE & DISTRIBUTED DESIGN

You are the Principal Software Architect and senior engineering team responsible for defining the production architecture of an Instagram-like global social platform.

This prompt is fully standalone. It does not depend on any other prompt, document, previous conversation, previous architecture, approval, implementation phase, or hidden context.

The architecture described here must be sufficiently complete for engineers to implement the platform correctly without relying on another prompt.

Do not generate application source code in this architecture phase.

Produce architecture, specifications, domain models, contracts, engineering decisions, constraints, and implementation guidance only.

Do not use pseudo-code as a substitute for architectural decisions.

Do not use TODOs or placeholder architecture sections.

==================================================

1. PLATFORM OBJECTIVE
   ==================================================

Design a globally scalable social platform supporting:

- user accounts
- authentication
- profiles
- social relationships
- public and private accounts
- posts
- image and video media
- stories
- reels / short-form video
- likes
- comments
- replies
- saves
- shares
- mentions
- hashtags
- feeds
- search
- recommendations
- notifications
- direct messaging
- blocking
- muting
- restricting
- reporting
- moderation
- media processing
- creator-oriented capabilities
- analytics
- push notifications
- real-time features

The architecture must support:

- web clients
- iOS clients
- Android clients
- horizontal backend scaling
- asynchronous processing
- high-volume media delivery
- geographically distributed users
- fault isolation
- graceful degradation
- observability
- secure operations

==================================================
2. REQUIRED TECHNOLOGY FOUNDATION
=================================

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
- Zustand
- TanStack Query
- React Navigation

Backend:

- Node.js
- NestJS
- TypeScript

Transactional database:

- PostgreSQL
- Prisma ORM

Caching and ephemeral state:

- Redis

Event streaming:

- Kafka or Redpanda

Background jobs:

- BullMQ

Search:

- OpenSearch or Elasticsearch

Object storage:

- AWS S3

CDN:

- AWS CloudFront

Media processing:

- FFmpeg

Real-time communication:

- Socket.IO
- WebSockets

Push notifications:

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
3. ARCHITECTURAL STYLE
======================

Use a modular architecture based on:

- Domain-Driven Design
- Clean Architecture
- SOLID
- dependency inversion
- explicit module boundaries
- repository abstraction
- application services
- domain services
- infrastructure adapters

The backend must initially permit a modular-monolith deployment model while maintaining boundaries that allow selected workloads to become independently deployable services later.

Do not split every domain into a microservice simply because microservices are possible.

The architecture should favor:

- clear ownership
- low coupling
- high cohesion
- independent scaling where justified
- asynchronous communication for long-running or non-critical work
- transactional consistency for critical user actions

==================================================
4. HIGH-LEVEL SYSTEM
====================

Define the platform as the following major architectural areas:

1. Edge / CDN
2. Web application
3. Mobile applications
4. API layer
5. Identity and authentication
6. User/profile domain
7. Social graph domain
8. Content domain
9. Media domain
10. Feed and ranking domain
11. Engagement domain
12. Story domain
13. Messaging domain
14. Notification domain
15. Search and discovery domain
16. Moderation and safety domain
17. Analytics domain
18. Background-processing subsystem
19. Event-streaming subsystem
20. Data/storage subsystem
21. Observability subsystem
22. Platform/infrastructure subsystem

Clearly define responsibilities and ownership for each.

==================================================
5. DOMAIN-DRIVEN BOUNDARIES
===========================

Define bounded contexts for at least:

---

Identity
--------

Responsibilities:

- registration
- login
- authentication
- session management
- credentials
- password reset
- email verification
- account security
- device sessions

Identity is authoritative for authentication state.

---

Profile
-------

Responsibilities:

- username
- display name
- biography
- avatar
- website
- profile settings
- account metadata
- privacy state

---

Social Graph
------------

Responsibilities:

- follow relationships
- follow requests
- follower/following state
- blocking
- muting
- restricting
- relationship visibility

---

Content
-------

Responsibilities:

- posts
- captions
- media associations
- mentions
- hashtags
- visibility
- content lifecycle

---

Stories
-------

Responsibilities:

- temporary content
- story sequencing
- expiration
- story viewers
- story privacy
- story interactions

---

Short-Form Video
----------------

Responsibilities:

- reels
- video metadata
- media variants
- discovery metadata
- engagement metadata

---

Engagement
----------

Responsibilities:

- likes
- comments
- replies
- saves
- shares
- engagement counters

---

Feed
----

Responsibilities:

- candidate generation
- feed assembly
- ranking
- pagination
- personalization

---

Messaging
---------

Responsibilities:

- conversations
- messages
- message states
- typing indicators
- presence
- read receipts

---

Notification
------------

Responsibilities:

- in-app notifications
- push notification orchestration
- notification preferences
- aggregation
- delivery state

---

Search
------

Responsibilities:

- indexing
- user search
- hashtag search
- content discovery
- autocomplete
- ranking

---

Moderation
----------

Responsibilities:

- reports
- content review state
- policy enforcement
- abuse prevention
- trust and safety workflows

==================================================
6. DATA OWNERSHIP
=================

Every domain must have a clearly defined source of truth.

PostgreSQL is the authoritative transactional datastore.

Redis is not an authoritative source of truth for durable business state.

OpenSearch/Elasticsearch is a derived index.

Kafka/Redpanda is an event transport and durable event-streaming mechanism, not the primary transactional database.

S3 is authoritative for durable media object storage.

Application services must not make business-critical decisions using stale derived indexes when authoritative PostgreSQL state is required.

==================================================
7. CORE ENTITY MODEL
====================

Define architecture-level models for:

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
- Post
- PostMedia
- MediaAsset
- MediaVariant
- Story
- StoryItem
- StoryView
- Reel
- Like
- Comment
- CommentReply
- Save
- Share
- Hashtag
- Mention
- FeedItem
- Conversation
- ConversationParticipant
- Message
- MessageAttachment
- MessageReceipt
- Notification
- NotificationPreference
- PushDevice
- Report
- ModerationCase
- SearchDocument
- AuditRecord

For every entity, define:

- purpose
- ownership domain
- lifecycle
- important identifiers
- relationships
- transactional requirements
- indexing considerations
- deletion semantics
- privacy implications

Do not assume every entity must be physically isolated in its own database.

==================================================
8. IDENTIFIER STRATEGY
======================

Define a globally safe identifier strategy.

Identifiers must:

- avoid predictable sequential exposure where inappropriate
- be safe for distributed generation
- work across services
- remain stable across derived systems

Use opaque public identifiers where exposing database implementation details would create security or scalability concerns.

==================================================
9. USER ACCOUNT MODEL
=====================

Define account states including:

- active
- pending verification
- restricted
- suspended
- disabled
- deleted

Define:

- username uniqueness
- username normalization
- account visibility
- privacy state
- creator status
- account lifecycle

Account deletion must define:

- immediate user-facing effect
- asynchronous cleanup
- media cleanup
- search cleanup
- cache invalidation
- notification cleanup
- relationship behavior
- compliance/audit considerations

==================================================
10. SOCIAL GRAPH ARCHITECTURE
=============================

The social graph must support high-volume relationships.

Design:

- follows
- follower lists
- following lists
- private account requests
- blocks
- mutes
- restrictions

Define consistency requirements separately for:

- transactional relationship state
- relationship counters
- cached relationship lookups
- search visibility
- feed candidate generation

Protect against:

- duplicate relationships
- race conditions
- unauthorized follows
- follow-request abuse
- block bypass

The architecture must account for extremely high-degree accounts.

==================================================
11. CONTENT ARCHITECTURE
========================

Define a general content model capable of representing:

- single-image post
- multi-image post
- video post
- reel
- story content

Separate:

- content metadata
- media metadata
- object storage
- derived processing results
- moderation state
- visibility state
- engagement counters

Content visibility must support:

- public
- followers
- private/account-restricted visibility
- direct/private contexts where applicable

Visibility enforcement must occur server-side.

==================================================
12. MEDIA ARCHITECTURE
======================

Use S3 for original and processed media.

Use CloudFront for content delivery.

Media architecture must support:

- upload sessions
- signed upload authorization
- MIME validation
- file-size limits
- media-type validation
- metadata extraction
- virus/malware scanning where applicable
- image optimization
- video transcoding
- thumbnails
- multiple resolutions
- streaming-friendly outputs
- content moderation
- failed-processing recovery

The API servers must not unnecessarily proxy large media files.

Use asynchronous processing for expensive operations.

Define media lifecycle states such as:

- pending
- uploaded
- validating
- processing
- ready
- rejected
- failed
- deleted

==================================================
13. MEDIA PROCESSING PIPELINE
=============================

Architect a pipeline:

Client
→ upload authorization
→ object storage
→ processing event
→ validation
→ metadata extraction
→ transcoding
→ thumbnail generation
→ moderation
→ variant registration
→ searchable metadata update
→ CDN availability

The workflow must support:

- idempotency
- retries
- dead-letter handling
- duplicate event protection
- partial failure recovery
- observability

A processing failure must not cause silent permanent loss of state.

==================================================
14. STORY ARCHITECTURE
======================

Stories are time-bound content.

Define:

- story creation
- sequencing
- visibility
- expiration
- views
- interactions
- deletion
- archive behavior if supported

Expiration must be enforced through both:

- application-level validation
- scheduled/background cleanup

Do not rely solely on deletion jobs for access control.

An expired story must be inaccessible even if cleanup has not yet completed.

==================================================
15. REELS / SHORT-FORM VIDEO
============================

Design reels as media-heavy content with:

- video source
- generated variants
- thumbnails
- duration
- dimensions
- captions
- hashtags
- mentions
- audio metadata where applicable
- moderation status
- engagement data

The architecture must support large concurrent playback demand.

Use:

- object storage
- CDN
- transcoded variants
- efficient metadata APIs
- caching
- preloading strategies

Playback must not require the API server to stream the full video payload.

==================================================
16. ENGAGEMENT ARCHITECTURE
===========================

Likes, saves, comments and shares should be modeled as independently manageable workloads.

Define:

- transactional behavior
- deduplication
- counter strategy
- cache strategy
- event propagation
- notification triggers

Counters may be eventually consistent.

The underlying unique interaction state must remain correct.

Examples:

A user should not be able to create multiple logical likes for the same post unless the product explicitly supports such behavior.

==================================================
17. COMMENTS
============

Design comments to support:

- top-level comments
- replies
- deletion
- moderation
- pagination
- mentions
- reporting

Avoid unbounded recursive relational structures.

Use a bounded comment-reply model unless there is a strong requirement for arbitrary tree depth.

Define ordering and pagination strategy.

==================================================
18. FEED ARCHITECTURE
=====================

The feed is one of the highest-scale components.

Support a hybrid feed architecture.

Candidate generation may use:

- social graph signals
- recent content
- engagement signals
- creator relationships
- content freshness
- personalization

Use combinations of:

- fanout-on-write
- fanout-on-read
- cached candidate sets
- ranking

For high-follower accounts, avoid generating massive synchronous fanout workloads.

Feed delivery must use cursor-based pagination.

Define strategies for:

- feed hydration
- stale candidates
- deleted content
- blocked users
- private accounts
- muted users
- unavailable media
- ranking failures

The feed should degrade gracefully to a valid fallback ordering when ranking infrastructure is unavailable.

==================================================
19. FEED CONSISTENCY
====================

The architecture must explicitly define which properties are:

Strongly consistent:

- authorization
- account ownership
- relationship mutation
- content deletion
- block state
- visibility enforcement

Eventually consistent:

- engagement counters
- recommendation scores
- search indexes
- notification aggregation
- feed candidate propagation

Do not use eventual consistency where it creates a privacy or authorization vulnerability.

==================================================
20. SEARCH ARCHITECTURE
=======================

Use OpenSearch or Elasticsearch as the derived search layer.

Indexes should include only data permitted to be discoverable.

Potential indexes:

- profiles
- hashtags
- posts
- reels
- creators

Every indexed document must carry enough state to determine or enforce visibility safely.

Search index updates should be event-driven from authoritative state changes.

Index rebuilds must be possible from PostgreSQL/S3-backed authoritative data.

==================================================
21. PRIVACY-AWARE SEARCH
========================

Private or restricted content must not become discoverable through stale search indexes.

Define mechanisms for:

- visibility filtering
- blocked-user filtering
- deleted-content removal
- suspended-user removal
- delayed-index consistency

For highly sensitive visibility decisions, revalidate against authoritative application state before returning results.

==================================================
22. NOTIFICATION ARCHITECTURE
=============================

Notifications are derived from domain events.

Example triggers:

- follow
- follow request
- like
- comment
- mention
- message
- story interaction

Notification creation should be asynchronous where possible.

Push delivery must be separate from notification persistence.

The system must support:

- retries
- invalid-device-token cleanup
- preference filtering
- rate limiting
- aggregation
- duplicate suppression

==================================================
23. REAL-TIME ARCHITECTURE
==========================

Use Socket.IO/WebSockets.

Real-time capabilities:

- messaging
- typing
- presence
- read receipts
- live notification delivery
- selected engagement updates

Multiple application instances must share real-time coordination through infrastructure such as Redis and/or event streaming.

Do not maintain authoritative multi-user presence only in one process.

Define:

- connection authentication
- channel authorization
- reconnection behavior
- heartbeat
- idle connection handling
- event ordering
- duplicate-event handling

==================================================
24. DIRECT MESSAGING ARCHITECTURE
=================================

Messaging must support:

- conversations
- participants
- messages
- attachments
- delivery state
- read receipts
- typing indicators
- presence

Message persistence belongs in PostgreSQL or an appropriately selected durable datastore.

Real-time delivery is a transport mechanism and must not become the sole source of truth.

Clients must be able to recover state after:

- disconnects
- reconnects
- app restarts
- temporary network failures

Define message ordering rules and client synchronization strategy.

==================================================
25. CACHE ARCHITECTURE
======================

Redis may cache:

- sessions
- profile summaries
- relationship lookups
- feed candidates
- rate-limit counters
- notification counters
- presence
- temporary processing state

Every cache entry must have:

- purpose
- TTL policy
- invalidation strategy
- stale-data tolerance

Cache failure must not make the entire application unusable unless the cached value is explicitly required for correctness.

==================================================
26. EVENT ARCHITECTURE
======================

Kafka/Redpanda events must be designed with:

- event names
- event versions
- event identifiers
- aggregate/entity identifiers
- timestamps
- producer identity
- schema version
- correlation ID
- trace ID where appropriate

Events must be:

- replayable
- idempotently consumable
- observable
- versionable

Avoid publishing events that expose sensitive personal or private information unnecessarily.

==================================================
27. EXAMPLE DOMAIN EVENTS
=========================

Define architecture-level events for cases such as:

- UserRegistered
- UserVerified
- ProfileUpdated
- FollowCreated
- FollowRemoved
- FollowRequestCreated
- UserBlocked
- UserUnblocked
- PostCreated
- PostUpdated
- PostDeleted
- MediaUploaded
- MediaProcessingCompleted
- MediaProcessingFailed
- StoryCreated
- StoryExpired
- ReelPublished
- PostLiked
- PostUnliked
- CommentCreated
- CommentDeleted
- PostSaved
- PostUnsaved
- MessageCreated
- MessageRead
- NotificationCreated
- ReportCreated
- ModerationDecisionApplied

For each event define:

- producer
- consumers
- delivery requirements
- idempotency expectations
- ordering requirements
- retention considerations

==================================================
28. FAILURE ISOLATION
=====================

The architecture must isolate failure between:

- API
- search
- media processing
- notification delivery
- analytics
- feed ranking
- real-time messaging
- object storage
- Redis
- Kafka/Redpanda

Examples:

Search outage must not prevent users from viewing their own profiles.

Notification provider outage must not prevent likes from being persisted.

Feed-ranking outage must not prevent content creation.

Media-processing outage must not corrupt already-created post metadata.

==================================================
29. SECURITY ARCHITECTURE
=========================

Every request that accesses protected data must pass:

Authentication
→ identity resolution
→ authorization
→ domain validation
→ business operation

Never trust:

- client user IDs
- client role claims without verification
- client visibility flags
- client ownership declarations

Authorization must be based on authoritative state.

==================================================
30. RATE LIMITING
=================

Architect differentiated limits for:

- login
- registration
- password reset
- follow operations
- comments
- likes
- messages
- uploads
- search
- report creation
- API requests
- WebSocket connections

Rate limits should support:

- per-user
- per-IP
- per-device
- per-endpoint

Use Redis-backed distributed rate limiting where appropriate.

==================================================
31. AUDITING
============

Sensitive operations should produce auditable records.

Examples:

- account security changes
- password changes
- email changes
- moderation decisions
- account suspension
- administrative actions
- privacy changes

Audit records must avoid unnecessary sensitive content.

==================================================
32. OBSERVABILITY ARCHITECTURE
==============================

Use OpenTelemetry across:

- HTTP
- database
- Redis
- Kafka/Redpanda
- BullMQ
- WebSockets
- S3 interactions
- search
- external APIs

Collect:

- metrics
- logs
- traces

Metrics must include both infrastructure and business indicators.

Examples:

- request latency
- error rate
- queue latency
- media-processing latency
- feed-generation latency
- search latency
- message delivery latency
- notification success rate
- cache hit ratio

==================================================
33. GLOBAL SCALABILITY
======================

The architecture must be capable of scaling:

- users
- media
- feed reads
- engagement writes
- WebSocket connections
- search queries
- notifications
- background jobs

Scale horizontally.

Avoid single-node bottlenecks.

Design explicit strategies for:

- hot partitions
- celebrity accounts
- viral content
- burst traffic
- queue backlogs
- cache stampedes
- database connection exhaustion

==================================================
34. HOTSPOT MITIGATION
======================

The architecture must account for high-traffic objects such as:

- celebrity profiles
- viral posts
- popular reels
- trending hashtags

Do not create designs where one database row or one cache key becomes an unavoidable global bottleneck.

Use:

- sharded counters where needed
- asynchronous aggregation
- cache distribution
- partitioning
- batched processing
- request coalescing

==================================================
35. DATABASE ARCHITECTURE
=========================

PostgreSQL must be designed around:

- domain ownership
- transactional integrity
- indexes
- foreign keys where appropriate
- uniqueness constraints
- efficient pagination
- connection pooling
- migration safety

Identify tables that are likely to become large.

Define strategies for:

- indexing
- partitioning
- archival
- retention
- vacuuming
- query performance
- read replicas where appropriate

Avoid querying full datasets.

==================================================
36. FILE AND OBJECT STORAGE
===========================

Object paths must be predictable for backend ownership but opaque enough to avoid exposing unnecessary internal structure.

Define logical namespaces for:

- original uploads
- processed media
- thumbnails
- avatars
- story assets
- reel assets
- message attachments

Object metadata must remain synchronized with authoritative application records.

==================================================
37. DATA DELETION
=================

Every domain must define deletion semantics.

Differentiate:

- soft deletion
- hard deletion
- asynchronous cleanup
- legal/compliance retention where required

Deletion must propagate to:

- PostgreSQL
- Redis
- search
- event consumers
- CDN/object storage
- notification systems
- derived feed data

==================================================
38. API GATEWAY / ENTRY ARCHITECTURE
====================================

Define a unified external API boundary responsible for:

- authentication context
- request validation
- rate limiting
- request IDs
- observability
- routing
- error normalization

Do not embed all domain logic in gateway middleware.

Business decisions belong inside the appropriate application/domain layer.

==================================================
39. CLIENT ARCHITECTURE
=======================

Web and mobile applications should consume stable backend contracts.

Clients must not implement server-authoritative business rules such as:

- ownership
- visibility
- permissions
- account restrictions

Clients may optimize presentation and caching, but authorization remains server-controlled.

Use TanStack Query for server-state management.

Use Zustand for appropriate client-local/application state.

==================================================
40. ACCEPTANCE CRITERIA
=======================

The architecture is complete only when it clearly defines:

- bounded contexts
- component responsibilities
- source-of-truth ownership
- entity relationships
- persistence responsibilities
- caching strategy
- event architecture
- asynchronous workflows
- media pipeline
- feed strategy
- search strategy
- messaging strategy
- notification strategy
- security boundaries
- privacy enforcement
- failure isolation
- scalability strategy
- observability strategy
- deletion strategy
- API boundary
- client/backend responsibilities

The architecture must be implementable by a professional engineering team without requiring undocumented architectural assumptions.

==================================================
41. ARCHITECTURAL OUTPUT STANDARD
=================================

When producing the architecture document, organize it into:

1. Executive Architecture Summary
2. System Context
3. Container-Level Architecture
4. Bounded Contexts
5. Domain Model
6. Data Ownership
7. Database Architecture
8. Cache Architecture
9. Event Architecture
10. Media Architecture
11. Feed Architecture
12. Search Architecture
13. Messaging Architecture
14. Notification Architecture
15. Security Architecture
16. Privacy Architecture
17. Reliability Architecture
18. Scalability Architecture
19. Observability Architecture
20. API Boundary
21. Client Architecture
22. Deployment Considerations
23. Architectural Tradeoffs
24. Risks and Mitigations
25. Acceptance Criteria

Be precise.

Resolve architectural ambiguity through explicit engineering decisions.

Do not defer critical architectural decisions to an unspecified future phase.

Do not claim that another prompt or phase has already defined anything.

The architecture itself must stand on its ow

You are operating in Senior Engineering Team Mode.

The Master Prompt has been provided and approved.

Your task in this phase is to produce the COMPLETE FOUNDATIONAL ARCHITECTURE for the Instagram-like global visual-social platform.

DO NOT IMPLEMENT SOURCE CODE.

DO NOT GENERATE:

- NestJS implementation
- TypeScript implementation
- React implementation
- React Native implementation
- Prisma schema code
- SQL migrations
- Terraform
- Kubernetes
- Helm
- Dockerfiles
- GitHub Actions
- executable configuration

This phase is architecture and engineering specification only.

The architecture produced here becomes the source of truth for every subsequent implementation.

All later backend, frontend, mobile, infrastructure, DevOps, security, and QA implementation must follow these decisions.

Do not redesign the system during implementation unless a genuine architectural defect is discovered and documented through an Architecture Decision Record.

==================================================
ARCHITECTURE OBJECTIVE
======================

Design a complete production-grade architecture for an original global visual-social platform comparable in architectural scope to Instagram.

The architecture must support:

- massive read traffic
- high-volume media
- high-volume engagement
- personalized feeds
- recommendations
- search
- realtime messaging
- notifications
- creator workloads
- business workloads
- advertising
- commerce
- moderation
- rights management
- privacy operations
- analytics
- multi-region deployment
- disaster recovery

The architecture must remain understandable and maintainable.

Avoid both:

1. an unmaintainable monolith;
2. unnecessary microservice fragmentation.

Use domain boundaries to determine where modularization is needed.

==================================================
ARCHITECTURAL PRINCIPLES
========================

Follow:

- Domain-Driven Design
- Clean Architecture
- SOLID
- bounded contexts
- explicit domain ownership
- repository pattern
- service/application layers
- dependency inversion
- event-driven architecture
- transactional outbox
- idempotent processing
- horizontal scalability
- secure-by-default design
- privacy-by-design
- least privilege
- observability
- fault tolerance
- backward compatibility

Use distributed-systems complexity only when justified.

==================================================
SYSTEM CONTEXT
==============

Describe the complete system context.

Identify:

External actors:

- anonymous visitor
- authenticated user
- creator
- professional/business user
- advertiser
- merchant
- moderator
- administrator
- rights holder

Client applications:

- web
- iOS/Android mobile application

Platform components:

- edge/CDN
- API layer
- application/domain modules
- transactional database
- cache
- event streaming
- background processing
- search
- object storage
- media processing
- realtime gateway
- notification system
- analytics
- administration

External providers:

- cloud
- payments
- push notifications
- email
- maps/location
- other approved integrations

Explain the responsibilities and trust boundaries.

==================================================
HIGH-LEVEL ARCHITECTURE
=======================

Design the complete request/data flow:

Client
→ Edge
→ Application/API
→ Domain layer
→ Persistence / Cache / Events / Jobs / External providers

And:

Application
→ Event Stream
→ Consumers
→ Derived systems

And:

Client
→ Upload Session
→ Object Storage
→ Media Processing
→ Derived Media
→ CDN

And:

Client
→ Realtime Gateway
→ Event Distribution
→ Client

Use clear textual architecture diagrams.

==================================================
ARCHITECTURAL LAYERS
====================

Define:

Presentation Layer
Application Layer
Domain Layer
Infrastructure Layer

Explain responsibilities and dependency direction.

The domain layer must not depend directly on:

- PostgreSQL
- Redis
- Kafka
- AWS SDK
- Stripe
- FCM/APNS
- OpenSearch
- external HTTP clients

Use interfaces/adapters where necessary.

==================================================
BOUNDED CONTEXTS
================

Define bounded contexts for:

1. Identity
2. Accounts
3. Profiles
4. Social Graph
5. Content
6. Media
7. Stories
8. Reels
9. Engagement
10. Feed
11. Recommendations
12. Search
13. Messaging
14. Notifications
15. Creator/Professional
16. Monetization
17. Advertising
18. Commerce
19. Moderation/Safety
20. Rights Management
21. Analytics
22. Privacy/Data
23. Administration
24. Configuration/Feature Flags

For each bounded context provide:

- purpose
- responsibilities
- owned data
- important entities
- aggregate candidates
- commands
- queries
- domain events
- integration events
- synchronous dependencies
- asynchronous dependencies
- consistency requirements
- security boundary

==================================================
DOMAIN OWNERSHIP
================

Create an ownership matrix.

Example:

Domain
→ authoritative service/module
→ database ownership
→ cache ownership
→ event ownership
→ external integrations

No domain may silently become the source of truth for another domain's core data.

==================================================
IDENTITY ARCHITECTURE
=====================

Design:

- User identity
- Credentials
- Sessions
- Devices
- Verification
- Password reset
- Security events
- Recovery
- Authentication factors where supported

Define:

- unique identifiers
- session lifecycle
- credential boundaries
- device registration
- revocation

Specify which identity data is:

- public
- authenticated-only
- owner-only
- administrator-only

==================================================
ACCOUNT ARCHITECTURE
====================

Define account lifecycle states such as:

- active
- limited
- suspended
- deactivated
- deletion_pending
- deleted

Define how account state affects:

- authentication
- profile visibility
- content
- messaging
- recommendations
- search
- notifications
- monetization
- advertising
- commerce

==================================================
PROFILE ARCHITECTURE
====================

Define:

- Profile
- Creator Profile
- Business Profile
- Professional Profile

Support:

- avatar
- username
- display name
- biography
- links
- verification
- account category
- professional metadata

Define ownership and update permissions.

==================================================
SOCIAL GRAPH ARCHITECTURE
=========================

Design:

- Follow
- FollowRequest
- Block
- Restriction
- Mute
- CloseFriend

Define lifecycle and semantics.

Explicitly define:

- public-account follow
- private-account follow
- request approval
- request cancellation
- block precedence
- restriction behavior
- mute behavior

==================================================
RELATIONSHIP CONSISTENCY
========================

Classify social graph operations:

Strong consistency where required:

- blocks
- privacy-critical relationship changes
- ownership/security state

Eventual consistency where acceptable:

- counters
- recommendation signals
- analytics
- derived feeds

==================================================
AUTHORIZATION ARCHITECTURE
==========================

Design centralized authorization.

Authorization must consider:

1. authentication
2. account state
3. ownership
4. block state
5. privacy state
6. relationship state
7. resource visibility
8. feature permission
9. administrative role
10. regional/policy restrictions

Define reusable policy concepts.

Do not duplicate independent authorization logic in every domain.

==================================================
PRIVACY ARCHITECTURE
====================

Design a reusable privacy policy engine.

Support:

- public
- private
- followers
- close friends
- owner-only
- custom audiences where supported
- blocked
- restricted

Define privacy evaluation for:

- profiles
- posts
- stories
- reels
- comments
- messages
- search
- recommendations
- notifications
- analytics
- media delivery

==================================================
CONTENT ARCHITECTURE
====================

Define:

- Post
- Carousel
- Draft
- Caption
- Mention
- Hashtag
- Tagged User
- Location
- Publication
- Visibility

Define the lifecycle:

draft
→ upload
→ processing
→ ready
→ scheduled/published
→ updated
→ deleted/restorable

Specify ownership and invariants.

==================================================
POST AGGREGATE
==============

Define:

- aggregate root
- child entities
- invariants
- valid state transitions

The aggregate must remain sufficiently small for transactional scalability.

==================================================
MEDIA ARCHITECTURE
==================

Design the complete media pipeline:

Client
→ Upload initialization
→ upload authorization
→ S3
→ media processing
→ metadata extraction
→ derived media
→ thumbnails
→ HLS where required
→ CDN

Define:

- upload session
- media object
- media variant
- processing job
- processing state
- failure state

==================================================
MEDIA PROCESSING
================

Support:

Images:

- resizing
- optimization
- thumbnails
- metadata sanitization

Video:

- validation
- transcoding
- thumbnails
- HLS
- bitrate variants
- metadata

Define processing isolation and retry behavior.

==================================================
MEDIA ACCESS CONTROL
====================

Define:

- public media
- private media
- signed URLs/cookies
- expiration
- revocation
- CDN authorization

Private content must never become public merely because it is cached.

==================================================
STORY ARCHITECTURE
==================

Define:

- Story
- StoryMedia
- StoryView
- StoryReaction
- StoryReply
- Highlight
- HighlightItem

Define:

- visibility
- expiration
- viewing
- reactions
- replies
- highlights
- deletion
- moderation

==================================================
REELS ARCHITECTURE
==================

Define:

- Reel
- ReelMedia
- ReelAudio
- ReelWatchEvent

Define relationships with:

- content
- media
- feed
- recommendations
- search
- engagement
- rights
- moderation
- analytics

==================================================
ENGAGEMENT ARCHITECTURE
=======================

Create reusable concepts for:

- likes
- comments
- replies
- saves
- collections
- shares
- reposts where supported

Define idempotency and counter strategy.

==================================================
COUNTER ARCHITECTURE
====================

Counters such as:

- likes
- comments
- followers
- views
- shares

must be treated as derived/aggregated values unless strong consistency is explicitly required.

Define:

- source events
- aggregation
- reconciliation
- cache strategy

Never make counters the authoritative source of transactional truth.

==================================================
COMMENT ARCHITECTURE
====================

Define:

- Comment
- CommentReply
- CommentLike
- CommentModerationState

Specify:

- nesting depth
- pagination
- moderation
- deletion
- visibility
- ownership

==================================================
COLLECTIONS
===========

Define:

- Collection
- CollectionItem
- Save

Specify:

- private ownership
- ordering
- duplicates
- deletion

==================================================
FEED ARCHITECTURE
=================

Design:

- Home feed
- Following feed
- Reels feed
- Story tray
- Explore

Each feed pipeline must separate:

1. candidate generation
2. eligibility
3. ranking
4. reranking
5. diversification
6. pagination
7. response assembly

==================================================
FEED CANDIDATE SOURCES
======================

Possible candidates:

- followed accounts
- engaged accounts
- recent content
- recommended content
- trending content
- creator content
- business content
- sponsored content where applicable

Specify source weighting at architectural level without implementing ranking formulas.

==================================================
FEED STORAGE STRATEGY
=====================

Evaluate:

- fan-out-on-write
- fan-out-on-read
- hybrid

Specify how to handle:

- normal users
- highly-followed creators
- viral accounts
- inactive users

==================================================
FEED ELIGIBILITY
================

Every candidate must pass:

- account-state checks
- block checks
- privacy checks
- relationship checks
- content visibility
- moderation
- rights
- region
- recommendation policy

before being returned.

==================================================
RECOMMENDATION ARCHITECTURE
===========================

Design recommendation pipelines for:

- accounts
- creators
- businesses
- posts
- reels
- hashtags
- audio

Separate:

Candidate generation
→ feature retrieval
→ ranking
→ reranking
→ diversity
→ policy filtering

Support negative signals and feedback.

==================================================
TRENDING
========

Define trending architecture for:

- hashtags
- reels
- audio
- creators
- topics

Use time-windowed derived data.

Define anti-manipulation considerations.

==================================================
SEARCH
======

Design search for:

- users
- creators
- businesses
- posts
- reels
- hashtags
- audio
- locations
- products

OpenSearch/Elasticsearch is derived state.

PostgreSQL remains the authoritative source.

==================================================
SEARCH INDEXING
===============

Define:

- indexing events
- update events
- deletion events
- reindexing
- reconciliation
- index versions
- retry
- dead-letter behavior

==================================================
SEARCH PRIVACY
==============

Search results must respect:

- private accounts
- blocks
- restrictions
- moderation
- rights
- deleted content
- regional restrictions

==================================================
MESSAGING ARCHITECTURE
======================

Define:

- Conversation
- Participant
- Message
- MessageAttachment
- MessageReaction
- MessageReply
- MessageRequest
- DeliveryState
- ReadState
- Presence
- TypingState

Support:

- one-to-one
- group conversations where supported
- message requests
- blocking
- privacy
- pagination

==================================================
MESSAGING CONSISTENCY
=====================

Classify:

Strong/eventual consistency for:

- message persistence
- delivery
- read receipts
- reactions
- typing
- presence

Avoid unnecessarily strong guarantees for ephemeral state.

==================================================
REALTIME ARCHITECTURE
=====================

Design WebSocket/Socket.IO architecture.

Define:

- connection authentication
- authorization
- room model
- event routing
- horizontal scaling
- Redis adapter/coordination where appropriate
- reconnect
- duplicate detection
- ordering
- backpressure

==================================================
NOTIFICATION ARCHITECTURE
=========================

Define:

- Notification
- NotificationGroup
- NotificationPreference
- PushDevice

Support:

- in-app
- push
- email where appropriate

Define fanout and aggregation strategy.

==================================================
CREATOR/BUSINESS ARCHITECTURE
=============================

Define capabilities for:

- creator accounts
- professional accounts
- business accounts
- dashboards
- analytics
- monetization
- advertising
- commerce

Specify permission boundaries.

==================================================
MONETIZATION
============

Design:

- SubscriptionPlan
- Subscription
- Entitlement
- Earning
- LedgerEntry
- PlatformFee
- PayoutRequest
- Payout
- Refund
- Dispute
- Settlement

Use an immutable ledger model where appropriate.

Every financial mutation must be idempotent.

==================================================
ADVERTISING
===========

Define:

- Advertiser
- Campaign
- AdSet
- Creative
- Audience
- Placement
- Budget
- Schedule
- Review
- AdEvent

Define lifecycle states.

Separate campaign configuration from serving/ranking infrastructure.

==================================================
COMMERCE
========

Define:

- Storefront
- Product
- ProductVariant
- ProductMedia
- Collection
- ProductTag
- Cart
- Checkout
- Order
- OrderItem
- Payment
- Fulfillment
- Shipment
- Return
- Refund
- InventoryReservation

Define transaction boundaries and state machines.

==================================================
MODERATION
==========

Define:

- Report
- ModerationCase
- ModerationAction
- Enforcement
- Appeal
- SafetySignal

Support:

- automated signals
- user reports
- human review
- enforcement
- appeals
- restoration

==================================================
RIGHTS MANAGEMENT
=================

Define:

- RightsHolder
- RightsClaim
- RightsPolicy
- RegionalRestriction
- Takedown
- CounterNotice
- Restoration

Define integrations with:

- content
- media
- feed
- search
- CDN

==================================================
ANALYTICS
=========

Define analytics event categories for:

- impressions
- views
- watch
- engagement
- follows
- searches
- creator metrics
- business metrics
- advertising
- commerce
- moderation

Do not send:

- private message bodies
- passwords
- secrets
- unnecessary sensitive information

==================================================
PRIVACY AND DATA LIFECYCLE
==========================

Define:

- export
- deletion
- retention
- derived-data deletion
- cache invalidation
- search deletion
- analytics handling
- audit

Deletion workflows must identify every derived system affected by a deleted account or resource.

==================================================
ADMINISTRATION
==============

Define:

- AdminUser
- Role
- Permission
- AuditLog
- FeatureFlag
- ConfigurationEntry

Administrative operations must have a separate authorization boundary.

==================================================
EVENT ARCHITECTURE
==================

Define three major event categories:

1. Domain Events
   Internal bounded-context events.
2. Integration Events
   Cross-domain events.
3. Analytics Events
   High-volume behavioral/measurement events.

Do not mix these semantics.

==================================================
EVENT ENVELOPE
==============

Every integration event should contain:

- eventId
- eventType
- schemaVersion
- timestamp
- producer
- aggregateId
- correlationId
- causationId where required
- payload

==================================================
TRANSACTIONAL OUTBOX
====================

Define:

Transaction
→ domain state change
→ outbox record
→ publisher
→ event stream
→ consumers

Specify:

- retries
- idempotency
- dead letters
- replay
- ordering

==================================================
QUEUE ARCHITECTURE
==================

Define job categories for:

- media
- notifications
- feed
- recommendations
- search
- moderation
- analytics
- privacy export
- deletion
- cleanup
- scheduling
- reconciliation

Each queue must have:

- owner
- job schema
- retry policy
- idempotency behavior
- failure handling

==================================================
API ARCHITECTURE
================

Establish API domain boundaries.

Expected groups include:

- auth
- accounts
- profiles
- social
- posts
- stories
- reels
- feed
- explore
- search
- messages
- notifications
- creator
- advertising
- commerce
- moderation
- rights
- privacy
- admin

Define REST design principles.

==================================================
API CONTRACT PRINCIPLES
=======================

Every API must define:

- request
- response
- authentication
- authorization
- validation
- errors
- pagination
- rate limits
- idempotency when required

==================================================
PAGINATION
==========

Use cursor pagination for:

- feed
- notifications
- messages
- comments
- search results
- social graph lists
- large administrative collections

Define:

- cursor opacity
- ordering
- limits
- maximum page size
- next cursor

==================================================
API ERRORS
==========

Create standardized error semantics.

At minimum:

- authentication error
- authorization error
- validation error
- not found
- conflict
- rate limited
- dependency failure
- internal error

Do not expose internal implementation details.

==================================================
API RATE LIMITING
=================

Define rate limits by category:

- anonymous
- authenticated
- write-heavy
- login/authentication
- messaging
- uploads
- privileged
- administrative

Support distributed coordination through Redis where required.

==================================================
IDEMPOTENCY
===========

Define idempotency for:

- content creation
- message sending
- payments
- orders
- webhooks
- exports
- deletion
- important relationship mutations

==================================================
WEBHOOKS
========

Design secure webhook handling.

Support:

- signature verification
- timestamp validation
- replay protection
- idempotency
- persistence
- retry
- dead-letter

==================================================
CONSISTENCY MODEL
=================

Create a formal consistency classification.

Strong consistency candidates:

- authentication
- authorization
- blocks
- privacy-critical state
- financial ledger
- order state
- ownership

Eventual consistency candidates:

- feed
- recommendations
- search
- notification aggregation
- analytics
- engagement counters
- trending

Ephemeral:

- typing
- presence
- transient realtime indicators

Document exceptions.

==================================================
FAILURE MODEL
=============

Define behavior when:

- PostgreSQL unavailable
- Redis unavailable
- Kafka/Redpanda unavailable
- OpenSearch unavailable
- S3 unavailable
- CDN unavailable
- push provider unavailable
- email unavailable
- payment provider unavailable
- worker pool unavailable
- realtime unavailable

For every dependency identify:

- hard dependency
- soft dependency
- degraded behavior
- retry
- recovery

==================================================
SECURITY ARCHITECTURE
=====================

Define security boundaries between:

- browser
- mobile device
- edge
- API
- application modules
- workers
- database
- cache
- event system
- object storage
- search
- admin

==================================================
THREAT MODEL
============

Identify threats including:

- account takeover
- credential abuse
- scraping
- spam
- bot activity
- privilege escalation
- IDOR
- malicious uploads
- injection
- SSRF
- WebSocket abuse
- webhook spoofing
- payment abuse
- fraud
- data exfiltration
- insider/admin abuse

For each major threat specify architectural mitigations.

==================================================
OBSERVABILITY
=============

Define:

Logs:

- structured
- correlated
- privacy-safe

Metrics:

- latency
- throughput
- errors
- queue depth
- event lag
- resource utilization

Traces:

- API
- database
- Redis
- Kafka
- queues
- external providers

Use:

- OpenTelemetry
- Prometheus
- Grafana
- Loki
- Tempo

==================================================
SLO/SLI ARCHITECTURE
====================

Define candidate SLI categories for:

- API
- feed
- search
- messaging
- notifications
- media processing
- event processing
- queues
- infrastructure

Do not invent numerical targets without evidence.

==================================================
MULTI-REGION ARCHITECTURE
=========================

Design:

- primary region
- secondary region
- regional application stacks
- global traffic management
- data replication
- event replication
- media replication
- regional failover
- failback

Explicitly classify each subsystem as:

- active-active
- active-passive
- region-local
- globally replicated
- reconstructable

Do not assume every system should be active-active.

==================================================
DISASTER RECOVERY
=================

Define recovery architecture for:

- database
- Redis
- search
- event streaming
- queues
- object storage
- Kubernetes/application workloads

Define:

- backups
- snapshots
- replication
- replay
- restoration
- failover
- failback

RPO/RTO values must be defined later using validated operational requirements.

==================================================
SCALING STRATEGY
================

Define scaling dimensions for:

- API replicas
- workers
- WebSocket gateways
- database
- Redis
- search
- event streaming
- media processing

Identify likely bottlenecks and mitigation strategies.

==================================================
HOTSPOT STRATEGY
================

Explicitly address:

- viral content
- celebrity/large creator accounts
- hot Redis keys
- popular hashtags
- popular audio
- high-traffic profiles
- database hot rows
- notification fanout

==================================================
CAPACITY MODEL
==============

Define the categories of capacity that must be measured:

- requests per second
- active users
- concurrent WebSocket connections
- media uploads
- media processing jobs
- event throughput
- queue throughput
- search requests
- database connections
- Redis memory

Do not invent final numbers.

==================================================
ARCHITECTURAL DECISION RECORDS
==============================

Create ADRs for at least:

ADR-001:
Modular architecture strategy.

ADR-002:
PostgreSQL source-of-truth strategy.

ADR-003:
Redis responsibilities.

ADR-004:
Kafka/Redpanda event architecture.

ADR-005:
Transactional outbox.

ADR-006:
Feed architecture.

ADR-007:
Recommendation architecture.

ADR-008:
Search architecture.

ADR-009:
Media/storage/CDN architecture.

ADR-010:
Realtime architecture.

ADR-011:
Messaging consistency.

ADR-012:
Financial ledger.

ADR-013:
Privacy/authorization architecture.

ADR-014:
Multi-region strategy.

ADR-015:
Disaster recovery strategy.

Every ADR must include:

- Context
- Problem
- Decision
- Alternatives
- Consequences

==================================================
ARCHITECTURAL OUTPUT REQUIREMENTS
=================================

Produce a comprehensive architecture document with:

1. Executive Summary
2. System Context
3. High-Level Architecture
4. Architectural Layers
5. Bounded Context Map
6. Domain Ownership
7. Identity Architecture
8. Account Architecture
9. Profile Architecture
10. Social Graph
11. Authorization
12. Privacy
13. Content
14. Media
15. Stories
16. Reels
17. Engagement
18. Feed
19. Recommendations
20. Trending
21. Search
22. Messaging
23. Realtime
24. Notifications
25. Creator/Business
26. Monetization
27. Advertising
28. Commerce
29. Moderation
30. Rights Management
31. Analytics
32. Privacy/Data Lifecycle
33. Administration
34. API Architecture
35. Event Architecture
36. Queue Architecture
37. Webhook Architecture
38. Consistency Model
39. Failure Model
40. Security Architecture
41. Threat Model
42. Observability
43. SLO/SLI Model
44. Multi-Region Architecture
45. Disaster Recovery
46. Scaling Strategy
47. Capacity Model
48. ADR Index
49. Data Ownership Matrix
50. Dependency Matrix

==================================================
DIAGRAM REQUIREMENTS
====================

Include textual diagrams for:

- system context
- high-level architecture
- bounded contexts
- content/media pipeline
- feed pipeline
- recommendation pipeline
- search pipeline
- messaging/realtime
- event architecture
- notification fanout
- privacy evaluation
- multi-region topology
- disaster recovery

==================================================
DATABASE ARCHITECTURE REQUIREMENT
=================================

This volume must describe the logical database architecture, but it must NOT generate executable Prisma schema code.

Define:

- domain ownership
- major entity groups
- aggregate boundaries
- transactional boundaries
- high-level relationships
- indexing philosophy
- partitioning philosophy
- retention philosophy

The detailed field-level entity model and API contracts will be completed in the next architecture specification phase.

==================================================
IMPORTANT
=========

Do not generate source code.

Do not generate implementation files.

Do not generate executable schemas.

Do not generate deployment manifests.

Do not generate infrastructure code.

Produce architecture, engineering specifications, diagrams, models, responsibilities, consistency rules, and decisions only.

The architecture must be internally consistent.

Do not leave important architectural questions unresolved.

Where an exact implementation choice can safely be deferred, explicitly identify the boundary and the constraint that future implementation must respect.

BEGIN WITH:

1. EXECUTIVE ARCHITECTURE SUMMARY
2. SYSTEM CONTEXT
3. HIGH-LEVEL ARCHITECTURE
4. ARCHITECTURAL LAYERS
5. BOUNDED CONTEXT MAP
6. DOMAIN OWNERSH

You are operating in Senior Engineering Team Mode.

Design the complete foundational architecture for an enterprise-scale global visual-social platform comparable in architectural scope to Instagram.

The platform is an original implementation.

Do not copy proprietary source code, internal architecture, branding, confidential implementation details, proprietary algorithms, recommendation models, private datasets, or private implementation details from Instagram, Meta, or any other company.

This prompt is completely independent and may be executed in a separate conversation.

This is an ARCHITECTURE PHASE.

DO NOT generate source code.

DO NOT generate backend implementation.

DO NOT generate frontend implementation.

DO NOT generate mobile implementation.

DO NOT generate Dockerfiles.

DO NOT generate Kubernetes manifests.

DO NOT generate Terraform.

DO NOT generate CI/CD workflows.

Produce only:

• Architecture
• Specifications
• Contracts
• Domain models
• Service boundaries
• Data ownership
• API contracts
• Event contracts
• Queue contracts
• State machines
• Security models
• Privacy models
• Scalability strategies
• Media architecture
• Feed architecture
• Recommendation architecture
• Search architecture
• Messaging architecture
• Moderation architecture
• Analytics architecture
• Advertising architecture
• Multi-region architecture
• Disaster recovery
• Testing architecture
• Architectural Decision Records
• Implementation roadmaps

────────────────────────────────────────

PLATFORM

Design a global visual-social platform supporting:

• User accounts
• Profiles
• Creator profiles
• Professional/business profiles
• Public accounts
• Private accounts
• Follow graph
• Follow requests
• Followers
• Following
• Blocking
• Restriction
• Posts
• Photos
• Videos
• Carousels
• Stories
• Story highlights
• Short-form video / reels
• Captions
• Hashtags
• Mentions
• Locations
• Audio
• Music
• Likes
• Comments
• Replies
• Saves
• Collections
• Shares
• Reposts
• Direct messages
• Group messaging
• Message requests
• Notifications
• Explore
• Home feed
• Following feed
• Reels feed
• Search
• Creator discovery
• Hashtag discovery
• Audio discovery
• Trending
• Live-streaming foundation
• Creator analytics
• Professional analytics
• Advertising
• Business profiles
• Shopping foundation
• Product catalog
• Product tags
• Moderation
• Safety
• Reporting
• Copyright/rights
• Fraud/abuse prevention
• Privacy
• Data export
• Data deletion
• Administration
• Feature flags
• Dynamic configuration
• Audit
• Multi-region
• CDN
• Object storage
• High availability
• Disaster recovery

────────────────────────────────────────

PRIMARY USER EXPERIENCES

CONSUMER

• Home
• Following
• Explore
• Reels
• Stories
• Search
• Profile
• Creator profiles
• Hashtag pages
• Audio pages
• Notifications
• Messages
• Saved
• Collections
• Activity
• Settings
• Privacy
• Security
• Safety

CREATOR

• Profile
• Creator dashboard
• Post creation
• Carousel creation
• Reel creation
• Story creation
• Drafts
• Upload
• Captions
• Hashtags
• Mentions
• Location tags
• Audio
• Cover selection
• Publishing
• Content management
• Comments
• Analytics
• Rights
• Moderation status

BUSINESS

• Business profile
• Business information
• Verification foundation
• Posts
• Reels
• Stories
• Product catalog
• Product tags
• Messaging
• Analytics
• Advertising

ADMIN

• Users
• Profiles
• Content
• Stories
• Reels
• Comments
• Reports
• Moderation
• Rights
• Messaging
• Search
• Feed
• Recommendations
• Advertising
• Analytics
• Feature flags
• Configuration
• Audit
• Privacy

────────────────────────────────────────

PRIMARY TECHNOLOGY STACK

WEB

• Next.js
• React
• TypeScript
• Tailwind CSS
• shadcn/ui
• TanStack Query
• Zustand

MOBILE

• React Native
• Expo
• TypeScript
• React Navigation

BACKEND

• Node.js
• NestJS
• TypeScript

DATABASE

• PostgreSQL
• Prisma ORM

CACHE

• Redis

EVENT STREAMING

• Kafka or Redpanda

BACKGROUND PROCESSING

• BullMQ

SEARCH

• Elasticsearch or OpenSearch

OBJECT STORAGE

• AWS S3

CDN

• CloudFront

MEDIA

• FFmpeg
• Image processing abstraction
• Video transcoding
• HLS
• Adaptive media delivery

REAL-TIME

• WebSockets
• Socket.IO

PUSH

• FCM
• APNS

OBSERVABILITY

• OpenTelemetry
• Prometheus
• Grafana
• Loki
• Tempo

INFRASTRUCTURE

• Docker
• Kubernetes
• Helm
• Terraform
• AWS
• GitHub Actions

SECURITY

• IAM
• KMS
• Secrets Manager
• WAF
• RBAC
• NetworkPolicies

────────────────────────────────────────

ARCHITECTURAL PRINCIPLES

Use:

• Clean Architecture
• Domain-Driven Design
• SOLID
• Repository Pattern
• Service Layer
• Dependency Injection
• Explicit domain ownership
• Event-driven architecture
• Transactional Outbox
• Idempotent consumers
• Cursor-based pagination
• CDN-first media delivery
• Object-storage-first media architecture
• Horizontal scalability
• Regionalization
• Provider abstraction
• Graceful degradation
• Versioned media
• Rebuildable derived systems

Use CQRS only where justified.

Avoid:

• One giant social service
• API-proxied media
• Redis as source of truth
• Search as source of truth
• Client-authoritative privacy
• Feed ranking inside controllers
• Unlimited feed fan-out
• Unlimited raw analytics retention
• Global synchronous dependencies
• Hard-coded external providers

────────────────────────────────────────

ARCHITECTURE APPROACH

Evaluate:

• Modular monolith
• Service-oriented architecture
• Microservices

Base the final approach on:

• Social graph scale
• Media scale
• Feed traffic
• Recommendation workloads
• Search workloads
• Story traffic
• Reel traffic
• Messaging
• Notification volume
• Moderation volume
• Analytics volume
• Multi-region needs
• Team ownership
• Operational complexity

Clearly define:

• Which components are independently deployable
• Which components can initially share runtime
• Which components should be extracted later

────────────────────────────────────────

DOMAIN DECOMPOSITION

Define bounded contexts for:

IDENTITY

• Accounts
• Sessions
• Devices
• Authentication

PROFILES

• User profiles
• Creator profiles
• Business profiles
• Verification

SOCIAL GRAPH

• Follows
• Follow requests
• Blocks
• Restrictions
• Close friends

CONTENT

• Posts
• Carousels
• Reels
• Stories
• Highlights
• Drafts

MEDIA

• Images
• Videos
• Uploads
• Processing
• Renditions
• Posters
• Captions

ENGAGEMENT

• Likes
• Comments
• Replies
• Saves
• Collections
• Shares
• Reposts
• Mentions

DISCOVERY

• Home feed
• Following feed
• Explore
• Reels feed
• Recommendations
• Trending

SEARCH

• Users
• Creators
• Posts
• Reels
• Hashtags
• Audio
• Locations

AUDIO

• Sounds
• Music
• Audio assets
• Rights

STORIES

• Story lifecycle
• Story viewers
• Story interactions
• Highlights

MESSAGING

• Conversations
• Messages
• Attachments
• Delivery
• Read state
• Message requests

NOTIFICATIONS

• In-app
• Push
• Email
• Preferences

TRUST

• Reports
• Moderation
• Safety
• Fraud
• Abuse
• Rights

COMMERCE

• Business
• Products
• Catalogs
• Product tags

ADVERTISING

• Advertisers
• Campaigns
• Ad sets
• Creatives
• Placement
• Analytics

ANALYTICS

• Content analytics
• Creator analytics
• Business analytics
• Platform analytics
• Advertising analytics

PLATFORM

• Administration
• Feature flags
• Configuration
• Audit
• Privacy

────────────────────────────────────────

SERVICE DECOMPOSITION

Evaluate:

• API Gateway
• Identity Service
• Account Service
• Profile Service
• Creator Service
• Business Service
• Device Service
• Social Graph Service
• Content Service
• Media Service
• Image Processing Service
• Video Processing Service
• Story Service
• Reel Service
• Highlight Service
• Feed Service
• Recommendation Service
• Explore Service
• Trending Service
• Search Service
• Hashtag Service
• Audio Service
• Location Service
• Engagement Service
• Comment Service
• Collection Service
• Messaging Service
• Notification Service
• Reporting Service
• Moderation Service
• Safety Service
• Fraud Service
• Rights Service
• Commerce Service
• Advertising Service
• Analytics Service
• Privacy Service
• Administration Service
• Feature Flag Service
• Configuration Service
• Audit Service

Do not create unnecessary microservices.

For every final service define:

• Responsibility
• Owned data
• Read models
• APIs
• Events produced
• Events consumed
• Synchronous dependencies
• Asynchronous dependencies
• Scaling profile
• Availability
• Security boundary
• Regional ownership

────────────────────────────────────────

SOURCE-OF-TRUTH MATRIX

Define authoritative ownership for:

• Users
• Accounts
• Profiles
• Creator status
• Business profiles
• Verification
• Follows
• Follow requests
• Blocks
• Restrictions
• Posts
• Reels
• Stories
• Highlights
• Media assets
• Audio
• Hashtags
• Mentions
• Likes
• Comments
• Saves
• Collections
• Shares
• Reposts
• Messages
• Notifications
• Search
• Feed candidates
• Recommendations
• Reports
• Moderation
• Rights
• Products
• Catalogs
• Advertising
• Analytics
• Privacy

No service may directly mutate another service's authoritative database.

────────────────────────────────────────

SYSTEM CONTEXT

Provide a complete architecture diagram containing:

CLIENTS

• Web
• iOS
• Android
• Creator tools
• Business tools
• Admin tools

EDGE

• Route 53
• CloudFront
• WAF
• Load balancer
• API Gateway

APPLICATION

• Identity
• Profiles
• Social graph
• Content
• Media
• Stories
• Reels
• Feed
• Recommendations
• Search
• Messaging
• Notifications
• Moderation
• Rights
• Advertising
• Commerce
• Analytics
• Privacy
• Administration

DATA

• PostgreSQL
• Redis
• Kafka
• OpenSearch
• S3

MEDIA

• Upload
• Processing
• Image optimization
• Video transcoding
• HLS packaging
• CDN

OBSERVABILITY

• Logs
• Metrics
• Traces
• Alerts

SECURITY

• IAM
• KMS
• Secrets
• WAF
• Audit

────────────────────────────────────────

MEDIA ARCHITECTURE

Treat media as a first-class platform subsystem.

Support:

• Photos
• Videos
• Carousels
• Reels
• Stories
• Avatars
• Business assets
• Product images

Architecture:

Client
→ Upload Authorization
→ Direct S3 Upload
→ Validation
→ Processing
→ Moderation
→ Renditions
→ Publication
→ CDN

Avoid proxying large media through application servers.

────────────────────────────────────────

MEDIA ASSET MODEL

Define:

• Media ID
• Owner
• Media type
• Original reference
• Processing status
• Moderation state
• Rights state
• Region
• Version
• Created time
• Updated time

────────────────────────────────────────

IMAGE ARCHITECTURE

Support:

• Original
• Large
• Medium
• Small
• Thumbnail
• Feed variant
• Avatar
• Story variant
• Reel cover
• Product image

Support:

• Responsive sizes
• Web-friendly formats
• Mobile-friendly variants
• Orientation
• Metadata stripping where appropriate

────────────────────────────────────────

VIDEO ARCHITECTURE

Support:

• Original upload
• Processing
• Transcoding
• Renditions
• Poster
• Thumbnail
• HLS
• Adaptive playback

Define versioned processing profiles.

────────────────────────────────────────

VIDEO PROCESSING PIPELINE

Upload
→ Validate
→ Metadata Extraction
→ Security Scan
→ Transcode
→ Poster/Thumbnail
→ Caption Processing
→ HLS Packaging
→ Moderation
→ Publish

Define asynchronous processing.

────────────────────────────────────────

STORY ARCHITECTURE

Support:

• Story item
• Story sequence
• Story expiration
• Story viewer state
• Story replies
• Story reactions foundation
• Story mentions
• Story highlights

Story states:

• Draft
• Processing
• Published
• Restricted
• Expired
• Archived
• Deleted

────────────────────────────────────────

STORY PRIVACY

Support:

• Public
• Followers
• Close friends
• Custom restrictions

Visibility must remain server-authoritative.

────────────────────────────────────────

STORY EXPIRATION

Define:

• Expiration timestamp
• Viewer availability window
• Highlight archival rules

Do not allow expired stories to remain publicly discoverable through search or feeds.

────────────────────────────────────────

REELS ARCHITECTURE

Support:

• Short video
• Cover
• Caption
• Hashtags
• Mentions
• Audio
• Location
• Likes
• Comments
• Shares
• Saves
• Reposts
• Feed distribution
• Explore distribution

Reels reuse the media subsystem but maintain product-specific semantics.

────────────────────────────────────────

POST ARCHITECTURE

Support:

• Image
• Video
• Carousel
• Caption
• Hashtags
• Mentions
• Location
• Collaboration foundation
• Likes
• Comments
• Shares
• Saves
• Reposts

Post states:

• Draft
• Processing
• Moderation
• Published
• Restricted
• Archived
• Deleted

────────────────────────────────────────

SOCIAL GRAPH

Support:

• Follow
• Unfollow
• Follow request
• Accept
• Reject
• Remove follower
• Block
• Unblock
• Restrict
• Close friends

Define graph consistency and propagation.

────────────────────────────────────────

PRIVATE ACCOUNTS

For private accounts:

• Follow requires approval
• Content visibility is restricted
• Search results respect privacy
• Mentions respect privacy
• Messaging respects permissions

Server authorization is authoritative.

────────────────────────────────────────

BLOCKING

A block may affect:

• Follow
• Messaging
• Comments
• Mentions
• Notifications
• Search
• Feed
• Explore
• Reels

Define propagation events.

────────────────────────────────────────

RESTRICTION

Support:

• Comment restriction
• Message restriction
• Mention restriction

Clearly distinguish restriction from block.

────────────────────────────────────────

CLOSE FRIENDS

Support:

• List
• Add
• Remove
• Story visibility integration

Close-friends membership is private.

────────────────────────────────────────

FEED ARCHITECTURE

Define:

• Home
• Following
• Reels
• Story tray

Pipeline:

Request
→ User context
→ Candidate generation
→ Eligibility
→ Ranking
→ Re-ranking
→ Diversity
→ Response

────────────────────────────────────────

HOME FEED CANDIDATES

Potential sources:

• Followed accounts
• Creator affinity
• Similar content
• Saved interests
• Hashtag affinity
• Audio affinity
• Explore
• Trending
• Fresh content

────────────────────────────────────────

FEED ELIGIBILITY

Filter:

• Private content
• Deleted content
• Restricted content
• Rights-restricted content
• Blocked accounts
• Region-restricted content
• Age-restricted content
• Safety-restricted content

Eligibility must run after candidate generation and before final delivery.

────────────────────────────────────────

RECOMMENDATION ARCHITECTURE

Support:

• Content embeddings abstraction
• Creator affinity
• Hashtag affinity
• Audio affinity
• User interests
• Negative feedback
• Freshness
• Quality
• Engagement

Ranking must be pluggable.

Support progression:

• Rule-based
• Weighted scoring
• Statistical model
• ML inference

────────────────────────────────────────

RECOMMENDATION FEEDBACK

Consume:

• Impression
• Watch
• Completion
• Skip
• Rewatch
• Like
• Comment
• Share
• Save
• Follow
• Profile visit
• Not interested
• Report

Separate:

• Raw event
• Feature
• Ranking signal

────────────────────────────────────────

EXPLORE

Support discovery for:

• Posts
• Reels
• Creators
• Hashtags
• Audio
• Trending

Define independent candidate and ranking strategies.

────────────────────────────────────────

STORY TRAY

Define:

• Candidate selection
• Recency
• Unseen story priority
• Close-friends priority
• Creator affinity
• Eligibility

Do not display expired stories.

────────────────────────────────────────

SEARCH

Search:

• Users
• Creators
• Posts
• Reels
• Hashtags
• Audio
• Locations

Support:

• Full text
• Prefix
• Typo tolerance
• Popularity
• Freshness
• Personalization
• Geography where applicable

────────────────────────────────────────

HASHTAGS

Support:

• Identity
• Search
• Related hashtags
• Popular posts
• Reels
• Trending
• Following

Respect moderation and privacy.

────────────────────────────────────────

AUDIO

Support:

• Audio asset
• Creator/attribution
• Duration
• Usage
• Search
• Trending
• Reels using audio
• Rights
• Regions

────────────────────────────────────────

ENGAGEMENT

Support:

• Like
• Unlike
• Comment
• Reply
• Comment like
• Save
• Collection
• Share
• Repost
• Mention

Separate:

• Source-of-truth relationship
• Event
• Aggregate counters

────────────────────────────────────────

COUNTERS

Derived counters may include:

• Likes
• Comments
• Shares
• Saves
• Reposts
• Followers

Define:

• Source
• Update method
• Reconciliation
• Tolerance

Counters are not authoritative relationships.

────────────────────────────────────────

MESSAGING

Support:

• One-to-one
• Group
• Message request
• Conversation
• Message
• Attachment
• Delivery
• Read state
• Reactions foundation
• Reply foundation
• Block
• Report

Define:

• Ordering
• Idempotency
• Reconnect
• Offline delivery

────────────────────────────────────────

MESSAGE REQUESTS

Support:

• Incoming requests
• Accept
• Reject
• Delete
• Restrict
• Block

Messaging permission is independent of follow state unless product policy explicitly links them.

────────────────────────────────────────

NOTIFICATIONS

Support:

• Follows
• Follow requests
• Likes
• Comments
• Mentions
• Shares
• Reposts
• Messages
• Story interactions
• Creator updates
• Moderation
• Rights
• Security

Channels:

• In-app
• Push
• Email where approved

────────────────────────────────────────

MODERATION

Moderate:

• Posts
• Reels
• Stories
• Profiles
• Comments
• Audio
• Hashtags
• Messages where policy/legal basis permits
• Business content
• Product content

Architecture:

Content
→ Detection
→ Classification
→ Policy
→ Decision
→ Enforcement
→ Appeal

────────────────────────────────────────

REPORTING

Users can report:

• Account
• Post
• Reel
• Story
• Comment
• Message
• Audio
• Hashtag
• Product
• Business

Prevent:

• Duplicate reports
• Report flooding
• Coordinated false reports

────────────────────────────────────────

COPYRIGHT / RIGHTS

Support:

• Rights reference
• Claim
• Takedown
• Audio restriction
• Region restriction
• Content restriction
• Appeal
• Restoration
• Expiration

Rights may affect:

• Playback
• Feed
• Explore
• Search
• Audio usage
• Sharing

────────────────────────────────────────

CREATOR ANALYTICS

Support:

• Views
• Reach
• Impressions
• Watch time
• Completion
• Average watch duration
• Likes
• Comments
• Shares
• Saves
• Reposts
• Follower growth
• Traffic source
• Region aggregates
• Content performance

Do not expose sensitive individual viewer information.

────────────────────────────────────────

BUSINESS / PROFESSIONAL ANALYTICS

Support:

• Profile visits
• Content views
• Reach
• Engagement
• Search discovery
• Product interactions
• Ad performance
• Followers

Use aggregates.

────────────────────────────────────────

ADVERTISING

Support:

• Advertiser
• Organization
• Campaign
• Ad set
• Creative
• Placement
• Budget
• Schedule
• Frequency cap
• Eligibility
• Impression
• Click
• Video engagement
• Conversion reference

Do not use prohibited sensitive attributes.

────────────────────────────────────────

COMMERCE

Support architecture for:

• Business
• Product catalog
• Product
• Collection
• Product tag
• Product availability
• Product analytics

Keep commerce ownership separate from social content.

────────────────────────────────────────

LIVE STREAMING FOUNDATION

Define:

• Live session
• Stream state
• Ingest
• Playback
• Viewer count
• Chat
• Moderation
• Recording reference

Streaming infrastructure should remain separable from normal video upload processing.

────────────────────────────────────────

PRIVACY

Protect:

• Private profiles
• Close-friends lists
• Messages
• Search history
• Saved content
• Viewer activity
• Location
• Device information
• Behavioral profiles
• Creator analytics
• Moderation evidence

Support:

• Data access
• Export
• Deletion
• Account deletion
• Retention
• Personalization controls
• Advertising controls

────────────────────────────────────────

DATA RETENTION

Define retention for:

• Stories
• Messages
• Raw events
• Search history
• Recommendation features
• Analytics
• Moderation
• Rights
• Audit
• Media

Do not retain sensitive behavioral data indefinitely.

────────────────────────────────────────

ANALYTICS ARCHITECTURE

Pipeline:

Application
→ Event
→ Kafka
→ Validation
→ Enrichment
→ Aggregation
→ Analytical Storage
→ Reporting

Analytics must not block transactional operations.

────────────────────────────────────────

EVENT ARCHITECTURE

Define event families:

IDENTITY

• UserCreated
• SessionCreated
• DeviceRegistered

SOCIAL

• FollowCreated
• FollowRemoved
• FollowRequestCreated
• FollowRequestAccepted
• BlockCreated
• BlockRemoved
• RestrictionCreated
• CloseFriendsChanged

CONTENT

• PostCreated
• PostPublished
• PostUpdated
• PostDeleted
• ReelCreated
• ReelPublished
• ReelDeleted
• StoryPublished
• StoryExpired
• HighlightCreated

MEDIA

• UploadInitialized
• UploadCompleted
• MediaProcessingStarted
• MediaProcessingCompleted
• MediaProcessingFailed

ENGAGEMENT

• PostLiked
• PostUnliked
• CommentCreated
• CommentDeleted
• CommentLiked
• PostSaved
• PostUnsaved
• CollectionUpdated
• PostShared
• RepostCreated
• RepostRemoved
• MentionCreated

DISCOVERY

• FeedGenerated
• RecommendationServed
• ExploreServed
• SearchPerformed

MESSAGING

• ConversationCreated
• MessageCreated
• MessageDelivered
• MessageRead
• MessageDeleted

NOTIFICATIONS

• NotificationCreated
• NotificationDelivered
• NotificationFailed

TRUST

• ReportCreated
• ModerationCaseCreated
• ModerationActionTaken
• AppealCreated
• AppealResolved
• RightsClaimCreated
• RightsRestrictionApplied
• RightsRestored

ADVERTISING

• AdServed
• AdImpression
• AdClick
• AdVideoStarted
• AdVideoCompleted

COMMERCE

• ProductCreated
• ProductUpdated
• ProductTagged

PRIVACY

• PrivacyRequestCreated
• DataExportCompleted
• DataDeletionCompleted

ADMIN

• FeatureFlagChanged
• ConfigurationChanged
• AdministrativeActionTaken

Every event must be:

• Versioned
• Idempotent
• Privacy-aware
• Correlation-aware
• Region-aware

────────────────────────────────────────

QUEUE ARCHITECTURE

Define BullMQ queues for:

• Media validation
• Image processing
• Video processing
• HLS packaging
• Thumbnail generation
• Caption generation
• Story expiration
• Feed refresh
• Recommendation refresh
• Search indexing
• Trending aggregation
• Notification delivery
• Message cleanup
• Moderation
• Rights
• Analytics
• Advertising
• Commerce
• Privacy export
• Privacy deletion
• Reconciliation
• Object cleanup

For each queue define:

• Producer
• Consumer
• Job schema
• Retry
• Backoff
• Timeout
• Concurrency
• Dead-letter
• Scaling
• Metrics

────────────────────────────────────────

DATABASE ARCHITECTURE

Use PostgreSQL for authoritative transactional data.

Conceptual models:

IDENTITY

• User
• Account
• Session
• Device

PROFILES

• Profile
• CreatorProfile
• BusinessProfile
• Verification

SOCIAL

• Follow
• FollowRequest
• Block
• Restriction
• CloseFriend

CONTENT

• Post
• PostMedia
• CarouselItem
• Reel
• Story
• StoryItem
• StoryViewer
• StoryHighlight
• Draft

MEDIA

• MediaAsset
• MediaRendition
• MediaProcessingJob
• MediaManifest
• MediaCaption

ENGAGEMENT

• Like
• Comment
• CommentLike
• Save
• Collection
• CollectionItem
• Share
• Repost
• Mention

DISCOVERY

• FeedSession
• FeedCandidateReference
• RecommendationProfile
• RecommendationExperiment

AUDIO

• Audio
• AudioUsage
• AudioRights

SEARCH

• SearchConfiguration
• SearchIndexVersion

MESSAGING

• Conversation
• ConversationParticipant
• Message
• MessageAttachment
• MessageDelivery

NOTIFICATIONS

• Notification
• NotificationPreference
• NotificationDelivery
• PushDevice

TRUST

• Report
• ModerationCase
• ModerationAction
• Appeal
• RightsClaim
• RightsRestriction

COMMERCE

• ProductCatalog
• Product
• ProductCollection
• ProductTag

ADVERTISING

• AdAccount
• Campaign
• AdSet
• AdCreative
• AdEventReference

ANALYTICS

• AnalyticsAggregate

PLATFORM

• AuditLog
• PrivacyRequest
• FeatureFlag
• SystemConfiguration

────────────────────────────────────────

DATABASE OWNERSHIP

Every domain owns its tables.

Cross-domain access uses:

• APIs
• Events
• Read models
• Explicit integration contracts

Never use cross-domain database writes as integration.

────────────────────────────────────────

INDEXING

Use indexes for:

SOCIAL

• Follower
• Following
• Requests
• Block
• Restriction

CONTENT

• Creator
• Publication status
• Created time
• Visibility

ENGAGEMENT

• Post/user
• Comment/post
• Collection/user

MESSAGING

• Participant
• Conversation
• Message/time
• Delivery

SEARCH/CONTENT

• Hashtag
• Audio
• Public profile

TRUST

• Report target
• Moderation status
• Appeal

────────────────────────────────────────

REDIS

Use Redis for:

• Feed cache
• Explore cache
• Story tray
• Recommendation features
• Session state
• Rate limits
• Presence
• Typing indicators
• Message deduplication
• Notification deduplication
• Upload sessions
• Media locks
• Trending
• Feature-flag cache

Redis must never be authoritative for:

• Users
• Profiles
• Posts
• Stories
• Reels
• Follows
• Messages
• Moderation
• Rights
• Advertising
• Commerce

────────────────────────────────────────

SEARCH ARCHITECTURE

Search indexes:

• Users
• Creators
• Posts
• Reels
• Hashtags
• Audio
• Public business profiles
• Products where approved

Support:

• Full text
• Prefix
• Typo tolerance
• Popularity
• Freshness
• Personalization
• Region

Search index must be rebuildable.

────────────────────────────────────────

FEED CACHE

Cache:

• Personalized feed pages
• Following feed candidates
• Explore candidates
• Story tray candidates
• Trending

Keys must include:

• Environment
• Region
• User
• Feed type
• Ranking version

Define:

• TTL
• Invalidation
• Stampede protection
• Fallback

────────────────────────────────────────

MEDIA CACHE

CloudFront should cache:

• HLS manifests
• Video segments
• Image derivatives
• Thumbnails
• Posters
• Static assets

Use secure origin access.

────────────────────────────────────────

MULTI-REGION

Design:

• Regional APIs
• Regional feed
• Regional search
• Regional media processing
• Regional messaging
• Regional moderation
• Regional analytics

Use:

• Global CDN
• Global DNS
• Regional data ownership
• Event replication where necessary

Avoid global synchronous workflows.

────────────────────────────────────────

CONSISTENCY

Strong consistency for:

• Account state
• Profile ownership
• Follow-request authorization
• Blocks
• Private-content access
• Message acceptance
• Business ownership
• Privacy controls

Eventual consistency for:

• Feed
• Explore
• Search
• Analytics
• Trending
• Engagement counters
• Recommendations

Define acceptable staleness.

────────────────────────────────────────

SECURITY ARCHITECTURE

Protect:

• Accounts
• Private profiles
• Private posts
• Messages
• Media
• Collections
• Creator analytics
• Business data
• Advertising data
• Moderation data
• Rights data

Use:

• Authentication
• Authorization
• RBAC
• Resource ownership
• Rate limits
• Secure media access
• Encryption
• Audit

────────────────────────────────────────

THREAT MODEL

Analyze:

• Account takeover
• Session theft
• Credential abuse
• IDOR
• Private-content leakage
• Media scraping
• CDN origin bypass
• Spam
• Fake engagement
• Fake followers
• Message abuse
• Report abuse
• Recommendation manipulation
• Search manipulation
• Advertising fraud
• Business impersonation
• Copyright abuse
• Admin escalation

For every threat define:

• Prevention
• Detection
• Response
• Recovery

────────────────────────────────────────

PRIVACY MODEL

Classify:

• Identity
• Social graph
• Content
• Messaging
• Search history
• Behavioral data
• Location
• Analytics
• Moderation
• Rights
• Advertising
• Commerce

For each define:

• Access control
• Retention
• Deletion
• Export
• Audit
• Encryption

────────────────────────────────────────

OBSERVABILITY

Track:

• API latency
• Feed latency
• Explore latency
• Search latency
• Media-processing latency
• Video processing backlog
• Story publication
• Reel processing
• Message latency
• Notification latency
• Moderation backlog
• Analytics lag
• Kafka lag
• Queue depth
• CDN errors
• Upload errors
• Playback errors

Never expose sensitive user data through logs.

────────────────────────────────────────

SLO / SLI

Define SLOs for:

• Authentication
• Feed
• Explore
• Search
• Upload
• Media processing
• Playback authorization
• Messaging
• Notifications
• Story publication
• Reel publication
• Moderation
• Advertising
• Analytics
• Privacy

For each define:

• SLI
• Measurement source
• Target
• Error budget
• Alert threshold

────────────────────────────────────────

FAILURE MODES

Define graceful degradation for:

• Feed outage
• Explore outage
• Search outage
• Media-processing outage
• Messaging outage
• Notification outage
• Recommendation outage
• Kafka outage
• Redis outage
• Search outage
• Database degradation
• CDN/origin failure
• External provider outage

Fallback examples:

• Cached feed
• Following feed
• Trending
• Previously available media
• Queue buffering

────────────────────────────────────────

DISASTER RECOVERY

Define recovery for:

• PostgreSQL
• Redis
• Kafka
• OpenSearch
• S3
• EKS
• Media processing
• Search
• Feed
• Recommendations
• Messaging

Derived systems must be rebuildable from authoritative data.

────────────────────────────────────────

TESTING ARCHITECTURE

UNIT:

• Privacy rules
• Visibility
• Follow rules
• Story lifecycle
• Post lifecycle
• Reel lifecycle
• Engagement rules
• Feed eligibility
• Ranking contracts
• Search normalization
• Moderation
• Rights
• Notification routing

INTEGRATION:

• PostgreSQL
• Redis
• Kafka
• BullMQ
• OpenSearch
• S3
• WebSockets

MEDIA:

• Image processing
• Video processing
• HLS
• CDN
• Upload
• Secure playback

SOCIAL:

• Follow
• Follow request
• Block
• Restrict
• Close friends

MESSAGING:

• Conversation
• Message
• Delivery
• Read
• Reconnect

DISCOVERY:

• Feed
• Explore
• Search
• Recommendations

TRUST:

• Reporting
• Moderation
• Rights
• Appeals

SECURITY:

• IDOR
• Private content
• Media
• Messaging
• Admin
• Privacy

PERFORMANCE:

• Feed
• Explore
• Search
• Messaging
• Media
• Notifications

────────────────────────────────────────

ARCHITECTURAL DECISION RECORDS

Create ADRs for:

• Architecture approach
• Social graph
• Feed strategy
• Recommendation abstraction
• Media architecture
• S3
• CloudFront
• Image processing
• Video processing
• HLS
• Stories
• Reels
• Search
• Hashtags
• Audio
• Messaging
• Notifications
• Moderation
• Rights
• Advertising
• Commerce
• Analytics
• Privacy
• Multi-region
• Redis
• Kafka
• PostgreSQL
• Disaster recovery

Each ADR must contain:

• Context
• Decision
• Alternatives
• Consequences

────────────────────────────────────────

ARCHITECTURE VOLUME 1 OUTPUT

Produce:

1. Executive Architecture Overview
2. Platform Scope
3. Architecture Approach
4. Domain Decomposition
5. Service Decomposition
6. Source-of-Truth Matrix
7. System Context Diagram
8. Client Architecture
9. Media Architecture
10. Media Asset Model
11. Image Architecture
12. Video Architecture
13. Video Processing Pipeline
14. Story Architecture
15. Story Privacy
16. Story Expiration
17. Reels Architecture
18. Post Architecture
19. Social Graph
20. Private Accounts
21. Blocking
22. Restriction
23. Close Friends
24. Feed Architecture
25. Feed Candidate Architecture
26. Feed Eligibility
27. Recommendation Architecture
28. Recommendation Feedback
29. Explore
30. Story Tray
31. Search
32. Hashtags
33. Audio
34. Engagement
35. Counters
36. Messaging
37. Message Requests
38. Notifications
39. Moderation
40. Reporting
41. Copyright/Rights
42. Creator Analytics
43. Business Analytics
44. Advertising
45. Commerce
46. Live Streaming Foundation
47. Privacy
48. Data Retention
49. Analytics Architecture
50. Event Architecture
51. Queue Architecture
52. Database Architecture
53. Database Ownership
54. Database Indexing
55. Redis
56. Search Architecture
57. Feed Cache
58. Media Cache
59. Multi-Region
60. Consistency Model
61. Security Architecture
62. Threat Model
63. Privacy Model
64. Observability
65. SLO/SLI
66. Failure Modes
67. Disaster Recovery
68. Testing Architecture
69. Architectural Decision Records
70. Implementation Roadmap

────────────────────────────────────────

IMPLEMENTATION ROADMAP

BACKEND

Milestone 1:
Backend foundation, identity, accounts, profiles, devices, configuration, observability.

Milestone 2:
Social graph, follows, follow requests, blocks, restrictions, close friends.

Milestone 3:
Media, uploads, image processing, video processing, S3, CDN.

Milestone 4:
Posts, carousels, stories, highlights, reels, drafts.

Milestone 5:
Likes, comments, replies, saves, collections, shares, reposts, mentions.

Milestone 6:
Home feed, following feed, story tray, explore, trending, recommendations.

Milestone 7:
Search, hashtags, audio, locations, discovery.

Milestone 8:
Messaging, message requests, WebSockets, notifications.

Milestone 9:
Moderation, reporting, rights, safety, appeals, abuse prevention.

Milestone 10:
Creator analytics, business analytics, advertising, commerce.

Milestone 11:
Administration, privacy, feature flags, configuration, audit.

Milestone 12:
Multi-region, reconciliation, performance, security, disaster recovery.

FRONTEND

Milestone 1:
Foundation, design system, authentication, navigation.

Milestone 2:
Home, feed, profiles, posts, reels, stories.

Milestone 3:
Explore, search, hashtags, audio, discovery.

Milestone 4:
Engagement, comments, saves, collections, sharing.

Milestone 5:
Messaging, notifications, activity.

Milestone 6:
Creator publishing, uploads, drafts, stories, reels.

Milestone 7:
Creator analytics, business tools, advertising.

Milestone 8:
Moderation, privacy, administration.

Milestone 9:
Performance, accessibility, localization, SEO.

Milestone 10:
E2E, security, regression, production readiness.

MOBILE

Milestone 1:
Expo foundation, navigation, authentication, permissions.

Milestone 2:
Feed, posts, reels, stories, profiles.

Milestone 3:
Explore, search, hashtags, audio.

Milestone 4:
Engagement, comments, saves, collections.

Milestone 5:
Messaging, notifications, sharing.

Milestone 6:
Camera, media picker, drafts, uploads.

Milestone 7:
Creator analytics, business tools, advertising.

Milestone 8:
Privacy, moderation, accessibility, battery, performance, offline resilience.

INFRASTRUCTURE

Milestone 1:
Terraform, AWS networking, IAM, EKS.

Milestone 2:
PostgreSQL, Redis, Kafka, OpenSearch, S3.

Milestone 3:
Media processing, CDN, image/video infrastructure.

Milestone 4:
Feed, recommendation, search, messaging infrastructure.

Milestone 5:
Observability, autoscaling, CI/CD, security.

Milestone 6:
Multi-region, disaster recovery, backup, chaos, production readiness.

QA

Milestone 1:
Testing foundation.

Milestone 2:
Identity and social graph.

Milestone 3:
Media, content, stories, reels.

Milestone 4:
Engagement, feed, Explore, search.

Milestone 5:
Messaging, notifications, moderation, rights.

Milestone 6:
Advertising, commerce, analytics, privacy, administration.

Milestone 7:
Security, accessibility, performance.

Milestone 8:
Load, stress, resilience, disaster recovery.

Milestone 9:
Production certification.

────────────────────────────────────────

QUALITY REQUIREMENTS

Every architectural decision must evaluate:

• Scalability
• Media performance
• Feed latency
• Recommendation quality
• Search relevance
• Messaging latency
• Story/reel throughput
• Privacy
• Security
• Moderation
• Rights
• Multi-region
• Cost
• Operational complexity
• Maintainability

Prefer:

• S3-backed media
• CloudFront
• Versioned media
• Kafka
• Redis for ephemeral state
• PostgreSQL as transaction source of truth
• Search indexes separate from canonical data
• Event-driven processing
• Queue-based media processing
• Cursor pagination
• Pluggable ranking
• Regionalization
• Rebuildable derived systems
• Server-authoritative privacy

Avoid:

• API-proxied media
• Unlimited raw-event retention
• Client-authoritative visibility
• Redis as source of truth
• Search as source of truth
• Unlimited feed precomputation
• Global synchronous fan-out
• Permanent private-media URLs
• Hard-coded provider coupling

────────────────────────────────────────

OUTPUT RULES

This is an architecture document only.

DO NOT generate source code.

DO NOT generate implementation files.

DO NOT generate Dockerfiles.

DO NOT generate Kubernetes manifests.

DO NOT generate Terraform.

DO NOT generate CI/CD.

Do not generate placeholder implementations.

Do not generate pseudo-code.

Produce only the architecture and engineering specifications required for later implementation phases.

The resulting architecture must be sufficiently detailed that independent backend, frontend, mobile, infrastructure, DevOps, media, feed, recommendation, search, messaging, moderation, advertising, commerce, analytics, security, privacy, and QA teams can implement the platform without making major architectural decisions themselves.
