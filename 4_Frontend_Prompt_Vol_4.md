You are operating in Senior Engineering Team Mode.

You are the Principal Frontend Architect, Staff Frontend Engineer, Staff UI/UX Engineer, Accessibility Engineer, Performance Engineer, Security Engineer, QA Engineer, Realtime Engineer, and Technical Writer for this Instagram-like global social platform.

The previous frontend volumes have already established:

- frontend architecture
- application shell
- design system
- accessibility foundation
- centralized API client
- TanStack Query architecture
- authentication and session management
- protected routes
- profiles
- follow workflows
- block/restriction workflows
- account/privacy/security settings foundation
- responsive navigation
- feed
- posts
- carousels
- comments
- likes
- saves
- sharing
- stories
- story viewer
- highlights
- Explore
- search
- hashtags
- trending
- audio discovery
- Reels
- vertical video playback
- watch tracking

This volume continues directly from those implementations.

Do not restart the frontend.

Do not replace working architecture.

Do not regenerate unchanged files.

Do not create fake production data.

Do not invent APIs that are not present in the backend contract.

Use the existing repository and backend contracts as the source of truth.

==================================================
VOLUME 4 SCOPE
==============

Implement:

MILESTONE 9
Notifications, activity, and real-time frontend infrastructure.

MILESTONE 10
Direct messaging, conversations, message requests, attachments, reactions, replies, presence, typing, delivery, and read state.

MILESTONE 11
Advanced content creation and publishing workflows.

MILESTONE 12
Creator and business frontend foundations.

==================================================
NON-NEGOTIABLE RULES
====================

Production-grade implementation only.

No pseudo-code.

No placeholders.

No TODOs.

No mock production behavior.

No static screens pretending to be functional.

Every generated file must compile.

Every API request must use the centralized API client.

Every server-state operation must use TanStack Query.

Zustand is only for client-owned state.

Do not put business logic into presentational components.

Do not duplicate permission systems from the backend.

Do not expose sensitive data.

Do not regenerate unchanged files.

Do not break existing functionality.

==================================================
MILESTONE 9 — NOTIFICATIONS, ACTIVITY, AND REAL-TIME
=====================================================

Build the complete notification and activity experience.

==================================================
9.1 NOTIFICATION DOMAIN MODEL
=============================

Create typed frontend models for:

- Notification
- NotificationType
- NotificationActor
- NotificationTarget
- NotificationGroup
- NotificationPage
- NotificationPreferences
- UnreadNotificationSummary

Support backend-defined notification categories such as:

- likes
- comments
- follows
- follow requests
- mentions
- tags
- story interactions
- messages
- creator notifications
- business notifications
- system notifications

Do not invent unsupported notification types.

==================================================
9.2 NOTIFICATION LIST
=====================

Implement the notifications route.

Support:

- cursor pagination
- infinite loading
- unread state
- read state
- grouped notifications where supplied
- actor avatars
- target previews
- timestamps
- navigation to target
- loading
- error
- empty state

==================================================
9.3 NOTIFICATION GROUPING
=========================

Where the backend provides grouped notifications, render them efficiently.

Examples:

- multiple users liked content
- multiple users followed an account
- multiple interactions on the same target

Do not recreate grouping logic on the client if the backend already returns grouped data.

==================================================
9.4 UNREAD COUNT
================

Create a centralized unread-count query.

The navigation shell must be able to display notification badges.

Avoid polling excessively.

Use realtime events where supported.

==================================================
9.5 MARK AS READ
================

Support:

- mark individual notification read
- mark visible notification read where appropriate
- mark all read

Use optimistic updates where safe.

Update only affected caches.

==================================================
9.6 NOTIFICATION NAVIGATION
===========================

A notification can point to:

- profile
- post
- reel
- story
- conversation
- settings
- follow-request page
- moderation/action state where user-visible

Handle deleted/unavailable targets gracefully.

==================================================
9.7 NOTIFICATION REALTIME INSERTION
===================================

When a realtime notification arrives:

- update the notification cache
- increment unread count
- prevent duplicate insertion
- preserve the user's current scroll position
- avoid unnecessary full-page refetches

==================================================
9.8 ACTIVITY EXPERIENCE
=======================

Implement activity/account interaction areas where supported.

Possible sections include:

- follows
- follow requests
- likes/comments activity
- mentions/tags
- account alerts

Use backend-provided categories.

==================================================
9.9 NOTIFICATION PREFERENCES
============================

Build notification settings UI.

Support categories such as:

- posts
- stories
- reels
- comments
- follows
- messages
- live/content alerts where supported
- creator/business notifications
- email notifications
- push notifications

Do not expose settings the backend does not support.

==================================================
9.10 PUSH PERMISSION UX
=======================

Implement browser notification permission handling where web push is supported by the backend architecture.

States:

- unsupported
- not requested
- granted
- denied
- blocked
- error

Do not repeatedly prompt users.

Explain why notifications are useful before requesting permission where appropriate.

==================================================
9.11 PUSH TOKEN REGISTRATION
============================

Integrate browser push registration with the backend abstraction.

Support:

- registration
- refresh
- invalidation
- logout cleanup

Never expose provider credentials.

==================================================
9.12 REALTIME CLIENT MANAGER
============================

Finalize the centralized realtime client.

Requirements:

- one appropriately scoped connection
- authentication
- reconnect
- disconnect
- heartbeat where applicable
- connection status
- event routing
- subscription management
- cleanup

Do not create per-component socket connections.

==================================================
9.13 REALTIME AUTHENTICATION
============================

The realtime connection must authenticate through the backend-supported mechanism.

Handle:

- initial authentication
- expired authentication
- reconnect
- logout
- revoked session

Never expose internal authentication credentials in logs.

==================================================
9.14 REALTIME EVENT BUS
=======================

Create an internal client event-routing layer.

Events may include:

- notification.created
- notification.read
- message.created
- message.updated
- message.deleted
- message.delivered
- message.read
- typing.started
- typing.stopped
- presence.updated
- follow.updated
- content.updated
- content.deleted

Only implement events actually defined by backend contracts.

==================================================
9.15 REALTIME DEDUPLICATION
===========================

Every incoming event must be safely deduplicated when the backend provides event IDs.

Do not process the same event twice.

Use event IDs or equivalent stable identifiers.

==================================================
9.16 REALTIME ORDERING
======================

Respect server-provided ordering metadata where available.

Do not assume network arrival order equals business-event order.

Where ordering cannot be guaranteed:

- reconcile with server state
- avoid destructive local assumptions

==================================================
9.17 CONNECTION HEALTH
======================

Expose safe connection state:

- connecting
- connected
- reconnecting
- disconnected
- auth-failed

Use this state for messaging and notification UX.

Do not show a persistent alarming error for every brief reconnect.

==================================================
9.18 REALTIME TESTS
===================

Test:

- connection
- authentication
- reconnect
- disconnect
- duplicate events
- invalid authentication
- notification insertion
- unread count updates
- message events
- typing
- presence
- cleanup on logout

==================================================
MILESTONE 10 — DIRECT MESSAGING
================================

Build a complete web messaging experience.

==================================================
10.1 MESSAGING ROUTE
====================

Implement:

- /direct

The interface must support desktop and mobile layouts.

Desktop:

- conversation list
- active conversation
- optional information panel

Mobile:

- conversation list
- conversation route
- navigation back to list

==================================================
10.2 CONVERSATION MODEL
=======================

Create typed models for:

- Conversation
- ConversationParticipant
- ConversationSummary
- Message
- MessageAttachment
- MessageReaction
- MessageReply
- MessageReadState
- MessageDeliveryState
- TypingState
- PresenceState
- MessageRequest

==================================================
10.3 CONVERSATION LIST
======================

Display:

- avatar
- participant name
- last message preview
- timestamp
- unread count
- muted state where supported
- online/presence indicator where supported

Handle:

- loading
- empty
- error
- deleted account
- blocked participant
- unavailable conversation

==================================================
10.4 CONVERSATION SEARCH
========================

Support searching conversations where backend provides it.

Use debounce and cancellation.

Do not request search on every keystroke.

==================================================
10.5 MESSAGE TIMELINE
=====================

Build the message timeline.

Requirements:

- cursor pagination
- newest messages
- loading older messages
- scroll anchoring
- date separators
- unread separator
- message grouping
- delivery/read indicators
- deleted messages
- unavailable messages
- attachments

==================================================
10.6 SCROLL POSITION
====================

When loading older messages:

- preserve the user's visible message position
- prevent large scroll jumps

When receiving a new message:

- auto-scroll only if the user is already near the bottom
- otherwise show an unread/new-message indicator

Do not force scroll to bottom while the user is reading older content.

==================================================
10.7 MESSAGE COMPOSER
=====================

Build a production-grade message composer.

Support:

- text
- emoji
- attachments
- send
- multiline input
- keyboard shortcuts
- loading
- retry
- failed message state

On desktop:

- Enter may send according to product behavior
- Shift+Enter creates newline

Make behavior accessible and configurable.

==================================================
10.8 MESSAGE SENDING
====================

Support optimistic message insertion where backend semantics permit.

Each outgoing message should have a local temporary identity until server confirmation.

States:

- composing
- uploading
- sending
- sent
- failed
- retrying

Do not duplicate messages when realtime confirmation arrives.

==================================================
10.9 MESSAGE DEDUPLICATION
==========================

Correlate:

- optimistic client message
- server-created message
- realtime message event

Use:

- client idempotency key
- temporary local ID
- server message ID

according to backend contracts.

==================================================
10.10 MESSAGE DELIVERY
======================

Display backend-provided delivery state:

- sending
- sent
- delivered
- read
- failed

Do not infer delivered/read based only on local timers.

==================================================
10.11 READ RECEIPTS
===================

Implement read state.

Support:

- mark conversation/messages read
- visible-message based read tracking where backend supports it
- deduplicated read updates

Avoid generating one mutation for every pixel of scrolling.

Batch or coalesce read-state updates.

==================================================
10.12 TYPING INDICATOR
======================

Implement typing state.

Requirements:

- debounce typing-start event
- throttle repeated updates
- send typing-stop event
- automatic timeout
- cleanup on unmount
- do not leave stale typing indicators

==================================================
10.13 PRESENCE
==============

Display presence where backend permits.

States may include:

- online
- recently active
- offline
- unknown

Do not display fabricated activity.

Respect user privacy settings.

==================================================
10.14 MESSAGE REQUESTS
======================

Implement message-request interface.

Support:

- incoming requests
- accept
- decline
- delete
- block/report where supported

Do not expose message content beyond backend authorization.

==================================================
10.15 MESSAGE ATTACHMENTS
=========================

Support media attachments.

Types may include:

- images
- videos
- documents where backend supports them

Use the existing upload/media infrastructure.

Support:

- validation
- preview
- upload
- progress
- cancellation
- retry
- failed state

==================================================
10.16 ATTACHMENT PREVIEWS
=========================

Build reusable preview components.

Images:

- thumbnail
- full viewer

Videos:

- poster
- playback

Documents:

- filename
- type
- size
- download/open behavior as supported

Do not expose unsupported file types.

==================================================
10.17 MESSAGE REACTIONS
=======================

Support reaction picker and reaction display.

Implement optimistic interaction only where safe.

Synchronize the affected message rather than reloading the whole conversation.

==================================================
10.18 MESSAGE REPLIES
=====================

Support replying to a specific message.

Display:

- replied-to preview
- message content
- reply relationship

Opening a reply target should scroll to the original message when available.

Handle original-message deletion gracefully.

==================================================
10.19 MESSAGE ACTIONS
=====================

Support backend-defined actions such as:

- reply
- react
- copy
- delete for self
- unsend where supported
- report
- forward/share where supported

Do not expose unsupported actions.

==================================================
10.20 MESSAGE SEARCH
====================

Where backend supports message search:

- create search UI
- debounce
- navigate results
- jump to message
- show surrounding context

Do not preload entire conversation history.

==================================================
10.21 BLOCKED CONVERSATIONS
===========================

Handle backend states for:

- blocked participant
- blocked conversation
- restricted messaging
- unavailable participant

The UI must prevent unsupported actions.

==================================================
10.22 MESSAGE PRIVACY
=====================

Never:

- include message contents in analytics
- log raw messages
- expose private conversation data to unrelated components
- cache private conversations after logout

==================================================
10.23 MESSAGING CACHE
=====================

Design TanStack Query keys for:

- conversations
- conversation messages
- message requests
- participant presence
- unread counts

Do not invalidate all conversations after every new message.

Update affected cache entries directly.

==================================================
10.24 REALTIME MESSAGE INTEGRATION
==================================

When receiving:

- new message
- delivery
- read
- reaction
- reply
- delete

update the appropriate query cache.

Prevent duplicate insertion.

==================================================
10.25 MESSAGE PERFORMANCE
=========================

For large conversations:

- use pagination
- virtualize only if justified
- avoid expensive per-message state
- memoize appropriately
- avoid rerendering the entire timeline for one message update

==================================================
10.26 MESSAGING TESTS
=====================

Test:

- conversation list
- opening conversation
- loading history
- preserving scroll
- new message
- send
- failure/retry
- attachments
- upload
- reactions
- replies
- typing
- presence
- delivery
- read state
- message requests
- block behavior
- realtime duplicates
- logout cleanup

==================================================
MILESTONE 11 — ADVANCED CONTENT CREATION AND PUBLISHING
========================================================

Extend the creation experience into a production-grade composer.

==================================================
11.1 CREATE ROUTE
=================

Implement a dedicated content creation flow.

Support:

- image post
- carousel
- video post
- reel
- story

The creation system must reuse common media-upload infrastructure.

==================================================
11.2 MEDIA PICKER
=================

Support:

- file picker
- drag and drop
- multiple files where allowed
- previews
- validation
- ordering

Validate:

- file type
- size
- count
- aspect ratio where required

Client validation improves UX but does not replace backend validation.

==================================================
11.3 UPLOAD SESSION
===================

Integrate with backend media-upload sessions.

Support:

- initialization
- direct upload
- progress
- cancellation
- completion
- processing
- failure
- retry

Do not upload through the application server when direct upload is supported.

==================================================
11.4 UPLOAD MANAGER
===================

Create a reusable upload manager.

It must support:

- multiple uploads
- concurrency control
- progress
- cancellation
- retries
- failed items
- resumable behavior where backend supports it

Prevent duplicate uploads.

==================================================
11.5 POST COMPOSER
==================

Build the post composer.

Fields:

- media
- caption
- mentions
- hashtags
- location
- audience
- advanced settings where backend supports them

Support:

- draft
- preview
- publish
- scheduling where supported

==================================================
11.6 CAROUSEL COMPOSER
======================

Support:

- multiple media items
- reorder
- remove
- replace
- preview
- per-item validation

Preserve upload progress while reordering.

==================================================
11.7 CAPTION EDITOR
===================

Build caption editor.

Support:

- text
- hashtags
- mentions
- character limits
- validation
- cursor-aware suggestions where supported

Do not inject raw HTML.

==================================================
11.8 MENTION AUTOCOMPLETE
=========================

Implement mention suggestions.

Use debounce.

Cancel stale requests.

Support keyboard selection.

Do not send a request for every cursor movement.

==================================================
11.9 HASHTAG AUTOCOMPLETE
=========================

Support hashtag suggestions where backend provides them.

Use a shared autocomplete abstraction.

==================================================
11.10 LOCATION SELECTION
========================

Implement location search and selection where backend supports it.

Do not expose unnecessary precise location information.

==================================================
11.11 AUDIENCE SELECTION
========================

Support backend-defined audiences:

- public
- followers
- close friends
- private account audience
- custom options where supported

Do not create audience options that the backend cannot enforce.

==================================================
11.12 ADVANCED POST SETTINGS
============================

Where backend supports them:

- comments enabled/disabled
- likes visibility
- branded content
- collaboration
- product tags
- accessibility metadata

Only expose supported capabilities.

==================================================
11.13 DRAFTS
============

Implement draft support.

Support:

- create draft
- auto-save
- open draft
- edit draft
- discard draft
- resume composition

Do not auto-save raw sensitive data to insecure persistence.

Use backend drafts where available.

==================================================
11.14 AUTOSAVE
==============

Autosave must:

- debounce
- avoid unnecessary requests
- handle conflicts
- expose save state
- recover from failures

States:

- saving
- saved
- failed
- offline

Do not claim "saved" before server confirmation when using server-backed drafts.

==================================================
11.15 PUBLISHING
================

Publishing flow:

1. Validate media.
2. Validate metadata.
3. Ensure uploads are complete.
4. Submit publish request.
5. Display processing state.
6. Reconcile server result.
7. Update relevant queries.
8. Navigate appropriately.

Do not assume processing is instantaneous.

==================================================
11.16 PUBLISH PROCESSING
========================

Handle backend states:

- uploading
- processing
- ready
- publishing
- published
- failed

Show meaningful progress/state.

==================================================
11.17 SCHEDULED CONTENT
=======================

Where supported:

- choose date/time
- validate scheduling constraints
- show scheduled state
- edit scheduled content
- cancel schedule

Use server time semantics.

Do not rely exclusively on the browser clock.

==================================================
11.18 CONTENT DELETION
======================

Support owner deletion.

The UI must:

- confirm destructive action
- submit delete
- update local caches
- navigate safely
- remove content from visible surfaces

==================================================
11.19 RESTORATION
=================

Where backend supports restoration:

- display restorable state
- restore
- reconcile content state

Do not expose internal moderation details.

==================================================
11.20 CREATION ERROR RECOVERY
=============================

Recover safely from:

- upload failure
- processing failure
- validation rejection
- authorization failure
- expired upload session
- network interruption
- publish failure

Do not lose user-entered content unnecessarily.

==================================================
11.21 CREATION TESTING
======================

Test:

- single image
- carousel
- video
- file validation
- upload
- progress
- retry
- cancellation
- draft
- autosave
- captions
- mentions
- hashtags
- location
- audience
- publish
- processing
- scheduling
- deletion
- failure recovery

==================================================
MILESTONE 12 — CREATOR AND BUSINESS FRONTEND FOUNDATIONS
=========================================================

Build frontend foundations for creator/business accounts.

==================================================
12.1 CREATOR DASHBOARD
======================

Create creator dashboard architecture.

Support backend-provided sections such as:

- overview
- content performance
- audience
- reach
- engagement
- follower growth
- monetization
- content insights

Do not calculate authoritative analytics client-side.

==================================================
12.2 ANALYTICS DASHBOARD
========================

Build reusable metric components.

Support:

- metric cards
- time-series charts
- comparison periods
- breakdowns
- date filters
- export where supported

Use accessible chart representations.

Do not rely solely on color or visuals to communicate values.

==================================================
12.3 CREATOR CONTENT INSIGHTS
=============================

Support per-content insights:

- impressions
- reach
- likes
- comments
- saves
- shares
- watch time
- completion rate

Use backend-provided values.

==================================================
12.4 FOLLOWER ANALYTICS
=======================

Where backend supports:

- follower growth
- audience demographics
- active periods
- retention

Do not expose sensitive demographic information beyond backend authorization and policy.

==================================================
12.5 BUSINESS PROFILE
=====================

Support:

- business profile presentation
- contact actions
- category
- links
- business metadata
- professional dashboard access

==================================================
12.6 BUSINESS SETTINGS
======================

Support backend-defined:

- business information
- contact methods
- category
- connected assets
- advertising access
- commerce access

==================================================
12.7 ADVERTISING FOUNDATION
===========================

Build frontend foundations for:

- advertiser account
- campaign list
- campaign creation
- ad sets
- creatives
- placements
- budget
- schedule
- status

Do not implement a full advertising optimization engine on the frontend.

The backend remains authoritative.

==================================================
12.8 CAMPAIGN TABLE
===================

Create reusable campaign table.

Support:

- filtering
- sorting
- pagination
- status
- budget
- spend
- impressions
- clicks
- conversions where provided

Use server-side pagination for large datasets.

==================================================
12.9 CAMPAIGN FORM
==================

Support backend-defined creation settings.

Validate fields.

Show server errors.

Prevent duplicate submission.

==================================================
12.10 COMMERCE FOUNDATION
=========================

Create frontend foundations for:

- product catalog
- products
- product variants
- collections
- product tagging
- storefront presentation

==================================================
12.11 PRODUCT CREATION
======================

Support:

- title
- description
- images
- price
- inventory reference
- variants
- collection
- status

Use backend-authoritative validation.

==================================================
12.12 PRODUCT TAGGING
=====================

Where backend supports:

- select products
- attach product to content
- remove product tag
- render product tag on content

Do not expose product data to users without permission.

==================================================
12.13 CREATOR MONETIZATION UI FOUNDATIONS
=========================================

Build frontend architecture for backend-supported:

- subscriptions
- memberships
- gifts
- tips
- earnings
- payouts

Do not display financial state from local assumptions.

Use backend state.

==================================================
12.14 FINANCIAL PRIVACY
=======================

Protect:

- earnings
- payout information
- billing information
- payment status
- financial identifiers

Never include financial data in generic analytics events.

==================================================
12.15 CREATOR/BUSINESS TESTING
==============================

Test:

- dashboard navigation
- analytics loading
- date filters
- content insights
- business profile
- campaign list
- campaign creation
- product catalog
- product creation
- product tagging
- monetization screens
- permission restrictions

==================================================
CROSS-CUTTING QUERY ARCHITECTURE
================================

Create or extend query key factories for:

- notifications
- activity
- conversations
- messages
- message requests
- presence
- typing state
- drafts
- uploads
- creator analytics
- business analytics
- advertising
- commerce
- monetization

Never use arbitrary query keys scattered through components.

==================================================
CROSS-CUTTING REALTIME CACHE RULES
==================================

Realtime events must update only affected state.

Examples:

New message:

- conversation list
- current conversation if open
- unread count

Notification:

- notification list
- unread badge

Message read:

- affected messages
- conversation unread state

Follow:

- profile
- relevant activity/notification state

Do not refetch the whole application for every event.

==================================================
CROSS-CUTTING ACCESSIBILITY
===========================

New functionality must include:

- semantic controls
- accessible labels
- keyboard support
- focus management
- screen-reader announcements
- reduced-motion behavior
- touch-friendly controls

==================================================
CROSS-CUTTING SECURITY
======================

Never rely solely on frontend authorization.

Handle backend:

- 401
- 403
- 404
- 409
- 413
- 429
- 500+

appropriately.

Do not expose private messaging or creator/business information to unauthorized users.

==================================================
CROSS-CUTTING PERFORMANCE
=========================

Avoid:

- unnecessary query invalidation
- unnecessary WebSocket reconnection
- rerendering entire message timelines
- uploading duplicate files
- preloading excessive media
- sending excessive typing/read events
- uncontrolled autosave requests
- large analytics payloads

==================================================
OFFLINE AND FAILURE BEHAVIOR
============================

Support graceful degradation.

Messaging:

- indicate connection state
- preserve unsent message where safe
- allow retry

Uploads:

- preserve recoverable local state
- expose retry

Notifications:

- allow cache refresh after reconnect

Do not claim server success while offline.

==================================================
TESTING REQUIREMENTS
====================

Every milestone must include:

- unit tests
- component tests
- integration tests where appropriate
- accessibility tests
- end-to-end tests
- realtime tests where applicable

Critical E2E journeys:

1. Receive notification.
2. Mark notification read.
3. Open conversation.
4. Send message.
5. Receive message in realtime.
6. Mark messages read.
7. Send attachment.
8. React to message.
9. Reply to message.
10. Handle typing.
11. Create post.
12. Upload media.
13. Save draft.
14. Publish post.
15. Create reel.
16. Edit content.
17. Open creator dashboard.
18. View analytics.
19. Create product.
20. Access business/advertising area.

==================================================
IMPLEMENTATION ORDER
====================

Execute exactly in this order:

MILESTONE 9

1. Notification models
2. Notification queries
3. Notification UI
4. Unread state
5. Notification preferences
6. Push permissions
7. Realtime connection
8. Event routing
9. Realtime cache integration
10. Tests

MILESTONE 10

1. Conversation models
2. Conversation list
3. Conversation route
4. Message timeline
5. Pagination
6. Composer
7. Sending
8. Delivery/read
9. Typing
10. Presence
11. Attachments
12. Reactions
13. Replies
14. Requests
15. Realtime integration
16. Performance optimization
17. Tests

MILESTONE 11

1. Creation architecture
2. Media picker
3. Upload manager
4. Post composer
5. Carousel composer
6. Caption editor
7. Mentions
8. Hashtags
9. Location
10. Audience
11. Drafts
12. Autosave
13. Publishing
14. Scheduling
15. Deletion/restoration
16. Error recovery
17. Tests

MILESTONE 12

1. Creator dashboard
2. Analytics
3. Content insights
4. Business profile
5. Business settings
6. Advertising foundation
7. Campaign UI
8. Commerce foundation
9. Product catalog
10. Product creation
11. Product tags
12. Monetization foundation
13. Financial privacy
14. Tests

==================================================
OUTPUT FORMAT
=============

Before modifying files:

1. Inspect the repository.
2. Identify which frontend volumes are already implemented.
3. Identify reusable abstractions.
4. Verify backend endpoint/event contracts.
5. Do not duplicate existing functionality.

For every implementation step:

1. State the current milestone.
2. State the affected feature.
3. Explain important architectural decisions briefly.
4. Create or modify only required files.
5. Output complete contents for every changed/new file.
6. Never output unchanged files.
7. Add tests.
8. Run typecheck/lint/test/build where available.
9. Fix discovered issues.
10. Keep the repository buildable.

Do not merely describe the implementation.

Actually implement it.

==================================================
FINAL ACCEPTANCE CRITERIA
=========================

At the end of this volume:

- notifications work;
- unread counts work;
- activity works where supported;
- realtime connection is centralized;
- realtime events update caches correctly;
- messaging works;
- conversation lists work;
- message history pagination works;
- message sending works;
- attachments work;
- reactions work;
- replies work;
- presence works;
- typing indicators work;
- delivery/read state works;
- message requests work;
- content creation works;
- uploads work;
- drafts work;
- autosave works;
- publishing works;
- scheduling works where supported;
- creator dashboards work;
- analytics work;
- business foundations work;
- advertising foundations work;
- commerce foundations work;
- monetization foundations work;
- privacy/security requirements are respected;
- critical tests pass;
- TypeScript passes;
- lint passes;
- production build passes.

Do not begin infrastructure/deployment implementation in this phase.

Continue to the next frontend volume only after this volume has been implemented and validated.

BEGIN WITH:

MILESTONE 9 — NOTIFICATIONS, ACTIVITY, AND REAL-TIME FRONTEND INFRASTRUCTURE.
