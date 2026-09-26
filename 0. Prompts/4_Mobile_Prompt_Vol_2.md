# Instagram — Mobile Prompt — Volume 2

# 1. ROLE

You are the **Senior Mobile Engineering implementation team** responsible for implementing the bounded mobile scope defined in this prompt for the Instagram project.

Operate as a production engineering organization with expertise in:

* React Native
* TypeScript
* mobile social-feed architecture
* high-performance media rendering
* image and video pipelines
* virtualized lists
* gesture and touch interaction
* optimistic UI
* server-state synchronization
* offline-aware behavior
* accessibility
* mobile performance
* automated testing
* observability
* secure API integration

Your responsibility is to implement the assigned mobile scope completely and coherently inside the repository while preserving compatibility with the existing mobile foundation, backend contracts, and shared domain model.

Do not implement unrelated mobile product domains merely because they exist in the global product definition.

Do not create fake APIs, fake persistence, placeholder screens, TODO-driven implementations, or simulated production behavior.

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

This prompt is limited to the **mobile home feed, post rendering, media consumption, post detail, and engagement experience**.

# 3. CURRENT MOBILE ASSIGNMENT

Implement the production mobile experience for:

* home feed
* feed pagination
* post rendering
* post media
* image consumption
* video consumption where part of normal posts
* post detail
* likes
* comments
* replies
* saves
* shares
* engagement synchronization
* optimistic interactions
* content loading/error/empty states
* responsive mobile layouts
* accessibility
* media performance
* automated testing
* observability
* reliable API integration

This prompt does not implement Stories, Reels-specific mobile experiences, Explore/search, messaging, notifications, or moderation/admin interfaces.

# 4. REPOSITORY INSPECTION

Before modifying code, inspect the repository sufficiently to understand:

* mobile application foundation
* authenticated navigation
* screen and route conventions
* API client
* server-state/data-fetching infrastructure
* client-state infrastructure
* profile and social-graph components
* shared mobile design primitives
* image/media abstractions
* typography
* theming
* loading/error primitives
* authentication/session handling
* telemetry
* accessibility utilities
* test setup
* iOS and Android configurations
* relevant documentation

Inspect authoritative contracts for:

* feed
* posts
* media
* engagement
* comments
* replies
* saves
* shares
* pagination
* identifiers
* timestamps
* authorization
* privacy
* errors
* media delivery

Treat the repository and project contracts as authoritative.

Do not invent backend fields or endpoint semantics.

# 5. TECHNOLOGY BASELINE

Use the established mobile technology:

* React Native
* TypeScript
* established navigation
* established API client
* established server-state architecture
* established client-state architecture
* established mobile design system
* established telemetry
* established test framework

Use platform-native behavior where appropriate without splitting shared business logic unnecessarily.

Maintain strict typing.

# 6. MOBILE HOME FEED

Implement the authenticated home feed.

Support:

* initial feed load
* refresh
* pagination
* cursor handling
* feed-item rendering
* loading state
* empty state
* error state
* retry
* end-of-feed state
* duplicate-item prevention
* stale-response protection
* preservation of visible content during background refresh

The backend remains authoritative for feed ordering.

Do not implement a client-side ranking system.

# 7. FEED PERFORMANCE

The feed must be designed for a large media-heavy social application.

Use appropriate React Native techniques for:

* virtualized lists
* stable item keys
* minimal rerenders
* incremental loading
* image prefetching where justified
* efficient media lifecycle
* controlled memory consumption

Avoid rendering the entire feed into an unbounded in-memory view hierarchy.

Do not use array indexes as identifiers when the contract provides stable content IDs.

# 8. REFRESH AND PAGINATION

Implement the established cursor-based or contract-defined pagination model.

Support:

* pull-to-refresh where appropriate
* initial pagination
* loading-more state
* retry after pagination failure
* end-of-results
* duplicate-page protection
* duplicate-item protection
* stale-response protection

A background refresh must not unnecessarily destroy visible content.

Do not mix cursors belonging to different feed contexts or sessions.

# 9. FEED ITEM

Implement a reusable feed-item component.

Support:

* author avatar
* username/display name
* author navigation
* timestamp
* media
* caption
* mentions
* hashtags where supported
* engagement controls
* engagement counts
* save state
* share action
* accessibility
* unavailable-content state

Reuse profile and shared identity components from the mobile foundation.

# 10. POST MEDIA

Implement production-quality post media rendering.

Support:

* image posts
* supported video posts
* portrait media
* landscape media
* square media
* aspect-ratio preservation
* responsive sizing
* loading placeholders
* failure states
* appropriate media URLs
* memory-conscious rendering
* navigation to detail/full media

Do not load unnecessarily large media variants when a smaller contract-defined representation is sufficient.

# 11. IMAGE PERFORMANCE

Use the mobile image infrastructure established in the repository.

Optimize:

* decoding
* memory use
* caching
* placeholder behavior
* progressive loading where available
* repeated rendering
* off-screen media

Avoid aggressively preloading every image in a long feed.

Ensure media dimensions are known early enough to reduce layout instability.

# 12. VIDEO POSTS

For standard post videos supported by this scope, implement:

* poster/preview
* playback
* pause
* mute/unmute
* loading
* buffering
* failure
* cleanup
* responsive sizing
* screen-reader/accessibility considerations

Respect platform media behavior.

Do not leave multiple off-screen videos playing simultaneously.

Do not assume unlimited autoplay behavior.

# 13. POST DETAIL

Implement the mobile post-detail experience.

Support:

* canonical content
* author context
* full supported media
* caption
* engagement state
* comments
* replies
* save
* share
* loading
* failure
* unavailable/deleted content
* navigation back to originating context where appropriate

Reuse feed and post components instead of duplicating domain logic.

# 14. LIKES

Implement like/unlike behavior.

Support:

* current like state
* like count
* optimistic update where safe
* rollback
* request deduplication
* duplicate-tap protection
* authoritative response reconciliation
* synchronization across feed/detail contexts

Do not allow stale mutation responses to overwrite newer state.

# 15. COMMENTS

Implement comments on posts.

Support:

* comment retrieval
* pagination
* author identity
* comment body
* timestamps
* empty state
* loading state
* failure and retry
* comment composition
* submission
* validation
* optimistic insertion where appropriate
* authoritative reconciliation
* removed/unavailable comment state

Treat comment content as untrusted user-generated content.

Never render arbitrary comment text as executable HTML.

# 16. REPLIES

Implement supported comment replies.

Support:

* expanding replies
* loading replies
* pagination
* reply composition
* submission
* loading/error states
* synchronization of relevant counts
* accessible interaction

Keep nesting behavior bounded and understandable.

Do not create uncontrolled recursive message trees.

# 17. SAVES

Implement save/unsave functionality.

Support:

* current save state
* optimistic behavior where safe
* rollback
* authoritative reconciliation
* synchronization across visible content contexts
* failure handling

Do not create local-only persistence for saved content.

# 18. SHARING

Implement contract-defined post sharing.

Support the appropriate combination of:

* share sheet
* native share capabilities
* copy-link behavior
* application-specific share action
* fallback behavior
* success/failure feedback

Do not expose private content through generated links.

Use canonical identifiers and URLs defined by the project.

# 19. ENGAGEMENT STATE

Keep engagement state consistent across:

* home feed
* post detail
* profile-related content already implemented
* other mobile surfaces that reuse the shared post components

Synchronize:

* like state
* like count
* comment count
* save state
* relevant freshness metadata

Use the existing server-state/cache architecture.

Do not create a separate mobile-only engagement database or cache.

# 20. OPTIMISTIC MUTATIONS

Optimistic interactions must:

1. capture prior state,
2. update UI when safe,
3. submit the real mutation,
4. reconcile with authoritative response,
5. rollback on failure,
6. display appropriate feedback,
7. protect against stale responses.

Do not use optimistic behavior where the operation has semantics that make local prediction unsafe.

# 21. USER-GENERATED CONTENT SAFETY

Treat captions, comments, replies, usernames, and other user-provided text as untrusted.

The implementation must:

* safely render text
* safely handle URLs
* avoid executable HTML
* avoid unsafe native rendering behavior
* avoid leaking internal metadata
* preserve server-defined content visibility

Do not rely on frontend filtering as authorization.

# 22. MEDIA AUTHORIZATION

Respect backend authorization for media.

The client must not:

* construct private media URLs manually
* bypass signed URL/session requirements
* expose storage credentials
* cache private media in unsafe shared stores
* display media after authoritative access denial

Handle media authorization failures gracefully.

# 23. OFFLINE-AWARE FEED BEHAVIOR

Use the mobile foundation's connectivity state to handle degraded connectivity.

Support where appropriate:

* previously cached feed content
* offline indication
* retry after reconnect
* preservation of visible content
* mutation failure/retry messaging

Do not claim full offline feed functionality unless the underlying data layer actually supports durable offline synchronization.

# 24. ERROR HANDLING

Handle:

* network failure
* timeout
* unauthorized
* forbidden
* deleted content
* unavailable content
* rate limiting
* validation failure
* pagination failure
* media failure
* comment failure
* engagement failure
* server failure

Do not display raw backend payloads.

Do not expose internal stack traces.

# 25. RESPONSIVE MOBILE BEHAVIOR

Support:

* small phones
* large phones
* tablets where supported
* portrait
* landscape where applicable

Ensure:

* controls remain reachable
* media is correctly sized
* captions remain readable
* comments are usable
* touch targets are adequate
* no important content is clipped
* safe-area handling is correct where applicable

# 26. ACCESSIBILITY

Implement:

* accessible post actions
* meaningful media labels
* accessible comment forms
* accessible like/save/share controls
* screen-reader-friendly state announcements
* logical navigation order
* adequate touch targets
* visible/focusable interaction states
* accessible loading and error states

Do not rely solely on icons or color to convey action state.

# 27. NAVIGATION INTEGRATION

Integrate feed and post-detail navigation with the mobile navigation architecture established by the mobile foundation.

Support:

* opening post detail
* returning to feed
* navigating to creator profiles
* deep-link entry into supported content
* preserving context when appropriate
* invalid/unavailable content handling

Do not create a second navigation system.

# 28. STATE AND CACHE MANAGEMENT

Use the established server-state architecture.

Maintain correct cache keys for:

* feed queries
* post detail
* comments
* replies
* engagement mutations

Ensure:

* session boundaries are respected
* private data is not shared between users
* realtime/fresh mutations reconcile with cached data
* logout clears or scopes private state correctly
* stale responses cannot overwrite newer state

# 29. OBSERVABILITY

Integrate this scope with existing mobile observability.

Capture appropriate technical signals for:

* feed failures
* pagination failures
* media failures
* engagement failures
* comment failures
* significant rendering errors
* important performance regressions

Do not collect:

* private message content
* private media content
* authentication tokens
* passwords
* unnecessary comment/caption content
* signed private-media URLs

# 30. TESTING

Add meaningful automated tests covering:

## Feed

* initial load
* refresh
* pagination
* duplicate prevention
* stale-response protection
* empty state
* failure/retry
* end-of-feed behavior

## Posts

* rendering
* media states
* author navigation
* unavailable/deleted states
* post detail navigation

## Engagement

* like
* unlike
* save
* unsave
* optimistic success
* optimistic rollback
* duplicate interactions
* cross-context synchronization

## Comments

* loading
* pagination
* submission
* validation
* failure
* retry
* replies
* removed comments

## Media

* image loading
* image failure
* video playback
* video cleanup
* no unintended simultaneous playback

## Accessibility

* action labels
* keyboard/assistive navigation where supported
* accessible comment composition
* state announcements

Do not rely solely on snapshots.

# 31. CONTRACT VALIDATION

Validate all mobile integration against authoritative contracts for:

* feed
* posts
* media
* likes
* comments
* replies
* saves
* shares
* pagination
* identifiers
* timestamps
* visibility
* authorization
* errors

Do not invent:

* feed ranking
* engagement counts
* endpoint paths
* response fields
* pagination semantics
* content states

# 32. PERFORMANCE VALIDATION

Inspect and validate:

* list virtualization
* rerender frequency
* memory behavior
* image loading
* video lifecycle
* pagination request frequency
* duplicate network requests
* cache reuse
* screen transition behavior

Where mobile profiling tools are available, use them to investigate obvious regressions.

Do not claim profiling results that were not actually obtained.

# 33. SHARED CROSS-MOBILE INTEGRATION

Reuse:

* authentication
* secure storage
* API client
* server-state architecture
* navigation
* design system
* profile components
* telemetry
* accessibility utilities
* error handling

Do not duplicate foundational services.

When shared infrastructure must change, preserve existing authentication and navigation behavior.

# 34. OUT OF SCOPE

Do not implement:

* mobile Stories
* mobile Reels-specific experience
* mobile Explore/search
* mobile direct messaging
* mobile notification center
* mobile moderation/admin
* backend changes
* database migrations
* Kafka infrastructure
* Redis infrastructure
* cloud deployment
* CI/CD production infrastructure
* unrelated web frontend changes

Do not create placeholder interfaces for these domains.

# 35. DOCUMENTATION

Update documentation as needed for:

* feed architecture
* mobile media strategy
* pagination behavior
* optimistic engagement behavior
* comment/reply synchronization
* cache strategy
* accessibility decisions
* performance considerations
* contract dependencies
* testing strategy

Documentation must accurately describe actual implementation.

# 36. IMPLEMENTATION DISCIPLINE

Do not:

* hardcode feed items
* hardcode users
* hardcode engagement counts
* fake API responses in production code
* fake pagination
* fake persistence
* fake media URLs
* bypass authorization
* expose secrets
* render unsafe HTML
* leave required TODO/FIXME placeholders
* suppress type/lint errors without justification
* introduce a duplicate state/cache architecture

Fixtures belong in tests.

# 37. VALIDATION

Before considering the implementation complete:

* run TypeScript validation
* run linting
* run relevant unit/component tests
* run integration tests
* validate available iOS builds
* validate available Android builds
* exercise feed loading and refresh
* exercise pagination
* exercise post detail
* exercise like/save mutations
* exercise comments/replies
* exercise media loading and failure
* inspect for list-performance problems
* inspect for unnecessary media downloads
* inspect for memory leaks
* inspect for stale-state bugs
* inspect for secrets
* inspect for unsafe rendering
* inspect for placeholder code
* inspect for contract mismatches

If a platform build cannot be executed because required native tooling is unavailable, report the limitation accurately.

# 38. IMPLEMENTATION REPORT

At the end of the work, provide:

## Implemented

Summarize the home-feed, post, media, engagement, comments, replies, and sharing functionality actually implemented.

## Files Changed

List meaningful created and modified files with their purposes.

## Contracts Integrated

Identify feed, post, media, engagement, comment, pagination, authorization, and error contracts integrated.

## Tests

List tests executed and their results.

## Validation

List TypeScript, lint, unit, integration, iOS, Android, accessibility, performance, and media validation actually performed.

## Important Decisions

Document significant engineering decisions and tradeoffs.

## Limitations

Document genuine limitations caused by repository constraints or unavailable native tooling/external capabilities.

Do not represent future work as completed functionality.

# 39. DEFINITION OF DONE

This prompt is complete only when:

* the mobile home feed is operational through real application contracts
* feed pagination and refresh work
* feed items render correctly
* image and video post media work
* post detail works
* likes and unlikes work
* saves and unsaves work
* shares use the real contract
* comments work
* replies work where supported
* engagement state is synchronized
* optimistic mutations reconcile correctly
* unavailable and removed content states work
* offline/degraded-network behavior is handled within supported capabilities
* responsive mobile layouts work
* accessibility requirements are addressed
* telemetry is integrated without leaking private data
* automated tests cover meaningful functionality
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

Where ambiguity materially affects compatibility, performance, or privacy, follow the established contract and existing mobile architecture.

Do not claim completion until the Definition of Done has been satisfied and the stated validation has actually been performed.
