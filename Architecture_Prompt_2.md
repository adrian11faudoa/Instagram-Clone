Using the approved Architecture Blueprint — Volume 1 and the Master Prompt above.

Continue Phase 1 architecture.

Do NOT generate implementation code.

Continue from the exact stopping point.

This volume completes the enterprise architecture and becomes the definitive blueprint for Backend, Frontend, Mobile, AI, Infrastructure, Security, DevOps, and Operations.

────────────────────────────────────────

SEARCH PLATFORM

Generate complete architecture for:

• User Search

• Creator Search

• Business Search

• Post Search

• Reels Search

• Stories Search

• Hashtag Search

• Audio Search

• Location Search

• Comment Search

• Semantic Search (future-ready)

• AI Search (future-ready)

Support:

Autocomplete

Trending Searches

Search Suggestions

Typo Tolerance

Geo-aware Ranking

Language-aware Search

Personalized Ranking

Search Analytics

────────────────────────────────────────

MESSAGING

Design architecture supporting:

• One-to-One Chats

• Group Chats

• Creator Channels

• Vanishing Messages

• Voice Messages

• Images

• Videos

• Documents

• GIFs

• Stickers

• Emoji Reactions

• Read Receipts

• Typing Indicators

• Online Presence

• Scheduled Messages

• Message Search

────────────────────────────────────────

NOTIFICATIONS

Generate architecture for:

Push Notifications

In-app Notifications

Email Notifications

SMS Notifications (future-ready)

Creator Alerts

Business Alerts

Follower Alerts

Comment Alerts

Like Alerts

Mention Alerts

Message Alerts

Live Stream Alerts

Marketing Notifications

Notification Preferences

────────────────────────────────────────

LIVE STREAMING

Generate architecture supporting:

Live Broadcast

Multi-host Streaming

Live Chat

Pinned Comments

Moderation Queue

Viewer Analytics

Replay Storage

Recording Pipeline

Adaptive Bitrate Streaming

Low-Latency Delivery

Future Live Commerce

────────────────────────────────────────

CREATOR PLATFORM

Design complete architecture for:

Creator Profiles

Creator Verification

Creator Dashboard

Creator Analytics

Audience Insights

Revenue Analytics

Content Scheduling

Brand Partnerships

Campaign Management

Creator Marketplace

Affiliate Platform

Digital Products

Memberships (future-ready)

────────────────────────────────────────

BUSINESS PLATFORM

Support:

Business Profiles

Business Verification

Business Insights

Advertising

Promotions

Product Catalog

Commerce Integration

Lead Generation

CRM Integrations

Marketing Analytics

────────────────────────────────────────

COMMERCE

Generate architecture supporting:

Product Catalog

Product Tagging

Shopping Posts

Checkout Integration

Order Tracking

Inventory Sync

Coupons

Discount Campaigns

Merchant APIs

Future Marketplace Expansion

────────────────────────────────────────

ADVERTISING PLATFORM

Generate architecture for:

Campaign Management

Audience Segmentation

Budget Management

Auction-ready Design

Ad Delivery

Ad Targeting

Sponsored Posts

Sponsored Stories

Sponsored Reels

Performance Analytics

Billing Integration

Fraud Detection

────────────────────────────────────────

MODERATION

Design architecture supporting:

User Reporting

Content Reporting

Spam Detection

Bot Detection

Fake Account Detection

NSFW Detection

Copyright Detection

Community Moderation

Appeals

Moderator Dashboard

Trust & Safety

────────────────────────────────────────

SECURITY

Generate architecture for:

JWT Authentication

OAuth

Refresh Tokens

Passkeys (future-ready)

Multi-factor Authentication

RBAC

ABAC (future-ready)

Rate Limiting

Fraud Detection

Account Recovery

Device Management

Session Validation

Encryption at Rest

Encryption in Transit

OWASP Compliance

────────────────────────────────────────

ANALYTICS

Generate architecture supporting:

Daily Active Users

Monthly Active Users

Engagement Metrics

Feed Performance

Creator Analytics

Business Analytics

Revenue Metrics

Advertising Metrics

Video Completion Rate

Story Completion Rate

Livestream Metrics

Recommendation Metrics

Platform Health

────────────────────────────────────────

AI PLATFORM

Prepare architecture for:

Recommendation Models

Ranking Models

Vision Models

Content Moderation AI

Semantic Search

Caption Generation

Automatic Hashtags

Creator Assistant

Advertising Optimization

Content Quality Scoring

AI Feature Store

Prompt Management

LLM Gateway

Model Registry

Inference Services

AI Audit Logs

────────────────────────────────────────

EVENT-DRIVEN ARCHITECTURE

Use Kafka (or Redpanda) as the event backbone.

Generate events for:

UserRegistered

ProfileUpdated

FollowCreated

FollowRemoved

PostCreated

PostEdited

PostDeleted

StoryPublished

StoryExpired

ReelUploaded

VideoProcessed

MediaUploaded

MediaProcessed

CommentCreated

CommentDeleted

ReactionAdded

ReactionRemoved

CollectionCreated

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

Generate producers, consumers, retry strategies, dead-letter topics, idempotency rules, and event versioning.

────────────────────────────────────────

DEPLOYMENT ARCHITECTURE

Generate:

Multi-region Kubernetes Topology

Regional API Gateways

Global CDN Architecture

Media Processing Clusters

Background Worker Clusters

Recommendation Clusters

Search Clusters

Analytics Clusters

Disaster Recovery

Zero-downtime Deployment Strategy

Autoscaling Strategy

────────────────────────────────────────

INFRASTRUCTURE OVERVIEW

Design infrastructure for:

Docker

Kubernetes

Helm

Terraform

GitHub Actions

Redis

Kafka

Elasticsearch

PostgreSQL

S3-compatible Storage

CloudFront

Vault

Prometheus

Grafana

Loki

Tempo

OpenTelemetry

────────────────────────────────────────

PHASE 1 REQUIREMENTS

Generate ONLY:

1. Complete Enterprise System Architecture
2. Domain Decomposition
3. Bounded Contexts
4. Service Boundaries
5. Monorepo Structure
6. Folder Hierarchy
7. ERD
8. PostgreSQL Schema
9. Prisma Schema
10. Redis Architecture
11. Kafka Event Catalog
12. Elasticsearch Mappings
13. Queue Architecture
14. API Contracts
15. WebSocket Architecture
16. Authentication Architecture
17. Authorization Model
18. Recommendation Architecture
19. Feed Generation Architecture
20. Media Processing Pipeline
21. Search Architecture
22. Live Streaming Architecture
23. Deployment Architecture
24. Kubernetes Topology
25. Infrastructure Overview
26. Security Architecture
27. AI Platform Architecture
28. Disaster Recovery Strategy
29. Project Index

Do NOT implement backend code.

STOP after Phase 1.

Wait for approval before backend implementation.

────────────────────────────────────────

ARCHITECTURAL DECISIONS

Unless there is a compelling technical reason otherwise, assume:

• NestJS for backend services

• PostgreSQL + Prisma for transactional data

• Redis for caching, sessions, distributed locks, and feed caching

• Kafka (or Redpanda) for event streaming

• BullMQ for asynchronous processing

• Socket.IO for real-time messaging

• Elasticsearch/OpenSearch for search

• AWS S3-compatible storage for media

• CloudFront for CDN

• FFmpeg for video processing

• Sharp for image processing

• Kubernetes for orchestration

• Terraform for Infrastructure as Code

• OpenTelemetry for observability

• Vault for secrets management

• Event-driven communication where appropriate

• CQRS where appropriate

• Clean Architecture

• Domain-Driven Design

• Repository Pattern

• Dependency Injection

Design every architectural decision for long-term scalability, maintainability, resilience, creator monetization, business growth, AI integration, and global deployment.
