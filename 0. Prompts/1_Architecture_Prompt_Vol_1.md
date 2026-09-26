# Instagram — Architecture Prompt — Volume 1

# 1. ROLE

You are the **Principal Architect and senior architecture team** responsible for defining the foundational architecture of the **Instagram** project.

Operate with the combined responsibilities of:

* Principal Architect
* Distributed Systems Architect
* Backend Architect
* Frontend Architect
* Mobile Architect
* Database Architect
* Security Architect
* Cloud Architect
* SRE / Reliability Architect
* Data / Analytics Architect
* Media Systems Architect
* QA Architect
* Technical Writer

This is an **architecture-definition assignment**.

Your responsibility in this prompt is to create a concrete, production-grade architectural blueprint and the portable artifacts required to guide later implementation.

Do **not** implement the complete Instagram application in this task.

Do **not** create the full backend, frontend, mobile application, infrastructure deployment, or complete automated test suite.

Architecture artifacts, schemas, contract definitions, configuration specifications, diagrams, and other documentation explicitly requested by this prompt are in scope.

---

# 2. PROJECT IDENTITY

**Project Name:** Instagram

**Product Type:** Production-grade visual social networking platform.

**Primary Product Model:** A mobile-first social platform centered on user identities, social graphs, photo and video content, stories, short-form video, personalized feeds, discovery, engagement, direct messaging, notifications, moderation, creator/professional capabilities, and large-scale media delivery.

The completed system must be capable of evolving toward approximately:

* 100 million registered accounts;
* 20 million daily active users;
* 2 million peak concurrent active sessions;
* approximately 100,000 sustained API requests per second across the platform;
* approximately 250,000 requests per second during peak edge bursts;
* very high media-ingestion and media-delivery workloads;
* high-fan-out social relationships;
* large-scale realtime interactions;
* geographically distributed traffic;
* multi-region resilience where operationally justified.

These are **architecture targets**, not a requirement to provision or implement the entire target scale during this architecture task.

The architecture must support incremental implementation without forcing premature operational complexity that is not justified by the current system state.

---

# 3. CURRENT ARCHITECTURE ASSIGNMENT

Create the **foundational architecture** for the Instagram platform.

This volume must establish the major system shape, domain boundaries, technology direction, data ownership principles, client/server boundaries, infrastructure boundaries, security boundaries, and cross-part integration model.

The architecture must be concrete enough that independently generated backend, web, mobile, infrastructure, and QA project parts can later implement against the same model.

The architecture must minimize undocumented assumptions.

This volume must establish the foundation for later deep contract artifacts without turning this task into the implementation of the application.

---

# 4. REPOSITORY INSPECTION

If a repository is available in the execution environment:

1. Inspect the repository structure before making architecture decisions that would conflict with what already exists.
2. Inspect package manifests and workspace configuration.
3. Inspect application entry points.
4. Inspect existing backend, frontend, and mobile structures.
5. Inspect database schemas and migrations.
6. Inspect existing API specifications.
7. Inspect existing event or queue definitions.
8. Inspect existing infrastructure-as-code.
9. Inspect configuration conventions.
10. Inspect existing test organization.
11. Inspect existing documentation.
12. Identify implemented architectural decisions that are already materially embedded in the repository.

Treat the repository as the source of truth for what actually exists.

Do not assume that an earlier AI prompt was executed.

Do not assume that another Claude conversation exists.

Do not assume that another AI-generated architecture artifact exists unless it is actually available in the repository or explicitly supplied as input.

If the repository contains an existing architecture, preserve compatible decisions where they are sound and document any necessary architectural correction within this prompt's scope.

If no repository exists, create a portable architecture artifact set that does not depend on repository state.

---

# 5. ARCHITECTURAL OBJECTIVES

The architecture must provide:

* clear bounded domains;
* explicit data ownership;
* scalable request handling;
* safe social-graph operations;
* high-volume media processing;
* reliable feed generation;
* controlled asynchronous processing;
* realtime communication;
* search and discovery;
* notification delivery;
* secure identity management;
* privacy enforcement;
* moderation and abuse controls;
* operational observability;
* graceful degradation;
* disaster recovery foundations;
* cost-aware infrastructure choices;
* coherent web and mobile integration;
* explicit portable contracts;
* evolution and versioning strategies.

The architecture must distinguish:

* authoritative data;
* derived data;
* cached data;
* eventually consistent data;
* ephemeral state;
* asynchronously processed state;
* externally sourced state.

Do not hide these distinctions inside implementation details.

---

# 6. TECHNOLOGY DIRECTION

Use this technology direction as the default architectural baseline unless the repository contains a strong compatibility constraint requiring an equivalent alternative.

## 6.1 Application Language

**TypeScript** is the default language for application services and clients.

The architecture must assume strict typing and shared contract discipline.

## 6.2 Web Application

Use:

**Next.js + React + TypeScript**

The architecture must accommodate:

* server-rendered content where beneficial;
* client-side interactive experiences;
* authenticated application routes;
* responsive layouts;
* content-heavy feeds;
* image/video experiences;
* SEO-relevant public surfaces where applicable;
* caching;
* realtime updates;
* accessibility.

## 6.3 Mobile Application

Use:

**React Native + TypeScript**

The architecture must support:

* iOS;
* Android;
* push notifications;
* media capture/selection;
* uploads;
* realtime communication;
* secure credential storage;
* background processing where platform rules permit;
* offline-aware behavior.

## 6.4 Backend

Use:

**Node.js + TypeScript**

Prefer a structured backend architecture such as:

**NestJS or an equivalent production-grade framework**

The architecture must emphasize domain modularity and clear ownership.

Do not force a large microservice topology solely because the target scale is large.

Use independently deployable services where there is a concrete operational or scaling reason.

Use modular boundaries that can support later decomposition when a modular monolith provides better economics during earlier implementation stages.

## 6.5 Primary Database

Use:

**PostgreSQL**

PostgreSQL is the primary transactional source of truth for relational business data where appropriate.

## 6.6 Cache

Use:

**Redis**

Redis may support:

* caching;
* rate limiting;
* ephemeral state;
* distributed coordination;
* selected counters;
* session-related state where appropriate.

Redis must not silently replace authoritative persistent storage.

## 6.7 Event Streaming

Use:

**Kafka or a compatible durable event-streaming platform**

Use event streaming for high-volume asynchronous domain propagation where event semantics are justified.

## 6.8 Background Jobs

Use a durable job-queue mechanism appropriate for:

* media processing;
* notification delivery;
* cleanup;
* moderation processing;
* feed work;
* search indexing;
* analytics aggregation;
* reconciliation;
* other asynchronous execution.

The architecture must distinguish event streams from work queues.

## 6.9 Search

Use:

**OpenSearch or an equivalent search engine**

Search indexing must remain derived from authoritative data.

## 6.10 Object Storage

Use:

**Amazon S3 or an equivalent production object-storage service**

Media must not be stored directly in the primary relational database unless an explicit architectural exception is justified.

## 6.11 CDN

Use:

**CloudFront or an equivalent CDN**

Media delivery must be designed around CDN-first serving patterns.

## 6.12 Media Processing

Use:

**FFmpeg or an equivalent production media-processing system**

The architecture must support asynchronous image/video processing.

## 6.13 Cloud

Use:

**AWS**

Prefer managed AWS services where they materially reduce operational burden without creating unreasonable cost or lock-in.

---

# 7. SYSTEM ARCHITECTURE MODEL

Define a coherent high-level architecture using the following conceptual layers.

## 7.1 Edge Layer

Define responsibilities for:

* DNS;
* TLS termination;
* CDN;
* edge caching;
* WAF;
* bot/abuse controls where appropriate;
* request routing;
* public media delivery.

Do not place application business logic into the edge layer unless there is a clear reason.

## 7.2 API / Gateway Layer

Define responsibilities for:

* request routing;
* authentication propagation;
* rate limiting;
* request correlation;
* API versioning;
* input validation boundaries;
* authorization-context propagation;
* response/error standards.

The architecture must distinguish externally exposed APIs from internal service communication.

## 7.3 Application / Domain Layer

Define bounded domains and their ownership.

The architecture must specify whether each domain is:

* a module;
* a separately deployable service;
* a shared platform subsystem.

Do not leave service/module boundaries vague.

## 7.4 Data Layer

Define:

* authoritative stores;
* derived stores;
* caches;
* indexes;
* media stores;
* analytical stores where applicable;
* event streams;
* background-job state.

## 7.5 Asynchronous Layer

Define the interaction between:

* event streaming;
* job queues;
* workers;
* scheduled tasks;
* retry infrastructure;
* dead-letter handling.

## 7.6 Client Layer

Define:

* web application boundaries;
* mobile application boundaries;
* shared domain contracts;
* authentication integration;
* media upload integration;
* realtime integration;
* notification integration.

## 7.7 Operational Layer

Define:

* observability;
* configuration;
* secrets;
* deployment;
* health checking;
* alerts;
* backups;
* disaster recovery.

---

# 8. DOMAIN BOUNDARIES

Establish explicit bounded domains.

At minimum evaluate the following domains:

1. Identity and Authentication
2. Account and Profile
3. Social Graph
4. Content / Posts
5. Stories
6. Short-Form Video
7. Engagement
8. Feed
9. Discovery / Search
10. Direct Messaging
11. Notifications
12. Media
13. Moderation / Trust and Safety
14. Administration
15. Analytics
16. Configuration / Platform Operations

For each domain, define:

* domain purpose;
* owned entities;
* authoritative data;
* external consumers;
* APIs exposed;
* events published;
* events consumed;
* background jobs owned;
* cache responsibilities;
* security boundary;
* privacy boundary;
* scaling characteristics;
* consistency requirements;
* failure isolation expectations.

Do not create duplicate ownership of the same authoritative entity across unrelated domains.

---

# 9. DATA OWNERSHIP MODEL

Create an explicit data ownership matrix.

At minimum document ownership for entities such as:

* User;
* Account;
* Profile;
* Session;
* Device;
* FollowRelationship;
* FollowRequest;
* BlockRelationship;
* MuteRelationship;
* Restriction;
* Post;
* PostMedia;
* Story;
* StoryItem;
* ShortVideo;
* Comment;
* CommentReply;
* Like;
* Save;
* Share;
* Hashtag;
* Mention;
* FeedEntry;
* Conversation;
* ConversationParticipant;
* Message;
* MessageAttachment;
* Notification;
* MediaAsset;
* MediaDerivative;
* Report;
* ModerationCase;
* AdministrativeAction;
* AnalyticsEvent.

The architecture must distinguish:

* primary ownership;
* read models;
* denormalized projections;
* caches;
* indexes;
* analytics copies.

A derived copy must never be confused with authoritative ownership.

---

# 10. PRIMARY REQUEST FLOWS

Define architecture-level flows for at least:

## 10.1 Account Creation

Cover:

* registration;
* validation;
* identity creation;
* credential setup;
* initial profile creation;
* verification;
* session issuance;
* anti-abuse controls.

## 10.2 Login

Cover:

* credential verification;
* rate limiting;
* session/device state;
* access credentials;
* refresh/rotation;
* security events.

## 10.3 Follow

Cover:

* public-account follow;
* private-account follow request;
* authorization;
* graph persistence;
* graph projection;
* notifications;
* feed consequences.

## 10.4 Create Post

Cover:

* media upload;
* metadata;
* validation;
* processing;
* publication state;
* persistence;
* indexing;
* feed propagation;
* notifications;
* moderation.

## 10.5 Story Publication

Cover:

* upload;
* processing;
* visibility;
* expiration;
* viewer authorization;
* view tracking;
* cleanup.

## 10.6 Short-Form Video Publication

Cover:

* ingest;
* transcoding;
* derivatives;
* moderation;
* publication;
* recommendation eligibility;
* CDN delivery.

## 10.7 Feed Read

Cover:

* viewer authorization;
* candidate sources;
* ranking;
* filtering;
* blocked/muted/private content;
* pagination;
* caching;
* consistency.

## 10.8 Engagement

Cover:

* like;
* comment;
* save;
* share;
* notification generation;
* counter updates;
* idempotency;
* duplicate requests.

## 10.9 Direct Message

Cover:

* conversation authorization;
* message persistence;
* event publication;
* realtime delivery;
* acknowledgement;
* read state;
* notifications;
* offline reconnect.

## 10.10 Media Access

Cover:

* authorization;
* CDN;
* signed access where appropriate;
* caching;
* expiration;
* deletion propagation.

Each flow must identify:

* synchronous operations;
* asynchronous operations;
* authoritative writes;
* derived writes;
* failure boundaries;
* retries;
* user-visible consistency.

---

# 11. SOCIAL GRAPH ARCHITECTURE

Define how the architecture supports high-volume:

* follows;
* follower lists;
* following lists;
* private-account requests;
* blocks;
* mutes;
* restrictions.

Address:

* high-degree users;
* celebrity accounts;
* hot partitions;
* graph reads;
* relationship checks;
* cache strategy;
* fan-out;
* pagination;
* consistency;
* deletion;
* privacy propagation.

Explicitly document how a graph relationship affects authorization and content eligibility.

---

# 12. FEED ARCHITECTURE

Define a scalable feed architecture.

Evaluate and document:

* fan-out-on-write;
* fan-out-on-read;
* hybrid fan-out;
* candidate stores;
* ranking services/modules;
* content eligibility;
* freshness;
* personalization inputs;
* high-fan-out accounts;
* feed caching;
* cursor pagination;
* deduplication;
* stale entry handling;
* deletion propagation;
* privacy filtering;
* blocked/muted relationship filtering.

The architecture must explicitly prevent a feed cache from becoming an authorization bypass.

Define the authoritative source for feed eligibility.

Define where ranking occurs.

Define where feed candidates are materialized.

Define what must happen synchronously versus asynchronously.

---

# 13. DISCOVERY AND SEARCH ARCHITECTURE

Define architecture for:

* user search;
* username search;
* hashtag search;
* content search;
* search suggestions;
* discovery feeds;
* recommended accounts;
* recommended content.

Define:

* source of truth;
* indexing pipeline;
* index schemas at a high level;
* indexing events;
* deletion propagation;
* reindexing;
* eventual-consistency expectations;
* search availability behavior;
* ranking responsibilities.

Search indexes must remain derived representations.

---

# 14. MEDIA ARCHITECTURE

Define a complete media lifecycle:

**upload → validation → security checks → metadata extraction → processing → derivatives → storage → publication → CDN delivery → retention/deletion**

Architectural requirements must cover:

* direct/pre-signed uploads;
* object naming;
* object ownership;
* metadata;
* file-size constraints;
* MIME validation;
* image dimensions;
* video duration;
* transcoding;
* thumbnail generation;
* derivative relationships;
* processing state;
* processing retries;
* failed processing;
* moderation integration;
* malware/security scanning;
* EXIF/privacy handling;
* CDN distribution;
* signed delivery where appropriate;
* deletion propagation;
* lifecycle expiration;
* media quotas.

Define the distinction between:

* original asset;
* processed asset;
* derivative asset;
* public delivery representation;
* metadata record.

---

# 15. STORIES ARCHITECTURE

Define story lifecycle semantics.

At minimum establish:

* story creation;
* story item ordering;
* expiration timestamp;
* visibility;
* audience authorization;
* views;
* interactions;
* replies where supported;
* deletion;
* expiration processing;
* cleanup;
* cache invalidation;
* search/index exclusion.

Expiration must be enforced by server-side state and asynchronous cleanup rather than relying exclusively on client timers.

---

# 16. DIRECT MESSAGING ARCHITECTURE

Establish the architecture for:

* one-to-one conversations;
* group conversations;
* participant membership;
* message persistence;
* attachments;
* delivery state;
* read state;
* realtime delivery;
* typing signals;
* presence where applicable;
* reconnect;
* offline synchronization;
* message pagination;
* notification interaction;
* block/restriction behavior;
* reporting.

Define:

* source of truth;
* transport;
* event model;
* storage;
* connection ownership;
* retry semantics;
* ordering requirements;
* idempotency;
* synchronization strategy.

Do not treat WebSocket delivery as durable persistence.

---

# 17. NOTIFICATION ARCHITECTURE

Define the architecture for:

* in-app notifications;
* push notifications;
* notification preferences;
* read/unread state;
* deduplication;
* aggregation;
* priority;
* retry;
* failure isolation;
* deep linking.

Notification delivery must not make core user-facing writes dependent on successful downstream push delivery.

Define the event-to-notification pipeline.

---

# 18. AUTHENTICATION ARCHITECTURE

Define the authentication architecture at a system level.

Cover:

* registration;
* login;
* password recovery;
* verification;
* session lifecycle;
* refresh rotation;
* device/session management;
* logout;
* credential revocation;
* multi-factor authentication capability;
* suspicious login detection boundaries;
* security-event generation.

Define which components:

* authenticate;
* issue credentials;
* validate credentials;
* revoke sessions;
* own security state.

Do not leave authentication ownership ambiguous.

---

# 19. AUTHORIZATION AND PRIVACY ARCHITECTURE

Define explicit authorization boundaries for:

* account access;
* profile access;
* public/private content;
* stories;
* posts;
* messages;
* media;
* moderation tools;
* administrative tools.

Define the policy inputs required for a request, including as appropriate:

* authenticated principal;
* resource ownership;
* relationship state;
* account privacy;
* content visibility;
* block status;
* restriction state;
* moderation state;
* administrative role.

Authorization must be enforced server-side.

The architecture must prevent cached or derived data from bypassing authorization.

---

# 20. MODERATION AND TRUST & SAFETY ARCHITECTURE

Define boundaries for:

* user reports;
* content reports;
* automated moderation;
* human moderation;
* moderation queues;
* account restrictions;
* content removal;
* appeals where applicable;
* abuse rate controls;
* audit records.

Define:

* moderation state ownership;
* evidence storage;
* decision recording;
* enforcement propagation;
* client visibility;
* administrative authorization.

Do not treat moderation as an afterthought.

---

# 21. ADMINISTRATION ARCHITECTURE

Define a separate administrative control plane or clearly isolated administrative boundary.

Cover:

* administrative authentication;
* role-based access;
* permissions;
* audit logging;
* moderation actions;
* account actions;
* content actions;
* operational diagnostics;
* security controls.

Administrative capabilities must not be exposed through ordinary user authorization paths.

---

# 22. ANALYTICS ARCHITECTURE

Define the architectural separation between:

* operational observability;
* product analytics;
* security/audit events;
* moderation signals.

Establish:

* event ownership;
* event collection;
* ingestion;
* asynchronous processing;
* retention;
* privacy;
* identifiers;
* timestamp semantics;
* downstream analytics consumers.

Avoid coupling critical application paths to synchronous analytics processing.

---

# 23. ASYNCHRONOUS ARCHITECTURE

Create an initial asynchronous workload matrix covering:

* media processing;
* feed propagation;
* search indexing;
* notification generation;
* push notification delivery;
* analytics processing;
* moderation processing;
* story expiration;
* cleanup;
* recommendation computation;
* counter reconciliation;
* data repair/reconciliation.

For each workload define:

* event versus job;
* producer;
* consumer/worker;
* payload responsibility;
* retry approach;
* idempotency requirement;
* ordering requirement;
* failure handling;
* dead-letter strategy;
* observability.

---

# 24. CACHE ARCHITECTURE

Define Redis/cache responsibilities explicitly.

At minimum consider caches for:

* session-related ephemeral state;
* profile reads where justified;
* relationship lookups;
* feed data;
* rate limiting;
* short-lived authorization-related lookups;
* notification counts;
* ephemeral realtime state.

For each major cache class define:

* key namespace;
* conceptual key format;
* TTL category;
* invalidation trigger;
* source of truth;
* acceptable staleness;
* failure behavior.

Do not make cache failure equivalent to database failure.

---

# 25. DATA CONSISTENCY MODEL

Define where the system uses:

* strong consistency;
* transactional consistency;
* read-after-write expectations;
* eventual consistency;
* asynchronous projection;
* best-effort counters.

At minimum evaluate:

* identity;
* relationships;
* account privacy;
* content visibility;
* messages;
* notifications;
* feed entries;
* engagement counters;
* search indexes;
* analytics.

Document user-visible consequences of eventual consistency.

---

# 26. FAILURE AND DEGRADATION MODEL

For the major domains, define what happens when:

* PostgreSQL is unavailable;
* Redis is unavailable;
* Kafka/event streaming is unavailable;
* background workers are unavailable;
* search is unavailable;
* object storage is unavailable;
* CDN/origin delivery is degraded;
* push notification services fail;
* media processing fails;
* one internal service is slow;
* one internal service is unavailable.

For each major dependency identify:

* timeout;
* retry policy;
* fallback;
* degraded behavior;
* queueing;
* user-visible impact;
* recovery behavior.

Do not prescribe retries without considering duplicate side effects.

---

# 27. SECURITY ARCHITECTURE

Create a high-level threat-oriented security architecture covering:

* identity;
* authentication;
* authorization;
* session security;
* credential protection;
* API abuse;
* rate limiting;
* media uploads;
* file validation;
* SSRF;
* injection;
* XSS;
* CSRF where applicable;
* account takeover;
* credential stuffing;
* malicious automation;
* message abuse;
* privacy leakage;
* administrative abuse;
* secret handling;
* service-to-service trust;
* supply-chain risk.

Define security boundaries between:

* public internet;
* edge;
* client applications;
* API layer;
* internal services/modules;
* databases;
* queues;
* object storage;
* administrative plane;
* observability systems.

---

# 28. PRIVACY ARCHITECTURE

Define privacy-sensitive data categories and their boundaries.

At minimum evaluate:

* authentication information;
* profile information;
* relationship data;
* private content;
* messages;
* media metadata;
* device data;
* IP/network information;
* audit data;
* analytics data.

Establish architectural principles for:

* minimization;
* retention;
* deletion;
* account deletion;
* content deletion;
* private-account enforcement;
* access control;
* cache invalidation;
* search deletion;
* media deletion;
* analytics retention.

---

# 29. DATABASE ARCHITECTURE

Create the relational database architecture at the entity and boundary level.

Define:

* database ownership;
* major tables/entities;
* relationships;
* transaction boundaries;
* indexing categories;
* uniqueness constraints;
* high-write entities;
* high-read entities;
* high-cardinality relationships;
* partitioning candidates;
* archival/retention candidates;
* replication/read-scaling strategy;
* migration strategy.

Do not produce a superficial entity list.

Explain why data belongs together or separately.

Identify workloads likely to become hot spots.

---

# 30. HIGH-SCALE DATA STRATEGY

Evaluate architecture for:

* social graph growth;
* follower/following fan-out;
* post volume;
* comments;
* likes;
* message volume;
* notification volume;
* feed entries;
* media metadata;
* video processing metadata.

Consider:

* read replicas;
* partitioning;
* sharding boundaries;
* denormalization;
* materialized projections;
* write amplification;
* hot-row avoidance;
* counter strategies;
* asynchronous aggregation.

Do not introduce sharding everywhere by default.

Define the conditions under which additional horizontal scaling mechanisms become necessary.

---

# 31. IDENTIFIER AND TIME MODEL

Define the initial project-wide model for:

* primary identifiers;
* public identifiers;
* idempotency keys;
* correlation/request IDs;
* event IDs;
* message IDs;
* media IDs;
* pagination cursors;
* timestamps.

The model must support distributed processing.

Use timezone-aware server timestamps.

Define:

* createdAt;
* updatedAt;
* deletedAt;
* publishedAt;
* expiresAt;
* processedAt;
* event timestamp semantics.

The architecture must not allow different domains to invent incompatible identifier or timestamp semantics.

---

# 32. API ARCHITECTURE

Define the API organization at an architectural level.

Establish:

* REST conventions;
* resource naming;
* route grouping;
* versioning;
* authentication boundary;
* authorization boundary;
* validation boundary;
* pagination convention;
* error convention;
* idempotency convention;
* request correlation;
* rate-limit representation.

Identify major API domains, including:

* authentication;
* profiles;
* relationships;
* posts;
* stories;
* reels/short video;
* feed;
* discovery;
* comments;
* saves;
* messaging;
* notifications;
* media;
* moderation;
* administration.

Do not need to specify every endpoint in this volume.

The goal is to establish the API architecture, ownership, conventions, and boundary model.

---

# 33. REALTIME ARCHITECTURE

Define the realtime architecture for:

* messaging;
* delivery acknowledgements;
* read state;
* typing;
* presence where justified;
* notification updates;
* feed updates where justified;
* story-related realtime interactions where applicable.

Establish:

* connection authentication;
* authorization;
* transport;
* connection lifecycle;
* heartbeats;
* reconnect;
* event envelope;
* event sequencing;
* duplicate handling;
* horizontal scaling;
* fan-out;
* persistence boundary.

Realtime events must not replace authoritative persistence.

---

# 34. EXTERNAL SERVICE BOUNDARIES

Define integration boundaries for potential external services.

Include, where applicable:

* email;
* SMS;
* push notifications;
* cloud storage;
* CDN;
* moderation systems;
* search infrastructure;
* observability platforms;
* analytics systems.

For each class of external service define:

* application boundary;
* provider dependency;
* failure behavior;
* timeout behavior;
* retry behavior;
* secret/configuration boundary;
* data privacy considerations.

Do not claim a specific provider is already provisioned.

---

# 35. ENVIRONMENT MODEL

Define conceptual environments:

* local;
* test;
* development;
* staging;
* production.

Establish configuration categories for:

* database;
* Redis;
* event streaming;
* queues;
* storage;
* CDN;
* authentication;
* external services;
* observability;
* feature flags.

Separate:

* configuration;
* secrets;
* runtime-generated state;
* infrastructure state.

Never include real secrets.

---

# 36. DEPLOYMENT TOPOLOGY

Create a high-level deployment topology covering:

* edge;
* web;
* API;
* workers;
* realtime;
* databases;
* Redis;
* event streaming;
* queues;
* object storage;
* CDN;
* search;
* observability;
* administrative surfaces.

The deployment design must identify:

* public versus private components;
* trust boundaries;
* network boundaries;
* scaling boundaries;
* stateful versus stateless components;
* failure domains.

Do not claim actual cloud provisioning.

---

# 37. SCALABILITY MODEL

For each major subsystem, classify its dominant scaling dimension:

* requests per second;
* concurrent connections;
* writes per second;
* reads per second;
* storage;
* bandwidth;
* fan-out;
* background throughput;
* search volume;
* media-processing throughput.

Identify likely bottlenecks for:

* social graph;
* feed;
* messaging;
* notifications;
* media;
* search;
* database;
* cache;
* event systems.

Define architectural scaling mechanisms without prematurely implementing every future optimization.

---

# 38. AVAILABILITY MODEL

Define target availability classes for major capabilities.

Distinguish between:

* critical identity operations;
* core content reads;
* content publication;
* feed;
* messaging;
* notifications;
* search/discovery;
* media processing;
* analytics;
* administration.

For each class identify:

* availability expectation;
* graceful degradation;
* recovery priority;
* dependency sensitivity.

Do not invent unsupported numeric SLOs where the repository or project requirements do not provide enough information; use explicit provisional targets where necessary and label them as architectural targets.

---

# 39. DISASTER RECOVERY MODEL

Define the architecture for:

* PostgreSQL backups;
* point-in-time restoration where appropriate;
* object-storage durability;
* media recovery;
* queue/event recovery;
* configuration recovery;
* infrastructure recovery;
* regional failure;
* data corruption.

Establish:

* recovery priorities;
* restoration dependencies;
* data-loss considerations;
* recovery ordering.

Do not claim that disaster recovery has been tested in this architecture task.

---

# 40. OBSERVABILITY ARCHITECTURE

Define observability boundaries for:

* edge;
* API;
* domain services/modules;
* database;
* Redis;
* event streaming;
* workers;
* realtime infrastructure;
* search;
* media processing;
* object storage;
* CDN.

Establish concepts for:

* logs;
* metrics;
* traces;
* correlation IDs;
* error tracking;
* health;
* readiness;
* liveness;
* queue depth;
* processing latency;
* API latency;
* database performance;
* cache performance.

Include privacy requirements for telemetry.

---

# 41. DOCUMENTATION ARTIFACTS TO CREATE

Create a portable architecture document set.

At minimum produce:

1. `docs/architecture/01-system-context.md`
2. `docs/architecture/02-system-architecture.md`
3. `docs/architecture/03-domain-boundaries.md`
4. `docs/architecture/04-data-ownership.md`
5. `docs/architecture/05-client-architecture.md`
6. `docs/architecture/06-api-architecture.md`
7. `docs/architecture/07-data-architecture.md`
8. `docs/architecture/08-cache-architecture.md`
9. `docs/architecture/09-event-and-async-architecture.md`
10. `docs/architecture/10-realtime-architecture.md`
11. `docs/architecture/11-media-architecture.md`
12. `docs/architecture/12-feed-and-discovery-architecture.md`
13. `docs/architecture/13-security-architecture.md`
14. `docs/architecture/14-privacy-architecture.md`
15. `docs/architecture/15-moderation-and-admin-architecture.md`
16. `docs/architecture/16-infrastructure-topology.md`
17. `docs/architecture/17-scalability-and-reliability.md`
18. `docs/architecture/18-disaster-recovery.md`
19. `docs/architecture/19-observability-architecture.md`
20. `docs/architecture/20-architecture-decisions.md`

You may add additional architecture artifacts when required by the actual system design, but do not create decorative documents with no engineering value.

---

# 42. ARCHITECTURE DIAGRAMS

Create diagrams where they materially improve understanding.

At minimum include diagrams for:

* system context;
* major component/container architecture;
* domain boundaries;
* primary data flow;
* media pipeline;
* feed pipeline;
* direct-messaging flow;
* asynchronous event/job topology;
* deployment topology.

Use a portable diagram representation such as Mermaid where appropriate.

Diagrams must correspond to the written architecture.

Do not create diagrams that contradict the architectural documents.

---

# 43. ARCHITECTURE DECISION RECORDS

Create ADRs or equivalent decision documentation for major decisions such as:

* modular monolith versus independently deployable services;
* PostgreSQL as transactional source of truth;
* Redis responsibilities;
* event-streaming strategy;
* queue strategy;
* object storage and CDN;
* media processing architecture;
* feed architecture;
* search architecture;
* realtime architecture;
* identifier strategy;
* consistency model;
* infrastructure direction.

Each decision should include:

* context;
* decision;
* alternatives considered;
* consequences;
* operational implications;
* scaling implications;
* security implications.

Do not fabricate historical discussions.

Document decisions as architectural decisions made for this project.

---

# 44. PORTABLE INTEGRATION CONTRACT

Create:

`docs/architecture/21-cross-part-integration-contract.md`

This artifact is especially important.

It must provide a concise authoritative map containing:

* domains;
* domain owners;
* major entities;
* identifier conventions;
* timestamp conventions;
* API conventions;
* error conventions;
* pagination;
* authentication boundaries;
* authorization boundaries;
* event naming rules;
* queue naming rules;
* media object conventions;
* configuration conventions;
* environment variable naming principles;
* service/module naming;
* compatibility requirements;
* versioning rules;
* realtime envelope principles;
* observability conventions.

The artifact must be usable by independently generated implementation prompts as a portable contract.

It must not rely on an earlier AI conversation.

---

# 45. REQUIREMENT-TO-ARCHITECTURE COVERAGE

Create:

`docs/architecture/22-requirement-coverage-map.md`

Map the major product requirements to their architectural destinations.

At minimum cover:

* accounts;
* authentication;
* profiles;
* social graph;
* posts;
* stories;
* short-form video;
* engagement;
* feed;
* discovery;
* direct messaging;
* notifications;
* media;
* moderation;
* administration;
* analytics;
* security;
* privacy;
* observability;
* reliability;
* deployment;
* disaster recovery.

For each requirement document:

* owning domain;
* primary data owner;
* primary API boundary;
* major asynchronous dependencies;
* major client consumers;
* major operational concerns.

This map is architectural traceability, not a request to implement the features now.

---

# 46. OUT OF SCOPE

The following are explicitly out of scope for this architecture volume:

* complete backend implementation;
* complete web implementation;
* complete mobile implementation;
* full database migrations;
* production cloud provisioning;
* deployment of live infrastructure;
* complete media-processing implementation;
* complete search implementation;
* complete ranking implementation;
* complete messaging implementation;
* complete notification implementation;
* full moderation implementation;
* full QA implementation;
* comprehensive load testing;
* live third-party account setup;
* production credentials;
* production secrets.

Creating architecture documentation or schemas that define these systems is in scope.

Implementing their complete runtime behavior is not.

---

# 47. NO FAKE IMPLEMENTATION

Do not:

* create fake APIs as substitutes for architecture;
* create fake persistence;
* create dummy services;
* create hardcoded credentials;
* create placeholder production infrastructure;
* claim external systems are operational;
* claim successful cloud deployment;
* claim load-test results;
* claim integration validation that was not performed.

Architecture artifacts must describe intended architecture honestly.

---

# 48. SECURITY REQUIREMENTS FOR THIS ARCHITECTURE TASK

All architecture artifacts must:

* avoid secrets;
* avoid credentials;
* avoid sensitive production endpoints;
* define least-privilege boundaries;
* define authentication and authorization ownership;
* identify trust boundaries;
* identify high-risk interfaces;
* identify media-security boundaries;
* identify administrative security boundaries;
* identify sensitive-data flows.

Do not place secrets in diagrams, examples, configuration samples, or documentation.

---

# 49. CONSISTENCY REQUIREMENTS

Use one consistent terminology system across every architecture artifact.

The following concepts must not be renamed casually:

* User
* Account
* Profile
* Post
* Story
* Short Video
* Follow Relationship
* Conversation
* Message
* Notification
* Media Asset
* Feed
* Discovery
* Moderation Case

Where the exact terminology requires refinement, establish the canonical term in the architecture and use it consistently thereafter.

Do not create multiple names for the same domain entity.

---

# 50. VALIDATION OF ARCHITECTURE

Before declaring the architecture volume complete, perform an internal consistency audit.

Verify that:

* every major domain has an owner;
* every major durable entity has an owner;
* authoritative versus derived data is identified;
* APIs have clear domain ownership;
* asynchronous workloads have a defined mechanism;
* realtime responsibilities are defined;
* media ownership is explicit;
* feed architecture respects privacy;
* search remains derived;
* notifications are decoupled from critical writes;
* cache ownership is explicit;
* authentication ownership is explicit;
* authorization boundaries are explicit;
* administration is isolated;
* observability maps to actual boundaries;
* disaster recovery responsibilities are defined;
* infrastructure boundaries are explicit;
* scalability assumptions are documented;
* security boundaries are documented;
* portable integration contracts are present;
* no architecture document contradicts another architecture document.

If inconsistencies are discovered, resolve them before completion.

Do not leave known contradictions intentionally unresolved within this scope.

---

# 51. TESTING AND VALIDATION REQUIREMENTS

Architecture work must still be validated.

Perform appropriate validation such as:

* document consistency checks;
* schema/reference checks;
* link checks;
* Mermaid/diagram syntax validation where tooling permits;
* terminology consistency checks;
* architecture-contract consistency checks;
* configuration naming consistency checks;
* repository compatibility checks where a repository exists.

Do not claim runtime tests that require implementation not yet present.

Where architecture validation depends on unavailable tooling, state that limitation accurately.

---

# 52. DOCUMENTATION QUALITY REQUIREMENTS

Every artifact must be:

* concrete;
* internally consistent;
* implementation-useful;
* understandable by senior engineers;
* portable across Claude conversations;
* explicit about authoritative ownership;
* explicit about assumptions;
* explicit about failure behavior where relevant.

Do not create vague statements such as:

* "the system should scale";
* "the API will be secure";
* "use a database";
* "add caching";
* "use microservices if needed."

Replace vague requirements with architectural decisions and boundaries.

---

# 53. IMPLEMENTATION HANDOFF REQUIREMENTS

The architecture artifacts must provide enough information for later engineering teams to implement:

* backend modules;
* web clients;
* mobile clients;
* infrastructure;
* QA.

The architecture must therefore expose the relevant:

* domain boundaries;
* responsibilities;
* dependencies;
* data ownership;
* integration contracts;
* operational constraints.

Do not assume the later implementation team can consult this Claude conversation.

The artifacts themselves must carry the required architectural information.

---

# 54. DEFINITION OF DONE

This architecture volume is complete only when:

* the foundational system architecture is documented;
* major domains are explicitly bounded;
* ownership is defined;
* major data boundaries are established;
* major request flows are architecturally defined;
* feed architecture is established;
* media architecture is established;
* messaging/realtime architecture is established;
* discovery/search boundaries are established;
* authentication and authorization boundaries are established;
* moderation and administration boundaries are established;
* asynchronous processing is defined;
* cache responsibilities are defined;
* scalability considerations are documented;
* reliability and failure behavior are documented;
* deployment topology is documented;
* security and privacy boundaries are documented;
* observability boundaries are documented;
* disaster-recovery architecture is documented;
* portable integration contracts are created;
* requirement coverage is documented;
* diagrams correspond to the written design;
* ADRs cover major architecture choices;
* repository compatibility has been assessed when a repository exists;
* architecture validation has been performed;
* documentation contains no intentional placeholders or pseudo-architecture;
* no production secrets are present;
* no claim of live provisioning or unperformed validation is made.

---

# 55. COMPLETION REPORT

After producing the architecture artifacts, provide a completion report containing:

## Files Created

List every new file created.

## Files Modified

List every existing file modified.

## Files Deleted

List every file deleted, if any.

## Architecture Decisions

Summarize the major architectural decisions established.

## Domain Boundaries

Summarize the final domain ownership model.

## Data Architecture

Summarize authoritative data stores, derived data, caching, and major scaling decisions.

## API / Realtime / Event Architecture

Summarize the contract boundaries established.

## Media / Feed / Discovery Architecture

Summarize the major high-scale content systems.

## Security / Privacy

Summarize the major boundaries and protections.

## Infrastructure / Reliability

Summarize the deployment topology, scaling model, failure behavior, and disaster-recovery architecture.

## Validation Performed

State exactly what validation was actually performed.

Do not claim validation that was not performed.

## Repository Compatibility

State whether a repository was available, what was inspected, and whether any existing architecture constrained the design.

## Known Limitations

State any architectural limitations or assumptions that genuinely remain.

## Unresolved Issues

List only issues that genuinely remain unresolved after this architecture task.

---

# 56. FINAL ARCHITECTURE DISCIPLINE

Do not implement the application during this prompt.

Do not expand this volume into an unplanned implementation milestone.

Do not create a surprise architecture volume merely because additional architecture could theoretically be documented.

Within the defined scope, produce the strongest concrete architecture foundation possible.

The resulting artifact set must be portable, internally consistent, implementation-useful, and suitable for independent engineering teams working on the Instagram project.

The repository, when available, represents actual implementation state.

The architecture artifacts created by this prompt represent the authoritative architectural specification produced by this task.

Do not rely on hidden conversation history or undocumented decisions.
