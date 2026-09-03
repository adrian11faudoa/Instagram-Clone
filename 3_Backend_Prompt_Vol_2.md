You are operating in Senior Engineering Team Mode.

The Master Prompt, Architecture Volume 1, Architecture Volume 2, and Backend Volume 1 have already been completed.

Backend Volume 1 established the backend foundation, including:

- NestJS application architecture
- configuration
- request context
- structured errors
- validation
- PostgreSQL/Prisma foundation
- Redis foundation
- transactional outbox
- Kafka/Redpanda integration foundation
- BullMQ foundation
- health checks
- authentication
- accounts
- sessions
- devices
- profiles
- creator/professional profile foundations
- follow relationships
- follow requests
- blocks
- restrictions
- close friends
- authorization foundation
- privacy foundation
- API documentation
- initial tests

This volume continues directly from that implementation.

Do not restart the backend.

Do not replace working architecture.

Do not regenerate unchanged files.

Do not introduce an incompatible domain model.

Use the approved architecture as the source of truth.

==================================================
BACKEND VOLUME 2 SCOPE
======================

Implement the complete media and content foundation:

1. Media upload architecture
2. Upload sessions
3. Multipart/resumable upload support
4. S3 integration
5. Media metadata
6. Image processing
7. Video processing
8. FFmpeg workers
9. Thumbnail generation
10. HLS generation
11. Media variants
12. Media security
13. Posts
14. Carousels
15. Drafts
16. Captions
17. Mentions
18. Hashtags
19. Locations
20. Post visibility
21. Publication workflow
22. Post scheduling
23. Post editing
24. Post deletion
25. Post restoration
26. Stories
27. Story media
28. Story viewers
29. Story replies
30. Story reactions
31. Story expiration
32. Story highlights
33. Reels
34. Reel media
35. Reel audio references
36. Reel publication
37. Media/content moderation states
38. Rights-related content state integration
39. Content lifecycle events
40. Media/content background jobs
41. APIs
42. Security
43. Privacy
44. Observability
45. Automated tests

==================================================
IMPLEMENTATION RULES
====================

Production-grade implementation only.

Never generate:

- pseudo-code
- placeholders
- TODOs
- incomplete implementations
- fake production APIs
- fake media processing
- fake upload completion
- fake S3 behavior
- fake FFmpeg processing

Every generated file must compile.

Every changed database model must have a valid Prisma migration.

Every state transition must be validated.

Every content mutation must enforce authorization.

Every media access path must enforce privacy.

Every asynchronous operation must be retry-safe.

Never regenerate unchanged files.

==================================================
CONTENT/MEDIA ARCHITECTURE
==========================

The core flow is:

Client
→ API
→ Upload Session
→ S3
→ Processing Queue
→ Media Processor
→ Derived Media
→ Database State Update
→ Event
→ CDN delivery

For publishing:

Client
→ Content Draft
→ Media Validation
→ Content Validation
→ Publication Transaction
→ Event
→ Feed/Search/Recommendation consumers later

Do not make feed/search/recommendation implementation part of this volume.

==================================================

1. MEDIA DOMAIN FOUNDATION
   ==================================================

Create the media domain/application/infrastructure structure.

Media responsibilities include:

- upload authorization
- upload sessions
- object references
- media metadata
- processing state
- variants
- thumbnails
- video derivatives
- HLS
- media deletion
- media restoration
- secure access

Do not mix media infrastructure logic directly into post business logic.

==================================================
2. MEDIA ENTITY
===============

Define and implement the media model required by the architecture.

Support fields conceptually including:

- ID
- owner
- storage location
- media type
- MIME type
- size
- checksum
- width
- height
- duration
- orientation where needed
- status
- processing state
- visibility/access metadata
- createdAt
- updatedAt
- deletedAt where required

Use the approved database design.

==================================================
3. UPLOAD SESSION
=================

Implement upload sessions.

A session must support:

- initialization
- ownership
- expected file type
- expected size
- upload state
- expiration
- completion
- cancellation
- failure

Validate ownership on every operation.

==================================================
4. DIRECT S3 UPLOAD
===================

Implement secure S3 upload initialization.

Where the architecture specifies presigned upload:

1. authenticate user;
2. validate requested media;
3. create upload session;
4. generate authorized upload information;
5. return only safe client-facing information.

Never return AWS credentials.

==================================================
5. MULTIPART/RESUMABLE UPLOAD
=============================

Support multipart/resumable upload where required.

Implement:

- initiate
- upload parts
- complete
- abort
- expiration

Do not allow a user to complete another user's upload session.

==================================================
6. UPLOAD VALIDATION
====================

Validate:

- MIME type
- extension
- size
- media category
- expected dimensions where appropriate

Never rely solely on client-provided MIME type.

Where feasible, verify actual file characteristics during processing.

==================================================
7. UPLOAD LIMITS
================

Use configurable limits for:

- image size
- video size
- carousel item count
- upload duration
- request frequency

Do not hard-code arbitrary production limits directly into domain logic.

==================================================
8. MEDIA CHECKSUM
=================

Support checksums where useful for:

- integrity
- duplicate detection
- upload verification

Do not assume client-provided hashes are trustworthy without server verification when integrity matters.

==================================================
9. MEDIA PROCESSING STATE
=========================

Define clear states such as:

- initialized
- uploading
- uploaded
- validating
- processing
- ready
- failed
- cancelled
- deleted

State transitions must be explicit.

==================================================
10. PROCESSING JOB
==================

Create media-processing BullMQ jobs.

Payload must identify:

- media ID
- processing type
- required parameters
- attempt/context information

Do not put enormous binary payloads into queue messages.

Store media in S3.

==================================================
11. IMAGE PROCESSING
====================

Implement image processing for:

- dimensions
- orientation
- resizing
- optimized variants
- thumbnails
- metadata sanitization where appropriate

The processor must be isolated from untrusted input.

==================================================
12. IMAGE VARIANTS
==================

Support appropriate variants such as:

- thumbnail
- small
- medium
- large
- original/approved source where permitted

Do not generate arbitrary unlimited variants.

==================================================
13. VIDEO PROCESSING
====================

Implement:

- validation
- metadata extraction
- thumbnail extraction
- transcoding
- variants
- processing-state tracking

Use FFmpeg through a secure adapter.

==================================================
14. FFMPEG INTEGRATION
======================

Never directly assemble shell commands from user-controlled strings.

Use safe argument arrays/process APIs.

Validate:

- input path
- output path
- codecs
- resource limits

==================================================
15. VIDEO VARIANTS
==================

Support backend-defined:

- resolutions
- bitrate variants
- codecs where required

Do not create unsupported combinations.

==================================================
16. HLS
=======

Implement HLS generation for supported video workflows.

Track:

- manifest
- segments
- variants
- processing state

Store generated artifacts securely.

==================================================
17. THUMBNAILS
==============

Generate thumbnails for:

- video
- reels
- supported images

Ensure thumbnails respect content visibility and deletion state.

==================================================
18. MEDIA METADATA
==================

Store only metadata required by the product.

Avoid preserving unnecessary sensitive EXIF/location information.

Sanitize metadata as required.

==================================================
19. MEDIA SECURITY
==================

Implement protections against:

- malicious uploads
- oversized files
- malformed media
- path traversal
- executable content
- content-type spoofing

Storage paths must be generated by the system.

Never derive filesystem/object keys directly from unsanitized user input.

==================================================
20. PRIVATE MEDIA ACCESS
========================

Private media must not be publicly accessible.

Use the architecture-approved mechanism:

- presigned URLs
- signed CloudFront access
- signed cookies
- authorization gateway

Every protected media request must respect:

- account privacy
- content visibility
- block
- restriction
- rights
- moderation

==================================================
21. MEDIA DELETION
==================

Implement secure deletion workflow.

A deleted media object must eventually remove or invalidate:

- database metadata
- derived variants
- thumbnails
- HLS artifacts
- search references where applicable
- caches
- CDN accessibility where required

==================================================
22. MEDIA RESTORATION
=====================

Where the architecture supports restoration:

- restore metadata
- restore eligibility
- regenerate missing derivatives if required
- republish appropriate derived state through events

==================================================
23. CONTENT DOMAIN
==================

Create content domain/application/infrastructure structures.

Support:

- posts
- carousels
- drafts
- captions
- mentions
- hashtags
- locations
- visibility
- publication
- scheduling
- editing
- deletion
- restoration

==================================================
24. POST ENTITY
===============

Implement the Post aggregate according to Architecture Volume 2.

The post must support:

- owner
- caption
- visibility
- status
- publication timestamp
- media references
- location
- metadata
- comments configuration where supported

Do not place unrelated engagement data inside the Post aggregate.

==================================================
25. POST MEDIA
==============

Associate posts with media using explicit relationships.

Support:

- ordering
- carousel membership
- media role
- primary media
- accessibility metadata where applicable

==================================================
26. POST CREATION
=================

Implement post creation.

Validate:

- ownership of media
- media readiness
- visibility
- caption
- mentions
- hashtags
- location
- audience

The post must not reference media the user is not authorized to use.

==================================================
27. CAROUSEL
============

Implement carousel behavior.

Support:

- multiple media items
- ordering
- constraints
- media validation
- publication

Use transactional guarantees to prevent partially published carousels.

==================================================
28. DRAFTS
==========

Implement drafts.

Support:

- create
- update
- retrieve
- delete
- convert draft to publication

Drafts must remain private to their owner.

==================================================
29. DRAFT MEDIA
===============

A draft may reference uploaded media.

Ensure:

- media ownership
- lifecycle
- abandoned-upload cleanup
- deletion

==================================================
30. CAPTIONS
============

Support:

- plain text
- hashtags
- mentions
- length validation
- parsing

Do not store client-generated HTML as trusted content.

==================================================
31. HASHTAGS
============

Implement normalized hashtag references.

Support:

- extraction
- normalization
- association with posts
- duplicate prevention

Do not build hashtag search/trending in this volume.

Create events needed for later discovery systems.

==================================================
32. MENTIONS
============

Implement mention references.

Validate mentioned users.

Handle:

- user deletion
- username changes
- private profiles
- blocked users

The mention relationship must remain consistent with privacy and authorization rules.

==================================================
33. LOCATIONS
=============

Implement location references as defined by the architecture.

Do not create a mapping provider integration unless required by the approved architecture.

Do not store precise location data unnecessarily.

==================================================
34. VISIBILITY
==============

Support content visibility:

- public
- followers
- close friends where applicable
- private-owner state

Visibility must be evaluated by reusable policy logic.

==================================================
35. CONTENT STATE
=================

Define states such as:

- draft
- processing
- scheduled
- published
- restricted
- removed
- deleted
- restored

State transitions must be guarded.

==================================================
36. PUBLICATION
===============

Publishing must verify:

- authenticated owner
- content validity
- media readiness
- visibility
- moderation requirements
- rights requirements where applicable

Do not publish partially processed media.

==================================================
37. SCHEDULED PUBLICATION
=========================

Implement scheduling.

Support:

- schedule creation
- server-time validation
- cancellation
- rescheduling
- execution worker
- failure
- retry

Use BullMQ for scheduled execution.

==================================================
38. PUBLICATION JOB
===================

Scheduled publishing jobs must be idempotent.

Running a scheduled publish job twice must not create duplicate posts.

==================================================
39. POST EDITING
================

Support editing allowed post metadata.

Do not permit changing immutable fields after publication unless architecture explicitly allows it.

Examples:

May be editable:

- caption
- location
- certain visibility settings

Architecture must define what is immutable.

==================================================
40. POST DELETION
=================

Implement deletion.

Support:

- owner authorization
- state transition
- deletion timestamp
- event publication
- asynchronous derived-state cleanup

==================================================
41. POST RESTORATION
====================

Where restoration is permitted:

- validate state
- validate authorization
- restore
- republish appropriate events

==================================================
42. STORIES
===========

Implement the Story domain.

Support:

- create
- publish
- visibility
- media
- viewers
- replies
- reactions
- expiration
- highlights

==================================================
43. STORY ENTITY
================

Implement:

- owner
- media
- publication
- expiration
- visibility
- status

Stories are ephemeral content.

Do not retain active-state assumptions indefinitely.

==================================================
44. STORY EXPIRATION
====================

Implement expiration via:

- expiration timestamp
- BullMQ scheduled/cleanup job
- state transition
- derived cleanup events

Do not depend only on a user opening the story to detect expiration.

==================================================
45. STORY VIEWER
================

Implement story-view recording.

Ensure:

- authorized viewing
- duplicate prevention
- privacy
- block/restriction handling

Viewer counts may be eventually consistent.

==================================================
46. STORY REACTIONS
===================

Implement supported story reactions.

Ensure:

- authorization
- duplicate protection
- privacy
- notification event generation

==================================================
47. STORY REPLIES
=================

Implement story replies.

Respect:

- story owner settings
- messaging permissions
- blocks
- restrictions

Do not duplicate messaging-domain logic.

Generate appropriate integration events for messaging/notifications.

==================================================
48. HIGHLIGHTS
==============

Implement:

- Highlight
- HighlightItem

Support:

- create
- rename
- add story
- remove story
- delete
- reorder where supported

Highlights may reference stories beyond their active expiration lifecycle according to product rules.

==================================================
49. HIGHLIGHT AUTHORIZATION
===========================

Only the profile owner or authorized professional account can modify highlights.

==================================================
50. REELS
=========

Implement the Reel domain.

A reel should integrate with:

- media
- captions
- mentions
- hashtags
- audio
- visibility
- publication
- moderation
- rights

Do not implement recommendation ranking in this volume.

==================================================
51. REEL ENTITY
===============

Implement required reel fields:

- owner
- media
- caption
- visibility
- publication state
- audio reference
- duration/metadata
- processing state

==================================================
52. REEL CREATION
=================

Validate:

- media readiness
- video compatibility
- ownership
- visibility
- caption
- audio where supported

==================================================
53. REEL PROCESSING
===================

Integrate with media processing state.

Do not allow publication before required derivatives are ready.

==================================================
54. AUDIO REFERENCES
====================

Create the internal relationship to reusable audio.

Do not build a complete music/audio catalog in this volume.

Provide the contract required by later audio discovery features.

==================================================
55. CONTENT MODERATION STATE
============================

Support content states from moderation systems such as:

- normal
- under_review
- restricted
- removed

The exact moderation decision remains owned by the moderation domain.

Content must react to the decision.

==================================================
56. RIGHTS STATE
================

Support rights-related states such as:

- clear
- restricted
- takedown_pending
- takedown
- restoration_pending

Do not implement the complete rights-management domain yet.

Integrate through explicit interfaces/events.

==================================================
57. CONTENT EVENTS
==================

Publish events such as:

- MediaUploaded
- MediaProcessingStarted
- MediaProcessingCompleted
- MediaProcessingFailed
- MediaDeleted
- PostCreated
- PostPublished
- PostUpdated
- PostDeleted
- PostRestored
- StoryPublished
- StoryViewed
- StoryReplied
- StoryReacted
- StoryExpired
- HighlightCreated
- HighlightUpdated
- HighlightDeleted
- ReelCreated
- ReelPublished
- ReelUpdated
- ReelDeleted
- ContentVisibilityChanged

Use the approved event envelope.

==================================================
58. EVENT IDEMPOTENCY
=====================

Every downstream consumer must be able to safely process duplicates.

Do not assume exactly-once delivery.

==================================================
59. CONTENT CLEANUP
===================

Implement cleanup jobs for:

- abandoned uploads
- expired stories
- failed processing artifacts
- temporary media
- orphan media
- obsolete variants

Cleanup must be idempotent.

==================================================
60. ORPHAN DETECTION
====================

Create jobs that detect media objects that have no valid referencing content.

Do not immediately delete newly uploaded files merely because they are not referenced yet.

Use age/status thresholds.

==================================================
61. API ENDPOINTS
=================

Implement REST APIs for:

MEDIA:

- upload session creation
- upload completion
- upload cancellation
- media status
- media access metadata where required

POSTS:

- create
- retrieve
- update
- delete
- restore
- schedule
- cancel schedule

DRAFTS:

- create
- list
- retrieve
- update
- delete

STORIES:

- create
- retrieve
- publish
- view
- reply
- react
- delete

HIGHLIGHTS:

- create
- update
- add/remove story
- delete

REELS:

- create
- retrieve
- update
- publish
- delete

Use the exact resource structure established by the architecture.

==================================================
62. API AUTHORIZATION
=====================

Every content endpoint must evaluate:

- authentication
- ownership
- privacy
- block
- restriction
- account state
- content state
- moderation state
- rights state

==================================================
63. CONTENT RETRIEVAL
=====================

When retrieving content, do not return:

- deleted content
- blocked content
- unauthorized private content
- restricted content the requester cannot access
- unavailable media

unless a specific administrative workflow authorizes it.

==================================================
64. CONTENT UPDATE
==================

Prevent unauthorized updates.

Validate optimistic concurrency where required.

Avoid lost updates.

==================================================
65. MEDIA ACCESS API
====================

The media-access layer must not become an authorization bypass.

An S3 key or CDN URL must never be treated as sufficient authorization.

==================================================
66. RATE LIMITING
=================

Apply appropriate limits to:

- upload initialization
- upload completion
- post creation
- story creation
- reel creation
- comment-related operations when later added
- media-processing requests
- scheduling operations

==================================================
67. SECURITY
============

Test against:

- path traversal
- malicious media
- MIME spoofing
- oversized payloads
- unauthorized media access
- unauthorized post mutation
- private content access
- blocked-user bypass
- direct S3 access
- signed URL misuse
- duplicate publication
- duplicate scheduling

==================================================
68. PRIVACY
===========

Private drafts must never become public.

Close-friends stories must never be accessible to unauthorized users.

Private account content must not be retrievable through direct identifiers.

Deleted content must eventually disappear from derived systems through events.

==================================================
69. OBSERVABILITY
=================

Instrument:

- upload initiation
- upload completion
- media processing
- publication
- scheduling
- story views
- story expiration
- reel processing
- deletion
- restoration
- cleanup

Track:

- latency
- failure rate
- queue depth
- processing duration
- upload failures
- publication failures

==================================================
70. MEDIA PROCESSING METRICS
============================

Expose:

- media jobs started
- completed
- failed
- retries
- processing duration
- queue backlog
- per-media-type processing time

==================================================
71. STORAGE METRICS
===================

Monitor:

- upload volume
- object count
- storage size
- failed uploads
- incomplete multipart uploads
- cleanup volume

==================================================
72. TESTING
===========

Implement unit tests for:

- media state transitions
- upload validation
- privacy
- visibility
- publication rules
- scheduling
- story expiration
- highlight ownership
- reel rules

Integration tests for:

- PostgreSQL
- Prisma
- S3 adapter
- Redis
- BullMQ
- outbox
- media processing adapters

E2E/API tests for:

- upload
- post creation
- carousel
- draft
- publish
- edit
- delete
- restore
- story
- story view
- story reply
- story reaction
- highlight
- reel

==================================================
73. MEDIA TESTING
=================

Use controlled test files representing:

- valid image
- invalid image
- valid video
- unsupported video
- oversized media
- malformed media
- corrupted media

Do not place large binaries in Git unnecessarily.

==================================================
74. PROCESSING FAILURE TESTS
============================

Simulate:

- processor crash
- FFmpeg failure
- S3 failure
- timeout
- queue retry
- duplicate job

Verify safe recovery.

==================================================
75. CONTENT CONCURRENCY
=======================

Test concurrent:

- edit
- delete
- publish
- schedule
- cancel schedule

Verify invalid state transitions are rejected.

==================================================
76. MEDIA IDEMPOTENCY
=====================

Repeated processing jobs must not create uncontrolled duplicate derivatives.

Use deterministic variant/object-key strategy where appropriate.

==================================================
77. PUBLICATION IDEMPOTENCY
===========================

Repeated publish requests must not create duplicate content.

Use request-level idempotency keys where required.

==================================================
78. SCHEDULED PUBLICATION IDEMPOTENCY
=====================================

A scheduling worker retry must create exactly one logical publication.

==================================================
79. STORY EXPIRATION IDEMPOTENCY
================================

Multiple expiration jobs must produce one final expiration state.

==================================================
80. DOCUMENTATION
=================

Update:

- backend module map
- media architecture
- upload flow
- S3 integration
- processing pipeline
- content lifecycle
- story lifecycle
- reel lifecycle
- API documentation
- event catalog
- queue catalog
- security model
- privacy model
- local development instructions
- testing instructions

==================================================
81. MIGRATION DISCIPLINE
========================

All database changes must be implemented with Prisma migrations.

Do not modify migration history destructively.

==================================================
82. DEPENDENCY BOUNDARIES
=========================

Do not allow:

Post domain
→ direct AWS SDK calls.

Use:

Post application/domain
→ Media interface
→ Media infrastructure adapter

Similarly:

Content
→ Search interface later

Content
→ Feed event later

Content
→ Notification event later

Do not directly import future implementation modules.

==================================================
83. FUTURE INTEGRATION CONTRACTS
================================

Provide stable integration contracts/events for:

- feed
- search
- recommendations
- notifications
- moderation
- rights
- analytics

Do not implement those systems here.

==================================================
84. NO FEED IMPLEMENTATION
==========================

Do not implement:

- feed ranking
- recommendation ranking
- Explore
- trending
- personalized feed generation

This volume only produces the content/events required by those systems later.

==================================================
85. NO SEARCH IMPLEMENTATION
============================

Do not implement OpenSearch query behavior or search APIs here.

Only publish the content/indexing events and interfaces needed later.

==================================================
86. NO FRONTEND
===============

Do not implement:

- Next.js
- React
- UI
- browser upload components

Expose backend contracts only.

==================================================
87. NO MOBILE
=============

Do not implement:

- React Native
- Expo
- native camera
- native media picker

==================================================
88. NO INFRASTRUCTURE
=====================

Do not implement:

- Terraform
- Kubernetes
- Helm
- AWS account provisioning
- CI/CD

Infrastructure integrations must remain inside appropriate adapters/configuration.

==================================================
89. IMPLEMENTATION DISCIPLINE
=============================

Before every change:

1. Inspect current repository.
2. Inspect Backend Volume 1 implementation.
3. Identify reusable abstractions.
4. Verify Architecture Volume 2 contract.
5. Implement only required changes.
6. Add migrations.
7. Add tests.
8. Validate.
9. Fix failures.
10. Continue.

Never regenerate unchanged files.

==================================================
90. VALIDATION
==============

Run:

- formatter
- lint
- typecheck
- unit tests
- integration tests
- API/E2E tests
- backend build

Where supported also validate:

- Prisma schema
- migrations
- event schemas
- queue configuration

==================================================
FINAL ACCEPTANCE CRITERIA
=========================

Backend Volume 2 is complete when:

MEDIA

- upload sessions work;
- secure direct uploads work;
- multipart/resumable uploads work where required;
- S3 integration works;
- media metadata is stored;
- image processing works;
- video processing works;
- FFmpeg integration works;
- thumbnails work;
- HLS works where required;
- media variants work;
- processing states work;
- failed processing can retry;
- cleanup works;
- private media is protected.

CONTENT

- posts work;
- carousels work;
- drafts work;
- captions work;
- hashtags work;
- mentions work;
- locations work;
- visibility works;
- scheduling works;
- publishing works;
- editing works;
- deletion works;
- restoration works.

STORIES

- stories work;
- expiration works;
- viewers work;
- reactions work;
- replies work;
- highlights work.

REELS

- reels work;
- reel media works;
- reel processing works;
- audio references work;
- reel publication works.

SECURITY

- media authorization works;
- private content is protected;
- malicious media is rejected safely;
- direct storage access does not bypass authorization;
- duplicate publishing is prevented.

EVENTS

- content events are published;
- media events are published;
- outbox is used;
- consumers can later process events idempotently.

QUEUES

- media jobs work;
- scheduled publication works;
- expiration jobs work;
- cleanup jobs work;
- retry policies work.

TESTING

- unit tests exist;
- integration tests exist;
- API/E2E tests exist;
- failure paths are tested;
- concurrency is tested;
- idempotency is tested.

OBSERVABILITY

- processing metrics exist;
- publication metrics exist;
- queue metrics exist;
- failures are observable;
- traces/logs are privacy-safe.

==================================================
FINAL RULE
==========

Do not implement discovery, feed ranking, search, recommendations, notifications, messaging, advertising, commerce, or infrastructure in this volume.

The output of Backend Volume 2 must be a stable, production-grade content and media foundation consumed by later backend volumes.

BEGIN WITH:

1. INSPECT THE EXISTING BACKEND REPOSITORY.
2. VERIFY BACKEND VOLUME 1 CONTRACTS.
3. IMPLEMENT THE MEDIA/UPLOAD FOUNDATION.
4. IMPLEMENT POSTS, CAROUSELS, DRAFTS, STORIES, HIGHLIGHTS, AND REEL

You are operating in Senior Engineering Team Mode.

The Master Prompt, Architecture Volume 1, Architecture Volume 2, and Backend Volume 1 have already been completed.

Backend Volume 1 established the backend foundation, including:

- NestJS application architecture
- configuration
- request context
- structured errors
- validation
- PostgreSQL/Prisma foundation
- Redis foundation
- transactional outbox
- Kafka/Redpanda integration foundation
- BullMQ foundation
- health checks
- authentication
- accounts
- sessions
- devices
- profiles
- creator/professional profile foundations
- follow relationships
- follow requests
- blocks
- restrictions
- close friends
- authorization foundation
- privacy foundation
- API documentation
- initial tests

This volume continues directly from that implementation.

Do not restart the backend.

Do not replace working architecture.

Do not regenerate unchanged files.

Do not introduce an incompatible domain model.

Use the approved architecture as the source of truth.

==================================================
BACKEND VOLUME 2 SCOPE
======================

Implement the complete media and content foundation:

1. Media upload architecture
2. Upload sessions
3. Multipart/resumable upload support
4. S3 integration
5. Media metadata
6. Image processing
7. Video processing
8. FFmpeg workers
9. Thumbnail generation
10. HLS generation
11. Media variants
12. Media security
13. Posts
14. Carousels
15. Drafts
16. Captions
17. Mentions
18. Hashtags
19. Locations
20. Post visibility
21. Publication workflow
22. Post scheduling
23. Post editing
24. Post deletion
25. Post restoration
26. Stories
27. Story media
28. Story viewers
29. Story replies
30. Story reactions
31. Story expiration
32. Story highlights
33. Reels
34. Reel media
35. Reel audio references
36. Reel publication
37. Media/content moderation states
38. Rights-related content state integration
39. Content lifecycle events
40. Media/content background jobs
41. APIs
42. Security
43. Privacy
44. Observability
45. Automated tests

==================================================
IMPLEMENTATION RULES
====================

Production-grade implementation only.

Never generate:

- pseudo-code
- placeholders
- TODOs
- incomplete implementations
- fake production APIs
- fake media processing
- fake upload completion
- fake S3 behavior
- fake FFmpeg processing

Every generated file must compile.

Every changed database model must have a valid Prisma migration.

Every state transition must be validated.

Every content mutation must enforce authorization.

Every media access path must enforce privacy.

Every asynchronous operation must be retry-safe.

Never regenerate unchanged files.

==================================================
CONTENT/MEDIA ARCHITECTURE
==========================

The core flow is:

Client
→ API
→ Upload Session
→ S3
→ Processing Queue
→ Media Processor
→ Derived Media
→ Database State Update
→ Event
→ CDN delivery

For publishing:

Client
→ Content Draft
→ Media Validation
→ Content Validation
→ Publication Transaction
→ Event
→ Feed/Search/Recommendation consumers later

Do not make feed/search/recommendation implementation part of this volume.

==================================================

1. MEDIA DOMAIN FOUNDATION
   ==================================================

Create the media domain/application/infrastructure structure.

Media responsibilities include:

- upload authorization
- upload sessions
- object references
- media metadata
- processing state
- variants
- thumbnails
- video derivatives
- HLS
- media deletion
- media restoration
- secure access

Do not mix media infrastructure logic directly into post business logic.

==================================================
2. MEDIA ENTITY
===============

Define and implement the media model required by the architecture.

Support fields conceptually including:

- ID
- owner
- storage location
- media type
- MIME type
- size
- checksum
- width
- height
- duration
- orientation where needed
- status
- processing state
- visibility/access metadata
- createdAt
- updatedAt
- deletedAt where required

Use the approved database design.

==================================================
3. UPLOAD SESSION
=================

Implement upload sessions.

A session must support:

- initialization
- ownership
- expected file type
- expected size
- upload state
- expiration
- completion
- cancellation
- failure

Validate ownership on every operation.

==================================================
4. DIRECT S3 UPLOAD
===================

Implement secure S3 upload initialization.

Where the architecture specifies presigned upload:

1. authenticate user;
2. validate requested media;
3. create upload session;
4. generate authorized upload information;
5. return only safe client-facing information.

Never return AWS credentials.

==================================================
5. MULTIPART/RESUMABLE UPLOAD
=============================

Support multipart/resumable upload where required.

Implement:

- initiate
- upload parts
- complete
- abort
- expiration

Do not allow a user to complete another user's upload session.

==================================================
6. UPLOAD VALIDATION
====================

Validate:

- MIME type
- extension
- size
- media category
- expected dimensions where appropriate

Never rely solely on client-provided MIME type.

Where feasible, verify actual file characteristics during processing.

==================================================
7. UPLOAD LIMITS
================

Use configurable limits for:

- image size
- video size
- carousel item count
- upload duration
- request frequency

Do not hard-code arbitrary production limits directly into domain logic.

==================================================
8. MEDIA CHECKSUM
=================

Support checksums where useful for:

- integrity
- duplicate detection
- upload verification

Do not assume client-provided hashes are trustworthy without server verification when integrity matters.

==================================================
9. MEDIA PROCESSING STATE
=========================

Define clear states such as:

- initialized
- uploading
- uploaded
- validating
- processing
- ready
- failed
- cancelled
- deleted

State transitions must be explicit.

==================================================
10. PROCESSING JOB
==================

Create media-processing BullMQ jobs.

Payload must identify:

- media ID
- processing type
- required parameters
- attempt/context information

Do not put enormous binary payloads into queue messages.

Store media in S3.

==================================================
11. IMAGE PROCESSING
====================

Implement image processing for:

- dimensions
- orientation
- resizing
- optimized variants
- thumbnails
- metadata sanitization where appropriate

The processor must be isolated from untrusted input.

==================================================
12. IMAGE VARIANTS
==================

Support appropriate variants such as:

- thumbnail
- small
- medium
- large
- original/approved source where permitted

Do not generate arbitrary unlimited variants.

==================================================
13. VIDEO PROCESSING
====================

Implement:

- validation
- metadata extraction
- thumbnail extraction
- transcoding
- variants
- processing-state tracking

Use FFmpeg through a secure adapter.

==================================================
14. FFMPEG INTEGRATION
======================

Never directly assemble shell commands from user-controlled strings.

Use safe argument arrays/process APIs.

Validate:

- input path
- output path
- codecs
- resource limits

==================================================
15. VIDEO VARIANTS
==================

Support backend-defined:

- resolutions
- bitrate variants
- codecs where required

Do not create unsupported combinations.

==================================================
16. HLS
=======

Implement HLS generation for supported video workflows.

Track:

- manifest
- segments
- variants
- processing state

Store generated artifacts securely.

==================================================
17. THUMBNAILS
==============

Generate thumbnails for:

- video
- reels
- supported images

Ensure thumbnails respect content visibility and deletion state.

==================================================
18. MEDIA METADATA
==================

Store only metadata required by the product.

Avoid preserving unnecessary sensitive EXIF/location information.

Sanitize metadata as required.

==================================================
19. MEDIA SECURITY
==================

Implement protections against:

- malicious uploads
- oversized files
- malformed media
- path traversal
- executable content
- content-type spoofing

Storage paths must be generated by the system.

Never derive filesystem/object keys directly from unsanitized user input.

==================================================
20. PRIVATE MEDIA ACCESS
========================

Private media must not be publicly accessible.

Use the architecture-approved mechanism:

- presigned URLs
- signed CloudFront access
- signed cookies
- authorization gateway

Every protected media request must respect:

- account privacy
- content visibility
- block
- restriction
- rights
- moderation

==================================================
21. MEDIA DELETION
==================

Implement secure deletion workflow.

A deleted media object must eventually remove or invalidate:

- database metadata
- derived variants
- thumbnails
- HLS artifacts
- search references where applicable
- caches
- CDN accessibility where required

==================================================
22. MEDIA RESTORATION
=====================

Where the architecture supports restoration:

- restore metadata
- restore eligibility
- regenerate missing derivatives if required
- republish appropriate derived state through events

==================================================
23. CONTENT DOMAIN
==================

Create content domain/application/infrastructure structures.

Support:

- posts
- carousels
- drafts
- captions
- mentions
- hashtags
- locations
- visibility
- publication
- scheduling
- editing
- deletion
- restoration

==================================================
24. POST ENTITY
===============

Implement the Post aggregate according to Architecture Volume 2.

The post must support:

- owner
- caption
- visibility
- status
- publication timestamp
- media references
- location
- metadata
- comments configuration where supported

Do not place unrelated engagement data inside the Post aggregate.

==================================================
25. POST MEDIA
==============

Associate posts with media using explicit relationships.

Support:

- ordering
- carousel membership
- media role
- primary media
- accessibility metadata where applicable

==================================================
26. POST CREATION
=================

Implement post creation.

Validate:

- ownership of media
- media readiness
- visibility
- caption
- mentions
- hashtags
- location
- audience

The post must not reference media the user is not authorized to use.

==================================================
27. CAROUSEL
============

Implement carousel behavior.

Support:

- multiple media items
- ordering
- constraints
- media validation
- publication

Use transactional guarantees to prevent partially published carousels.

==================================================
28. DRAFTS
==========

Implement drafts.

Support:

- create
- update
- retrieve
- delete
- convert draft to publication

Drafts must remain private to their owner.

==================================================
29. DRAFT MEDIA
===============

A draft may reference uploaded media.

Ensure:

- media ownership
- lifecycle
- abandoned-upload cleanup
- deletion

==================================================
30. CAPTIONS
============

Support:

- plain text
- hashtags
- mentions
- length validation
- parsing

Do not store client-generated HTML as trusted content.

==================================================
31. HASHTAGS
============

Implement normalized hashtag references.

Support:

- extraction
- normalization
- association with posts
- duplicate prevention

Do not build hashtag search/trending in this volume.

Create events needed for later discovery systems.

==================================================
32. MENTIONS
============

Implement mention references.

Validate mentioned users.

Handle:

- user deletion
- username changes
- private profiles
- blocked users

The mention relationship must remain consistent with privacy and authorization rules.

==================================================
33. LOCATIONS
=============

Implement location references as defined by the architecture.

Do not create a mapping provider integration unless required by the approved architecture.

Do not store precise location data unnecessarily.

==================================================
34. VISIBILITY
==============

Support content visibility:

- public
- followers
- close friends where applicable
- private-owner state

Visibility must be evaluated by reusable policy logic.

==================================================
35. CONTENT STATE
=================

Define states such as:

- draft
- processing
- scheduled
- published
- restricted
- removed
- deleted
- restored

State transitions must be guarded.

==================================================
36. PUBLICATION
===============

Publishing must verify:

- authenticated owner
- content validity
- media readiness
- visibility
- moderation requirements
- rights requirements where applicable

Do not publish partially processed media.

==================================================
37. SCHEDULED PUBLICATION
=========================

Implement scheduling.

Support:

- schedule creation
- server-time validation
- cancellation
- rescheduling
- execution worker
- failure
- retry

Use BullMQ for scheduled execution.

==================================================
38. PUBLICATION JOB
===================

Scheduled publishing jobs must be idempotent.

Running a scheduled publish job twice must not create duplicate posts.

==================================================
39. POST EDITING
================

Support editing allowed post metadata.

Do not permit changing immutable fields after publication unless architecture explicitly allows it.

Examples:

May be editable:

- caption
- location
- certain visibility settings

Architecture must define what is immutable.

==================================================
40. POST DELETION
=================

Implement deletion.

Support:

- owner authorization
- state transition
- deletion timestamp
- event publication
- asynchronous derived-state cleanup

==================================================
41. POST RESTORATION
====================

Where restoration is permitted:

- validate state
- validate authorization
- restore
- republish appropriate events

==================================================
42. STORIES
===========

Implement the Story domain.

Support:

- create
- publish
- visibility
- media
- viewers
- replies
- reactions
- expiration
- highlights

==================================================
43. STORY ENTITY
================

Implement:

- owner
- media
- publication
- expiration
- visibility
- status

Stories are ephemeral content.

Do not retain active-state assumptions indefinitely.

==================================================
44. STORY EXPIRATION
====================

Implement expiration via:

- expiration timestamp
- BullMQ scheduled/cleanup job
- state transition
- derived cleanup events

Do not depend only on a user opening the story to detect expiration.

==================================================
45. STORY VIEWER
================

Implement story-view recording.

Ensure:

- authorized viewing
- duplicate prevention
- privacy
- block/restriction handling

Viewer counts may be eventually consistent.

==================================================
46. STORY REACTIONS
===================

Implement supported story reactions.

Ensure:

- authorization
- duplicate protection
- privacy
- notification event generation

==================================================
47. STORY REPLIES
=================

Implement story replies.

Respect:

- story owner settings
- messaging permissions
- blocks
- restrictions

Do not duplicate messaging-domain logic.

Generate appropriate integration events for messaging/notifications.

==================================================
48. HIGHLIGHTS
==============

Implement:

- Highlight
- HighlightItem

Support:

- create
- rename
- add story
- remove story
- delete
- reorder where supported

Highlights may reference stories beyond their active expiration lifecycle according to product rules.

==================================================
49. HIGHLIGHT AUTHORIZATION
===========================

Only the profile owner or authorized professional account can modify highlights.

==================================================
50. REELS
=========

Implement the Reel domain.

A reel should integrate with:

- media
- captions
- mentions
- hashtags
- audio
- visibility
- publication
- moderation
- rights

Do not implement recommendation ranking in this volume.

==================================================
51. REEL ENTITY
===============

Implement required reel fields:

- owner
- media
- caption
- visibility
- publication state
- audio reference
- duration/metadata
- processing state

==================================================
52. REEL CREATION
=================

Validate:

- media readiness
- video compatibility
- ownership
- visibility
- caption
- audio where supported

==================================================
53. REEL PROCESSING
===================

Integrate with media processing state.

Do not allow publication before required derivatives are ready.

==================================================
54. AUDIO REFERENCES
====================

Create the internal relationship to reusable audio.

Do not build a complete music/audio catalog in this volume.

Provide the contract required by later audio discovery features.

==================================================
55. CONTENT MODERATION STATE
============================

Support content states from moderation systems such as:

- normal
- under_review
- restricted
- removed

The exact moderation decision remains owned by the moderation domain.

Content must react to the decision.

==================================================
56. RIGHTS STATE
================

Support rights-related states such as:

- clear
- restricted
- takedown_pending
- takedown
- restoration_pending

Do not implement the complete rights-management domain yet.

Integrate through explicit interfaces/events.

==================================================
57. CONTENT EVENTS
==================

Publish events such as:

- MediaUploaded
- MediaProcessingStarted
- MediaProcessingCompleted
- MediaProcessingFailed
- MediaDeleted
- PostCreated
- PostPublished
- PostUpdated
- PostDeleted
- PostRestored
- StoryPublished
- StoryViewed
- StoryReplied
- StoryReacted
- StoryExpired
- HighlightCreated
- HighlightUpdated
- HighlightDeleted
- ReelCreated
- ReelPublished
- ReelUpdated
- ReelDeleted
- ContentVisibilityChanged

Use the approved event envelope.

==================================================
58. EVENT IDEMPOTENCY
=====================

Every downstream consumer must be able to safely process duplicates.

Do not assume exactly-once delivery.

==================================================
59. CONTENT CLEANUP
===================

Implement cleanup jobs for:

- abandoned uploads
- expired stories
- failed processing artifacts
- temporary media
- orphan media
- obsolete variants

Cleanup must be idempotent.

==================================================
60. ORPHAN DETECTION
====================

Create jobs that detect media objects that have no valid referencing content.

Do not immediately delete newly uploaded files merely because they are not referenced yet.

Use age/status thresholds.

==================================================
61. API ENDPOINTS
=================

Implement REST APIs for:

MEDIA:

- upload session creation
- upload completion
- upload cancellation
- media status
- media access metadata where required

POSTS:

- create
- retrieve
- update
- delete
- restore
- schedule
- cancel schedule

DRAFTS:

- create
- list
- retrieve
- update
- delete

STORIES:

- create
- retrieve
- publish
- view
- reply
- react
- delete

HIGHLIGHTS:

- create
- update
- add/remove story
- delete

REELS:

- create
- retrieve
- update
- publish
- delete

Use the exact resource structure established by the architecture.

==================================================
62. API AUTHORIZATION
=====================

Every content endpoint must evaluate:

- authentication
- ownership
- privacy
- block
- restriction
- account state
- content state
- moderation state
- rights state

==================================================
63. CONTENT RETRIEVAL
=====================

When retrieving content, do not return:

- deleted content
- blocked content
- unauthorized private content
- restricted content the requester cannot access
- unavailable media

unless a specific administrative workflow authorizes it.

==================================================
64. CONTENT UPDATE
==================

Prevent unauthorized updates.

Validate optimistic concurrency where required.

Avoid lost updates.

==================================================
65. MEDIA ACCESS API
====================

The media-access layer must not become an authorization bypass.

An S3 key or CDN URL must never be treated as sufficient authorization.

==================================================
66. RATE LIMITING
=================

Apply appropriate limits to:

- upload initialization
- upload completion
- post creation
- story creation
- reel creation
- comment-related operations when later added
- media-processing requests
- scheduling operations

==================================================
67. SECURITY
============

Test against:

- path traversal
- malicious media
- MIME spoofing
- oversized payloads
- unauthorized media access
- unauthorized post mutation
- private content access
- blocked-user bypass
- direct S3 access
- signed URL misuse
- duplicate publication
- duplicate scheduling

==================================================
68. PRIVACY
===========

Private drafts must never become public.

Close-friends stories must never be accessible to unauthorized users.

Private account content must not be retrievable through direct identifiers.

Deleted content must eventually disappear from derived systems through events.

==================================================
69. OBSERVABILITY
=================

Instrument:

- upload initiation
- upload completion
- media processing
- publication
- scheduling
- story views
- story expiration
- reel processing
- deletion
- restoration
- cleanup

Track:

- latency
- failure rate
- queue depth
- processing duration
- upload failures
- publication failures

==================================================
70. MEDIA PROCESSING METRICS
============================

Expose:

- media jobs started
- completed
- failed
- retries
- processing duration
- queue backlog
- per-media-type processing time

==================================================
71. STORAGE METRICS
===================

Monitor:

- upload volume
- object count
- storage size
- failed uploads
- incomplete multipart uploads
- cleanup volume

==================================================
72. TESTING
===========

Implement unit tests for:

- media state transitions
- upload validation
- privacy
- visibility
- publication rules
- scheduling
- story expiration
- highlight ownership
- reel rules

Integration tests for:

- PostgreSQL
- Prisma
- S3 adapter
- Redis
- BullMQ
- outbox
- media processing adapters

E2E/API tests for:

- upload
- post creation
- carousel
- draft
- publish
- edit
- delete
- restore
- story
- story view
- story reply
- story reaction
- highlight
- reel

==================================================
73. MEDIA TESTING
=================

Use controlled test files representing:

- valid image
- invalid image
- valid video
- unsupported video
- oversized media
- malformed media
- corrupted media

Do not place large binaries in Git unnecessarily.

==================================================
74. PROCESSING FAILURE TESTS
============================

Simulate:

- processor crash
- FFmpeg failure
- S3 failure
- timeout
- queue retry
- duplicate job

Verify safe recovery.

==================================================
75. CONTENT CONCURRENCY
=======================

Test concurrent:

- edit
- delete
- publish
- schedule
- cancel schedule

Verify invalid state transitions are rejected.

==================================================
76. MEDIA IDEMPOTENCY
=====================

Repeated processing jobs must not create uncontrolled duplicate derivatives.

Use deterministic variant/object-key strategy where appropriate.

==================================================
77. PUBLICATION IDEMPOTENCY
===========================

Repeated publish requests must not create duplicate content.

Use request-level idempotency keys where required.

==================================================
78. SCHEDULED PUBLICATION IDEMPOTENCY
=====================================

A scheduling worker retry must create exactly one logical publication.

==================================================
79. STORY EXPIRATION IDEMPOTENCY
================================

Multiple expiration jobs must produce one final expiration state.

==================================================
80. DOCUMENTATION
=================

Update:

- backend module map
- media architecture
- upload flow
- S3 integration
- processing pipeline
- content lifecycle
- story lifecycle
- reel lifecycle
- API documentation
- event catalog
- queue catalog
- security model
- privacy model
- local development instructions
- testing instructions

==================================================
81. MIGRATION DISCIPLINE
========================

All database changes must be implemented with Prisma migrations.

Do not modify migration history destructively.

==================================================
82. DEPENDENCY BOUNDARIES
=========================

Do not allow:

Post domain
→ direct AWS SDK calls.

Use:

Post application/domain
→ Media interface
→ Media infrastructure adapter

Similarly:

Content
→ Search interface later

Content
→ Feed event later

Content
→ Notification event later

Do not directly import future implementation modules.

==================================================
83. FUTURE INTEGRATION CONTRACTS
================================

Provide stable integration contracts/events for:

- feed
- search
- recommendations
- notifications
- moderation
- rights
- analytics

Do not implement those systems here.

==================================================
84. NO FEED IMPLEMENTATION
==========================

Do not implement:

- feed ranking
- recommendation ranking
- Explore
- trending
- personalized feed generation

This volume only produces the content/events required by those systems later.

==================================================
85. NO SEARCH IMPLEMENTATION
============================

Do not implement OpenSearch query behavior or search APIs here.

Only publish the content/indexing events and interfaces needed later.

==================================================
86. NO FRONTEND
===============

Do not implement:

- Next.js
- React
- UI
- browser upload components

Expose backend contracts only.

==================================================
87. NO MOBILE
=============

Do not implement:

- React Native
- Expo
- native camera
- native media picker

==================================================
88. NO INFRASTRUCTURE
=====================

Do not implement:

- Terraform
- Kubernetes
- Helm
- AWS account provisioning
- CI/CD

Infrastructure integrations must remain inside appropriate adapters/configuration.

==================================================
89. IMPLEMENTATION DISCIPLINE
=============================

Before every change:

1. Inspect current repository.
2. Inspect Backend Volume 1 implementation.
3. Identify reusable abstractions.
4. Verify Architecture Volume 2 contract.
5. Implement only required changes.
6. Add migrations.
7. Add tests.
8. Validate.
9. Fix failures.
10. Continue.

Never regenerate unchanged files.

==================================================
90. VALIDATION
==============

Run:

- formatter
- lint
- typecheck
- unit tests
- integration tests
- API/E2E tests
- backend build

Where supported also validate:

- Prisma schema
- migrations
- event schemas
- queue configuration

==================================================
FINAL ACCEPTANCE CRITERIA
=========================

Backend Volume 2 is complete when:

MEDIA

- upload sessions work;
- secure direct uploads work;
- multipart/resumable uploads work where required;
- S3 integration works;
- media metadata is stored;
- image processing works;
- video processing works;
- FFmpeg integration works;
- thumbnails work;
- HLS works where required;
- media variants work;
- processing states work;
- failed processing can retry;
- cleanup works;
- private media is protected.

CONTENT

- posts work;
- carousels work;
- drafts work;
- captions work;
- hashtags work;
- mentions work;
- locations work;
- visibility works;
- scheduling works;
- publishing works;
- editing works;
- deletion works;
- restoration works.

STORIES

- stories work;
- expiration works;
- viewers work;
- reactions work;
- replies work;
- highlights work.

REELS

- reels work;
- reel media works;
- reel processing works;
- audio references work;
- reel publication works.

SECURITY

- media authorization works;
- private content is protected;
- malicious media is rejected safely;
- direct storage access does not bypass authorization;
- duplicate publishing is prevented.

EVENTS

- content events are published;
- media events are published;
- outbox is used;
- consumers can later process events idempotently.

QUEUES

- media jobs work;
- scheduled publication works;
- expiration jobs work;
- cleanup jobs work;
- retry policies work.

TESTING

- unit tests exist;
- integration tests exist;
- API/E2E tests exist;
- failure paths are tested;
- concurrency is tested;
- idempotency is tested.

OBSERVABILITY

- processing metrics exist;
- publication metrics exist;
- queue metrics exist;
- failures are observable;
- traces/logs are privacy-safe.

==================================================
FINAL RULE
==========

Do not implement discovery, feed ranking, search, recommendations, notifications, messaging, advertising, commerce, or infrastructure in this volume.

The output of Backend Volume 2 must be a stable, production-grade content and media foundation consumed by later backend volumes.

BEGIN WITH:

1. INSPECT THE EXISTING BACKEND REPOSITORY.
2. VERIFY BACKEND VOLUME 1 CONTRACTS.
3. IMPLEMENT THE MEDIA/UPLOAD FOUNDATION.
4. IMPLEMENT POSTS, CAROUSELS, DRAFTS, STORIES, HIGHLIGHTS, AND REEL

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
