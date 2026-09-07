# PROJECT 1 — INSTAGRAM-LIKE GLOBAL SOCIAL PLATFORM

# BACKEND PROMPT — VOLUME 4

# DIRECT MESSAGING, REAL-TIME COMMUNICATION, PRESENCE, PUSH & SECURITY HARDENING

You are the Staff Backend Engineering team responsible for implementing the production-grade direct messaging, real-time communication, presence, delivery-state, push-notification integration, and associated security systems of an Instagram-like global social platform.

This prompt is fully standalone. It does not depend on any other prompt, document, previous conversation, previous implementation, previous architecture, previous volume, approval, or hidden context.

You must inspect the current repository before making changes and integrate with compatible existing implementation.

Repository state is the source of truth for existing code.

Implement real production functionality.

Do not generate pseudo-code.

Do not create placeholder implementations.

Do not use TODO/FIXME as substitutes for implementation.

Do not claim functionality exists when it has not been implemented.

Do not regenerate unchanged files.

Preserve existing working unrelated functionality.

==================================================

1. BACKEND SCOPE
   ==================================================

Implement the backend required for:

- one-to-one direct messaging
- conversations
- conversation participants
- text messages
- message attachments
- message persistence
- message delivery state
- read receipts
- typing indicators
- online/offline presence
- WebSocket authentication
- Socket.IO communication
- reconnection
- synchronization after disconnect
- unread message state
- push notifications
- device registration
- FCM integration
- APNS integration
- notification delivery retries
- blocking/privacy enforcement
- message authorization
- abuse prevention
- message rate limiting
- real-time observability
- failure recovery

The system must support multiple backend instances and horizontal scaling.

==================================================
2. REQUIRED TECHNOLOGY
======================

Backend:

- Node.js
- NestJS
- TypeScript

Persistence:

- PostgreSQL
- Prisma ORM

Distributed state:

- Redis

Event streaming:

- Kafka or Redpanda

Background jobs:

- BullMQ

Real-time:

- Socket.IO
- WebSockets

Object storage:

- AWS S3

CDN:

- AWS CloudFront

Push notifications:

- Firebase Cloud Messaging
- Apple Push Notification service

Observability:

- OpenTelemetry
- Prometheus
- Grafana
- Loki
- Tempo

==================================================
3. DOMAIN MODULES
=================

Create or integrate modules for:

- messaging
- conversations
- messages
- attachments
- receipts
- presence
- realtime
- websocket-authentication
- push-notifications
- devices
- messaging-security
- abuse-controls
- event-publishing
- background-workers

Keep controllers, application logic, domain rules, and infrastructure adapters separated.

==================================================
4. CONVERSATION MODEL
=====================

Implement durable conversation records.

Support one-to-one conversations.

A conversation should include:

- conversation ID
- created timestamp
- updated timestamp
- participant relationship
- last-message metadata where appropriate
- state

Participant membership must be stored durably.

Do not infer conversation membership solely from client state.

==================================================
5. PARTICIPANT MODEL
====================

Implement ConversationParticipant with:

- conversation ID
- user ID
- joined timestamp
- role/state where applicable
- last-read position or equivalent synchronization metadata where appropriate
- notification/mute state where applicable

Enforce uniqueness for:

conversation + user

==================================================
6. ONE-TO-ONE CONVERSATION CREATION
===================================

For a direct conversation between users A and B:

1. authenticate requester
2. validate target
3. validate account state
4. evaluate block state
5. evaluate messaging/privacy permissions
6. locate existing conversation
7. create only if one does not exist
8. return conversation

Concurrent creation requests must not create duplicate conversations.

Use database constraints and transactional logic.

==================================================
7. MESSAGE MODEL
================

Implement durable Message records with:

- message ID
- conversation ID
- sender ID
- message type
- content where applicable
- client-generated idempotency identifier where appropriate
- server creation timestamp
- edit state if editing is supported
- deletion state
- moderation state

Do not store unnecessary sensitive metadata.

==================================================
8. MESSAGE TYPES
================

Support at minimum:

- text
- media/attachment reference
- system message where required by product behavior

Message types must be explicitly validated.

Do not accept arbitrary client-defined message types.

==================================================
9. MESSAGE CREATION
===================

Message creation must:

1. authenticate sender
2. validate conversation membership
3. verify sender account state
4. verify recipient availability
5. check block/privacy rules
6. validate content
7. validate attachment ownership if present
8. enforce rate limits
9. persist message transactionally
10. create outbox event
11. return authoritative message state

Do not send external network requests while holding the database transaction open.

==================================================
10. MESSAGE IDEMPOTENCY
=======================

Clients may retry after network failures.

Support client-generated idempotency keys for message creation.

A repeated request with the same valid idempotency key must not create duplicate logical messages.

Persist sufficient information to return the original result.

Handle conflicting reuse of an idempotency key safely.

==================================================
11. MESSAGE ORDERING
====================

Define deterministic ordering.

Every message requires a server-authoritative ordering mechanism such as:

- server timestamp plus unique ID
- monotonically sortable message ID
- conversation sequence

Do not rely solely on mobile device timestamps.

Client timestamps may be retained as metadata when useful but must not determine authoritative order.

==================================================
12. CONVERSATION PAGINATION
===========================

Implement cursor-based message pagination.

Support:

- initial history
- older messages
- synchronization after reconnection
- bounded page sizes

Cursors must be opaque.

Do not allow arbitrary offset pagination over large message histories.

==================================================
13. MESSAGE SYNCHRONIZATION
===========================

A client that reconnects must be able to determine messages it missed.

Support synchronization using a durable cursor/sequence strategy.

Example model:

client-known conversation position
→ request missing range
→ server validates conversation membership
→ return ordered messages
→ return next synchronization position

Do not assume WebSocket delivery was reliable.

==================================================
14. MESSAGE DELIVERY STATES
===========================

Support appropriate message states such as:

- persisted
- accepted
- delivered
- read

Distinguish:

- server persistence
- recipient delivery
- recipient read

A message cannot be considered delivered merely because the sender's request succeeded.

==================================================
15. DELIVERY ACKNOWLEDGEMENT
============================

Where the real-time client acknowledges receipt:

client receives message
→ client sends delivery acknowledgement
→ server validates recipient
→ server updates delivery state
→ server emits event if required

Repeated acknowledgements must be idempotent.

Do not allow one user to acknowledge messages for another participant.

==================================================
16. READ RECEIPTS
=================

Implement read state using a scalable conversation-level cursor or equivalent where appropriate.

Avoid creating unnecessary database rows for every message read when a conversation position can represent the same semantics.

Read operations must:

- authenticate
- verify membership
- update only the user's read state
- be idempotent
- trigger appropriate real-time updates

==================================================
17. UNREAD COUNT
================

Support efficient unread calculation.

Prefer durable read position plus message ordering over incrementing a counter for every message when practical.

A cached unread count may be used for acceleration.

The authoritative state must remain reconstructible.

Handle concurrent:

- message creation
- message deletion
- read updates
- reconnects

==================================================
18. TYPING INDICATORS
=====================

Typing indicators are ephemeral.

Use Redis and WebSockets as appropriate.

Do not persist every typing event to PostgreSQL.

Typing events should:

- expire automatically
- be authorized by conversation membership
- be rate limited
- tolerate packet loss
- not block messaging

Typing indicators must not disclose conversation membership to unauthorized users.

==================================================
19. PRESENCE MODEL
==================

Support online/away/offline presence where product requirements permit.

Presence is ephemeral.

Use Redis or an equivalent distributed mechanism.

Track appropriate state such as:

- user
- session/device
- last heartbeat
- status
- expiration

Do not make process-local memory authoritative for presence.

==================================================
20. PRESENCE HEARTBEAT
======================

WebSocket-connected clients should send/trigger heartbeats.

The server must:

- refresh ephemeral presence
- expire stale connections
- avoid infinite presence retention
- handle abrupt disconnects

A crashed mobile app must eventually transition to offline without relying on graceful disconnect.

==================================================
21. MULTI-INSTANCE SOCKET.IO
============================

The real-time layer must support multiple backend instances.

Use a distributed adapter/coordination layer as appropriate, typically Redis-based.

Do not assume all participants in a conversation are connected to the same server.

Message events must reach clients regardless of which application instance holds their connection.

==================================================
22. WEBSOCKET AUTHENTICATION
============================

Authenticate Socket.IO/WebSocket connections.

The connection handshake must establish:

- authenticated user
- session validity
- device/session information
- authorization context

Do not trust arbitrary user IDs provided by the client.

Expired/revoked sessions must lose access to protected channels.

==================================================
23. WEBSOCKET AUTHORIZATION
===========================

Every conversation subscription must verify membership.

For example:

client requests conversation A
→ server verifies authenticated principal
→ verify membership
→ permit subscription

Do not expose conversation existence to unauthorized users through differentiated error behavior where this creates enumeration risk.

==================================================
24. SOCKET EVENT CONTRACT
=========================

Define versioned events for:

- message.created
- message.delivered
- message.read
- message.deleted
- typing.started
- typing.stopped
- presence.updated
- conversation.updated
- notification.created

Every event should have:

- event ID
- event type
- version
- server timestamp
- correlation ID
- relevant resource identifier

Do not include secrets.

==================================================
25. REAL-TIME DUPLICATE HANDLING
================================

Clients may receive duplicate events because of:

- reconnects
- retries
- adapter behavior
- consumer restarts

Events must have stable identifiers.

Clients should be able to ignore duplicates.

Server-side event generation must also avoid unnecessary duplicate durable state.

==================================================
26. RECONNECTION
================

Support reconnect after:

- temporary network loss
- app backgrounding
- mobile network switching
- server restart
- load-balancer changes

Upon reconnect:

1. reauthenticate
2. re-establish permitted subscriptions
3. synchronize missed durable messages
4. restore relevant unread state
5. restore presence

Do not assume previously received in-memory subscriptions are authoritative.

==================================================
27. MESSAGE ATTACHMENTS
=======================

Support secure attachment workflows using S3.

Do not send large media payloads through WebSocket messages.

Instead:

Client
→ request attachment upload authorization
→ upload to S3
→ validate/process media
→ send attachment reference with message
→ backend verifies ownership/readiness
→ persist message

Attachment objects must be authorized to the message sender.

==================================================
28. ATTACHMENT VALIDATION
=========================

Validate:

- media ownership
- object path
- MIME type
- size
- processing status
- moderation status

Never allow a sender to reference another user's private S3 object.

==================================================
29. PRIVATE MESSAGE MEDIA
=========================

Message attachments may contain private content.

Use controlled access through application authorization and short-lived signed access where necessary.

Do not expose permanent publicly accessible URLs for private message media.

CDN behavior must not bypass message authorization.

==================================================
30. MESSAGE DELETION
====================

Implement message deletion semantics appropriate to the product.

Possible states:

- active
- deleted-for-sender
- deleted-for-all
- moderated

Define exactly which users can see the message after each state transition.

Deletion must be enforced server-side.

==================================================
31. MESSAGE EDITING
===================

Where editing is supported:

- verify sender ownership
- enforce edit window if applicable
- validate new content
- persist edit history metadata where required
- emit message-updated event

Never allow editing another participant's message.

==================================================
32. BLOCKING INTEGRATION
========================

Messaging must respect user blocks.

When A blocks B:

- unauthorized new messages must fail
- protected conversation access must follow product policy
- notification delivery must be restricted
- existing real-time subscriptions must be closed or restricted as necessary

Block state must remain authoritative.

==================================================
33. PRIVACY INTEGRATION
=======================

Messaging must support privacy controls such as:

- who can message
- follower-only messaging
- restricted interactions
- blocked users

These rules must be evaluated server-side at message creation and conversation access.

==================================================
34. MESSAGE REQUESTS
====================

If the product supports message requests:

- store request state explicitly
- prevent unsolicited content from bypassing request rules
- allow accept/reject
- integrate with notifications
- respect block/restriction settings

Do not treat every conversation as automatically trusted.

==================================================
35. MESSAGE RATE LIMITING
=========================

Protect:

- conversation creation
- message creation
- attachment initialization
- typing events
- WebSocket connection attempts
- synchronization requests

Use Redis-backed distributed rate limiting.

Rate policies should consider:

- user
- device
- IP
- endpoint/event type

==================================================
36. SPAM AND ABUSE CONTROLS
===========================

Support detection/controls for:

- mass unsolicited messages
- repeated identical messages
- automated account behavior
- message flooding
- attachment abuse
- conversation-creation abuse
- connection flooding

Potential responses:

- throttling
- temporary messaging restriction
- additional verification
- moderation review

Do not make abuse controls solely client-side.

==================================================
37. MESSAGE EVENTS
==================

Publish durable events such as:

- ConversationCreated
- MessageCreated
- MessageDeleted
- MessageEdited
- MessageDelivered
- MessageRead
- UserBlocked
- UserUnblocked

Events must be suitable for:

- notifications
- analytics
- real-time distribution
- moderation
- auditing

==================================================
38. OUTBOX RELIABILITY
======================

For message creation:

database transaction
→ message record
→ outbox event

Then:

outbox
→ Kafka/Redpanda
→ consumers

Do not rely solely on directly emitting a Kafka event after the transaction without durable event intent.

==================================================
39. REAL-TIME EVENT CONSUMER
============================

Real-time delivery should consume durable domain events or equivalent application events.

Event flow:

MessageCreated
→ authorized real-time fanout
→ active recipient connection
→ event delivery

A user not currently connected must still be able to retrieve the message later.

==================================================
40. PUSH NOTIFICATION PIPELINE
==============================

When the recipient is eligible for push:

MessageCreated
→ notification policy
→ user/device preference evaluation
→ push job
→ FCM/APNS
→ result handling

Do not block message persistence while waiting for push delivery.

==================================================
41. DEVICE REGISTRATION
=======================

Implement device registration.

Track:

- device ID
- user ID
- platform
- push token
- token status
- app version
- last active timestamp

A user may have multiple devices.

Do not assume one token per user.

==================================================
42. PUSH TOKEN SECURITY
=======================

Treat push tokens as sensitive infrastructure identifiers.

Do not expose tokens in:

- logs
- public API responses
- analytics events
- Kafka events unless strictly required

Store them securely.

==================================================
43. FCM ADAPTER
===============

Implement a provider abstraction for Firebase Cloud Messaging.

Map provider responses into application-level categories:

- delivered/accepted
- retryable failure
- invalid token
- permanent failure

Do not expose FCM-specific details throughout the domain layer.

==================================================
44. APNS ADAPTER
================

Implement a provider abstraction for Apple Push Notification service.

Handle:

- authorization
- provider failures
- invalid device token
- transient provider errors
- permanent failures

Keep APNS-specific implementation isolated behind an adapter.

==================================================
45. PUSH RETRIES
================

Use BullMQ for push delivery.

Retry transient failures with bounded exponential backoff.

Do not retry:

- invalid token
- permanent invalid payload
- unauthorized credential configuration

indefinitely.

==================================================
46. INVALID DEVICE TOKENS
=========================

When FCM/APNS indicates an invalid token:

- mark token invalid
- prevent future sends
- optionally clean token asynchronously
- record metric

Do not repeatedly retry permanently invalid tokens.

==================================================
47. PUSH PREFERENCES
====================

Respect notification preferences.

A user must be able to disable appropriate message-related push notifications.

Preference evaluation must happen server-side.

==================================================
48. QUIET / SUPPRESSION RULES
=============================

Where the product supports notification suppression:

- evaluate the user's preference
- avoid sending unnecessary push
- preserve durable message state

Push suppression must not prevent in-app message delivery.

==================================================
49. NOTIFICATION CONTENT
========================

Push payloads should contain minimal necessary content.

Avoid exposing private message bodies unnecessarily on lock screens.

Support privacy-aware notification content policies.

Never place:

- access tokens
- secrets
- internal database IDs without need
- private infrastructure information

into push payloads.

==================================================
50. REAL-TIME NOTIFICATION DELIVERY
===================================

If the recipient has an authenticated active socket:

- deliver new message/notification event in real time where appropriate

If unavailable:

- durable persistence remains sufficient for later retrieval

Do not assume online delivery.

==================================================
51. MESSAGE LIST APIs
=====================

Implement stable APIs for:

- conversation list
- conversation retrieval
- message history
- unread state
- read updates
- message creation
- message deletion
- message synchronization

Use cursor pagination.

Return explicit DTOs rather than database entities.

==================================================
52. CONVERSATION LIST
=====================

Conversation list may be ordered by:

- last relevant message
- updated timestamp
- unread status
- product-defined ranking

Define deterministic tie-breaking.

Do not load all messages to build the conversation list.

Use stored summary fields where justified.

==================================================
53. MESSAGE SEARCH
==================

Do not automatically make private message bodies globally searchable.

Any message-search capability must:

- authenticate
- verify conversation membership
- enforce privacy
- limit query scope
- rate limit
- prevent data leakage

Implement a search index only when justified by product requirements.

==================================================
54. DATABASE INDEXING
=====================

Create indexes for:

Conversations:

- participant
- updated time

Messages:

- conversation + ordered message position
- sender
- created time
- state where useful

Conversation participants:

- conversation + user
- user + conversation

Push devices:

- user
- token status

Presence state may primarily live in Redis and should avoid excessive PostgreSQL writes.

==================================================
55. MESSAGE RETENTION
=====================

Define retention semantics for:

- active messages
- deleted messages
- attachments
- delivery state
- audit logs

Do not automatically hard-delete data without considering:

- product behavior
- moderation
- compliance requirements
- backup retention

==================================================
56. ATTACHMENT CLEANUP
======================

When a message attachment becomes eligible for deletion:

- revoke application access
- remove CDN accessibility where applicable
- delete S3 object asynchronously
- remove derived variants
- record cleanup state

Do not delete an attachment still referenced by an active message.

==================================================
57. REAL-TIME FAILURE MODES
===========================

Handle:

- Redis outage
- Socket.IO adapter failure
- Kafka lag
- worker failure
- push-provider outage
- client reconnect storm

Core durable messaging should remain available whenever possible even if real-time delivery is degraded.

==================================================
58. REDIS FAILURE
=================

If Redis is unavailable:

- do not lose durable messages
- degrade ephemeral presence
- degrade typing indicators
- apply safe fallback for rate limiting
- preserve database-backed functionality

Do not treat Redis-only presence or typing state as durable data.

==================================================
59. KAFKA FAILURE
=================

If Kafka/Redpanda is unavailable:

- persist critical durable message transaction where architecture permits
- retain outbox event
- retry publication
- avoid silently dropping events

Real-time delivery may temporarily lag while durable state remains intact.

==================================================
60. PUSH PROVIDER FAILURE
=========================

If FCM/APNS fails:

- preserve message
- preserve notification state if notification was created
- retry transient failures
- mark permanent failures
- expose metrics

Never fail the message creation request because a push provider is temporarily unavailable.

==================================================
61. CONNECTION FLOOD PROTECTION
===============================

Protect WebSocket endpoints against:

- excessive connection attempts
- authentication brute force
- reconnect storms
- oversized connection metadata
- subscription abuse

Use:

- distributed rate limits
- connection quotas
- backoff
- heartbeat limits

==================================================
62. SECURITY
============

Protect against:

- unauthorized conversation access
- IDOR
- message spoofing
- sender impersonation
- conversation enumeration
- blocked-user bypass
- private attachment leakage
- push-token leakage
- WebSocket hijacking
- replay
- connection abuse
- message flooding

Never authorize based solely on client-provided identifiers.

==================================================
63. AUDIT LOGGING
=================

Audit sensitive messaging operations such as:

- security-sensitive messaging changes
- account messaging restrictions
- administrative access
- moderation actions
- message deletion by moderators
- device registration/revocation where appropriate

Avoid logging private message content unnecessarily.

==================================================
64. OBSERVABILITY
=================

Instrument:

- WebSocket connections
- authentication handshakes
- subscriptions
- message creation
- message persistence
- event publication
- event consumption
- message delivery
- read receipt processing
- push delivery
- Redis presence
- BullMQ jobs

Metrics should include:

- active connections
- connection failure rate
- reconnect rate
- message latency
- persistence latency
- delivery latency
- read latency
- push success rate
- invalid token rate
- queue latency
- Kafka lag
- Redis errors

==================================================
65. DISTRIBUTED TRACING
=======================

Propagate trace context across:

HTTP
→ message service
→ database
→ outbox
→ Kafka/Redpanda
→ real-time consumer
→ Socket.IO
→ push worker
→ FCM/APNS

This must permit end-to-end tracing of delayed or failed message delivery.

==================================================
66. TESTING
===========

Implement automated tests for:

Conversations:

- creation
- duplicate prevention
- membership
- block rules
- privacy rules

Messages:

- creation
- idempotency
- ordering
- pagination
- authorization
- deletion
- editing if supported

Read/delivery:

- acknowledgement
- duplicate acknowledgement
- read state
- unread count

Real-time:

- authentication
- authorization
- subscriptions
- reconnect
- duplicate events
- multi-instance delivery

Presence:

- heartbeat
- expiration
- multi-device state

Push:

- registration
- FCM
- APNS
- retries
- invalid tokens
- preference suppression

==================================================
67. SECURITY TESTING
====================

Explicitly test:

- unauthorized conversation access
- conversation ID enumeration
- message IDOR
- blocked-user messaging
- private attachment access
- forged sender ID
- forged delivery acknowledgement
- forged read acknowledgement
- token replay
- WebSocket authentication bypass
- WebSocket subscription bypass
- push-token abuse
- rate-limit bypass
- reconnect flooding

==================================================
68. LOAD TESTING
================

Test:

- many simultaneous connections
- connection churn
- message bursts
- large conversation lists
- high message-history pagination
- reconnect storms
- push bursts
- Kafka lag
- Redis degradation

The system must remain stable under realistic spikes.

==================================================
69. ACCEPTANCE CRITERIA
=======================

This implementation is complete only when:

- conversations work
- conversation membership works
- duplicate conversation creation is prevented
- messages persist durably
- message idempotency works
- message ordering works
- cursor pagination works
- synchronization after reconnect works
- delivery states work
- read receipts work
- unread state works
- typing indicators work
- presence works
- multi-instance Socket.IO works
- WebSocket authentication works
- WebSocket authorization works
- reconnection works
- attachment upload/access works
- message media privacy works
- blocking rules work
- messaging privacy rules work
- message rate limiting works
- abuse controls exist
- durable messaging events work
- outbox reliability works
- push device registration works
- FCM integration works
- APNS integration works
- invalid token handling works
- push retries work
- notification preferences work
- Redis failure handling exists
- Kafka failure handling exists
- push-provider failure handling exists
- observability exists
- distributed tracing exists
- critical tests pass
- TypeScript compiles
- Prisma migrations succeed
- no required functionality remains a placeholder

==================================================
70. IMPLEMENTATION FINISHING RULE
=================================

Do not stop after creating schemas, WebSocket gateways, interfaces, or service skeletons.

Implement the actual working system.

Inspect the current repository first.

Reuse compatible infrastructure.

Integrate with existing modules.

Do not rewrite unrelated working code.

Validate:

- formatting
- linting
- TypeScript
- Prisma schema/migrations
- HTTP API behavior
- WebSocket behavior
- Redis behavior
- Kafka/Redpanda behavior
- BullMQ workers
- S3 attachment flow
- FCM/APNS adapters
- unit tests
- integration tests
- authorization/security tests
- concurrency-sensitive behavior

The resulting backend must provide a production-grade messaging and real-time communication system capable of operating across multiple application instances.
