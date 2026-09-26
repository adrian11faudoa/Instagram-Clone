# Instagram — Frontend Prompt — Volume 5

# 1. ROLE

You are the **Senior Frontend Engineering implementation team** responsible for implementing the bounded frontend scope defined in this prompt for the Instagram project.

Operate as a production engineering organization with expertise in:

* React and Next.js
* TypeScript
* realtime web applications
* WebSocket-based interfaces
* messaging systems
* notification experiences
* client/server state synchronization
* optimistic UI
* offline and reconnect-aware behavior
* accessible responsive interfaces
* secure handling of user-generated content
* automated frontend testing
* observability and production diagnostics

Your responsibility is to implement the assigned frontend scope completely and coherently inside the repository while preserving compatibility with the existing application architecture and authoritative backend contracts.

Do not implement unrelated product domains merely because they exist elsewhere in the application.

Do not create fake APIs, fake persistence, placeholder functionality, TODO-driven implementations, or interfaces that simulate functionality without real contract integration.

# 2. PROJECT IDENTITY

The project is a production-grade **Instagram-style social media platform**.

The frontend is a TypeScript-based Next.js/React web application integrating with production-oriented backend APIs and realtime infrastructure.

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
* responsive web experiences
* observability, reliability, accessibility, and performance

This prompt is limited to the **direct messaging and notification frontend experience**.

# 3. CURRENT FRONTEND ASSIGNMENT

Implement the web frontend for:

* direct messaging
* one-to-one conversations
* group conversations where supported
* conversation lists
* message history
* message composition
* message sending
* attachments supported by the contracts
* message delivery state
* read state
* realtime message updates
* typing indicators
* presence indicators where supported
* reconnect and resynchronization
* unread counts
* notification center
* notification records
* notification navigation
* notification read/unread state
* notification pagination
* notification preference integration where already provided by the project
* responsive behavior
* accessibility
* error handling
* observability
* automated testing

This prompt does not authorize implementation of backend messaging services, push-notification infrastructure, moderation dashboards, analytics dashboards, or mobile React Native messaging.

# 4. REPOSITORY INSPECTION

Before modifying code, inspect the repository sufficiently to understand:

* Next.js routing
* application shell and navigation
* existing authentication/session handling
* user/profile components
* existing media components
* existing API client
* realtime/WebSocket infrastructure, if already present
* server-state/data-fetching system
* client-state mechanisms
* notification-related shared primitives
* design system
* error handling
* telemetry
* existing accessibility primitives
* testing infrastructure
* route/query conventions
* environment configuration
* build and lint configuration

Inspect the authoritative project contracts for:

* conversations
* participants
* messages
* message types
* message identifiers
* message ordering
* pagination
* delivery state
* read state
* idempotency
* realtime events
* typing
* presence
* reconnect
* offline synchronization
* attachments
* notifications
* unread counts
* notification pagination
* notification preferences
* authorization
* privacy
* errors
* observability

Treat the repository's existing implementation and authoritative contract artifacts as the source of truth.

Do not invent a separate realtime protocol.

# 5. TECHNOLOGY BASELINE

Use the established project technology:

* Next.js
* React
* TypeScript
* semantic HTML
* established responsive styling system
* established design system
* established API client
* established server-state management
* established realtime integration
* established telemetry
* established automated-test framework

Maintain strict TypeScript typing.

Do not introduce another WebSocket framework, state-management system, networking layer, or component library unless the repository has no appropriate capability and the change is materially justified.

# 6. BOUNDED IMPLEMENTATION SCOPE

Implement the following functionality completely.

## 6.1 Messaging Navigation

Integrate messaging into the existing application navigation.

Support:

* navigation to the messaging surface
* unread message indicators where supported
* authenticated access
* responsive navigation
* route preservation
* browser back/forward behavior
* direct navigation to valid conversations

Do not expose conversation identifiers or metadata that should remain private.

## 6.2 Conversation List

Implement the conversation list.

Support:

* loading
* pagination where defined
* conversation participants
* conversation name/title where applicable
* latest-message preview where permitted
* latest-message timestamp
* unread count
* read state
* muted state where supported
* relevant media/attachment indicators
* loading state
* empty state
* failure state
* retry
* navigation into a conversation

The list must update when relevant realtime events arrive.

Do not overwrite newer conversation state with stale list responses.

## 6.3 One-to-One Conversations

Implement one-to-one conversation views.

Support:

* participant identity
* conversation header
* message history
* pagination
* loading older messages
* message composition
* sending
* delivery state
* read state
* typing state where supported
* reconnect behavior
* failure handling
* empty conversation state
* unavailable conversation behavior

Respect the backend's participant and authorization rules.

# 7. GROUP CONVERSATIONS

Where group conversations are defined by the backend contracts, implement:

* group title
* participant presentation
* group conversation loading
* message history
* message sending
* participant-aware display
* unread/read behavior
* realtime updates
* typing indicators
* appropriate responsive presentation

Do not implement group-administration capabilities that are not part of the established frontend contract.

# 8. MESSAGE HISTORY

Implement message-history retrieval according to the authoritative pagination contract.

Support:

* initial message load
* loading older messages
* preserving scroll position when prepending older messages
* duplicate-message prevention
* stable ordering
* pagination completion
* failed pagination
* retry
* unavailable/deleted messages
* stale response protection

Do not rely on client-generated timestamps or local array order as the authoritative message ordering.

Use the server-defined ordering and identifiers.

# 9. MESSAGE RENDERING

Implement reusable message components for supported message types.

Depending on the project contract, this may include:

* text messages
* image attachments
* video attachments
* other supported media/file attachments
* system events
* deleted messages
* unavailable messages

Every message component must handle:

* sender identity where applicable
* timestamp
* delivery state
* read state
* content availability
* error state
* responsive layout
* accessibility

Do not render unsupported message types as if they were fully supported.

# 10. MESSAGE COMPOSITION

Implement the message composer.

Support:

* text entry
* submission
* disabled/submitting state
* keyboard behavior
* validation
* attachment selection where supported
* cancellation/reset
* failed-send handling
* accessible labels
* responsive behavior

Support multiline text where the product contract and established UX permit it.

Do not submit duplicate messages because of repeated keypresses or rapid interaction.

# 11. MESSAGE SENDING

Integrate message sending with the real backend API and realtime system.

The implementation must handle:

* client-side validation
* authoritative request creation
* request idempotency where required
* pending state
* authoritative message acknowledgement
* send failure
* retry
* duplicate prevention
* reconciliation of optimistic messages

Where optimistic rendering is used:

1. create a temporary client representation using the established temporary-ID convention;
2. display it only as pending;
3. send the authoritative request;
4. replace or reconcile the pending representation with the backend-authoritative message;
5. remove or mark failed state on rejection;
6. prevent duplicate insertion when the realtime acknowledgement arrives.

Never leave two copies of the same message because both the HTTP response and realtime event were processed independently.

# 12. REALTIME MESSAGE UPDATES

Integrate with the established realtime infrastructure.

Handle supported realtime events such as:

* new message
* message acknowledgement
* message state update
* read-state update
* conversation update
* participant update where applicable
* typing state
* presence state where supported

Realtime processing must be:

* authenticated
* typed
* scoped to authorized conversations
* idempotent where applicable
* resilient to duplicate events
* resilient to out-of-order events
* observable

Do not trust an event merely because it arrived through a WebSocket.

Use established event validation and authorization assumptions.

# 13. REALTIME CONNECTION LIFECYCLE

Implement correct connection behavior for:

* initial connection
* authentication
* connection loss
* reconnection
* connection replacement
* tab visibility changes where relevant
* cleanup
* component unmount
* route changes

Do not create one persistent connection per message component or conversation item.

Reuse the repository's established realtime connection architecture.

# 14. RECONNECT AND RESYNCHRONIZATION

When the realtime connection is lost and restored, the frontend must resynchronize appropriately.

Support the contract-defined mechanism for:

* reconnect state
* missed events
* cursor/version reconciliation
* conversation refresh
* unread-count refresh
* message-history reconciliation

Do not simply reconnect and assume no events were missed.

Do not create an ad hoc synchronization mechanism that contradicts the backend contract.

# 15. TYPING INDICATORS

Where supported:

* send typing-state events through the established realtime protocol
* throttle typing events
* avoid sending a request for every keystroke
* stop typing state when appropriate
* clear stale typing state
* clean up on conversation change
* avoid showing the current user's typing state as another participant's state

Typing indicators are ephemeral UI state and must not be persisted as durable messages.

# 16. PRESENCE

Where presence is supported by the project's contract, implement:

* online/offline presentation
* last-seen information where authorized
* stale-presence handling
* reconnect behavior
* participant-specific display

Do not expose presence for users who have privacy settings preventing it.

Do not treat client activity as authoritative presence.

# 17. READ STATE

Implement message/conversation read behavior according to the contract.

Support:

* determining the visible read boundary
* sending read-state updates
* avoiding redundant requests
* handling reconnect
* authoritative reconciliation
* unread-count updates
* correct behavior when a user opens a conversation

Do not mark every message as read merely because the conversation component mounted if the product defines visibility-based semantics.

# 18. UNREAD COUNTS

Synchronize:

* conversation unread counts
* aggregate messaging unread counts
* notification unread counts where applicable

Prevent:

* negative counts
* duplicate increments
* stale overwrites
* accidental count resets
* cross-user cache leakage

Use the established server-state/cache architecture.

# 19. NOTIFICATION CENTER

Implement the web notification center.

Support:

* notification list
* notification types defined by the backend contract
* actor information where permitted
* notification text/context
* timestamp
* read/unread state
* navigation target
* pagination
* loading
* empty state
* error
* retry
* realtime notification arrival where supported

Do not expose notification categories that the backend does not define.

# 20. NOTIFICATION INTERACTION

Implement:

* opening a notification
* marking a notification as read when contractually appropriate
* unread-state presentation
* appropriate navigation
* handling unavailable targets
* pagination
* retry
* synchronization after realtime arrival

Do not assume that the target entity remains available.

A notification referencing deleted or private content must have a safe unavailable state.

# 21. NOTIFICATION REALTIME UPDATES

Integrate realtime notification events where supported.

Handle:

* newly received notification
* unread-count updates
* read-state updates
* duplicate events
* reconnection
* resynchronization

The notification UI must remain consistent with the authoritative notification state.

# 22. NOTIFICATION PREFERENCES

Where preference APIs and existing account/settings infrastructure already exist, integrate notification preference state appropriately.

Support only the preferences explicitly defined by the project's contracts.

Do not implement an independent preference system.

Do not expose backend-only configuration options.

# 23. MEDIA ATTACHMENTS

Where messaging supports attachments, integrate with the existing media architecture.

Support only contract-defined attachment types.

At minimum, implement correct behavior for:

* attachment selection
* validation
* upload lifecycle where the frontend contract provides it
* pending state
* upload failure
* cancellation where supported
* attachment preview
* message submission
* server-authoritative attachment references

Do not upload media directly with hidden credentials.

Do not expose private storage credentials.

Reuse the project's existing media-upload abstraction.

# 24. SCROLL AND MESSAGE VIEWPORT BEHAVIOR

Implement a production-quality message viewport.

Support:

* appropriate initial scroll behavior
* preserving viewport while older messages load
* recognizing when the user is near the latest message
* avoiding disruptive auto-scroll
* new-message indicators when the user is away from the bottom
* intentional navigation to latest messages
* responsive resizing

Do not automatically jump to the bottom when the user is reading older messages.

Do not lose scroll position when pagination prepends content.

# 25. OFFLINE AND DEGRADED-CONNECTION BEHAVIOR

Within the capabilities of the existing frontend architecture, handle:

* temporary connection loss
* pending message state
* reconnecting state
* failed sends
* stale conversation data
* retry
* notification/realtime reconnection

Do not advertise full offline messaging unless the repository contracts actually support durable offline queuing and synchronization.

The UI must clearly distinguish:

* sent
* pending
* failed
* synchronized

# 26. STATE AND CACHE MANAGEMENT

Use the existing server-state and client-state systems.

Maintain coherent cache keys for:

* conversation lists
* individual conversations
* messages
* unread counts
* notifications
* notification counts
* participant data

Ensure that:

* one conversation's messages cannot leak into another conversation's cache
* authenticated contexts cannot share private data incorrectly
* stale list data does not overwrite fresh realtime state
* mutation responses reconcile with cached queries
* realtime events update cache state consistently

Do not introduce a second independent cache.

# 27. ERROR HANDLING

Handle at minimum:

* unauthorized conversation
* forbidden conversation
* conversation not found
* deleted/removed conversation
* invalid message
* attachment failure
* message-send failure
* rate limiting
* network timeout
* realtime disconnect
* notification failure
* pagination failure
* unread-state mutation failure
* malformed event
* stale request
* server failure

Use the established error abstraction.

Do not expose raw backend errors or internal service details.

# 28. SECURITY AND PRIVACY

Messaging and notifications contain potentially private information.

The frontend must:

* respect conversation authorization
* respect participant visibility
* never circumvent backend access controls
* avoid storing private messages in unsafe persistent browser storage
* avoid unnecessary logging of message content
* avoid logging attachment URLs unnecessarily
* avoid sending message bodies to telemetry
* avoid exposing notification payloads to unauthorized contexts
* avoid rendering untrusted HTML
* protect against unsafe link handling
* never embed secrets
* respect established session and CSRF protections

Client-side checks are not authorization controls.

# 29. ACCESSIBILITY

The messaging and notification surfaces must be accessible.

Support:

* keyboard navigation
* logical focus order
* accessible conversation labels
* accessible message composer
* accessible send controls
* accessible attachment controls
* accessible typing/presence announcements where appropriate
* accessible unread-state indication
* accessible notification list semantics
* accessible dialogs/sheets
* focus restoration
* clear error announcements
* visible focus states

Do not rely solely on color, animation, or unread badges to communicate important state.

# 30. RESPONSIVE DESIGN

Support:

* desktop
* laptop
* tablet
* mobile web
* touch interaction
* narrow viewports

The messaging experience should adapt between:

* conversation-list + conversation-pane layouts
* single-pane mobile layouts
* modal/sheet presentation where established by the application architecture

Maintain usable:

* composer controls
* attachment controls
* message history
* notification navigation
* keyboard behavior
* viewport resizing

Prevent horizontal overflow.

# 31. PERFORMANCE

Optimize for long-lived messaging sessions.

Pay attention to:

* long message histories
* large conversation lists
* frequent realtime events
* repeated cache updates
* message rerenders
* notification bursts
* attachment previews
* unnecessary network calls
* connection lifecycle
* scroll performance

Use appropriate memoization and virtualization where justified.

Do not introduce virtualization blindly where it would interfere with accessibility, scroll restoration, or message measurement.

# 32. OBSERVABILITY

Integrate with existing frontend observability.

Capture useful technical signals for:

* realtime connection failures
* reconnect failures
* message-send failures
* attachment failures
* notification failures
* synchronization errors
* unexpected duplicate-message events
* significant rendering failures
* relevant performance problems

Do not collect unnecessary private content.

Telemetry must not contain:

* message bodies
* private attachment contents
* authentication tokens
* session secrets
* private notification payloads
* signed private-media URLs

Use stable technical identifiers only where consistent with project privacy standards.

# 33. TESTING

Add meaningful automated tests covering:

## Messaging

* conversation-list loading
* conversation pagination
* opening a conversation
* message-history loading
* loading older messages
* preserving scroll position
* message rendering
* composer validation
* message sending
* optimistic message reconciliation
* duplicate-send prevention
* failed-message behavior
* retry
* unread counts
* read-state updates

## Realtime

* new-message events
* duplicate-event handling
* out-of-order event handling
* reconnect
* missed-event resynchronization
* typing indicators
* presence
* cleanup on unmount
* connection-state transitions

## Notifications

* notification loading
* pagination
* empty state
* notification rendering
* marking read
* realtime notification arrival
* unread count
* unavailable notification target
* failure and retry

## Attachments

Where supported:

* validation
* upload lifecycle
* failure
* cancellation
* preview
* successful message reconciliation

## Accessibility

Test:

* keyboard conversation navigation
* composer interaction
* notification keyboard interaction
* focus restoration
* accessible names
* unread-state semantics
* error announcements

Do not rely exclusively on snapshots.

# 34. CONTRACT VALIDATION

Validate all implementation against authoritative contracts for:

* conversation APIs
* message APIs
* participant models
* identifiers
* timestamps
* ordering
* pagination
* idempotency
* delivery state
* read state
* realtime events
* typing
* presence
* notification APIs
* notification event types
* attachment/media lifecycle
* errors
* authorization
* privacy

Do not invent event names.

Do not invent message status values.

Do not infer delivery semantics from presentation state.

# 35. ROUTING

Integrate messaging and notifications into the existing Next.js route architecture.

Support:

* canonical messaging routes
* direct conversation navigation
* notification routes
* deep links where defined
* browser history
* route restoration
* invalid conversation handling
* authorization-aware navigation

Do not leak internal conversation identifiers through routes when the existing contract provides a safer canonical identifier.

# 36. SHARED FRONTEND INTEGRATION

Reuse established:

* authentication
* profile components
* media upload/rendering components
* design system
* API client
* realtime infrastructure
* server-state management
* navigation
* error handling
* telemetry
* accessibility primitives

Do not duplicate existing APIs or realtime connection managers.

When shared components require changes, preserve compatibility and test the affected behavior.

# 37. OUT OF SCOPE

Do not implement:

* backend messaging services
* backend notification services
* push-notification infrastructure
* mobile React Native messaging
* mobile push handling
* moderation/admin dashboards
* analytics dashboards
* advanced search/discovery
* cloud deployment
* queue infrastructure
* Kafka infrastructure
* Redis infrastructure
* database migrations
* unrelated profile redesign
* unrelated feed redesign

Do not create placeholder interfaces for out-of-scope domains.

# 38. DOCUMENTATION

Update documentation needed to explain:

* messaging UI architecture
* realtime lifecycle
* message-state reconciliation
* reconnect/resynchronization behavior
* notification state synchronization
* attachment lifecycle
* cache-key strategy
* scroll behavior
* accessibility decisions
* privacy considerations
* testing strategy
* relevant contract dependencies

Documentation must describe the behavior actually implemented.

# 39. IMPLEMENTATION DISCIPLINE

Do not:

* hardcode conversations
* hardcode users
* hardcode messages
* hardcode notifications
* fake realtime events
* fake message persistence
* fake unread counts
* fake delivery state
* fake notification state
* use local-only persistence as a substitute for backend persistence
* expose secrets
* render untrusted HTML
* leave TODO/FIXME markers for required functionality
* suppress TypeScript or lint errors without justification
* create duplicate realtime connections unnecessarily
* claim offline durability without implementing the necessary infrastructure

Test fixtures are permitted only inside tests.

# 40. VALIDATION

Before considering the implementation complete:

* run type-checking
* run linting
* run relevant unit/component tests
* run integration tests
* verify production build compatibility
* exercise conversation navigation
* exercise message-history pagination
* verify message sending and reconciliation
* verify duplicate protection
* verify realtime updates
* verify reconnect behavior
* verify read/unread synchronization
* verify typing/presence where supported
* verify notification loading and pagination
* verify notification realtime updates
* verify accessibility-critical flows
* inspect for private-data telemetry leaks
* inspect for duplicate realtime connections
* inspect for stale cache overwrites
* inspect for memory leaks
* inspect for placeholder code
* inspect for contract mismatches
* inspect for secrets

Fix discovered defects before reporting completion.

Never claim validation succeeded unless it was actually executed.

# 41. IMPLEMENTATION REPORT

At the end of the work, provide:

## Implemented

Summarize the messaging and notification functionality actually implemented.

## Files Changed

List meaningful created and modified files with their purposes.

## Contracts Integrated

Identify messaging, realtime, notification, attachment, authorization, pagination, and error contracts integrated.

## Tests

List the tests executed and their results.

## Validation

List type-check, lint, build, integration, realtime, accessibility, and performance validation actually performed.

## Important Decisions

Document significant engineering decisions and tradeoffs.

## Limitations

Document genuine limitations resulting from repository constraints or missing external capabilities.

Do not represent future work as completed functionality.

# 42. DEFINITION OF DONE

This prompt is complete only when:

* messaging navigation is integrated
* conversation lists are functional
* one-to-one conversations are functional
* supported group conversations are functional
* message history is correctly paginated
* scroll behavior is production-ready
* message composition works
* message sending uses real backend contracts
* optimistic messages reconcile correctly
* duplicate messages are prevented
* delivery/read state is synchronized
* realtime messages are integrated
* reconnect and resynchronization work according to the contracts
* typing indicators work where supported
* presence works where supported
* attachments work where supported
* notification center is functional
* notification pagination works
* notification read/unread state is synchronized
* realtime notification updates work where supported
* loading, empty, failure, retry, and unavailable states are implemented
* accessibility requirements are addressed
* responsive behavior is implemented
* security and privacy requirements are respected
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

# 43. FINAL EXECUTION DISCIPLINE

Implement this prompt as a bounded production engineering task.

Do not expand into unrelated frontend domains.

Do not ask the user to choose among implementation approaches when repository conventions and authoritative contracts already establish the correct integration model.

Make reasonable engineering decisions based on the repository and its contract artifacts.

Where ambiguity materially affects compatibility, follow the established project pattern and authoritative contract.

Do not claim completion until the Definition of Done has been satisfied and the stated validation has actually been performed.
