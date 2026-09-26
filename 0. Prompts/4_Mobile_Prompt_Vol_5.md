# Instagram — Mobile Prompt — Volume 5

# 1. ROLE

You are the **Senior Mobile Engineering implementation team** responsible for implementing the bounded mobile scope defined in this prompt for the Instagram project.

Operate as a production engineering organization with expertise in:

* React Native
* TypeScript
* realtime mobile applications
* direct messaging
* WebSocket lifecycle management
* offline-aware synchronization
* push notifications
* secure notification payload handling
* attachment workflows
* mobile background/foreground behavior
* optimistic UI
* server-state synchronization
* accessibility
* battery and memory optimization
* automated mobile testing
* observability
* privacy and security

Your responsibility is to implement the assigned mobile scope completely and coherently inside the repository while preserving compatibility with the mobile foundation, backend contracts, realtime architecture, and shared domain model.

Do not implement unrelated mobile product domains merely because they exist in the global product definition.

Do not create fake APIs, fake persistence, placeholder screens, TODO-driven implementations, or simulated realtime behavior presented as production functionality.

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

This prompt is limited to the **mobile direct messaging, realtime conversation, and notification experience**.

# 3. CURRENT MOBILE ASSIGNMENT

Implement the production mobile experience for:

* conversation list
* one-to-one conversations
* group conversations where supported
* message history
* message composition
* message sending
* supported attachments
* delivery state
* read state
* typing indicators
* presence where supported
* realtime message events
* realtime conversation updates
* reconnect and resynchronization
* unread conversation counts
* notification center
* notification pagination
* notification read/unread state
* realtime notifications
* notification-driven navigation
* push-notification integration
* foreground/background notification handling
* accessibility
* privacy/security
* performance
* observability
* automated testing

This prompt does not implement moderation/admin, mobile Explore/search, or other unrelated product domains.

# 4. REPOSITORY INSPECTION

Before modifying code, inspect the repository sufficiently to understand:

* mobile application foundation
* authenticated navigation
* API client
* server-state/data-fetching system
* client-state architecture
* existing realtime/WebSocket infrastructure
* secure storage
* push-notification registration foundation
* deep-link infrastructure
* profile/user components
* media/attachment components
* design-system primitives
* loading/error/empty-state components
* telemetry
* accessibility utilities
* lifecycle/connectivity handling
* iOS notification configuration
* Android notification configuration
* test infrastructure
* relevant documentation

Inspect authoritative contracts governing:

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
* push tokens
* notification payloads
* notification preferences
* authorization
* privacy
* errors

Treat the repository and those contracts as authoritative.

Do not invent event names, message states, notification types, or push-payload schemas.

# 5. TECHNOLOGY BASELINE

Use the established mobile technology:

* React Native
* TypeScript
* established navigation
* established API client
* established server-state architecture
* established client-state architecture
* established realtime infrastructure
* established secure storage
* established push-notification infrastructure
* established media/attachment primitives
* established telemetry
* established testing framework

Do not introduce a second realtime library, notification framework, state system, API client, or persistence layer without a material compatibility reason.

# 6. CONVERSATION LIST

Implement the mobile conversation list.

Support:

* loading
* empty state
* pagination where defined
* participant information
* conversation title where applicable
* latest-message preview where permitted
* latest-message timestamp
* unread count
* muted state where supported
* attachment/media indicators where applicable
* failure state
* retry
* refresh/revalidation
* navigation into the conversation

The list must react to relevant realtime updates.

Do not allow stale HTTP responses to overwrite fresher realtime state.

# 7. ONE-TO-ONE CONVERSATIONS

Implement one-to-one conversation screens.

Support:

* conversation header
* participant identity
* message history
* pagination
* message composition
* message sending
* delivery state
* read state
* typing
* presence where supported
* reconnect behavior
* failure handling
* empty state
* unavailable conversation state

Respect the backend's authorization and participant rules.

# 8. GROUP CONVERSATIONS

Where group conversations are defined by the contracts, support:

* group title
* participant presentation
* participant-aware message rendering
* message history
* sending
* delivery/read behavior
* typing
* realtime updates
* responsive presentation

Do not implement unsupported group-management functionality.

# 9. MESSAGE HISTORY

Implement message-history retrieval according to the authoritative pagination contract.

Support:

* initial history load
* loading older messages
* preserving scroll position when older messages are inserted
* stable ordering
* duplicate prevention
* pagination completion
* pagination retry
* unavailable/deleted-message state
* stale-response protection

Use server-defined message identifiers and ordering.

Do not sort authoritative message history purely by client-generated timestamps.

# 10. MESSAGE RENDERING

Implement reusable mobile message components for supported message types.

Depending on the contracts, this may include:

* text
* image attachments
* video attachments
* supported file/media attachments
* system events
* deleted messages
* unavailable messages

Each message must correctly represent:

* sender
* timestamp
* delivery state
* read state
* pending state
* failure state
* accessibility
* available/unavailable content

Do not render unsupported message types as if they were fully supported.

# 11. MESSAGE COMPOSER

Implement the message composer.

Support:

* text input
* multiline behavior where appropriate
* send action
* keyboard interaction
* validation
* disabled/submitting state
* attachment selection where supported
* attachment cancellation
* failed-send state
* retry
* accessible labels
* responsive/mobile keyboard behavior

Prevent duplicate sends caused by rapid interaction or repeated submission.

# 12. MESSAGE SENDING

Integrate message sending with the real backend contract and realtime system.

Where optimistic rendering is supported:

1. create a temporary client representation using the established temporary-ID convention;
2. display it as pending;
3. submit the authoritative request;
4. reconcile the response;
5. reconcile the realtime acknowledgement;
6. remove or mark failed state on rejection;
7. prevent duplicate insertion.

Support contract-defined idempotency semantics.

Never display both the optimistic message and its authoritative counterpart as two distinct messages.

# 13. DELIVERY AND READ STATE

Implement message-state presentation according to the backend contracts.

Support:

* pending
* sent
* delivered
* read
* failed

only where those exact states are contractually defined.

Implement read-state behavior according to the server's authoritative rules.

Do not infer delivery semantics from client network state.

# 14. READ POSITION AND SCROLL BEHAVIOR

Implement production-quality message scrolling.

Support:

* correct initial positioning
* loading older history without visual jumps
* near-bottom detection
* automatic scrolling only when appropriate
* new-message indicator when the user is reading older messages
* intentional return-to-latest behavior
* orientation/layout changes
* keyboard resizing

Do not force the user to the latest message while they are reading history.

# 15. REALTIME MESSAGE EVENTS

Integrate with the project's established realtime system.

Handle contract-defined events such as:

* new message
* message acknowledgement
* message-state update
* conversation update
* read-state update
* typing state
* presence state

Realtime processing must be:

* authenticated
* typed
* scoped
* validated
* idempotent where required
* resilient to duplicate events
* resilient to out-of-order events
* observable

Do not trust arbitrary client-supplied event data.

# 16. REALTIME CONNECTION LIFECYCLE

Implement mobile realtime lifecycle behavior for:

* connect
* authentication
* connection loss
* reconnect
* connection replacement
* app foreground
* app background
* screen transitions
* logout
* cleanup

Do not create one persistent connection per conversation component.

Reuse the established realtime connection architecture.

# 17. RECONNECT AND RESYNCHRONIZATION

When realtime connectivity is interrupted:

* represent connection state appropriately
* reconnect according to the project strategy
* refresh or resynchronize missed data according to the contract
* reconcile conversation lists
* reconcile unread counts
* reconcile message history where required
* avoid duplicate messages/events

Do not assume that reconnect alone restores missed events.

Do not invent an incompatible synchronization mechanism.

# 18. TYPING INDICATORS

Where supported, implement:

* throttled typing events
* typing start/stop
* cleanup when leaving the conversation
* stale typing expiration
* participant-specific presentation
* correct behavior during reconnect

Do not send a network event for every keystroke.

Typing state must remain ephemeral.

# 19. PRESENCE

Where presence is supported:

* display online/offline state
* display last-seen information where authorized
* handle stale presence
* update on reconnect
* clear state on appropriate lifecycle transitions

Respect account privacy settings.

Do not treat client activity as authoritative presence.

# 20. ATTACHMENTS

Where messaging supports attachments, integrate with the existing mobile media infrastructure.

Support contract-defined attachment types.

Handle:

* selection
* validation
* preview
* upload initialization
* upload progress where supported
* cancellation where supported
* failure
* retry
* authoritative attachment references
* message submission

Do not embed storage credentials.

Do not upload directly to private storage without the contract-defined authorization flow.

# 21. OFFLINE AND DEGRADED NETWORK BEHAVIOR

Use the mobile connectivity foundation to support degraded messaging behavior.

Within actual repository capabilities, support:

* connection-loss indication
* pending outbound messages
* retry
* failed-send state
* reconnect
* resynchronization
* preservation of visible conversation data

Do not claim durable offline message queuing unless it is genuinely implemented and synchronized with the backend.

Clearly distinguish:

* pending
* sent
* failed
* synchronized

# 22. UNREAD COUNTS

Synchronize:

* conversation unread counts
* aggregate messaging unread state
* notification unread counts where applicable

Prevent:

* negative counts
* duplicate increments
* stale resets
* cross-account cache leakage
* inconsistent list/detail state

Use the existing server-state architecture.

# 23. NOTIFICATION CENTER

Implement the mobile notification center.

Support:

* notification list
* supported notification types
* actor/context information
* timestamp
* read/unread state
* navigation target
* pagination
* loading
* empty state
* failure
* retry
* refresh/revalidation
* realtime notification arrival where supported

Do not expose notification types that the backend does not define.

# 24. NOTIFICATION INTERACTION

Support:

* opening a notification
* marking as read when appropriate
* updating unread state
* navigating to the target
* handling unavailable/deleted targets
* pagination
* retry
* synchronization after realtime updates

A notification must not assume that its referenced content still exists.

# 25. PUSH NOTIFICATIONS

Integrate with the push-registration foundation established previously.

Support the actual project contract for:

* device-token registration
* token refresh
* notification delivery handling
* opening the notification from background
* opening the notification from terminated state
* foreground notification handling
* navigation from notification payload
* logout/unregistration
* invalid-token handling where represented by the backend

Do not implement provider credentials in the client.

# 26. NOTIFICATION PAYLOAD SECURITY

Treat notification payloads as untrusted input.

Validate:

* notification type
* target type
* target identifier
* navigation parameters
* optional display metadata

Do not trust a notification payload to grant authorization.

Before opening private content, rely on normal application authorization.

Never place access tokens or secrets into notification payloads.

# 27. NOTIFICATION PREFERENCES

Where mobile settings already expose notification preferences and the backend contract provides them, integrate the supported preference state.

Support only contract-defined preference categories.

Do not implement a separate preference store.

Do not assume that disabling one notification category disables all push delivery.

# 28. APP LIFECYCLE AND NOTIFICATIONS

Correctly handle notifications across:

* foreground
* background
* terminated application
* notification tap
* deep-link continuation
* logout/account switch

Ensure that notification events do not navigate into private content belonging to a previous account session.

Clear pending notification navigation when authentication state changes in a way that invalidates its target.

# 29. ACCESSIBILITY

Implement accessible messaging and notification experiences.

Support:

* accessible conversation titles
* accessible send controls
* accessible attachment controls
* accessible message-state descriptions
* accessible typing/presence announcements where useful
* accessible unread indicators
* accessible notification items
* accessible navigation
* focus/state restoration
* accessible error feedback

Do not communicate critical state exclusively through color or animation.

# 30. PERFORMANCE AND RESOURCE MANAGEMENT

Optimize for long-lived mobile messaging sessions.

Pay attention to:

* large message histories
* list virtualization
* message rerenders
* rapid realtime events
* attachment previews
* image memory
* connection lifecycle
* notification bursts
* cache updates
* battery use
* background behavior

Use virtualization only where it preserves correct scrolling and accessibility.

Ensure realtime subscriptions are released when no longer needed.

# 31. SECURITY AND PRIVACY

Messaging and notifications contain private user data.

The mobile client must:

* respect conversation authorization
* protect private message content
* avoid unnecessary local persistence of messages
* avoid sensitive-content telemetry
* avoid logging tokens
* avoid logging message bodies
* avoid exposing private attachment URLs
* avoid storing secrets in regular storage
* respect account/session boundaries
* clear private session state appropriately on logout
* prevent notification content from bypassing application authorization

Client checks never replace backend authorization.

# 32. OBSERVABILITY

Integrate messaging and notifications with established mobile observability.

Capture technical signals for:

* realtime connection failure
* reconnect failure
* message-send failure
* synchronization failure
* attachment failure
* notification processing failure
* push registration failure
* navigation/deep-link failure
* significant performance problems

Do not collect:

* message bodies
* notification payload contents beyond what is technically necessary
* private media
* passwords
* access tokens
* session secrets
* signed private-media URLs

# 33. TESTING

Add meaningful automated tests covering:

## Messaging

* conversation-list loading
* pagination
* opening conversation
* message-history retrieval
* older-message pagination
* scroll preservation
* message rendering
* composer
* validation
* message send
* optimistic reconciliation
* duplicate prevention
* failed send
* retry
* read state
* unread counts

## Realtime

* new-message event
* duplicate-event handling
* out-of-order event handling
* reconnect
* resynchronization
* typing
* presence
* connection lifecycle
* cleanup

## Notifications

* notification-list loading
* pagination
* empty state
* read/unread
* notification navigation
* realtime notification arrival
* unread count
* unavailable notification target
* failure/retry

## Push

Where native test infrastructure supports it:

* token registration
* token refresh
* foreground delivery
* background/terminated handling
* notification tap navigation
* logout cleanup

## Attachments

Where supported:

* selection
* validation
* upload
* cancellation
* failure
* retry
* message reconciliation

## Security / Privacy

Verify that:

* private content is not sent to telemetry
* notification payloads cannot bypass authorization
* session changes invalidate stale notification navigation
* secrets never enter logs or persistent regular storage

## Accessibility

Test key messaging and notification interactions for accessibility.

Do not rely exclusively on snapshots.

# 34. CONTRACT VALIDATION

Validate against authoritative contracts for:

* conversations
* participants
* messages
* message ordering
* message identifiers
* pagination
* idempotency
* delivery state
* read state
* realtime events
* typing
* presence
* attachments
* notification records
* notification types
* unread counts
* push registration
* notification payloads
* authorization
* privacy
* errors

Do not invent:

* event names
* message states
* notification types
* push payload schemas
* unread semantics
* synchronization rules

# 35. SHARED MOBILE INTEGRATION

Reuse:

* authentication
* secure storage
* navigation
* deep-link infrastructure
* API client
* server-state management
* realtime connection manager
* media infrastructure
* profile/user components
* telemetry
* accessibility utilities
* connectivity handling
* error handling

Do not create duplicate connection managers, notification registries, or authentication mechanisms.

# 36. OUT OF SCOPE

Do not implement:

* mobile moderation/admin interfaces
* backend messaging services
* backend notification services
* push-provider backend infrastructure
* Kafka infrastructure
* Redis infrastructure
* database migrations
* cloud deployment
* CI/CD production infrastructure
* mobile Explore/search
* unrelated Stories/Reels redesign
* unrelated web frontend changes

Do not create placeholder interfaces for these areas.

# 37. DOCUMENTATION

Update documentation required to explain:

* conversation architecture
* message-state lifecycle
* realtime lifecycle
* reconnect/resynchronization
* attachment lifecycle
* unread-count synchronization
* notification-state lifecycle
* push notification handling
* notification navigation
* privacy/security considerations
* accessibility decisions
* performance/resource decisions
* testing strategy
* relevant contracts

Document actual implemented behavior only.

# 38. IMPLEMENTATION DISCIPLINE

Do not:

* hardcode messages
* hardcode conversations
* hardcode notifications
* fake realtime events
* fake push notifications
* fake unread counts
* fake delivery/read states
* store passwords
* expose push-provider secrets
* persist private messages insecurely
* leave required TODO/FIXME placeholders
* suppress type/lint errors without justification
* create duplicate realtime connections
* bypass backend authorization
* claim durable offline messaging without implementing synchronization

Fixtures belong in tests.

# 39. VALIDATION

Before considering the implementation complete:

* run TypeScript validation
* run linting
* run relevant mobile unit/component tests
* run integration tests
* validate available iOS builds
* validate available Android builds
* exercise conversation-list behavior
* exercise message history
* exercise message send/retry
* verify optimistic reconciliation
* verify realtime message events
* verify reconnect/resynchronization
* verify read/unread synchronization
* verify typing/presence where supported
* verify attachment flows
* exercise notification center
* verify notification pagination
* verify realtime notification behavior
* verify push-token lifecycle where tooling permits
* verify notification-tap navigation
* inspect logs for private-data leakage
* inspect storage for secrets/private data
* inspect realtime connection cleanup
* inspect for placeholder functionality
* inspect for contract mismatches

If a native build or push-provider validation cannot be executed because required tooling or external services are unavailable, report that limitation accurately.

# 40. IMPLEMENTATION REPORT

At the end of the work, provide:

## Implemented

Summarize the messaging, realtime, attachment, notification, and push-related functionality actually implemented.

## Files Changed

List meaningful created and modified files with their purposes.

## Contracts Integrated

Identify conversation, message, realtime, attachment, notification, push-registration, authorization, and error contracts integrated.

## Tests

List tests executed and their results.

## Validation

List TypeScript, lint, unit, integration, iOS, Android, realtime, accessibility, security, privacy, and performance validation actually performed.

## Important Decisions

Document significant engineering decisions and tradeoffs.

## Limitations

Document genuine limitations caused by repository constraints, native tooling, push-provider dependencies, or other external capabilities.

Do not represent future work as completed functionality.

# 41. DEFINITION OF DONE

This prompt is complete only when:

* conversation lists are functional
* one-to-one conversations are functional
* supported group conversations are functional
* message history is correctly paginated
* scroll behavior is production-ready
* message composition works
* supported attachments work
* message sending uses real backend contracts
* optimistic messages reconcile correctly
* duplicate messages are prevented
* delivery/read state is synchronized
* realtime messages are integrated
* reconnect and resynchronization work according to the contracts
* typing works where supported
* presence works where supported
* unread counts are synchronized
* notification center is functional
* notification pagination works
* notification read/unread state works
* realtime notifications work where supported
* push-token and notification lifecycle work where supported
* notification-driven navigation works
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

# 42. FINAL EXECUTION DISCIPLINE

Implement this prompt as a bounded production mobile engineering task.

Do not expand into unrelated mobile domains.

Do not ask the user to choose among implementation approaches when repository conventions and authoritative contracts establish the correct direction.

Make reasonable engineering decisions based on the repository and project contracts.

Where ambiguity materially affects privacy, realtime correctness, notification behavior, or compatibility, follow the established contract and mobile architecture.

Do not claim completion until the Definition of Done has been satisfied and the stated validation has actually been performed.
