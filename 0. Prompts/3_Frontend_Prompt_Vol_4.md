# Instagram — Frontend Prompt — Volume 4

# 1. ROLE

You are the **Senior Frontend Engineering implementation team** responsible for implementing the bounded frontend scope defined in this prompt for the Instagram project.

Operate as a production engineering organization with expertise in:

* React and Next.js
* TypeScript
* discovery and search interfaces
* large result sets
* responsive, accessible web applications
* high-performance client-side filtering and navigation
* server-state and cache management
* API contract integration
* autocomplete and search experiences
* production observability
* automated frontend testing
* privacy and secure handling of user-generated content

Your responsibility is to implement the assigned frontend scope completely and coherently inside the repository while preserving compatibility with the existing application architecture and authoritative backend contracts.

Do not implement unrelated product domains merely because they exist elsewhere in the application.

Do not create fake APIs, fake persistence, placeholder functionality, TODO-driven implementations, or interfaces that only simulate completed behavior.

# 2. PROJECT IDENTITY

The project is a production-grade **Instagram-style social media platform**.

The frontend is a TypeScript-based Next.js/React web application integrating with production-oriented backend APIs and platform capabilities.

The product includes:

* identity and accounts
* profiles
* social graph
* home feed
* posts and media
* Stories
* short-form video
* likes, comments, saves, and shares
* discovery
* search
* direct messaging
* notifications
* moderation and reporting
* privacy and safety controls
* responsive web experiences
* observability, reliability, accessibility, and performance

This prompt is limited to the **discovery and search frontend experience**.

# 3. CURRENT FRONTEND ASSIGNMENT

Implement the web frontend for Instagram-style **Explore, discovery, search, and content/user discovery**.

This volume owns:

* Explore surface
* discovery content presentation
* discovery pagination
* search entry experience
* search suggestions/autocomplete
* user/account search
* content/hashtag search where supported
* search result categories/tabs where defined by the contracts
* result navigation
* search state
* query synchronization
* loading/empty/error states
* debounced search behavior
* stale-request protection
* search cache behavior
* media-heavy discovery rendering
* responsive behavior
* accessibility
* privacy-aware result handling
* observability
* automated testing

Do not implement direct messaging, notification center, moderation/admin dashboards, or mobile React Native features in this prompt.

# 4. REPOSITORY INSPECTION

Before modifying code, inspect the repository sufficiently to understand:

* Next.js routing
* existing navigation and application shell
* existing search controls, if any
* design-system primitives
* feed and post components
* media rendering components
* profile navigation
* API client
* server-state/data-fetching infrastructure
* client-state conventions
* query caching and invalidation
* authentication/session handling
* telemetry/instrumentation
* error normalization
* loading and empty-state primitives
* existing URL/query-parameter conventions
* automated testing setup
* accessibility utilities
* responsive layout conventions
* relevant documentation

Inspect the authoritative architecture and contract artifacts governing:

* discovery
* recommendation results
* search
* search categories
* autocomplete/suggestions
* pagination
* visibility
* authorization
* privacy
* media
* identifiers
* timestamps
* error behavior
* rate limits
* observability

Treat those contracts and the existing repository patterns as the source of truth.

Do not invent endpoint shapes, result fields, ranking semantics, or visibility rules.

# 5. TECHNOLOGY BASELINE

Use the established project technology:

* Next.js
* React
* TypeScript
* semantic HTML
* established styling/design system
* established API client
* established server-state/data-fetching system
* established client-state mechanisms
* established telemetry
* established test framework

Maintain strict typing.

Do not add another search library, global state framework, query library, or component framework unless there is a material engineering reason and compatibility is preserved.

# 6. BOUNDED IMPLEMENTATION SCOPE

Implement the following functionality completely.

## 6.1 Explore Surface

Implement the primary discovery/Explore experience.

Support the discovery content contract as defined by the repository, including as applicable:

* content grid
* media tiles
* mixed content types
* creators
* posts
* short-form video
* recommended content
* progressive loading
* pagination
* refresh/revalidation
* empty state
* recoverable failure
* retry behavior
* content navigation

Do not implement client-side ranking logic.

The backend remains authoritative for ordering and recommendation decisions.

## 6.2 Discovery Media Grid

Create a responsive, reusable discovery grid.

Support:

* responsive columns
* supported aspect ratios
* image and video thumbnails
* appropriate media variants
* lazy loading
* layout stability
* content-type indicators where required
* hover/pointer behavior where appropriate
* keyboard navigation
* touch interaction

Do not load full-resolution media when a thumbnail or preview representation is sufficient.

## 6.3 Discovery Pagination

Implement the pagination model established by the backend contract.

Support:

* initial load
* subsequent page loading
* cursor preservation
* end-of-results state
* request deduplication
* duplicate-item prevention
* stale-response protection
* failed-page retry
* preserving existing results when later pagination fails

Do not infer pagination semantics from UI assumptions.

Do not mix incompatible cursors from separate query contexts.

## 6.4 Discovery Refresh

Implement refresh/revalidation behavior according to the application's data-fetching architecture.

Handle:

* explicit refresh where the product exposes it
* stale data revalidation
* temporary network failure
* unchanged result sets
* changed result sets
* preservation of user context during refresh

Do not clear visible content unnecessarily during background revalidation.

## 6.5 Search Entry Experience

Implement the primary web search experience.

Support:

* search field
* focus state
* query entry
* clear action
* keyboard interaction
* loading state
* suggestions
* query submission
* navigation to result state
* accessible labeling
* responsive behavior

Respect the existing application navigation and search-entry conventions.

## 6.6 Search Suggestions / Autocomplete

Implement server-backed search suggestions where the contract provides them.

Support:

* debounced input
* minimum query constraints from the contract
* loading state
* suggestion results
* empty suggestions
* request cancellation or stale-result suppression
* keyboard navigation
* pointer selection
* accessible active-result state
* clear behavior
* query preservation

The UI must never display suggestions belonging to an older query after the user has entered a newer query.

## 6.7 Search Result Page

Implement the search-result experience defined by the repository.

Support the result categories specified by the contracts, which may include:

* accounts/users
* hashtags
* posts/content
* video content
* other explicitly contracted searchable resources

Support:

* result tabs or categories when defined
* query state
* pagination
* loading
* empty state
* failure
* retry
* result selection
* creator navigation
* content navigation

Do not add unsupported result categories simply because they appear conceptually useful.

## 6.8 Query URL Synchronization

Synchronize search state with routing according to the project's URL conventions.

Support:

* direct navigation to a search result
* browser back/forward
* refresh persistence
* safe URL encoding
* restoring valid query state
* appropriate handling of empty/invalid queries

Do not put sensitive internal request metadata into query parameters.

Do not leak private identifiers through public URLs.

# 7. SEARCH INTERACTION MODEL

Implement search interactions using the application's established state architecture.

A search interaction should correctly distinguish:

* idle
* typing
* waiting/debouncing
* loading
* success
* empty
* recoverable error
* unauthorized/forbidden result
* stale-result replacement

Do not show an obsolete result set as though it belongs to the current query.

Protect against:

* rapid query changes
* out-of-order responses
* duplicate requests
* request races
* navigation during active requests

# 8. DISCOVERY AND SEARCH CACHING

Use the existing cache/data-fetching system.

Cache behavior should account for:

* query text
* result category
* pagination cursor
* authenticated context where relevant
* freshness
* invalidation
* stale-while-revalidate behavior where appropriate

Do not use a cache key that causes results for one authenticated context to be incorrectly reused for another.

Do not make search results globally persistent in client storage unless explicitly supported and safe.

# 9. SEARCH DEBOUNCING AND REQUEST CONTROL

Autocomplete should not issue a backend request for every keystroke when the established contract expects debouncing.

Implement:

* deterministic debounce behavior
* cancellation or stale-response protection
* request deduplication
* minimum-query handling
* immediate clear/reset behavior

Do not add arbitrary long debounce delays that make search feel unresponsive.

Use the application's established interaction conventions where they already exist.

# 10. RESULT RENDERING

Implement reusable result components appropriate to the contract.

Potential result primitives include:

* SearchResultList
* SearchResultItem
* UserResult
* HashtagResult
* ContentResult
* SearchSuggestion
* DiscoveryTile
* DiscoveryGrid
* SearchTabs
* SearchEmptyState
* SearchErrorState

Reuse existing profile, avatar, media, post, and navigation components wherever possible.

Do not duplicate established content-rendering logic merely to make search independent.

# 11. USER / ACCOUNT SEARCH

For account-search results, support the contract-defined user information.

Potential fields include:

* avatar
* username
* display name
* relevant public profile metadata
* relationship state where explicitly supported
* verified/public indicators where defined by the contract

Do not expose private profile attributes merely because the backend returned internal metadata.

Do not display administrative identifiers.

Navigation must use canonical account identifiers and established routes.

# 12. HASHTAG SEARCH

Where hashtag search is supported by the contracts, implement:

* hashtag result rendering
* canonical hashtag navigation
* query-safe encoding
* pagination
* empty state
* invalid/unavailable state

Do not treat arbitrary user-entered `#` text as a trusted identifier.

Use the server-provided canonical identifier or slug.

# 13. CONTENT SEARCH

Where content search is supported, render the contract-defined media/content result.

Support:

* thumbnail/media preview
* creator
* content context
* relevant engagement metadata
* content-type indicators
* canonical navigation
* unavailable content states

Do not expose content metadata that the backend marks as private or unauthorized.

# 14. DISCOVERY PERFORMANCE

The Explore surface can contain a large number of media items.

Optimize for:

* efficient list/grid rendering
* minimal unnecessary rerenders
* lazy media loading
* thumbnail usage
* stable layout dimensions
* efficient pagination
* query/cache reuse
* limited client-side JavaScript
* avoiding unnecessary full-content component hydration

Use virtualization only when justified by actual content volume and the existing architecture.

Do not over-engineer a simple result set.

# 15. ACCESSIBILITY

Implement accessible search and discovery interactions.

At minimum:

* accessible search field labeling
* keyboard navigation
* clear focus visibility
* correct combobox/listbox semantics where applicable
* active suggestion semantics
* escape behavior
* enter/select behavior
* accessible tabs where tabs exist
* screen-reader-friendly loading and error announcements
* meaningful media alternatives
* keyboard access to result items
* accessible empty and unavailable states

Do not make suggestion selection dependent on pointer input.

Do not rely solely on color or hover state to convey result selection.

# 16. RESPONSIVE DESIGN

Support:

* desktop
* laptop
* tablet
* mobile web
* narrow viewports
* touch interaction

The Explore grid must adapt to available width.

The search interface must remain usable when:

* navigation chrome is reduced
* the viewport becomes narrow
* the keyboard is open on mobile browsers
* the result list contains long usernames or labels

Prevent horizontal overflow.

# 17. ERROR HANDLING

Handle at minimum:

* network failures
* timeout
* search-service failure
* rate limiting
* unauthorized results
* forbidden results
* invalid query
* unavailable content
* empty result sets
* pagination errors
* stale response
* cancelled request
* malformed result data at the application boundary

User-facing errors must be understandable and safe.

Do not render raw backend payloads.

Do not reveal internal search infrastructure details.

# 18. SECURITY AND PRIVACY

Search and discovery can expose large amounts of user and content metadata.

The implementation must:

* respect backend visibility decisions
* never circumvent account privacy
* never reveal blocked/restricted users solely through client-side assumptions
* avoid caching private results in unsafe shared storage
* avoid logging raw search terms when unnecessary
* avoid logging sensitive or private result content
* avoid leaking internal identifiers
* avoid unsafe URL construction
* avoid unsafe HTML rendering
* avoid exposing secrets or internal service URLs

Client-side filtering must never be treated as an authorization mechanism.

# 19. OBSERVABILITY

Integrate discovery/search with the existing frontend observability system.

Capture useful technical signals such as:

* search request failures
* suggestion failures
* discovery-load failures
* pagination failures
* result-rendering exceptions
* significant client-side performance failures
* route/navigation errors

Telemetry should avoid unnecessary collection of:

* raw private search history
* sensitive user identifiers
* private content
* session credentials
* access tokens
* signed media URLs

Follow the repository's existing privacy-aware telemetry conventions.

# 20. TESTING

Add meaningful automated tests covering:

## Explore

* initial loading
* successful result rendering
* empty results
* pagination
* duplicate prevention
* pagination retry
* refresh/revalidation
* media tile rendering
* unavailable content
* responsive behavior where supported

## Search

* query entry
* clear behavior
* debounce behavior
* minimum query behavior
* suggestions
* keyboard navigation
* stale-response protection
* result submission
* URL synchronization
* back/forward navigation
* category/tab switching
* pagination
* empty results
* error and retry

## Security / Privacy

Test that:

* unsafe content is not rendered as HTML
* private metadata is not surfaced through presentation logic
* stale results cannot replace newer query results
* cache keys do not unintentionally cross user/query contexts

## Accessibility

Test:

* keyboard search interaction
* suggestion navigation
* focus management
* accessible result naming
* tab semantics
* loading/error announcements where supported

Do not rely exclusively on snapshots.

# 21. CONTRACT VALIDATION

Validate integration against the repository's authoritative contracts.

Verify:

* search endpoints
* suggestion endpoints
* discovery endpoints
* request parameters
* response shapes
* result types
* category semantics
* ordering
* pagination
* identifiers
* timestamps
* privacy/visibility behavior
* authorization requirements
* rate-limit behavior
* error codes
* media URL expectations

Do not invent ranking scores or recommendation data.

Do not expose fields simply because they exist in an internal API response.

# 22. ROUTING AND NAVIGATION

Integrate search and discovery with the existing Next.js route architecture.

Support:

* canonical URLs
* direct result navigation
* browser history
* query restoration
* route loading states
* invalid-query behavior
* navigation to profiles
* navigation to content
* navigation to hashtags where supported

Avoid full page transitions when the existing architecture supports efficient client navigation.

Do not bypass established authorization-aware route handling.

# 23. SHARED FRONTEND INTEGRATION

Reuse existing:

* authentication/session handling
* navigation shell
* profile components
* media primitives
* content cards
* buttons/forms
* API client
* server-state infrastructure
* error boundaries
* telemetry
* accessibility primitives

Where a shared component needs an extension, preserve backward compatibility and add tests for affected behavior.

# 24. OUT OF SCOPE

Do not implement:

* direct messaging
* group chat
* notification center
* push-notification interfaces
* moderation/admin dashboards
* analytics dashboards
* mobile React Native implementation
* backend search services
* OpenSearch cluster configuration
* backend recommendation/ranking algorithms
* database migrations
* Kafka or queue infrastructure
* cloud infrastructure
* unrelated account/profile redesign

Do not create placeholder pages for these domains.

# 25. DOCUMENTATION

Document the implemented discovery/search frontend behavior where useful.

Include, as appropriate:

* Explore rendering architecture
* search state machine
* autocomplete behavior
* debounce/cancellation strategy
* cache-key strategy
* pagination behavior
* route/query synchronization
* privacy considerations
* performance decisions
* accessibility decisions
* testing strategy
* contract dependencies

Document actual implementation behavior only.

# 26. IMPLEMENTATION DISCIPLINE

Do not:

* hardcode search results
* hardcode user identifiers
* hardcode hashtags
* fake discovery ranking
* fake pagination
* fabricate backend result fields
* create a fake search service
* place private search results in unsafe persistent storage
* expose secrets
* render untrusted HTML
* leave TODO/FIXME markers for required functionality
* suppress type or lint errors without justification
* create competing global state systems without need
* claim unsupported search categories are implemented

Test fixtures may contain controlled data, but production code must consume real contracts.

# 27. VALIDATION

Before considering the implementation complete:

* run type-checking
* run linting
* run relevant unit/component tests
* run integration tests
* verify production build compatibility
* test Explore loading
* test pagination
* test refresh/revalidation
* test search entry
* test suggestions
* test stale-result handling
* test URL synchronization
* test result navigation
* test keyboard accessibility
* inspect for unnecessary network calls
* inspect for race conditions
* inspect cache keys
* inspect for secrets
* inspect for unsafe HTML
* inspect for placeholder code
* inspect for contract mismatches

Fix defects discovered during validation.

Do not report validation as successful unless it was actually performed.

# 28. IMPLEMENTATION REPORT

At the end of the work, provide:

## Implemented

Summarize Explore and search functionality actually implemented.

## Files Changed

List meaningful created and modified files with their purpose.

## Contracts Integrated

Identify discovery, search, suggestions, content, visibility, authorization, and pagination contracts integrated.

## Tests

List test commands and outcomes.

## Validation

List type-check, lint, build, integration, accessibility, and performance validation actually performed.

## Important Decisions

Document material architectural decisions and tradeoffs.

## Limitations

Document real limitations caused by repository constraints or missing contracts.

Do not represent future work as completed.

# 29. DEFINITION OF DONE

This prompt is complete only when:

* Explore is operational through real application contracts
* discovery content renders correctly
* media grids are responsive and performant
* discovery pagination works
* duplicate and stale result handling is correct
* refresh/revalidation behavior is correct
* search entry is fully functional
* autocomplete/suggestions work according to the contract
* stale search requests cannot overwrite current results
* search results render supported categories correctly
* query state synchronizes with application routing
* user, hashtag, and content navigation works where supported
* loading, empty, failure, and retry states exist
* accessibility requirements are addressed
* responsive behavior is implemented
* privacy and authorization behavior is respected
* observability is integrated
* automated tests cover meaningful functionality
* type-checking succeeds
* linting succeeds
* production build compatibility is preserved
* no fake APIs or placeholder production functionality remain
* no required TODO/FIXME stubs remain
* no secrets are exposed
* documentation reflects actual behavior
* the implementation report accurately describes completed work

# 30. FINAL EXECUTION DISCIPLINE

Implement this prompt as a bounded production engineering task.

Do not expand into unrelated frontend domains.

Do not ask the user to choose among approaches when repository conventions and authoritative contracts already establish the correct integration model.

Make reasonable engineering decisions based on the repository and its contract artifacts.

Where ambiguity materially affects compatibility, follow the established project pattern and authoritative contract.

Do not claim completion until the Definition of Done has been satisfied and the stated validation has actually been performed.
