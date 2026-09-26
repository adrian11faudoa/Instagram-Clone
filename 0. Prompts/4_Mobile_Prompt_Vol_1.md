# Instagram — Mobile Prompt — Volume 1

# 1. ROLE

You are the **Senior Mobile Engineering implementation team** responsible for implementing the bounded mobile scope defined in this prompt for the Instagram project.

Operate as a production engineering organization with expertise in:

* React Native
* TypeScript
* iOS and Android application architecture
* mobile navigation
* secure authentication
* mobile API integration
* offline-aware state management
* secure credential and token storage
* push notification foundations
* deep linking
* media-heavy mobile applications
* accessibility
* mobile performance
* automated mobile testing
* observability
* mobile privacy and security

Your responsibility is to implement the assigned mobile scope completely and coherently inside the repository while preserving compatibility with the project's backend contracts and shared domain model.

Do not implement unrelated mobile product areas merely because they exist in the global product definition.

Do not create fake APIs, fake persistence, placeholder screens, TODO-driven implementations, or mock functionality presented as production functionality.

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

This prompt is limited to the **mobile application foundation, authentication, navigation, account/profile foundation, social-graph foundation, networking, state management, secure storage, and mobile platform integration**.

# 3. CURRENT MOBILE ASSIGNMENT

Implement the foundational React Native application architecture required for all later mobile implementation volumes.

This volume owns:

* mobile application bootstrap
* environment/configuration handling
* navigation architecture
* authentication screens and flows
* secure session handling
* token/credential storage
* account lifecycle UI
* profile foundation
* settings foundation
* social-graph foundation
* API integration layer
* server/client state architecture
* request lifecycle handling
* error handling
* app lifecycle handling
* connectivity awareness
* deep-link foundation
* push-notification registration foundation
* analytics/telemetry foundation
* accessibility foundations
* mobile testing foundation
* iOS/Android platform integration where required for this scope
* build and configuration foundations

This prompt does not implement the full feed, Stories, Reels, discovery, messaging, notification center, or moderation experience.

# 4. REPOSITORY INSPECTION

Before modifying code, inspect the repository sufficiently to determine:

* existing mobile directory structure
* React Native framework/version
* package manager
* TypeScript configuration
* native iOS project
* native Android project
* build configuration
* environment/configuration system
* navigation implementation
* authentication implementation, if any
* API client
* generated/shared types
* server-state/data-fetching infrastructure
* client-state management
* local persistence
* secure-storage dependencies
* existing push-notification integration
* deep-link configuration
* analytics/telemetry
* error reporting
* design system
* shared UI primitives
* testing framework
* linting
* formatting
* CI configuration
* relevant architecture and contract documentation

Inspect the authoritative project contracts governing:

* identity
* authentication
* sessions
* account lifecycle
* profiles
* social graph
* identifiers
* timestamps
* API errors
* authorization
* privacy
* configuration
* observability
* deep links
* push notifications
* device registration

Treat the repository and authoritative contract artifacts as the source of truth.

Do not assume that the mobile client may invent APIs independently of the backend contract.

# 5. TECHNOLOGY BASELINE

Use the repository's established mobile technology direction.

The expected baseline is:

* React Native
* TypeScript
* established mobile navigation framework
* established HTTP/API layer
* established server-state architecture
* established client-state architecture
* secure mobile storage
* native iOS and Android integration where required
* established testing framework
* established telemetry/error-reporting infrastructure

Do not introduce a second competing navigation system, API client, global state library, or persistence system unless there is a material engineering reason and compatibility is preserved.

Maintain strict TypeScript typing.

# 6. MOBILE APPLICATION FOUNDATION

Establish a maintainable mobile application structure.

Implement clear boundaries for:

* application bootstrap
* navigation
* authentication
* account/profile
* social graph
* API/networking
* state management
* local persistence
* platform services
* analytics/telemetry
* shared UI
* tests

Avoid creating a monolithic root component that owns unrelated business logic.

Keep domain modules independently testable.

Do not create architecture that requires future mobile volumes to duplicate foundational infrastructure.

# 7. APPLICATION BOOTSTRAP

Implement production-oriented application startup.

Support:

* loading configuration
* initializing required platform services
* initializing telemetry
* restoring secure authentication state
* initializing state/data layers
* selecting the correct authenticated/unauthenticated navigation tree
* handling initialization failure
* preventing duplicate initialization
* safe app startup on cold launch
* appropriate splash/loading behavior

Do not render authenticated application content before authentication restoration and authorization state are safely established.

# 8. ENVIRONMENT AND CONFIGURATION

Implement the mobile configuration system using repository conventions.

Support environment-specific values for:

* API base URLs
* realtime endpoints where required
* application identifiers
* telemetry configuration
* feature configuration that is explicitly supported
* deep-link prefixes
* other public client configuration

Never embed:

* private API keys
* service credentials
* storage credentials
* signing secrets
* backend secrets
* privileged tokens

Clearly distinguish public mobile configuration from confidential server-side configuration.

# 9. NAVIGATION ARCHITECTURE

Implement the foundational navigation hierarchy.

Support:

* unauthenticated navigation
* authenticated navigation
* root application navigation
* stack/screen navigation
* modal presentation where required
* tab/navigation-shell foundation where the product contract requires it
* guarded routes
* deep-link entry points
* navigation reset after authentication changes
* browser-like back behavior where platform conventions require it

Navigation must respect authentication and authorization state.

Do not allow stale authenticated routes to remain reachable after logout.

# 10. AUTHENTICATION

Implement the mobile authentication foundation.

Support the authentication flows defined by the project contract, including as applicable:

* account registration
* login
* logout
* session restoration
* email/identity verification
* password recovery
* credential reset
* session expiration
* authentication failure
* unauthorized API response handling

Use the backend's actual authentication contracts.

Do not fabricate authentication endpoints.

Do not persist raw passwords.

# 11. SECURE SESSION STORAGE

Use secure mobile platform storage for credentials and session material.

Support:

* secure token persistence where the authentication contract requires it
* secure token retrieval
* token refresh
* session replacement
* logout cleanup
* invalid-session cleanup
* device/session metadata where explicitly defined

Use:

* iOS Keychain-compatible secure storage
* Android Keystore-backed secure storage

or the repository's established secure-storage mechanism.

Do not use ordinary local storage, AsyncStorage, plaintext files, or unencrypted databases for secrets.

# 12. TOKEN AND SESSION LIFECYCLE

Implement session lifecycle behavior according to the backend contract.

Handle:

* access-token expiration
* refresh-token flow where supported
* concurrent requests during refresh
* refresh failure
* session invalidation
* logout
* account disablement
* unauthorized API responses

Prevent multiple concurrent refresh requests when a single refresh operation can safely satisfy pending requests.

Never retry indefinitely.

Never expose tokens through logs or telemetry.

# 13. API CLIENT

Implement or integrate the mobile API client.

Support:

* typed requests
* typed responses
* authentication headers according to contract
* timeout handling
* request cancellation where appropriate
* request correlation where supported
* centralized error normalization
* session-expiration handling
* retries only where safe
* network/connectivity classification

Do not scatter raw HTTP calls across screen components.

Do not silently transform contract fields in ways that lose important semantics.

# 14. SERVER-STATE MANAGEMENT

Establish the mobile server-state strategy used by later implementation volumes.

Support:

* query keys
* caching
* invalidation
* mutation lifecycle
* stale data
* refresh
* request deduplication
* pagination-ready abstractions
* authentication-aware cache boundaries

Ensure that authenticated data cannot leak between different user sessions.

Clear or scope private caches appropriately on logout/account change.

# 15. CLIENT-STATE MANAGEMENT

Establish client state for:

* session state
* navigation/application state
* connectivity
* app lifecycle
* transient UI state
* relevant account/profile state

Do not duplicate server state in global client state merely for convenience.

Keep server-authoritative data in the established server-state system.

# 16. CONNECTIVITY AWARENESS

Implement mobile connectivity handling.

Detect and represent:

* online
* offline
* reconnecting
* temporarily unavailable network

Integrate connectivity information with:

* API requests
* authentication refresh
* visible error states
* retry behavior
* app lifecycle
* later offline-capable features

Do not interpret local connectivity as proof that an external API is reachable.

# 17. APP LIFECYCLE

Handle mobile application lifecycle transitions including:

* cold start
* foreground
* background
* inactive/interrupted states where applicable
* return to foreground
* termination/restart

Ensure that:

* sensitive screens do not retain invalid authentication state
* stale data can be refreshed according to policy
* realtime connections are not leaked
* timers and subscriptions are cleaned up
* push/deep-link processing remains correct

Do not assume that background execution will remain active indefinitely.

# 18. ACCOUNT LIFECYCLE

Implement the mobile account-management foundation already represented by the backend contract.

Support where defined:

* profile/account retrieval
* account data refresh
* account settings entry
* logout
* verification state
* password/credential-management entry points
* account deletion flow entry if part of the established contract

Destructive account actions must use explicit confirmation and authoritative server results.

Do not implement server-side deletion logic inside the mobile client.

# 19. PROFILE FOUNDATION

Implement the foundational mobile profile experience.

Support:

* profile header
* avatar
* username
* display name
* biography/public profile fields
* profile statistics where provided
* profile navigation
* profile loading
* profile empty/unavailable states
* profile refresh
* authorized profile actions already defined by the project

Do not implement the full profile-content grid if that belongs to a later mobile content prompt.

# 20. SOCIAL GRAPH FOUNDATION

Implement mobile interfaces for the social-graph operations included in the existing backend contract.

Depending on supported relationships, this may include:

* follow
* unfollow
* follow-request state
* accept follow request
* decline follow request
* block
* relationship-state rendering

Support:

* authoritative state
* optimistic updates where safe
* rollback
* loading
* duplicate-action protection
* authorization failures
* synchronization with already loaded profile state

Do not create a separate client-only relationship store.

# 21. MOBILE FORMS AND VALIDATION

Implement foundational mobile form handling for:

* login
* registration
* password recovery
* verification
* supported account forms
* profile editing where included in this scope
* social actions requiring confirmation

Validation must:

* align with backend validation
* provide accessible feedback
* avoid silently modifying user input
* distinguish client validation from server validation
* preserve form state across recoverable failures where appropriate

Do not duplicate complex backend validation rules if they are likely to diverge.

Client validation is for usability; backend validation remains authoritative.

# 22. ACCESSIBILITY FOUNDATION

Establish accessibility standards for the mobile application.

Support:

* accessible labels
* screen-reader-compatible controls
* logical focus/navigation behavior
* dynamic text considerations
* sufficient touch targets
* meaningful state announcements
* accessible forms
* accessible errors
* accessible dialogs and confirmations

Follow platform accessibility conventions for iOS and Android.

Do not rely solely on color, animation, or icons to communicate critical state.

# 23. RESPONSIVE AND PLATFORM-AWARE UI

Implement layouts that adapt to:

* small phones
* large phones
* tablets where supported
* portrait
* landscape where applicable

Respect platform differences without fragmenting the architecture unnecessarily.

Use platform-specific behavior only where it materially improves correctness or follows platform requirements.

# 24. DEEP-LINK FOUNDATION

Implement the application's foundational deep-linking architecture.

Support:

* application URL scheme or universal/app-link configuration according to project direction
* authenticated deep links
* unauthenticated deep links
* deferred navigation when authentication is required
* invalid link handling
* navigation restoration after login
* safe parameter parsing

Do not place secrets or sensitive tokens inside deep-link URLs.

Do not trust arbitrary deep-link parameters as authorization information.

# 25. PUSH NOTIFICATION FOUNDATION

Establish the mobile foundation required for later notification implementation.

Support where the repository and contracts provide the necessary infrastructure:

* notification permission state
* device token registration
* device registration lifecycle
* token refresh
* logout/unregistration
* deep-link routing from notification payloads
* safe handling of notification payload data

Do not implement the complete notification center in this volume.

Do not store notification-provider secrets in the client.

# 26. ANALYTICS AND TELEMETRY FOUNDATION

Integrate the mobile application with the established observability architecture.

Support:

* application startup events
* navigation/technical events where appropriate
* authentication lifecycle telemetry
* API error diagnostics
* crash/error reporting
* performance measurement
* connectivity diagnostics

Do not collect unnecessary personal or sensitive data.

Do not send:

* passwords
* authentication tokens
* private message content
* private media contents
* sensitive report descriptions
* security credentials

Follow the project's privacy and telemetry contracts.

# 27. SECURITY

The mobile implementation must follow production mobile security principles.

At minimum:

* secure credential storage
* secure logout
* no secrets in source code
* no secrets in telemetry
* certificate/TLS expectations from the project
* safe URL handling
* protected authenticated routes
* safe deep-link parsing
* secure token refresh
* no sensitive information in debug logging
* appropriate screen/data handling on logout
* server-authoritative authorization

Do not claim certificate pinning or other controls unless actually implemented and validated.

# 28. PRIVACY

Respect the project's privacy model.

The mobile client must:

* display only server-authorized data
* avoid unnecessary local persistence of private data
* clear private session state on logout
* avoid exposing private data through screenshots/logging where the platform/product requirements call for mitigation
* avoid unnecessary analytics collection
* follow account-privacy and relationship rules
* protect sensitive settings and credentials

Do not implement client-side shortcuts around privacy restrictions.

# 29. PERFORMANCE

Optimize the mobile foundation for a large-scale social application.

Pay attention to:

* cold-start time
* JavaScript bundle size
* unnecessary rerenders
* navigation initialization
* image loading foundations
* network request duplication
* state hydration
* secure-storage access
* memory usage
* subscription lifecycle
* background/foreground transitions

Avoid premature micro-optimizations that make the foundation difficult to maintain.

# 30. ERROR HANDLING

Centralize mobile errors into the established error architecture.

Handle:

* network failure
* timeout
* unauthorized
* forbidden
* validation error
* rate limiting
* server failure
* malformed responses
* connectivity loss
* session expiration
* secure-storage failure
* deep-link failure
* push-registration failure

User-facing errors must be safe and understandable.

Do not display stack traces or internal service details.

# 31. TESTING

Add meaningful automated tests for the mobile foundation.

At minimum, test:

## Application

* bootstrap
* authenticated/unauthenticated routing
* initialization failure
* app lifecycle handling
* configuration loading

## Authentication

* login success
* login failure
* registration
* verification where supported
* password recovery
* session restoration
* token refresh
* concurrent refresh protection
* logout
* expired session

## Secure Storage

* credential persistence
* credential retrieval
* logout cleanup
* invalid-storage handling
* no plaintext secret persistence

## API

* authenticated request behavior
* unauthorized handling
* timeout
* normalized errors
* retry rules
* request cancellation where supported

## Profile / Social Graph

* profile loading
* profile failure
* follow/unfollow
* follow-request states where supported
* block behavior where supported
* mutation rollback
* synchronization

## Deep Links

* authenticated link
* unauthenticated link
* deferred navigation
* invalid link

## Push Registration

Where supported:

* registration
* token refresh
* logout/unregistration
* invalid payload handling

## Accessibility

Test foundational accessibility semantics and critical authentication flows.

Do not rely exclusively on snapshots.

# 32. CONTRACT VALIDATION

Validate mobile integration against authoritative contracts for:

* authentication
* sessions
* identifiers
* profiles
* relationships
* API errors
* timestamps
* authorization
* configuration
* device registration
* deep links
* push notifications

Do not invent:

* endpoint paths
* token formats
* relationship states
* role values
* device-registration semantics
* notification payload schemas

Use the established backend contract.

# 33. NATIVE PLATFORM INTEGRATION

Where this volume requires native changes, correctly configure:

## iOS

* application identifiers
* URL schemes
* universal-link foundation where applicable
* secure-storage integration
* required permission declarations
* notification-registration foundation
* environment/build configuration

## Android

* application identifiers
* intent/deep-link configuration
* secure-storage integration
* notification-registration foundation
* required permission declarations
* environment/build configuration

Do not add permissions that are not required.

Do not claim production signing configuration or credentials were created unless they actually exist.

# 34. SHARED CROSS-PLATFORM ARCHITECTURE

Prefer shared TypeScript business logic for:

* API models
* domain models
* validation
* authentication orchestration
* query/state logic
* error normalization

Use platform-specific code only where platform APIs materially differ.

Keep native-specific behavior behind clear interfaces.

# 35. OUT OF SCOPE

Do not implement:

* full mobile home feed
* mobile post-detail experience
* complete mobile Stories
* complete mobile Reels
* mobile Explore/search experience
* complete mobile messaging
* complete mobile notification center
* full mobile moderation/admin interface
* backend services
* database migrations
* Kafka infrastructure
* Redis infrastructure
* cloud deployment
* CI/CD production infrastructure
* unrelated web frontend changes

Do not create placeholder screens for these domains merely to claim they exist.

# 36. DOCUMENTATION

Update mobile documentation needed to explain:

* application architecture
* navigation structure
* authentication/session lifecycle
* secure-storage strategy
* API integration
* state-management architecture
* deep-link behavior
* push-registration foundation
* accessibility conventions
* security/privacy decisions
* native platform configuration
* testing strategy
* local development requirements

Documentation must describe what actually exists in the repository.

# 37. IMPLEMENTATION DISCIPLINE

Do not:

* hardcode users
* hardcode credentials
* hardcode access tokens
* hardcode production secrets
* fake authentication
* fake sessions
* store passwords
* fake API responses in production code
* leave TODO/FIXME markers for required functionality
* bypass backend authorization
* use plaintext storage for secrets
* create duplicate networking layers
* create duplicate navigation systems
* suppress type or lint failures without justification
* claim native functionality was configured when it was not

Test fixtures may contain controlled data but must remain inside test infrastructure.

# 38. VALIDATION

Before considering the implementation complete:

* run TypeScript validation
* run linting
* run relevant mobile unit/component tests
* run integration tests available in the repository
* validate iOS compilation where the environment permits
* validate Android compilation where the environment permits
* verify authenticated and unauthenticated navigation
* verify session restoration
* verify token refresh
* verify logout cleanup
* verify secure-storage behavior
* verify deep links
* verify push-registration foundations
* verify profile and social-graph actions
* verify accessibility-critical authentication flows
* inspect debug logs for sensitive-data leakage
* inspect configuration for secrets
* inspect native permissions
* inspect for placeholder implementations
* inspect for contract mismatches

If a platform build cannot be executed because the environment lacks the required native tooling, report that limitation accurately rather than claiming success.

# 39. IMPLEMENTATION REPORT

At the end of the work, provide:

## Implemented

Summarize the mobile foundation, authentication, navigation, profile, social-graph, networking, secure storage, deep-link, and push-registration functionality actually implemented.

## Files Changed

List meaningful files created or modified and explain their purpose.

## Contracts Integrated

Identify authentication, session, profile, relationship, device-registration, deep-link, configuration, and error contracts integrated.

## Tests

List tests executed and their results.

## Validation

List TypeScript, lint, unit, integration, iOS, Android, accessibility, security, and performance validation actually performed.

## Important Decisions

Document significant engineering decisions and tradeoffs.

## Limitations

Document genuine limitations caused by repository constraints, unavailable native tooling, or unavailable external services.

Do not represent future work as completed functionality.

# 40. DEFINITION OF DONE

This prompt is complete only when:

* the mobile application foundation is operational
* application bootstrap is implemented
* authenticated and unauthenticated navigation works
* authentication flows use real backend contracts
* secure session storage is implemented
* token lifecycle is handled correctly
* API networking is centralized and typed
* server/client state management foundations are established
* connectivity awareness is implemented
* app lifecycle behavior is handled
* profile foundation is functional
* supported social-graph actions are functional
* deep-link foundations work
* push-notification registration foundations work where supported
* telemetry/error reporting is integrated
* security and privacy requirements are respected
* accessibility foundations are implemented
* responsive/platform-aware behavior is implemented
* automated tests cover meaningful behavior
* TypeScript validation succeeds
* linting succeeds
* available mobile builds remain valid
* no fake authentication or persistence remains
* no required TODO/FIXME stubs remain
* no secrets are exposed
* documentation reflects actual behavior
* the implementation report accurately describes completed work

# 41. FINAL EXECUTION DISCIPLINE

Implement this prompt as a bounded production mobile engineering task.

Do not expand into the later mobile product domains listed as out of scope.

Do not ask the user to choose among implementation approaches when repository conventions and authoritative contracts establish the correct direction.

Make reasonable engineering decisions from the repository and project contracts.

Where platform-specific behavior differs, follow established iOS and Android conventions while preserving shared domain and API behavior.

Do not claim completion until the Definition of Done has been satisfied and the stated validation has actually been performed.
