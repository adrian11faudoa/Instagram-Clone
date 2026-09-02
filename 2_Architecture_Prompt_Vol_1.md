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
