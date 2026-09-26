# Instagram — Backend Prompt — Volume 5

# 1. ROLE

You are the **Staff Backend Engineering team** responsible for implementing the direct-messaging, realtime communication, and notification backend domains for the **Instagram** project.

Operate with the combined responsibilities of:

* Staff Backend Engineer
* Realtime Systems Engineer
* Distributed Systems Engineer
* Messaging Systems Engineer
* Database Engineer
* Security Engineer
* Privacy Engineer
* Reliability Engineer
* Performance Engineer
* QA-minded Backend Engineer
* Observability Engineer

This is a **bounded backend implementation assignment**.

You must implement the real backend functionality defined by this prompt.

Do not implement unrelated future product areas merely because they appear in the global Instagram product vision.

The mandatory rule for this task is:

**Implement only the current prompt's scope.**

---

# 2. PROJECT IDENTITY

**Project Name:** Instagram

**Product Type:** Production-grade visual social networking platform.

The backend is part of a larger system containing:

* identity and accounts;
* profiles;
* social graph;
* posts;
* stories;
* short-form video;
* media;
* engagement;
* feed;
* discovery/search;
* direct messaging;
* notifications;
* moderation;
* administration;
* analytics;
* web;
* mobile;
* infrastructure.

The completed platform is intended to support approximately:

* 100 million registered accounts;
* 20 million daily active users;
* 2 million peak concurrent active sessions;
* approximately 100,000 sustained API requests per second;
* approximately 250,000 requests per second during peak bursts;
* large numbers of simultaneous realtime connections;
* high-volume message traffic;
* high-volume notification generation and delivery.

These are global architectural targets.

This prompt implements the **direct-messaging, realtime, and notification backend foundation**.

---

# 3. CURRENT BACKEND ASSIGNMENT

Implement:

1. one-to-one conversations;
2. group conversations;
3. conversation participants;
4. conversation lifecycle;
5. message persistence;
6. message attachments;
7. message ordering;
8. message idempotency;
9. message delivery state;
10. message read state;
11. realtime connection management;
12. realtime event delivery;
13. typing indicators;
14. presence where justified;
15. reconnect/synchronization behavior;
16. offline synchronization APIs;
17. message pagination;
18. notification persistence;
19. notification generation;
20. notification preferences;
21. notification read/unread state;
22. notification aggregation where appropriate;
23. push-notification provider boundaries;
24. relevant asynchronous jobs;
25. Redis realtime state;
26. event-stream integration;
27. authorization/privacy;
28. blocking/restriction-aware messaging;
29. observability;
30. security;
31. reliability;
32. tests;
33. documentation.

This milestone must provide the backend foundation for messaging and notifications without implementing the web or mobile clients.

---

# 4. REPOSITORY INSPECTION

Before modifying or creating code, inspect the repository.

Inspect, where present:

* backend application structure;
* account/profile modules;
* social graph;
* content;
* engagement;
* feed;
* event/outbox infrastructure;
* Kafka/event streaming;
* background queues;
* Redis;
* existing WebSocket/realtime infrastructure;
* database schema;
* migrations;
* API conventions;
* authorization policies;
* notification abstractions;
* push-provider adapters;
* observability;
* tests;
* documentation.

Treat the repository as the source of truth for actual implementation state.

Do not assume another AI prompt was executed.

Do not assume another Claude conversation exists.

Do not fabricate messaging or notification infrastructure.

Reuse compatible existing infrastructure.

---

# 5. TECHNOLOGY BASELINE

Use the repository's existing backend stack with the project baseline of:

* TypeScript;
* Node.js;
* PostgreSQL;
* Redis;
* durable event streaming;
* background jobs;
* WebSocket or equivalent realtime transport;
* REST APIs;
* structured validation;
* structured logging;
* tracing/metrics;
* automated tests.

Do not introduce a new messaging technology merely because it is fashionable.

Use durable PostgreSQL persistence for authoritative message state.

Use Redis for ephemeral realtime state where justified.

---

# 6. BOUNDED IMPLEMENTATION SCOPE

## In Scope

Implement:

* conversation creation;
* conversation retrieval;
* group conversation creation;
* participant membership;
* participant management;
* message creation;
* message persistence;
* message attachments as media references;
* message pagination;
* message idempotency;
* message delivery states;
* read states;
* typing indicators;
* presence where justified;
* realtime connection authentication;
* realtime event envelopes;
* realtime delivery;
* reconnect behavior;
* synchronization cursors;
* missed-event synchronization;
* notification records;
* notification generation;
* notification preferences;
* notification read/unread state;
* notification aggregation where appropriate;
* push notification integration boundaries;
* notification delivery jobs;
* retries and deduplication;
* Redis realtime state;
* relevant database migrations;
* events;
* observability;
* security;
* privacy;
* tests;
* documentation.

## Out of Scope

Do not implement:

* web messaging UI;
* mobile messaging UI;
* media-processing pipelines;
* media transcoding;
* message search;
* end-to-end encryption;
* full moderation workflows;
* administration UI;
* complete analytics pipelines;
* full cloud/realtime infrastructure provisioning;
* recommendation systems;
* feed functionality.

This prompt must establish extension boundaries where necessary, but must not implement excluded domains.

---

# 7. CONVERSATION MODEL

Implement a durable conversation domain.

A conversation must support:

* conversation ID;
* type;
* creator/owner where applicable;
* lifecycle state;
* created time;
* updated time;
* last-message reference or equivalent derived state;
* participant relationships.

Conversation types must be explicit.

At minimum support:

* direct;
* group.

Do not rely on participant count alone to determine conversation type.

---

# 8. DIRECT CONVERSATIONS

Implement one-to-one conversation semantics.

Prevent unauthorized creation of duplicate logical direct conversations where product semantics require a single canonical conversation per participant pair.

Where a canonical pair relationship is required:

* normalize participant ordering;
* enforce uniqueness;
* handle concurrent creation safely.

Do not solve duplicates solely with an application pre-check.

---

# 9. GROUP CONVERSATIONS

Implement group conversation creation.

Support:

* group creation;
* participant membership;
* member addition where authorized;
* member removal where authorized;
* leaving a conversation;
* conversation lifecycle.

Do not implement arbitrary administrative roles unless required by the current product model.

Use explicit authorization for membership changes.

---

# 10. PARTICIPANT MODEL

Implement a conversation-participant record supporting:

* conversation ID;
* account ID;
* membership state;
* joined time;
* left time where applicable;
* role where explicitly required;
* last-read position where appropriate.

A participant may belong to many conversations.

Do not embed participant data directly in the conversation record.

---

# 11. CONVERSATION AUTHORIZATION

Every conversation operation must verify:

* authenticated account;
* active membership where required;
* participant lifecycle;
* block relationship;
* account state;
* conversation state.

Do not allow arbitrary conversation-ID access.

A user knowing a conversation ID must not gain access to it.

---

# 12. BLOCKING AND RESTRICTIONS

Messaging must respect the existing relationship policy.

At minimum consider:

* user blocks another user;
* another user blocks the caller;
* restrictions;
* private-account messaging rules where applicable;
* account suspension.

Define behavior for:

* new conversation creation;
* message sending;
* existing conversation visibility;
* participant additions.

Do not duplicate the social-graph data model.

Consume centralized relationship policy where available.

---

# 13. MESSAGE MODEL

Implement durable message persistence.

A message must support, as appropriate:

* message ID;
* conversation ID;
* sender account ID;
* client-generated idempotency identifier;
* message type;
* text/body where applicable;
* attachment references;
* server creation timestamp;
* edit timestamp where supported;
* deletion state;
* sequence/order information.

Do not place arbitrary unbounded data into the main message row.

---

# 14. MESSAGE TYPES

Support an explicit message-type model.

At minimum support:

* text;
* media attachment;
* system/conversation event where required.

Do not use ambiguous nullable fields to represent unrelated message semantics when a typed model is more appropriate.

Future message types must be extensible without breaking existing clients.

---

# 15. MESSAGE ATTACHMENTS

Messages may reference media assets through stable identifiers.

Do not store media binaries in the message record.

Validate:

* sender authorization;
* media ownership;
* media availability;
* attachment type;
* lifecycle state.

Do not implement full media upload or transcoding here.

Use the existing media domain contracts.

---

# 16. MESSAGE ORDERING

Implement deterministic ordering.

Use a server-authoritative message sequence or equivalent ordering model.

The ordering model must support:

* pagination;
* realtime delivery;
* reconnect;
* duplicate handling;
* concurrent senders.

Do not rely solely on client timestamps.

Client timestamps may be metadata, but server-side ordering must remain authoritative.

---

# 17. MESSAGE IDEMPOTENCY

Message creation must support retries.

Use a client-generated idempotency identifier or equivalent stable mutation key.

The same logical request retried due to:

* timeout;
* connection failure;
* client retry;

must not create duplicate messages.

Define:

* key scope;
* retention;
* conflict behavior;
* response replay behavior;
* cleanup.

---

# 18. MESSAGE PERSISTENCE FLOW

Implement a durable send flow:

1. authenticate sender;
2. validate conversation membership;
3. validate block/restriction policy;
4. validate message input;
5. validate attachment references;
6. assign authoritative message identity;
7. persist message;
8. persist required event/outbox state;
9. make the message available to realtime delivery;
10. return authoritative message state.

Realtime delivery must not be the durable source of truth.

---

# 19. MESSAGE DELIVERY STATES

Implement appropriate message delivery states.

At minimum distinguish:

* persisted;
* delivered;
* read.

Where appropriate also support:

* failed.

Delivery state must be associated with the intended recipient/participant where necessary.

Do not assume that one global message status is sufficient for group conversations.

---

# 20. DELIVERY ACKNOWLEDGEMENTS

Implement realtime or API acknowledgement semantics for delivery.

A delivery acknowledgement must have a clear meaning.

Distinguish:

* server accepted;
* message persisted;
* recipient connection received;
* message read.

Do not collapse all of these into one ambiguous "delivered" state.

---

# 21. READ STATE

Implement read-state tracking.

Support:

* marking a conversation through a specific message position as read;
* retrieving unread state;
* determining the latest read sequence;
* efficient unread calculations.

Avoid writing one row per read event when a monotonic read cursor can represent the state.

Use an idempotent read-state update.

---

# 22. READ RECEIPTS

Where the product requires explicit message-level receipts, support them through a scalable model.

For group conversations, avoid creating an unnecessarily large message × participant matrix unless genuinely required.

Prefer participant read cursors when they can represent equivalent product semantics.

---

# 23. MESSAGE EDITION AND DELETION

If message editing/deletion is part of the current product behavior:

Implement:

* authorization;
* lifecycle state;
* updated timestamp;
* deletion state;
* relevant event.

Do not permanently mutate historical semantics in a way that prevents audit/debugging where the architecture requires lifecycle history.

Do not implement irreversible physical erasure if a tombstone is required to keep distributed clients consistent.

---

# 24. MESSAGE PAGINATION

Implement cursor-based pagination for conversation messages.

Define:

* stable ordering;
* cursor contents;
* page size;
* maximum page size;
* deleted-message behavior;
* participant authorization;
* reconnect compatibility.

Do not use large offsets.

---

# 25. CONVERSATION PAGINATION

Implement cursor-based pagination for conversation lists.

Sort by an explicit derived field such as:

* latest relevant activity.

Do not rely on implicit database row order.

Define behavior when a conversation becomes inactive.

---

# 26. REALTIME CONNECTION AUTHENTICATION

Realtime connections must be authenticated.

Define:

* authentication during connection;
* session/token validation;
* account identity;
* authorization context;
* session revocation behavior.

A client must not be able to subscribe to arbitrary conversation channels.

---

# 27. REALTIME TRANSPORT

Implement a WebSocket or repository-compatible realtime transport.

Support:

* connection;
* authentication;
* subscription;
* unsubscribe;
* message events;
* delivery acknowledgements;
* read events;
* typing events;
* synchronization requests;
* reconnect.

Use one canonical realtime event envelope.

---

# 28. REALTIME EVENT ENVELOPE

Every realtime event must identify, as appropriate:

* event ID;
* event type;
* event version;
* sequence/order information where required;
* conversation/resource ID;
* timestamp;
* payload.

Do not expose internal persistence models directly.

Keep the envelope versionable.

---

# 29. REALTIME AUTHORIZATION

Before sending a realtime event to a connection, enforce:

* authenticated identity;
* active conversation membership;
* current account state;
* block/restriction policy where relevant.

Do not assume that authorization granted when the connection opened remains valid forever.

Handle membership removal and session revocation.

---

# 30. HORIZONTAL REALTIME SCALING

The realtime implementation must support multiple application instances.

Do not store authoritative connection ownership solely in process memory without a strategy for distributed delivery.

Use Redis/pub-sub, a compatible event bus, or another appropriate shared mechanism where required.

Connection-local state may remain in memory when it is ephemeral and reconstructible.

---

# 31. REALTIME FAN-OUT

For a new message:

1. persist it;
2. publish a durable event or equivalent;
3. route the realtime event to currently connected authorized recipients.

Do not synchronously iterate through all participants in a way that blocks persistence under high fan-out.

Group conversation fan-out must remain bounded and observable.

---

# 32. TYPING INDICATORS

Implement typing indicators as ephemeral realtime state.

Typing events must:

* not require durable message persistence;
* expire automatically;
* be rate limited;
* be scoped to authorized conversation participants.

Redis or another ephemeral coordination mechanism may be used.

Do not write every keystroke to PostgreSQL.

---

# 33. PRESENCE

Implement presence only to the level justified by the product requirements.

Where supported, presence should be:

* ephemeral;
* TTL-based;
* connection-aware;
* privacy-aware;
* tolerant of stale state.

Do not represent presence as permanent database state.

Do not claim exact online status after connectivity loss when the system cannot prove it.

---

# 34. RECONNECT BEHAVIOR

Implement reconnection support.

When a client reconnects:

* authenticate again or validate the existing session safely;
* identify synchronization position;
* detect missed events;
* return missed durable events from the authoritative message/event store;
* restore subscriptions;
* avoid duplicate processing.

Do not rely solely on realtime transport history that may be lost when a connection closes.

---

# 35. SYNCHRONIZATION CURSOR

Define a durable synchronization position.

The cursor must support:

* message/event continuity;
* reconnect;
* gap detection;
* replay;
* duplicate suppression.

Use server-authoritative sequence semantics.

Do not rely solely on wall-clock timestamps for replay correctness.

---

# 36. MESSAGE OFFLINE SYNCHRONIZATION

Implement an API or service capability that allows a client to recover messages missed during disconnection.

Support:

* conversation selection;
* sync cursor;
* bounded result sets;
* pagination;
* current authorization;
* message deletion/tombstone semantics.

Do not implement an unbounded "return the entire conversation" endpoint.

---

# 37. REDIS REALTIME STATE

Use Redis for appropriate ephemeral state:

* connection/session routing;
* typing indicators;
* presence;
* realtime fan-out coordination;
* short-lived synchronization metadata where justified.

Define:

* key namespace;
* TTL;
* serialization;
* ownership;
* failure behavior.

Redis must not become the authoritative message store.

---

# 38. REALTIME FAILURE BEHAVIOR

When realtime transport or Redis is unavailable:

* durable message persistence must remain authoritative;
* message sending must not create false delivery claims;
* clients must be able to synchronize later;
* realtime failures must be observable.

Do not roll back a successfully persisted message merely because realtime delivery failed.

---

# 39. NOTIFICATION DOMAIN

Implement durable in-app notification records.

A notification should support:

* notification ID;
* recipient;
* type;
* actor where applicable;
* related resource;
* aggregation key;
* read state;
* created time;
* expiration where appropriate.

Do not store entire source-domain entities inside notifications.

Use stable resource identifiers.

---

# 40. NOTIFICATION TYPES

Support notifications originating from relevant current product domains, such as:

* likes;
* comments;
* follows;
* follow requests;
* mentions;
* shares;
* messages;
* story interactions where event contracts are available;
* security/account events where appropriate.

Do not invent unsupported source events.

Design notification type handling so future types can be added without breaking clients.

---

# 41. NOTIFICATION GENERATION

Notifications must be generated asynchronously from durable domain events where possible.

Do not make the primary business operation depend synchronously on push-notification provider success.

For example:

**like created → event → notification job → in-app notification → optional push delivery**

not:

**like API → wait for push provider → commit like**

---

# 42. NOTIFICATION AGGREGATION

Where multiple equivalent events occur in a short time, support aggregation.

Examples may include:

* multiple likes;
* repeated engagement on one content item.

Define:

* aggregation key;
* time window;
* maximum aggregate size;
* update behavior;
* read-state behavior.

Do not create an uncontrolled number of near-identical notifications.

---

# 43. NOTIFICATION READ STATE

Implement:

* mark notification read;
* mark multiple notifications read where appropriate;
* unread count;
* paginated notification retrieval.

Use cursor pagination.

Read operations should be idempotent.

---

# 44. NOTIFICATION PREFERENCES

Implement notification preference storage.

Support preference controls for appropriate notification classes.

At minimum evaluate:

* likes;
* comments;
* follows;
* follow requests;
* mentions;
* messages;
* security/account notifications.

Security-critical notifications must not be disabled merely because an ordinary notification preference is disabled.

---

# 45. PUSH NOTIFICATION BOUNDARY

Create a provider abstraction for push delivery.

Support:

* push-device registration;
* token lifecycle;
* platform;
* application/environment;
* active/inactive state;
* provider response handling.

Do not hardcode APNs/FCM credentials.

Do not claim push delivery succeeded unless the provider actually accepted the request.

---

# 46. PUSH DELIVERY JOBS

Implement asynchronous push-delivery jobs.

Jobs must support:

* notification ID;
* recipient;
* device token/reference;
* platform;
* attempt count;
* retryability;
* provider result;
* correlation ID.

Handle:

* transient provider errors;
* permanent invalid tokens;
* duplicate delivery attempts;
* expired tokens.

---

# 47. DEVICE PUSH TOKENS

Persist device push registrations securely.

Support:

* account;
* device;
* platform;
* token;
* application environment;
* timestamps;
* active state.

Do not expose tokens to other users.

Do not store provider secrets.

---

# 48. NOTIFICATION DEDUPLICATION

Prevent duplicate notifications caused by:

* duplicate event delivery;
* repeated jobs;
* retry;
* multiple consumers.

Use deterministic notification keys or idempotency where appropriate.

Notification creation must be safe under at-least-once event processing.

---

# 49. NOTIFICATION ORDERING

Notifications should have deterministic ordering based on server-side timestamps and stable identifiers.

Do not rely exclusively on client clocks.

When aggregated notifications are updated, preserve coherent ordering semantics.

---

# 50. NOTIFICATION CLEANUP

Define lifecycle behavior for old notifications.

Use configurable retention or expiration where appropriate.

Do not let notification tables grow without bounds.

Do not remove security-critical history prematurely when retention is required for the product's operational model.

---

# 51. EVENT CONSUMERS

Implement consumers for appropriate existing events, including concepts corresponding to:

* like created;
* comment created;
* follow created;
* follow request created;
* mention created;
* share created;
* message persisted;
* security/account events.

Consumer processing must be idempotent.

Do not assume exactly-once event delivery.

---

# 52. EVENT CONSUMER FAILURE

When a notification consumer fails:

* acknowledge/process according to the queue/event system semantics;
* retry transient failures;
* dead-letter permanent failures;
* preserve correlation IDs;
* avoid losing durable notification intent.

Do not cause a successful user action to fail merely because notification processing is unavailable.

---

# 53. SECURITY

Protect messaging and notification systems against:

* unauthorized conversation access;
* conversation enumeration;
* message spoofing;
* unauthorized message mutation;
* participant escalation;
* token leakage;
* notification privacy leakage;
* push-token exposure;
* connection hijacking;
* event injection.

Do not trust client-provided sender identity.

Do not trust client-provided conversation membership.

---

# 54. PRIVACY

Messaging is private data.

Do not place message bodies in:

* standard logs;
* metrics;
* notification payloads unless required;
* analytics;
* broad event payloads.

Use minimal event payloads.

Notification previews must respect product privacy settings.

Do not expose conversation existence to unauthorized callers.

---

# 55. RATE LIMITING

Protect:

* conversation creation;
* group creation;
* message send;
* read-state updates;
* typing;
* presence;
* realtime connection creation;
* synchronization;
* notification queries;
* push-token registration.

Use configurable limits.

Avoid making normal active chats unusable under ordinary traffic.

---

# 56. MESSAGE ABUSE CONTROLS

Implement basic abuse protections such as:

* send-rate limits;
* conversation-creation limits;
* participant-addition limits;
* connection limits;
* payload-size limits.

Do not implement the full trust-and-safety moderation system here.

Expose observable events for future abuse analysis.

---

# 57. DATABASE DESIGN

Implement real PostgreSQL persistence for:

* conversations;
* participants;
* messages;
* message attachment references;
* notification records;
* notification preferences;
* push-device registrations;
* relevant delivery/read state where durable;
* required idempotency state.

Use:

* foreign keys;
* uniqueness;
* indexes;
* timestamps;
* explicit state fields.

---

# 58. MESSAGE TABLE SCALING

Design message persistence for high volume.

Use appropriate:

* indexes;
* partitioning evaluation;
* cursor pagination;
* archival/retention strategy;
* write patterns.

Do not create indexes that make every message write unnecessarily expensive.

Do not introduce partitioning unless the actual design benefits from it.

---

# 59. DATABASE INDEXING

At minimum evaluate indexes for:

## Conversations

* participant lookup;
* last activity;
* account membership.

## Messages

* conversation + sequence;
* conversation + timestamp;
* sender + timestamp where operationally useful;
* idempotency key.

## Notifications

* recipient + timestamp;
* recipient + unread state;
* aggregation key where needed.

## Push Devices

* account + active state;
* token uniqueness as appropriate.

---

# 60. TRANSACTIONS

Use transactions for:

* conversation creation with initial participants;
* message persistence with durable event/outbox state;
* participant membership changes;
* notification creation where required;
* notification preference mutations;
* push-device registration changes.

Do not create distributed transactions across the push provider or realtime transport.

---

# 61. CONCURRENCY

Handle races involving:

* duplicate direct conversation creation;
* duplicate message send;
* concurrent participant removal;
* message read-state updates;
* notification generation;
* repeated push-token registration;
* simultaneous session/realtime revocation.

Use database constraints, idempotency, transactions, and monotonic cursors where appropriate.

---

# 62. API SURFACE

Implement APIs equivalent to:

## Conversations

* create direct conversation;
* create group conversation;
* list conversations;
* get conversation;
* list participants;
* add/remove participants where authorized;
* leave conversation.

## Messages

* send message;
* list messages;
* get message where needed;
* mark read;
* synchronize missed messages;
* edit/delete where supported.

## Notifications

* list notifications;
* unread count;
* mark read;
* mark multiple read;
* get/update notification preferences.

## Push Devices

* register device token;
* update token;
* deactivate token.

Use repository-established route and version conventions.

---

# 63. REALTIME API

Implement the realtime protocol necessary for:

* connection;
* authentication;
* subscription;
* message events;
* delivery acknowledgement;
* read acknowledgement;
* typing;
* presence where supported;
* synchronization.

Do not expose internal event-stream topics directly to clients.

---

# 64. ERROR CONTRACT

Use the project's canonical error structure.

Return safe errors for:

* unauthorized conversation access;
* conversation not found;
* participant not found;
* invalid message;
* message too large;
* attachment unavailable;
* duplicate mutation;
* invalid synchronization cursor;
* rate limit;
* unavailable dependency.

Do not expose provider-specific errors unnecessarily.

---

# 65. OBSERVABILITY

Instrument:

## Messaging

* message-send latency;
* persistence latency;
* realtime-delivery latency;
* delivery failures;
* synchronization latency;
* active connections;
* connection failures;
* duplicate/idempotent requests.

## Notifications

* notification creation;
* aggregation;
* delivery-job throughput;
* push success/failure;
* invalid-token rate;
* unread count latency.

Never log raw message bodies or push credentials.

---

# 66. RELIABILITY

Messaging must remain usable during partial failures.

Examples:

* if Redis is unavailable, durable messages remain persisted;
* if WebSocket delivery fails, messages remain synchronizable;
* if push delivery fails, in-app notifications remain available;
* if the push provider is unavailable, notification jobs retry asynchronously;
* if a notification consumer is down, source-domain actions still succeed.

---

# 67. TESTING STRATEGY

Create real tests.

## Unit Tests

Cover:

* conversation authorization;
* participant rules;
* block restrictions;
* message validation;
* message idempotency;
* read cursor behavior;
* notification aggregation;
* notification preferences;
* push-token handling;
* realtime authorization.

## Integration Tests

Cover:

* conversation persistence;
* message persistence;
* idempotent send;
* message pagination;
* read state;
* participant changes;
* notification creation;
* notification aggregation;
* push-device registration;
* event consumers;
* Redis realtime state.

## API Tests

Cover:

* authorization;
* message send;
* pagination;
* synchronization;
* notifications;
* preferences;
* push-device registration.

## Realtime Tests

Cover:

* authenticated connection;
* subscription authorization;
* message delivery;
* acknowledgement;
* reconnect;
* missed-event synchronization;
* duplicate suppression;
* typing expiration.

---

# 68. SECURITY TESTING

Test:

* unauthorized conversation access;
* unauthorized participant mutation;
* forged sender identity;
* message spoofing;
* blocked-user messaging restrictions;
* invalid realtime authentication;
* unauthorized realtime subscription;
* notification privacy;
* push-token isolation;
* rate-limit enforcement.

---

# 69. CONCURRENCY TESTING

Where practical, validate:

* simultaneous direct-conversation creation;
* duplicate message submission;
* concurrent read-state updates;
* participant removal during messaging;
* duplicate notification event delivery;
* duplicate push jobs.

Verify durable state remains consistent.

---

# 70. PERFORMANCE VALIDATION

Perform targeted validation for:

* message insertion;
* conversation pagination;
* message pagination;
* batch unread-state calculation;
* realtime connection management;
* notification retrieval;
* notification aggregation.

Do not claim production-scale performance from local tests.

Record actual conditions.

---

# 71. DOCUMENTATION

Create/update documentation for:

* conversation APIs;
* message APIs;
* message lifecycle;
* idempotency;
* realtime protocol;
* synchronization;
* typing/presence;
* notification APIs;
* notification preferences;
* push-provider abstraction;
* background jobs;
* rate limits;
* privacy/security;
* testing.

Document the actual protocol and implementation.

---

# 72. PORTABLE CONTRACTS

Maintain explicit portable contracts for:

* conversation;
* participant;
* message;
* attachment;
* delivery state;
* read state;
* realtime envelope;
* synchronization cursor;
* notification;
* notification preference;
* push-device registration;
* delivery job;
* event consumers.

These contracts must be understandable by later web, mobile, infrastructure, QA, moderation, and analytics implementations without relying on this conversation.

---

# 73. CROSS-PART COMPATIBILITY

Preserve compatibility with:

* account/profile;
* social graph;
* content/media;
* engagement;
* feed;
* notification clients;
* moderation;
* analytics;
* web;
* mobile;
* infrastructure.

Do not implement client UI.

Do not redesign the content/media contracts.

Do not duplicate user identity state.

---

# 74. NO FAKE COMPLETENESS

Do not use:

* fake realtime delivery;
* fake message persistence;
* hardcoded conversations;
* in-memory message storage in production paths;
* fabricated push delivery;
* placeholder notification logic;
* fake WebSocket authorization;
* TODO/FIXME gaps;
* pseudo-code.

All current-scope functionality must be real.

---

# 75. VALIDATION

Before completion:

1. run formatting;
2. run linting;
3. run type checking;
4. validate migrations;
5. run unit tests;
6. run integration tests;
7. run API/contract tests;
8. run realtime tests;
9. run security tests;
10. run concurrency tests where available;
11. validate notification/event contracts;
12. validate documentation.

If external push providers or cloud infrastructure are unavailable, distinguish local validation from unavailable external validation.

Do not claim push delivery succeeded if it was not actually exercised.

---

# 76. IMPLEMENTATION REPORT

After implementation, provide a completion report containing:

## Files Created

List every file created.

## Files Modified

List every file modified.

## Files Deleted

List every file deleted, if any.

## Backend Domains Implemented

Summarize:

* conversations;
* participants;
* messages;
* realtime;
* synchronization;
* notifications;
* push-device registration.

## Database Changes

List:

* tables;
* indexes;
* constraints;
* migrations.

## Redis Changes

List:

* realtime keys;
* typing/presence state;
* connection routing;
* TTLs.

## Event Changes

List:

* consumed events;
* produced events;
* event schemas;
* outbox behavior.

## Queue/Job Changes

List:

* message-related jobs;
* notification jobs;
* push-delivery jobs;
* cleanup jobs.

## API Changes

List endpoints and major contracts.

## Realtime Changes

List:

* connection protocol;
* event types;
* synchronization;
* acknowledgement semantics.

## Security/Privacy Changes

Summarize authorization, privacy, token handling, and abuse controls.

## Tests Created

List test categories and important scenarios.

## Tests Executed

State exactly which tests were executed.

## Validation Performed

State exact validation performed.

## Documentation Changes

List documentation created or updated.

## Integration Considerations

Explain how web/mobile clients and future moderation, analytics, and infrastructure systems consume the messaging and notification contracts.

## Compatibility Considerations

Identify compatibility-sensitive changes.

## Known Limitations

List genuine limitations.

## Unresolved Issues

List only issues that remain unresolved.

---

# 77. DEFINITION OF DONE

This backend milestone is complete only when:

* direct conversations work;
* group conversations work;
* participant membership is persistent;
* conversation authorization works;
* block/restriction policy is enforced;
* messages persist durably;
* message ordering is deterministic;
* message idempotency works;
* message pagination works;
* message attachments use canonical media references;
* delivery state works;
* read state works;
* realtime authentication works;
* realtime authorization works;
* realtime events are versioned;
* horizontal realtime delivery has an appropriate shared coordination model;
* typing indicators work as ephemeral state;
* presence, if implemented, is TTL-based and bounded;
* reconnect synchronization works;
* missed durable messages/events can be recovered;
* notification records are persisted;
* notification generation is asynchronous where appropriate;
* notification aggregation works;
* notification read state works;
* notification preferences work;
* push-device registration works;
* push delivery is abstracted behind a provider boundary;
* push jobs are retryable and idempotent;
* Redis usage is bounded;
* database migrations exist;
* observability exists;
* privacy/security controls exist;
* unit tests exist;
* integration tests exist;
* API/contract tests exist;
* realtime tests exist;
* security tests exist;
* concurrency tests exist where practical;
* documentation reflects actual behavior;
* no real credentials are committed;
* no fake functionality exists;
* no intentional implementation gaps remain within this scope.

---

# 78. FINAL IMPLEMENTATION DISCIPLINE

Implement **only the current prompt's scope**.

Do not implement:

* web messaging UI;
* mobile messaging UI;
* message search;
* end-to-end encryption;
* moderation workflows;
* administration;
* creator analytics;
* recommendation systems;
* feed systems;
* infrastructure provisioning.

Do not redesign:

* identity;
* account/profile;
* social graph;
* content/media;
* engagement

unless a concrete compatibility issue inside the current messaging/notification scope requires a narrowly scoped adjustment.

Do not assume another AI prompt has been executed.

Do not depend on another AI conversation.

Do not expose private message content in telemetry.

Do not claim external push delivery or production realtime infrastructure exists unless it was actually provisioned and validated.

Produce real, tested, documented backend functionality for Instagram's messaging, realtime communication, and notification systems.
