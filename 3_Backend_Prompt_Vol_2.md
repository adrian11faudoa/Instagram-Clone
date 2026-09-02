You are operating in Senior Engineering Team Mode.

Build the production-ready backend for the core visual-social content and media platform of an enterprise-scale global application comparable in architectural scope to Instagram.

The platform is an original implementation.

Do not copy proprietary source code, internal architecture, branding, confidential implementation details, proprietary algorithms, proprietary datasets, or private implementation details from Instagram, Meta, or any other company.

This prompt is completely independent and may be executed in a separate conversation.

Use the previously approved architecture and backend foundation as the single source of truth.

Do not redesign the approved architecture.

Do not generate frontend code.

Do not generate mobile code.

Do not generate infrastructure implementation code.

Do not generate Terraform.

Do not generate Kubernetes manifests.

Do not generate CI/CD workflows.

────────────────────────────────────────

MISSION

Implement the production-ready backend domains for:

• Media assets
• Media uploads
• Multipart/resumable uploads
• Image processing
• Video processing
• Media validation
• Media moderation integration
• Media rights state
• Posts
• Post media
• Carousels
• Drafts
• Stories
• Story items
• Story viewers
• Story replies
• Story reactions
• Story highlights
• Reels
• Captions
• Hashtags
• Mentions
• Audio
• Music
• Location tagging
• Content visibility
• Content lifecycle
• Content versioning
• Publication
• Scheduled publication foundation
• Content deletion
• Content archival
• Content restoration
• Content access authorization

The implementation must integrate with the existing:

• Identity
• Accounts
• Profiles
• Creators
• Businesses
• Devices
• Sessions
• Social graph
• Blocks
• Restrictions
• Close friends
• PostgreSQL
• Prisma
• Redis
• Kafka/Redpanda
• BullMQ
• WebSockets
• S3 abstraction
• Observability
• Security
• Privacy

────────────────────────────────────────

PRIMARY TECHNOLOGY STACK

Backend:

• Node.js
• NestJS
• TypeScript

Database:

• PostgreSQL
• Prisma ORM

Cache:

• Redis

Event streaming:

• Kafka or Redpanda

Background processing:

• BullMQ

Object storage:

• AWS S3

CDN:

• CloudFront

Media:

• FFmpeg
• Image processing abstraction
• Video transcoding
• HLS
• Adaptive delivery

Real-time:

• WebSockets
• Socket.IO

Observability:

• OpenTelemetry
• Prometheus
• Grafana
• Loki
• Tempo

Testing:

• Jest
• Supertest
• Integration testing tools

────────────────────────────────────────

IMPLEMENTATION RULES

Never generate pseudo-code.

Never generate placeholders.

Never generate TODO comments.

Never omit implementations.

Never say:

- "implement similarly"
- "left as an exercise"
- "for brevity"
- "remaining code omitted"

Every generated file must be complete.

Every generated file must compile.

Never regenerate unchanged files.

Only modify existing files when required.

Use strict TypeScript.

Use dependency injection.

Keep controllers thin.

Keep business logic outside controllers.

Use repositories for persistence.

Use DTOs for external contracts.

Use centralized validation.

Use centralized error handling.

Use structured logging.

Use idempotency for uploads, publication, jobs, and retriable mutations.

Use optimistic concurrency where appropriate.

Never trust client-supplied ownership.

Never trust client-supplied visibility.

Never trust client-supplied moderation status.

Never expose private-media credentials.

────────────────────────────────────────

DOMAIN OWNERSHIP

Maintain explicit boundaries between:

• Media
• Posts
• Stories
• Reels
• Audio
• Hashtags
• Mentions
• Locations
• Drafts

Do not combine:

• Media asset with post
• Processing job with publication state
• Story with reel
• Audio rights with audio metadata
• Search data with canonical content
• CDN access with content authorization

────────────────────────────────────────

MEDIA ASSET DOMAIN

Implement canonical media assets.

Support:

• Media ID
• Owner
• Media type
• Original object
• Processing state
• Moderation state
• Rights state
• Visibility reference
• Version
• Region
• Created time
• Updated time

Types:

• Image
• Video

────────────────────────────────────────

MEDIA LIFECYCLE

States:

• Uploading
• Uploaded
• Validating
• Processing
• Moderating
• Ready
• Restricted
• Failed
• Deleted

Define valid transitions.

Every transition must be:

• Authorized
• Version-aware
• Auditable
• Idempotent where appropriate

────────────────────────────────────────

MEDIA OWNERSHIP

Every media asset must be bound to:

• User
• Creator
• Business where authorized

Never allow one user to reference another user's private source asset.

────────────────────────────────────────

UPLOAD AUTHORIZATION

Implement:

• Upload session
• Direct S3 authorization
• Object namespace
• Owner binding
• Expiration
• File-size limits
• Content-type constraints
• Upload checksum

────────────────────────────────────────

UPLOAD SESSION

Fields:

• Upload session ID
• Owner
• Media type
• Expected size
• Expected MIME
• Object key reference
• Status
• Created
• Expiration
• Completed time

States:

• Initialized
• Uploading
• Completed
• Expired
• Canceled
• Failed

────────────────────────────────────────

MULTIPART UPLOAD

Support:

• Multipart initialization
• Part authorization
• Part completion
• Part retry
• Pause
• Resume
• Finalization
• Abort

Use idempotency.

Do not create duplicate media assets because a client retries completion.

────────────────────────────────────────

UPLOAD VALIDATION

Validate server-side:

• File signature
• MIME
• Size
• Container
• Codec
• Resolution
• Frame rate
• Duration
• Orientation
• Metadata
• Corruption

Client metadata is advisory only.

────────────────────────────────────────

OBJECT KEY DESIGN

Create deterministic namespaced object references using:

• Environment
• Region
• Owner reference
• Media ID
• Version
• Asset type

Do not expose raw storage structure as a public contract.

────────────────────────────────────────

MEDIA SECURITY

Protect against:

• Path traversal
• Malicious files
• MIME spoofing
• Oversized files
• Unsupported formats
• Malformed media
• Zip/decompression bombs where relevant
• Unauthorized object access

────────────────────────────────────────

IMAGE PROCESSING

Implement asynchronous processing for:

• Thumbnail
• Small
• Medium
• Large
• Feed
• Story
• Avatar
• Reel cover
• Business image
• Product image

Support:

• Resize
• Compression
• Orientation normalization
• Metadata handling
• Modern image formats

────────────────────────────────────────

VIDEO PROCESSING

Implement asynchronous processing for:

• Metadata extraction
• Validation
• Transcoding
• Poster
• Thumbnail
• Preview
• HLS
• Captions foundation
• Quality validation

Use FFmpeg workers where approved.

────────────────────────────────────────

VIDEO RENDITIONS

Support configurable profiles:

• Resolution
• Bitrate
• Codec
• Frame rate
• Audio

Every rendition references:

• Media ID
• Processing version
• Profile
• Resolution
• Codec
• Bitrate

────────────────────────────────────────

HLS

Generate:

• Master manifest
• Variant playlists
• Media segments

Validate:

• Manifest references
• Segment availability
• Rendition completeness
• Version consistency

────────────────────────────────────────

MEDIA VERSIONING

Every processing run must have:

• Media version
• Processing version
• Profile version

Older processing jobs must never overwrite newer outputs.

────────────────────────────────────────

MEDIA PROCESSING CONCURRENCY

Prevent:

• Duplicate processing
• Stale worker overwrite
• Double publication
• Concurrent state corruption

Use:

• Idempotency
• Version checks
• Locks where required
• Processing revision

────────────────────────────────────────

MEDIA ACCESS

Support:

• Public media
• Followers-only media
• Close-friends media
• Private media
• Restricted media

Access must be determined server-side.

────────────────────────────────────────

CDN ACCESS

Provide short-lived secure media access where required.

Use:

• Signed URL/cookie foundation
• CloudFront origin protection
• Object storage privacy

Never expose unrestricted private S3 objects.

────────────────────────────────────────

POST DOMAIN

Implement:

• Post
• Post media
• Post visibility
• Post state
• Caption
• Location reference
• Publication timestamp
• Creator reference

────────────────────────────────────────

POST TYPES

Support:

• Single image
• Single video
• Carousel

Do not duplicate the media binary inside post storage.

────────────────────────────────────────

POST LIFECYCLE

States:

• Draft
• Uploading
• Processing
• Moderation
• Scheduled
• Published
• Restricted
• Archived
• Deleted

Visibility remains a separate attribute.

────────────────────────────────────────

POST PUBLICATION

Publish only when:

• All required media is ready
• Required moderation has completed
• Rights state permits
• Visibility settings are valid
• Creator/account is eligible

Publication must be idempotent.

────────────────────────────────────────

SCHEDULED PUBLICATION FOUNDATION

Support:

• Scheduled time
• Time zone
• Scheduled state
• Cancellation
• Publication worker

Do not let client clocks determine server publication time.

────────────────────────────────────────

POST VISIBILITY

Support:

• Public
• Followers
• Close Friends

Integrate with:

• Private accounts
• Blocks
• Restrictions

────────────────────────────────────────

CONTENT AUTHORIZATION

For every read determine:

• Viewer
• Owner
• Account state
• Block state
• Restriction
• Follow relationship
• Visibility
• Rights
• Moderation
• Region

────────────────────────────────────────

CAROUSELS

Implement:

• Carousel
• Ordered media
• Cover item
• Item order
• Caption
• Hashtags
• Mentions
• Location

Publication requires every required media item to be valid.

────────────────────────────────────────

DRAFTS

Support drafts for:

• Posts
• Carousels
• Reels
• Stories

Drafts are:

• Private
• User-owned
• Versioned
• Recoverable

────────────────────────────────────────

DRAFT VERSIONING

Prevent concurrent editing conflicts using:

• Revision number
• Updated time
• Optimistic concurrency

────────────────────────────────────────

STORIES

Implement:

• Story
• Story item
• Story sequence
• Expiration
• Visibility
• Viewer state
• Reply
• Reaction
• Mention
• Highlight reference

────────────────────────────────────────

STORY TYPES

Support:

• Image
• Video

Use common media pipeline.

────────────────────────────────────────

STORY LIFECYCLE

States:

• Draft
• Processing
• Moderation
• Published
• Restricted
• Expired
• Archived
• Deleted

────────────────────────────────────────

STORY EXPIRATION

Every story item has:

• Published time
• Expiration time

Expired story content must not appear in:

• Feed
• Search
• Explore
• Public profiles

unless explicitly preserved as an authorized highlight representation.

────────────────────────────────────────

STORY VIEWER MODEL

Support:

• Story
• Viewer
• Seen timestamp

Avoid writing duplicate viewer events indefinitely.

Use appropriate unique constraints.

────────────────────────────────────────

STORY REPLIES

Support:

• Reply
• Author
• Story
• Message reference where applicable

Respect:

• Block
• Restriction
• Messaging permissions
• Story visibility

────────────────────────────────────────

STORY REACTIONS

Support reaction foundation:

• Reaction
• Type
• Author
• Story
• Created time

Ensure duplicate reaction behavior is deterministic.

────────────────────────────────────────

STORY HIGHLIGHTS

Implement:

• Highlight
• Title
• Cover
• Ordered story references
• Visibility

A highlight may preserve eligible story content after normal expiration.

────────────────────────────────────────

REELS

Implement:

• Reel
• Media reference
• Cover
• Caption
• Audio
• Hashtags
• Mentions
• Location
• Visibility
• Publication state

────────────────────────────────────────

REEL LIFECYCLE

States:

• Draft
• Processing
• Moderation
• Published
• Restricted
• Archived
• Deleted

────────────────────────────────────────

REEL DISTRIBUTION

Publish events for downstream:

• Feed
• Explore
• Search
• Recommendation
• Trending
• Analytics

The Reel service itself does not implement final ranking.

────────────────────────────────────────

CAPTIONS

Support:

• Caption text
• Language
• Accessibility metadata
• Auto-caption status
• Caption version

Prepare for generated captions.

────────────────────────────────────────

HASHTAGS

Implement canonical hashtag domain.

Support:

• Normalized value
• Display value
• Identity
• Usage
• Status

Associate content through references rather than duplicate hashtag strings everywhere.

────────────────────────────────────────

HASHTAG NORMALIZATION

Normalize:

• Case
• Unicode
• Whitespace
• Supported punctuation

Prevent visually equivalent duplicates where policy requires.

────────────────────────────────────────

MENTIONS

Implement:

• Mention
• Target user
• Content
• Position
• Visibility
• Notification eligibility

Before creating mention:

• Validate target
• Validate content permissions
• Check block/restriction rules

────────────────────────────────────────

LOCATION TAGGING

Support:

• Location reference
• Display name
• Provider/source reference where needed

Do not automatically expose precise creator/device location.

────────────────────────────────────────

AUDIO DOMAIN

Implement:

• Audio
• Source
• Creator/rights owner reference
• Duration
• Usage count
• Region
• Rights state
• Availability

────────────────────────────────────────

AUDIO STATES

Support:

• Active
• Restricted
• Region Restricted
• Removed
• Expired

────────────────────────────────────────

AUDIO USAGE

Track references from:

• Reels
• Stories where supported
• Posts where supported

Do not duplicate audio binaries across content.

────────────────────────────────────────

AUDIO RIGHTS

Support:

• Rights claim
• Region
• Effective time
• Expiration
• Restriction

Rights state must affect publication and playback.

────────────────────────────────────────

CONTENT RIGHTS

Every post/reel/story media relationship may be affected by:

• Rights
• Moderation
• Region
• Account state

Read paths must enforce current effective state.

────────────────────────────────────────

CONTENT DELETION

Support:

• User deletion
• Admin removal
• Moderation removal
• Rights removal
• Privacy deletion

Deletion must propagate to:

• Search
• Feed
• Explore
• Recommendations
• Trending
• Notifications
• Analytics
• Caches

────────────────────────────────────────

CONTENT RESTORATION

Support authorized restoration after:

• Moderation reversal
• Appeal
• Rights restoration
• Administrative correction

Re-restoration must create new state/revision as needed.

────────────────────────────────────────

CONTENT ARCHIVAL

Support archival where business rules require.

Archived content must not automatically remain publicly discoverable.

────────────────────────────────────────

CONTENT VERSIONING

Track revisions to:

• Caption
• Visibility
• Media arrangement
• Location
• Mentions
• Hashtags
• Cover
• Audio

Use immutable audit history where needed.

────────────────────────────────────────

POST UPDATE CONCURRENCY

Use optimistic concurrency for:

• Caption changes
• Media reordering where allowed
• Visibility
• Cover
• Metadata

Prevent stale clients from silently overwriting newer updates.

────────────────────────────────────────

DATABASE

Implement Prisma models and migrations for:

MEDIA

• MediaAsset
• MediaVersion
• MediaRendition
• MediaProcessingJob
• MediaManifest
• MediaCaption
• UploadSession
• UploadPart

POSTS

• Post
• PostMedia
• PostLocation
• PostHashtag
• PostMention
• PostRevision

CAROUSELS

• Carousel
• CarouselItem

DRAFTS

• ContentDraft
• DraftRevision

STORIES

• Story
• StoryItem
• StoryViewer
• StoryReplyReference
• StoryReaction
• StoryHighlight
• StoryHighlightItem

REELS

• Reel
• ReelRevision
• ReelAudioReference
• ReelHashtag
• ReelMention
• ReelLocation

AUDIO

• Audio
• AudioUsage
• AudioRights

HASHTAGS

• Hashtag

MENTIONS

• Mention

RIGHTS

• RightsReference
• RightsRestriction

────────────────────────────────────────

DATABASE CONSTRAINTS

Use:

• Unique identifiers
• Foreign keys
• Unique owner/content relationships
• Composite indexes
• Status indexes
• Timestamp indexes
• Revision/version fields

Prevent:

• Duplicate media
• Duplicate carousel ordering
• Duplicate story viewers
• Duplicate audio usage where applicable
• Duplicate content relations

────────────────────────────────────────

DATABASE INDEXING

MEDIA:

• Owner
• Status
• Type
• Created

POSTS:

• Owner
• Visibility
• State
• Published time

STORIES:

• Owner
• State
• Expiration
• Published

REELS:

• Owner
• State
• Published

HASHTAGS:

• Normalized value
• Status

AUDIO:

• Status
• Region
• Search references

────────────────────────────────────────

REDIS

Use Redis for:

• Upload-session acceleration
• Media-processing locks
• Content-read cache
• Story tray cache
• Story viewer state
• Trending counters
• Hashtag usage cache
• Audio usage counters
• Idempotency
• Rate limiting

Redis must never be authoritative for:

• Posts
• Stories
• Reels
• Media ownership
• Audio rights
• Hashtag ownership

────────────────────────────────────────

KAFKA / REDPANDA EVENTS

MEDIA:

• MediaUploadInitialized
• MediaUploadCompleted
• MediaValidationStarted
• MediaValidationCompleted
• MediaProcessingStarted
• MediaProcessingCompleted
• MediaProcessingFailed
• MediaDeleted

POSTS:

• PostCreated
• PostPublished
• PostUpdated
• PostDeleted
• PostArchived
• PostRestored

STORIES:

• StoryCreated
• StoryPublished
• StoryViewed
• StoryExpired
• StoryDeleted
• StoryHighlighted

REELS:

• ReelCreated
• ReelPublished
• ReelUpdated
• ReelDeleted

AUDIO:

• AudioCreated
• AudioRestricted
• AudioRestored
• AudioUsageRecorded

HASHTAGS:

• HashtagCreated
• HashtagReferenced

MENTIONS:

• MentionCreated

All events must be:

• Versioned
• Idempotent
• Privacy-aware
• Correlation-aware
• Region-aware

────────────────────────────────────────

BULLMQ

Create queues for:

• Upload validation
• Image processing
• Video processing
• HLS packaging
• Poster generation
• Thumbnail generation
• Caption processing
• Story expiration
• Scheduled publication
• Search indexing
• Feed notification
• Media cleanup
• Expired-object cleanup
• Rights propagation
• Moderation propagation
• Reconciliation

Every queue defines:

• Job schema
• Retry
• Backoff
• Timeout
• Concurrency
• Idempotency
• Dead-letter
• Metrics

────────────────────────────────────────

API

MEDIA

• Initialize upload
• Get upload status
• Complete upload
• Cancel upload
• Get media status
• Get media metadata
• Request secure playback
• Request image variants

POSTS

• Create draft
• Get post
• Update post
• Publish post
• Schedule post
• Archive post
• Delete post
• Restore post where authorized

CAROUSELS

• Add item
• Remove item
• Reorder item
• Update cover

STORIES

• Create story
• Publish
• Get story
• Get story tray
• Mark viewed
• Reply
• React
• Delete
• Create highlight

REELS

• Create draft
• Get reel
• Update
• Publish
• Schedule
• Delete

AUDIO

• Search
• Get audio
• Get availability
• Get usage metadata

HASHTAGS

• Get
• Search
• Related

MENTIONS

• Create where authorized
• Remove where authorized

Every endpoint must implement:

• Authentication
• Authorization
• Validation
• Rate limiting
• Idempotency where required
• OpenAPI
• Consistent error handling

────────────────────────────────────────

MEDIA API SECURITY

Never return:

• S3 credentials
• Permanent private URLs
• Internal bucket structure
• Processing internals unnecessarily

Secure playback must respect:

• Visibility
• Rights
• Moderation
• Region
• Account state

────────────────────────────────────────

STORY VIEW AUTHORIZATION

Before returning a story evaluate:

• Account state
• Block
• Private account
• Follow relationship
• Close-friends membership
• Story visibility
• Story expiration
• Moderation
• Rights

────────────────────────────────────────

POST AUTHORIZATION

Before returning a post evaluate:

• Owner
• Visibility
• Follower relationship
• Close friends
• Block
• Restriction
• Account state
• Moderation
• Rights
• Region

────────────────────────────────────────

REEL AUTHORIZATION

Same principles as posts plus:

• Recommendation eligibility
• Audio rights
• Regional playback rights

────────────────────────────────────────

STORY TRAY

Create backend contract for:

• Recent stories
• Unseen state
• Eligibility
• Close friends
• Creator ordering

Do not implement final recommendation ranking here.

────────────────────────────────────────

STORY VIEW EVENT

Marking a story viewed must be:

• Idempotent
• Efficient
• Deduplicated

Do not write infinite duplicate rows for repeated opens.

────────────────────────────────────────

MENTION NOTIFICATIONS

Creating a valid mention may emit a notification event.

Notification delivery belongs to the notification subsystem.

────────────────────────────────────────

HASHTAG USAGE

Increment usage asynchronously.

Do not make content publication depend on a global synchronous hashtag-counter update.

────────────────────────────────────────

AUDIO USAGE

Record usage through asynchronous event processing.

Do not block publication solely on the usage counter.

────────────────────────────────────────

CONTENT PUBLICATION TRANSACTION

Publication should atomically establish:

• Content state
• Publication time
• Required metadata
• Publication event/outbox record

External side effects happen after successful transaction.

────────────────────────────────────────

SCHEDULED PUBLICATION

A scheduled content job must:

• Recheck authorization
• Recheck account state
• Recheck media state
• Recheck moderation
• Recheck rights
• Recheck visibility

before publication.

────────────────────────────────────────

SECURITY

Protect against:

• Unauthorized post access
• Private-story leakage
• Private-reel leakage
• Media scraping
• S3 origin bypass
• Upload abuse
• Duplicate upload
• Malicious media
• Mention abuse
• Hashtag spam
• Audio misuse
• Cross-user draft access
• Draft enumeration
• Content-ID enumeration

────────────────────────────────────────

PRIVACY

Protect:

• Drafts
• Private posts
• Close-friends stories
• Viewer lists
• Story interactions
• Private media
• Search-related content metadata
• User-generated captions/drafts

Viewer lists should never become public API data unless explicitly authorized.

────────────────────────────────────────

OBSERVABILITY

Instrument:

• Upload initialization
• Upload completion
• Media validation
• Media processing
• HLS
• Image processing
• Publication
• Story expiration
• Story viewing
• Reel publication
• Audio usage
• Hashtag usage
• Content deletion
• Content restoration

Track:

• Upload latency
• Processing latency
• Failure rate
• Queue depth
• Processing backlog
• Publication latency
• Story expiration lag
• Media error rate
• CDN authorization failures

Never log:

• Private content
• Raw signed URLs
• User drafts
• Viewer identities unnecessarily

────────────────────────────────────────

HEALTH CHECKS

Check:

• PostgreSQL
• Redis
• Kafka
• BullMQ
• S3

Separate liveness from dependency readiness.

────────────────────────────────────────

TESTING

UNIT TESTS

Test:

• Media lifecycle
• Upload lifecycle
• Post lifecycle
• Story lifecycle
• Reel lifecycle
• Visibility
• Publication
• Expiration
• Mention rules
• Hashtag normalization
• Audio rights
• Revision conflicts

MEDIA TESTS

• Valid image
• Invalid image
• Valid video
• Invalid video
• MIME spoof
• Corrupt file
• Oversize file
• Unsupported codec
• Duplicate completion
• Expired upload

IMAGE TESTS

• Resize
• Orientation
• Compression
• Metadata

VIDEO TESTS

• Transcoding
• Renditions
• HLS
• Poster
• Thumbnail

POST TESTS

• Draft
• Publish
• Schedule
• Update
• Delete
• Restore

STORY TESTS

• Publish
• Visibility
• View
• Reply
• Reaction
• Expiration
• Highlight

REEL TESTS

• Draft
• Publish
• Delete
• Audio
• Rights

SECURITY TESTS

• Private-content IDOR
• Draft access
• Media access
• Signed URL abuse
• Story viewer leakage
• Cross-account media access

CONCURRENCY TESTS

• Duplicate upload completion
• Concurrent publication
• Stale post update
• Story view race
• Media processing race
• Scheduled publication race

PERFORMANCE TESTS

• Upload initialization
• Media status
• Story tray
• Content reads
• Publication
• Media-processing queues

────────────────────────────────────────

DOCUMENTATION

Generate:

• Media architecture
• Upload lifecycle
• Multipart uploads
• Media validation
• Image processing
• Video processing
• HLS
• Media versioning
• CDN access
• Post architecture
• Post lifecycle
• Visibility
• Publication
• Scheduling
• Carousels
• Drafts
• Stories
• Story viewers
• Story replies
• Story reactions
• Highlights
• Reels
• Captions
• Hashtags
• Mentions
• Locations
• Audio
• Rights
• Deletion
• Restoration
• API contracts
• Event contracts
• Queue contracts
• Database schema
• Redis catalog
• Security
• Privacy
• Observability
• Testing

────────────────────────────────────────

PROJECT INDEX

Update the backend Project Index with:

• Media
• Upload sessions
• Upload parts
• Media versions
• Renditions
• Processing jobs
• HLS manifests
• Captions
• Posts
• Post media
• Post revisions
• Carousels
• Carousel items
• Drafts
• Draft revisions
• Stories
• Story items
• Story viewers
• Story replies
• Story reactions
• Story highlights
• Reels
• Reel revisions
• Audio
• Audio usage
• Audio rights
• Hashtags
• Mentions
• Locations
• Rights references
• APIs
• Kafka topics
• BullMQ queues
• Redis keys
• Database migrations
• Security
• Privacy
• Observability
• Tests
• Generated files
• Modified files
• Remaining work
• Current milestone
• Dependencies

────────────────────────────────────────

IMPLEMENTATION MILESTONES

BACKEND MILESTONE 11

Media assets, upload sessions, direct S3 authorization, multipart uploads, validation, object ownership, media lifecycle, and secure access.

BACKEND MILESTONE 12

Image processing, video processing, FFmpeg workers, renditions, posters, thumbnails, HLS packaging, media versioning, and processing concurrency.

BACKEND MILESTONE 13

Posts, post media, carousels, captions, locations, visibility, publication, scheduling foundation, archival, deletion, restoration, and revisions.

BACKEND MILESTONE 14

Drafts, draft revisions, story creation, story publication, story visibility, expiration, viewers, replies, reactions, and highlights.

BACKEND MILESTONE 15

Reels, reel lifecycle, audio integration, captions, hashtags, mentions, locations, rights state, and publication propagation.

BACKEND MILESTONE 16

Content authorization, secure playback, privacy enforcement, blocks/restrictions integration, rights enforcement, moderation integration, and deletion propagation.

BACKEND MILESTONE 17

Kafka events, transactional outbox integration, BullMQ workers, scheduled publication, story expiration, media cleanup, reconciliation, and derived-state propagation.

BACKEND MILESTONE 18

API hardening, rate limiting, security testing, media-abuse protection, content-access testing, concurrency controls, and performance optimization.

BACKEND MILESTONE 19

Observability, metrics, tracing, queue monitoring, media operational dashboards, publication diagnostics, failure handling, and recovery.

BACKEND MILESTONE 20

Full integration, regression testing, security validation, privacy validation, load testing, documentation, Project Index completion, and production-readiness review.

Each milestone should contain approximately 20–40 files where practical.

Every milestone must compile before proceeding.

────────────────────────────────────────

OUTPUT FORMAT

For every generated file provide:

1. Exact file path
2. Complete file contents

Never truncate code.

Never summarize source code instead of generating it.

Never generate pseudo-code.

Never generate placeholders.

Never generate TODO implementations.

When modifying an existing file:

1. Provide the exact file path.
2. State why it must change.
3. Provide the complete updated file.

Never regenerate unchanged files.

────────────────────────────────────────

SCOPE RESTRICTION

This volume covers the core content and media backend:

• Media
• Upload
• Multipart/resumable upload
• Image processing
• Video processing
• HLS
• Media versions
• Posts
• Carousels
• Drafts
• Stories
• Story viewers
• Story replies
• Story reactions
• Highlights
• Reels
• Captions
• Hashtags
• Mentions
• Locations
• Audio
• Rights integration
• Visibility
• Publication
• Scheduling foundation
• Deletion
• Restoration
• Content authorization
• Related events
• Related queues
• Related APIs
• Related tests

Do not implement complete:

• Feed ranking
• Recommendation algorithms
• Explore ranking
• Trending algorithms
• Search ranking
• Full messaging
• Notification delivery
• Full moderation platform
• Full rights platform
• Advertising
• Commerce
• Analytics platform
• Administration UI
• Frontend
• Mobile
• Infrastructure

Use the existing identity, social graph, account, profile, security, privacy, database, Redis, Kafka, BullMQ, WebSocket, and S3 foundations.

────────────────────────────────────────

QUALITY BAR

Treat media, content ownership, content visibility, publication, and private-content access as mission-critical.

Assume:

• Hundreds of millions of users
• Millions of creators
• Billions of media objects
• Massive upload traffic
• Massive video-processing workloads
• Massive story/reel traffic
• Multiple regions
• Strict privacy
• High availability

Prioritize:

• Media integrity
• Secure storage
• Secure playback
• Correct visibility
• Idempotent publication
• Reliable processing
• Efficient CDN delivery
• Concurrency safety
• Rights enforcement
• Privacy
• Security
• Scalability
• Observability
• Maintainability
• Production readiness
