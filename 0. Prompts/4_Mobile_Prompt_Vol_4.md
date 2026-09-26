# Instagram — Mobile Prompt — Volume 4

# 1. ROLE

You are the **Senior Mobile Engineering implementation team** responsible for implementing the bounded mobile scope defined in this prompt for the Instagram project.

Operate as a production engineering organization with expertise in:

* React Native
* TypeScript
* mobile discovery and search
* autocomplete and query interactions
* media-heavy result grids
* virtualized lists
* server-state and cache management
* responsive mobile interaction
* deep-link navigation
* accessibility
* privacy-aware search interfaces
* automated mobile testing
* observability
* performance optimization

Your responsibility is to implement the assigned mobile scope completely and coherently inside the repository while preserving compatibility with the mobile foundation, existing content infrastructure, backend contracts, and shared domain model.

Do not implement unrelated mobile product domains merely because they exist in the global product definition.

Do not create fake APIs, fake persistence, placeholder screens, TODO-driven implementations, or simulated discovery behavior presented as production functionality.

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

This prompt is limited to the **mobile Explore, discovery, search, autocomplete, and search-result experience**.

# 3. CURRENT MOBILE ASSIGNMENT

Implement the production mobile experience for:

* Explore/discovery surface
* discovery media grid
* recommended content presentation
* discovery pagination
* search entry
* search queries
* search suggestions/autocomplete
* account/user search
* hashtag search where supported
* content search where supported
* result categories/tabs where defined
* query URL/deep-link synchronization
* result navigation
* loading/empty/error/retry states
* stale-request protection
* search caching
* responsive mobile behavior
* accessibility
* privacy/security
* performance
* observability
* automated testing

This prompt does not implement direct messaging, notification center, moderation/admin, or unrelated mobile domains.

# 4. REPOSITORY INSPECTION

Before modifying code, inspect the repository sufficiently to understand:

* mobile application foundation
* authenticated navigation
* existing Explore/discovery components
* existing feed/post/media components
* profile navigation
* API client
* server-state/data-fetching infrastructure
* client-state management
* query/cache conventions
* deep-link handling
* design-system primitives
* loading/error/empty-state primitives
* telemetry
* accessibility utilities
* testing infrastructure
* iOS/Android configuration
* relevant documentation

Inspect authoritative contracts covering:

* discovery
* recommendations
* search
* search suggestions
* account/user search
* hashtags
* content search
* pagination
* visibility
* authorization
* privacy
* identifiers
* timestamps
* errors
* media delivery
* rate limiting

Treat the repository and contract artifacts as authoritative.

Do not invent search result fields, ranking logic, endpoint semantics, or privacy rules.

# 5. TECHNOLOGY BASELINE

Use the established mobile technology:

* React Native
* TypeScript
* established navigation
* established API client
* established server-state architecture
* established client-state architecture
* established media primitives
* established design system
* established telemetry
* established testing framework

Do not introduce a competing query library, global state system, search framework, or component library without a material compatibility justification.

Maintain strict TypeScript typing.

# 6. EXPLORE SURFACE

Implement the mobile Explore/discovery surface.

Support the contract-defined discovery experience, including where applicable:

* media grid
* mixed content types
* image tiles
* video tiles
* creators
* posts
* short-form video
* recommendations
* progressive loading
* pagination
* refresh/revalidation
* empty state
* failure
* retry
* canonical content navigation

The backend remains authoritative for content ordering and recommendation decisions.

Do not build a client-side recommendation engine.

# 7. DISCOVERY MEDIA GRID

Implement a reusable mobile discovery grid.

Support:

* responsive column behavior
* supported aspect ratios
* image thumbnails
* video thumbnails
* content-type indicators where required
* appropriate media variants
* lazy loading
* layout stability
* touch interaction
* accessibility labels
* navigation to content

Avoid loading full-resolution media when thumbnails are sufficient.

Use the existing mobile media infrastructure.

# 8. DISCOVERY PERFORMANCE

Optimize Explore for mobile resource constraints.

Pay attention to:

* virtualized rendering
* memory consumption
* image decoding
* thumbnail sizing
* cache reuse
* rerender frequency
* pagination frequency
* network usage
* layout measurement
* scroll performance

Do not render an unbounded number of media tiles simultaneously.

Do not preload large media unnecessarily.

# 9. DISCOVERY PAGINATION

Implement the contract-defined pagination model.

Support:

* initial load
* loading more
* cursor preservation
* end-of-results
* duplicate-item prevention
* duplicate-page protection
* stale-response protection
* failed-page retry
* preservation of existing results when later pages fail

Do not infer cursor semantics from local array state.

Do not mix cursors across different discovery contexts.

# 10. DISCOVERY REFRESH

Implement refresh/revalidation according to the existing mobile data layer.

Support:

* pull-to-refresh where established
* explicit refresh where provided
* background revalidation
* temporary network failure
* unchanged results
* updated results
* preservation of user scroll context where appropriate

Do not clear visible discovery content unnecessarily during background refresh.

# 11. SEARCH ENTRY

Implement the primary mobile search experience.

Support:

* search field
* focus
* query entry
* clear action
* keyboard behavior
* search submission
* suggestions
* loading state
* accessible labels
* navigation to result state
* responsive mobile layout

Use the established mobile navigation and design patterns.

# 12. SEARCH SUGGESTIONS

Implement server-backed autocomplete where the contract provides it.

Support:

* minimum query requirements
* debounce
* loading
* suggestions
* empty suggestions
* clear
* keyboard selection
* touch selection
* accessible selection state
* request cancellation or stale-result suppression
* query preservation

The interface must never display suggestions belonging to an outdated query.

# 13. SEARCH REQUEST CONTROL

Protect the search experience against rapid input and concurrent responses.

Handle:

* rapidly changing queries
* out-of-order responses
* duplicate requests
* stale responses
* cancellation
* connectivity changes
* navigation away during search

Use deterministic debounce behavior.

Do not introduce an arbitrarily long debounce interval.

# 14. SEARCH RESULT EXPERIENCE

Implement the search-result experience defined by the project contracts.

Support contract-defined categories such as:

* accounts/users
* hashtags
* posts/content
* short-form video
* other explicitly supported searchable resources

Support:

* category tabs where defined
* query state
* pagination
* loading
* empty
* failure
* retry
* result selection
* profile navigation
* content navigation

Do not add unsupported result categories.

# 15. USER / ACCOUNT RESULTS

Render account-search results using only contract-defined public fields.

Potentially include:

* avatar
* username
* display name
* public profile information
* relationship state when explicitly supported
* public/verified indicators where defined

Do not expose:

* private account metadata
* internal identifiers
* administrative fields
* backend-only attributes

Use canonical profile navigation.

# 16. HASHTAG RESULTS

Where hashtag search is supported, implement:

* hashtag result rendering
* canonical hashtag navigation
* safe query/identifier encoding
* pagination
* empty state
* unavailable state

Use the server-provided canonical identifier or slug.

Do not treat arbitrary user-entered hashtag text as an authoritative internal identifier.

# 17. CONTENT RESULTS

Where content search is supported, render:

* media preview
* creator
* content context
* supported engagement metadata
* content-type indicator
* canonical navigation
* unavailable-content state

Do not display metadata that the backend marks private or unauthorized.

# 18. QUERY STATE AND DEEP LINKS

Synchronize supported search state with the mobile navigation/deep-link architecture.

Support:

* direct search links where the project defines them
* query restoration
* authenticated continuation
* browser-like navigation semantics appropriate to mobile
* safe parameter parsing
* invalid-query handling
* navigation from result to canonical content

Never place authentication tokens or sensitive internal information in search URLs or deep links.

# 19. SEARCH CACHE STRATEGY

Use the existing server-state/cache system.

Cache keys must appropriately distinguish:

* query
* category
* pagination state
* authenticated user context
* relevant discovery context

Ensure search results from one authenticated context cannot be reused for another.

Do not persist search history or results locally unless explicitly supported by the product's privacy model.

# 20. CLIENT STATE

Keep ephemeral state separate from server state.

Client state may include:

* search-input focus
* temporary query text
* active result category
* transient loading indicators
* currently selected result
* search-screen UI state

Server-backed results must remain in the established server-state system.

Do not create a second global search store.

# 21. RESULT NAVIGATION

Support navigation from search/discovery into:

* creator profiles
* post detail
* short-form video
* hashtag/content destinations
* other explicitly contracted destinations

Use established navigation routes and canonical identifiers.

Do not construct internal service URLs in the client.

# 22. EMPTY, ERROR, AND UNAVAILABLE STATES

Implement clear mobile states for:

* no discovery content
* no search results
* suggestions unavailable
* invalid query
* search failure
* pagination failure
* unavailable profile
* unavailable content
* rate limiting
* network outage

Users must be able to retry appropriate failures.

Do not replace failures with misleading empty states.

# 23. SECURITY AND PRIVACY

Search and discovery can expose sensitive account and content relationships.

The mobile implementation must:

* honor backend visibility
* respect account privacy
* not reveal blocked/restricted users through client-side shortcuts
* avoid storing private results in unsafe persistent storage
* avoid logging raw sensitive search information
* avoid exposing internal identifiers
* avoid unsafe URL handling
* avoid unsafe HTML/content rendering
* never embed service secrets
* follow established authentication/session protections

Client-side filtering is not authorization.

# 24. ACCESSIBILITY

Implement mobile accessibility for search and discovery.

Support:

* accessible search labels
* logical focus behavior
* screen-reader-friendly result descriptions
* accessible suggestion states
* clear selected-category semantics
* accessible loading/error announcements where supported
* meaningful media labels
* touch targets of appropriate size
* accessible empty/unavailable states

Do not make search dependent on gesture-only interaction.

# 25. TOUCH AND MOBILE INTERACTION

Ensure the experience works well with:

* touch
* hardware keyboard where available
* system keyboard
* portrait orientation
* supported landscape contexts
* small displays
* large displays
* tablet layouts where supported

Prevent:

* accidental result activation
* inaccessible tiny controls
* horizontal overflow
* keyboard occlusion of critical controls

# 26. NETWORK AND CONNECTIVITY

Use the existing connectivity foundation to handle:

* offline state
* reconnecting
* transient request failures
* retry
* cached metadata where appropriate
* revalidation after reconnect

Do not claim offline search if the underlying repository does not support durable offline search.

# 27. OBSERVABILITY

Integrate search/discovery into mobile observability.

Capture useful technical signals for:

* discovery failures
* search failures
* suggestion failures
* pagination failures
* navigation failures
* significant rendering/performance failures

Do not log:

* passwords
* tokens
* private search history unnecessarily
* private content
* sensitive user data
* signed private-media URLs

Follow the project's privacy-aware telemetry standards.

# 28. TESTING

Add meaningful automated tests covering:

## Explore

* initial loading
* successful content rendering
* empty state
* pagination
* duplicate prevention
* refresh
* retry
* unavailable content
* media tile rendering

## Search

* query entry
* clear
* minimum-query behavior
* debounce
* suggestions
* keyboard behavior where supported
* stale-response protection
* query submission
* result categories
* pagination
* empty results
* error/retry
* result navigation

## Privacy / Security

Test that:

* private fields are not rendered
* unsafe content is not executed
* stale results cannot overwrite current results
* cache keys do not cross user contexts
* sensitive search information is not sent to telemetry

## Accessibility

Test:

* accessible search field
* suggestion navigation
* result labels
* category/tab semantics
* loading/error states

Do not rely exclusively on snapshots.

# 29. CONTRACT VALIDATION

Validate implementation against authoritative contracts for:

* discovery
* recommendations
* search
* autocomplete
* users
* hashtags
* content
* pagination
* identifiers
* timestamps
* visibility
* authorization
* media
* errors
* rate limits

Do not invent:

* ranking scores
* recommendation semantics
* endpoint fields
* pagination behavior
* visibility rules
* searchable resource types

# 30. PERFORMANCE VALIDATION

Verify:

* Explore grid virtualization
* image loading behavior
* thumbnail usage
* search request frequency
* autocomplete debounce
* cache reuse
* duplicate-request prevention
* scroll performance
* memory behavior
* navigation latency where measurable

Do not claim profiling results that were not measured.

# 31. SHARED MOBILE INTEGRATION

Reuse:

* authentication
* navigation
* deep-link infrastructure
* API client
* server-state architecture
* media primitives
* profile components
* content navigation
* telemetry
* accessibility utilities
* connectivity handling
* error infrastructure

Do not duplicate foundational services.

# 32. OUT OF SCOPE

Do not implement:

* mobile direct messaging
* mobile notification center
* mobile moderation/admin
* backend search/discovery services
* OpenSearch infrastructure
* recommendation/ranking backend
* database migrations
* Kafka infrastructure
* Redis infrastructure
* cloud deployment
* CI/CD production infrastructure
* unrelated web frontend changes
* unrelated profile or feed redesign

Do not create placeholder interfaces for those domains.

# 33. DOCUMENTATION

Update documentation required to explain:

* Explore architecture
* search state management
* autocomplete behavior
* debounce/cancellation
* cache keys
* pagination
* deep-link/query behavior
* privacy decisions
* accessibility decisions
* performance considerations
* contract dependencies
* testing strategy

Document actual behavior only.

# 34. IMPLEMENTATION DISCIPLINE

Do not:

* hardcode discovery content
* hardcode search results
* hardcode users
* hardcode hashtags
* fake ranking
* fake pagination
* fabricate result fields
* create a fake search API
* persist private search data insecurely
* expose secrets
* render unsafe content
* leave required TODO/FIXME placeholders
* suppress type/lint errors without justification
* create a duplicate cache architecture
* claim unsupported search capabilities are implemented

Fixtures belong in tests.

# 35. VALIDATION

Before considering the implementation complete:

* run TypeScript validation
* run linting
* run relevant mobile unit/component tests
* run integration tests
* validate available iOS builds
* validate available Android builds
* exercise Explore loading
* exercise pagination
* exercise refresh
* exercise search
* exercise suggestions
* verify stale-response protection
* verify result-category navigation
* verify deep-link handling where supported
* verify accessibility-critical interactions
* inspect network request frequency
* inspect cache boundaries
* inspect private-data telemetry
* inspect for secrets
* inspect for unsafe content handling
* inspect for placeholder code
* inspect for contract mismatches

If native validation cannot be performed because required tooling is unavailable, report that limitation accurately.

# 36. IMPLEMENTATION REPORT

At the end of the work, provide:

## Implemented

Summarize the Explore, discovery, search, autocomplete, result, and navigation functionality actually implemented.

## Files Changed

List meaningful created and modified files and explain their purpose.

## Contracts Integrated

Identify discovery, search, autocomplete, content, account, pagination, visibility, authorization, and error contracts integrated.

## Tests

List tests executed and their results.

## Validation

List TypeScript, lint, unit, integration, iOS, Android, accessibility, performance, security, and privacy validation actually performed.

## Important Decisions

Document significant engineering decisions and tradeoffs.

## Limitations

Document genuine limitations caused by repository constraints, native tooling, or unavailable external services.

Do not represent future work as completed functionality.

# 37. DEFINITION OF DONE

This prompt is complete only when:

* Explore is operational through real application contracts
* discovery media grids render correctly
* discovery pagination works
* refresh/revalidation works
* search entry works
* autocomplete works
* stale search responses cannot overwrite current results
* supported account/hashtag/content results work
* result categories work where defined
* query/deep-link behavior works where supported
* result navigation works
* loading, empty, unavailable, and failure states are implemented
* responsive mobile behavior works
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

# 38. FINAL EXECUTION DISCIPLINE

Implement this prompt as a bounded production mobile engineering task.

Do not expand into the later mobile domains listed as out of scope.

Do not ask the user to choose among implementation approaches when repository conventions and authoritative contracts establish the correct direction.

Make reasonable engineering decisions based on the repository and project contracts.

Where ambiguity materially affects privacy, navigation, performance, or compatibility, follow the established contract and mobile architecture.

Do not claim completion until the Definition of Done has been satisfied and the stated validation has actually been performed.
