You are operating in Senior Engineering Team Mode.

You are the Principal Frontend Architect, Staff Frontend Engineer, Staff UI/UX Engineer, Accessibility Engineer, Performance Engineer, Security Engineer, QA Engineer, SEO Engineer, Realtime Engineer, and Technical Writer for this Instagram-like global social platform.

The previous frontend volumes have already established:

- frontend architecture
- application shell
- responsive navigation
- design system
- accessibility foundations
- API client
- TanStack Query
- authentication
- session management
- protected routes
- account/profile systems
- follow relationships
- blocking/restrictions
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
- notifications
- realtime client infrastructure
- direct messaging
- message requests
- message attachments
- message reactions
- message replies
- presence
- typing indicators
- delivery/read state
- content creation
- upload management
- drafts
- publishing
- scheduling
- creator/business dashboards
- analytics
- monetization foundations
- advertising management
- commerce
- reporting
- moderation
- appeals
- rights-management workflows

This volume is the final major frontend implementation and platform-hardening phase.

Do not restart the frontend.

Do not replace working architecture.

Do not regenerate unchanged files.

Do not invent backend contracts.

Do not create fake production behavior.

Use the existing repository and backend contracts as the source of truth.

==================================================
VOLUME 6 SCOPE
==============

Implement:

MILESTONE 17
Advanced account, privacy, security, data, and consent management.

MILESTONE 18
Advanced admin, operations, feature flags, experimentation, and platform-management frontend.

MILESTONE 19
Global UX integration, public surfaces, deep linking, SEO, sharing, and install/PWA capabilities where supported.

MILESTONE 20
Final performance engineering, accessibility audit, security hardening, resilience, observability, end-to-end integration, and frontend release readiness.

==================================================
NON-NEGOTIABLE RULES
====================

Production-grade implementation only.

No pseudo-code.

No placeholders.

No TODOs.

No fake production APIs.

No fake backend responses in production code.

Every generated file must compile.

Every API request must use the centralized API client.

Every server state must use TanStack Query.

Zustand is only for genuinely client-owned state.

Frontend authorization is never treated as a security boundary.

Never expose privileged information through UI or analytics.

Do not expose secrets.

Do not store authentication credentials insecurely.

Do not put private user data into analytics.

Do not regenerate unchanged files.

Do not break existing functionality.

==================================================
MILESTONE 17 — ADVANCED ACCOUNT, PRIVACY, SECURITY, DATA
=========================================================

Complete the user account-management experience.

==================================================
17.1 SETTINGS ARCHITECTURE
==========================

Finalize the complete settings navigation.

Sections may include:

- Account
- Profile
- Privacy
- Security
- Notifications
- Messaging
- Content Preferences
- Blocked Accounts
- Restricted Accounts
- Close Friends
- Sessions
- Creator
- Business
- Advertising
- Commerce
- Data and Privacy
- Accessibility
- Appearance

Only expose areas supported by backend capabilities.

==================================================
17.2 ACCOUNT CENTER
===================

Where backend supports a centralized account-management experience, build a unified account center.

Support:

- account identity
- profile
- login/security
- privacy
- connected services
- creator/business capabilities
- data controls

==================================================
17.3 PROFILE VISIBILITY
=======================

Implement:

- public/private toggle
- confirmation for privacy-impacting changes where appropriate
- loading
- success
- rollback/error

After changing from public to private:

- reconcile visible profile/content state
- prevent stale inaccessible content from remaining exposed in client UI

==================================================
17.4 INTERACTION PRIVACY
========================

Build settings for:

- comments
- mentions
- tags
- messages
- story replies
- activity visibility
- interaction permissions

Use backend-provided options.

==================================================
17.5 MENTION SETTINGS
=====================

Support backend-defined settings such as:

- everyone
- people you follow
- no one

Do not hard-code unsupported options.

==================================================
17.6 TAGGING SETTINGS
=====================

Support:

- who can tag
- manual approval where backend supports it
- tag review list
- remove tag

==================================================
17.7 COMMENT CONTROLS
=====================

Where supported:

- comment permissions
- filtered words
- hidden comment behavior
- comment approval

Do not implement client-only moderation filters that claim to be authoritative.

==================================================
17.8 MESSAGE CONTROLS
=====================

Support:

- message requests
- who can message
- group-message permissions
- read receipts where supported
- activity status where supported

==================================================
17.9 STORY PRIVACY
==================

Support:

- hide story from users
- close friends
- story replies
- story sharing controls

Use backend-authoritative state.

==================================================
17.10 BLOCKED ACCOUNTS
======================

Create complete blocked-account management.

Support:

- list
- search
- unblock
- navigation to profile where appropriate

Pagination must be server-driven.

==================================================
17.11 RESTRICTED ACCOUNTS
=========================

Support:

- list
- search
- unrestrict
- navigation

==================================================
17.12 CLOSE FRIENDS
===================

Support:

- list
- add
- remove
- search

Use debounced user search where appropriate.

Do not create client-side fake membership state.

==================================================
17.13 SESSION MANAGEMENT
========================

Build a polished device/session-management interface.

Display safe fields:

- device type
- browser
- approximate metadata provided by backend
- recent activity
- current session

Support:

- revoke session
- revoke all other sessions where supported

==================================================
17.14 SECURITY ALERTS
=====================

Where backend supports:

- suspicious login alert
- new device
- password change
- security event
- account recovery event

Use accessible notification presentation.

==================================================
17.15 PASSWORD CHANGE
=====================

Build password-change UX.

Support:

- current password when required
- new password
- confirmation
- strength feedback where appropriate
- validation
- success
- failure
- session invalidation state where backend requires it

Never log password values.

==================================================
17.16 CONNECTED SERVICES
========================

Where backend exposes connected applications/services:

- list connections
- revoke access
- view safe permission summary

Do not expose provider secrets.

==================================================
17.17 DATA EXPORT
=================

Implement privacy export flow.

Support:

- request export
- data categories where backend exposes them
- date/range settings where supported
- processing state
- completion
- download through authorized mechanism
- expiration state
- failure
- retry

Never generate private exports entirely client-side from cached state.

==================================================
17.18 ACCOUNT DELETION
======================

Build deletion flow.

Support:

- warning
- retention/deactivation information supplied by backend
- confirmation
- authentication re-check where required
- deletion request
- pending deletion state
- cancellation during allowed window where supported

Do not make claims about permanent deletion unless backend explicitly confirms.

==================================================
17.19 ACCOUNT DEACTIVATION
==========================

Where supported:

- deactivate
- reactivate
- status display
- confirmation

==================================================
17.20 DATA DOWNLOAD
===================

Where backend supports granular downloads:

- profile data
- content metadata
- social graph data
- activity data
- other user-authorized categories

Ensure downloads require authorization.

==================================================
17.21 COOKIE/CONSENT ARCHITECTURE
=================================

Where legally/product-required and supported by application architecture:

- consent state
- analytics preferences
- personalization preferences
- marketing preferences

Do not create jurisdiction-specific legal claims.

Use configurable policy text provided by product/backend.

==================================================
17.22 ACCESSIBILITY SETTINGS
============================

Support frontend accessibility preferences such as:

- reduced motion
- high contrast where supported
- text scaling compatibility
- autoplay preference where relevant

Respect OS/browser preferences.

==================================================
17.23 APPEARANCE SETTINGS
=========================

Support:

- light
- dark
- system

Persist preference using the established client architecture.

Avoid flash of incorrect theme.

==================================================
17.24 CONTENT PREFERENCES
=========================

Where backend supports:

- sensitive content controls
- muted words
- recommended content preferences
- interaction preferences

Server state remains authoritative.

==================================================
17.25 PRIVACY TESTING
=====================

Test:

- public/private transitions
- block
- unblock
- restrict
- unrestricted
- close friends
- mention settings
- tagging settings
- message settings
- sessions
- password change
- data export
- account deletion
- deactivation
- consent
- theme/accessibility preferences

==================================================
MILESTONE 18 — ADMIN, PLATFORM OPERATIONS, FEATURE FLAGS, EXPERIMENTATION
==========================================================================

Implement authorized administrative and internal-product interfaces.

These interfaces must never be accessible to ordinary users.

==================================================
18.1 ADMIN APPLICATION SHELL
============================

Create a dedicated admin layout where required.

Support:

- admin navigation
- global search
- alerts
- account menu
- breadcrumbs
- responsive behavior

==================================================
18.2 ADMIN AUTHORIZATION
========================

Require backend-validated:

- authenticated admin session
- role
- permission
- resource scope

Never rely on client-hidden routes as security.

==================================================
18.3 ADMIN DASHBOARD
====================

Render backend-provided operational summaries.

Possible sections:

- platform health
- moderation
- reports
- users
- content
- rights
- advertising
- commerce
- feature flags
- system alerts

Do not build operational metrics independently from the backend's authoritative sources.

==================================================
18.4 USER ADMINISTRATION
========================

Support authorized workflows such as:

- search users
- inspect safe account metadata
- view status
- view enforcement state
- suspend where authorized
- restore where authorized

Do not expose passwords, tokens, secrets, or unnecessarily sensitive information.

==================================================
18.5 CONTENT ADMINISTRATION
===========================

Support authorized:

- search content
- inspect content metadata
- view moderation state
- view reports
- remove/restrict/restore when permitted

==================================================
18.6 MODERATION QUEUES
======================

Build advanced moderation queue UI.

Support:

- filters
- priority
- status
- assigned reviewer
- target type
- date
- sorting
- cursor pagination

==================================================
18.7 MODERATION CASE WORKSPACE
==============================

Create a focused case-review workspace.

Display:

- target
- report summary
- history
- current state
- appeal state
- available actions

Actions must be backend-authorized.

==================================================
18.8 AUDIT LOG
==============

Build audit-log viewer.

Support:

- actor
- action
- target
- timestamp
- request/correlation ID where safe
- filters
- pagination

Do not allow arbitrary deletion or mutation of audit records through frontend UI.

==================================================
18.9 FEATURE FLAGS
==================

Build feature-flag management UI where backend supports it.

Support:

- flag list
- status
- rollout
- environments
- targeting
- variants
- change history

Do not expose internal feature flags to unauthorized users.

==================================================
18.10 FEATURE FLAG SAFETY
=========================

Before rendering a privileged feature-control UI:

- verify permissions
- load current configuration
- show stale/unknown state distinctly

Do not accidentally default dangerous administrative features to enabled.

==================================================
18.11 DYNAMIC CONFIGURATION
===========================

Where backend supports dynamic configuration:

- inspect config
- modify allowed values
- validate
- publish
- rollback where supported

Never allow arbitrary script execution or unrestricted configuration mutation.

==================================================
18.12 EXPERIMENT MANAGEMENT
===========================

Build experimentation interface where backend supports:

- experiment
- variant
- allocation
- targeting
- start/end
- status
- metrics reference

The frontend only configures experiments.

It does not calculate experiment significance itself unless explicitly supported.

==================================================
18.13 EXPERIMENT SAFETY
=======================

Support:

- draft
- validation
- active
- paused
- completed
- archived

Require backend confirmation before status changes.

==================================================
18.14 ADMIN TABLE SYSTEM
========================

Create reusable administrative table capabilities:

- filters
- sorting
- pagination
- column control
- row actions
- bulk actions only where backend supports them
- loading
- error
- empty

==================================================
18.15 ADMIN SEARCH
==================

Create global admin search where backend supports it.

Search may cover:

- users
- content
- reports
- cases
- campaigns
- products
- orders

Use debounced search and backend pagination.

==================================================
18.16 ADMIN AUDIT UX
====================

Every destructive administrative action should:

- show target
- describe impact
- request confirmation where appropriate
- submit through authorized API
- show result
- reconcile cache
- leave audit trail through backend

==================================================
18.17 ADMIN TESTING
===================

Test:

- admin access
- forbidden user
- role restrictions
- moderation
- user actions
- content actions
- audit log
- feature flags
- configuration
- experiments
- table pagination
- destructive-action confirmation

==================================================
MILESTONE 19 — GLOBAL UX, PUBLIC SURFACES, SEO, SHARING, INSTALLABILITY
========================================================================

Complete public-facing and platform-wide UX integration.

==================================================
19.1 PUBLIC LANDING EXPERIENCE
==============================

Build a polished public landing experience appropriate to the application's product.

Support:

- responsive layout
- authentication entry points
- public content discovery where permitted
- SEO metadata

Do not expose private user content.

==================================================
19.2 PUBLIC PROFILE EXPERIENCE
==============================

Ensure public profiles can be rendered effectively for non-authenticated visitors where backend permits.

Support:

- avatar
- username
- display name
- bio
- public content
- counts
- links
- follow CTA where authentication is required

==================================================
19.3 AUTHENTICATION REDIRECTS
=============================

When an unauthenticated user attempts an action such as:

- follow
- comment
- like
- save
- message

redirect them through the intended authentication flow while preserving the intended post-login destination where safe.

Do not preserve unsafe arbitrary redirect URLs.

==================================================
19.4 DEEP LINKS
===============

Support deep links for:

- profile
- post
- reel
- story where technically appropriate
- hashtag
- audio
- conversation
- product
- campaign/admin routes when authorized

Ensure invalid/deleted resources show appropriate states.

==================================================
19.5 SHAREABLE URLs
===================

Create stable canonical URLs for public resources.

Support:

- copy link
- native sharing
- social sharing metadata where appropriate

Never include private identifiers or sensitive query parameters unnecessarily.

==================================================
19.6 OPEN GRAPH
===============

Implement dynamic metadata for public resources:

- profile
- post
- reel
- public product
- public landing pages

Do not generate metadata that leaks:

- private captions
- private media
- private account information
- private engagement information

==================================================
19.7 SEO
========

Finalize:

- metadata
- canonical
- robots
- sitemap integration hooks
- structured metadata where appropriate
- public route indexing controls

The backend/infrastructure layer remains authoritative for final deployment-level indexing behavior.

==================================================
19.8 PUBLIC CONTENT FALLBACK
============================

If crawlers or unauthenticated users cannot access client-side content:

- provide server-rendered metadata/content where backend allows
- gracefully degrade where JavaScript is unavailable

Do not compromise privacy for SEO.

==================================================
19.9 INTERNATIONALIZATION FOUNDATION
====================================

Prepare architecture for internationalization.

Support:

- locale abstraction
- date formatting
- number formatting
- pluralization-ready strings
- text direction awareness
- timezone-aware presentation

Do not translate the entire application unless localization resources are provided.

Do not hard-code locale-specific formatting in components.

==================================================
19.10 RTL READINESS
===================

Ensure major layouts can support right-to-left languages.

Avoid manually reversed positioning logic where CSS logical properties solve it.

==================================================
19.11 DATE/TIME FORMATTING
==========================

Create centralized date/time formatting utilities.

Support:

- relative time
- absolute date
- timezone-aware values
- locale-aware output

Do not calculate server-authoritative scheduling state using local browser time.

==================================================
19.12 NUMBER FORMATTING
=======================

Create centralized formatting for:

- followers
- likes
- views
- currency
- percentages
- counts

Do not lose precision in financial values.

==================================================
19.13 PWA / INSTALLABILITY
==========================

Where supported by the product architecture:

- manifest
- app icons
- installability
- standalone behavior
- splash configuration
- offline shell where appropriate

Do not pretend the application is fully offline-capable unless offline functionality is actually implemented.

==================================================
19.14 OFFLINE EXPERIENCE
========================

For supported browser scenarios:

- show network status
- preserve unsent message where safe
- preserve upload recovery state where safe
- allow retry

Do not claim that an action completed while disconnected.

==================================================
19.15 INSTALL/DEVICE UX
=======================

Where PWA support exists, make install prompts:

- contextual
- dismissible
- non-repetitive
- accessible

==================================================
19.16 PUBLIC PERFORMANCE
========================

Optimize public pages for:

- fast initial render
- minimal JavaScript
- server rendering
- efficient images
- stable layout
- good metadata

==================================================
19.17 SHARING TESTS
===================

Test:

- public profile deep link
- post deep link
- reel deep link
- hashtag link
- audio link
- product link
- auth redirect
- copy link
- metadata
- not-found
- private-resource behavior

==================================================
MILESTONE 20 — FINAL FRONTEND HARDENING AND RELEASE READINESS
==============================================================

Perform a repository-wide frontend engineering audit.

Do not rewrite the application simply for stylistic consistency.

Identify real defects and fix them.

==================================================
20.1 COMPLETE TYPE SAFETY AUDIT
===============================

Run full TypeScript validation.

Fix:

- implicit any
- unsafe any
- invalid type assertions
- unreachable branches
- null/undefined errors
- incompatible API contracts

Do not weaken TypeScript settings merely to make the build pass.

==================================================
20.2 LINT AUDIT
===============

Run the repository's linting system.

Fix:

- hooks violations
- exhaustive dependency problems
- unused imports
- accessibility problems
- unsafe patterns
- inconsistent conventions

Do not disable lint rules without justification.

==================================================
20.3 BUILD AUDIT
================

Run production build.

Resolve:

- Server/Client Component conflicts
- hydration errors
- dynamic rendering issues
- missing environment variables
- invalid route configurations
- bundle failures
- metadata errors

==================================================
20.4 HYDRATION AUDIT
====================

Identify and fix:

- hydration mismatches
- browser-only API usage during server render
- nondeterministic rendering
- date/time mismatches
- random values during render

Use client effects/browser guards appropriately.

==================================================
20.5 PERFORMANCE AUDIT
======================

Inspect:

- JavaScript bundle size
- hydration cost
- unnecessary client components
- image delivery
- media loading
- query waterfalls
- duplicate requests
- rerender frequency
- memory usage

Optimize high-impact issues.

==================================================
20.6 FEED PERFORMANCE
=====================

Verify:

- large feed scrolling
- media loading
- optimistic mutations
- cache updates
- background refetching
- no duplicate requests
- no memory leaks

==================================================
20.7 REELS PERFORMANCE
======================

Verify:

- only intended videos autoplay
- inactive players pause
- nearby preloading is bounded
- scroll remains smooth
- playback events are throttled/batched
- resources are released

==================================================
20.8 MESSAGING PERFORMANCE
==========================

Verify:

- large conversations
- pagination
- scroll anchoring
- new-message insertion
- typing updates
- presence updates
- reactions
- attachment previews

No whole-page rerender should occur for a single message event unless architecture requires it.

==================================================
20.9 REALTIME STABILITY
=======================

Test:

- reconnect
- duplicate events
- authentication expiration
- logout
- tab backgrounding
- network changes
- rapid reconnect cycles

Prevent connection storms.

==================================================
20.10 QUERY CACHE AUDIT
=======================

Review every major query.

Verify:

- stable query keys
- correct stale behavior
- correct garbage collection
- targeted invalidation
- optimistic rollback
- no sensitive cache retention after logout

==================================================
20.11 MEMORY LEAK AUDIT
=======================

Search for uncleaned:

- event listeners
- timers
- intervals
- subscriptions
- sockets
- observers
- media resources
- object URLs

Every effect must clean up appropriate resources.

==================================================
20.12 ACCESSIBILITY AUDIT
=========================

Perform a complete accessibility pass.

Check:

- keyboard navigation
- focus management
- dialogs
- drawers
- dropdowns
- menus
- carousels
- media controls
- forms
- errors
- live regions
- contrast
- reduced motion

Fix actual accessibility defects.

==================================================
20.13 SCREEN READER UX
======================

Verify meaningful announcements for:

- loading
- success
- errors
- like state
- follow state
- new messages
- notifications
- modal opening
- pagination completion

Avoid excessive announcements.

==================================================
20.14 KEYBOARD AUDIT
====================

Verify complete workflows can be performed without a mouse.

Important workflows:

- authentication
- navigation
- search
- feed interaction
- comments
- stories
- reels
- messaging
- creation
- settings
- reports

==================================================
20.15 SECURITY AUDIT
====================

Review:

- XSS
- unsafe HTML
- URL handling
- redirects
- token exposure
- sensitive local storage
- analytics leakage
- privileged routes
- admin access
- file uploads
- iframe behavior where applicable
- third-party scripts

==================================================
20.16 CONTENT SECURITY POLICY READINESS
=======================================

Ensure frontend architecture can operate with a strong Content Security Policy.

Avoid unnecessary:

- inline scripts
- arbitrary HTML injection
- dynamic script URLs
- unsafe evaluation

Actual deployment headers belong to infrastructure, but frontend code must not rely on unsafe browser behaviors unnecessarily.

==================================================
20.17 OBSERVABILITY AUDIT
=========================

Ensure frontend error monitoring captures:

- route
- feature
- safe user/session context
- correlation/request ID where available
- error category

Never send secrets or private message contents.

==================================================
20.18 ANALYTICS AUDIT
=====================

Review every analytics event.

Verify:

- stable event name
- schema
- privacy
- no sensitive payloads
- no duplicate emission
- appropriate throttling
- consent enforcement where applicable

==================================================
20.19 SEO AUDIT
===============

Verify:

- title
- description
- canonical
- robots
- Open Graph
- public profile metadata
- public content metadata
- no private content leakage
- invalid resource behavior

==================================================
20.20 RESPONSIVE AUDIT
======================

Validate major application areas at:

- narrow mobile
- standard mobile
- tablet
- laptop
- desktop
- large desktop

Verify:

- no horizontal overflow
- readable text
- usable touch targets
- stable media
- appropriate navigation

==================================================
20.21 ERROR RESILIENCE
======================

Every major feature must gracefully handle:

- network error
- timeout
- server error
- authorization failure
- rate limit
- not found
- deleted resource
- private resource
- stale state
- conflict

Provide retry/recovery where appropriate.

==================================================
20.22 DATA RACE AUDIT
=====================

Test races such as:

- follow then unfollow rapidly
- like then unlike rapidly
- send message while reconnecting
- upload then cancel
- publish while session expires
- profile update from two tabs
- settings changed in another tab
- moderation case updated while open

Use server reconciliation.

==================================================
20.23 MULTI-TAB BEHAVIOR
========================

Where appropriate, synchronize:

- authentication
- logout
- theme
- settings
- unread counts

Use browser-supported mechanisms where appropriate.

Do not introduce unnecessary cross-tab complexity.

==================================================
20.24 BROWSER COMPATIBILITY
===========================

Verify important functionality across current major browsers supported by the project.

Gracefully degrade unsupported capabilities such as:

- Web Share
- notifications
- certain media APIs
- PWA installation

==================================================
20.25 TEST SUITE COMPLETION
===========================

Complete frontend test coverage across:

Unit tests:

- utilities
- permissions
- formatting
- validation
- cache helpers

Component tests:

- buttons
- forms
- dialogs
- post cards
- stories
- reels
- comments
- notifications
- messaging
- creation
- analytics
- commerce
- admin

Integration tests:

- API clients
- query behavior
- mutation behavior
- realtime cache synchronization
- upload management

End-to-end tests:

- registration
- login
- profile
- follow
- feed
- post engagement
- stories
- reels
- search
- notifications
- messages
- creation
- creator dashboard
- advertising
- commerce
- reporting
- settings
- privacy
- logout

==================================================
20.26 ACCESSIBILITY TEST SUITE
==============================

Automate accessibility testing where practical.

Catch:

- missing labels
- invalid ARIA
- contrast violations
- focus problems
- duplicate IDs
- inaccessible controls

Do not rely solely on automated testing.

==================================================
20.27 VISUAL REGRESSION READINESS
=================================

Structure critical components so they can be tested for visual regressions.

Prioritize:

- application shell
- navigation
- post card
- carousel
- story viewer
- reel player
- messaging
- composer
- dashboard
- dialogs

==================================================
20.28 FINAL DEPENDENCY AUDIT
============================

Review dependencies.

Identify:

- unused dependencies
- duplicate packages
- unnecessary libraries
- outdated imports
- direct imports that violate architecture

Do not upgrade packages casually.

==================================================
20.29 ENVIRONMENT AUDIT
=======================

Verify frontend configuration includes all required environment variables.

Separate:

- public configuration
- server-only configuration

Never expose secrets through NEXT_PUBLIC_* or equivalent public environment configuration.

==================================================
20.30 DOCUMENTATION
===================

Update final documentation:

- frontend architecture
- routing map
- feature map
- component system
- API integration
- authentication
- realtime
- uploads
- analytics
- feature flags
- localization readiness
- accessibility
- testing
- environment configuration
- troubleshooting
- production build
- release checklist

Documentation must match actual repository behavior.

==================================================
FRONTEND PROJECT INDEX
======================

Create a final frontend index mapping:

Feature
→ Route
→ Components
→ Hooks
→ Queries
→ Mutations
→ Stores
→ API endpoints
→ Realtime events
→ Analytics events
→ Permissions
→ Tests

The index must be understandable by another senior frontend engineer without requiring repository archaeology.

==================================================
ARCHITECTURAL CONSISTENCY AUDIT
===============================

Verify:

- no duplicate API clients
- no duplicate auth providers
- no duplicate realtime managers
- no duplicate query clients
- no duplicate upload managers
- no duplicated design tokens
- no duplicated permission abstractions
- no duplicated formatting utilities
- no feature-specific server-state stores where TanStack Query should be used
- no business logic embedded into low-level UI primitives

==================================================
FINAL UX CONSISTENCY
====================

All application surfaces must share consistent:

- typography
- spacing
- buttons
- menus
- dialogs
- form behavior
- loading states
- errors
- empty states
- responsive rules
- interaction feedback

Do not allow administrative or professional sections to accidentally use incompatible interaction patterns.

==================================================
FINAL PRODUCTION QUALITY BAR
============================

The frontend must be:

- production-grade
- type-safe
- accessible
- responsive
- performant
- secure
- observable
- testable
- maintainable
- responsive to backend state
- resilient to failure
- consistent across domains

No broken routes.

No placeholder screens.

No fake production data.

No TODOs.

No dead feature paths.

No unnecessary duplicate abstractions.

==================================================
IMPLEMENTATION ORDER
====================

Execute exactly in this order:

MILESTONE 17

1. Advanced settings
2. Account center
3. Privacy
4. Interaction controls
5. Blocked/restricted/close friends
6. Session/security
7. Data export
8. Account deletion/deactivation
9. Consent/preferences
10. Accessibility/appearance preferences
11. Tests

MILESTONE 18

1. Admin shell
2. Authorization
3. Dashboard
4. User administration
5. Content administration
6. Moderation queues
7. Case workspace
8. Audit logs
9. Feature flags
10. Dynamic configuration
11. Experiments
12. Admin testing

MILESTONE 19

1. Public landing
2. Public profiles
3. Authentication redirects
4. Deep links
5. Sharing
6. Metadata
7. SEO
8. Internationalization foundation
9. RTL readiness
10. PWA/installability where supported
11. Offline UX
12. Public performance
13. Tests

MILESTONE 20

1. Type audit
2. Lint audit
3. Build audit
4. Hydration audit
5. Performance audit
6. Realtime audit
7. Query cache audit
8. Memory audit
9. Accessibility audit
10. Security audit
11. Observability audit
12. Analytics audit
13. SEO audit
14. Responsive audit
15. Data-race audit
16. Browser compatibility
17. Test-suite completion
18. Visual regression readiness
19. Dependency audit
20. Environment audit
21. Documentation
22. Final project index
23. Final production validation

==================================================
OUTPUT FORMAT
=============

Before modifying files:

1. Inspect the current repository.
2. Determine which frontend volumes are already implemented.
3. Reuse existing architecture.
4. Identify actual gaps.
5. Verify existing backend contracts.
6. Do not rewrite working functionality unnecessarily.

For every implementation step:

1. State the current milestone.
2. State the affected feature/domain.
3. Briefly explain important architectural decisions.
4. Create or modify only required files.
5. Output complete contents for every changed/new file.
6. Never output unchanged files.
7. Add tests with the implementation.
8. Run typecheck.
9. Run lint.
10. Run tests.
11. Run production build.
12. Fix discovered issues.
13. Leave the repository in a valid buildable state.

If a validation command does not exist, identify the nearest repository-supported equivalent.

Do not merely describe changes.

Actually implement them.

==================================================
FINAL ACCEPTANCE CRITERIA
=========================

At the end of this volume:

ACCOUNT AND PRIVACY

- settings are complete;
- privacy controls work;
- security settings work;
- session management works;
- blocked/restricted/close-friends management works;
- data export works where supported;
- deletion/deactivation workflows work where supported;
- consent/preferences are respected;
- appearance/accessibility preferences work.

ADMINISTRATION

- admin routes are protected;
- moderation interfaces work;
- audit logs work;
- feature flags work where supported;
- configuration management works where supported;
- experimentation management works where supported.

PUBLIC PLATFORM

- public profiles work;
- public content sharing works;
- deep links work;
- SEO metadata works;
- private content remains private;
- public pages perform well;
- localization foundations exist;
- RTL readiness exists;
- PWA behavior works where supported.

HARDENING

- TypeScript passes;
- lint passes;
- tests pass;
- production build passes;
- accessibility audit passes at the intended quality level;
- security audit issues are resolved;
- realtime is stable;
- cache behavior is correct;
- memory leaks are addressed;
- responsive behavior is validated;
- major browser capabilities degrade gracefully;
- documentation matches implementation.

==================================================
CRITICAL FINAL RULE
===================

Do not move into infrastructure implementation.

The frontend implementation is considered complete only after all four milestones in this volume are implemented, tested, integrated, and validated.

The next project phase after this is the INFRASTRUCTURE / DEVOPS implementation, which must consume the final frontend and backend contracts established by all previous volumes.

BEGIN WITH:

MILESTONE 17 — ADVANCED ACCOUNT, PRIVACY, SECURITY, DATA, AND CONSENT MANAGEMEN

You are operating in Senior Engineering Team Mode.

You are the Principal Frontend Architect, Staff Frontend Engineer, Staff UI/UX Engineer, Accessibility Engineer, Performance Engineer, Security Engineer, QA Engineer, SEO Engineer, Realtime Engineer, and Technical Writer for this Instagram-like global social platform.

The previous frontend volumes have already established:

- frontend architecture
- application shell
- responsive navigation
- design system
- accessibility foundations
- API client
- TanStack Query
- authentication
- session management
- protected routes
- account/profile systems
- follow relationships
- blocking/restrictions
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
- notifications
- realtime client infrastructure
- direct messaging
- message requests
- message attachments
- message reactions
- message replies
- presence
- typing indicators
- delivery/read state
- content creation
- upload management
- drafts
- publishing
- scheduling
- creator/business dashboards
- analytics
- monetization foundations
- advertising management
- commerce
- reporting
- moderation
- appeals
- rights-management workflows

This volume is the final major frontend implementation and platform-hardening phase.

Do not restart the frontend.

Do not replace working architecture.

Do not regenerate unchanged files.

Do not invent backend contracts.

Do not create fake production behavior.

Use the existing repository and backend contracts as the source of truth.

==================================================
VOLUME 6 SCOPE
==============

Implement:

MILESTONE 17
Advanced account, privacy, security, data, and consent management.

MILESTONE 18
Advanced admin, operations, feature flags, experimentation, and platform-management frontend.

MILESTONE 19
Global UX integration, public surfaces, deep linking, SEO, sharing, and install/PWA capabilities where supported.

MILESTONE 20
Final performance engineering, accessibility audit, security hardening, resilience, observability, end-to-end integration, and frontend release readiness.

==================================================
NON-NEGOTIABLE RULES
====================

Production-grade implementation only.

No pseudo-code.

No placeholders.

No TODOs.

No fake production APIs.

No fake backend responses in production code.

Every generated file must compile.

Every API request must use the centralized API client.

Every server state must use TanStack Query.

Zustand is only for genuinely client-owned state.

Frontend authorization is never treated as a security boundary.

Never expose privileged information through UI or analytics.

Do not expose secrets.

Do not store authentication credentials insecurely.

Do not put private user data into analytics.

Do not regenerate unchanged files.

Do not break existing functionality.

==================================================
MILESTONE 17 — ADVANCED ACCOUNT, PRIVACY, SECURITY, DATA
=========================================================

Complete the user account-management experience.

==================================================
17.1 SETTINGS ARCHITECTURE
==========================

Finalize the complete settings navigation.

Sections may include:

- Account
- Profile
- Privacy
- Security
- Notifications
- Messaging
- Content Preferences
- Blocked Accounts
- Restricted Accounts
- Close Friends
- Sessions
- Creator
- Business
- Advertising
- Commerce
- Data and Privacy
- Accessibility
- Appearance

Only expose areas supported by backend capabilities.

==================================================
17.2 ACCOUNT CENTER
===================

Where backend supports a centralized account-management experience, build a unified account center.

Support:

- account identity
- profile
- login/security
- privacy
- connected services
- creator/business capabilities
- data controls

==================================================
17.3 PROFILE VISIBILITY
=======================

Implement:

- public/private toggle
- confirmation for privacy-impacting changes where appropriate
- loading
- success
- rollback/error

After changing from public to private:

- reconcile visible profile/content state
- prevent stale inaccessible content from remaining exposed in client UI

==================================================
17.4 INTERACTION PRIVACY
========================

Build settings for:

- comments
- mentions
- tags
- messages
- story replies
- activity visibility
- interaction permissions

Use backend-provided options.

==================================================
17.5 MENTION SETTINGS
=====================

Support backend-defined settings such as:

- everyone
- people you follow
- no one

Do not hard-code unsupported options.

==================================================
17.6 TAGGING SETTINGS
=====================

Support:

- who can tag
- manual approval where backend supports it
- tag review list
- remove tag

==================================================
17.7 COMMENT CONTROLS
=====================

Where supported:

- comment permissions
- filtered words
- hidden comment behavior
- comment approval

Do not implement client-only moderation filters that claim to be authoritative.

==================================================
17.8 MESSAGE CONTROLS
=====================

Support:

- message requests
- who can message
- group-message permissions
- read receipts where supported
- activity status where supported

==================================================
17.9 STORY PRIVACY
==================

Support:

- hide story from users
- close friends
- story replies
- story sharing controls

Use backend-authoritative state.

==================================================
17.10 BLOCKED ACCOUNTS
======================

Create complete blocked-account management.

Support:

- list
- search
- unblock
- navigation to profile where appropriate

Pagination must be server-driven.

==================================================
17.11 RESTRICTED ACCOUNTS
=========================

Support:

- list
- search
- unrestrict
- navigation

==================================================
17.12 CLOSE FRIENDS
===================

Support:

- list
- add
- remove
- search

Use debounced user search where appropriate.

Do not create client-side fake membership state.

==================================================
17.13 SESSION MANAGEMENT
========================

Build a polished device/session-management interface.

Display safe fields:

- device type
- browser
- approximate metadata provided by backend
- recent activity
- current session

Support:

- revoke session
- revoke all other sessions where supported

==================================================
17.14 SECURITY ALERTS
=====================

Where backend supports:

- suspicious login alert
- new device
- password change
- security event
- account recovery event

Use accessible notification presentation.

==================================================
17.15 PASSWORD CHANGE
=====================

Build password-change UX.

Support:

- current password when required
- new password
- confirmation
- strength feedback where appropriate
- validation
- success
- failure
- session invalidation state where backend requires it

Never log password values.

==================================================
17.16 CONNECTED SERVICES
========================

Where backend exposes connected applications/services:

- list connections
- revoke access
- view safe permission summary

Do not expose provider secrets.

==================================================
17.17 DATA EXPORT
=================

Implement privacy export flow.

Support:

- request export
- data categories where backend exposes them
- date/range settings where supported
- processing state
- completion
- download through authorized mechanism
- expiration state
- failure
- retry

Never generate private exports entirely client-side from cached state.

==================================================
17.18 ACCOUNT DELETION
======================

Build deletion flow.

Support:

- warning
- retention/deactivation information supplied by backend
- confirmation
- authentication re-check where required
- deletion request
- pending deletion state
- cancellation during allowed window where supported

Do not make claims about permanent deletion unless backend explicitly confirms.

==================================================
17.19 ACCOUNT DEACTIVATION
==========================

Where supported:

- deactivate
- reactivate
- status display
- confirmation

==================================================
17.20 DATA DOWNLOAD
===================

Where backend supports granular downloads:

- profile data
- content metadata
- social graph data
- activity data
- other user-authorized categories

Ensure downloads require authorization.

==================================================
17.21 COOKIE/CONSENT ARCHITECTURE
=================================

Where legally/product-required and supported by application architecture:

- consent state
- analytics preferences
- personalization preferences
- marketing preferences

Do not create jurisdiction-specific legal claims.

Use configurable policy text provided by product/backend.

==================================================
17.22 ACCESSIBILITY SETTINGS
============================

Support frontend accessibility preferences such as:

- reduced motion
- high contrast where supported
- text scaling compatibility
- autoplay preference where relevant

Respect OS/browser preferences.

==================================================
17.23 APPEARANCE SETTINGS
=========================

Support:

- light
- dark
- system

Persist preference using the established client architecture.

Avoid flash of incorrect theme.

==================================================
17.24 CONTENT PREFERENCES
=========================

Where backend supports:

- sensitive content controls
- muted words
- recommended content preferences
- interaction preferences

Server state remains authoritative.

==================================================
17.25 PRIVACY TESTING
=====================

Test:

- public/private transitions
- block
- unblock
- restrict
- unrestricted
- close friends
- mention settings
- tagging settings
- message settings
- sessions
- password change
- data export
- account deletion
- deactivation
- consent
- theme/accessibility preferences

==================================================
MILESTONE 18 — ADMIN, PLATFORM OPERATIONS, FEATURE FLAGS, EXPERIMENTATION
==========================================================================

Implement authorized administrative and internal-product interfaces.

These interfaces must never be accessible to ordinary users.

==================================================
18.1 ADMIN APPLICATION SHELL
============================

Create a dedicated admin layout where required.

Support:

- admin navigation
- global search
- alerts
- account menu
- breadcrumbs
- responsive behavior

==================================================
18.2 ADMIN AUTHORIZATION
========================

Require backend-validated:

- authenticated admin session
- role
- permission
- resource scope

Never rely on client-hidden routes as security.

==================================================
18.3 ADMIN DASHBOARD
====================

Render backend-provided operational summaries.

Possible sections:

- platform health
- moderation
- reports
- users
- content
- rights
- advertising
- commerce
- feature flags
- system alerts

Do not build operational metrics independently from the backend's authoritative sources.

==================================================
18.4 USER ADMINISTRATION
========================

Support authorized workflows such as:

- search users
- inspect safe account metadata
- view status
- view enforcement state
- suspend where authorized
- restore where authorized

Do not expose passwords, tokens, secrets, or unnecessarily sensitive information.

==================================================
18.5 CONTENT ADMINISTRATION
===========================

Support authorized:

- search content
- inspect content metadata
- view moderation state
- view reports
- remove/restrict/restore when permitted

==================================================
18.6 MODERATION QUEUES
======================

Build advanced moderation queue UI.

Support:

- filters
- priority
- status
- assigned reviewer
- target type
- date
- sorting
- cursor pagination

==================================================
18.7 MODERATION CASE WORKSPACE
==============================

Create a focused case-review workspace.

Display:

- target
- report summary
- history
- current state
- appeal state
- available actions

Actions must be backend-authorized.

==================================================
18.8 AUDIT LOG
==============

Build audit-log viewer.

Support:

- actor
- action
- target
- timestamp
- request/correlation ID where safe
- filters
- pagination

Do not allow arbitrary deletion or mutation of audit records through frontend UI.

==================================================
18.9 FEATURE FLAGS
==================

Build feature-flag management UI where backend supports it.

Support:

- flag list
- status
- rollout
- environments
- targeting
- variants
- change history

Do not expose internal feature flags to unauthorized users.

==================================================
18.10 FEATURE FLAG SAFETY
=========================

Before rendering a privileged feature-control UI:

- verify permissions
- load current configuration
- show stale/unknown state distinctly

Do not accidentally default dangerous administrative features to enabled.

==================================================
18.11 DYNAMIC CONFIGURATION
===========================

Where backend supports dynamic configuration:

- inspect config
- modify allowed values
- validate
- publish
- rollback where supported

Never allow arbitrary script execution or unrestricted configuration mutation.

==================================================
18.12 EXPERIMENT MANAGEMENT
===========================

Build experimentation interface where backend supports:

- experiment
- variant
- allocation
- targeting
- start/end
- status
- metrics reference

The frontend only configures experiments.

It does not calculate experiment significance itself unless explicitly supported.

==================================================
18.13 EXPERIMENT SAFETY
=======================

Support:

- draft
- validation
- active
- paused
- completed
- archived

Require backend confirmation before status changes.

==================================================
18.14 ADMIN TABLE SYSTEM
========================

Create reusable administrative table capabilities:

- filters
- sorting
- pagination
- column control
- row actions
- bulk actions only where backend supports them
- loading
- error
- empty

==================================================
18.15 ADMIN SEARCH
==================

Create global admin search where backend supports it.

Search may cover:

- users
- content
- reports
- cases
- campaigns
- products
- orders

Use debounced search and backend pagination.

==================================================
18.16 ADMIN AUDIT UX
====================

Every destructive administrative action should:

- show target
- describe impact
- request confirmation where appropriate
- submit through authorized API
- show result
- reconcile cache
- leave audit trail through backend

==================================================
18.17 ADMIN TESTING
===================

Test:

- admin access
- forbidden user
- role restrictions
- moderation
- user actions
- content actions
- audit log
- feature flags
- configuration
- experiments
- table pagination
- destructive-action confirmation

==================================================
MILESTONE 19 — GLOBAL UX, PUBLIC SURFACES, SEO, SHARING, INSTALLABILITY
========================================================================

Complete public-facing and platform-wide UX integration.

==================================================
19.1 PUBLIC LANDING EXPERIENCE
==============================

Build a polished public landing experience appropriate to the application's product.

Support:

- responsive layout
- authentication entry points
- public content discovery where permitted
- SEO metadata

Do not expose private user content.

==================================================
19.2 PUBLIC PROFILE EXPERIENCE
==============================

Ensure public profiles can be rendered effectively for non-authenticated visitors where backend permits.

Support:

- avatar
- username
- display name
- bio
- public content
- counts
- links
- follow CTA where authentication is required

==================================================
19.3 AUTHENTICATION REDIRECTS
=============================

When an unauthenticated user attempts an action such as:

- follow
- comment
- like
- save
- message

redirect them through the intended authentication flow while preserving the intended post-login destination where safe.

Do not preserve unsafe arbitrary redirect URLs.

==================================================
19.4 DEEP LINKS
===============

Support deep links for:

- profile
- post
- reel
- story where technically appropriate
- hashtag
- audio
- conversation
- product
- campaign/admin routes when authorized

Ensure invalid/deleted resources show appropriate states.

==================================================
19.5 SHAREABLE URLs
===================

Create stable canonical URLs for public resources.

Support:

- copy link
- native sharing
- social sharing metadata where appropriate

Never include private identifiers or sensitive query parameters unnecessarily.

==================================================
19.6 OPEN GRAPH
===============

Implement dynamic metadata for public resources:

- profile
- post
- reel
- public product
- public landing pages

Do not generate metadata that leaks:

- private captions
- private media
- private account information
- private engagement information

==================================================
19.7 SEO
========

Finalize:

- metadata
- canonical
- robots
- sitemap integration hooks
- structured metadata where appropriate
- public route indexing controls

The backend/infrastructure layer remains authoritative for final deployment-level indexing behavior.

==================================================
19.8 PUBLIC CONTENT FALLBACK
============================

If crawlers or unauthenticated users cannot access client-side content:

- provide server-rendered metadata/content where backend allows
- gracefully degrade where JavaScript is unavailable

Do not compromise privacy for SEO.

==================================================
19.9 INTERNATIONALIZATION FOUNDATION
====================================

Prepare architecture for internationalization.

Support:

- locale abstraction
- date formatting
- number formatting
- pluralization-ready strings
- text direction awareness
- timezone-aware presentation

Do not translate the entire application unless localization resources are provided.

Do not hard-code locale-specific formatting in components.

==================================================
19.10 RTL READINESS
===================

Ensure major layouts can support right-to-left languages.

Avoid manually reversed positioning logic where CSS logical properties solve it.

==================================================
19.11 DATE/TIME FORMATTING
==========================

Create centralized date/time formatting utilities.

Support:

- relative time
- absolute date
- timezone-aware values
- locale-aware output

Do not calculate server-authoritative scheduling state using local browser time.

==================================================
19.12 NUMBER FORMATTING
=======================

Create centralized formatting for:

- followers
- likes
- views
- currency
- percentages
- counts

Do not lose precision in financial values.

==================================================
19.13 PWA / INSTALLABILITY
==========================

Where supported by the product architecture:

- manifest
- app icons
- installability
- standalone behavior
- splash configuration
- offline shell where appropriate

Do not pretend the application is fully offline-capable unless offline functionality is actually implemented.

==================================================
19.14 OFFLINE EXPERIENCE
========================

For supported browser scenarios:

- show network status
- preserve unsent message where safe
- preserve upload recovery state where safe
- allow retry

Do not claim that an action completed while disconnected.

==================================================
19.15 INSTALL/DEVICE UX
=======================

Where PWA support exists, make install prompts:

- contextual
- dismissible
- non-repetitive
- accessible

==================================================
19.16 PUBLIC PERFORMANCE
========================

Optimize public pages for:

- fast initial render
- minimal JavaScript
- server rendering
- efficient images
- stable layout
- good metadata

==================================================
19.17 SHARING TESTS
===================

Test:

- public profile deep link
- post deep link
- reel deep link
- hashtag link
- audio link
- product link
- auth redirect
- copy link
- metadata
- not-found
- private-resource behavior

==================================================
MILESTONE 20 — FINAL FRONTEND HARDENING AND RELEASE READINESS
==============================================================

Perform a repository-wide frontend engineering audit.

Do not rewrite the application simply for stylistic consistency.

Identify real defects and fix them.

==================================================
20.1 COMPLETE TYPE SAFETY AUDIT
===============================

Run full TypeScript validation.

Fix:

- implicit any
- unsafe any
- invalid type assertions
- unreachable branches
- null/undefined errors
- incompatible API contracts

Do not weaken TypeScript settings merely to make the build pass.

==================================================
20.2 LINT AUDIT
===============

Run the repository's linting system.

Fix:

- hooks violations
- exhaustive dependency problems
- unused imports
- accessibility problems
- unsafe patterns
- inconsistent conventions

Do not disable lint rules without justification.

==================================================
20.3 BUILD AUDIT
================

Run production build.

Resolve:

- Server/Client Component conflicts
- hydration errors
- dynamic rendering issues
- missing environment variables
- invalid route configurations
- bundle failures
- metadata errors

==================================================
20.4 HYDRATION AUDIT
====================

Identify and fix:

- hydration mismatches
- browser-only API usage during server render
- nondeterministic rendering
- date/time mismatches
- random values during render

Use client effects/browser guards appropriately.

==================================================
20.5 PERFORMANCE AUDIT
======================

Inspect:

- JavaScript bundle size
- hydration cost
- unnecessary client components
- image delivery
- media loading
- query waterfalls
- duplicate requests
- rerender frequency
- memory usage

Optimize high-impact issues.

==================================================
20.6 FEED PERFORMANCE
=====================

Verify:

- large feed scrolling
- media loading
- optimistic mutations
- cache updates
- background refetching
- no duplicate requests
- no memory leaks

==================================================
20.7 REELS PERFORMANCE
======================

Verify:

- only intended videos autoplay
- inactive players pause
- nearby preloading is bounded
- scroll remains smooth
- playback events are throttled/batched
- resources are released

==================================================
20.8 MESSAGING PERFORMANCE
==========================

Verify:

- large conversations
- pagination
- scroll anchoring
- new-message insertion
- typing updates
- presence updates
- reactions
- attachment previews

No whole-page rerender should occur for a single message event unless architecture requires it.

==================================================
20.9 REALTIME STABILITY
=======================

Test:

- reconnect
- duplicate events
- authentication expiration
- logout
- tab backgrounding
- network changes
- rapid reconnect cycles

Prevent connection storms.

==================================================
20.10 QUERY CACHE AUDIT
=======================

Review every major query.

Verify:

- stable query keys
- correct stale behavior
- correct garbage collection
- targeted invalidation
- optimistic rollback
- no sensitive cache retention after logout

==================================================
20.11 MEMORY LEAK AUDIT
=======================

Search for uncleaned:

- event listeners
- timers
- intervals
- subscriptions
- sockets
- observers
- media resources
- object URLs

Every effect must clean up appropriate resources.

==================================================
20.12 ACCESSIBILITY AUDIT
=========================

Perform a complete accessibility pass.

Check:

- keyboard navigation
- focus management
- dialogs
- drawers
- dropdowns
- menus
- carousels
- media controls
- forms
- errors
- live regions
- contrast
- reduced motion

Fix actual accessibility defects.

==================================================
20.13 SCREEN READER UX
======================

Verify meaningful announcements for:

- loading
- success
- errors
- like state
- follow state
- new messages
- notifications
- modal opening
- pagination completion

Avoid excessive announcements.

==================================================
20.14 KEYBOARD AUDIT
====================

Verify complete workflows can be performed without a mouse.

Important workflows:

- authentication
- navigation
- search
- feed interaction
- comments
- stories
- reels
- messaging
- creation
- settings
- reports

==================================================
20.15 SECURITY AUDIT
====================

Review:

- XSS
- unsafe HTML
- URL handling
- redirects
- token exposure
- sensitive local storage
- analytics leakage
- privileged routes
- admin access
- file uploads
- iframe behavior where applicable
- third-party scripts

==================================================
20.16 CONTENT SECURITY POLICY READINESS
=======================================

Ensure frontend architecture can operate with a strong Content Security Policy.

Avoid unnecessary:

- inline scripts
- arbitrary HTML injection
- dynamic script URLs
- unsafe evaluation

Actual deployment headers belong to infrastructure, but frontend code must not rely on unsafe browser behaviors unnecessarily.

==================================================
20.17 OBSERVABILITY AUDIT
=========================

Ensure frontend error monitoring captures:

- route
- feature
- safe user/session context
- correlation/request ID where available
- error category

Never send secrets or private message contents.

==================================================
20.18 ANALYTICS AUDIT
=====================

Review every analytics event.

Verify:

- stable event name
- schema
- privacy
- no sensitive payloads
- no duplicate emission
- appropriate throttling
- consent enforcement where applicable

==================================================
20.19 SEO AUDIT
===============

Verify:

- title
- description
- canonical
- robots
- Open Graph
- public profile metadata
- public content metadata
- no private content leakage
- invalid resource behavior

==================================================
20.20 RESPONSIVE AUDIT
======================

Validate major application areas at:

- narrow mobile
- standard mobile
- tablet
- laptop
- desktop
- large desktop

Verify:

- no horizontal overflow
- readable text
- usable touch targets
- stable media
- appropriate navigation

==================================================
20.21 ERROR RESILIENCE
======================

Every major feature must gracefully handle:

- network error
- timeout
- server error
- authorization failure
- rate limit
- not found
- deleted resource
- private resource
- stale state
- conflict

Provide retry/recovery where appropriate.

==================================================
20.22 DATA RACE AUDIT
=====================

Test races such as:

- follow then unfollow rapidly
- like then unlike rapidly
- send message while reconnecting
- upload then cancel
- publish while session expires
- profile update from two tabs
- settings changed in another tab
- moderation case updated while open

Use server reconciliation.

==================================================
20.23 MULTI-TAB BEHAVIOR
========================

Where appropriate, synchronize:

- authentication
- logout
- theme
- settings
- unread counts

Use browser-supported mechanisms where appropriate.

Do not introduce unnecessary cross-tab complexity.

==================================================
20.24 BROWSER COMPATIBILITY
===========================

Verify important functionality across current major browsers supported by the project.

Gracefully degrade unsupported capabilities such as:

- Web Share
- notifications
- certain media APIs
- PWA installation

==================================================
20.25 TEST SUITE COMPLETION
===========================

Complete frontend test coverage across:

Unit tests:

- utilities
- permissions
- formatting
- validation
- cache helpers

Component tests:

- buttons
- forms
- dialogs
- post cards
- stories
- reels
- comments
- notifications
- messaging
- creation
- analytics
- commerce
- admin

Integration tests:

- API clients
- query behavior
- mutation behavior
- realtime cache synchronization
- upload management

End-to-end tests:

- registration
- login
- profile
- follow
- feed
- post engagement
- stories
- reels
- search
- notifications
- messages
- creation
- creator dashboard
- advertising
- commerce
- reporting
- settings
- privacy
- logout

==================================================
20.26 ACCESSIBILITY TEST SUITE
==============================

Automate accessibility testing where practical.

Catch:

- missing labels
- invalid ARIA
- contrast violations
- focus problems
- duplicate IDs
- inaccessible controls

Do not rely solely on automated testing.

==================================================
20.27 VISUAL REGRESSION READINESS
=================================

Structure critical components so they can be tested for visual regressions.

Prioritize:

- application shell
- navigation
- post card
- carousel
- story viewer
- reel player
- messaging
- composer
- dashboard
- dialogs

==================================================
20.28 FINAL DEPENDENCY AUDIT
============================

Review dependencies.

Identify:

- unused dependencies
- duplicate packages
- unnecessary libraries
- outdated imports
- direct imports that violate architecture

Do not upgrade packages casually.

==================================================
20.29 ENVIRONMENT AUDIT
=======================

Verify frontend configuration includes all required environment variables.

Separate:

- public configuration
- server-only configuration

Never expose secrets through NEXT_PUBLIC_* or equivalent public environment configuration.

==================================================
20.30 DOCUMENTATION
===================

Update final documentation:

- frontend architecture
- routing map
- feature map
- component system
- API integration
- authentication
- realtime
- uploads
- analytics
- feature flags
- localization readiness
- accessibility
- testing
- environment configuration
- troubleshooting
- production build
- release checklist

Documentation must match actual repository behavior.

==================================================
FRONTEND PROJECT INDEX
======================

Create a final frontend index mapping:

Feature
→ Route
→ Components
→ Hooks
→ Queries
→ Mutations
→ Stores
→ API endpoints
→ Realtime events
→ Analytics events
→ Permissions
→ Tests

The index must be understandable by another senior frontend engineer without requiring repository archaeology.

==================================================
ARCHITECTURAL CONSISTENCY AUDIT
===============================

Verify:

- no duplicate API clients
- no duplicate auth providers
- no duplicate realtime managers
- no duplicate query clients
- no duplicate upload managers
- no duplicated design tokens
- no duplicated permission abstractions
- no duplicated formatting utilities
- no feature-specific server-state stores where TanStack Query should be used
- no business logic embedded into low-level UI primitives

==================================================
FINAL UX CONSISTENCY
====================

All application surfaces must share consistent:

- typography
- spacing
- buttons
- menus
- dialogs
- form behavior
- loading states
- errors
- empty states
- responsive rules
- interaction feedback

Do not allow administrative or professional sections to accidentally use incompatible interaction patterns.

==================================================
FINAL PRODUCTION QUALITY BAR
============================

The frontend must be:

- production-grade
- type-safe
- accessible
- responsive
- performant
- secure
- observable
- testable
- maintainable
- responsive to backend state
- resilient to failure
- consistent across domains

No broken routes.

No placeholder screens.

No fake production data.

No TODOs.

No dead feature paths.

No unnecessary duplicate abstractions.

==================================================
IMPLEMENTATION ORDER
====================

Execute exactly in this order:

MILESTONE 17

1. Advanced settings
2. Account center
3. Privacy
4. Interaction controls
5. Blocked/restricted/close friends
6. Session/security
7. Data export
8. Account deletion/deactivation
9. Consent/preferences
10. Accessibility/appearance preferences
11. Tests

MILESTONE 18

1. Admin shell
2. Authorization
3. Dashboard
4. User administration
5. Content administration
6. Moderation queues
7. Case workspace
8. Audit logs
9. Feature flags
10. Dynamic configuration
11. Experiments
12. Admin testing

MILESTONE 19

1. Public landing
2. Public profiles
3. Authentication redirects
4. Deep links
5. Sharing
6. Metadata
7. SEO
8. Internationalization foundation
9. RTL readiness
10. PWA/installability where supported
11. Offline UX
12. Public performance
13. Tests

MILESTONE 20

1. Type audit
2. Lint audit
3. Build audit
4. Hydration audit
5. Performance audit
6. Realtime audit
7. Query cache audit
8. Memory audit
9. Accessibility audit
10. Security audit
11. Observability audit
12. Analytics audit
13. SEO audit
14. Responsive audit
15. Data-race audit
16. Browser compatibility
17. Test-suite completion
18. Visual regression readiness
19. Dependency audit
20. Environment audit
21. Documentation
22. Final project index
23. Final production validation

==================================================
OUTPUT FORMAT
=============

Before modifying files:

1. Inspect the current repository.
2. Determine which frontend volumes are already implemented.
3. Reuse existing architecture.
4. Identify actual gaps.
5. Verify existing backend contracts.
6. Do not rewrite working functionality unnecessarily.

For every implementation step:

1. State the current milestone.
2. State the affected feature/domain.
3. Briefly explain important architectural decisions.
4. Create or modify only required files.
5. Output complete contents for every changed/new file.
6. Never output unchanged files.
7. Add tests with the implementation.
8. Run typecheck.
9. Run lint.
10. Run tests.
11. Run production build.
12. Fix discovered issues.
13. Leave the repository in a valid buildable state.

If a validation command does not exist, identify the nearest repository-supported equivalent.

Do not merely describe changes.

Actually implement them.

==================================================
FINAL ACCEPTANCE CRITERIA
=========================

At the end of this volume:

ACCOUNT AND PRIVACY

- settings are complete;
- privacy controls work;
- security settings work;
- session management works;
- blocked/restricted/close-friends management works;
- data export works where supported;
- deletion/deactivation workflows work where supported;
- consent/preferences are respected;
- appearance/accessibility preferences work.

ADMINISTRATION

- admin routes are protected;
- moderation interfaces work;
- audit logs work;
- feature flags work where supported;
- configuration management works where supported;
- experimentation management works where supported.

PUBLIC PLATFORM

- public profiles work;
- public content sharing works;
- deep links work;
- SEO metadata works;
- private content remains private;
- public pages perform well;
- localization foundations exist;
- RTL readiness exists;
- PWA behavior works where supported.

HARDENING

- TypeScript passes;
- lint passes;
- tests pass;
- production build passes;
- accessibility audit passes at the intended quality level;
- security audit issues are resolved;
- realtime is stable;
- cache behavior is correct;
- memory leaks are addressed;
- responsive behavior is validated;
- major browser capabilities degrade gracefully;
- documentation matches implementation.

==================================================
CRITICAL FINAL RULE
===================

Do not move into infrastructure implementation.

The frontend implementation is considered complete only after all four milestones in this volume are implemented, tested, integrated, and validated.

The next project phase after this is the INFRASTRUCTURE / DEVOPS implementation, which must consume the final frontend and backend contracts established by all previous volumes.

BEGIN WITH:

MILESTONE 17 — ADVANCED ACCOUNT, PRIVACY, SECURITY, DATA, AND CONSENT MANAGEMENT.
