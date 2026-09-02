You are operating in Senior Engineering Team Mode.

Continue and complete the architectural blueprint for an enterprise-scale global visual-social platform comparable in architectural scope to Instagram.

The platform is an original implementation.

Do not copy proprietary source code, internal architecture, branding, confidential implementation details, proprietary algorithms, proprietary datasets, or private implementation details from Instagram, Meta, or any other company.

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
• Detailed domain specifications
• Data models
• API contracts
• Event contracts
• Queue contracts
• State machines
• Read/write models
• Caching strategy
• Media architecture
• Feed architecture
• Recommendation architecture
• Messaging architecture
• Notification architecture
• Moderation architecture
• Rights architecture
• Advertising architecture
• Commerce architecture
• Analytics architecture
• Privacy architecture
• Security architecture
• Multi-region architecture
• Disaster recovery
• Scalability strategy
• Operational strategy
• Testing architecture
• ADRs
• Implementation roadmaps

────────────────────────────────────────

ARCHITECTURE SCOPE

Complete the detailed architecture for:

• Identity
• Accounts
• Profiles
• Creator profiles
• Business profiles
• Verification
• Devices
• Social graph
• Private accounts
• Follow requests
• Blocks
• Restrictions
• Close Friends
• Posts
• Carousels
• Stories
• Story viewers
• Story replies/reactions
• Story highlights
• Reels
• Drafts
• Media
• Image processing
• Video processing
• Audio
• Music
• Hashtags
• Mentions
• Locations
• Likes
• Comments
• Replies
• Saves
• Collections
• Shares
• Reposts
• Feed
• Explore
• Recommendations
• Trending
• Search
• Messaging
• Message requests
• Notifications
• Moderation
• Safety
• Reports
• Rights
• Appeals
• Creator analytics
• Business analytics
• Advertising
• Commerce
• Live streaming
• Privacy
• Administration
• Feature flags
• Dynamic configuration
• Audit
• Analytics
• Multi-region
• Disaster recovery

────────────────────────────────────────

IDENTITY ARCHITECTURE

Define:

• User identity
• Account
• Authentication
• Session
• Device
• Login method
• Verification
• Account recovery
• Security events

Separate:

• Authentication identity
• Public profile
• Internal account state

Support:

• Email
• Username
• Password
• OAuth foundation
• MFA foundation
• Passkey foundation
• Device registration

────────────────────────────────────────

ACCOUNT LIFECYCLE

States:

• Pending
• Active
• Restricted
• Suspended
• Deactivated
• Deletion Requested
• Deleted

Define valid transitions.

Account state must affect:

• Login
• Content
• Messaging
• Feed
• Search
• Notifications
• Advertising
• Analytics

────────────────────────────────────────

PROFILE ARCHITECTURE

Support:

• Username
• Display name
• Bio
• Avatar
• Links
• Pronouns where product policy allows
• Verification
• Profile visibility
• Creator category
• Business category

Separate public profile information from private account metadata.

────────────────────────────────────────

USERNAME SYSTEM

Define:

• Uniqueness
• Case normalization
• Unicode normalization
• Reserved names
• Rename rules
• Previous-name history
• Impersonation protection

Avoid exposing internal account IDs unnecessarily.

────────────────────────────────────────

PRIVATE ACCOUNT ARCHITECTURE

Define:

• Public account
• Private account

Private account requires:

• Follow request
• Approval
• Explicit visibility controls

Private content must be excluded from:

• Unauthorized feed
• Search
• Explore
• Public profile surfaces
• Public share links

────────────────────────────────────────

VERIFICATION

Support:

• Verification state
• Application
• Review
• Approval
• Rejection
• Revocation

Do not expose internal verification evidence.

────────────────────────────────────────

DEVICE ARCHITECTURE

Track:

• Device ID
• Platform
• App version
• Push-token reference
• Last active
• Security state

Do not use device identity as the only security factor.

────────────────────────────────────────

SOCIAL GRAPH

Define graph edges:

• Follow
• Pending follow
• Block
• Restriction
• Close friend

For every relationship define:

• Source
• Target
• State
• Created
• Updated
• Version

────────────────────────────────────────

FOLLOW REQUEST STATE MACHINE

States:

• Requested
• Accepted
• Rejected
• Canceled
• Expired

Define race conditions:

• Request + block
• Accept + block
• Reject + cancel
• Private → public while pending

────────────────────────────────────────

BLOCK ARCHITECTURE

A block should suppress or affect:

• Profile discovery
• Follow
• Messaging
• Comments
• Mentions
• Notifications
• Feed
• Explore
• Search
• Story viewing
• Reels distribution

Define event propagation.

────────────────────────────────────────

RESTRICTION ARCHITECTURE

Restriction is distinct from block.

Support configurable limitations for:

• Comments
• Messaging
• Mentions
• Interaction visibility

────────────────────────────────────────

CLOSE FRIENDS

Define:

• List owner
• Member
• Added time
• Removed time

Close-friends membership is private.

Integrate with:

• Stories
• Notifications
• Visibility

────────────────────────────────────────

CONTENT MODEL

Use separate domain concepts for:

• Post
• Carousel
• Reel
• Story
• Highlight

Do not use a single generic content entity as a substitute for domain ownership.

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

Define visibility separately from lifecycle.

────────────────────────────────────────

POST VISIBILITY

Support:

• Public
• Followers
• Close Friends
• Restricted audience where approved

Visibility must be enforced at read time.

────────────────────────────────────────

CAROUSELS

Support:

• Ordered media items
• Cover
• Caption
• Mentions
• Hashtags
• Location

Define:

• Maximum items
• Media ordering
• Partial processing
• Publication only after valid media state

────────────────────────────────────────

STORIES

Define:

• Story
• Story item
• Story sequence
• Viewer
• Reply
• Reaction
• Mention
• Highlight reference

Story expiration must be explicit.

────────────────────────────────────────

STORY VIEW MODEL

Track viewer state:

• Unseen
• Seen

Avoid storing excessive repeated viewer events unnecessarily.

Use derived read models for story trays.

────────────────────────────────────────

STORY REPLIES / REACTIONS

Support:

• Reply
• Reaction
• Emoji reaction foundation
• Mention

Respect:

• Privacy
• Messaging permissions
• Block
• Restriction

────────────────────────────────────────

STORY HIGHLIGHTS

Support:

• Highlight
• Ordered stories
• Cover
• Title
• Visibility

Highlights survive the normal story expiration lifecycle where product policy allows.

────────────────────────────────────────

REELS

Define short-form video content separately from regular video posts.

Support:

• Cover
• Caption
• Audio
• Hashtags
• Mentions
• Location
• Engagement
• Distribution
• Explore
• Search

────────────────────────────────────────

DRAFTS

Support drafts across:

• Posts
• Carousels
• Reels
• Stories

Drafts should be:

• Private
• Recoverable
• Versioned
• Expirable where appropriate

────────────────────────────────────────

MEDIA ARCHITECTURE

Media pipeline:

Client
→ Authorization
→ Direct Object Upload
→ Validation
→ Malware/Safety Validation
→ Metadata Extraction
→ Processing
→ Optimization
→ Moderation
→ Publication
→ CDN

────────────────────────────────────────

IMAGE PIPELINE

Generate variants:

• Original
• Large
• Medium
• Small
• Thumbnail
• Feed
• Story
• Avatar
• Cover

Support:

• Orientation
• Compression
• Modern formats
• Metadata handling
• Responsive delivery

────────────────────────────────────────

VIDEO PIPELINE

Generate:

• Original
• Processing intermediate
• Renditions
• Poster
• Preview
• HLS manifest
• HLS segments

Use versioned processing profiles.

────────────────────────────────────────

MEDIA VERSIONING

Every media version should identify:

• Media ID
• Version
• Processing profile
• Codec
• Resolution
• Bitrate
• Region
• Creation time

Old versions remain available only according to retention policy.

────────────────────────────────────────

CDN ARCHITECTURE

Use CDN for:

• Images
• Thumbnails
• Video manifests
• Video segments
• Static assets

Never expose object storage directly where origin protection is required.

────────────────────────────────────────

MEDIA ACCESS

Use:

• Public CDN objects where genuinely public
• Short-lived signed access where restricted
• Origin access control
• Authorization checks

Never expose permanent private-media credentials.

────────────────────────────────────────

AUDIO ARCHITECTURE

Define:

• Audio
• Audio source
• Audio creator
• Duration
• Usage
• Rights
• Region availability

Support:

• Search
• Trending
• Audio pages
• Reels using audio

────────────────────────────────────────

HASHTAG ARCHITECTURE

Define:

• Canonical hashtag
• Normalized value
• Display value
• Usage
• Trend
• Related hashtags

Prevent excessive duplicate representations caused by normalization differences.

────────────────────────────────────────

MENTION ARCHITECTURE

Support:

• User mention
• Creator mention
• Business mention

Validate whether target allows:

• Mention
• Notification
• Visibility

────────────────────────────────────────

LOCATION TAGGING

Support:

• Location reference
• Display name
• Optional geographic coordinates

Do not automatically expose a creator's precise location from metadata unless intended.

────────────────────────────────────────

ENGAGEMENT ARCHITECTURE

Define:

• Like
• Comment
• Reply
• Save
• Share
• Repost
• Collection

Separate:

• Authoritative relationship
• Event stream
• Aggregate metrics

────────────────────────────────────────

LIKE MODEL

A like is generally unique per:

• User
• Content

Use idempotent semantics.

Prevent duplicate likes.

────────────────────────────────────────

COMMENT MODEL

Support:

• Comment
• Reply
• Author
• Parent
• Content
• Moderation state
• Created time
• Updated time

Use cursor pagination.

────────────────────────────────────────

COMMENT TREE

Avoid loading unbounded nested trees.

Use:

• Parent reference
• Depth
• Child pagination
• Top-level pagination

────────────────────────────────────────

SAVE / COLLECTIONS

Support:

• Save
• Collection
• Collection item

Collections:

• Private
• Shared where explicitly supported

────────────────────────────────────────

SHARING

Support:

• External share
• Internal share
• Copy link
• Deep links

Share access must re-check authorization at destination.

────────────────────────────────────────

REPOSTS

Define:

• Reposter
• Original content
• Repost time
• Visibility
• Removal

Do not duplicate original media unnecessarily.

────────────────────────────────────────

FEED ARCHITECTURE

Support:

• Home feed
• Following feed
• Reels feed
• Story tray
• Explore

Core pipeline:

User Context
→ Candidate Generation
→ Eligibility
→ Ranking
→ Re-ranking
→ Diversity
→ Response
→ Event Logging

────────────────────────────────────────

CANDIDATE GENERATION

Sources:

• Followed creators
• Similar creators
• Similar content
• Saved content
• Hashtag affinity
• Audio affinity
• Trending
• Explore
• Fresh content

Define candidate budgets.

────────────────────────────────────────

ELIGIBILITY

Filter:

• Private content
• Blocked users
• Deleted content
• Moderated content
• Rights restrictions
• Region restrictions
• Age restrictions
• Recommendation restrictions

Eligibility is non-negotiable.

────────────────────────────────────────

RANKING

Define pluggable stages:

• Retrieval
• Filtering
• Scoring
• Re-ranking
• Diversity

Potential signals:

• Watch
• Completion
• Rewatch
• Like
• Comment
• Save
• Share
• Follow
• Profile visit
• Negative feedback
• Freshness
• Creator affinity

────────────────────────────────────────

RANKING VERSIONING

Every recommendation response should identify:

• Ranking version
• Experiment version where appropriate
• Candidate-generation version

Do not expose internal model information publicly.

────────────────────────────────────────

DIVERSITY

Prevent feed concentration around:

• One creator
• One topic
• One hashtag
• One audio
• One content format

Define configurable diversity constraints.

────────────────────────────────────────

NEGATIVE FEEDBACK

Support:

• Not interested
• Hide creator
• Hide content
• Report

Negative feedback should become a recommendation signal asynchronously.

────────────────────────────────────────

EXPLORE

Use different candidate strategy from home feed.

Support:

• Discovery
• Trending
• Topic exploration
• Creators
• Hashtags
• Audio

────────────────────────────────────────

TRENDING

Define ranking signals:

• Velocity
• Engagement
• Freshness
• Diversity
• Abuse-adjusted activity

Avoid making raw engagement count sufficient to determine trend status.

────────────────────────────────────────

SEARCH ARCHITECTURE

Search:

• Users
• Creators
• Posts
• Reels
• Hashtags
• Audio
• Places

Define:

• Index
• Ranking
• Personalization
• Privacy filtering
• Freshness

────────────────────────────────────────

MESSAGING ARCHITECTURE

Support:

• One-to-one conversations
• Group conversations
• Message requests
• Messages
• Attachments
• Delivery
• Read
• Reactions foundation
• Replies foundation

────────────────────────────────────────

MESSAGE ORDERING

Use:

• Server sequence
• Created timestamp
• Conversation revision

Do not depend on client clocks.

────────────────────────────────────────

MESSAGE IDEMPOTENCY

Every send supports:

• Client mutation ID
• Idempotency key

Retries must not create duplicate messages.

────────────────────────────────────────

MESSAGE DELIVERY

Persist accepted message before delivery orchestration.

Channels:

• WebSocket
• Push
• Offline sync

────────────────────────────────────────

MESSAGE REQUESTS

For non-permitted conversations support:

• Request
• Accept
• Reject
• Delete
• Block
• Report

────────────────────────────────────────

NOTIFICATIONS

Sources:

• Follow
• Like
• Comment
• Mention
• Share
• Repost
• Message
• Story interaction
• Creator update
• Moderation
• Rights
• Security

Channels:

• In-app
• Push
• Email where approved

────────────────────────────────────────

NOTIFICATION FANOUT

Design asynchronous delivery.

Avoid synchronous fanout to thousands/millions of followers.

Use:

• Event stream
• Queues
• Batching
• Aggregation
• Provider throttling

────────────────────────────────────────

MODERATION ARCHITECTURE

Content types:

• Posts
• Reels
• Stories
• Comments
• Profiles
• Audio
• Hashtags
• Messages
• Products
• Business content

Workflow:

Content
→ Detection
→ Classification
→ Policy
→ Decision
→ Enforcement
→ Appeal

────────────────────────────────────────

MODERATION POLICY

Every decision identifies:

• Policy version
• Rule
• Severity
• Confidence
• Decision
• Actor

Internal reasoning should remain restricted.

────────────────────────────────────────

REPORTING

Support:

• User
• Post
• Reel
• Story
• Comment
• Message
• Audio
• Hashtag
• Product
• Business

Use:

• Deduplication
• Rate limiting
• Aggregation
• Risk signals

────────────────────────────────────────

SAFETY

Support high-severity workflows for:

• Credible threats
• Child safety
• Severe abuse
• Coordinated harmful activity

Define:

• Priority
• Escalation
• Access restrictions
• Evidence retention
• Audit

────────────────────────────────────────

COPYRIGHT / RIGHTS

Support:

• Claim
• Takedown
• Restriction
• Regional limitation
• Audio restriction
• Appeal
• Restoration
• Expiration

Rights enforcement must propagate to discovery and playback.

────────────────────────────────────────

ADVERTISING ARCHITECTURE

Define:

• Advertiser
• Organization
• Campaign
• Ad set
• Creative
• Placement
• Targeting
• Budget
• Frequency cap
• Billing reference
• Analytics

Separate advertising from organic ranking.

────────────────────────────────────────

AD ELIGIBILITY

Before serving:

• Campaign active
• Creative approved
• Budget available
• Placement valid
• Schedule valid
• Frequency valid
• Privacy rules valid
• Safety rules valid

────────────────────────────────────────

COMMERCE

Define:

• Business
• Product catalog
• Product
• Product collection
• Product tag
• Product availability
• Commerce analytics

Product data is independently owned.

────────────────────────────────────────

PRODUCT TAGGING

A post/reel may reference:

• Product ID
• Product position
• Product metadata snapshot where justified

Do not duplicate the entire product as permanent content state.

────────────────────────────────────────

LIVE STREAMING

Define:

• Live session
• Creator
• Ingest
• Playback
• Viewer count
• Chat
• Moderation
• Recording

Streaming should use dedicated infrastructure.

────────────────────────────────────────

ANALYTICS ARCHITECTURE

Capture events:

• Feed impression
• Video start
• Watch duration
• Completion
• Rewatch
• Like
• Comment
• Save
• Share
• Repost
• Follow
• Search
• Explore
• Story view
• Reel view
• Message
• Notification
• Ad impression
• Ad click

────────────────────────────────────────

ANALYTICS PIPELINE

Application
→ Event
→ Kafka
→ Validation
→ Enrichment
→ Aggregation
→ Analytical storage
→ Reporting

Analytics must not block user-facing requests.

────────────────────────────────────────

ANALYTICS PRIVACY

Separate:

• Raw event
• Aggregated event
• User-level event
• Creator metrics
• Business metrics
• Platform metrics

Apply retention and access controls.

────────────────────────────────────────

CREATOR ANALYTICS

Support:

• Reach
• Impressions
• Views
• Watch time
• Completion
• Average watch
• Likes
• Comments
• Shares
• Saves
• Reposts
• Follower growth
• Traffic source
• Audience aggregates

────────────────────────────────────────

BUSINESS ANALYTICS

Support:

• Profile visits
• Content reach
• Product views
• Engagement
• Search discovery
• Ad analytics

Use aggregate views where appropriate.

────────────────────────────────────────

PRIVACY ARCHITECTURE

Classify:

• Identity
• Social graph
• Content
• Messages
• Search history
• Behavioral data
• Location
• Analytics
• Moderation
• Rights
• Advertising
• Commerce

Define:

• Access
• Retention
• Export
• Deletion
• Audit

────────────────────────────────────────

DATA DELETION

Deletion must propagate through:

• Identity
• Profiles
• Social graph
• Posts
• Media
• Stories
• Reels
• Comments
• Likes
• Saves
• Collections
• Messages
• Search
• Feed features
• Recommendations
• Analytics
• Advertising
• Commerce
• Moderation

Use asynchronous deletion workflows where needed.

────────────────────────────────────────

SEARCH / RECOMMENDATION DELETION

Deleted or restricted content must be removed from:

• Search
• Explore
• Feed candidate stores
• Recommendation features
• Trending
• Caches

within defined policy time limits.

────────────────────────────────────────

ADMINISTRATION

Define administrative roles:

• Support
• Moderator
• Safety
• Rights
• Fraud
• Advertising
• Analytics
• Operations
• Privacy
• Security
• System administrator

Every permission should be explicit.

────────────────────────────────────────

ADMIN ACTIONS

Sensitive actions require:

• Permission
• Reason
• Confirmation
• Audit

Examples:

• Suspend account
• Restore account
• Remove content
• Restore content
• Modify rights
• Modify configuration
• Change feature flag
• Access sensitive data
• Process privacy request

────────────────────────────────────────

FEATURE FLAGS

Support:

• Boolean
• Percentage
• Region
• Platform
• App version
• User cohort
• Creator cohort
• Business cohort

Include:

• Versioning
• Rollout
• Kill switch
• Expiration
• Audit

────────────────────────────────────────

DYNAMIC CONFIGURATION

Support:

• Feed limits
• Recommendation thresholds
• Upload limits
• Media-processing profiles
• Story settings
• Notification limits
• Moderation thresholds
• Search limits
• Ad frequency

Configuration must be:

• Typed
• Versioned
• Validated
• Audited
• Rollback-capable

────────────────────────────────────────

MULTI-REGION ARCHITECTURE

Define:

• Regional data ownership
• Regional APIs
• Regional media processing
• Regional search
• Regional recommendation
• Regional moderation
• Regional messaging

Use:

• Global CDN
• Global DNS
• Regional event processing

Avoid unnecessary synchronous cross-region writes.

────────────────────────────────────────

CONSISTENCY

STRONG:

• Account state
• Private profile visibility
• Block
• Message ownership
• Business ownership
• Privacy controls

EVENTUAL:

• Feed
• Explore
• Recommendations
• Search
• Trending
• Analytics
• Engagement counters

Define acceptable convergence windows.

────────────────────────────────────────

DISASTER RECOVERY

Support:

• Database recovery
• Object storage recovery
• Search rebuild
• Kafka recovery
• Redis recovery
• EKS recovery
• Media processing recovery
• Feed/recommendation rebuild

Every derived system must be rebuildable.

────────────────────────────────────────

OBSERVABILITY

Define:

• Metrics
• Logs
• Traces
• Alerts
• SLOs

Monitor:

• Feed latency
• Search latency
• Media-processing latency
• Upload failures
• Video startup
• Messaging latency
• Notification latency
• Moderation backlog
• Analytics lag
• Kafka lag
• Queue depth
• CDN errors

Never put private user content in logs.

────────────────────────────────────────

SECURITY THREAT MODEL

Analyze:

• Account takeover
• Session hijacking
• Credential abuse
• IDOR
• Private-content leakage
• Media scraping
• CDN bypass
• Message leakage
• Fake engagement
• Botting
• Report abuse
• Recommendation manipulation
• Search scraping
• Ad fraud
• Business impersonation
• Copyright abuse
• Admin privilege escalation
• Privacy leakage

For each provide:

• Prevention
• Detection
• Response
• Recovery

────────────────────────────────────────

ARCHITECTURAL DECISION RECORDS

Create ADRs for:

• Identity
• Social graph
• Private accounts
• Media architecture
• S3/CDN
• Video/HLS
• Stories
• Reels
• Feed
• Recommendation
• Explore
• Trending
• Search
• Messaging
• Notifications
• Moderation
• Rights
• Advertising
• Commerce
• Analytics
• Privacy
• Multi-region
• Database
• Redis
• Kafka
• Disaster recovery

Each ADR:

• Context
• Decision
• Alternatives
• Consequences

────────────────────────────────────────

ARCHITECTURE VOLUME 2 OUTPUT

Produce:

1. Identity Architecture
2. Account Lifecycle
3. Profile Architecture
4. Username System
5. Private Accounts
6. Verification
7. Device Architecture
8. Social Graph
9. Follow Request State Machine
10. Blocking
11. Restriction
12. Close Friends
13. Content Model
14. Post Lifecycle
15. Post Visibility
16. Carousels
17. Stories
18. Story Viewer Model
19. Story Replies/Reactions
20. Story Highlights
21. Reels
22. Drafts
23. Media Architecture
24. Image Pipeline
25. Video Pipeline
26. Media Versioning
27. CDN
28. Media Access
29. Audio
30. Hashtags
31. Mentions
32. Location Tagging
33. Engagement
34. Likes
35. Comments
36. Comment Trees
37. Saves/Collections
38. Sharing
39. Reposts
40. Feed
41. Candidate Generation
42. Eligibility
43. Ranking
44. Ranking Versioning
45. Diversity
46. Negative Feedback
47. Explore
48. Trending
49. Search
50. Messaging
51. Message Ordering
52. Message Idempotency
53. Message Delivery
54. Message Requests
55. Notifications
56. Notification Fanout
57. Moderation
58. Moderation Policy
59. Reporting
60. Safety
61. Copyright/Rights
62. Advertising
63. Ad Eligibility
64. Commerce
65. Product Tagging
66. Live Streaming
67. Analytics
68. Analytics Pipeline
69. Analytics Privacy
70. Creator Analytics
71. Business Analytics
72. Privacy Architecture
73. Data Deletion
74. Search/Recommendation Deletion
75. Administration
76. Admin Actions
77. Feature Flags
78. Dynamic Configuration
79. Multi-Region
80. Consistency Model
81. Disaster Recovery
82. Observability
83. Security Threat Model
84. ADRs
85. Final Architecture Integration Matrix

────────────────────────────────────────

FINAL INTEGRATION MATRIX

Provide a complete matrix showing how the domains interact.

For each interaction specify:

• Source domain
• Target domain
• Synchronous API
• Asynchronous event
• Data exchanged
• Ownership
• Consistency requirement
• Failure behavior
• Retry
• Idempotency
• Security
• Privacy

At minimum cover:

• Identity → Social Graph
• Identity → Content
• Profiles → Discovery
• Social Graph → Feed
• Content → Feed
• Content → Search
• Media → Content
• Media → CDN
• Audio → Reels
• Hashtags → Search
• Engagement → Recommendations
• Messaging → Notifications
• Moderation → Content
• Rights → Content
• Rights → Audio
• Advertising → Feed
• Commerce → Content
• Analytics → Creator dashboard
• Privacy → all domains
• Administration → all controlled domains

────────────────────────────────────────

FINAL QUALITY BAR

The architecture must support:

• Hundreds of millions of users
• Millions of creators
• Billions of content objects
• Massive image/video traffic
• Massive feed traffic
• Massive recommendation workloads
• Massive search traffic
• Massive messaging traffic
• Large moderation workloads
• Large advertising workloads
• Large analytics workloads
• Multiple regions
• High availability
• Disaster recovery
• Strict privacy
• Strict security

The resulting architecture must be sufficiently complete that independent backend, web, mobile, media, feed, recommendation, search, messaging, moderation, advertising, commerce, analytics, infrastructure, security, privacy, DevOps, and QA teams can implement the platform without making major architectural decisions themselves.

Do not generate source code in this phase.
