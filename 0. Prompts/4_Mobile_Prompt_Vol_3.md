# Instagram — Mobile Prompt — Volume 3

# 1. ROLE

You are the **Senior Mobile Engineering implementation team** responsible for implementing the bounded mobile scope defined in this prompt for the Instagram project.

Operate as a production engineering organization with expertise in:

* React Native
* TypeScript
* mobile media applications
* Stories and ephemeral content
* short-form vertical video
* gesture-driven interfaces
* high-performance video playback
* media caching and lifecycle management
* realtime interaction
* server-state synchronization
* accessibility
* battery and memory optimization
* automated mobile testing
* observability
* privacy and secure media handling

Your responsibility is to implement the assigned mobile scope completely and coherently inside the repository while preserving compatibility with the mobile foundation, existing content infrastructure, backend contracts, and shared domain model.

Do not implement unrelated mobile product domains merely because they exist in the global product definition.

Do not create fake APIs, fake persistence, placeholder screens, TODO-driven implementations, or simulated media behavior presented as production functionality.

# 2. PROJECT IDENTITY

The project is a production-grade **Instagram-style social media platform**.

The mobile client is a TypeScript-based React Native application targeting supported iOS and Android platforms.

The product includes:

* identity and accounts
* profiles
* social graph
* home feed
* posts and media
* Stories
* short-form video
* likes, comments, saves, and shares
* discovery and search
* direct messaging
* notifications
* moderation and reporting
* privacy and safety controls
* offline-aware behavior
* realtime communication
* deep links
* push notifications
* secure mobile storage
* mobile observability
* accessibility
* performance and reliability

This prompt is limited to the **mobile Stories and short-form vertical-video experience**.

# 3. CURRENT MOBILE ASSIGNMENT

Implement the production mobile experience for:

* Stories entry surface
* story tray
* story viewer
* story sequencing
* story progress
* story image/video playback
* story navigation
* story pause/resume
* story view registration
* story expiration and availability
* short-form vertical-video feed
* active-video selection
* vertical navigation
* video playback controls
* video pagination
* media lifecycle
* media preloading within safe limits
* engagement integration
* creator navigation
* deep-link-compatible content entry where supported
* accessibility
* performance
* observability
* automated testing

This prompt does not implement Explore/search, direct messaging, notification center, moderation/admin, or other unrelated mobile product areas.

# 4. REPOSITORY INSPECTION

Before modifying code, inspect the repository sufficiently to understand:

* mobile application foundation
* authenticated navigation
* feed/post components
* media components
* image caching
* video playback infrastructure
* API client
* server-state/data-fetching infrastructure
* client-state architecture
* route/deep-link handling
* connectivity awareness
* telemetry
* accessibility utilities
* design system
* native iOS/Android media capabilities
* test infrastructure
* relevant documentation

Inspect authoritative contracts covering:

* stories
* story sequences
* story visibility
* story expiration
* story media
* story views
* short-form video
* media delivery
* pagination
* identifiers
* timestamps
* authorization
* privacy
* errors
* engagement

Treat those contracts and existing repository implementations as authoritative.

Do not invent video-feed ranking, story-ordering, media fields, or view semantics.

# 5. TECHNOLOGY BASELINE

Use the established mobile technology:

* React Native
* TypeScript
* established navigation
* established API client
* established server-state architecture
* established client-state architecture
* established media primitives
* established telemetry
* established test framework

Use native/platform APIs only where required for correct mobile media behavior.

Do not introduce a competing video-player stack or state-management system without a strong compatibility and maintenance justification.

# 6. STORIES ENTRY SURFACE

Implement the mobile Stories discovery surface.

Support the contract-defined presentation of available stories, including as applicable:

* story avatars
* creator identity
* viewed/unviewed state
* story availability
* ordering
* horizontal scrolling
* loading state
* empty state
* retry
* accessibility

Use the server-provided sequence and availability.

Do not implement independent client-side story ranking.

# 7. STORY VIEWER

Implement the primary mobile Story viewer.

Support:

* opening a story sequence
* current-story state
* previous/next navigation
* movement between creators
* close behavior
* progress indicators
* pause/resume
* image stories
* video stories
* loading
* buffering
* failure
* unavailable content
* expired content
* safe-area-aware controls
* portrait-oriented presentation
* touch interaction

The viewer must maintain a single authoritative current position.

# 8. STORY PROGRESS

Implement deterministic story-progress behavior.

Support:

* image-duration timing
* video-duration-based progression where applicable
* progress reset
* pause/resume
* transition to the next story
* previous-story restoration behavior according to the product contract
* cleanup
* protection against multiple timers
* handling of rapid navigation
* handling of unavailable content

There must never be multiple active timers advancing the same story sequence.

# 9. STORY MEDIA

Implement mobile story media rendering.

For images:

* appropriate aspect-ratio handling
* responsive sizing
* efficient decoding
* loading placeholder
* failure state
* accessibility

For videos:

* controlled playback
* muted startup when required
* play/pause
* buffering
* duration/progress integration
* media cleanup
* failure recovery
* memory-aware resource handling

Do not unnecessarily preload numerous full-resolution story assets.

# 10. STORY NAVIGATION GESTURES

Implement mobile-appropriate story navigation.

Support the project's defined gesture behavior, such as:

* tap/press zones
* swipe navigation where required
* press-and-hold pause
* close gesture where appropriate
* navigation controls

Ensure controls do not conflict with media interaction.

Do not make the viewer dependent exclusively on gestures when accessible alternatives are required.

# 11. STORY VIEW STATE

Integrate story-view registration with the real backend contract.

Support:

* marking a story as viewed at the contract-defined point
* avoiding unnecessary duplicate requests
* retrying recoverable failures
* reconciliation with server state
* correct behavior when the viewer advances rapidly
* cleanup on viewer exit

The client must not treat local view state as authoritative.

# 12. STORY EXPIRATION AND AVAILABILITY

Correctly handle:

* expired stories
* deleted stories
* removed stories
* unauthorized stories
* unavailable media
* story sequence changes while open

When a current story becomes invalid, move to the next valid state or present an explicit unavailable state.

Never leave the user on a permanent spinner or blank viewer.

# 13. STORY SEQUENCE CONSISTENCY

Protect against inconsistent sequence data.

Handle:

* duplicate story identifiers
* overlapping page responses where pagination exists
* stale cached sequences
* creator removal
* story deletion
* sequence shrinking
* refreshed story order

Do not insert duplicate story items.

Do not allow stale sequence responses to overwrite newer state.

# 14. SHORT-FORM VIDEO FEED

Implement the mobile short-form vertical-video experience.

Support:

* initial feed retrieval
* vertical content presentation
* one active primary video at a time
* pagination
* loading
* end-of-results
* empty state
* failure and retry
* unavailable-video handling
* creator navigation
* engagement controls supported by the contracts

The backend remains authoritative for content ordering and ranking.

Do not create a local recommendation engine.

# 15. ACTIVE VIDEO MANAGEMENT

Implement deterministic active-video selection.

Support appropriate mechanisms such as:

* viewport visibility
* scroll position
* explicit user selection
* lifecycle events

The system must:

* activate the intended visible video
* pause videos that are no longer active
* avoid multiple simultaneous playback sessions
* release resources when a video leaves the active region
* handle rapid scrolling
* handle navigation away from the screen

Do not leave hidden videos consuming playback resources.

# 16. VIDEO PLAYBACK

Implement production-quality mobile video playback.

Support:

* poster image
* loading
* buffering
* play
* pause
* mute
* unmute
* seek behavior where supported
* playback error
* retry
* cleanup
* responsive aspect ratio
* app lifecycle behavior

Respect iOS and Android media policies.

Do not assume that background playback is permitted.

# 17. VIDEO PRELOADING

Implement controlled preloading where it improves UX without creating excessive resource usage.

Preload only when justified by:

* near-future visibility
* established media infrastructure
* available network conditions
* available device resources

Avoid:

* preloading the entire feed
* downloading large videos unnecessarily
* preloading sensitive/private content indiscriminately
* uncontrolled memory growth

# 18. VIDEO PAGINATION

Implement the contract-defined pagination mechanism.

Support:

* first page
* loading additional pages
* cursor preservation
* duplicate prevention
* end-of-content
* retry
* stale-response protection

Do not mix cursors between different authenticated contexts or query sessions.

# 19. VIDEO ENGAGEMENT

Where supported by existing backend/frontend contracts, integrate:

* likes
* comments
* saves
* shares
* creator navigation

Reuse the engagement infrastructure implemented by the previous mobile content work.

Do not create another implementation of like/save/comment behavior.

Engagement state must remain synchronized with shared post/content state.

# 20. CONTENT CREATOR NAVIGATION

Support navigation from Stories and short-form video to:

* creator profile
* canonical content detail
* other explicitly defined product destinations

Use established navigation and identifier conventions.

Do not create ad hoc routes.

Do not expose internal storage or service identifiers through navigation.

# 21. DEEP-LINK INTEGRATION

Where the mobile deep-link foundation supports media entry, implement:

* direct story/content entry
* authentication-gated continuation
* invalid-content handling
* unavailable-content handling
* correct navigation restoration

Do not place authentication tokens or other secrets in deep links.

# 22. CACHE AND SERVER-STATE MANAGEMENT

Use the existing server-state system for:

* story lists
* story sequences
* story state
* story-view mutations
* short-form video feeds
* video pagination
* engagement state

Ensure cache keys include all relevant authenticated/query context.

Do not allow story or video data from one account context to appear under another account.

# 23. OFFLINE AND DEGRADED NETWORK

Use the mobile connectivity foundation to handle degraded conditions.

Support, where appropriate:

* showing already cached metadata
* offline indication
* retry after reconnect
* preserving current state
* graceful media failure
* avoiding endless loading

Do not imply that uncached media is available offline.

Do not implement durable offline video/story synchronization unless the underlying architecture supports it.

# 24. BATTERY AND MEMORY MANAGEMENT

Media-heavy mobile experiences require deliberate resource management.

Optimize:

* active-player count
* video decoding
* image decoding
* timers
* gesture subscriptions
* native event listeners
* preloading
* cache pressure
* screen transitions

Ensure resources are released when:

* a screen unmounts
* the viewer closes
* a video becomes inactive
* the app backgrounds
* navigation moves to another domain

Do not trade battery or memory safety for marginal preloading gains.

# 25. APP LIFECYCLE AND MEDIA

Handle:

* app foreground
* app background
* interruption
* incoming system UI
* navigation away
* screen unmount

Correctly pause/resume or release media according to platform behavior.

Never leave media playback active in a hidden screen unless explicitly required.

# 26. ACCESSIBILITY

Implement accessible Story and short-form video experiences.

Support:

* accessible close control
* meaningful media labels
* pause controls
* navigation alternatives
* screen-reader-friendly progress information
* accessible like/save/share actions
* accessible creator navigation
* accessible unavailable/error states

Do not rely only on gesture interaction.

Respect relevant reduced-motion/accessibility settings where the product experience permits.

# 27. RESPONSIVE AND SAFE-AREA BEHAVIOR

Support different mobile screen sizes and platform safe areas.

Ensure:

* controls avoid notches/cutouts
* bottom controls avoid home indicators
* text remains readable
* media fills the intended viewport without unexpected clipping
* orientation behavior follows application policy
* interactive targets remain reachable

# 28. PRIVACY AND SECURITY

Stories and short-form video may contain private or restricted content.

The client must:

* respect backend visibility
* respect authorization failures
* not construct unauthorized media URLs
* not expose signed/private URLs through telemetry
* not persist sensitive media unnecessarily
* avoid storing private content in insecure shared storage
* not expose internal media metadata
* never embed storage credentials or privileged tokens

Client-side hiding is not authorization.

# 29. OBSERVABILITY

Integrate mobile media telemetry with the existing observability system.

Capture useful technical signals for:

* story-load failures
* story-view registration failures
* video-feed failures
* media-load failures
* playback errors
* pagination failures
* significant media performance issues
* navigation/media lifecycle errors

Do not capture:

* private media contents
* access tokens
* passwords
* signed private-media URLs
* unnecessary story/comment/caption contents

Follow project privacy requirements.

# 30. TESTING

Add meaningful automated tests covering:

## Stories

* story tray loading
* viewed/unviewed rendering
* viewer opening
* next/previous navigation
* progress timing
* pause/resume
* image stories
* video stories
* view registration
* duplicate-view prevention where appropriate
* expiration
* unavailable story
* deleted/removed story
* timer cleanup
* media cleanup

## Short-Form Video

* initial loading
* pagination
* active-video selection
* playback
* pause/resume
* mute/unmute
* buffering
* playback failure
* retry
* off-screen playback prevention
* cleanup
* engagement actions
* creator navigation

## Lifecycle

* backgrounding
* foregrounding
* navigation away
* screen unmount
* interruption handling

## Accessibility

* accessible controls
* non-gesture navigation
* state announcements
* meaningful labels

Do not rely exclusively on snapshots.

# 31. CONTRACT VALIDATION

Validate implementation against authoritative contracts for:

* stories
* story media
* story ordering
* story views
* expiration
* short-form video
* media delivery
* pagination
* identifiers
* timestamps
* engagement
* authorization
* privacy
* errors

Do not invent:

* story ordering
* durations
* video ranking
* view semantics
* content visibility
* media URL structures
* endpoint behavior

# 32. PERFORMANCE VALIDATION

Where profiling tools are available, inspect:

* feed scroll performance
* active-video switching
* memory usage
* image/video decoding behavior
* playback startup
* media cleanup
* network utilization
* battery-sensitive behavior

At minimum verify that:

* inactive videos stop playback
* timers are cleaned up
* media resources are released
* pagination does not trigger duplicate requests
* unnecessary full-resolution media is not downloaded

Do not claim profiling results that were not actually measured.

# 33. SHARED MOBILE INTEGRATION

Reuse:

* authentication
* navigation
* API client
* server-state management
* engagement components
* profile navigation
* media abstractions where compatible
* telemetry
* accessibility utilities
* connectivity state
* error handling

Do not duplicate the foundation already established in earlier mobile work.

# 34. OUT OF SCOPE

Do not implement:

* mobile Explore/search
* mobile direct messaging
* mobile notification center
* mobile moderation/admin
* backend changes
* database migrations
* media-processing infrastructure
* Kafka infrastructure
* Redis infrastructure
* cloud deployment
* CI/CD production infrastructure
* unrelated web frontend changes
* unrelated account/profile redesign

Do not create placeholder screens for these domains.

# 35. DOCUMENTATION

Update documentation required to explain:

* Story viewer architecture
* story progress behavior
* story-view synchronization
* short-form video lifecycle
* active-video selection
* preloading strategy
* memory/battery considerations
* cache behavior
* deep-link integration
* accessibility decisions
* performance decisions
* relevant contracts
* testing strategy

Document only actual implemented behavior.

# 36. IMPLEMENTATION DISCIPLINE

Do not:

* hardcode stories
* hardcode video content
* hardcode view counts
* hardcode media URLs
* fake story expiration
* fake story-view persistence
* fake video pagination
* fake playback state
* expose secrets
* bypass authorization
* leave required TODO/FIXME placeholders
* suppress type/lint errors without justification
* leave inactive videos playing
* create an independent media state architecture
* claim offline media availability without implementation

Fixtures belong in tests.

# 37. VALIDATION

Before considering the implementation complete:

* run TypeScript validation
* run linting
* run relevant mobile unit/component tests
* run integration tests
* validate available iOS builds
* validate available Android builds
* exercise Story opening/navigation
* verify progress and timer cleanup
* verify view-state registration
* verify expiration handling
* exercise short-form video pagination
* verify active-video behavior
* verify playback and cleanup
* verify engagement integration
* verify deep-link behavior where supported
* inspect memory/media lifecycle
* inspect for unnecessary media downloads
* inspect for duplicate network calls
* inspect for secrets
* inspect for unsafe media access
* inspect for placeholder code
* inspect for contract mismatches

If a platform build or profiling workflow cannot be executed because the environment lacks the required tooling, report that limitation accurately.

# 38. IMPLEMENTATION REPORT

At the end of the work, provide:

## Implemented

Summarize the Stories and short-form vertical-video functionality actually implemented.

## Files Changed

List meaningful created and modified files with their purposes.

## Contracts Integrated

Identify story, media, view-state, video-feed, pagination, authorization, engagement, and error contracts integrated.

## Tests

List tests executed and their results.

## Validation

List TypeScript, lint, unit, integration, iOS, Android, accessibility, media-performance, memory, and lifecycle validation actually performed.

## Important Decisions

Document significant engineering decisions and tradeoffs.

## Limitations

Document genuine limitations caused by repository constraints, unavailable native tooling, or unavailable external capabilities.

Do not represent future work as completed functionality.

# 39. DEFINITION OF DONE

This prompt is complete only when:

* the mobile Stories entry surface is operational
* the Story viewer is functional
* story sequencing and navigation work
* story progress is deterministic
* image and video stories render correctly
* story view state integrates with the backend
* expired/unavailable stories are handled correctly
* short-form vertical-video feed is operational
* video pagination works
* active-video selection works
* inactive videos are stopped and cleaned up
* playback states are handled correctly
* engagement integrates with shared content infrastructure
* creator navigation works
* deep-link integration works where supported
* degraded-network behavior is handled within actual platform capabilities
* accessibility requirements are addressed
* privacy/security requirements are respected
* observability is integrated
* automated tests cover meaningful behavior
* TypeScript validation succeeds
* linting succeeds
* available iOS/Android builds remain valid
* no fake production APIs or persistence remain
* no required TODO/FIXME stubs remain
* no secrets are exposed
* documentation reflects actual behavior
* the implementation report accurately describes completed work

# 40. FINAL EXECUTION DISCIPLINE

Implement this prompt as a bounded production mobile engineering task.

Do not expand into the later mobile domains listed as out of scope.

Do not ask the user to choose among implementation approaches when repository conventions and authoritative contracts establish the correct direction.

Make reasonable engineering decisions based on the repository and project contracts.

Where ambiguity materially affects media behavior, privacy, performance, or compatibility, follow the established contract and mobile architecture.

Do not claim completion until the Definition of Done has been satisfied and the stated validation has actually been performed.
