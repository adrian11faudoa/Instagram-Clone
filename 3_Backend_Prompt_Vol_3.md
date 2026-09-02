You are operating in Senior Engineering Team Mode.

Build the production-ready backend for the discovery, feed, recommendation, Explore, trending, search, hashtags, audio discovery, engagement aggregation, and content-distribution systems of an enterprise-scale global visual-social platform comparable in architectural scope to Instagram.

The platform is an original implementation.

Do not copy proprietary source code, internal architecture, branding, confidential implementation details, proprietary algorithms, proprietary datasets, private implementation details, or internal systems from Instagram, Meta, or any other company.

This prompt is completely independent and may be executed in a separate conversation.

Use the previously approved architecture and previously implemented backend foundations as the single source of truth.

Do not redesign the approved architecture.

Do not generate frontend code.

Do not generate mobile code.

Do not generate infrastructure implementation code.

Do not generate Terraform.

Do not generate Kubernetes manifests.

Do not generate CI/CD workflows.

────────────────────────────────────────

MISSION

Implement the production-ready backend required for:

• Home feed
• Following feed
• Reels feed
• Story tray
• Explore
• Recommendations
• Candidate generation
• Candidate eligibility
• Ranking
• Re-ranking
• Diversity
• Freshness
• Negative feedback
• Content affinity
• Creator affinity
• Hashtag affinity
• Audio affinity
• Trending
• Personalized discovery
• Creator discovery
• User discovery
• Hashtag discovery
• Audio discovery
• Feed pagination
• Feed caching
• Recommendation profiles
• Recommendation features
• Experimentation
• Ranking versions
• Candidate-source attribution
• Feed impression tracking
• Watch events
• Engagement signals
• Search
• User search
• Creator search
• Post search
• Reel search
• Hashtag search
• Audio search
• Search suggestions
• Search history foundation
• Search indexing
• Search deletion
• Search reindexing
• Search ranking
• Search privacy filtering
• Trending aggregation
• Recommendation safety filtering
• Discovery abuse protection
• Engagement counters
• Content distribution events
• Feed reconciliation

The implementation must integrate with:

• Identity
• Accounts
• Profiles
• Creators
• Businesses
• Devices
• Social Graph
• Blocks
• Restrictions
• Close Friends
• Posts
• Reels
• Stories
• Media
• Audio
• Hashtags
• Mentions
• Locations
• Rights
• Moderation
• PostgreSQL
• Prisma
• Redis
• Kafka/Redpanda
• BullMQ
• OpenSearch/Elasticsearch
• WebSockets
• S3/CDN
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

• Elasticsearch or OpenSearch

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

Use idempotency for events and retriable operations.

Use optimistic concurrency where appropriate.

Never trust client-supplied ranking decisions.

Never trust client-supplied content eligibility.

Never expose internal recommendation features or ranking scores.

────────────────────────────────────────

DOMAIN OWNERSHIP

Maintain explicit boundaries between:

• Feed
• Recommendations
• Explore
• Trending
• Search
• Hashtags
• Audio discovery
• Engagement signals
• Content
• Social graph
• Moderation
• Rights

Do not make:

• Search the source of truth for content
• Feed the source of truth for content
• Recommendation caches authoritative
• Engagement counters authoritative over relationships
• Trending directly controllable by clients

────────────────────────────────────────

FEED ARCHITECTURE

Implement:

Request
→ Context
→ Candidate Generation
→ Eligibility
→ Ranking
→ Re-ranking
→ Diversity
→ Response
→ Impression/Event recording

Support feed types:

• Home
• Following
• Reels

────────────────────────────────────────

FEED CONTEXT

Context may include:

• User
• Account state
• Follow graph
• Blocks
• Restrictions
• Locale
• Region
• Device
• App version
• Recent interactions
• Content history
• Experiment assignment
• Platform configuration

Do not expose sensitive internal context to clients.

────────────────────────────────────────

CANDIDATE SOURCES

Candidate generation may use:

• Followed creators
• Creator affinity
• Similar content
• Similar creators
• Hashtag affinity
• Audio affinity
• Saved content
• Previously interacted content
• Trending content
• Explore content
• Fresh content
• Business/creator discovery
• Regional discovery

Each candidate should retain source attribution internally.

────────────────────────────────────────

CANDIDATE BUDGETS

Define per-source limits.

Prevent one candidate source from overwhelming the entire feed.

Support configurable budgets.

────────────────────────────────────────

CANDIDATE DEDUPLICATION

Deduplicate using:

• Content ID
• Repost relationship
• Original-content relationship

Prevent multiple representations of the same content from consuming the same feed slots unnecessarily.

────────────────────────────────────────

ELIGIBILITY

Every candidate must be evaluated for:

• Account status
• Content status
• Visibility
• Private account
• Follow relationship
• Block
• Restriction
• Rights
• Moderation
• Region
• Age/safety policy
• Recommendation eligibility

Eligibility must be server-side.

────────────────────────────────────────

DELETED CONTENT

Deleted content must not be returned from:

• Home
• Following
• Explore
• Reels
• Recommendations
• Trending

Use event propagation and defensive read-time filtering.

────────────────────────────────────────

PRIVATE CONTENT

Private content can appear only when:

• Viewer is authorized
• Follow relationship permits it
• Visibility policy permits it

Private content must never enter public recommendation surfaces.

────────────────────────────────────────

BLOCKING

Blocked users/content must be filtered from:

• Feed
• Explore
• Search
• Recommendations
• Stories
• Reels

Use graph events and read-time validation.

────────────────────────────────────────

RIGHTS / MODERATION FILTER

Content restricted by:

• Copyright
• Region
• Safety
• Moderation
• Account suspension

must be excluded from discovery.

────────────────────────────────────────

RANKING ARCHITECTURE

Implement pluggable ranking stages:

• Candidate scoring
• Relevance
• Engagement likelihood
• Freshness
• Creator affinity
• Topic affinity
• Quality
• Diversity
• Re-ranking

Do not embed model-specific implementation details into controllers.

────────────────────────────────────────

RANKING VERSION

Every feed response should internally record:

• Ranking version
• Candidate version
• Eligibility version
• Experiment assignment
• Feed type

Do not expose proprietary scoring details publicly.

────────────────────────────────────────

RANKING SIGNALS

Potential signals:

• Impression
• Watch duration
• Completion
• Rewatch
• Like
• Comment
• Share
• Save
• Repost
• Follow
• Profile visit
• Negative feedback
• Freshness
• Creator affinity
• Content affinity
• Search interaction

Signal availability must respect privacy policy.

────────────────────────────────────────

WATCH SIGNALS

Track:

• Start
• Watch duration
• Completion
• Rewatch
• Skip

Do not treat a single noisy event as definitive preference.

────────────────────────────────────────

NEGATIVE SIGNALS

Support:

• Not interested
• Hide content
• Hide creator
• Mute creator/topic
• Report

Negative feedback must influence future candidate eligibility or ranking according to policy.

────────────────────────────────────────

RE-RANKING

Apply constraints for:

• Creator diversity
• Topic diversity
• Audio diversity
• Format diversity
• Freshness
• Repetition limits

Do not let re-ranking violate:

• Privacy
• Rights
• Moderation
• Blocking

────────────────────────────────────────

DIVERSITY

Prevent excessive concentration around:

• One creator
• One hashtag
• One audio
• One topic
• One content format

Define configurable constraints.

────────────────────────────────────────

FRESHNESS

Support:

• New-content boost
• Time decay
• Freshness windows

Avoid burying high-quality content immediately after publication.

────────────────────────────────────────

FEED PAGINATION

Use opaque cursor pagination.

Cursor must account for:

• Feed type
• Ranking version where appropriate
• Feed session
• Position
• Expiration

Prevent:

• Duplicate items
• Unexpected ordering
• Cross-feed cursor reuse

────────────────────────────────────────

FEED SESSION

Represent:

• Session ID
• User
• Feed type
• Ranking version
• Created time
• Expiration
• Cursor state

Session state may be cached.

Do not make feed cache authoritative.

────────────────────────────────────────

FEED CACHE

Use Redis for:

• Feed candidate pages
• Candidate pools
• Story tray
• Following feed
• Reels feed
• Explore

Keys include:

• Environment
• Region
• User
• Feed type
• Ranking version

────────────────────────────────────────

CACHE STAMPEDE PROTECTION

Implement:

• Request coalescing
• Short locks
• Jittered expiration
• Background refresh where justified

Do not allow large user populations to regenerate identical candidate pools simultaneously.

────────────────────────────────────────

FOLLOWING FEED

Primary source:

• Followed accounts

Still enforce:

• Block
• Restriction
• Private visibility
• Deleted content
• Moderation
• Rights

────────────────────────────────────────

HOME FEED

Potential sources:

• Followed accounts
• Recommendations
• Similar content
• Trending
• Discovery

Apply personalized ranking.

────────────────────────────────────────

REELS FEED

Candidate sources:

• Fresh reels
• Creator affinity
• Similar content
• Trending audio
• Trending topics
• Exploration

Use separate ranking configuration from standard posts.

────────────────────────────────────────

STORY TRAY

Implement:

• Candidate generation
• Eligibility
• Seen state
• Unseen priority
• Close friends
• Recency
• Creator affinity

Do not return expired stories.

────────────────────────────────────────

STORY VIEW STATE

Track:

• Story item
• Viewer
• Seen timestamp

Use efficient uniqueness and idempotency.

────────────────────────────────────────

EXPLORE

Implement discovery independent of the home feed.

Support:

• Posts
• Reels
• Creators
• Hashtags
• Audio

Potential signals:

• Global popularity
• Regional popularity
• Topic affinity
• Creator affinity
• Freshness
• Engagement quality
• Diversity

────────────────────────────────────────

EXPLORE ELIGIBILITY

Exclude:

• Private content
• Deleted content
• Blocked accounts
• Restricted content
• Rights-restricted content
• Safety-restricted content

────────────────────────────────────────

TRENDING

Implement aggregation for:

• Hashtags
• Audio
• Creators
• Topics
• Reels
• Posts

Signals:

• Velocity
• Engagement
• Freshness
• Distinct users
• Distinct creators
• Geographic distribution
• Abuse-adjusted activity

────────────────────────────────────────

TRENDING WINDOW

Support configurable windows such as:

• Minutes
• Hour
• Several hours
• Daily

Use event streams and aggregation rather than synchronous counters for every request.

────────────────────────────────────────

TRENDING ABUSE

Do not allow raw volume alone to determine trending.

Adjust for:

• Spam
• Bot signals
• Coordinated behavior
• Duplicate events
• Suspicious bursts

────────────────────────────────────────

RECOMMENDATION PROFILE

Define internal profile containing:

• Content affinities
• Creator affinities
• Hashtag affinities
• Audio affinities
• Negative signals
• Topic interests
• Experiment assignments
• Model/ranking version

Do not store prohibited or unnecessary sensitive attributes.

────────────────────────────────────────

RECOMMENDATION FEATURES

Features may be:

• User-level
• Content-level
• Creator-level
• Interaction-level
• Temporal
• Aggregate

Separate:

• Raw events
• Derived features
• Model inputs

────────────────────────────────────────

FEATURE FRESHNESS

Track:

• Feature version
• Generated timestamp
• Expiration
• Source

Do not use stale high-impact features indefinitely.

────────────────────────────────────────

EXPERIMENTATION

Support:

• Experiment
• Variant
• Assignment
• Start/end time
• Eligibility
• Region
• Platform

Persist assignment deterministically.

────────────────────────────────────────

EXPERIMENT ISOLATION

Do not mix experimental ranking behavior across incompatible feed sessions without explicit handling.

Every experiment must have:

• Owner
• Version
• Status
• Configuration

────────────────────────────────────────

SEARCH ARCHITECTURE

Search:

• Users
• Creators
• Posts
• Reels
• Hashtags
• Audio

Optional:

• Public businesses
• Public locations

────────────────────────────────────────

SEARCH QUERY MODEL

Track:

• Query
• Normalized query
• User context where allowed
• Region
• Language
• Search type
• Session ID
• Timestamp

Do not retain raw query history indefinitely.

────────────────────────────────────────

SEARCH NORMALIZATION

Normalize:

• Case
• Unicode
• Whitespace
• Hashtag syntax
• Common variations

Do not destroy user-visible spelling unnecessarily.

────────────────────────────────────────

SEARCH RESULTS

Return:

• Public ID
• Display name/title
• Thumbnail where available
• Content type
• Creator
• Relevance metadata safe for public use

Do not expose:

• Internal scores
• Fraud signals
• Moderation internals
• Recommendation features

────────────────────────────────────────

SEARCH RANKING

Rank using:

• Text relevance
• Popularity
• Freshness
• User context where permitted
• Social context
• Content quality
• Region

Ranking must remain pluggable.

────────────────────────────────────────

SEARCH PRIVACY

Before returning a result check:

• Account visibility
• Content visibility
• Block
• Restriction
• Rights
• Moderation
• Region

Private content must never appear to unauthorized users.

────────────────────────────────────────

SEARCH INDEXING

Pipeline:

Canonical Content
→ Event
→ Queue
→ Search Document
→ Search Index

Support:

• Create
• Update
• Delete
• Bulk indexing
• Full rebuild
• Alias switching

────────────────────────────────────────

SEARCH DELETE

When content becomes:

• Deleted
• Private
• Moderated
• Rights restricted
• Account restricted

trigger index removal/update.

────────────────────────────────────────

SEARCH REINDEX

Support:

• New index
• Bulk indexing
• Document validation
• Count validation
• Sample query validation
• Alias switch
• Rollback

Never destroy the current index before validating the replacement.

────────────────────────────────────────

SEARCH SUGGESTIONS

Support:

• User
• Creator
• Hashtag
• Audio
• Recent query foundation

Do not expose other users' private search histories.

────────────────────────────────────────

SEARCH HISTORY

Where product policy permits:

• Store user search history
• Read own history
• Clear history
• Delete individual history item
• Delete all history

History must remain private.

────────────────────────────────────────

HASHTAG DISCOVERY

Support:

• Hashtag page
• Related hashtags
• Popular posts
• Popular reels
• Recent content
• Trending

Apply privacy, moderation, and rights filters.

────────────────────────────────────────

HASHTAG RANKING

Signals:

• Usage
• Velocity
• Engagement
• Freshness
• Distinct authors
• Abuse-adjusted volume

────────────────────────────────────────

AUDIO DISCOVERY

Support:

• Search
• Audio page
• Related audio
• Trending audio
• Reels using audio
• Usage count

Respect:

• Rights
• Region
• Moderation

────────────────────────────────────────

ENGAGEMENT AGGREGATES

Maintain derived counters for:

• Likes
• Comments
• Shares
• Saves
• Reposts
• Views
• Follows

Counters must be derived from authoritative records/events.

────────────────────────────────────────

COUNTER RECONCILIATION

Periodically compare aggregates against source data.

Repair discrepancies.

Do not use Redis-only counters as the permanent source of truth.

────────────────────────────────────────

IMPRESSION EVENTS

Track:

• Feed impression
• Explore impression
• Reel impression
• Story impression
• Search result impression

Include internal:

• Feed session
• Candidate source
• Ranking version
• Position

Do not expose ranking details to end users.

────────────────────────────────────────

EVENT DEDUPLICATION

Impression/engagement events may be retried.

Use:

• Event ID
• Client event ID
• Idempotency key

Avoid duplicate analytics signals.

────────────────────────────────────────

CONTENT DISTRIBUTION EVENTS

Publish:

• Content eligible
• Content published
• Content restricted
• Content deleted
• Content restored
• Creator blocked
• Rights restriction
• Moderation restriction

Consumers include:

• Feed
• Search
• Explore
• Trending
• Recommendation

────────────────────────────────────────

KAFKA EVENTS

DISCOVERY:

• FeedRequested
• FeedGenerated
• CandidateGenerated
• RecommendationServed
• ExploreGenerated
• SearchPerformed
• SearchSuggestionSelected

ENGAGEMENT:

• ContentImpression
• ContentWatched
• ContentCompleted
• ContentRewatched
• ContentSkipped
• ContentLiked
• ContentCommented
• ContentShared
• ContentSaved
• ContentReposted
• ProfileViewed
• CreatorFollowed
• NegativeFeedbackRecorded

TRENDING:

• TrendingSignalGenerated
• TrendingItemUpdated

SEARCH:

• SearchIndexRequested
• SearchIndexUpdated
• SearchIndexDeleted

EXPERIMENTS:

• ExperimentAssigned
• ExperimentExposureRecorded

All events must:

• Be versioned
• Be idempotent
• Include correlation metadata
• Minimize personal data

────────────────────────────────────────

BULLMQ

Queues:

• Feed candidate refresh
• Story tray refresh
• Recommendation feature refresh
• Search indexing
• Search deletion
• Full reindex
• Trending aggregation
• Feature aggregation
• Counter reconciliation
• Feed cache refresh
• Ranking-model/config propagation
• Cleanup
• Privacy deletion propagation

Each queue requires:

• Job schema
• Retry
• Backoff
• Timeout
• Concurrency
• Dead-letter handling
• Idempotency
• Metrics

────────────────────────────────────────

DATABASE

Implement Prisma models/migrations for:

FEED:

• FeedSession
• FeedCandidateReference
• FeedExposure
• FeedConfiguration
• RankingVersion

RECOMMENDATION:

• RecommendationProfile
• RecommendationFeature
• RecommendationExperiment
• ExperimentAssignment

SEARCH:

• SearchQueryReference
• SearchIndexVersion
• SearchConfiguration

TRENDING:

• TrendingEntity
• TrendingSnapshot
• TrendingSignalAggregate

ENGAGEMENT:

• EngagementAggregate
• CounterReconciliation

ANALYTICS REFERENCES:

• ImpressionReference
• WatchEventReference
• NegativeFeedbackReference

Use:

• Foreign keys
• Unique constraints
• Composite indexes
• Version fields
• Timestamps
• Expiration

────────────────────────────────────────

DATABASE INDEXING

Feed:

• User
• Feed type
• Created
• Expiration

Recommendations:

• User
• Feature type
• Version
• Updated

Trending:

• Entity
• Region
• Window
• Timestamp

Search:

• User
• Search session
• Timestamp where retained

Exposure:

• User
• Content
• Session
• Timestamp

────────────────────────────────────────

REDIS

Use Redis for:

• Feed cache
• Story tray
• Explore candidates
• Recommendation feature cache
• Trending state
• Search suggestions
• Search result cache
• Feed-generation locks
• Experiment assignment cache
• Rate limiting

Never use Redis as authoritative storage for:

• Feed relationships
• Content
• Search history
• Recommendation decisions
• Engagement relationships
• User privacy

────────────────────────────────────────

API

FEED

• Get home feed
• Get following feed
• Get reels feed
• Refresh feed
• Continue feed using cursor

EXPLORE

• Get explore
• Refresh explore

RECOMMENDATIONS

• Get recommended creators
• Get recommended content
• Submit negative feedback

SEARCH

• Search
• Suggestions
• Search history
• Clear search history

HASHTAGS

• Get hashtag
• Get related hashtags
• Get trending hashtags

AUDIO

• Search audio
• Get audio
• Get related audio
• Get trending audio

TRENDING

• Get trending content
• Get trending creators
• Get trending hashtags
• Get trending audio

ENGAGEMENT SIGNALS

Internal endpoints/services for:

• Impression ingestion
• Watch ingestion
• Completion
• Rewatch
• Negative feedback

Do not expose internal ranking controls as public APIs.

────────────────────────────────────────

FEED API

Use cursor pagination.

Response may include:

• Content
• Creator
• Media
• Minimal ranking metadata required by client
• Feed session cursor

Do not expose:

• Ranking score
• Model features
• Fraud score
• Experiment internals

────────────────────────────────────────

RECOMMENDATION API

Server controls:

• Eligibility
• Candidate count
• Ranking
• Diversity
• Safety

Client only requests recommendations.

────────────────────────────────────────

NEGATIVE FEEDBACK API

Support:

• Not interested
• Hide creator
• Hide topic
• Report

Requests are idempotent.

────────────────────────────────────────

SEARCH API

Support:

• Query
• Type/filter
• Cursor
• Language
• Region

Server controls:

• Maximum query length
• Result count
• Rate limits
• Privacy filtering

────────────────────────────────────────

SECURITY

Protect against:

• Feed scraping
• Search scraping
• Recommendation scraping
• Content enumeration
• Ranking extraction
• Experiment leakage
• Trending manipulation
• Fake engagement
• Bot activity
• Query abuse
• Cache poisoning

Use:

• Rate limiting
• Authentication where required
• Authorization
• Device/account signals
• Request budgets
• Abuse controls

────────────────────────────────────────

PRIVACY

Protect:

• Search history
• Recommendation profile
• Negative feedback
• Feed exposure history
• Behavioral signals
• Experiment assignments

Do not expose individualized ranking or behavioral data publicly.

────────────────────────────────────────

OBSERVABILITY

Instrument:

• Feed generation
• Candidate generation
• Eligibility
• Ranking
• Re-ranking
• Explore
• Recommendation
• Search
• Autocomplete
• Trending
• Counter aggregation
• Cache

Track:

• Feed latency
• Candidate latency
• Ranking latency
• Recommendation latency
• Search latency
• Autocomplete latency
• Cache hit ratio
• Duplicate rate
• Eligibility rejection rate
• Kafka lag
• Queue depth
• Indexing lag
• Feature freshness
• Trending freshness

────────────────────────────────────────

SLO / SLI

Define SLOs for:

• Home feed
• Following feed
• Reels feed
• Explore
• Recommendations
• Search
• Autocomplete
• Trending
• Impression ingestion

For each define:

• SLI
• Measurement
• Target
• Error budget
• Alert threshold

────────────────────────────────────────

FAILURE MODES

Define graceful fallback for:

• Recommendation outage
• Ranking failure
• Search outage
• Trending outage
• Redis failure
• Kafka delay
• OpenSearch outage
• Feature-store/cache failure

Possible fallbacks:

• Following feed
• Recent content
• Popular content
• Cached results
• Previous valid ranking version

Never bypass:

• Privacy
• Rights
• Moderation
• Blocking

────────────────────────────────────────

TESTING

UNIT TESTS

Test:

• Candidate eligibility
• Ranking contract
• Diversity
• Freshness
• Cursor generation
• Feed session
• Experiment assignment
• Search normalization
• Trending calculations
• Negative feedback
• Counter reconciliation

FEED TESTS

• Home
• Following
• Reels
• Cursor pagination
• Deduplication
• Deleted content
• Private content
• Blocked content
• Restricted content
• Rights restriction
• Cache behavior

RECOMMENDATION TESTS

• Candidate generation
• Feature availability
• Ranking
• Diversity
• Negative feedback
• Experiment assignment
• Model/version changes

SEARCH TESTS

• Users
• Creators
• Posts
• Reels
• Hashtags
• Audio
• Privacy
• Deleted content
• Typo
• Prefix
• Region

TRENDING TESTS

• Velocity
• Freshness
• Diversity
• Distinct users
• Abuse-adjustment
• Window boundaries

SECURITY TESTS

• Feed scraping
• Search scraping
• Ranking extraction
• Private-content leakage
• Behavioral-data leakage
• Rate-limit bypass

CONCURRENCY

• Duplicate impressions
• Counter race
• Feed-generation race
• Search index update/delete race
• Experiment assignment race

PERFORMANCE

• Feed generation
• Search
• Autocomplete
• Trending
• Recommendation

────────────────────────────────────────

DOCUMENTATION

Generate:

• Feed architecture
• Feed session
• Candidate generation
• Candidate budgets
• Eligibility
• Ranking
• Ranking versions
• Re-ranking
• Diversity
• Freshness
• Negative feedback
• Feed pagination
• Feed cache
• Home feed
• Following feed
• Reels feed
• Story tray
• Explore
• Trending
• Recommendation profiles
• Recommendation features
• Experimentation
• Search
• Search history
• Search normalization
• Search ranking
• Search indexing
• Search deletion
• Search reindexing
• Search suggestions
• Hashtags
• Hashtag discovery
• Audio discovery
• Engagement aggregates
• Counter reconciliation
• Impression events
• Event deduplication
• Distribution events
• Kafka event catalog
• BullMQ queue catalog
• Database schema
• Redis key catalog
• Security
• Privacy
• Observability
• Testing
• Failure modes

────────────────────────────────────────

PROJECT INDEX

Update the backend Project Index with:

• Home feed
• Following feed
• Reels feed
• Story tray
• Feed sessions
• Feed candidates
• Candidate sources
• Eligibility
• Ranking
• Ranking versions
• Re-ranking
• Diversity
• Freshness
• Negative feedback
• Feed cache
• Explore
• Trending
• Recommendation profiles
• Recommendation features
• Experiments
• Search
• Search suggestions
• Search history
• Search indexes
• Search versions
• Hashtags
• Hashtag discovery
• Audio discovery
• Engagement aggregates
• Counters
• Counter reconciliation
• Impressions
• Watch events
• Negative feedback events
• Kafka topics
• BullMQ queues
• Redis keys
• Database migrations
• APIs
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

BACKEND MILESTONE 21

Feed service foundation, feed sessions, feed cursors, candidate-source abstraction, candidate budgets, eligibility, content-visibility filtering, and feed APIs.

BACKEND MILESTONE 22

Following feed, home feed, Reels feed, Story tray, feed caching, cache-stampede protection, pagination, deduplication, and content-distribution events.

BACKEND MILESTONE 23

Recommendation profiles, features, affinity signals, watch signals, negative feedback, ranking abstraction, ranking versions, experimentation, and recommendation APIs.

BACKEND MILESTONE 24

Re-ranking, diversity, freshness, creator/topic/audio balancing, model/configuration propagation, recommendation safety, and ranking observability.

BACKEND MILESTONE 25

Explore, personalized discovery, creator discovery, content discovery, regional discovery, Explore caching, and eligibility.

BACKEND MILESTONE 26

Trending infrastructure, velocity calculations, time windows, abuse-adjusted trending, regional trends, audio trends, hashtag trends, creator trends, and trending APIs.

BACKEND MILESTONE 27

Search backend, search normalization, search ranking, suggestions, search history, privacy filtering, search indexing, deletion, reindexing, and aliases.

BACKEND MILESTONE 28

Hashtag discovery, audio discovery, engagement-signal ingestion, impressions, watch events, negative feedback events, counter aggregation, and reconciliation.

BACKEND MILESTONE 29

Kafka/BullMQ integration, Redis optimization, failure handling, fallback feeds, search fallback, security hardening, scraping protection, privacy controls, and observability.

BACKEND MILESTONE 30

Full feed/recommendation/search integration, concurrency testing, load testing, ranking regression, privacy validation, security testing, documentation, and Project Index completion.

Each milestone should contain approximately 20–40 files where practical.

Every milestone must compile before proceeding.

────────────────────────────────────────

OUTPUT FORMAT

For every generated file provide:

1. Exact file path
2. Complete file contents

Never truncate code.

Never summarize implementation instead of generating it.

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

• Feed
• Explore
• Recommendations
• Candidate generation
• Eligibility
• Ranking
• Re-ranking
• Diversity
• Freshness
• Negative feedback
• Feed pagination
• Feed caching
• Story tray
• Trending
• Search
• Search suggestions
• Search history
• Search ranking
• Search indexing
• Search deletion
• Search reindexing
• Hashtag discovery
• Audio discovery
• Engagement signals
• Impression events
• Watch events
• Counter aggregation
• Counter reconciliation
• Discovery security
• Discovery privacy
• Related events
• Related queues
• Related workers
• Related APIs
• Related tests

Do not implement complete:

• Messaging
• Notification delivery
• Full moderation platform
• Full rights platform
• Advertising
• Commerce
• Complete analytics warehouse
• Administration UI
• Frontend
• Mobile
• Infrastructure

Use the existing identity, social graph, content, media, audio, hashtag, rights, moderation, PostgreSQL, Redis, Kafka, BullMQ, OpenSearch, and security foundations.

────────────────────────────────────────

QUALITY BAR

Treat feed, recommendations, discovery, search, and trending as high-scale distributed systems.

Assume:

• Hundreds of millions of users
• Billions of content objects
• Massive feed traffic
• Massive recommendation requests
• Massive search traffic
• Massive impression streams
• Large real-time engagement streams
• Multiple regions
• Rapidly changing content
• Strict privacy
• Strict moderation and rights enforcement

Prioritize:

• Low latency
• Recommendation safety
• Feed correctness
• Privacy
• Ranking isolation
• Eligibility correctness
• Search relevance
• Trending integrity
• Cache efficiency
• Event idempotency
• Abuse resistance
• Horizontal scalability
• Observability
• Fault tolerance
• Maintainability
• Production readiness
