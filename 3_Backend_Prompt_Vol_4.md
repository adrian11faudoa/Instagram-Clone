You are operating in Senior Engineering Team Mode.

Build the production-ready backend for messaging, notifications, moderation, safety, reporting, copyright/rights, creator analytics, business analytics, advertising foundations, commerce foundations, administration, privacy, audit, feature flags, dynamic configuration, and final platform hardening for an enterprise-scale global visual-social platform comparable in architectural scope to Instagram.

The platform is an original implementation.

Do not copy proprietary source code, internal architecture, branding, confidential implementation details, proprietary algorithms, proprietary datasets, private implementation details, or internal systems from Instagram, Meta, or any other company.

This prompt is completely independent and may be executed in a separate conversation.

Use the approved architecture and previously implemented backend foundations as the single source of truth.

Do not redesign the approved architecture.

Do not generate frontend code.

Do not generate mobile code.

Do not generate infrastructure implementation code.

Do not generate Terraform.

Do not generate Kubernetes manifests.

Do not generate CI/CD workflows.

────────────────────────────────────────

MISSION

Implement production-ready backend domains for:

• Direct messaging
• Group messaging
• Message requests
• Conversation permissions
• Messages
• Message attachments
• Message delivery
• Read receipts
• Message reactions
• Message replies
• Typing indicators
• Presence foundation
• Real-time messaging
• Notifications
• Notification preferences
• Push notifications
• FCM
• APNS
• In-app notifications
• Email notification foundation
• User reports
• Content reports
• Moderation cases
• Moderation actions
• Appeals
• Safety workflows
• Abuse prevention
• Copyright claims
• Content rights
• Audio rights
• Regional restrictions
• Rights appeals
• Rights restoration
• Creator analytics
• Business analytics
• Advertising foundation
• Advertiser accounts
• Campaigns
• Ad sets
• Creatives
• Placements
• Frequency caps
• Ad events
• Commerce foundation
• Product catalogs
• Products
• Product collections
• Product tags
• Privacy requests
• Data export
• Data deletion
• Retention
• Administration
• Audit
• Feature flags
• Dynamic configuration
• Reconciliation
• Operational hardening
• Final backend production integration

The implementation must integrate with:

• Identity
• Accounts
• Profiles
• Creators
• Businesses
• Devices
• Sessions
• Social graph
• Follows
• Blocks
• Restrictions
• Close Friends
• Posts
• Reels
• Stories
• Media
• Audio
• Hashtags
• Locations
• Feed
• Explore
• Recommendations
• Search
• PostgreSQL
• Prisma
• Redis
• Kafka/Redpanda
• BullMQ
• OpenSearch
• WebSockets
• S3
• CloudFront
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

Search:

• Elasticsearch/OpenSearch

Object storage:

• AWS S3

Real-time:

• WebSockets
• Socket.IO

Notifications:

• FCM
• APNS
• Email provider abstraction

Observability:

• OpenTelemetry
• Prometheus
• Grafana
• Loki
• Tempo

Testing:

• Jest
• Supertest
• Integration testing

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

Use DTOs for public contracts.

Use centralized validation.

Use centralized error handling.

Use structured logging.

Use idempotency for:

• Message sends
• Notification creation
• Report creation
• Moderation actions
• Rights actions
• Ad events
• Commerce mutations
• Privacy requests
• Background jobs

Use optimistic concurrency where appropriate.

Never trust client-controlled:

• Moderation state
• Rights state
• Ad eligibility
• Product ownership
• Business permissions
• Privacy completion
• Message delivery state

────────────────────────────────────────

DOMAIN OWNERSHIP

Maintain separate ownership for:

• Messaging
• Notifications
• Moderation
• Safety
• Reports
• Rights
• Analytics
• Advertising
• Commerce
• Administration
• Privacy
• Audit
• Configuration

Do not make:

• Analytics authoritative for transactions
• Notifications authoritative for messages
• Moderation authoritative for original content
• Search authoritative for content
• Redis authoritative for durable state

────────────────────────────────────────

MESSAGING ARCHITECTURE

Implement one-to-one messaging and group-messaging foundations.

Support:

• Conversation
• Participant
• Message
• Attachment
• Delivery
• Read state
• Reaction
• Reply
• Message request
• Conversation settings
• Block interaction

────────────────────────────────────────

CONVERSATION TYPES

Support:

• Direct
• Group
• Message Request

Define:

• Conversation ID
• Type
• Creator
• Status
• Created time
• Updated time
• Version

────────────────────────────────────────

CONVERSATION MEMBERSHIP

Represent:

• User
• Role where group permissions require it
• Joined time
• Left time
• Status

Group roles may include:

• Owner
• Admin
• Member

Use explicit authorization.

────────────────────────────────────────

MESSAGE MODEL

Each message should contain:

• Message ID
• Conversation ID
• Sender
• Client mutation ID
• Server sequence
• Content
• Attachment references
• Reply reference
• Created time
• Edited time
• Deleted time
• Version
• Status

Do not rely on client timestamps for ordering.

────────────────────────────────────────

MESSAGE ORDERING

Use server-side ordering.

Each conversation has a monotonic sequence/reference sufficient to determine message order.

Handle:

• Concurrent sends
• Retries
• Delayed packets
• Reconnect
• Clock skew

────────────────────────────────────────

MESSAGE IDEMPOTENCY

Every send accepts:

• Client mutation ID
• Idempotency key

A retry must return the already-created message rather than create another message.

────────────────────────────────────────

MESSAGE DELIVERY

Delivery pipeline:

Persist
→ Event
→ Real-time delivery
→ Push fallback
→ Delivery/read update

Do not make message persistence depend on push-provider success.

────────────────────────────────────────

MESSAGE STATUS

Support:

• Accepted
• Delivered
• Read
• Edited
• Deleted

Do not allow clients to forge server-side delivery state.

────────────────────────────────────────

READ RECEIPTS

Support:

• Last-read sequence
• Read timestamp

Prefer a conversation-level read cursor over one database row for every message where feasible.

────────────────────────────────────────

MESSAGE REACTIONS

Support:

• Message
• User
• Reaction type
• Created
• Updated

Define uniqueness.

────────────────────────────────────────

MESSAGE REPLIES

Support reference to an original message.

Do not duplicate the full original message in every reply.

────────────────────────────────────────

MESSAGE ATTACHMENTS

Support:

• Image
• Video
• File foundation

Use S3-backed objects.

Attachment access must inherit conversation authorization.

────────────────────────────────────────

MESSAGE ATTACHMENT SECURITY

Validate:

• File type
• Size
• Ownership
• Object key
• Malware/security state

Never expose permanent private object URLs.

────────────────────────────────────────

MESSAGE REQUESTS

Support:

• Request
• Accept
• Reject
• Delete
• Restrict
• Block

Message-request eligibility may depend on:

• Account state
• Privacy settings
• Follow state
• Existing conversation
• Blocks

────────────────────────────────────────

BLOCK + MESSAGING

A block must affect:

• New messages
• Existing conversations
• Message requests
• Notifications
• Presence
• Typing indicators

Define exact behavior.

────────────────────────────────────────

MESSAGE PRIVACY

Private message data must never appear in:

• Public search
• Public analytics
• Recommendation feeds
• Explore
• Trending

────────────────────────────────────────

REAL-TIME MESSAGING

Use WebSockets/Socket.IO.

Support:

• Authentication
• Authorization
• Connection
• Reconnect
• Heartbeat
• Conversation subscription
• New message
• Delivery
• Read
• Reaction
• Typing

────────────────────────────────────────

REAL-TIME IDEMPOTENCY

Clients may reconnect and replay events.

Use:

• Server sequence
• Event ID
• Conversation revision

to avoid duplicate delivery.

────────────────────────────────────────

PRESENCE FOUNDATION

Prepare:

• Online
• Offline
• Last active

Presence may be ephemeral.

Do not store unnecessary precise activity history.

────────────────────────────────────────

TYPING INDICATORS

Use ephemeral state.

Do not persist every typing event in PostgreSQL.

Apply:

• TTL
• Rate limit
• Debouncing

────────────────────────────────────────

NOTIFICATION ARCHITECTURE

Implement:

• Notification
• Notification preference
• Delivery
• Device token
• Notification grouping
• Read state

────────────────────────────────────────

NOTIFICATION SOURCES

Support:

• Follow
• Follow request
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
• Business update
• Security
• Privacy
• Ad/account events where appropriate

────────────────────────────────────────

NOTIFICATION GROUPING

Support aggregation such as:

• Multiple likes
• Multiple follows
• Multiple comments

Do not generate unbounded notification spam.

────────────────────────────────────────

NOTIFICATION IDEMPOTENCY

Use:

• Source event ID
• Notification type
• Recipient
• Grouping key

to avoid duplicates.

────────────────────────────────────────

NOTIFICATION PREFERENCES

Support:

• Social
• Messaging
• Creator updates
• Recommendations
• Marketing
• Business
• Security
• Privacy

Security-critical notifications cannot always be disabled.

────────────────────────────────────────

PUSH DEVICES

Track:

• Device ID
• User
• Platform
• Push token reference
• App version
• Last active

Support token rotation.

────────────────────────────────────────

FCM / APNS

Implement provider abstractions.

Handle:

• Success
• Invalid token
• Expired token
• Provider failure
• Provider throttling
• Retry
• Permanent failure

────────────────────────────────────────

EMAIL NOTIFICATIONS

Prepare provider-neutral interface.

Support:

• Verification
• Security
• Privacy
• Account notifications

Do not put provider-specific APIs in domain services.

────────────────────────────────────────

MODERATION ARCHITECTURE

Moderate:

• Posts
• Reels
• Stories
• Comments
• Profiles
• Audio
• Hashtags
• Messages where policy/legal basis permits
• Business content
• Product content

────────────────────────────────────────

MODERATION CASE

Model:

• Case ID
• Target
• Content type
• Policy
• Severity
• Confidence
• Status
• Assignee
• Created
• Updated

States:

• Open
• In Review
• Actioned
• Appealed
• Resolved
• Reopened

────────────────────────────────────────

MODERATION ACTIONS

Support:

• Allow
• Restrict
• Hide
• Remove
• Suspend
• Escalate

Every action must be:

• Authorized
• Audited
• Version-aware
• Idempotent

────────────────────────────────────────

MODERATION POLICY VERSIONING

Every automated decision references:

• Policy version
• Model/version where applicable
• Rule
• Confidence
• Decision

Do not expose internal moderation reasoning to ordinary users.

────────────────────────────────────────

REPORTING

Support reports for:

• User
• Profile
• Post
• Reel
• Story
• Comment
• Message
• Audio
• Hashtag
• Product
• Business

────────────────────────────────────────

REPORT DEDUPLICATION

Prevent report flooding using:

• Reporter
• Target
• Reason
• Time-window rules
• Existing active case

Do not equate report count with guilt.

────────────────────────────────────────

SAFETY WORKFLOWS

Support priority handling for:

• Credible threats
• Severe harassment
• Child-safety concerns
• Serious abuse
• Coordinated harmful activity

Define:

• Priority
• Access controls
• Escalation
• Evidence handling
• Audit

────────────────────────────────────────

APPEALS

Support:

• Appeal creation
• Appeal reason
• Review
• Decision
• Restoration
• Final state

Appeal decisions must be auditable.

────────────────────────────────────────

COPYRIGHT / RIGHTS

Implement:

• Rights claim
• Content restriction
• Audio restriction
• Region restriction
• Takedown
• Appeal
• Restoration
• Expiration

────────────────────────────────────────

RIGHTS STATES

Support:

• Clear
• Claimed
• Restricted
• Removed
• Region Restricted
• Expired
• Restored

────────────────────────────────────────

RIGHTS PROPAGATION

Rights changes may affect:

• Post
• Reel
• Story
• Audio
• Feed
• Explore
• Search
• Recommendations
• Sharing
• Playback

Propagate via events.

────────────────────────────────────────

CREATOR ANALYTICS

Implement aggregate analytics for:

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
• Traffic sources
• Audience regions

────────────────────────────────────────

CREATOR ANALYTICS PRIVACY

Do not expose:

• Individual viewer identity
• Private viewer behavior
• Sensitive audience attributes

Use aggregation thresholds where required.

────────────────────────────────────────

BUSINESS ANALYTICS

Support:

• Profile views
• Content views
• Reach
• Engagement
• Search discovery
• Product interactions
• Follower growth
• Advertising performance

Business users see only authorized business data.

────────────────────────────────────────

ADVERTISING FOUNDATION

Implement:

• Advertiser account
• Organization
• Campaign
• Ad set
• Creative
• Placement
• Budget
• Schedule
• Frequency cap
• Eligibility
• Ad event
• Performance aggregate

────────────────────────────────────────

CAMPAIGN STATES

Support:

• Draft
• Pending Review
• Approved
• Scheduled
• Active
• Paused
• Completed
• Rejected
• Archived

────────────────────────────────────────

AD ELIGIBILITY

Before serving:

• Campaign active
• Ad set active
• Creative approved
• Budget available
• Placement valid
• Schedule valid
• Frequency rules valid
• Privacy rules valid
• Safety rules valid

────────────────────────────────────────

AD TARGETING

Support policy-compliant targeting such as:

• Geography
• Context
• Broad audience
• Interest categories where allowed

Do not design prohibited sensitive targeting.

────────────────────────────────────────

AD FREQUENCY

Track exposure by:

• User
• Campaign
• Creative
• Placement
• Time window

Use Redis for fast ephemeral enforcement with durable event backing.

────────────────────────────────────────

AD EVENTS

Track:

• Ad served
• Impression
• Click
• Video start
• Video completion
• Conversion reference

Events must be idempotent.

────────────────────────────────────────

AD BILLING BOUNDARY

Keep billing/payment provider details behind an abstraction.

Advertising event tracking must not become the payment source of truth.

────────────────────────────────────────

COMMERCE FOUNDATION

Support:

• Business
• Product catalog
• Product
• Product collection
• Product tag
• Availability
• Product analytics

────────────────────────────────────────

PRODUCT CATALOG

Support:

• Catalog owner
• Name
• Status
• Currency
• Products
• Collections

Business ownership is authoritative.

────────────────────────────────────────

PRODUCT

Include:

• Product ID
• Catalog
• Name
• Description
• Media
• External URL/reference
• Price reference
• Availability
• Status

Do not assume the platform itself is the seller.

────────────────────────────────────────

PRODUCT TAGS

Content may reference:

• Product
• Position
• Display metadata

Do not duplicate the entire product record into every post.

────────────────────────────────────────

ADMINISTRATION

Create backend administration APIs for:

• Users
• Profiles
• Creators
• Businesses
• Content
• Messages where authorized
• Reports
• Moderation
• Rights
• Advertising
• Commerce
• Search
• Feed diagnostics
• Analytics
• Privacy
• Feature flags
• Configuration
• Audit

────────────────────────────────────────

ADMIN ROLES

Define:

• Support
• Moderator
• Safety
• Rights
• Fraud
• Advertising
• Commerce
• Analytics
• Privacy
• Security
• Operations
• Administrator

Use least privilege.

────────────────────────────────────────

ADMIN DATA ACCESS

Sensitive resources require:

• Permission
• Reason
• Audit

Do not expose full private message or location data merely because an employee is an administrator.

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

Every flag has:

• Owner
• Version
• State
• Start time
• Expiration
• Rollback behavior

────────────────────────────────────────

DYNAMIC CONFIGURATION

Support typed configuration for:

• Upload limits
• Feed limits
• Recommendation thresholds
• Search limits
• Message limits
• Notification limits
• Moderation thresholds
• Ad frequency
• Product limits
• API rate limits

Configuration must be:

• Typed
• Validated
• Versioned
• Audited
• Rollback-capable

────────────────────────────────────────

AUDIT

Audit:

• Admin actions
• Moderation
• Rights changes
• Business ownership
• Advertising changes
• Feature flags
• Configuration
• Privacy actions
• Security actions

Fields:

• Actor
• Role
• Action
• Resource
• Reason
• Request ID
• Correlation ID
• Region
• Timestamp
• Result

Audit records are append-only.

────────────────────────────────────────

PRIVACY ARCHITECTURE

Support:

• Data access
• Data export
• Data deletion
• Account deletion
• Search-history deletion
• Message deletion/retention
• Saved-content deletion
• Recommendation-data controls
• Advertising controls
• Analytics controls

────────────────────────────────────────

DATA EXPORT

Export authorized user data including, where policy permits:

• Profile
• Social graph
• Posts
• Reels
• Stories metadata
• Comments
• Saves
• Collections
• Messages
• Search history
• Account settings
• Privacy settings
• Contributions
• Analytics available to the user

Exports should be generated asynchronously.

────────────────────────────────────────

EXPORT SECURITY

Export artifacts must use:

• Private S3
• Encryption
• Short-lived download authorization
• Expiration
• Audit

Never expose export objects publicly.

────────────────────────────────────────

DATA DELETION

Support asynchronous deletion across:

• Identity
• Profile
• Social graph
• Content
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
• Notifications

────────────────────────────────────────

DELETION ORCHESTRATION

Use:

Privacy Request
→ Domain deletion tasks
→ Progress tracking
→ Verification
→ Derived-data cleanup
→ Completion

Each domain reports completion independently.

────────────────────────────────────────

RETENTION

Define separate policies for:

• Stories
• Messages
• Media
• Raw analytics
• Search history
• Recommendation features
• Moderation evidence
• Rights evidence
• Audit records
• Advertising events

Do not retain sensitive data indefinitely.

────────────────────────────────────────

DELETION RECONCILIATION

Verify deletion propagation across:

• PostgreSQL
• Redis
• OpenSearch
• Kafka-derived stores
• Analytics
• Recommendation features
• Notification state
• Search history

────────────────────────────────────────

DATABASE

Implement Prisma models/migrations for:

MESSAGING

• Conversation
• ConversationParticipant
• ConversationRequest
• Message
• MessageAttachment
• MessageReaction
• MessageReadState
• MessageDelivery

NOTIFICATIONS

• Notification
• NotificationPreference
• NotificationDelivery
• PushDevice
• NotificationGroup

MODERATION

• Report
• ModerationCase
• ModerationAction
• ModerationEvidenceReference
• Appeal
• SafetyEscalation

RIGHTS

• RightsClaim
• RightsRestriction
• RightsAppeal
• RightsReference

ADVERTISING

• AdAccount
• AdvertiserOrganization
• Campaign
• AdSet
• AdCreative
• AdPlacement
• AdFrequencyState
• AdEventReference
• AdPerformanceAggregate

COMMERCE

• ProductCatalog
• Product
• ProductCollection
• ProductTag

ANALYTICS

• CreatorAnalyticsAggregate
• BusinessAnalyticsAggregate
• PlatformAnalyticsAggregate

PRIVACY

• PrivacyRequest
• PrivacyTask
• ExportArtifact
• DeletionTask

ADMIN

• AdminRole
• AdminPermission
• AuditLog
• FeatureFlag
• FeatureFlagVersion
• SystemConfiguration
• ConfigurationVersion

────────────────────────────────────────

DATABASE CONSTRAINTS

Use:

• Foreign keys
• Unique constraints
• Composite indexes
• Status indexes
• Timestamp indexes
• Revision/version fields
• Expiration fields

Messaging uniqueness should protect against duplicate mutation IDs.

Notification uniqueness should prevent repeated event fanout.

Report constraints should prevent uncontrolled duplication.

────────────────────────────────────────

DATABASE INDEXING

MESSAGING:

• Conversation
• Participant
• Message sequence
• Message time
• Request status

NOTIFICATIONS:

• Recipient
• Read state
• Created time

MODERATION:

• Target
• Status
• Priority
• Assignee

RIGHTS:

• Content
• Region
• Status

ADVERTISING:

• Advertiser
• Campaign
• Status
• Schedule

COMMERCE:

• Catalog
• Business
• Product status

PRIVACY:

• User
• Request status
• Created time

AUDIT:

• Actor
• Resource
• Action
• Timestamp

────────────────────────────────────────

REDIS

Use Redis for:

• Presence
• Typing indicators
• Message fanout coordination
• Notification deduplication
• Ad frequency state
• Rate limiting
• Moderation job coordination
• Feature-flag cache
• Configuration cache
• Privacy-job locks
• Temporary export status
• Realtime connection state

Redis is never authoritative for:

• Messages
• Notifications
• Reports
• Moderation cases
• Rights
• Advertising campaigns
• Products
• Privacy requests
• Audit

────────────────────────────────────────

KAFKA EVENTS

MESSAGING:

• ConversationCreated
• MessageRequestCreated
• MessageCreated
• MessageEdited
• MessageDeleted
• MessageDelivered
• MessageRead
• MessageReactionCreated

NOTIFICATIONS:

• NotificationCreated
• NotificationDelivered
• NotificationFailed

TRUST:

• ReportCreated
• ModerationCaseCreated
• ModerationActionTaken
• AppealCreated
• AppealResolved
• SafetyEscalationCreated

RIGHTS:

• RightsClaimCreated
• RightsRestrictionApplied
• RightsRestrictionRemoved
• RightsAppealCreated
• RightsRestored

ANALYTICS:

• CreatorMetricUpdated
• BusinessMetricUpdated
• PlatformMetricUpdated

ADVERTISING:

• AdCampaignCreated
• AdCampaignActivated
• AdServed
• AdImpression
• AdClick
• AdVideoStarted
• AdVideoCompleted

COMMERCE:

• ProductCreated
• ProductUpdated
• ProductTagged
• ProductRemoved

PRIVACY:

• PrivacyRequestCreated
• PrivacyTaskCompleted
• DataExportCompleted
• DataDeletionCompleted

ADMIN:

• FeatureFlagChanged
• ConfigurationChanged
• AdministrativeActionTaken

All events must be:

• Versioned
• Idempotent
• Region-aware
• Privacy-aware
• Correlation-aware

────────────────────────────────────────

BULLMQ

Queues:

• Notification delivery
• Push delivery
• Email delivery
• Message cleanup
• Moderation
• Safety escalation
• Rights processing
• Analytics aggregation
• Advertising event aggregation
• Commerce processing
• Privacy export
• Privacy deletion
• Reconciliation
• Audit maintenance
• Configuration propagation
• Feature-flag propagation
• Cleanup

Every queue requires:

• Job schema
• Retry
• Backoff
• Timeout
• Concurrency
• Idempotency
• Dead-letter handling
• Metrics

────────────────────────────────────────

API

MESSAGING:

• Create conversation
• Get conversation
• List conversations
• Send message
• Edit message
• Delete message
• Add reaction
• Remove reaction
• Mark read
• Send message request
• Accept request
• Reject request
• Delete request
• Add/remove participant where authorized

NOTIFICATIONS:

• List
• Get
• Mark read
• Mark all read
• Preferences
• Register device
• Remove device

REPORTING:

• Create report
• Get own report status

MODERATION:

• Create case
• Get case
• Add action
• Appeal
• Resolve

RIGHTS:

• Submit claim
• Get claim
• Submit appeal
• Restrict content where authorized
• Restore where authorized

ADVERTISING:

• Create advertiser
• Create campaign
• Update campaign
• Create ad set
• Create creative
• Activate
• Pause
• Analytics

COMMERCE:

• Create catalog
• Create product
• Update product
• Create collection
• Tag product
• Remove product tag

PRIVACY:

• Request export
• Get export status
• Download authorization
• Request deletion
• Get deletion status
• Cancel where policy allows

ADMIN:

• Users
• Content
• Reports
• Moderation
• Rights
• Advertising
• Commerce
• Analytics
• Feature flags
• Configuration
• Audit
• Privacy

All endpoints must implement:

• Authentication
• Authorization
• Validation
• Rate limiting
• Idempotency where required
• OpenAPI
• Consistent errors
• Audit where required

────────────────────────────────────────

WEBSOCKET API

Support:

• Message created
• Message updated
• Message deleted
• Delivery update
• Read update
• Reaction update
• Typing
• Presence
• Notification update
• Moderation-status update where appropriate

Every subscription requires authorization.

────────────────────────────────────────

SECURITY

Protect against:

• Message IDOR
• Conversation enumeration
• Private-content access
• Notification spoofing
• Push-token abuse
• Report flooding
• Moderation escalation
• Rights manipulation
• Ad fraud
• Product ownership takeover
• Privacy-request abuse
• Admin privilege escalation
• Audit manipulation
• WebSocket hijacking

────────────────────────────────────────

MESSAGING SECURITY

Validate:

• Sender membership
• Conversation state
• Block
• Message permissions
• Attachment ownership

Never allow arbitrary message access by ID.

────────────────────────────────────────

NOTIFICATION SECURITY

Never trust client input for:

• Notification origin
• Notification recipient
• Security classification

These come from server-side event context.

────────────────────────────────────────

MODERATION SECURITY

Only authorized roles may:

• Change moderation state
• Access restricted evidence
• Escalate safety cases
• Restore content

────────────────────────────────────────

ADVERTISING SECURITY

Protect against:

• Duplicate impressions
• Fake clicks
• Budget race conditions
• Frequency-cap bypass
• Creative unauthorized edits

────────────────────────────────────────

PRIVACY SECURITY

Protect against:

• Unauthorized export
• Export-token reuse
• Deletion-request spoofing
• Cross-user deletion
• Privacy status tampering

────────────────────────────────────────

OBSERVABILITY

Instrument:

• Message send
• Message delivery
• Message read
• WebSocket connections
• Notification creation
• Push delivery
• Moderation queue
• Rights actions
• Ad event ingestion
• Commerce mutations
• Privacy jobs
• Admin actions

Track:

• Message latency
• Delivery latency
• WebSocket connections
• Notification latency
• Push failure rate
• Moderation backlog
• Rights backlog
• Analytics lag
• Ad event lag
• Privacy workflow duration
• Queue depth
• Kafka lag
• Reconciliation mismatches

Never log:

• Message content
• Private media URLs
• Private moderation evidence
• Push credentials
• Export links
• Sensitive personal data

────────────────────────────────────────

SLO / SLI

Define SLOs for:

• Message send
• Message delivery
• WebSocket connection
• Notification generation
• Push delivery
• Moderation processing
• Rights processing
• Analytics ingestion
• Privacy export
• Privacy deletion
• Ad event ingestion

For each define:

• SLI
• Measurement
• Target
• Error budget
• Alert threshold

────────────────────────────────────────

FAILURE MODES

Define graceful behavior for:

• WebSocket outage
• Push provider outage
• Email provider outage
• Kafka delay
• Redis failure
• Moderation worker outage
• Rights-provider outage
• Analytics outage
• Ad-event pipeline outage
• Privacy worker failure

Fallbacks:

• Persist message and deliver later
• Queue notifications
• Retry moderation
• Retry analytics
• Queue privacy tasks
• Preserve authoritative transaction state

Never bypass:

• Authorization
• Privacy
• Rights
• Moderation

────────────────────────────────────────

TESTING

MESSAGING:

• Conversation creation
• Membership
• Message send
• Idempotent retry
• Ordering
• Edit
• Delete
• Read
• Reaction
• Reply
• Attachments
• Message requests
• Blocking

WEBSOCKET:

• Authentication
• Subscription authorization
• Reconnect
• Duplicate events
• Backpressure
• Connection drain

NOTIFICATIONS:

• Event conversion
• Grouping
• Preferences
• Push
• Invalid token
• Retry
• Deduplication

MODERATION:

• Report
• Case
• Action
• Appeal
• Restore
• Role authorization

RIGHTS:

• Claim
• Restriction
• Appeal
• Restore
• Region

ADVERTISING:

• Campaign
• Budget
• Eligibility
• Frequency
• Duplicate event
• Reporting

COMMERCE:

• Catalog
• Product
• Tag
• Authorization

PRIVACY:

• Export
• Authorization
• Expiration
• Deletion
• Reconciliation

SECURITY:

• IDOR
• Admin escalation
• Report abuse
• Export abuse
• Message enumeration
• Conversation access

CONCURRENCY:

• Duplicate message
• Delivery/read race
• Moderation action race
• Campaign budget race
• Frequency-cap race
• Privacy task race

PERFORMANCE:

• Concurrent messaging
• WebSocket connections
• Notification fanout
• Moderation throughput
• Analytics ingestion
• Ad event ingestion
• Privacy workloads

────────────────────────────────────────

DOCUMENTATION

Generate:

• Messaging architecture
• Conversation model
• Membership
• Message model
• Ordering
• Idempotency
• Delivery
• Read receipts
• Reactions
• Replies
• Attachments
• Message requests
• Real-time
• Presence
• Typing
• Notification architecture
• Notification grouping
• Notification preferences
• Push
• FCM
• APNS
• Email
• Moderation
• Moderation cases
• Moderation actions
• Reporting
• Safety
• Appeals
• Rights
• Copyright claims
• Rights enforcement
• Creator analytics
• Business analytics
• Advertising
• Campaigns
• Ad sets
• Creatives
• Frequency caps
• Ad events
• Commerce
• Product catalogs
• Products
• Product tags
• Administration
• Feature flags
• Dynamic configuration
• Audit
• Privacy
• Data export
• Data deletion
• Retention
• Reconciliation
• Security
• Observability
• Testing

────────────────────────────────────────

PROJECT INDEX

Update the backend Project Index with:

• Messaging
• Conversations
• Participants
• Message requests
• Messages
• Attachments
• Reactions
• Replies
• Read state
• Delivery state
• Presence
• Typing
• WebSockets
• Notifications
• Preferences
• Push devices
• Notification delivery
• Reports
• Moderation cases
• Moderation actions
• Appeals
• Safety escalations
• Rights claims
• Rights restrictions
• Rights appeals
• Creator analytics
• Business analytics
• Advertising
• Ad accounts
• Campaigns
• Ad sets
• Creatives
• Placements
• Frequency caps
• Ad events
• Commerce
• Catalogs
• Products
• Product collections
• Product tags
• Privacy requests
• Export artifacts
• Deletion tasks
• Admin roles
• Audit logs
• Feature flags
• Configuration
• Reconciliation
• Kafka topics
• BullMQ queues
• Redis keys
• Database migrations
• APIs
• WebSocket events
• Tests
• Security
• Privacy
• Observability
• Generated files
• Modified files
• Remaining work
• Current milestone
• Dependencies

────────────────────────────────────────

IMPLEMENTATION MILESTONES

BACKEND MILESTONE 31

Messaging foundation, conversations, participants, membership authorization, message requests, message ordering, idempotent send, message persistence, and APIs.

BACKEND MILESTONE 32

Message attachments, reactions, replies, edits, deletions, read state, delivery state, blocking integration, privacy, and message retention.

BACKEND MILESTONE 33

WebSockets, Socket.IO, reconnect, presence, typing indicators, real-time delivery, connection authorization, Redis coordination, and backpressure.

BACKEND MILESTONE 34

Notifications, notification grouping, preferences, device registration, FCM/APNS adapters, push delivery, retries, deduplication, and in-app notifications.

BACKEND MILESTONE 35

Reporting, moderation cases, moderation actions, policy versioning, safety escalation, appeals, evidence references, and authorization.

BACKEND MILESTONE 36

Copyright/rights claims, restrictions, regional rights, audio restrictions, takedowns, appeals, restoration, expiration, and rights propagation.

BACKEND MILESTONE 37

Creator analytics, business analytics, aggregation pipelines, privacy-safe reporting, analytics reconciliation, and dashboard contracts.

BACKEND MILESTONE 38

Advertising accounts, campaigns, ad sets, creatives, placements, eligibility, budgets, frequency caps, event ingestion, fraud protection, and analytics.

BACKEND MILESTONE 39

Commerce catalogs, products, collections, product tagging, business permissions, privacy controls, administration, feature flags, configuration, audit, and reconciliation.

BACKEND MILESTONE 40

Privacy export/deletion, retention, cross-domain cleanup, full messaging/notification/moderation/rights/advertising/commerce integration, security hardening, performance testing, disaster recovery validation, documentation, and final Project Index completion.

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

This volume covers:

• Messaging
• Conversations
• Message requests
• Messages
• Attachments
• Reactions
• Replies
• Delivery
• Read receipts
• Presence
• Typing
• WebSockets
• Notifications
• Push
• FCM
• APNS
• Reporting
• Moderation
• Safety
• Appeals
• Rights
• Copyright
• Creator analytics
• Business analytics
• Advertising
• Commerce
• Administration
• Feature flags
• Configuration
• Audit
• Privacy
• Export
• Deletion
• Retention
• Reconciliation
• Security hardening
• Operational hardening
• Final backend integration

Do not redesign or reimplement the previously approved:

• Identity
• Accounts
• Profiles
• Creators
• Businesses
• Devices
• Sessions
• Social graph
• Posts
• Reels
• Stories
• Media
• Audio
• Hashtags
• Feed
• Explore
• Recommendations
• Search
• PostgreSQL
• Prisma
• Redis
• Kafka
• BullMQ
• S3
• Content authorization

Consume their established APIs, repositories, events, queues, and ownership boundaries.

Do not implement:

• Frontend
• Mobile
• Infrastructure
• Terraform
• Kubernetes
• CI/CD

────────────────────────────────────────

QUALITY BAR

Treat messaging, notifications, moderation, rights, privacy, advertising, commerce, and administration as mission-critical systems.

Assume:

• Hundreds of millions of users
• Massive messaging traffic
• Billions of notification events
• Large moderation workloads
• Large rights workflows
• Large creator analytics datasets
• Large advertising event volumes
• Large commerce catalogs
• Massive privacy requests
• Multiple regions
• High availability
• Strict privacy
• Strict security

Prioritize:

• Message correctness
• Message ordering
• Idempotency
• Real-time reliability
• Notification reliability
• Moderation safety
• Rights correctness
• Analytics accuracy
• Advertising integrity
• Commerce authorization
• Privacy
• Auditability
• Reconciliation
• Horizontal scalability
• Observability
• Fault tolerance
• Maintainability
• Production readiness
