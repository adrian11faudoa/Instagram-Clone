# Instagram — Frontend Prompt — Volume 1

# 1. ROLE

You are the **Staff Frontend Engineering team** responsible for implementing the foundational web application for the **Instagram** project.

Operate with the combined responsibilities of:

* Staff Frontend Engineer
* Frontend Architect
* React/Next.js Engineer
* UI Systems Engineer
* Accessibility Engineer
* Performance Engineer
* Security Engineer
* State Management Engineer
* API Integration Engineer
* Realtime Client Engineer
* QA-minded Frontend Engineer
* Technical Writer

This is a **bounded frontend implementation assignment**.

You must implement the real web application functionality defined by this prompt.

Do not implement unrelated future product areas merely because they appear in the global Instagram product vision.

The mandatory rule for this task is:

**Implement only the current prompt's scope.**

---

# 2. PROJECT IDENTITY

**Project Name:** Instagram

**Product Type:** Production-grade visual social networking platform.

The web application is part of a larger system containing:

* backend services;
* PostgreSQL;
* Redis;
* event infrastructure;
* object storage;
* CDN;
* feed;
* discovery/search;
* messaging;
* notifications;
* moderation;
* administration;
* mobile clients;
* infrastructure.

The completed product is intended to provide:

* authenticated social interaction;
* profiles;
* social graph navigation;
* content consumption;
* media presentation;
* feed experiences;
* discovery;
* search;
* stories;
* short-form video;
* messaging;
* notifications;
* moderation-aware experiences;
* responsive web access.

These are global product capabilities.

This prompt implements only the **foundational web application architecture, shell, authentication, profile, relationship, shared data, and core navigation foundation**.

---

# 3. CURRENT FRONTEND ASSIGNMENT

Implement the production-grade foundational web application, including:

1. Next.js application structure;
2. TypeScript configuration appropriate to the repository;
3. routing architecture;
4. shared layout system;
5. design-system foundation;
6. global styling;
7. responsive behavior foundation;
8. accessibility foundation;
9. authentication flows;
10. session-aware client behavior;
11. protected/public route handling;
12. profile pages;
13. account settings foundation;
14. follow/follow-request UI;
15. block/mute/restrict controls where applicable to this scope;
16. API integration layer;
17. server/client state boundaries;
18. error handling;
19. loading states;
20. empty states;
21. optimistic updates only where safe;
22. client-side caching;
23. telemetry hooks;
24. security protections;
25. frontend testing;
26. documentation.

Do not implement the complete feed, messaging, discovery, stories, reels, notifications, moderation console, or other future UI domains in this prompt.

---

# 4. REPOSITORY INSPECTION

Before modifying or creating code, inspect the repository.

Inspect:

* existing web application;
* monorepo/workspace structure;
* package manager;
* Next.js version;
* React version;
* TypeScript configuration;
* styling system;
* component libraries;
* design tokens;
* routing;
* authentication code;
* API clients;
* generated API types;
* state-management libraries;
* test setup;
* linting;
* formatting;
* accessibility tooling;
* environment configuration;
* analytics/telemetry;
* existing layouts/pages/components.

Treat the repository as the source of truth for actual implementation state.

Do not assume another AI prompt was executed.

Do not assume another Claude conversation exists.

Do not fabricate backend behavior.

If compatible frontend infrastructure already exists, extend it instead of replacing it without a concrete reason.

---

# 5. TECHNOLOGY BASELINE

Use:

* Next.js;
* React;
* TypeScript;
* the repository's existing styling/design-system approach;
* the repository's existing state-management approach where sound;
* the project's API contract;
* the project's authentication/session contract;
* automated frontend tests.

Do not introduce a second competing UI library or state-management framework without a concrete repository-level reason.

Prefer server components/server rendering where they provide real value and client components where interactivity requires them.

---

# 6. BOUNDED IMPLEMENTATION SCOPE

## In Scope

Implement:

* web application shell;
* route hierarchy;
* application layouts;
* responsive navigation foundation;
* reusable UI primitives;
* design tokens;
* theme/foundation styling;
* accessibility primitives;
* authentication pages;
* login;
* registration;
* password recovery UI;
* verification UI;
* session handling;
* authenticated application bootstrapping;
* route protection;
* profile pages;
* profile editing;
* username editing where supported;
* privacy settings foundation;
* follow/unfollow UI;
* follow-request UI;
* block/mute/restrict controls where backend contracts support them;
* API client;
* typed API responses;
* client-side caching;
* request/error handling;
* loading and empty states;
* telemetry foundation;
* security protections;
* frontend unit/integration/component tests;
* documentation.

## Out of Scope

Do not implement:

* home feed UI;
* Explore/discovery UI;
* search UI;
* stories UI;
* reels/short-video UI;
* likes/comments/share interfaces;
* direct messaging UI;
* notification center;
* moderation/admin UI;
* creator analytics UI;
* complete mobile application;
* infrastructure provisioning.

Create reusable foundations required by later frontend prompts, but do not implement those future product surfaces.

---

# 7. APPLICATION ARCHITECTURE

Create a clear frontend architecture separating:

* application shell;
* routes;
* layouts;
* pages/screens;
* shared components;
* domain components;
* API clients;
* server-state;
* local UI state;
* authentication;
* authorization;
* utilities;
* telemetry;
* validation.

Avoid creating a single monolithic component tree.

Domain modules must remain independently understandable.

---

# 8. ROUTING ARCHITECTURE

Define a coherent route hierarchy.

At minimum provide conceptual routes for:

* authentication;
* registration;
* password recovery;
* verification;
* home/application shell;
* profile;
* account settings.

Separate public and authenticated route groups where appropriate.

Do not rely exclusively on client-side redirects for security-sensitive access control.

---

# 9. APPLICATION SHELL

Implement the global application shell.

Provide:

* primary navigation;
* responsive navigation behavior;
* application content area;
* account access controls;
* route transition behavior;
* appropriate loading states;
* mobile-width web behavior.

The shell must be reusable by future feed, search, messaging, and notification surfaces.

Do not hardcode future feature screens into the current implementation.

---

# 10. RESPONSIVE FOUNDATION

The web application must support:

* desktop;
* tablet;
* narrow mobile-web widths.

Define responsive behavior for:

* navigation;
* content width;
* spacing;
* typography;
* buttons;
* forms;
* cards;
* profile layouts.

Avoid designing desktop first and allowing mobile to become a broken compressed version.

---

# 11. DESIGN SYSTEM FOUNDATION

Create reusable UI primitives appropriate to the repository.

At minimum consider:

* buttons;
* inputs;
* text areas;
* forms;
* links;
* cards;
* avatar;
* badges;
* dialogs;
* menus;
* dropdowns;
* tabs;
* skeleton loaders;
* alerts;
* toasts;
* confirmation dialogs;
* pagination/loading primitives.

Use consistent:

* spacing;
* typography;
* radii;
* borders;
* focus states;
* interaction states.

Do not create multiple visually conflicting button or form systems.

---

# 12. DESIGN TOKENS

Create a centralized token strategy for:

* typography;
* spacing;
* sizing;
* radii;
* borders;
* shadows;
* z-index layers;
* motion;
* focus states;
* light/dark or theme variants where applicable.

Do not scatter arbitrary numeric values throughout components when a reusable token is appropriate.

---

# 13. ACCESSIBILITY FOUNDATION

Implement accessibility from the beginning.

Provide:

* semantic HTML;
* keyboard navigation;
* visible focus states;
* accessible names;
* form labels;
* error associations;
* appropriate ARIA only when needed;
* reduced-motion support where relevant;
* sufficient contrast;
* screen-reader-friendly loading/error states.

Do not use color as the sole indicator of state.

---

# 14. AUTHENTICATION ARCHITECTURE

Implement the web authentication integration using the backend's authoritative contract.

Support:

* registration;
* login;
* logout;
* session restoration;
* password recovery;
* password update;
* verification;
* session expiration handling.

Do not create a separate authentication backend.

The web application must consume the backend's authentication/session contract.

---

# 15. AUTHENTICATION STATE

Create a clear authentication state model distinguishing:

* unknown/loading;
* unauthenticated;
* authenticated;
* session expired;
* authentication error.

Avoid flashing authenticated content to unauthenticated users during initial hydration.

Avoid flashing unauthenticated UI to already authenticated users unnecessarily.

---

# 16. SESSION SECURITY

Use secure browser session mechanisms appropriate to the backend contract.

Prefer secure server-managed cookies where supported by the architecture.

Do not store long-lived authentication secrets in arbitrary local storage.

Do not expose refresh credentials to unrelated client code.

Do not log authentication credentials.

---

# 17. AUTHENTICATED ROUTES

Implement route protection.

Protected pages must verify actual authentication state.

Unauthenticated users should be redirected or otherwise handled according to route policy.

Do not treat a locally stored `isAuthenticated` boolean as authoritative security state.

---

# 18. PUBLIC ROUTES

Support public access where appropriate to:

* login;
* registration;
* password recovery;
* verification;
* public profile routes if the backend permits them.

Avoid loading authenticated application state unnecessarily on purely public routes.

---

# 19. API CLIENT

Implement a centralized API client.

It should handle:

* base configuration;
* authentication;
* request headers;
* request IDs/correlation where applicable;
* serialization;
* response parsing;
* error mapping;
* retries only for safe operations;
* cancellation;
* timeout behavior where appropriate.

Do not create independent ad hoc `fetch` wrappers throughout the application.

---

# 20. TYPED API CONTRACTS

Use strong typing for backend integration.

Where the repository provides generated schemas/types, consume them.

Where generation is not currently available, create explicit request/response types aligned with the backend contract.

Do not infer response fields from UI assumptions.

Do not duplicate backend business logic in frontend types.

---

# 21. API ERROR MODEL

Create a common client error model.

Handle categories such as:

* validation;
* authentication;
* authorization;
* conflict;
* not found;
* rate limit;
* server failure;
* unavailable dependency.

Expose useful user-facing messages while preserving machine-readable error codes internally.

Do not display raw backend stack traces.

---

# 22. REQUEST CANCELLATION

Support cancellation for requests where appropriate.

This is particularly important for:

* navigation changes;
* profile lookups;
* search-like future requests;
* forms;
* concurrent route transitions.

Do not allow obsolete requests to overwrite newer state.

---

# 23. SERVER VS CLIENT STATE

Clearly distinguish:

**server state**

from:

**local UI state**.

Server state includes:

* authenticated account;
* profile data;
* relationship data;
* session data.

Local state includes:

* open dialogs;
* selected tabs;
* form drafts;
* temporary UI state.

Do not duplicate server data into unrelated local state unnecessarily.

---

# 24. CLIENT-SIDE CACHING

Use the repository's chosen server-state/cache library where available.

Cache appropriate data such as:

* current account;
* profiles;
* relationship state.

Define:

* stale behavior;
* invalidation;
* refetch;
* mutation updates.

Do not cache authorization-sensitive responses globally without appropriate scoping.

---

# 25. OPTIMISTIC UPDATES

Use optimistic updates only where the operation is safe and reversible.

Good candidates may include:

* follow/unfollow;
* mute/unmute;
* block/unblock where UX requires immediate feedback.

When a mutation fails:

* restore the previous state;
* surface a meaningful error;
* avoid leaving the UI inconsistent with the backend.

Do not use optimistic updates for operations where incorrect temporary state could cause security or data-integrity problems.

---

# 26. ACCOUNT MODEL

Implement client-facing account state for:

* account ID;
* username;
* display name;
* privacy state;
* account type;
* profile reference;
* verification state where exposed.

Do not expose internal backend account fields to UI code.

---

# 27. CURRENT-USER CONTEXT

Implement a reusable current-user context/state boundary.

It must support:

* loading;
* authenticated account;
* logout;
* session expiry;
* profile updates.

Avoid fetching the current user separately from every page.

---

# 28. PROFILE PAGE

Implement a production-grade profile page.

Support:

* username;
* display name;
* avatar;
* biography;
* follower count where backend contract provides it;
* following count where provided;
* account privacy state;
* follow state;
* follow-request state;
* relationship actions;
* content area placeholder/extension boundary for later content UI.

Do not implement the complete post grid in this prompt unless it is required by the current repository foundation.

---

# 29. PROFILE AUTHORIZATION UX

The UI must reflect backend authorization.

Examples:

* private profile with unauthorized viewer;
* blocked profile;
* unavailable/deleted account;
* restricted relationship.

Do not attempt to reconstruct privacy behavior purely from frontend state.

The backend response remains authoritative.

---

# 30. PROFILE EDITING

Implement profile editing for fields supported by the backend.

Support:

* display name;
* biography;
* username;
* profile link where supported;
* privacy state.

Use:

* validation;
* accessible forms;
* pending state;
* error state;
* success feedback.

Do not allow direct manipulation of server-managed fields.

---

# 31. USERNAME EDITING

Implement username-change UX.

Handle:

* validation;
* normalization;
* availability response;
* conflict;
* loading;
* successful update;
* server rejection.

Do not perform client-only uniqueness assumptions.

The backend remains authoritative.

---

# 32. PRIVACY SETTINGS

Implement account privacy controls.

Support:

* public/private state.

The UI must clearly communicate that privacy changes affect content visibility and social relationships.

Do not expose unsupported policy options.

---

# 33. RELATIONSHIP UI

Implement follow relationship controls.

Support:

* follow;
* unfollow;
* follow request;
* cancel request where the backend supports it;
* approve/reject requests where the authenticated user is the target;
* block;
* unblock;
* mute;
* unmute;
* restrict;
* unrestrict.

The exact actions shown must depend on the current relationship state.

---

# 34. RELATIONSHIP STATE MODEL

Create a canonical frontend relationship-state model.

Possible states may include:

* none;
* following;
* follower;
* mutual;
* pending outgoing;
* pending incoming;
* blocked;
* muted;
* restricted.

Do not allow multiple independent booleans to produce impossible combinations unless the state model explicitly permits them.

---

# 35. FOLLOW MUTATION UX

For follow/unfollow:

* disable or stabilize controls while mutation is pending where appropriate;
* prevent duplicate requests;
* handle optimistic state safely;
* revert on failure;
* handle rate-limit responses;
* handle privacy changes;
* handle account unavailability.

Do not display an "approved" state before a pending request is actually accepted by the backend.

---

# 36. FOLLOW REQUEST UI

For private accounts, distinguish:

* not following;
* request pending;
* accepted follower;
* incoming request.

Provide appropriate actions.

Do not assume a private account's follow request is equivalent to an active follow.

---

# 37. BLOCK/MUTE/RESTRICT UX

Provide accessible confirmation flows for consequential relationship actions.

Explain the action sufficiently for users to understand what it does.

Handle successful state transitions by invalidating/refetching dependent profile/relationship state.

Do not implement unsupported downstream behavior inside the client.

---

# 38. ACCOUNT SETTINGS FOUNDATION

Create the initial settings architecture.

Support appropriate sections for:

* account/profile;
* privacy;
* security;
* sessions/devices.

Do not implement advanced notification preferences, creator analytics, or messaging settings yet.

---

# 39. SESSION/DEVICE SETTINGS

Implement a session/device management surface based on the backend contract.

Support:

* current session identification where available;
* list sessions;
* revoke session;
* revoke all other sessions.

Do not expose raw session tokens.

---

# 40. FORM ARCHITECTURE

Create reusable form infrastructure supporting:

* field registration;
* validation;
* server errors;
* accessible labels;
* submission state;
* dirty state;
* reset;
* success feedback.

Avoid duplicating form-state logic in every page.

---

# 41. LOADING STATES

Implement meaningful loading states for:

* authentication;
* current-user loading;
* profile loading;
* relationship mutations;
* settings loading;
* session loading.

Prefer skeletons or structured loading indicators over arbitrary spinners where a content skeleton improves continuity.

Do not make loading states inaccessible to assistive technologies.

---

# 42. ERROR STATES

Implement reusable error-state UI.

Support:

* recoverable network errors;
* authentication expiration;
* validation;
* permission denied;
* missing resource;
* server failure;
* rate limit.

Provide useful recovery actions where appropriate.

Do not expose internal implementation details.

---

# 43. EMPTY STATES

Implement meaningful empty states for:

* unavailable relationship data;
* no sessions;
* optional empty profile information;
* no follow requests where that screen exists.

Do not make empty states visually indistinguishable from loading failures.

---

# 44. NOTIFICATIONS FOUNDATION

Do not implement the notification center in this prompt.

However, establish a reusable frontend architecture boundary for future:

* notification data;
* unread count;
* push registration;
* notification center.

Do not create fake notification data.

---

# 45. REALTIME FOUNDATION

Do not implement the complete realtime messaging UI in this prompt.

Establish reusable infrastructure for future authenticated realtime use where the repository architecture requires it.

The abstraction should account for:

* authentication;
* reconnect;
* connection state;
* event parsing;
* cleanup;
* error handling.

Do not connect to undeclared fake websocket endpoints.

---

# 46. MEDIA FOUNDATION

The web foundation must be capable of supporting future media-heavy surfaces.

Create reusable primitives where genuinely useful for:

* avatar presentation;
* responsive images;
* media loading;
* fallback states.

Do not implement full post/video uploads in this prompt.

---

# 47. SECURITY

Frontend security requirements include:

* no hardcoded secrets;
* no privileged backend credentials in browser code;
* safe rendering;
* safe link handling;
* secure authentication storage;
* CSRF protection where applicable to the auth architecture;
* origin checks where relevant;
* safe error handling;
* controlled third-party scripts.

Never rely on the frontend for authorization.

---

# 48. CONTENT SECURITY

Treat all user-generated content as untrusted.

Do not render arbitrary HTML from:

* bios;
* captions;
* names;
* comments;
* external profile links

without an explicit safe rendering policy.

Use appropriate escaping/sanitization.

Do not use `dangerouslySetInnerHTML` casually.

---

# 49. ACCESSIBILITY TESTING

Include automated and manual-oriented checks where tooling permits for:

* keyboard navigation;
* focus order;
* form labels;
* error association;
* accessible names;
* modal behavior;
* button state;
* navigation landmarks.

Do not equate automated accessibility checks with complete accessibility compliance.

---

# 50. PERFORMANCE

Optimize the foundational web application for:

* initial load;
* route transitions;
* authenticated boot;
* profile rendering;
* image delivery;
* bundle size;
* unnecessary rerenders;
* API request duplication.

Use:

* server rendering where appropriate;
* code splitting;
* lazy loading;
* memoization only where justified;
* responsive image sizing;
* caching.

Do not add premature optimization that makes the code harder to maintain.

---

# 51. RESPONSIVE NAVIGATION

Implement navigation behavior that adapts across viewport sizes.

Desktop and mobile-web navigation may use different layouts while sharing:

* route definitions;
* accessible labels;
* active-state semantics;
* navigation targets.

Do not create two separate navigation systems with divergent route logic.

---

# 52. TELEMETRY

Create a frontend telemetry boundary.

Capture safe operational information such as:

* route transition failures;
* API errors;
* client performance metrics;
* application errors;
* authentication failures where appropriate.

Do not send:

* passwords;
* authentication tokens;
* raw private messages;
* private media content;
* sensitive form fields

to telemetry.

---

# 53. CLIENT ERROR BOUNDARIES

Implement appropriate React/application error boundaries.

Handle unexpected rendering failures without leaving the entire application unusable.

Provide:

* safe fallback UI;
* error identifier/correlation information where available;
* recovery/reload option.

Do not display raw stack traces.

---

# 54. ERROR REPORTING

Integrate the repository's chosen error-monitoring abstraction where available.

Ensure:

* environment is included;
* release/build identifier is included;
* sensitive fields are redacted;
* duplicate errors are controlled.

Do not hardcode provider credentials.

---

# 55. API RETRY BEHAVIOR

Frontend retries must be conservative.

Retry only:

* safe idempotent reads;
* explicitly retry-safe operations.

Do not automatically retry:

* account creation;
* follow mutations;
* profile updates;
* password changes;

unless the API contract provides an idempotency mechanism and the operation is explicitly safe.

---

# 56. CACHING AND INVALIDATION

Define cache invalidation after:

* profile update;
* username update;
* privacy change;
* follow/unfollow;
* block/unblock;
* mute/unmute;
* restriction change;
* session changes.

Avoid stale UI that contradicts successful mutations.

---

# 57. TESTING STRATEGY

Create real frontend tests.

## Unit Tests

Cover:

* validation;
* relationship-state logic;
* route guards;
* API error mapping;
* cache invalidation;
* authentication-state transitions.

## Component Tests

Cover:

* login form;
* registration form;
* profile;
* profile editor;
* follow controls;
* follow-request controls;
* privacy settings;
* session-management UI;
* dialogs and error states.

## Integration Tests

Cover:

* login flow;
* registration;
* protected routes;
* profile retrieval;
* profile edit;
* follow/unfollow;
* private-account request flow;
* block/mute/restrict actions;
* session revocation.

---

# 58. ACCESSIBILITY TESTING

Run appropriate accessibility checks against foundational components and pages.

At minimum validate:

* keyboard navigation;
* labels;
* focus handling;
* dialogs;
* buttons;
* forms;
* error messages.

Document tooling limitations.

---

# 59. SECURITY TESTING

Test:

* authenticated-route protection;
* unauthorized UI access;
* safe logout;
* token/credential non-exposure;
* unsafe HTML handling;
* malicious link handling;
* permission-denied states;
* session-expiry behavior.

Remember that client-side authorization checks are UX controls, not security boundaries.

---

# 60. PERFORMANCE VALIDATION

Perform targeted validation for:

* initial application render;
* authenticated boot;
* profile render;
* navigation;
* duplicated API requests;
* unnecessary component rerenders where measurable.

Do not claim global performance from a single local machine.

Record actual conditions.

---

# 61. DOCUMENTATION

Create/update documentation for:

* web application structure;
* routing;
* authentication;
* API integration;
* state management;
* design-system conventions;
* accessibility;
* responsive behavior;
* testing;
* local development;
* environment configuration;
* telemetry.

Documentation must describe actual implementation.

---

# 62. PORTABLE CONTRACTS

Maintain explicit frontend-facing contracts for:

* authentication state;
* current-user model;
* profile model;
* relationship state;
* API errors;
* pagination primitives;
* session management;
* telemetry conventions.

These contracts must remain compatible with backend and later frontend/mobile prompts.

---

# 63. CROSS-PART COMPATIBILITY

The web implementation must preserve compatibility with:

* backend APIs;
* authentication/session behavior;
* account/profile contracts;
* social graph;
* media contracts;
* feed;
* discovery;
* messaging;
* notifications;
* moderation;
* infrastructure;
* QA.

Do not create frontend-only versions of backend entities that diverge from authoritative schemas.

---

# 64. NO MOCK PRODUCTION BEHAVIOR

Do not use:

* hardcoded fake users in production flows;
* fake authentication;
* fake API responses;
* static relationship state;
* placeholder pages presented as finished functionality;
* TODO/FIXME implementation gaps;
* pseudo-code.

Test mocks are acceptable only inside test boundaries.

The actual runtime application must use the real backend contract.

---

# 65. VALIDATION

Before completion:

1. run formatting;
2. run linting;
3. run TypeScript type checking;
4. run unit tests;
5. run component tests;
6. run integration tests;
7. run accessibility checks where available;
8. run security-focused frontend tests;
9. validate production build;
10. validate route behavior;
11. validate environment configuration;
12. validate generated API/client contracts;
13. validate documentation.

If backend services or external systems required for an integration test are unavailable, clearly distinguish unavailable environment validation from tests that actually executed.

Do not claim successful external integration without actual execution.

---

# 66. IMPLEMENTATION REPORT

After implementation, provide a completion report containing:

## Files Created

List every file created.

## Files Modified

List every file modified.

## Files Deleted

List every file deleted, if any.

## Frontend Architecture Implemented

Summarize:

* application shell;
* routing;
* layouts;
* design system;
* responsive foundation;
* accessibility foundation.

## Authentication

Summarize:

* login;
* registration;
* recovery;
* verification;
* session handling;
* route protection.

## Profiles and Relationships

Summarize:

* profile;
* editing;
* privacy;
* follow;
* follow requests;
* block/mute/restrict.

## API/State Management

Summarize:

* API client;
* typed contracts;
* caching;
* invalidation;
* error handling.

## Security

Summarize:

* credential handling;
* safe rendering;
* route protection;
* telemetry redaction.

## Tests Created

List test categories and important scenarios.

## Tests Executed

State exactly which tests were executed.

## Validation Performed

State exact validation performed.

## Documentation Changes

List documentation created or updated.

## Integration Considerations

Explain how later feed, discovery, messaging, notifications, media, and mobile-facing work will consume the frontend foundation.

## Compatibility Considerations

Identify compatibility-sensitive changes.

## Known Limitations

List genuine limitations.

## Unresolved Issues

List only issues that remain unresolved.

---

# 67. DEFINITION OF DONE

This frontend milestone is complete only when:

* the Next.js application foundation works;
* the route hierarchy is coherent;
* the application shell is implemented;
* responsive navigation works;
* shared UI primitives exist;
* design tokens/styles are centralized;
* accessibility foundations exist;
* authentication flows work;
* session state is handled correctly;
* protected routes work;
* profile pages work;
* profile editing works;
* username editing works;
* privacy settings work;
* follow/unfollow works;
* follow-request flows work;
* block/mute/restrict actions work where supported;
* account/session settings work;
* API integration is centralized;
* API errors are handled;
* server state and local UI state are separated;
* caching/invalidation works;
* loading/empty/error states exist;
* telemetry is implemented safely;
* client error boundaries exist;
* security protections are implemented;
* unit tests exist;
* component tests exist;
* integration tests exist;
* accessibility validation is performed;
* production build succeeds;
* documentation reflects actual implementation;
* no secrets are committed;
* no fake runtime functionality exists;
* no intentional implementation gaps remain inside the defined scope.

---

# 68. FINAL IMPLEMENTATION DISCIPLINE

Implement **only the current prompt's scope**.

Do not implement:

* home feed;
* Explore;
* search UI;
* stories UI;
* reels UI;
* likes/comments/share UI;
* direct messaging UI;
* notification center;
* moderation/admin UI;
* creator analytics UI;
* mobile application.

Do not redesign the backend contracts.

Do not assume another AI prompt has been executed.

Do not depend on another AI conversation.

Do not place secrets in browser-accessible code.

Do not treat frontend authorization as a security boundary.

Produce real, tested, documented foundational web functionality for Instagram's authentication, application shell, profiles, account settings, and social-relationship experiences.
