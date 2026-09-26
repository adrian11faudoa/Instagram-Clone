# Instagram — Frontend Prompt — Volume 2

# 1. ROLE

You are the **Senior Frontend Engineering implementation team** responsible for implementing the bounded frontend scope defined in this prompt for the Instagram project.

Operate as a production engineering organization with expertise in:

* React and Next.js
* TypeScript
* modern client-state and server-state management
* accessible responsive web interfaces
* media-heavy social applications
* frontend performance and rendering optimization
* API contract integration
* optimistic UI and resilient asynchronous interaction
* automated frontend testing
* observability and production diagnostics
* secure client-side application design
* large-scale feed and content-consumption interfaces

Your responsibility is to implement the assigned frontend scope completely and coherently inside the repository, while preserving compatibility with the existing project architecture and backend contracts.

Do not implement unrelated project areas merely because they exist in the product vision.

Do not create pseudo-implementations, mock production APIs, fake persistence, fake authentication, placeholder components, TODO-driven stubs, incomplete wiring, or visually convincing features that do not actually work.

# 2. PROJECT IDENTITY

The project is a production-grade **Instagram-style social media platform**.

The frontend is a TypeScript-based Next.js/React web application consuming production-oriented backend APIs and realtime capabilities.

The product experience includes:

* identity and accounts
* user profiles
* social graph interactions
* home feed
* posts and media
* likes and comments
* saves and shares
* stories
* short-form video
* discovery and search
* direct messaging
* notifications
* moderation and reporting
* privacy and safety controls
* responsive web experiences
* observability, reliability, accessibility, and performance

The implementation in this prompt is limited to the frontend content-consumption and engagement surface defined below.

# 3. CURRENT FRONTEND ASSIGNMENT

Implement the **core Instagram content browsing and engagement experience** for the web application.

This volume owns the user-facing experience for:

* Home feed
* feed item rendering
* post presentation
* image and video media consumption
* post detail experience
* likes
* comments and replies
* saves
* shares
* engagement counts and state
* content loading and pagination
* optimistic engagement interactions
* authenticated content actions
* relevant content error, empty, loading, and retry states
* responsive behavior for desktop, tablet, and mobile web
* accessibility for all implemented content and engagement surfaces

The resulting frontend must connect to real application APIs/contracts already represented by the repository and architecture artifacts.

This prompt does **not** authorize implementation of unrelated frontend domains such as messaging, stories, reels, discovery/search, notification center, moderation dashboards, or mobile applications.

# 4. REPOSITORY INSPECTION

Before changing code, inspect the repository comprehensively enough to determine the existing frontend structure and integration boundaries.

At minimum, inspect:

* frontend application entry points
* Next.js routing and layout structure
* TypeScript configuration
* package manager configuration
* design system and reusable UI primitives
* existing authentication/session mechanisms
* API client and request abstraction
* server-state/data-fetching infrastructure
* client-state infrastructure
* existing profile and social-graph components
* shared types and generated API types if present
* environment configuration
* error handling
* telemetry/instrumentation
* frontend tests
* linting and formatting configuration
* build configuration
* existing documentation relevant to frontend implementation
* repository architecture/contracts that define feed, content, engagement, media, authorization, pagination, and error behavior

Treat the repository's existing implementation and authoritative contract artifacts as the source of truth for integration details.

Do not silently replace established infrastructure with a second competing pattern.

If existing code is incomplete, extend it consistently rather than creating unnecessary parallel abstractions.

If an authoritative contract is absent or insufficient for a required integration detail, document the limitation explicitly and implement only what can be safely derived from the existing system rather than inventing incompatible backend behavior.

# 5. TECHNOLOGY BASELINE

Use the project's established frontend technology choices.

The expected baseline is:

* Next.js
* React
* TypeScript
* semantic HTML
* responsive CSS/design-system primitives
* the repository's established server-state/data-fetching approach
* the repository's established client-state approach
* the repository's established API client
* the repository's established testing framework
* the repository's established telemetry/instrumentation

Do not introduce a new major framework, state-management paradigm, component library, networking abstraction, or styling architecture without a documented engineering reason and compatibility with the existing application.

Use strict typing throughout the implementation.

Avoid unsafe `any` usage except where a narrowly justified integration boundary requires it and the reason is documented.

# 6. BOUNDED IMPLEMENTATION SCOPE

Implement the following frontend capabilities completely.

## 6.1 Home Feed

Create the primary authenticated home-feed experience.

The implementation must support:

* loading the feed
* initial data retrieval
* stable feed rendering
* cursor-based or contract-defined pagination
* loading additional content as the user reaches the appropriate threshold
* explicit loading-more states
* end-of-feed behavior
* empty-feed behavior
* recoverable feed failures
* retry behavior
* preservation of already rendered content when subsequent pagination fails
* prevention of duplicate page insertion
* appropriate handling of stale or refreshed feed data
* correct authorization-aware rendering
* navigation from feed items into the relevant content context

Respect the pagination semantics defined by the backend contract.

Do not invent offset/cursor semantics that contradict the API.

## 6.2 Feed Item Architecture

Create reusable feed-item primitives capable of representing the different supported post states.

A feed item should support:

* author identity
* author avatar
* author navigation
* post timestamp
* caption
* mentions where supported
* hashtags where supported
* media
* engagement controls
* engagement counts
* saved state
* share action
* content navigation
* privacy-aware rendering
* unavailable/deleted/removed-content states where represented by the backend
* accessibility labels and context

Separate reusable content primitives from feed-specific orchestration so the same post presentation can be reused by profile and post-detail surfaces without duplicating business logic.

## 6.3 Image Media Consumption

Implement production-quality post-image rendering.

Support:

* responsive image sizing
* correct aspect-ratio preservation
* constrained layout behavior
* appropriate loading strategy
* lazy loading where applicable
* graceful loading placeholders
* failure states
* alt text strategy
* high-density display
* prevention of layout instability
* correct handling of portrait, landscape, and square media
* full-size/media-detail navigation where supported by the application contract

Do not ship image behavior that causes avoidable cumulative layout shift.

## 6.4 Video Media Consumption

Implement post-video presentation for supported video content.

Support:

* correct aspect-ratio handling
* poster/preview behavior
* controlled playback
* mute/unmute behavior
* play/pause behavior
* loading state
* buffering state
* failure state
* accessibility
* responsive controls
* reduced-motion considerations
* cleanup of media resources when components unmount
* avoidance of unnecessary autoplay behavior

Respect browser autoplay restrictions.

Do not assume that every video can autoplay with sound.

Do not download or initialize heavyweight media unnecessarily.

## 6.5 Post Detail Experience

Implement navigation to a dedicated or contract-defined post-detail experience.

The post-detail experience must provide:

* canonical post context
* author information
* complete supported media
* caption
* mentions and hashtags where applicable
* engagement state
* engagement controls
* comments
* replies
* save state
* share behavior
* loading behavior
* error handling
* deleted/unavailable content handling
* responsive presentation

The implementation must avoid duplicating business logic between the feed and detail surfaces.

## 6.6 Likes

Implement the complete user interaction for liking and unliking posts.

Support:

* current like state
* current like count
* optimistic state update where appropriate
* reconciliation with the server response
* rollback on failure
* duplicate-click protection
* request cancellation or stale-response protection where necessary
* disabled/loading behavior where required
* accessibility feedback
* synchronization when the same post appears in more than one rendered context

The UI must never permanently display an optimistic state that the backend rejected.

## 6.7 Comments

Implement post comments.

Support:

* comment list retrieval
* cursor-based pagination according to contract
* comment author information
* comment body
* timestamps
* loading states
* empty state
* error state
* retry behavior
* comment creation
* validation
* submission state
* successful insertion into the visible list
* failed submission rollback or preservation of unsent text according to UX design
* correct handling of authorization errors
* correct handling of removed or unavailable comments where represented by the API

The implementation must safely render user-generated content.

Do not render arbitrary comment content as executable HTML.

## 6.8 Replies

Implement supported comment-reply interactions.

Support:

* opening/closing replies where the product contract supports progressive disclosure
* loading replies
* pagination
* posting replies
* loading/error states
* author identity
* timestamps
* accessibility
* synchronization with comment counts

Keep nested interaction behavior understandable and responsive rather than creating an unnecessarily deep recursive UI.

## 6.9 Saves

Implement saving and unsaving posts.

Support:

* saved state
* optimistic interaction where safe
* rollback on failure
* correct synchronization of state
* authenticated-action enforcement
* loading/error feedback

Do not create a local-only saved collection that implies persistence unless the backend contract provides such persistence.

## 6.10 Shares

Implement the post share action according to the project's actual contract.

Support the appropriate combination of:

* share target selection where implemented
* copy/share-link behavior where supported
* native browser sharing where appropriate
* authenticated share behavior where required
* graceful fallback when native capabilities are unavailable
* success and failure feedback
* privacy-aware handling

Do not expose internal IDs or private resources through generated share links.

## 6.11 Engagement State Synchronization

The feed, post detail, profile-related post surfaces, and other already implemented content contexts must not maintain contradictory engagement state.

Create a coherent client-side strategy for:

* like state
* like counts
* save state
* comment counts
* relevant post freshness
* stale query reconciliation

Reuse the repository's existing cache/query invalidation infrastructure.

Do not build a second independent cache system without a documented reason.

# 7. DATA FETCHING AND CLIENT STATE

Use the established application data-fetching architecture.

Implement:

* typed request functions
* typed response handling
* query keys or cache identifiers
* cache invalidation
* mutation lifecycle handling
* stale-data reconciliation
* pagination state
* request cancellation where appropriate
* duplicate-request prevention
* protection against stale mutations overwriting fresher state

The frontend must correctly distinguish:

* loading
* success
* empty
* partial success where applicable
* recoverable failure
* authorization failure
* unavailable content
* terminal content state

Do not equate an empty result with an error.

Do not silently treat authorization failures as empty content.

# 8. OPTIMISTIC UI RULES

Use optimistic interactions only for operations where the product behavior and backend semantics make them safe.

For an optimistic mutation:

1. capture the previous state,
2. update the UI immediately where appropriate,
3. send the backend request,
4. accept and reconcile authoritative response data,
5. rollback or otherwise restore consistent state on failure,
6. surface an understandable user-facing error,
7. prevent stale responses from corrupting newer state.

Do not apply optimistic updates blindly to operations with ordering or authorization constraints that make them unsafe.

# 9. ERROR HANDLING

Implement production-grade frontend error handling.

Errors must be:

* typed or normalized through the established API layer
* translated into appropriate user-facing states
* observable through the existing telemetry system
* safe to display
* free of secrets and internal stack traces

Handle at minimum:

* network failure
* request timeout
* unauthorized request
* forbidden action
* not-found content
* deleted content
* validation failure
* rate limiting
* server failure
* media loading failure
* pagination failure
* mutation failure

Do not display raw backend payloads directly to users unless the existing error contract explicitly defines them as safe presentation text.

# 10. LOADING, EMPTY, AND FAILURE EXPERIENCES

Every implemented content surface must have intentional states for:

* first load
* loading additional content
* empty result
* failed first load
* failed subsequent load
* mutation in progress
* mutation failure
* unavailable content
* completed pagination

Avoid indefinite spinners.

Avoid blank screens.

Do not use decorative skeletons that materially differ from the final layout in a way that creates layout instability.

# 11. RESPONSIVE DESIGN

The complete implementation must work across:

* desktop web
* laptop displays
* tablet layouts
* narrow mobile web
* touch-oriented interaction

Support:

* fluid content widths
* responsive media presentation
* appropriate control sizing
* readable typography
* touch-safe interactive targets
* stable fixed/sticky behavior
* correct viewport handling
* keyboard access on desktop
* no horizontal overflow caused by feed content

The interface should adapt to available space rather than merely shrinking the desktop layout.

# 12. ACCESSIBILITY

Implement the feed and engagement surfaces using accessible semantics.

At minimum:

* semantic landmarks
* accessible buttons
* meaningful accessible names
* keyboard navigation
* visible focus states
* logical tab ordering
* accessible dialogs/sheets where applicable
* correct labels for like/save/share actions
* meaningful media alternative text behavior
* screen-reader announcements for important async state changes
* correct disabled/loading semantics
* accessible error presentation
* accessible comment forms

Do not rely solely on color to communicate state.

Ensure interaction patterns remain usable when pointer input is unavailable.

# 13. DESIGN SYSTEM INTEGRATION

Use the project's established design-system primitives.

Create reusable components only where repetition or domain consistency justifies them.

Potential shared components include:

* Feed
* FeedItem
* PostHeader
* PostMedia
* PostActions
* EngagementSummary
* CommentList
* CommentItem
* ReplyList
* CommentComposer
* ContentSkeleton
* ContentErrorState
* ContentUnavailableState
* ShareControl

Do not create dozens of micro-components with no architectural value.

Do not bypass the existing design system with isolated hardcoded styling.

# 14. CONTENT SAFETY AND USER-GENERATED CONTENT

Treat all user-generated content as untrusted input.

The frontend must:

* safely render captions
* safely render comments
* safely render replies
* safely render mentions/hashtags according to established parsing contracts
* avoid executable HTML injection
* avoid unsafe URL handling
* avoid dangerous DOM APIs
* avoid exposing internal service metadata

Do not move security responsibilities from the backend into client-side assumptions.

Client-side checks improve UX but do not replace backend authorization.

# 15. PERFORMANCE REQUIREMENTS

Optimize the implementation for a high-volume media-heavy social application.

Pay particular attention to:

* unnecessary rerenders
* oversized component trees
* duplicate network requests
* duplicate media downloads
* expensive list rendering
* unnecessary client-side JavaScript
* query invalidation storms
* large serialized props
* image loading
* video initialization
* scroll performance
* event-handler churn

Use appropriate techniques such as:

* component memoization when justified
* stable callbacks where useful
* virtualization only where warranted by actual list characteristics
* lazy loading
* code splitting
* responsive media delivery
* request deduplication
* cache reuse
* incremental rendering

Do not prematurely optimize with abstractions that substantially reduce maintainability.

# 16. MEDIA PERFORMANCE

Because this project is media-heavy, media behavior must be treated as a first-class performance concern.

Verify:

* correct media URL construction
* appropriate CDN usage according to existing contracts
* responsive image delivery
* no accidental full-resolution loading where thumbnails are sufficient
* no unnecessary preload behavior
* correct cleanup of video resources
* no repeated media initialization caused by rerendering
* graceful handling of slow connections

Never embed production credentials or storage-provider secrets in browser-executed code.

# 17. SECURITY AND PRIVACY

The frontend implementation must respect the project's security and privacy model.

At minimum:

* do not trust client-side authorization checks
* do not expose secrets
* do not place private credentials in browser bundles
* do not log authentication tokens
* do not log sensitive user-generated content unnecessarily
* avoid leaking private post metadata through client state
* honor server-provided visibility and authorization results
* use secure URL behavior for media and shared content
* avoid unsafe HTML rendering
* follow established CSRF/session protections
* follow existing content-security and security-header assumptions

Any frontend telemetry must avoid collecting unnecessary sensitive information.

# 18. OBSERVABILITY

Integrate the implemented surfaces with existing frontend observability.

Capture appropriate technical signals for:

* feed load failures
* pagination failures
* mutation failures
* media loading failures
* comment submission failures
* major client-side exceptions
* important performance milestones

Include appropriate correlation information where the existing telemetry architecture supports it.

Do not emit:

* access tokens
* session secrets
* private message content
* raw sensitive user data
* unnecessary full captions/comments
* unrestricted backend payloads

# 19. TESTING

Add meaningful automated tests for the implemented functionality.

Testing should cover:

* feed rendering
* feed loading
* empty feed
* feed failure and retry
* pagination
* duplicate-page protection
* post rendering
* image rendering states
* video rendering states
* post-detail navigation
* like success
* like rollback
* save success/failure
* comment creation
* comment validation
* comment pagination
* replies
* share behavior
* synchronization of engagement state
* authorization failures
* unavailable content
* responsive behavior where the existing test infrastructure supports it
* accessibility-critical interactions

Use realistic fixtures and typed mocks consistent with the application's API contracts.

Do not build tests around fake backend behavior that contradicts the real contracts.

Do not settle for snapshot-only coverage of behavior-heavy components.

# 20. INTEGRATION AND CONTRACT VALIDATION

Validate all frontend/backend integrations against the repository's authoritative contracts.

Verify:

* endpoint paths
* HTTP methods
* request shapes
* response shapes
* authentication requirements
* authorization behavior
* pagination semantics
* idempotency behavior where applicable
* error codes
* mutation semantics
* media URL expectations
* identifier formats
* timestamp handling

Do not silently invent response fields.

Do not rename contract fields merely for frontend convenience unless the transformation is isolated and documented.

Do not make backend changes outside this prompt's scope merely to make an incorrect frontend assumption work.

# 21. CROSS-FRONTEND COMPATIBILITY

The implementation must remain compatible with the already established frontend foundation, including:

* authentication/session handling
* profile navigation
* social graph controls
* API infrastructure
* design system
* routing
* state management
* telemetry
* error handling
* build/test infrastructure

Do not break previously implemented functionality.

Where shared components or utilities must be adjusted, preserve existing contracts and test affected behavior.

# 22. OUT OF SCOPE

Do not implement the following in this prompt unless a minimal shared change is strictly necessary for integration:

* Stories
* Reels-specific product experiences
* Explore/discovery UI
* advanced search UI
* direct messaging UI
* group chat UI
* notification center
* push-notification settings UI
* moderation/admin dashboards
* analytics dashboards
* mobile React Native implementation
* infrastructure deployment
* backend services
* database migrations
* Kafka infrastructure
* OpenSearch infrastructure
* object-storage infrastructure
* CDN infrastructure
* production cloud configuration

Do not create placeholder screens for those areas merely to claim broader completion.

# 23. DOCUMENTATION

Update or create documentation needed to make the implemented frontend scope understandable to future engineers.

Document, where applicable:

* component architecture
* feed data flow
* pagination behavior
* cache/query strategy
* optimistic mutation strategy
* media rendering decisions
* accessibility decisions
* performance-sensitive areas
* integration assumptions
* testing strategy
* known contract dependencies

Documentation must describe what is actually implemented.

Do not document imaginary future functionality as completed functionality.

# 24. IMPLEMENTATION DISCIPLINE

Do not:

* leave TODOs for required functionality
* leave FIXME markers for unresolved required work
* use placeholder text instead of real implementation
* use fake API endpoints
* create mock persistence that appears production-ready
* hardcode users, post IDs, engagement counts, or production URLs
* hardcode secrets
* bypass authentication
* disable validation merely to make tests pass
* silence TypeScript errors without justification
* suppress lint errors without justification
* weaken security controls for convenience
* duplicate existing infrastructure without reason

When a requirement cannot safely be implemented because the repository lacks a required contract or dependency, identify the exact dependency in the implementation report instead of fabricating it.

# 25. VALIDATION

Before considering this prompt complete, perform appropriate validation.

At minimum:

* type-check the frontend
* run linting
* run relevant unit/component tests
* run integration tests available for this frontend scope
* verify production build compatibility
* verify route behavior
* verify feed pagination
* verify engagement mutations
* verify failure and retry paths
* verify accessibility-critical controls
* verify media behavior
* verify responsive behavior
* inspect changed files for accidental debug output
* inspect for secrets
* inspect for placeholder code
* inspect for contract mismatches

Fix implementation defects discovered during validation.

Do not report tests as passing if they were not actually run.

# 26. IMPLEMENTATION REPORT

At the end of the work, provide a concise engineering report containing:

## Implemented

Summarize the concrete functionality implemented in this prompt.

## Files Changed

List the meaningful files created or modified and briefly explain their purpose.

## Contracts Integrated

Identify the relevant backend/frontend contracts used.

## Tests

List the tests executed and their results.

## Validation

List the type-check, lint, build, integration, accessibility, or performance validation actually performed.

## Important Decisions

Document significant implementation decisions and tradeoffs.

## Limitations

Document genuine limitations caused by missing repository capabilities or authoritative contracts.

Do not describe future work as completed work.

# 27. DEFINITION OF DONE

This prompt is complete only when:

* the home feed is operational through real application APIs
* feed pagination follows the established contract
* feed items render supported post content correctly
* image and video media are handled robustly
* post detail works through the established routing model
* likes work with correct state reconciliation
* comments work with validation, pagination, and error handling
* replies work where supported
* saves work with correct server synchronization
* sharing uses the established product contract
* loading, empty, unavailable, and failure states are implemented
* responsive layouts are implemented
* accessibility requirements are addressed
* security and privacy requirements are respected
* observability is integrated
* relevant tests are implemented and passing
* type-checking and linting succeed
* the production build remains valid
* no fake APIs, placeholder implementations, TODOs, hardcoded secrets, or fake persistence remain
* existing frontend functionality remains compatible
* documentation reflects the actual implementation
* the implementation report accurately describes what was done

# 28. FINAL EXECUTION DISCIPLINE

Implement this prompt as a bounded production engineering task.

Do not expand the scope into unrelated product areas.

Do not ask the user to choose between implementation approaches when the repository and architecture already establish the required direction.

Make reasonable engineering decisions from the existing repository, contracts, and established patterns.

When a decision is genuinely ambiguous and materially affects compatibility, follow the authoritative contract or existing project convention rather than inventing a new standard.

Do not claim completion until the Definition of Done has been satisfied and the stated validation has actually been performed.
