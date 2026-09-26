# Instagram — Frontend Prompt — Volume 3

# 1. ROLE

You are the **Senior Frontend Engineering implementation team** responsible for implementing the bounded frontend scope defined in this prompt for the Instagram project.

Operate as a production engineering organization with expertise in:

* React and Next.js
* TypeScript
* responsive media-heavy interfaces
* real-time and time-sensitive user experiences
* accessible interaction design
* high-performance media playback
* client-side caching and synchronization
* API contract integration
* automated frontend testing
* observability and production diagnostics
* secure rendering of user-generated content

Your responsibility is to implement the assigned frontend scope completely and coherently inside the repository while preserving compatibility with the existing application architecture and backend contracts.

Do not implement unrelated project areas merely because they exist elsewhere in the product.

Do not create pseudo-implementations, fake APIs, fake persistence, placeholder components, TODO-driven stubs, or visually convincing functionality that is not actually wired to the application's contracts.

# 2. PROJECT IDENTITY

The project is a production-grade **Instagram-style social media platform**.

The frontend is a TypeScript-based Next.js/React web application consuming production-oriented backend APIs and supporting large-scale media consumption.

The product includes:

* identity and accounts
* profiles
* social graph
* home feed
* posts and media
* stories
* short-form video
* likes, comments, saves, and shares
* discovery and search
* direct messaging
* notifications
* moderation and reporting
* privacy and safety controls
* responsive web experiences
* observability, reliability, accessibility, and performance

This prompt is limited to the **Stories and short-form video frontend experience**.

# 3. CURRENT FRONTEND ASSIGNMENT

Implement the Instagram-style **Stories and short-form video consumption experience** for the web application.

This volume owns:

* Stories entry points
* Stories viewer
* story sequencing
* story navigation
* story progress
* story expiration and unavailable states
* story media rendering
* story interaction controls
* story view state
* story-related API integration
* short-form video discovery/consumption surface where defined by existing application contracts
* vertical video playback
* video feed navigation
* media loading and buffering states
* gesture/pointer/keyboard interaction
* performance-conscious media lifecycle management
* responsive presentation
* accessibility
* telemetry and error handling
* automated tests for all implemented behavior

Do not use this prompt to implement direct messaging, advanced discovery/search, notifications, moderation dashboards, or mobile React Native applications.

# 4. REPOSITORY INSPECTION

Before modifying code, inspect the repository sufficiently to identify:

* existing Next.js routing
* application layouts
* design-system primitives
* media components from earlier frontend work
* feed/post components
* API client
* server-state/data-fetching infrastructure
* client-state mechanisms
* authentication/session handling
* shared media types
* story/content contracts
* short-form video contracts
* event and telemetry infrastructure
* error handling
* testing infrastructure
* responsive layout conventions
* accessibility utilities
* build and lint configuration
* environment configuration

Inspect authoritative architecture and contract artifacts covering:

* stories
* story lifecycle
* story visibility
* story media
* story viewing
* short-form video
* media delivery
* authorization
* pagination
* engagement
* errors
* identifiers
* timestamps
* observability

Treat existing implementation patterns and repository contracts as authoritative.

Do not create a competing media architecture when reusable infrastructure already exists.

# 5. TECHNOLOGY BASELINE

Use the repository's existing technology choices, expected to include:

* Next.js
* React
* TypeScript
* semantic HTML
* established responsive styling system
* established component/design system
* existing API client
* established server-state management
* existing telemetry
* established test framework

Do not introduce a new state-management or media framework without a concrete compatibility and maintenance justification.

Maintain strict TypeScript typing.

# 6. BOUNDED IMPLEMENTATION SCOPE

Implement the following functionality completely.

## 6.1 Stories Entry Surface

Implement the authenticated web experience for discovering available stories.

Support the product's established story-entry presentation, including as applicable:

* story avatars
* user identity
* viewed/unviewed state
* story availability
* ordering
* horizontal navigation
* responsive presentation
* loading state
* empty state
* failure state
* accessibility

Use the backend's story ordering and visibility semantics.

Do not invent client-side ranking logic that contradicts server-provided ordering.

## 6.2 Story Viewer

Implement the primary story viewing experience.

Support:

* opening a story sequence
* rendering the current story
* advancing to the next story
* returning to the previous story
* moving between stories from different users
* progress indication
* pause behavior
* resume behavior
* close behavior
* loading states
* failed-media states
* unavailable story states
* expiration handling
* keyboard interaction
* pointer interaction
* touch interaction where supported by the web experience

The viewer must keep the current story and overall sequence state coherent.

## 6.3 Story Progress

Implement deterministic story progress behavior.

Support:

* time-based progress for supported media
* media-duration-aware timing
* progress reset when changing stories
* pause/resume without accidental advancement
* prevention of multiple concurrent timers
* proper cleanup during route changes and unmount
* transition to the next story on completion
* correct handling of immediately unavailable content

Never allow multiple timers to advance the viewer simultaneously.

## 6.4 Story Media

Support the media types defined by the application's contracts.

For images:

* responsive sizing
* correct aspect ratio
* appropriate loading
* layout stability
* failure handling
* accessibility

For video:

* controlled playback
* autoplay behavior consistent with browser restrictions
* muted startup where required
* play/pause lifecycle
* buffering handling
* progress integration
* cleanup
* failure handling
* responsive presentation

Do not assume browser support or autoplay behavior that is not guaranteed.

## 6.5 Story Navigation

Implement clear navigation between story items.

Support:

* next
* previous
* close
* direct selection where supported
* keyboard navigation
* pointer/tap navigation
* appropriate disabled or unavailable behavior

Avoid accidental navigation when interacting with controls or media.

Navigation state must remain synchronized with the actual story sequence.

## 6.6 Story Interaction Controls

Implement controls defined by the project's story contract.

These may include:

* pause/resume
* mute/unmute
* close
* navigation
* view-related actions where applicable
* share/action affordances where explicitly supported

Do not expose backend or moderation controls that belong to other frontend domains.

## 6.7 Story View State

Integrate story-view tracking according to the backend contract.

Support:

* recording the current user's story-view state
* avoiding duplicate requests when the contract permits client deduplication
* correct timing of view registration
* handling already-viewed content
* retry/failure behavior
* stale state reconciliation

Do not treat local state as authoritative persistence.

The backend remains authoritative for durable story-view state.

## 6.8 Story Expiration and Availability

Stories are time-bound content.

Handle:

* expired stories
* deleted stories
* removed stories
* unavailable media
* authorization changes
* invalid story references
* sequence changes while the viewer is open

Do not leave users on a blank or permanently loading screen when a story becomes unavailable.

Move to the appropriate next valid state or provide an explicit unavailable-content experience.

## 6.9 Story Sequence Consistency

Protect the viewer against inconsistencies caused by changing story data.

Handle cases such as:

* an item disappearing from the sequence
* an item being removed after initial loading
* duplicate story IDs
* stale cached story data
* a user having no remaining available stories
* a sequence becoming shorter while viewing

Never render duplicate story items merely because two pagination or refresh responses overlap.

# 7. SHORT-FORM VIDEO EXPERIENCE

Implement the web frontend for the project's short-form vertical-video consumption surface defined by the repository contracts.

## 7.1 Video Feed

Support:

* loading short-form videos
* rendering one active video at a time where appropriate
* vertical navigation
* pagination
* loading-more behavior
* end-of-content handling
* empty state
* failure and retry
* unavailable-video handling

Honor the backend's content ordering and authorization rules.

## 7.2 Video Playback

Implement production-quality playback behavior.

Support:

* active/inactive playback state
* play/pause
* muted startup where required
* mute/unmute
* loading
* buffering
* poster/thumbnail
* playback error
* cleanup
* responsive layout
* browser capability constraints

Only initialize or play videos that need to be active.

Do not allow off-screen videos to continue consuming media resources indefinitely.

## 7.3 Active Video Detection

Use the established frontend architecture to determine which short-form video is active.

Where appropriate, use:

* intersection-based activation
* viewport visibility
* explicit user selection
* keyboard navigation

The implementation must prevent multiple off-screen videos from playing simultaneously unless the product contract explicitly requires otherwise.

## 7.4 Video Navigation

Support:

* vertical swipe/pointer interaction where the established web design calls for it
* keyboard navigation
* next/previous controls where appropriate
* URL or route synchronization where defined
* restoration of the current position when navigation semantics require it

Do not make gesture behavior inaccessible to keyboard and assistive-technology users.

# 8. SHORT-FORM VIDEO ENGAGEMENT

Integrate the content-engagement functionality already owned by the project's backend contracts.

Where supported by the existing system, the video experience must be able to expose:

* like state
* like count
* comments
* save state
* share action
* creator navigation

Reuse the engagement infrastructure and state-management patterns established by the existing frontend.

Do not build a second implementation of likes, saves, comments, or sharing when existing reusable components already provide the required behavior.

# 9. CREATOR AND CONTENT NAVIGATION

Support navigation from stories and short-form content to relevant existing product surfaces.

Examples include:

* creator profile
* post/content detail
* media detail
* associated content where explicitly defined by the contract

Navigation must respect:

* authentication
* content visibility
* route conventions
* stable identifiers
* existing application layouts

Do not hardcode route paths that contradict the existing routing architecture.

# 10. DATA FETCHING

Use the established data-fetching layer for stories and short-form video.

Implement:

* typed API calls
* query keys
* cache behavior
* pagination
* invalidation
* mutation handling
* request deduplication
* cancellation where appropriate
* stale-response protection
* retry behavior

Respect server-provided cursors and pagination semantics.

Do not independently infer pagination from array lengths or UI state when the API provides explicit pagination metadata.

# 11. CLIENT STATE

Create only the client state required for ephemeral interaction behavior.

Examples include:

* active story index
* active video
* playback status
* pause state
* mute state
* progress
* currently visible media
* transient error state
* viewer open/closed state

Do not duplicate server state in a second global store merely for convenience.

Server-backed state should remain in the application's established server-state/cache system.

# 12. MEDIA LIFECYCLE

Media resources must be managed deliberately.

For every implemented media component:

* initialize resources only when needed
* clean up on unmount
* release obsolete media references
* avoid duplicate event listeners
* stop inactive playback
* prevent timer leaks
* prevent stale callback execution
* prevent multiple simultaneous playback controllers

Pay special attention to route transitions and rapid user navigation.

# 13. RESPONSIVE WEB BEHAVIOR

The stories and short-form video experiences must work across:

* desktop
* laptop
* tablet
* mobile web
* touch and pointer input

Adapt appropriately to viewport dimensions.

The implementation must correctly handle:

* portrait media
* landscape media where supported
* narrow screens
* browser chrome/viewport changes
* safe-area considerations where relevant
* control placement
* readable text
* touch-safe controls
* keyboard access

Do not simply scale a desktop viewer down to mobile dimensions.

# 14. ACCESSIBILITY

Implement accessible story and short-form video experiences.

Provide:

* semantic controls
* accessible names
* logical keyboard navigation
* visible focus indicators
* accessible progress information
* pause controls
* meaningful media alternatives where appropriate
* screen-reader announcements for significant state transitions
* accessible errors
* accessible close controls
* non-pointer navigation alternatives

Do not make essential content navigation dependent on gesture input alone.

Support reduced-motion preferences where animation behavior is optional.

# 15. PERFORMANCE

Optimize aggressively where media behavior could affect real-world performance.

Pay particular attention to:

* video startup
* image decoding
* unnecessary preloading
* off-screen media
* repeated media initialization
* expensive React rerenders
* viewer transitions
* timers
* event listeners
* network duplication
* large media metadata
* cache behavior

Use preloading selectively.

Do not preload an arbitrary number of full-size videos.

Prefer thumbnails/posters and appropriate media variants until full playback is justified.

# 16. NETWORK AND SLOW-CONNECTION BEHAVIOR

The implementation must remain usable under degraded network conditions.

Handle:

* slow media startup
* stalled playback
* failed requests
* transient network failures
* pagination delays
* retry
* partially loaded content
* unavailable media

Do not block unrelated application interaction while a media resource loads.

Do not convert every transient media issue into a full-page failure.

# 17. ERROR HANDLING

Normalize and present errors through the application's established error infrastructure.

Handle:

* unauthorized content
* forbidden content
* missing stories
* expired stories
* deleted stories
* removed stories
* invalid content IDs
* network failures
* timeout
* rate limiting
* server failures
* media failures
* playback failures
* pagination failures
* view-state mutation failures

Do not display raw stack traces or unsafe server payloads.

# 18. SECURITY AND PRIVACY

Treat story and video content as potentially private user-generated content.

The implementation must:

* respect server-provided visibility
* respect authorization responses
* never expose private media through client-side shortcuts
* avoid logging private media URLs unnecessarily
* avoid leaking signed URLs into telemetry
* avoid exposing internal storage metadata
* avoid unsafe HTML
* avoid embedded secrets
* follow existing session and CSRF protections
* follow established security-header expectations

Client-side visibility checks are not authorization controls.

# 19. OBSERVABILITY

Integrate with the established frontend observability system.

Capture useful technical telemetry for:

* story-load failures
* story-view registration failures
* media-load failures
* playback failures
* video-feed failures
* pagination failures
* significant viewer exceptions
* relevant performance events

Telemetry must not include:

* authentication tokens
* session secrets
* private message content
* unnecessary private content data
* unrestricted backend payloads
* sensitive signed media URLs

Use stable identifiers only where the existing observability architecture permits them.

# 20. TESTING

Add meaningful automated tests covering the implemented behavior.

At minimum, cover:

## Stories

* story-entry rendering
* viewed/unviewed state
* viewer opening
* story ordering
* next navigation
* previous navigation
* close behavior
* progress handling
* pause/resume
* image stories
* video stories
* expired stories
* unavailable stories
* story-view registration
* failure and retry
* duplicate-view prevention where appropriate
* cleanup of timers and media listeners

## Short-Form Video

* feed loading
* pagination
* active-video selection
* playback state
* pause/play
* mute/unmute
* buffering state
* failed playback
* navigation
* cleanup
* prevention of simultaneous off-screen playback
* engagement integration

## Accessibility

Test:

* keyboard navigation
* accessible controls
* focus behavior
* accessible errors
* pause controls
* non-gesture navigation

## Integration

Test relevant API contract transformations and error semantics.

Do not rely exclusively on snapshots.

# 21. CONTRACT VALIDATION

Validate implementation against the repository's authoritative contracts.

Verify:

* story endpoints
* story response shape
* story sequencing
* story identifiers
* story timestamps
* story expiration semantics
* view-state endpoints
* video-feed endpoints
* pagination
* media URLs
* playback-related metadata
* authorization requirements
* engagement contracts
* error codes

Do not invent fields because they would simplify the UI.

Do not silently reinterpret backend timestamps or durations.

Use the established identifier and time conventions.

# 22. SHARED COMPONENT INTEGRATION

Reuse existing components from the frontend foundation and previous content implementation where appropriate.

Possible reusable primitives include:

* Avatar
* MediaImage
* MediaVideo
* LoadingState
* ErrorState
* Modal/Dialog
* Button
* PostActions
* EngagementSummary
* CreatorHeader

Extend shared primitives when the added behavior is genuinely reusable.

Do not duplicate a component solely because a specialized surface needs slightly different styling.

# 23. ROUTING

Integrate story and short-form video navigation with the established Next.js routing model.

Support:

* deep-linkable states where the application's routing contract requires them
* browser back/forward behavior
* route transitions
* direct navigation to valid media contexts
* invalid route handling

Do not create route structures that conflict with existing application navigation.

# 24. OUT OF SCOPE

Do not implement the following in this prompt except for minimal integration required by this volume:

* advanced Explore/discovery UI
* search UI
* direct messaging
* group messaging
* notification center
* moderation/admin dashboards
* analytics dashboards
* mobile React Native implementation
* backend story/video services
* database migrations
* Kafka infrastructure
* Redis infrastructure
* OpenSearch infrastructure
* cloud deployment
* CDN infrastructure
* unrelated account/profile redesign
* unrelated feed architecture changes

Do not create placeholder pages for out-of-scope domains.

# 25. DOCUMENTATION

Update documentation needed to explain the implemented frontend scope.

Document, as applicable:

* story viewer architecture
* story sequencing
* progress lifecycle
* view-state integration
* short-form video activation behavior
* media lifecycle management
* performance decisions
* accessibility decisions
* caching and pagination
* relevant contract assumptions
* testing strategy

Documentation must describe actual behavior rather than aspirational behavior.

# 26. IMPLEMENTATION DISCIPLINE

Do not:

* leave TODOs for required functionality
* leave FIXME markers for unresolved required functionality
* use fake story/video APIs
* hardcode production content
* hardcode user IDs
* hardcode media URLs
* fake story expiration
* fake view persistence
* fake video-feed pagination
* disable authentication
* bypass authorization
* expose secrets
* suppress type errors without justification
* disable lint rules without justification
* create a parallel media architecture without reason
* claim browser functionality that was not tested

Do not use static mock data as the production data source.

Test fixtures belong only in tests.

# 27. VALIDATION

Before considering the implementation complete:

* run type-checking
* run linting
* run relevant unit/component tests
* run relevant integration tests
* verify production build compatibility
* exercise story opening and navigation
* verify progress/timer cleanup
* verify story-view behavior
* verify expiration handling
* verify short-form video activation
* verify playback cleanup
* verify pagination
* verify engagement integration
* verify keyboard accessibility
* inspect for console errors
* inspect for leaked timers/listeners
* inspect for accidental media overfetching
* inspect for secrets
* inspect for placeholder code
* inspect for contract mismatches

Fix defects discovered during validation.

Never report a command as successful unless it was actually executed.

# 28. IMPLEMENTATION REPORT

At the end of the work, provide a concise engineering report containing:

## Implemented

Summarize the concrete Stories and short-form video functionality implemented.

## Files Changed

List meaningful files created or modified and explain their purpose.

## Contracts Integrated

Identify the story, media, video, engagement, authorization, and pagination contracts actually used.

## Tests

List tests executed and their outcomes.

## Validation

List type-check, lint, build, integration, accessibility, and media validation actually performed.

## Important Decisions

Document significant implementation decisions and tradeoffs.

## Limitations

Document genuine limitations resulting from missing repository capabilities or authoritative contracts.

Do not represent future work as completed functionality.

# 29. DEFINITION OF DONE

This prompt is complete only when:

* story entry surfaces are implemented
* story viewer is operational
* story ordering and navigation are correct
* story progress behaves deterministically
* image and video stories render correctly
* story view state integrates with the backend contract
* expired and unavailable stories are handled correctly
* short-form video consumption is operational through real application contracts
* active-video behavior prevents unnecessary simultaneous playback
* video playback handles loading, buffering, pause, resume, mute, and failure states
* engagement controls reuse the existing engagement infrastructure
* responsive behavior is implemented
* keyboard and accessibility behavior is implemented
* telemetry and error handling are integrated
* automated tests cover meaningful behavior
* type-checking succeeds
* linting succeeds
* production build compatibility is preserved
* no fake APIs or persistence remain
* no required TODO/FIXME stubs remain
* no secrets are exposed
* existing frontend functionality remains compatible
* documentation reflects the actual implementation
* the implementation report accurately describes completed work

# 30. FINAL EXECUTION DISCIPLINE

Implement this prompt as a bounded production engineering task.

Do not expand the scope into unrelated frontend domains.

Do not ask the user to choose among implementation approaches when repository conventions and authoritative contracts already establish the appropriate direction.

Make reasonable engineering decisions from the existing codebase and contract artifacts.

When ambiguity materially affects compatibility, prefer the established repository contract and existing frontend pattern.

Do not claim completion until the Definition of Done has been satisfied and the stated validation has actually been performed.
