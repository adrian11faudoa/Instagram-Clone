Using the approved Architecture Blueprint — Volume 1, the approved Architecture Blueprint — Volume 2, and the Master Prompt above.

Begin backend implementation ONLY.

Do NOT generate frontend code.

Do NOT generate mobile code.

Do NOT generate infrastructure code unless a minimal local development dependency is strictly required for backend execution and testing.

Do NOT redesign the architecture.

Do NOT redesign the approved database model, service boundaries, event contracts, or API contracts unless an implementation conflict makes a correction absolutely necessary. If a correction is required, explicitly document it before modifying the approved design.

Assume the architecture has been approved.

Follow it exactly.

Generate production-ready backend code incrementally according to the Master Prompt milestone strategy.

────────────────────────────────────────

MISSION

Build the complete production-ready backend for a global visual-first social media, creator, business, commerce, messaging, advertising, and AI-ready platform.

The backend must support:

• Photos

• Carousels

• Posts

• Short-form Video

• Reels

• Stories

• Highlights

• Live Streaming

• User Profiles

• Creator Profiles

• Professional Accounts

• Business Accounts

• Social Graph

• Followers

• Following

• Private Accounts

• Close Friends

• Feed Generation

• Explore

• Recommendations

• Likes

• Reactions

• Comments

• Mentions

• Hashtags

• Bookmarks

• Collections

• Direct Messaging

• Notifications

• Search

• Creator Analytics

• Business Analytics

• Commerce

• Advertising

• Moderation

• Trust & Safety

• AI-ready capabilities

Design and implement for:

• 1B+ registered users

• 300M+ daily active users

• 100B+ posts

• 20B+ videos

• 50B+ images

• Billions of feed requests

• Millions of concurrent users

• Global multi-region deployment

• Active-active architecture

• Horizontal scaling

• High availability

• Zero-downtime deployments

────────────────────────────────────────

TECHNOLOGY STACK

Language

• TypeScript

Runtime

• Node.js

Framework

• NestJS

Database

• PostgreSQL

ORM

• Prisma

Cache

• Redis

Event Streaming

• Kafka or Redpanda

Background Jobs

• BullMQ

Search

• Elasticsearch or OpenSearch

Realtime

• Socket.IO

Object Storage

• AWS S3-compatible storage

CDN

• CloudFront-compatible CDN architecture

Image Processing

• Sharp

Video Processing

• FFmpeg

API Documentation

• OpenAPI / Swagger

Observability

• OpenTelemetry

• Structured Logging

• Metrics

────────────────────────────────────────

ARCHITECTURAL PRINCIPLES

Strictly follow:

• Clean Architecture

• Domain-Driven Design

• SOLID

• Repository Pattern

• Service Layer

• Dependency Injection

• Feature-first organization

• Domain boundaries

• Event-driven architecture where appropriate

• CQRS where appropriate

• Strict TypeScript

• Idempotent event consumers

• Versioned event contracts

• Backward-compatible APIs where possible

Never violate approved service boundaries without documenting the reason.

────────────────────────────────────────

BACKEND APPLICATION STRUCTURE

Implement a production-ready monorepo structure containing the approved backend services, shared packages, contracts, infrastructure interfaces, testing utilities, and developer tooling.

Generate and maintain:

• Service applications

• Shared domain packages

• Shared DTO packages

• Event contracts

• API contracts

• Configuration packages

• Authentication utilities

• Authorization utilities

• Logging utilities

• Error handling utilities

• Validation utilities

• Database packages

• Redis utilities

• Kafka utilities

• Queue utilities

• Storage utilities

• Observability utilities

• Testing utilities

────────────────────────────────────────

IMPLEMENT THE FOLLOWING SERVICES

API Gateway

Authentication Service

Authorization Service

Identity Service

User Service

Profile Service

Social Graph Service

Post Service

Media Service

Image Processing Service

Video Processing Service

Story Service

Reels Service

Feed Service

Recommendation Service

Hashtag Service

Search Service

Comment Service

Reaction Service

Bookmark Service

Collection Service

Messaging Service

Notification Service

Creator Service

Business Service

Advertising Service

Commerce Service

Analytics Service

Moderation Service

Spam Detection Service

Trust & Safety Service

Audit Service

Feature Flag Service

Administration Service

Developer Platform Service

────────────────────────────────────────

API GATEWAY

Implement:

• API routing

• Request validation

• Authentication integration

• Authorization integration

• Rate limiting

• Request IDs

• Correlation IDs

• Structured request logging

• API versioning

• Pagination standards

• Filtering

• Sorting

• Error normalization

• OpenAPI aggregation where applicable

• Health endpoints

• Readiness endpoints

• Liveness endpoints

────────────────────────────────────────

AUTHENTICATION

Implement:

• Registration

• Login

• Logout

• Email verification

• Password hashing

• Password reset

• JWT access tokens

• Refresh tokens

• Token rotation

• Token revocation

• Session management

• Device management

• OAuth integration architecture

• Multi-factor authentication readiness

• Passkey readiness

• Suspicious login detection

• Rate limiting

• Account lockout policies

• Secure recovery flows

Never store sensitive credentials in plaintext.

────────────────────────────────────────

AUTHORIZATION

Implement:

• RBAC

• Resource ownership checks

• Role permissions

• Creator permissions

• Business permissions

• Advertiser permissions

• Moderator permissions

• Administrator permissions

• Service-to-service authorization

• API scopes

• Permission caching where appropriate

Design interfaces that can support future ABAC expansion.

────────────────────────────────────────

USER AND PROFILE DOMAIN

Implement:

• User creation

• User lifecycle management

• Profile management

• Usernames

• Display names

• Bios

• Avatars

• Websites

• Professional profiles

• Creator profiles

• Business profiles

• Verification states

• Privacy settings

• Account visibility

• Account deletion

• Account recovery

• Username changes

• Profile metadata

• Privacy enforcement

────────────────────────────────────────

SOCIAL GRAPH

Implement:

• Follow requests

• Following

• Followers

• Follow approvals

• Follow removal

• Blocked users

• Muted users

• Close Friends

• Relationship queries

• Follower counts

• Following counts

• Relationship state caching

• Privacy-aware graph queries

• Event publication

Optimize for high-volume reads and writes.

────────────────────────────────────────

POSTS

Implement:

• Create posts

• Draft posts

• Scheduled posts

• Publish posts

• Edit posts

• Delete posts

• Soft deletion

• Content visibility

• Public posts

• Followers-only posts

• Private-account enforcement

• Carousel posts

• Media attachments

• Captions

• Mentions

• Tags

• Hashtags

• Location metadata

• Collaboration support

• Branded content metadata

• Post analytics hooks

────────────────────────────────────────

MEDIA SERVICE

Implement:

• Media upload initialization

• Signed upload URLs

• Upload completion verification

• Media ownership validation

• Media metadata

• Media lifecycle states

• Signed download URLs

• Access control

• CDN-ready delivery URLs

• Deletion workflows

• Lifecycle events

• Retry-safe processing

Support:

• Images

• Videos

• Audio

• GIFs

• Documents where approved

────────────────────────────────────────

IMAGE PROCESSING

Implement asynchronous workers for:

• Image validation

• File type verification

• Metadata extraction

• EXIF processing

• Orientation correction

• Image resizing

• Responsive variants

• Thumbnail generation

• Compression

• Optimization

• Malware scanning integration points

• Content moderation integration points

• Processing status tracking

• Retry policies

• Dead-letter handling

────────────────────────────────────────

VIDEO PROCESSING

Implement:

• Video validation

• Metadata extraction

• Duration detection

• Resolution detection

• Transcoding pipeline

• Multiple quality variants

• Thumbnail generation

• Preview generation

• Audio extraction where required

• Processing status tracking

• Retry policies

• Idempotent processing

• Dead-letter handling

Prepare contracts for adaptive streaming delivery.

────────────────────────────────────────

STORIES

Implement:

• Story creation

• Story publishing

• Story expiration

• Viewer tracking

• Close Friends visibility

• Replies

• Reactions

• Story deletion

• Story archive readiness

• Story analytics

• Scheduled expiration workers

• Idempotent expiration handling

────────────────────────────────────────

HIGHLIGHTS

Implement:

• Highlight collections

• Story selection

• Ordering

• Cover images

• Visibility rules

• Update operations

• Deletion

────────────────────────────────────────

REELS

Implement:

• Reel creation

• Video processing integration

• Audio metadata

• Captions

• Hashtags

• Mentions

• Publishing

• Editing

• Deletion

• Visibility controls

• Engagement tracking

• Recommendation events

• View tracking

• Completion metrics

────────────────────────────────────────

FEED SERVICE

Implement architecture and production-ready logic for:

• Home Feed

• Following Feed

• Creator Feed

• Hashtag Feed

• Location Feed

• Trending Feed

• Sponsored Feed integration points

Support:

• Cursor pagination

• Feed caching

• Candidate generation

• Ranking integration

• Fanout-on-write where appropriate

• Fanout-on-read where appropriate

• Hybrid feed strategies

• Feed invalidation

• Privacy filtering

• Block filtering

• Mute filtering

• Deduplication

• Content availability checks

Design the implementation so ranking models can evolve without rewriting the entire feed system.

────────────────────────────────────────

RECOMMENDATION SERVICE

Implement interfaces and services for:

• Candidate generation

• Content ranking

• Creator recommendations

• User recommendations

• Explore recommendations

• Interest signals

• Engagement signals

• Trending signals

• Real-time signals

• Batch-generated recommendations

• Recommendation caching

• Experiment integration

• Feature flag integration

• Recommendation event tracking

Prepare clean interfaces for future ML inference services and feature stores.

────────────────────────────────────────

HASHTAGS

Implement:

• Hashtag extraction

• Normalization

• Validation

• Trending calculations

• Hashtag pages

• Associated content

• Search indexing events

• Popularity metrics

• Abuse controls

────────────────────────────────────────

COMMENTS

Implement:

• Create comments

• Replies

• Threaded replies

• Edit comments

• Delete comments

• Soft deletion

• Mentions

• Reactions where approved

• Pagination

• Moderation states

• Reporting

• Spam controls

• Privacy enforcement

────────────────────────────────────────

REACTIONS

Implement:

• Likes

• Reactions where supported

• Idempotent creation

• Idempotent removal

• Aggregate counters

• Event publication

• Abuse protection

• High-write-volume optimization

────────────────────────────────────────

BOOKMARKS AND COLLECTIONS

Implement:

• Save posts

• Remove saved posts

• Private bookmarks

• Collections

• Create collections

• Rename collections

• Delete collections

• Add content

• Remove content

• Pagination

────────────────────────────────────────

MESSAGING

Implement according to the approved architecture:

• One-to-one conversations

• Group conversations

• Conversation membership

• Messages

• Media messages

• Voice message support

• GIFs

• Stickers

• Emoji reactions

• Typing indicators

• Read receipts

• Delivery states

• Presence integration

• Message pagination

• Message search

• Real-time delivery

• Offline synchronization

• Retry-safe delivery

• Connection recovery

Maintain clear boundaries so advanced messaging features can evolve independently.

────────────────────────────────────────

REAL-TIME ARCHITECTURE

Implement Socket.IO or approved WebSocket architecture supporting:

• Authentication

• Connection lifecycle

• Connection recovery

• Room management

• Presence

• Typing indicators

• Message delivery

• Notification delivery

• Live engagement events

• Rate limits

• Heartbeats

• Distributed scaling through Redis or approved adapters

• Connection metrics

• Graceful shutdown

────────────────────────────────────────

NOTIFICATIONS

Implement:

• Notification creation

• Notification preferences

• Push notification jobs

• In-app notifications

• Email notification integration

• Notification aggregation

• Deduplication

• Retry policies

• Deep-link payload generation

• Read/unread state

• Batch delivery

• Quiet preferences

────────────────────────────────────────

SEARCH

Implement Elasticsearch or OpenSearch integration supporting:

• Users

• Creators

• Businesses

• Posts

• Reels

• Hashtags

• Locations

• Audio

Support:

• Full-text search

• Autocomplete

• Suggestions

• Typo tolerance

• Filters

• Personalized ranking hooks

• Trending searches

• Index synchronization

• Event-driven indexing

• Retry handling

• Dead-letter handling

• Index versioning

────────────────────────────────────────

CREATOR PLATFORM

Implement backend capabilities for:

• Creator account management

• Creator verification

• Creator settings

• Creator analytics

• Audience analytics

• Content analytics

• Revenue analytics hooks

• Content scheduling

• Brand partnership workflows

• Campaign participation

• Creator marketplace architecture

• Digital product architecture

• Membership readiness

────────────────────────────────────────

BUSINESS PLATFORM

Implement:

• Business profiles

• Business verification

• Business account management

• Team roles

• Business analytics

• Promotions

• Product catalog integration

• Lead generation hooks

• CRM integration interfaces

────────────────────────────────────────

COMMERCE

Implement approved commerce capabilities for:

• Product catalogs

• Product tagging

• Merchant integrations

• Shopping content

• Inventory synchronization interfaces

• Coupons

• Discounts

• Order integration contracts

• Checkout integration boundaries

Do not couple commerce domain logic directly to the core social graph.

────────────────────────────────────────

ADVERTISING PLATFORM

Implement foundational services for:

• Advertiser accounts

• Campaigns

• Ad groups

• Creative assets

• Targeting definitions

• Budget configuration

• Scheduling

• Sponsored content

• Delivery events

• Impression tracking

• Click tracking

• Conversion event interfaces

• Fraud detection hooks

• Billing integration boundaries

• Performance analytics

Design the architecture to support future auction and real-time bidding systems.

────────────────────────────────────────

ANALYTICS

Implement event collection and aggregation for:

• DAU

• MAU

• Engagement

• Post performance

• Video views

• Video completion

• Story views

• Story completion

• Creator metrics

• Business metrics

• Feed performance

• Recommendation performance

• Search performance

• Notification delivery

• Platform health

Ensure analytics processing does not block transactional user flows.

────────────────────────────────────────

MODERATION

Implement:

• User reporting

• Content reporting

• Review queues

• Moderation states

• Moderator actions

• Content takedown

• Account restrictions

• Appeals

• Automated moderation integration interfaces

• Moderation audit trails

• Escalation workflows

────────────────────────────────────────

SPAM DETECTION AND TRUST & SAFETY

Implement infrastructure and domain logic for:

• Abuse signals

• Spam reports

• Rate-based detection

• Suspicious activity

• Bot detection hooks

• Fake-account signals

• Fraud signals

• Risk scoring interfaces

• Account restrictions

• Automated enforcement hooks

• Manual review escalation

────────────────────────────────────────

FEATURE FLAGS

Implement:

• Flag definitions

• Environment targeting

• User targeting

• Percentage rollouts

• Feature evaluation

• Cached evaluation

• Audit history

• Rollback capability

────────────────────────────────────────

AUDIT

Implement immutable or append-oriented audit records for:

• Administrative actions

• Moderation actions

• Permission changes

• Verification actions

• Sensitive account changes

• Feature flag changes

• Business actions

• Advertising actions

• System events where required

────────────────────────────────────────

EVENT-DRIVEN ARCHITECTURE

Use Kafka or Redpanda according to the approved architecture.

Implement versioned events, producers, consumers, retries, idempotency, dead-letter topics, observability, and failure handling.

Support events including:

UserRegistered

UserLoggedIn

ProfileUpdated

FollowCreated

FollowRemoved

PostCreated

PostEdited

PostDeleted

StoryPublished

StoryExpired

ReelCreated

MediaUploaded

MediaProcessed

ImageProcessed

VideoProcessed

CommentCreated

CommentDeleted

ReactionAdded

ReactionRemoved

BookmarkCreated

BookmarkRemoved

MessageSent

NotificationQueued

CreatorVerified

BusinessVerified

CampaignCreated

AdvertisementDelivered

RecommendationGenerated

ReportSubmitted

ModerationCompleted

AnalyticsUpdated

FeatureFlagUpdated

AuditEventCreated

Do not create consumers that silently discard failures.

────────────────────────────────────────

BACKGROUND WORKERS

Generate production-ready workers for:

• Image processing

• Video processing

• Thumbnail generation

• Media cleanup

• Story expiration

• Scheduled publishing

• Notification delivery

• Search indexing

• Feed maintenance

• Analytics aggregation

• Recommendation generation

• Trending calculations

• Data retention

• Cache invalidation

• Retry processing

• Dead-letter recovery workflows where appropriate

────────────────────────────────────────

REDIS

Implement Redis for:

• Sessions

• Token revocation where required

• Rate limiting

• Distributed locks

• Feed caching

• Recommendation caching

• Relationship caching

• Presence

• WebSocket scaling

• Feature flags

• Idempotency keys where appropriate

• Short-lived analytics counters where appropriate

Define key namespaces, TTL strategies, invalidation policies, and failure behavior.

────────────────────────────────────────

DATABASE

Implement the approved PostgreSQL and Prisma architecture.

Generate:

• Prisma models

• Migrations

• Foreign keys

• Constraints

• Unique indexes

• Composite indexes

• Partial indexes where appropriate

• Partitioning strategies where approved

• Soft-delete patterns where required

• Transaction boundaries

• Concurrency protection

• Optimistic locking where appropriate

Optimize high-volume domains without sacrificing data integrity.

────────────────────────────────────────

API STANDARDS

Implement:

• REST APIs according to approved contracts

• OpenAPI documentation

• DTO validation

• Zod or approved validation where architecturally appropriate

• Consistent pagination

• Cursor pagination for high-volume resources

• Filtering

• Sorting

• API versioning

• Idempotency keys for sensitive write operations

• Consistent error responses

• Correlation IDs

• Rate limiting

• Authorization checks

────────────────────────────────────────

OBSERVABILITY

Implement:

• Structured logging

• Correlation IDs

• Distributed tracing

• OpenTelemetry instrumentation

• Metrics

• Business metrics

• Health checks

• Readiness checks

• Liveness checks

• Database metrics

• Redis metrics

• Kafka metrics

• Queue metrics

• Search metrics

• WebSocket metrics

• Media processing metrics

────────────────────────────────────────

RESILIENCE

Implement:

• Graceful shutdown

• Timeouts

• Retries with backoff

• Circuit breakers where appropriate

• Bulkheads where appropriate

• Idempotent consumers

• Idempotent APIs where required

• Dead-letter queues/topics

• Failure isolation

• Dependency health checks

• Backpressure-aware processing

────────────────────────────────────────

SECURITY

Implement:

• OWASP best practices

• Secure authentication

• Refresh-token rotation

• Authorization enforcement

• Rate limiting

• Input validation

• Output encoding where required

• Secure headers

• CORS

• CSRF protection where applicable

• SQL injection protection

• File validation

• Media type validation

• Upload size limits

• Signed URLs

• Secrets management integration

• Audit logging

• Principle of least privilege

────────────────────────────────────────

TESTING

Generate:

• Unit tests

• Service tests

• Repository tests

• Controller tests

• Integration tests

• Contract tests

• Event producer tests

• Event consumer tests

• Queue worker tests

• Authentication tests

• Authorization tests

• Feed tests

• Recommendation tests

• Search tests

• Media pipeline tests

• Messaging tests

• WebSocket tests

• Performance test architecture

• Security tests

• Load-testing readiness

────────────────────────────────────────

DOCUMENTATION

Generate:

• Backend architecture documentation

• Service documentation

• API documentation

• Event catalog documentation

• Local development guide

• Testing guide

• Authentication guide

• Authorization guide

• Database migration guide

• Operational runbook foundations

────────────────────────────────────────

PROJECT ORGANIZATION

Maintain throughout implementation:

Current Milestone

Generated Files

Completed Services

Completed APIs

Completed Database Objects

Completed Events

Completed Workers

Dependencies

Remaining Work

Next File

────────────────────────────────────────

OUTPUT FORMAT

For every generated file provide:

1. Exact file path
2. Complete file contents

Never generate pseudo-code.

Never generate placeholders.

Never generate TODO comments.

Never omit implementations.

Never say:

• "implement similarly"

• "left as an exercise"

• "for brevity"

• "remaining code omitted"

Every generated file must integrate with previously generated files.

Do not regenerate unchanged files.

Only modify files when required.

────────────────────────────────────────

STOP CONDITIONS

Generate the backend incrementally according to the Master Prompt.

Each milestone should contain approximately 20–40 files.

At the end of every milestone:

• Verify compilation and type consistency.

• Verify integration with previously generated modules.

• Update the project index.

• List completed services.

• List completed APIs.

• List completed database objects.

• List completed events and workers.

• Identify the exact next file or logical implementation unit.

STOP and wait for approval before generating the next milestone.
