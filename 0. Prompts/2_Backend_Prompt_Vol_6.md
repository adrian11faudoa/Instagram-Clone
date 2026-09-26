# Instagram — Backend Prompt — Volume 6

# 1. ROLE

You are the **Staff Backend Engineering team** responsible for implementing the trust-and-safety, moderation, administration, audit, and analytics backend domains for the **Instagram** project.

Operate with the combined responsibilities of:

* Staff Backend Engineer
* Security Engineer
* Trust & Safety Engineer
* Moderation Systems Engineer
* Administration Platform Engineer
* Database Engineer
* Distributed Systems Engineer
* Privacy Engineer
* Analytics Engineer
* Reliability Engineer
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
* messaging;
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
* high-volume user-generated content;
* large moderation workloads;
* significant administrative activity;
* high-volume audit and analytics events.

These are global architectural targets.

This prompt implements the **moderation, trust-and-safety, administration, audit, and analytics backend foundation**.

---

# 3. CURRENT BACKEND ASSIGNMENT

Implement:

1. user/content reporting;
2. moderation cases;
3. moderation state management;
4. moderation decisions;
5. enforcement actions;
6. account restrictions/suspensions where applicable;
7. content restrictions/removal;
8. administrative roles;
9. administrative permissions;
10. secure administrative APIs;
11. administrative audit logging;
12. moderation audit trails;
13. moderation queues;
14. moderation job processing;
15. abuse/risk signal ingestion boundaries;
16. product analytics event ingestion;
17. analytics event validation;
18. analytics event delivery;
19. analytics privacy controls;
20. analytics retention/lifecycle boundaries;
21. moderation events;
22. administrative events;
23. audit events;
24. Redis usage where justified;
25. asynchronous jobs;
26. observability;
27. security;
28. privacy;
29. database migrations;
30. tests;
31. documentation.

This milestone must provide the backend trust, safety, administrative, and analytics foundations required by the completed platform.

---

# 4. REPOSITORY INSPECTION

Before modifying or creating code, inspect the repository.

Inspect, where present:

* account and identity modules;
* authentication/session management;
* content/posts;
* stories;
* short-form video;
* media;
* engagement;
* feed;
* discovery/search;
* messaging;
* notifications;
* event infrastructure;
* job/queue infrastructure;
* Redis;
* database schemas;
* migrations;
* existing admin code;
* existing moderation code;
* authorization;
* audit/logging;
* analytics infrastructure;
* observability;
* test infrastructure;
* documentation.

Treat the repository as the source of truth for actual implementation state.

Do not assume an earlier AI prompt was executed.

Do not assume another Claude conversation exists.

Do not fabricate administrative, moderation, or analytics infrastructure.

Reuse compatible foundations already present.

---

# 5. TECHNOLOGY BASELINE

Use the repository's existing backend stack with the project baseline of:

* TypeScript;
* Node.js;
* PostgreSQL;
* Redis;
* durable event streaming;
* background jobs;
* REST APIs;
* strict validation;
* structured logging;
* tracing/metrics;
* automated tests.

Use the existing authorization architecture for privileged administrative access.

Do not create a parallel identity system for administrators unless the actual architecture requires a separate control plane.

---

# 6. BOUNDED IMPLEMENTATION SCOPE

## In Scope

Implement:

* report creation;
* report retrieval for authorized actors;
* moderation case creation;
* moderation queue state;
* moderation case assignment where appropriate;
* moderation decision recording;
* content enforcement;
* account enforcement;
* administrative roles;
* administrative permissions;
* administrative APIs;
* moderation APIs;
* secure audit logging;
* administrative audit logs;
* moderation audit logs;
* abuse-signal ingestion boundaries;
* moderation jobs;
* analytics event ingestion;
* analytics event validation;
* analytics event batching/delivery;
* analytics privacy handling;
* analytics retention configuration;
* analytics event contracts;
* relevant Redis structures;
* event/outbox integration;
* migrations;
* observability;
* security controls;
* privacy controls;
* tests;
* documentation.

## Out of Scope

Do not implement:

* machine-learning moderation models;
* facial recognition;
* biometric identification;
* automatic content-classification models;
* full advertising analytics;
* business intelligence dashboards;
* administrative web UI;
* administrative mobile UI;
* complete data warehouse infrastructure;
* complete SIEM platform;
* legal/compliance certification;
* cloud provisioning;
* infrastructure deployment.

Create integration boundaries for future systems where needed.

---

# 7. TRUST & SAFETY DOMAIN

The backend must distinguish:

* report;
* moderation case;
* moderation decision;
* enforcement action;
* account state;
* content state;
* audit event.

Do not collapse these concepts into one generic status field.

A report represents a submitted signal.

A moderation case represents the operational review unit.

A decision represents the outcome of a review.

An enforcement action represents the resulting restriction or state change.

---

# 8. REPORT MODEL

Implement reports for appropriate targets.

A report should support:

* report ID;
* reporter account;
* target resource;
* target type;
* reason code;
* optional structured context;
* created time;
* state;
* associated moderation case where applicable.

Do not store arbitrary unbounded report payloads.

Validate target existence where appropriate without leaking private resource information to unauthorized reporters.

---

# 9. REPORT TARGETS

Support report targets such as:

* account;
* post;
* story;
* short-form video;
* comment;
* conversation/message where the current privacy model permits reporting.

Use an explicit target-type model.

Do not use separate incompatible report tables unless the data model requires it.

---

# 10. REPORT AUTHORIZATION

Only authenticated users with the appropriate product permissions may submit reports.

Prevent:

* reporting nonexistent resources;
* unauthorized access through the reporting endpoint;
* arbitrary administrative state mutation;
* duplicate report abuse where appropriate.

Do not reveal private-resource information through error responses.

---

# 11. REPORT DEDUPLICATION

Prevent abusive duplicate reporting where appropriate.

Define whether repeated reports are:

* merged;
* accepted as separate signals;
* rate limited;
* linked to the same moderation case.

Do not accidentally turn a single event into unlimited moderation workload.

---

# 12. MODERATION CASE MODEL

Implement a moderation-case model supporting:

* case ID;
* priority;
* target;
* source reports/signals;
* state;
* assigned reviewer;
* created time;
* updated time;
* decision;
* resolution time.

Define explicit case states such as:

* open;
* queued;
* assigned;
* under_review;
* resolved;
* dismissed;
* escalated.

Do not rely on free-form strings without a controlled state model.

---

# 13. MODERATION CASE ASSIGNMENT

Implement authorized case assignment.

Support:

* assignment to moderator;
* reassignment where permitted;
* assignment timestamps;
* current assignee;
* workload visibility.

Prevent unauthorized users from manipulating case ownership.

All assignment mutations must be audited.

---

# 14. MODERATION DECISIONS

Implement explicit moderation decisions.

A decision should include:

* case ID;
* decision code;
* reviewer;
* reason;
* enforcement action where applicable;
* created timestamp;
* reversal state where supported.

Decision history must remain auditable.

Do not overwrite historical moderation decisions without preserving the audit trail.

---

# 15. ENFORCEMENT ACTIONS

Implement enforcement actions appropriate to the platform.

Consider:

* content restriction;
* content removal;
* content visibility reduction state where applicable;
* account restriction;
* account suspension;
* account restoration;
* feature restriction;
* messaging restriction where appropriate.

Each action must have:

* target;
* action type;
* actor;
* reason;
* created time;
* expiration where applicable;
* reversal behavior.

Do not implement arbitrary unbounded administrative powers.

---

# 16. ACCOUNT ENFORCEMENT

Implement secure account-state enforcement.

Account states must remain compatible with the existing account domain.

Do not duplicate account records.

Support controlled state transitions such as:

* active → restricted;
* active → suspended;
* suspended → restored;
* restricted → active.

Every privileged transition must be authorized and audited.

---

# 17. CONTENT ENFORCEMENT

Implement enforcement against content.

Support state transitions appropriate to:

* posts;
* stories;
* short-form video;
* comments.

Enforcement must propagate through existing content visibility checks.

Do not duplicate content ownership.

Do not delete content physically merely because a moderation decision requires it unless the content lifecycle contract explicitly requires physical deletion.

---

# 18. MODERATION VISIBILITY

A moderation action must be distinguishable from ordinary user deletion.

This distinction is important for:

* audit;
* appeals;
* operational reporting;
* restoration;
* analytics.

Do not represent every moderation action as though the user voluntarily deleted the resource.

---

# 19. APPEAL-READY DESIGN

Create data structures capable of supporting future appeals.

At minimum preserve:

* original decision;
* enforcing actor;
* reason;
* timestamp;
* target;
* enforcement state.

Do not implement a complete appeals workflow if it is outside the current scope.

---

# 20. MODERATION QUEUES

Implement backend queue state for moderation work.

Queues should support:

* priority;
* target;
* case;
* state;
* assignment;
* created time;
* aging.

Do not expose queue internals directly to ordinary users.

Administrative access must be authorized.

---

# 21. MODERATION JOBS

Create asynchronous jobs where required for:

* case enrichment;
* enforcement propagation;
* moderation-state synchronization;
* cleanup;
* reconciliation.

Jobs must be:

* idempotent;
* retryable;
* observable;
* bounded.

Do not implement automatic AI moderation models.

---

# 22. ABUSE SIGNALS

Create a backend boundary for abuse/risk signals.

Potential signals include:

* excessive reports;
* repeated failed authentication;
* abnormal engagement;
* excessive account creation;
* excessive messaging;
* suspicious API usage;
* high-rate relationship changes.

Signals must be normalized and observable.

Do not implement a full fraud/risk engine.

---

# 23. ABUSE SIGNAL MODEL

Where useful, represent:

* signal ID;
* account/resource;
* signal type;
* severity;
* source;
* timestamp;
* metadata;
* processing state.

Do not store unnecessary sensitive telemetry.

---

# 24. ADMINISTRATIVE CONTROL PLANE

Create a clearly separated administrative authorization boundary.

Administrative APIs must not rely on ordinary user privileges.

At minimum distinguish:

* ordinary user;
* moderator;
* administrator;
* security/operations role where actually required.

Use least privilege.

Do not create a single unrestricted `isAdmin` boolean as the sole security mechanism for sensitive operations.

---

# 25. ADMINISTRATIVE ROLES

Implement explicit roles or permissions appropriate to the scope.

Examples may include:

* moderator;
* senior moderator;
* support operator;
* administrator;
* security operator.

Do not create more roles than the actual authorization model requires.

Every role must have explicit permissions.

---

# 26. ADMINISTRATIVE PERMISSIONS

Define permissions for actions such as:

* view moderation case;
* assign case;
* resolve case;
* restrict account;
* suspend account;
* restore account;
* restrict content;
* remove content;
* inspect audit information;
* manage configuration where authorized.

Privileged operations must use permission checks rather than hardcoded role-name conditions scattered across controllers.

---

# 27. ADMIN AUTHENTICATION

Administrative APIs must require strong authentication.

Use the existing project authentication foundation plus additional administrative controls where available.

Where the architecture supports MFA, require it for privileged roles where appropriate.

Do not create a separate plaintext-password admin system.

---

# 28. ADMIN AUDIT LOG

Implement an append-oriented audit record for privileged actions.

Each audit record should include:

* audit ID;
* actor;
* action;
* target;
* reason;
* timestamp;
* request/correlation ID;
* relevant state transition;
* safe metadata.

Do not store secrets.

Do not permit ordinary users to modify or delete audit records.

---

# 29. AUDIT IMMUTABILITY

Administrative and moderation audit history must be tamper-resistant within the application's authorization model.

Avoid exposing generic delete/update APIs for audit records.

If cleanup/retention is required, implement controlled retention mechanisms rather than ordinary user mutation.

---

# 30. MODERATION AUDIT

Audit:

* report creation;
* assignment;
* reassignment;
* decision;
* enforcement;
* restoration;
* escalation.

The audit trail must make it possible to reconstruct who did what and when.

---

# 31. SECURITY EVENTS

Integrate this milestone with the existing security-event architecture.

Relevant events may include:

* administrative login;
* privilege changes;
* moderation action;
* account suspension;
* account restoration;
* configuration-sensitive action.

Do not leak sensitive administrative details into ordinary product events.

---

# 32. ANALYTICS DOMAIN

Implement a product-analytics event ingestion boundary.

This is distinct from:

* operational telemetry;
* security audit;
* moderation signals.

Analytics events must be explicitly typed and versioned.

---

# 33. ANALYTICS EVENT MODEL

Support fields such as:

* event ID;
* event name;
* schema version;
* actor/account reference where permitted;
* anonymous/session reference where appropriate;
* resource reference;
* timestamp;
* client platform;
* application version;
* source;
* properties.

Do not store arbitrary unknown payloads without validation.

---

# 34. ANALYTICS VALIDATION

Validate:

* event name;
* schema version;
* required fields;
* supported property types;
* property-size limits;
* allowed event sources.

Reject malformed or oversized analytics events.

Do not allow analytics ingestion to become an unrestricted data-exfiltration channel.

---

# 35. ANALYTICS PRIVACY

Do not place in analytics events:

* passwords;
* access tokens;
* refresh credentials;
* message bodies;
* raw private-content bodies;
* unnecessary personal data.

Where account identifiers are used, use the project's approved identifier policy.

Avoid collecting information that is not required for the event.

---

# 36. ANALYTICS INGESTION

Implement an asynchronous ingestion path where practical.

The product-facing API should not depend synchronously on downstream analytics processing.

Use:

* event batching;
* queueing;
* retry;
* dead-letter behavior.

The ingestion path must be observable.

---

# 37. ANALYTICS EVENT DELIVERY

Create an event or queue contract for downstream analytics systems.

The contract must define:

* event name;
* schema version;
* event ID;
* timestamp;
* source;
* payload;
* privacy classification where useful.

Do not implement the complete analytics warehouse.

---

# 38. ANALYTICS DEDUPLICATION

Analytics ingestion must tolerate retries.

Use event IDs or equivalent deduplication keys.

Do not require exactly-once delivery when at-least-once delivery plus deduplication is the realistic architecture.

---

# 39. ANALYTICS RETENTION

Define configurable retention boundaries.

Analytics events must not grow indefinitely in the primary transactional database.

Use asynchronous delivery to a future analytics system.

If the current repository provides an analytics storage destination, integrate with it through an explicit boundary.

Do not invent a data warehouse that is not actually available.

---

# 40. ANALYTICS RATE LIMITING

Protect analytics ingestion against:

* event floods;
* malformed high-rate clients;
* abusive clients;
* oversized payloads.

Use configurable limits by:

* account;
* device/session;
* API key/application identity where applicable;
* network source.

Do not allow analytics collection to become an uncontrolled resource-consumption path.

---

# 41. MODERATION AND ANALYTICS SEPARATION

Do not mix:

* moderation decisions;
* audit logs;
* product analytics.

A moderation action may generate analytics or operational events, but the systems must retain different purposes and access controls.

---

# 42. REDIS USAGE

Use Redis only where justified for this scope.

Potential uses include:

* moderation queue acceleration;
* rate limiting;
* short-lived abuse-signal aggregation;
* analytics ingestion buffering;
* administrative session state where appropriate.

Define:

* namespace;
* TTL;
* source of truth;
* invalidation;
* failure behavior.

Do not store authoritative moderation decisions only in Redis.

---

# 43. EVENT CONTRACTS

Publish durable events for important trust/safety state changes such as:

* report created;
* moderation case opened;
* moderation decision recorded;
* content restricted;
* content restored;
* account restricted;
* account suspended;
* account restored;
* administrative action recorded;
* analytics event accepted where appropriate.

Use the established event envelope and versioning.

Do not publish sensitive moderation evidence indiscriminately.

---

# 44. EVENT SECURITY

Event payloads must contain only what downstream consumers require.

Avoid sending:

* private moderation notes;
* raw message bodies;
* sensitive personal data;
* security secrets.

Where different consumers require different sensitivity levels, use separate event types or controlled views rather than indiscriminately expanding one payload.

---

# 45. TRANSACTIONS

Use transactions for state transitions requiring atomicity.

Examples:

* moderation decision + enforcement state;
* administrative role mutation + audit record;
* account suspension + audit event;
* content enforcement + audit event;
* report creation + case creation where required.

Do not include slow external systems in database transactions.

---

# 46. CONCURRENCY

Handle:

* two moderators resolving the same case;
* an administrator suspending an account while another restores it;
* duplicate moderation jobs;
* repeated report submissions;
* duplicate analytics events;
* concurrent permission changes.

Use:

* optimistic concurrency;
* state/version checks;
* unique constraints;
* idempotency;
* transactions.

Do not allow stale administrative actions to silently overwrite newer decisions.

---

# 47. OPTIMISTIC CONCURRENCY

Administrative and moderation mutations should verify that the current resource state still matches the state expected by the operator when the action was initiated, where such protection is necessary.

If a case was already resolved:

* reject the stale mutation;
* return a conflict;
* require the current state to be re-evaluated.

Do not silently overwrite a newer moderation decision.

---

# 48. API SURFACE

Implement APIs equivalent to:

## Reports

* create report;
* retrieve authorized reporter-visible report state where appropriate.

## Moderation

* create/list cases for authorized moderators;
* assign case;
* resolve case;
* record decision;
* enforce action;
* restore/reverse action where permitted.

## Administration

* inspect account moderation state;
* inspect content moderation state;
* apply authorized administrative actions;
* manage role/permission information where this scope requires it.

## Analytics

* ingest analytics events;
* batch analytics events.

Administrative and moderation endpoints must have explicit authorization requirements.

---

# 49. API RESPONSE SECURITY

Administrative APIs must return only fields appropriate to the operator's permission set.

Do not expose:

* passwords;
* access tokens;
* raw private messages unless a separately authorized policy permits it;
* provider credentials;
* internal infrastructure secrets.

Moderation evidence access must be tightly controlled.

---

# 50. MODERATION DATA PRIVACY

Treat moderation data as sensitive.

Protect:

* reporter identity where policy requires;
* moderator notes;
* evidence;
* internal risk signals;
* administrative metadata.

Do not put sensitive moderation information into ordinary application logs.

---

# 51. RATE LIMITING

Protect:

* report creation;
* moderation APIs;
* administrative APIs;
* analytics ingestion;
* abuse-signal ingestion.

Administrative rate limits must be operationally practical and distinguish legitimate bulk work from abusive traffic.

---

# 52. ABUSE PREVENTION

Implement basic protections for:

* report spam;
* analytics flooding;
* administrative endpoint abuse;
* repeated suspicious actions.

Do not implement a full ML fraud engine.

Expose durable events and metrics for later trust-and-safety systems.

---

# 53. OBSERVABILITY

Instrument:

## Moderation

* report rate;
* case creation;
* queue depth;
* processing latency;
* resolution latency;
* enforcement failures.

## Administration

* privileged action count;
* authorization denials;
* stale-state conflicts;
* audit-write failures.

## Analytics

* event ingestion rate;
* validation failures;
* queue lag;
* delivery failures;
* duplicate events;
* payload rejection.

Do not log sensitive moderation evidence or private content.

---

# 54. RELIABILITY

Trust/safety controls must remain reliable under partial failure.

Examples:

* moderation state must remain durable if Redis fails;
* audit records must not disappear because downstream analytics is unavailable;
* analytics failures must not break core user interactions;
* moderation jobs must retry safely;
* administrative actions must not depend on external analytics completion.

Do not make analytics availability a dependency for critical enforcement.

---

# 55. FAILURE BEHAVIOR

Define behavior for:

* PostgreSQL unavailable;
* Redis unavailable;
* event streaming unavailable;
* moderation queue unavailable;
* analytics destination unavailable;
* duplicate job execution;
* conflicting administrative action;
* stale moderation case.

Critical enforcement state must remain durable.

Asynchronous downstream delivery must retry rather than silently disappear.

---

# 56. DATABASE DESIGN

Implement persistence for:

* reports;
* moderation cases;
* moderation decisions;
* enforcement actions;
* administrative roles/permissions where required;
* administrative audit logs;
* moderation audit logs;
* analytics ingestion state where required;
* relevant abuse signals.

Use:

* foreign keys;
* indexes;
* state constraints;
* timestamps;
* retention/lifecycle fields.

Keep sensitive data separated appropriately.

---

# 57. DATABASE INDEXING

Evaluate indexes for:

## Reports

* target;
* reporter;
* state;
* created time.

## Moderation Cases

* state;
* priority;
* assignee;
* created time;
* target.

## Audit Logs

* actor;
* action;
* target;
* timestamp.

## Analytics

Avoid using the transactional database as the long-term high-volume analytics store.

If ingestion metadata is stored transactionally, index it only for the operational queries actually required.

---

# 58. DATA RETENTION

Define explicit retention policies for:

* reports;
* moderation cases;
* audit logs;
* analytics ingestion metadata;
* abuse signals.

Do not delete audit information casually.

Do not retain sensitive data forever without a defined operational reason.

Retention values must be configurable where appropriate.

---

# 59. MIGRATIONS

Create real schema migrations.

Migrations must:

* be deterministic;
* preserve existing data;
* support the repository's migration system;
* use safe rollout patterns;
* avoid destructive operations without a deliberate migration strategy.

Do not use automatic schema synchronization in production.

---

# 60. TESTING STRATEGY

Create real tests.

## Unit Tests

Cover:

* report validation;
* moderation state transitions;
* enforcement rules;
* role/permission checks;
* analytics event validation;
* retention logic;
* audit generation;
* optimistic concurrency.

## Integration Tests

Cover:

* report persistence;
* case creation;
* moderation decision;
* enforcement;
* restoration;
* role/permission checks;
* audit persistence;
* analytics ingestion;
* duplicate-event handling;
* background jobs.

## API Tests

Cover:

* user report creation;
* moderator authorization;
* administrator authorization;
* case transitions;
* enforcement;
* analytics ingestion;
* validation;
* error responses.

---

# 61. SECURITY TESTING

Test:

* ordinary user cannot access moderation APIs;
* moderator cannot perform administrator-only actions;
* unauthorized role escalation fails;
* audit logs cannot be modified through public APIs;
* sensitive fields are excluded from responses;
* moderation data cannot be accessed by unauthorized operators;
* report spam controls;
* analytics ingestion abuse controls;
* stale administrative mutation conflicts;
* duplicate moderation actions are prevented.

---

# 62. CONCURRENCY TESTING

Where practical, validate:

* two moderators resolving one case;
* simultaneous suspension/restoration;
* repeated enforcement jobs;
* duplicate report submissions;
* duplicate analytics event delivery;
* concurrent role mutation.

Verify that only valid state transitions succeed.

---

# 63. PERFORMANCE VALIDATION

Perform targeted tests for:

* moderation queue queries;
* report listing;
* case retrieval;
* audit append performance;
* analytics ingestion validation;
* batch analytics ingestion.

Do not claim production-scale analytics throughput from local tests.

---

# 64. DOCUMENTATION

Create or update documentation for:

* reporting;
* moderation lifecycle;
* enforcement;
* administrative roles;
* permissions;
* audit logging;
* abuse signals;
* analytics events;
* analytics privacy;
* retention;
* event consumers;
* jobs;
* security requirements;
* testing.

Documentation must describe actual implementation behavior.

---

# 65. PORTABLE CONTRACTS

Maintain explicit contracts for:

* report;
* moderation case;
* moderation decision;
* enforcement action;
* administrative role;
* permission;
* audit event;
* abuse signal;
* analytics event;
* moderation events;
* analytics ingestion jobs.

These contracts must be usable by later infrastructure, QA, web/admin, mobile, and analytics integration work.

---

# 66. CROSS-PART COMPATIBILITY

Preserve compatibility with:

* account lifecycle;
* content lifecycle;
* engagement;
* messaging;
* notifications;
* feed;
* discovery;
* infrastructure;
* analytics;
* QA.

Moderation must consume existing domain ownership rather than duplicating content/account persistence.

---

# 67. NO FAKE COMPLETENESS

Do not implement:

* fake moderation models;
* fake administrator authorization;
* fake audit storage;
* mock analytics persistence in production paths;
* hardcoded privileged accounts;
* bypass permissions;
* placeholder enforcement;
* TODO/FIXME gaps;
* pseudo-code.

All current-scope functionality must be real.

---

# 68. VALIDATION

Before completion:

1. run formatting;
2. run linting;
3. run type checking;
4. validate migrations;
5. run unit tests;
6. run integration tests;
7. run API/contract tests;
8. run security tests;
9. run concurrency tests where available;
10. validate event contracts;
11. validate documentation.

If external analytics or moderation systems are unavailable, distinguish local validation from unavailable external validation.

Do not claim external delivery or classification occurred if it did not.

---

# 69. IMPLEMENTATION REPORT

After implementation, provide a completion report containing:

## Files Created

List every file created.

## Files Modified

List every file modified.

## Files Deleted

List every file deleted, if any.

## Backend Domains Implemented

Summarize:

* reports;
* moderation;
* enforcement;
* administration;
* audit;
* abuse signals;
* analytics ingestion.

## Database Changes

List:

* tables;
* indexes;
* constraints;
* migrations;
* retention-related fields.

## API Changes

List implemented endpoints and major authorization boundaries.

## Redis Changes

List:

* namespaces;
* TTLs;
* rate-limit/abuse uses;
* operational caches.

## Event Changes

List:

* moderation events;
* administrative events;
* analytics-related events;
* consumed events.

## Queue/Job Changes

List:

* moderation jobs;
* analytics jobs;
* cleanup/reconciliation jobs.

## Security Changes

Summarize:

* administrative authorization;
* audit protection;
* privacy;
* rate limits;
* abuse controls.

## Tests Created

List test categories and important scenarios.

## Tests Executed

State exactly which tests were executed.

## Validation Performed

State exact validation performed.

## Documentation Changes

List documentation created or updated.

## Integration Considerations

Explain how feed, messaging, content, notifications, infrastructure, analytics, and client/admin systems consume the implemented contracts.

## Compatibility Considerations

Identify compatibility-sensitive changes.

## Known Limitations

List genuine limitations.

## Unresolved Issues

List only issues that remain unresolved.

---

# 70. DEFINITION OF DONE

This backend milestone is complete only when:

* report creation works;
* duplicate/report-abuse behavior is controlled;
* moderation cases are persistent;
* case state transitions are implemented;
* assignments are authorized;
* moderation decisions are durable;
* enforcement actions work;
* account enforcement integrates with account lifecycle;
* content enforcement integrates with content visibility;
* administrative roles are explicit;
* administrative permissions are explicit;
* privileged APIs are protected;
* administrative actions are audited;
* moderation actions are audited;
* abuse signals have a defined ingestion boundary;
* analytics events are validated;
* analytics ingestion works;
* analytics deduplication works;
* analytics privacy controls work;
* analytics retention is defined;
* moderation/administrative events are durable;
* asynchronous jobs are retryable;
* Redis usage is bounded;
* database migrations exist;
* observability exists;
* security controls exist;
* privacy controls exist;
* unit tests exist;
* integration tests exist;
* API/contract tests exist;
* security tests exist;
* concurrency tests exist where practical;
* documentation reflects actual behavior;
* no privileged credentials are committed;
* no fake functionality exists;
* no intentional implementation gaps remain inside the defined scope.

---

# 71. FINAL IMPLEMENTATION DISCIPLINE

Implement **only the current prompt's scope**.

Do not implement:

* ML moderation models;
* recommendation systems;
* advertising;
* complete analytics warehouse infrastructure;
* admin web UI;
* admin mobile UI;
* full SIEM infrastructure;
* legal/compliance certification;
* cloud provisioning;
* future trust-and-safety systems not defined here.

Do not redesign:

* identity;
* content;
* engagement;
* messaging;
* notifications

unless a concrete compatibility issue within moderation, administration, audit, or analytics requires a narrowly scoped adjustment.

Do not assume another AI prompt has been executed.

Do not depend on another AI conversation.

Do not expose moderation evidence or private user content through ordinary telemetry.

Do not create privileged backdoors or hardcoded administrator accounts.

Produce real, tested, documented backend functionality for Instagram's moderation, administration, audit, abuse-signal, and analytics foundations.
