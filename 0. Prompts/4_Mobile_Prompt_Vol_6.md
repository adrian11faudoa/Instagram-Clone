# Instagram — Mobile Prompt — Volume 6

# 1. ROLE

You are the **Senior Mobile Engineering implementation team** responsible for implementing the bounded mobile scope defined in this prompt for the Instagram project.

Operate as a production engineering organization with expertise in:

* React Native
* TypeScript
* mobile privacy and safety
* reporting workflows
* account and content safety controls
* authorization-aware mobile interfaces
* sensitive-content presentation
* secure local data handling
* accessible mobile forms and dialogs
* automated mobile testing
* observability
* performance and reliability
* iOS and Android platform behavior

Your responsibility is to implement the assigned mobile scope completely and coherently inside the repository while preserving compatibility with the existing mobile foundation, backend contracts, shared domain model, and platform architecture.

Do not implement unrelated mobile product domains merely because they exist in the global product definition.

Do not create fake APIs, fake persistence, placeholder screens, TODO-driven implementations, or simulated moderation behavior presented as production functionality.

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

This prompt is limited to the **mobile reporting, privacy, safety, and moderation-user experience**.

# 3. CURRENT MOBILE ASSIGNMENT

Implement the mobile experience for:

* reporting posts
* reporting comments
* reporting accounts
* reporting Stories where supported
* reporting short-form video where supported
* reporting messages/content where supported
* blocking and unblocking
* muting and unmuting where supported
* restricting and unrestricting where supported
* content-unavailable and moderation-related states
* user-facing safety explanations
* privacy-aware account controls
* account/content safety confirmations
* moderation-result presentation where the user-facing contract provides it
* authorized moderation interfaces only where explicitly supported by the mobile product contract
* accessibility
* privacy/security
* observability
* automated testing

This prompt does not implement backend moderation engines, moderation classifiers, cloud trust-and-safety systems, or unrelated mobile domains.

# 4. REPOSITORY INSPECTION

Before modifying code, inspect the repository sufficiently to understand:

* mobile application foundation
* authenticated navigation
* profile and account screens
* post/feed screens
* Stories and video screens
* comment and messaging screens
* shared dialogs/sheets
* form and selection components
* API client
* server-state/data-fetching architecture
* client-state management
* authorization utilities
* privacy settings
* secure storage
* telemetry
* error handling
* accessibility utilities
* test infrastructure
* iOS/Android configuration
* relevant documentation

Inspect authoritative contracts covering:

* reports
* report categories
* content visibility
* moderation state
* account safety
* block
* mute
* restrict
* authorization
* privacy
* identifiers
* timestamps
* errors
* pagination
* enforcement/result states where user-visible

Treat the repository and contract artifacts as authoritative.

Do not invent report categories, moderation states, privacy behavior, or safety permissions.

# 5. TECHNOLOGY BASELINE

Use the established mobile technology:

* React Native
* TypeScript
* established navigation
* established API client
* established server-state architecture
* established client-state architecture
* established design system
* established secure storage
* established telemetry
* established testing framework

Do not introduce another form library, permission system, state architecture, or navigation architecture without a material compatibility reason.

Maintain strict TypeScript typing.

# 6. REPORT ENTRY POINTS

Integrate reporting into supported mobile content surfaces.

Reportable resources may include:

* posts
* comments
* accounts
* Stories
* short-form videos
* messages
* other explicitly supported resources

The report control must:

* appear only where supported
* identify the resource through the correct canonical identifier
* open the established reporting workflow
* be accessible
* prevent accidental duplicate submissions

Do not expose report actions for resources the backend does not authorize for the current user.

# 7. REPORT WORKFLOW

Implement the report workflow using the actual backend contract.

Support:

* reason selection
* additional information where required
* validation
* submission state
* cancellation
* retry
* duplicate-submission protection
* success state
* failure state
* accessible confirmation behavior

Use only server-defined report reasons.

Do not create a local moderation taxonomy.

# 8. REPORT SUBMISSION

Integrate the report form with the real API.

Handle:

* authenticated submission
* request validation
* loading
* success
* duplicate report
* rate limiting
* authorization failure
* network failure
* server error

After success:

* present an appropriate confirmation
* prevent duplicate submission
* reconcile any contract-defined resource state
* close/reset the workflow appropriately
* restore focus/accessibility context where required

Do not promise a particular enforcement result or moderation timeline unless explicitly guaranteed by the contract.

# 9. ACCOUNT SAFETY CONTROLS

Where supported by the existing contracts, implement:

* block
* unblock
* mute
* unmute
* restrict
* unrestrict
* other explicitly defined safety relationships

Each mutation must:

* use real API contracts
* display current authoritative state
* require confirmation where appropriate
* protect against duplicate requests
* handle failure
* reconcile server state
* update relevant visible surfaces

Do not maintain safety relationships only in local device state.

# 10. BLOCKING

Implement block/unblock behavior.

Support:

* initiation
* confirmation
* loading
* successful state transition
* failure
* retry
* relevant UI synchronization
* navigation behavior according to product contracts

Do not automatically remove every locally visible object unless the product contract defines that effect.

The backend remains authoritative for visibility and authorization.

# 11. MUTING

Where supported, implement mute/unmute.

Support:

* current mute state
* state mutation
* loading
* success
* failure
* state synchronization

Respect any server-defined visibility and notification semantics.

Do not imply that mute changes backend storage or deletion behavior if the contract does not say so.

# 12. RESTRICTING

Where supported, implement restrict/unrestrict.

Support:

* current state
* mutation
* loading
* success
* failure
* authoritative reconciliation

Do not expose private restriction metadata to other users.

# 13. CONTENT SAFETY STATES

Represent backend-provided content states such as:

* unavailable
* removed
* restricted
* hidden
* deleted
* inaccessible
* moderation-limited

Only distinguish states when the backend contract provides the required information.

Do not expose internal moderation reasoning, confidential policy details, reviewer identities, or internal enforcement metadata to ordinary users.

# 14. USER-FACING SAFETY EXPLANATIONS

Where the product contract specifies explanations, provide clear mobile presentation for:

* content removal
* blocked content
* restricted content
* safety action confirmation
* reporting success
* unavailable content
* account restriction

Use neutral, factual UI language.

Do not fabricate moderation explanations.

Do not imply that a report resulted in enforcement unless the server explicitly reports that result.

# 15. MODERATION-RESULT PRESENTATION

Where the backend provides user-visible moderation outcomes, render them correctly.

Potential contract-defined states may include:

* report accepted
* report already exists
* content removed
* action pending
* action completed
* action unavailable

Only implement states actually represented by authoritative contracts.

Do not infer a moderation outcome from a successful HTTP response if the response semantics do not provide one.

# 16. AUTHORIZATION-AWARE UI

The mobile application must respect authorization.

Support:

* hiding unavailable actions
* handling `401`
* handling `403`
* handling expired sessions
* refreshing authorized state where appropriate
* safe navigation behavior
* preventing stale administrative/safety controls from remaining actionable

Client-side permission checks are only UX guards.

Backend authorization remains authoritative.

# 17. PRIVACY SETTINGS INTEGRATION

Where the existing account/settings contracts provide privacy controls, integrate relevant safety settings without creating a separate settings system.

Support only contract-defined options, which may include:

* account visibility
* interaction restrictions
* blocked accounts
* muted accounts
* restricted accounts
* other explicitly provided privacy controls

Do not expose backend-only configuration.

# 18. SENSITIVE CONTENT HANDLING

Some reporting and moderation flows may contain sensitive content.

The mobile implementation must:

* display sensitive material only when authorized
* avoid unnecessary automatic media playback
* avoid unnecessary downloads
* avoid persistent storage of sensitive evidence
* protect private screenshots/previews where product/platform policy requires mitigation
* avoid sending sensitive content to telemetry
* handle restricted media safely

Do not bypass media authorization to support a moderation workflow.

# 19. SECURE LOCAL DATA HANDLING

Do not persist sensitive moderation or reporting data in ordinary storage unless explicitly required and protected by the architecture.

Avoid storing:

* report descriptions
* private moderation details
* sensitive account information
* private media references
* confidential enforcement data

Where transient persistence is unavoidable for usability, use the secure storage mechanisms and retention rules established by the repository.

# 20. ACCESSIBILITY

Implement accessible safety workflows.

Support:

* accessible report dialogs/sheets
* meaningful form labels
* accessible report-reason selection
* readable validation errors
* accessible confirmation prompts
* destructive-action semantics
* screen-reader announcements
* focus restoration
* sufficient touch targets
* accessible unavailable-content states

Do not communicate safety state only through color or iconography.

# 21. RESPONSIVE MOBILE PRESENTATION

Safety and reporting workflows must work across:

* small phones
* large phones
* tablets where supported
* portrait
* landscape where applicable

Ensure:

* controls remain reachable above the keyboard
* dialogs do not clip
* long report reasons remain readable
* confirmation buttons remain visible
* scrollable content remains accessible
* system safe areas are respected

# 22. PERFORMANCE

Optimize safety interfaces for reliable interaction without unnecessary network or memory costs.

Avoid:

* repeated state refetching
* duplicate mutation requests
* loading sensitive media unnecessarily
* re-rendering large content trees when only a dialog changed
* retaining confidential evidence longer than needed

Use the established cache and invalidation model.

# 23. ERROR HANDLING

Handle:

* invalid report
* unauthorized
* forbidden
* duplicate report
* rate limiting
* content unavailable
* target deleted
* network failure
* timeout
* stale state
* conflicting mutation
* server failure

Present errors safely and understandably.

Do not display internal moderation infrastructure details.

Do not expose stack traces or raw server payloads.

# 24. SECURITY AND PRIVACY

The mobile implementation must:

* respect account privacy
* respect server authorization
* prevent unauthorized moderation data access
* prevent unsafe deep-link access
* avoid insecure sensitive-data storage
* avoid sensitive telemetry
* avoid logging reports
* avoid logging moderation content
* avoid exposing signed private media URLs
* never embed secrets
* follow session/CSRF/TLS expectations
* securely handle account/session changes

Do not use local permission state as a security boundary.

# 25. OBSERVABILITY

Integrate with existing mobile observability.

Capture technical signals for:

* report failures
* safety-action failures
* authorization failures
* privacy-control failures
* significant UI errors
* state synchronization problems
* important performance failures

Do not capture:

* report descriptions
* private message contents
* private media
* sensitive moderation data
* access tokens
* passwords
* signed private-media URLs

Use privacy-preserving identifiers consistent with the project standards.

# 26. TESTING

Add meaningful automated tests covering:

## Reporting

* report entry-point visibility
* report reason selection
* validation
* successful submission
* duplicate submission
* failure
* retry
* authorization handling
* success confirmation

## Safety Controls

* block
* unblock
* mute
* unmute
* restrict
* unrestrict
* mutation failure
* rollback/reconciliation
* stale-state handling

## Content States

* removed
* unavailable
* restricted
* deleted
* unauthorized

## Privacy / Security

Test that:

* sensitive data is not written to ordinary storage
* reports are not sent to telemetry
* unauthorized moderation information is not rendered
* private content cannot be opened solely through local state
* unsafe content is not executed as native/HTML code

## Accessibility

Test:

* report workflow keyboard/assistive interaction where applicable
* confirmation focus
* form errors
* accessible labels
* destructive-action semantics

Do not rely exclusively on snapshots.

# 27. CONTRACT VALIDATION

Validate against authoritative contracts for:

* reports
* report categories
* report responses
* block
* mute
* restrict
* privacy settings
* moderation/content statuses
* authorization
* pagination
* identifiers
* timestamps
* errors

Do not invent:

* report categories
* enforcement states
* permission values
* privacy options
* moderation explanations
* API response fields

# 28. SHARED MOBILE INTEGRATION

Reuse:

* authentication
* authorization utilities
* navigation
* profile screens
* content screens
* API client
* server-state/cache infrastructure
* secure storage
* design-system dialogs/forms
* telemetry
* accessibility utilities
* error infrastructure

Do not create a separate safety-state system.

When shared components need changes, preserve existing behavior and add regression tests.

# 29. ROUTING AND DEEP-LINK SAFETY

Integrate safety workflows with established mobile routing.

Support:

* report dialogs/routes
* account-safety destinations
* privacy settings
* authorized administrative destinations only if explicitly supported
* invalid target handling
* authentication-gated continuation

Never trust deep-link parameters to grant permission.

# 30. OUT OF SCOPE

Do not implement:

* automated moderation classifiers
* machine-learning moderation
* backend moderation services
* backend report services
* trust-and-safety analytics pipelines
* moderation database migrations
* moderator/admin mobile dashboards unless explicitly defined as part of the mobile product contract
* Kafka infrastructure
* Redis infrastructure
* cloud deployment
* CI/CD production infrastructure
* unrelated messaging/search/feed work
* unrelated web frontend changes

Do not create placeholder interfaces for these areas.

# 31. DOCUMENTATION

Update documentation required to explain:

* mobile reporting flow
* safety-control architecture
* privacy-control integration
* authorization-aware UI behavior
* sensitive-content handling
* secure local-data decisions
* error handling
* accessibility decisions
* telemetry/privacy decisions
* testing strategy
* relevant contracts

Document only functionality actually implemented.

# 32. IMPLEMENTATION DISCIPLINE

Do not:

* hardcode report categories
* hardcode permissions
* hardcode moderation states
* fake reports
* fake safety actions
* fake privacy settings
* fake backend enforcement results
* store confidential report data insecurely
* expose secrets
* bypass backend authorization
* leave required TODO/FIXME placeholders
* suppress type/lint errors without justification
* expose internal moderation information to ordinary users
* claim functionality that depends on unavailable backend contracts

Fixtures belong only in tests.

# 33. VALIDATION

Before considering the implementation complete:

* run TypeScript validation
* run linting
* run relevant mobile unit/component tests
* run integration tests
* validate available iOS builds
* validate available Android builds
* exercise report submission
* exercise report failure/retry
* exercise block/unblock
* exercise mute/unmute
* exercise restrict/unrestrict where supported
* verify unavailable/removed-content states
* verify authorization behavior
* verify privacy settings integration where supported
* inspect secure/local storage
* inspect telemetry for sensitive-data leakage
* inspect deep-link safety
* inspect for secrets
* inspect for placeholder code
* inspect for contract mismatches

If native or external-service validation cannot be performed because required tooling/services are unavailable, report the limitation accurately.

# 34. IMPLEMENTATION REPORT

At the end of the work, provide:

## Implemented

Summarize the reporting, safety, privacy, and moderation-related mobile functionality actually implemented.

## Files Changed

List meaningful created and modified files with their purposes.

## Contracts Integrated

Identify reporting, safety, privacy, authorization, moderation-state, and error contracts integrated.

## Tests

List tests executed and their results.

## Validation

List TypeScript, lint, unit, integration, iOS, Android, accessibility, security, privacy, and performance validation actually performed.

## Important Decisions

Document significant engineering decisions and tradeoffs.

## Limitations

Document genuine limitations caused by repository constraints, unavailable native tooling, external dependencies, or missing contracts.

Do not represent future work as completed functionality.

# 35. DEFINITION OF DONE

This prompt is complete only when:

* reporting is integrated into supported mobile content surfaces
* report workflows use real backend contracts
* report validation works
* duplicate submissions are prevented
* success/failure/retry states work
* supported block/unblock actions work
* supported mute/unmute actions work
* supported restrict/unrestrict actions work
* privacy controls integrate with authoritative account settings where applicable
* unavailable/removed/restricted content states are represented correctly
* authorization-aware UI works
* sensitive information is handled securely
* accessibility requirements are addressed
* responsive mobile presentation works
* observability is integrated without sensitive-data leakage
* automated tests cover meaningful behavior
* TypeScript validation succeeds
* linting succeeds
* available iOS/Android builds remain valid
* no fake production APIs or persistence remain
* no required TODO/FIXME stubs remain
* no secrets are exposed
* documentation reflects actual behavior
* the implementation report accurately describes completed work

# 36. FINAL EXECUTION DISCIPLINE

Implement this prompt as a bounded production mobile engineering task.

Do not expand into unrelated mobile domains.

Do not ask the user to choose among implementation approaches when repository conventions and authoritative contracts establish the correct direction.

Make reasonable engineering decisions based on the repository and project contracts.

Where ambiguity materially affects privacy, authorization, or safety, follow the authoritative contract and server-enforced behavior.

Do not claim completion until the Definition of Done has been satisfied and the stated validation has actually been performed.
