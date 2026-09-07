# PROJECT 1 — INSTAGRAM-LIKE GLOBAL SOCIAL PLATFORM

# BACKEND PROMPT — VOLUME 2

# CONTENT, MEDIA, POSTS, STORIES, REELS & ENGAGEMENT

You are the Staff Backend Engineering team responsible for implementing the content and media backend of a production-grade Instagram-like global social platform.

This prompt is fully standalone. It does not depend on any other prompt, document, previous conversation, previous implementation, previous architecture, previous volume, approval, or hidden context.

You must inspect the current repository before making changes and integrate with compatible existing implementation.

Repository state is the source of truth for code that already exists.

Implement real production functionality.

Do not generate pseudo-code.

Do not create placeholder implementations.

Do not use TODO/FIXME as substitutes for required behavior.

Do not claim functionality is complete when it is not implemented.

Do not regenerate unchanged files.

Preserve existing working functionality unless modification is required for this scope.

==================================================

1. BACKEND SCOPE
   ==================================================

Implement the backend systems required for:

- media upload authorization
- media lifecycle management
- image processing
- video processing
- thumbnails
- media variants
- posts
- multi-media posts
- captions
- mentions
- hashtags
- post visibility
- post updates
- post deletion
- stories
- story expiration
- story viewers
- reels / short-form video
- likes
- comments
- replies
- saves
- shares
- engagement counters
- moderation integration
- search integration
- event propagation

The implementation must be secure, scalable, asynchronous where appropriate, and resilient to failure.

==================================================
2. REQUIRED TECHNOLOGY
======================

Backend:

- Node.js
- NestJS
- TypeScript

Persistence:

- PostgreSQL
- Prisma ORM

Caching and coordination:

- Redis

Events:

- Kafka or Redpanda

Background jobs:

- BullMQ

Storage:

- AWS S3

CDN:

- AWS CloudFront

Media:

- FFmpeg

Search:

- OpenSearch or Elasticsearch

Real-time integration:

- Socket.IO
- WebSockets

Observability:

- OpenTelemetry
- Prometheus
- Grafana
- Loki
- Tempo

==================================================
3. DOMAIN MODULES
=================

Create or integrate modules for:

- media
- media-processing
- posts
- stories
- reels
- comments
- likes
- saves
- shares
- hashtags
- mentions
- content-visibility
- engagement
- moderation integration
- search integration
- events
- background jobs

Keep responsibilities separated.

Controllers must remain thin.

Business rules belong in application/domain layers.

Persistence must be isolated through repositories or equivalent abstractions.

==================================================
4. MEDIA ASSET MODEL
====================

Create a durable MediaAsset model representing an uploaded media object.

It should support:

- media ID
- owner/user ID
- media type
- MIME type
- original filename where appropriate
- object key
- size
- checksum where practical
- width
- height
- duration
- processing state
- moderation state
- created timestamp
- updated timestamp
- deletion timestamp where applicable

Do not expose internal S3 object keys unnecessarily through public APIs.

==================================================
5. MEDIA VARIANT MODEL
======================

Create a MediaVariant model representing generated versions.

Support fields appropriate for:

- thumbnail
- preview
- feed image
- full image
- video resolution
- bitrate
- format
- codec
- width
- height
- duration
- file size
- object key
- processing status

A media asset may contain multiple variants.

==================================================
6. MEDIA LIFECYCLE
==================

Implement explicit media states.

At minimum:

- initialized
- uploading
- uploaded
- validating
- processing
- moderating
- ready
- rejected
- failed
- deleted

State transitions must be validated.

Do not permit a rejected or deleted asset to be used for publication.

==================================================
7. UPLOAD AUTHORIZATION
=======================

Implement secure upload-session creation.

Flow:

Client
→ authenticated upload request
→ validate user/account
→ validate intended media type
→ validate size limits
→ create media record
→ generate short-lived signed upload authorization
→ return upload information

Never trust the client to decide that an object uploaded to S3 is valid.

Server-side validation must occur after upload.

==================================================
8. DIRECT S3 UPLOAD
===================

Large media files should upload directly from clients to S3.

Application servers should not proxy the entire payload unnecessarily.

Signed upload authorization must:

- expire
- be scoped
- target controlled object paths
- prevent unintended object replacement
- restrict content type where practical
- enforce object size policy through the upload workflow

==================================================
9. UPLOAD COMPLETION
====================

Implement an upload completion endpoint/workflow.

The backend must:

1. authenticate user
2. locate the media asset
3. verify ownership
4. verify expected object location
5. confirm object existence
6. validate object metadata
7. transition media state
8. enqueue processing
9. return processing state

Calling completion multiple times must not create duplicate processing workflows.

==================================================
10. ABANDONED UPLOADS
=====================

Implement cleanup for incomplete uploads.

Track upload age.

Use BullMQ scheduled jobs to identify and clean expired temporary objects.

Cleanup must be safe when:

- upload already completed
- object was deleted externally
- processing already started
- completion was delayed

==================================================
11. MEDIA VALIDATION
====================

Validate uploaded media independently of client declarations.

Check where appropriate:

- content type
- actual file format
- file size
- dimensions
- duration
- codec
- corruption
- supported formats

Reject unsupported or dangerous content.

Never execute untrusted files directly on the host.

==================================================
12. IMAGE PROCESSING
====================

Implement asynchronous image-processing jobs.

Support:

- dimensions
- thumbnails
- resized variants
- optimization
- supported output formats

Processing must protect against:

- decompression bombs
- extreme dimensions
- malformed files
- excessive memory use

Define bounded worker concurrency.

==================================================
13. VIDEO PROCESSING
====================

Use FFmpeg in isolated worker execution.

The workflow should include:

- metadata extraction
- codec validation
- duration validation
- resolution validation
- transcoding
- thumbnails
- poster frame
- playback variants
- streaming packaging where appropriate

Never construct shell commands unsafely from user-provided values.

All user media metadata must be treated as untrusted input.

==================================================
14. FFmpeg RESOURCE CONTROLS
============================

Workers must enforce:

- maximum processing duration
- CPU constraints
- memory constraints
- concurrency limits
- file-size limits
- output-size limits

A single malicious or pathological video must not consume all worker capacity.

==================================================
15. PROCESSING RETRIES
======================

Media jobs should have bounded retries.

Use:

- exponential backoff
- retry count limits
- failure classification

Do not retry permanently invalid media indefinitely.

After final failure:

- mark asset failed
- persist failure reason safely
- emit media-processing failure event
- notify relevant application workflow where required

==================================================
16. MEDIA PROCESSING IDEMPOTENCY
================================

Processing must be safe against:

- duplicate job creation
- worker retries
- worker crashes
- duplicate events

Generated variants must not produce unlimited duplicates.

Use deterministic identifiers or equivalent idempotency controls.

==================================================
17. POST MODEL
==============

Implement a Post entity supporting:

- post ID
- author ID
- caption
- visibility
- status
- created timestamp
- updated timestamp
- deleted timestamp
- media relationship
- moderation state

Posts must not be published using media that is not authorized for the user.

==================================================
18. POST MEDIA RELATIONSHIP
===========================

Support multiple media assets per post.

Store:

- post ID
- media ID
- ordering
- media role where useful

Ordering must be deterministic.

Do not expose a way for a user to attach another user's media asset.

==================================================
19. POST CREATION
=================

Implement:

1. authenticate author
2. verify account state
3. validate caption
4. validate visibility
5. validate media ownership
6. verify media state
7. validate media count
8. validate mentions/hashtags
9. perform transactional creation
10. create outbox/domain event
11. schedule asynchronous derived processing

The post should become authoritative only through the successful database transaction.

==================================================
20. POST CAPTIONS
=================

Define strict limits for:

- caption length
- Unicode handling
- number of mentions
- number of hashtags

Do not permit unbounded user-generated text.

Do not store unnecessary duplicated parsing state unless justified.

==================================================
21. HASHTAG EXTRACTION
======================

Implement deterministic hashtag extraction.

Normalize hashtags consistently.

Avoid duplicate hashtag associations within one post.

Create or reuse hashtag records safely under concurrency.

Emit indexing events for search/discovery.

==================================================
22. MENTION EXTRACTION
======================

Mentions must:

- validate username format
- resolve users through authoritative data
- ignore nonexistent users
- respect account state
- respect privacy/product rules
- avoid duplicate associations

Mention processing must not allow unauthorized information exposure.

==================================================
23. POST VISIBILITY
===================

Support visibility states appropriate for the product, such as:

- public
- followers
- restricted/private contexts

Visibility must be enforced in:

- direct post retrieval
- feeds
- search
- notifications
- profile grids
- recommendations
- shared links

Never rely only on frontend filtering.

==================================================
24. POST RETRIEVAL
==================

Post retrieval must:

- authenticate where required
- verify visibility
- verify account state
- check block/restriction relationships
- confirm moderation status
- omit inaccessible media
- return stable DTOs

A known post ID must not bypass authorization.

==================================================
25. POST UPDATE
===============

Support updating permitted fields such as:

- caption
- visibility

Every update must:

- authenticate
- authorize ownership
- validate current state
- update transactionally
- emit update event
- update derived systems asynchronously

Do not allow mutation of immutable ownership information.

==================================================
26. POST DELETION
=================

Deletion must immediately prevent normal access.

Implementation must:

- mark post deleted or otherwise transition it out of active state
- invalidate relevant caches
- emit deletion event
- remove search representation
- remove/disable feed eligibility
- asynchronously clean related derived objects
- clean media objects according to lifecycle policy

A stale cache must not make deleted content readable.

==================================================
27. STORY MODEL
===============

Implement:

- Story
- StoryItem
- StoryView

Stories must support:

- author
- media
- ordering
- expiration timestamp
- visibility
- creation time
- deletion status

==================================================
28. STORY CREATION
==================

Validate:

- ownership
- media readiness
- supported media type
- account state
- visibility
- expiration configuration

Create story transactionally.

Emit appropriate asynchronous event.

==================================================
29. STORY EXPIRATION
====================

Stories must expire automatically.

Implement:

- database-level expiration fields
- request-time expiration checks
- scheduled cleanup jobs
- cache invalidation
- object cleanup

Never rely solely on the cleanup job.

A story with expiration in the past must be inaccessible immediately even if its cleanup job has not run.

==================================================
30. STORY ACCESS
================

Story access must verify:

- story exists
- story is not expired
- story not deleted
- viewer relationship
- block state
- account privacy
- story-specific visibility

Do not expose expired story content.

==================================================
31. STORY VIEW TRACKING
=======================

Implement story-view tracking with duplicate protection.

A viewer should not create unlimited logical duplicate views for the same story item unless explicitly required.

Use an appropriate uniqueness model.

High-volume view counting should avoid turning one database row into an unavoidable hotspot.

==================================================
32. REELS MODEL
===============

Implement a dedicated Reel domain that can reference video media.

Support:

- reel ID
- author
- media asset
- caption
- thumbnail
- duration
- publication state
- moderation state
- created timestamp
- updated timestamp
- deleted timestamp

Reels must use processed video variants.

==================================================
33. REEL PUBLICATION
====================

A reel may only become publicly available when:

- media processing succeeded
- required variants are ready
- moderation requirements are satisfied
- author is allowed to publish

Do not expose partially processed media as finished content.

==================================================
34. VIDEO DELIVERY METADATA
===========================

Return only necessary media delivery metadata.

For a ready reel, provide:

- playback URL or signed access strategy
- poster/thumbnail
- dimensions
- duration
- available variants

Do not expose private S3 credentials or internal infrastructure metadata.

==================================================
35. LIKE MODEL
==============

Implement durable likes with uniqueness:

(user_id, target_content_id)

A user must not create duplicate logical likes.

Use database constraints to enforce uniqueness under concurrent requests.

==================================================
36. LIKE OPERATIONS
===================

Implement:

- like
- unlike
- like-state retrieval

The API must be safe under repeated calls.

For example, repeated unlike operations should not create inconsistent counters or errors that leak internal state.

==================================================
37. ENGAGEMENT COUNTERS
=======================

Counters for:

- likes
- comments
- saves
- shares
- views

may be eventually consistent.

The authoritative underlying relationships must remain correct.

Counter updates should use asynchronous events or atomic aggregation techniques as appropriate.

==================================================
38. COMMENT MODEL
=================

Implement:

- Comment
- parent comment relationship where replies are supported
- author
- target content
- body
- status
- moderation state
- timestamps
- deletion state

Use bounded reply depth.

Do not implement arbitrary recursive comment trees unless there is a concrete requirement.

==================================================
39. COMMENT CREATION
====================

Validate:

- authenticated user
- target visibility
- account state
- text limits
- moderation
- mention rules where supported
- rate limits

Create comment transactionally.

Emit event afterward.

==================================================
40. COMMENT DELETION
====================

Comment deletion must respect:

- author ownership
- moderator privileges
- content status
- parent/reply relationships

Deleted comments must not reappear through:

- cached lists
- feeds
- notifications
- search where indexed

==================================================
41. COMMENT PAGINATION
======================

Use cursor pagination.

Define stable ordering, such as:

- newest-first
- oldest-first
- ranking order where explicitly supported

Never accept unrestricted pagination sizes.

==================================================
42. SAVE MODEL
==============

Implement user-specific saves.

A save must associate:

- user
- content
- created time

Prevent duplicate saves.

Saving must not expose content to users who are otherwise unauthorized to access it.

==================================================
43. SHARE MODEL
===============

Define a share operation appropriate to the product.

Do not implement sharing by blindly copying private content into public storage.

A share must respect original content visibility and authorization.

Emit a share event for engagement/analytics.

==================================================
44. ENGAGEMENT EVENT FLOW
=========================

Implement domain events such as:

- PostCreated
- PostUpdated
- PostDeleted
- ReelPublished
- StoryCreated
- StoryExpired
- MediaUploaded
- MediaProcessingCompleted
- MediaProcessingFailed
- PostLiked
- PostUnliked
- CommentCreated
- CommentDeleted
- PostSaved
- PostUnsaved
- PostShared

Events should include:

- event ID
- type
- version
- timestamp
- aggregate ID
- actor ID when appropriate
- correlation ID
- trace ID where available

Never publish passwords, access tokens, refresh tokens, or unnecessary private message data.

==================================================
45. OUTBOX PATTERN
==================

For authoritative content mutations:

database transaction
→ content state
→ outbox event

A publisher then delivers the event to Kafka/Redpanda.

Do not require the HTTP request to remain active while asynchronous event delivery occurs.

==================================================
46. BULLMQ WORKERS
==================

Create appropriate workers for:

- image processing
- video processing
- thumbnail generation
- story cleanup
- media cleanup
- search indexing triggers
- engagement aggregation
- abandoned upload cleanup

Each worker must provide:

- bounded concurrency
- retry policy
- timeout
- structured logging
- metrics
- failure handling

==================================================
47. REDIS CACHE
===============

Cache suitable read-heavy data such as:

- post summary
- profile/content relationship data where appropriate
- engagement summaries
- story metadata
- media delivery metadata

Every cache must define:

- TTL
- invalidation rules
- stale-data tolerance

Never use cache alone for access-control decisions.

==================================================
48. CACHE INVALIDATION
======================

Mutations must invalidate or update relevant cache entries.

At minimum consider:

- post update
- post deletion
- like/unlike
- comment changes
- save changes
- story expiration
- block relationship changes
- privacy changes

When invalidation is asynchronous, authoritative request-time authorization must still protect data.

==================================================
49. SEARCH INTEGRATION
======================

Content changes should publish search indexing events.

Index only information that is intended to be searchable.

When content becomes:

- deleted
- private
- restricted
- suspended
- moderation-blocked

the derived search representation must be removed or updated.

Search remains a derived system.

==================================================
50. MODERATION INTEGRATION
==========================

Content creation should integrate with moderation workflows.

Media/content may transition through moderation states such as:

- pending
- approved
- rejected
- restricted

The API must not expose prohibited content merely because media processing succeeded.

==================================================
51. SECURITY
============

Protect against:

- unauthorized media access
- object-key manipulation
- IDOR
- malicious uploads
- oversized files
- image bombs
- malicious videos
- command injection through media metadata
- privacy bypass
- spam
- automated engagement abuse

Validate both authorization and ownership.

==================================================
52. RATE LIMITING
=================

Apply distributed limits to:

- media upload initialization
- upload completion
- post creation
- comment creation
- likes
- saves
- shares
- story creation
- reel publication

Rates should be configurable.

==================================================
53. DATABASE INDEXING
=====================

Create indexes supporting:

Posts:

- author
- created time
- status
- visibility

Post media:

- post
- media
- ordering

Comments:

- target
- created time
- parent

Likes:

- user + target
- target + created time

Saves:

- user + target

Stories:

- author
- expiration
- active status

Story views:

- story item + viewer

Reels:

- author
- publication state
- created time

Do not add indexes without query justification.

==================================================
54. CONCURRENCY
===============

Handle simultaneous operations for:

- like/unlike
- save/unsave
- post creation
- post deletion
- story expiration
- media completion
- processing retries
- comment creation

Use:

- unique constraints
- transactions
- atomic updates
- idempotency keys
- state-transition checks

==================================================
55. MEDIA DELETION
==================

When media is no longer referenced and retention rules permit deletion:

- remove derived access
- delete or schedule deletion of variants
- delete S3 objects
- invalidate CDN references where applicable
- mark media deleted
- emit cleanup events

Do not delete media that remains referenced by an active valid object.

==================================================
56. CDN ARCHITECTURE
====================

Use CloudFront for media distribution.

Do not make application servers the default video/image streaming path.

Public assets may use public CDN caching.

Private assets require controlled access mechanisms.

CDN configuration must avoid bypassing application authorization for private resources.

==================================================
57. API CONTRACTS
=================

Implement stable DTOs for:

- media
- posts
- stories
- reels
- comments
- likes
- saves
- shares

Never expose Prisma entities directly.

Define explicit API contracts.

==================================================
58. API EXAMPLES
================

Provide production endpoints following the application's versioned API convention.

Examples include:

POST /api/v1/media/uploads
POST /api/v1/media/uploads/:mediaId/complete

POST /api/v1/posts
GET /api/v1/posts/:postId
PATCH /api/v1/posts/:postId
DELETE /api/v1/posts/:postId

POST /api/v1/posts/:postId/like
DELETE /api/v1/posts/:postId/like

GET /api/v1/posts/:postId/comments
POST /api/v1/posts/:postId/comments

POST /api/v1/posts/:postId/save
DELETE /api/v1/posts/:postId/save

POST /api/v1/stories
GET /api/v1/stories
POST /api/v1/stories/:storyId/view
DELETE /api/v1/stories/:storyId

POST /api/v1/reels
GET /api/v1/reels/:reelId

Use the repository's established naming/versioning convention when one already exists.

==================================================
59. ERROR HANDLING
==================

Return stable application errors for:

- invalid media
- unauthorized access
- missing resource
- expired story
- unavailable content
- invalid state transition
- duplicate interaction
- rate limiting
- processing failure
- dependency failure

Never expose raw S3, FFmpeg, Prisma, or filesystem errors.

==================================================
60. OBSERVABILITY
=================

Trace:

- media upload initialization
- upload completion
- processing jobs
- post creation
- post retrieval
- engagement operations
- story retrieval
- reel publication
- S3 operations
- Redis operations
- Kafka operations
- BullMQ jobs

Record metrics such as:

- media-processing duration
- media failure rate
- upload completion rate
- post creation latency
- engagement write rate
- comment latency
- queue depth
- queue wait time
- cache hit rate

Use structured logs without exposing secrets.

==================================================
61. TESTING
===========

Implement tests for:

Media:

- upload authorization
- ownership
- validation
- duplicate completion
- unsupported media
- processing failure
- processing retry
- cleanup

Posts:

- create
- update
- delete
- visibility
- multiple media
- unauthorized access

Stories:

- create
- expiration
- expired access rejection
- viewer authorization
- duplicate view prevention

Reels:

- processing requirement
- publication rules
- access

Engagement:

- duplicate likes
- unlike
- duplicate saves
- comments
- replies
- deletion
- shares

==================================================
62. SECURITY TESTING
====================

Explicitly test:

- IDOR
- attaching another user's media
- accessing private post
- accessing expired story
- accessing deleted content
- manipulating S3 object identifiers
- bypassing moderation state
- abusing upload completion
- replaying engagement mutations
- unauthorized deletion
- unauthorized editing

==================================================
63. ACCEPTANCE CRITERIA
=======================

This implementation is complete only when:

- media lifecycle exists
- upload authorization exists
- direct S3 upload flow exists
- upload completion exists
- abandoned-upload cleanup exists
- image processing exists
- video processing exists
- FFmpeg processing is isolated and bounded
- media variants exist
- posts work
- multi-media posts work
- captions work
- mentions work
- hashtags work
- visibility is enforced
- post update works
- post deletion works
- stories work
- story expiration is enforced
- story views work
- reels work
- likes work
- comments work
- replies work
- saves work
- shares work
- engagement counters are handled safely
- domain events are published reliably
- background workers exist
- search integration exists
- moderation integration exists
- cache behavior is implemented
- security controls exist
- observability exists
- OpenAPI contracts are updated
- automated tests cover critical behavior
- TypeScript compiles
- Prisma migrations succeed
- no required functionality is left as a placeholder

==================================================
64. IMPLEMENTATION FINISHING RULE
=================================

Do not stop after creating schemas, entities, or controllers.

Complete the actual functionality.

Inspect the existing repository first.

Reuse compatible components.

Integrate with existing infrastructure.

Do not rewrite unrelated working code.

Run appropriate validation for:

- formatting
- linting
- type checking
- Prisma validation
- database migrations
- unit tests
- integration tests
- security tests
- relevant worker execution

The resulting backend must provide a real production-grade content and media subsystem.
