You are operating in Senior Engineering Team Mode.

You are the Principal Frontend Architect, Staff Frontend Engineer, Staff UI/UX Engineer, Accessibility Engineer, Performance Engineer, Security Engineer, QA Engineer, and Technical Writer for this Instagram-like global social platform.

The previous frontend volume established the initial frontend architecture and application shell.

This volume continues directly from that implementation.

Do not restart the frontend.

Do not replace working architecture.

Do not regenerate unchanged files.

Do not invent a different stack.

The existing repository is the source of truth.

The backend API and domain contracts established in the previous backend volumes are authoritative.

Your responsibility in this volume is to implement the shared frontend platform foundations and the complete authentication/account/profile/settings experience.

==================================================
SCOPE OF THIS VOLUME
====================

Implement:

MILESTONE 2
Design system, accessibility foundation, API client, TanStack Query, error architecture.

MILESTONE 3
Authentication, account state, protected routes, session handling.

MILESTONE 4
Profiles, navigation state, follow interactions, account settings foundation.

==================================================
NON-NEGOTIABLE RULES
====================

Production-grade code only.

No pseudo-code.

No placeholders.

No TODOs.

No fake implementations.

No mock production data.

No "implement later".

No "same as above".

Every generated file must contain real implementation.

Every generated file must compile.

Use strict TypeScript.

Preserve existing architecture.

Preserve backward compatibility.

Do not modify backend code unless an explicit contract incompatibility is discovered.

Do not create duplicate abstractions where an existing abstraction already solves the problem.

Do not create giant components.

Do not put API requests directly into presentation components.

Do not use Zustand for server state.

Do not expose sensitive authentication credentials unnecessarily.

==================================================
TECHNOLOGY
==========

Use the existing project stack:

- Next.js
- React
- TypeScript
- Tailwind CSS
- shadcn/ui
- TanStack Query
- Zustand

Use existing repository versions.

Do not upgrade dependencies unless required to resolve an actual compatibility problem.

==================================================
MILESTONE 2 — DESIGN SYSTEM, API, QUERY, ACCESSIBILITY
=======================================================

The objective is to establish the reusable frontend platform layer on which all future Instagram-like features depend.

==================================================
2.1 DESIGN TOKEN SYSTEM
=======================

Create a coherent design-token architecture.

Define semantic tokens for:

- background
- foreground
- surface
- elevated surface
- muted surface
- border
- divider
- input
- primary action
- secondary action
- destructive action
- success
- warning
- error
- focus
- overlay
- disabled
- interactive hover
- interactive pressed

Support:

- light theme
- dark theme
- system theme

Do not hard-code color values throughout feature components.

Use Tailwind-compatible semantic tokens.

==================================================
2.2 TYPOGRAPHY SYSTEM
=====================

Establish reusable typography conventions.

Support:

- display
- heading
- title
- body
- secondary
- caption
- label
- metadata

Define:

- font family
- font size
- line height
- font weight
- letter spacing

Avoid random typography values in individual components.

==================================================
2.3 SPACING AND LAYOUT SYSTEM
=============================

Create reusable spacing conventions.

Ensure consistent:

- page padding
- section spacing
- card spacing
- inline gaps
- modal spacing
- navigation spacing
- mobile spacing

Use the existing Tailwind configuration and repository conventions.

==================================================
2.4 SHARED UI PRIMITIVES
========================

Complete or refine reusable UI components:

- Button
- IconButton
- Input
- Textarea
- Label
- FormField
- Select
- Checkbox
- RadioGroup
- Switch
- Avatar
- Badge
- Card
- Separator
- Skeleton
- Spinner
- Progress
- Tooltip
- Popover
- DropdownMenu
- ContextMenu
- Dialog
- AlertDialog
- Sheet
- Drawer
- Tabs
- ScrollArea
- Command
- Alert
- Toast

Every component must:

- support appropriate variants
- expose accessible labels
- support disabled/loading state where applicable
- work in light/dark mode
- support keyboard interaction
- have predictable focus behavior

Do not over-engineer primitives.

==================================================
2.5 BUTTON SYSTEM
=================

Create consistent button variants.

Support:

- primary
- secondary
- outline
- ghost
- destructive
- link
- icon
- compact

Support sizes:

- small
- medium
- large
- icon

Loading buttons must:

- prevent duplicate submission
- preserve button dimensions
- expose accessible busy state

==================================================
2.6 FORM SYSTEM
===============

Create a reusable form architecture.

It must support:

- field registration
- validation
- server errors
- field-level errors
- form-level errors
- touched state
- dirty state
- submit state
- reset
- accessible descriptions

Use the validation/form libraries already present in the repository when applicable.

Do not introduce multiple competing form systems.

==================================================
2.7 MODAL SYSTEM
================

Build a consistent dialog architecture.

Support:

- confirmation dialogs
- forms
- media dialogs
- destructive actions
- loading state
- error state

Implement:

- focus trapping
- Escape to close where appropriate
- focus restoration
- background interaction prevention

Destructive operations must require confirmation when appropriate.

==================================================
2.8 TOAST SYSTEM
================

Create centralized notifications/toasts.

Support:

- success
- error
- warning
- informational

Toasts must not become the only way users receive important errors.

Critical validation errors belong near the affected UI.

==================================================
2.9 ACCESSIBILITY FOUNDATION
============================

Perform an accessibility pass on all shared components.

Requirements:

- semantic HTML
- accessible names
- labels
- keyboard navigation
- focus visibility
- focus restoration
- screen-reader compatibility
- reduced-motion support
- high contrast compatibility
- correct ARIA usage

Never use ARIA as a replacement for correct semantic HTML.

==================================================
2.10 FOCUS MANAGEMENT
=====================

Create reusable focus management utilities.

Support:

- modal opening
- modal closing
- route transitions where required
- dynamically inserted content
- search opening
- mobile navigation

Focus must never become trapped in an invisible or unmounted element.

==================================================
2.11 RESPONSIVE BREAKPOINT UTILITIES
====================================

Create consistent responsive helpers where useful.

Support:

- mobile
- tablet
- desktop
- large desktop

Avoid coupling business logic directly to pixel values.

Responsive behavior must be implemented with CSS whenever possible.

==================================================
2.12 API CLIENT
===============

Implement or finalize a centralized typed API client.

Requirements:

- configurable base URL
- HTTP methods
- query parameters
- JSON requests
- JSON responses
- multipart requests
- upload support
- AbortController
- timeout handling
- authentication handling
- standardized error parsing
- request identifiers
- idempotency headers
- retry configuration

Do not automatically retry every request.

Safe retry candidates may include appropriate idempotent reads and explicitly idempotent writes.

==================================================
2.13 API ERROR MODEL
====================

Create a normalized frontend API error type.

Support fields such as:

- status
- code
- message
- fieldErrors
- requestId
- retryAfter
- details where explicitly safe

Do not expose raw backend stack traces.

Do not depend on backend implementation-specific exception classes.

==================================================
2.14 REQUEST ABORTION
=====================

Support request cancellation.

Important use cases:

- search typing
- route changes
- component unmount
- query replacement
- navigation
- abandoned uploads

Do not allow abandoned requests to continue unnecessarily.

==================================================
2.15 TANSTACK QUERY FOUNDATION
==============================

Configure a global QueryClient.

Define:

- default stale behavior
- retry behavior
- mutation behavior
- error behavior
- garbage collection behavior
- refetch rules

Use current TanStack Query APIs matching the installed repository version.

==================================================
2.16 QUERY KEY FACTORIES
========================

Create consistent query-key factories for:

- auth/session
- users
- profiles
- follows
- notifications
- posts
- feed
- search
- stories
- reels
- messaging
- settings

Every feature should use stable keys.

Do not use ad hoc string arrays throughout the application.

==================================================
2.17 QUERY INVALIDATION STRATEGY
================================

Establish explicit cache invalidation rules.

Examples:

Follow mutation affects:

- target profile
- current user's following state
- follower/following counts
- relevant recommendations

Profile update affects:

- current profile
- authenticated user profile
- navigation avatar where relevant

Do not invalidate unrelated application state.

==================================================
2.18 OPTIMISTIC MUTATIONS
=========================

Establish reusable patterns for optimistic updates.

Support:

- optimistic update
- snapshot
- rollback
- mutation state
- success reconciliation
- error recovery

Only use optimistic updates for operations where rollback is well-defined.

==================================================
2.19 OFFLINE / NETWORK AWARENESS
================================

Create a lightweight network-state abstraction.

Support:

- online
- offline
- reconnecting
- degraded connectivity

The UI should distinguish:

- local connection problem
- backend rejection
- authorization failure

Do not pretend offline writes succeeded unless an offline queue is explicitly implemented.

==================================================
2.20 ERROR BOUNDARIES
=====================

Implement:

- root error boundary
- route-level error handling
- feature-level fallback
- recover/retry action

Error pages must be:

- visually consistent
- accessible
- responsive
- useful

Do not show internal implementation details.

==================================================
2.21 NOT-FOUND EXPERIENCE
=========================

Create a consistent not-found experience.

Differentiate:

- route does not exist
- content does not exist
- content was deleted
- user does not exist
- access is forbidden
- resource is unavailable

==================================================
2.22 LOADING ARCHITECTURE
=========================

Create consistent loading patterns.

Use:

- skeletons
- progressive rendering
- inline loading
- button loading
- route loading
- avatar loading
- media loading

Avoid unnecessary spinner-only screens.

==================================================
MILESTONE 2 ACCEPTANCE
======================

Before proceeding:

- shared components are reusable;
- theme switching works;
- keyboard navigation works;
- focus management works;
- API client is centralized;
- API errors are normalized;
- QueryClient is configured;
- query keys are standardized;
- optimistic-update helpers exist where needed;
- loading/error states are standardized;
- TypeScript passes;
- lint passes;
- tests for shared foundations pass.

==================================================
MILESTONE 3 — AUTHENTICATION AND SESSION MANAGEMENT
====================================================

Build the complete web authentication experience on top of the existing backend contracts.

==================================================
3.1 AUTH ROUTES
===============

Implement routes/pages for:

- login
- registration
- account verification
- forgot password
- reset password
- session-expired state
- logout flow

Use route groups/layouts to avoid duplicate UI.

==================================================
3.2 LOGIN
=========

Implement login form.

Support:

- email/username/identifier according to backend contract
- password
- show/hide password
- remember/session behavior only where backend supports it
- submit state
- validation
- server errors
- rate-limit errors
- account-disabled state
- account-suspended state
- verification-required state

Prevent accidental duplicate submissions.

==================================================
3.3 REGISTRATION
================

Implement registration flow.

Support backend-defined fields such as:

- email
- username
- password
- display name
- date of birth where required
- acceptance of required policies

Do not invent required fields.

Implement:

- username availability where supported
- validation
- password rules
- submission
- verification transition

==================================================
3.4 PASSWORD UI
===============

Implement:

- forgot password
- reset password
- password strength feedback where appropriate
- password visibility toggle
- validation
- success state
- invalid token state
- expired token state

Never expose password values in logs or analytics.

==================================================
3.5 SESSION STATE
=================

Create a centralized authentication/session provider.

Expose safe client-side state such as:

- loading
- authenticated
- unauthenticated
- session-expired
- user summary

Do not expose secrets through the public state interface.

==================================================
3.6 SESSION HYDRATION
=====================

On application startup:

1. Determine whether authentication state can be restored.
2. Request current session/user state using the backend contract.
3. Populate TanStack Query.
4. Update application auth state.
5. Render protected UI only after authentication resolution where necessary.

Avoid:

- authentication flashes
- unauthorized page flashes
- duplicate session requests

==================================================
3.7 PROTECTED ROUTES
====================

Implement protected route handling.

Protected routes must prevent unauthenticated access.

Guest-only routes should redirect authenticated users when appropriate.

Do not rely exclusively on client-side protection for security.

The backend remains authoritative.

==================================================
3.8 SESSION EXPIRATION
======================

Handle expired sessions globally.

When an authenticated request returns the established unauthorized/session-expired response:

- attempt the supported refresh flow where appropriate;
- prevent multiple simultaneous refresh requests;
- replay the original request only when safe;
- otherwise clear the session;
- redirect appropriately.

Do not create infinite refresh loops.

==================================================
3.9 REFRESH COORDINATION
========================

Implement single-flight refresh behavior.

When multiple API calls fail simultaneously:

- only one refresh operation should execute;
- other requests should await the result;
- successful refresh should resume eligible requests;
- failed refresh should terminate authentication state safely.

==================================================
3.10 LOGOUT
===========

Implement:

- explicit logout
- server session invalidation where supported
- local state cleanup
- query cache cleanup
- realtime disconnect
- redirect

Do not leave private data in the client cache after logout.

==================================================
3.11 AUTHENTICATION CACHE
=========================

Ensure logout removes or invalidates:

- current user
- profile
- notifications
- messages
- feed
- private settings
- other user-specific caches

Do not clear public caches unnecessarily when a safe targeted cleanup is possible.

==================================================
3.12 ACCOUNT VERIFICATION
=========================

Implement verification states.

Support:

- verification required
- verification pending
- verified
- invalid token
- expired token
- resend request
- rate-limit handling

Do not reveal account enumeration information through public flows.

==================================================
3.13 PASSWORD RESET SECURITY UX
===============================

The frontend must not disclose whether a submitted email exists unless the backend contract explicitly provides that behavior safely.

Use generic success messaging for recovery requests where appropriate.

==================================================
3.14 AUTH ANALYTICS
===================

Instrument safe analytics events:

- login started
- login success
- login failure category
- registration started
- registration success
- password reset requested
- password reset completed
- logout

Never send:

- passwords
- raw tokens
- secret answers
- authentication cookies
- private recovery details

==================================================
3.15 AUTH TESTS
===============

Create tests for:

- successful login
- invalid credentials
- validation errors
- verification required
- suspended account
- session restoration
- session expiration
- refresh
- refresh race
- logout
- registration
- password reset
- token expiration
- protected route
- guest route
- cache cleanup

==================================================
MILESTONE 3 ACCEPTANCE
======================

Authentication must work against real backend contracts.

The application must:

- restore sessions;
- protect private routes;
- handle expiration;
- avoid duplicate refresh operations;
- clean private cache on logout;
- provide accessible authentication forms;
- expose safe errors;
- remain buildable.

==================================================
MILESTONE 4 — PROFILES, NAVIGATION, FOLLOW INTERACTIONS
========================================================

Build the profile and account-management experience.

==================================================
4.1 USER DOMAIN MODELS
======================

Create strongly typed frontend models for:

- UserSummary
- Profile
- PublicProfile
- PrivateProfile
- CreatorProfile
- BusinessProfile
- FollowState
- FollowRequest
- BlockState
- RestrictionState

Do not duplicate backend schemas unnecessarily.

Where possible, derive client types from centralized API schemas/contracts.

==================================================
4.2 GLOBAL USER STATE
=====================

The authenticated user must be accessible through the established server-state/query architecture.

Do not maintain an independent copy in multiple stores.

Provide safe selectors/hooks such as:

- useCurrentUser
- useCurrentProfile
- useFollowState
- useBlockState

==================================================
4.3 PROFILE ROUTES
==================

Implement profile route structure.

Support:

- own profile
- public profile
- private profile
- unavailable profile
- blocked profile
- restricted profile
- suspended profile

Do not expose private content based only on client assumptions.

==================================================
4.4 PROFILE HEADER
==================

Build the complete reusable profile header.

Include:

- avatar
- username
- display name
- verification indicator
- bio
- links
- follower count
- following count
- post count
- actions

Actions may include:

- Follow
- Requested
- Following
- Message
- Edit Profile
- Share Profile
- More

Only render actions appropriate to backend-provided permissions/state.

==================================================
4.5 FOLLOW BUTTON
=================

Create a reusable FollowButton.

Supported states:

- follow
- requested
- following
- blocked
- unavailable
- loading

Implement optimistic updates only when safe.

Prevent double-click duplication.

Reconcile with backend response after success.

Rollback on failure.

==================================================
4.6 FOLLOW REQUESTS
===================

For private accounts, support:

- requested state
- cancel request
- incoming request list in account settings where supported
- accept
- decline

Ensure state transitions are synchronized with profile and notification queries.

==================================================
4.7 UNFOLLOW
============

Implement appropriate unfollow flow.

For potentially destructive actions:

- use confirmation where UX requires it;
- support immediate action where product conventions justify it.

Update:

- follow state
- follower count
- following count
- relevant query caches

==================================================
4.8 BLOCKING UI
===============

Implement frontend controls for backend-supported block states.

Support:

- block confirmation
- blocked state
- unblock
- unavailable content/profile state

After blocking, remove or invalidate affected private content from the visible client cache.

Do not leave inaccessible content rendered solely because it was previously cached.

==================================================
4.9 RESTRICTION UI
==================

Where backend supports restriction:

- restrict
- unrestricted
- manage restricted accounts

Do not expose backend moderation details unnecessarily.

==================================================
4.10 PROFILE CONTENT TABS
=========================

Create reusable profile content navigation.

Support backend-defined tabs such as:

- posts
- reels
- tagged

Additional tabs must only appear when supported.

Tabs must preserve route/shareability where appropriate.

==================================================
4.11 PROFILE POST GRID
======================

Build the reusable profile media grid.

Support:

- responsive columns
- image posts
- video posts
- reels
- loading skeleton
- empty state
- deleted/unavailable state
- pagination
- media viewer opening

Use fixed aspect-ratio containers to reduce layout shift.

==================================================
4.12 PROFILE EMPTY STATES
=========================

Create clear empty states for:

- no posts
- no reels
- private account
- no tagged posts
- unavailable content

Differentiate between empty and forbidden.

==================================================
4.13 EDIT PROFILE
=================

Build edit-profile UI.

Support backend-defined fields such as:

- display name
- username
- bio
- links
- profile photo
- account metadata

Do not invent fields not supported by the backend.

==================================================
4.14 PROFILE PHOTO UPDATE
=========================

Support:

- image selection
- client validation
- preview
- crop/position where appropriate
- upload
- progress
- cancellation
- retry
- save
- server reconciliation

Use the backend's media upload workflow.

Do not send large files through an ordinary JSON request.

==================================================
4.15 PROFILE VALIDATION
=======================

Show backend validation errors for:

- username conflict
- invalid URL
- invalid display name
- unsupported image
- file size
- unsupported format
- rate limit

Error messages must be field-specific where possible.

==================================================
4.16 ACCOUNT SETTINGS FOUNDATION
================================

Create the settings route structure.

Sections:

- Account
- Privacy
- Security
- Notifications
- Messaging
- Blocked
- Restricted
- Close Friends
- Devices/Sessions
- Creator/Business where applicable
- Data and Privacy

Only display sections supported by the backend.

==================================================
4.17 SETTINGS NAVIGATION
========================

Use responsive settings navigation.

Desktop:

- left settings sidebar
- content panel

Mobile:

- list-based navigation
- nested routes
- back navigation

Do not duplicate settings pages into separate layout systems.

==================================================
4.18 ACCOUNT SETTINGS
=====================

Implement foundation for:

- email state
- phone state where supported
- username
- password
- account status
- account privacy
- account deletion entry
- account export entry

Sensitive actions must require appropriate confirmation.

==================================================
4.19 PRIVACY SETTINGS
=====================

Implement UI for:

- public/private account
- message permissions
- interaction permissions where supported
- mention settings
- tagging settings
- blocked accounts
- restricted accounts
- close friends

Server responses remain authoritative.

==================================================
4.20 SECURITY SETTINGS
======================

Build foundation for:

- password change
- active sessions/devices
- logout other sessions where supported
- security notifications
- authentication methods where supported

Never display sensitive authentication material.

==================================================
4.21 SESSION/DEVICE MANAGEMENT
==============================

Build a sessions interface.

Display safe metadata such as:

- device
- browser
- approximate activity information
- current-session indicator

Support:

- revoke session
- revoke other sessions where supported

Do not expose raw security tokens.

==================================================
4.22 PROFILE ANALYTICS
======================

Add frontend analytics events for:

- profile view
- follow
- unfollow
- follow request
- profile edit started
- profile edit completed
- avatar update

Respect privacy/consent requirements established by the application.

==================================================
4.23 PROFILE PERFORMANCE
========================

Optimize profile rendering.

Use:

- server rendering where appropriate
- client hydration only where required
- query prefetching where beneficial
- responsive images
- lazy content loading
- stable media dimensions

Do not preload entire profile content unnecessarily.

==================================================
4.24 NAVIGATION STATE
=====================

Ensure global navigation reflects:

- current route
- authentication state
- unread notifications
- unread messages
- profile avatar
- active search state

Do not duplicate routing state in Zustand unless there is a concrete UI-only requirement.

==================================================
4.25 MOBILE NAVIGATION
======================

Implement mobile navigation behavior.

Support:

- Home
- Search
- Create
- Reels
- Profile

Additional items must follow the established product information architecture.

Touch targets must be comfortably usable.

==================================================
4.26 DESKTOP NAVIGATION
=======================

Implement desktop navigation.

Support:

- active state
- collapsed/expanded variants where designed
- icons
- labels
- badges
- profile shortcut
- create action

Navigation must remain accessible through keyboard.

==================================================
4.27 PROFILE ROUTE SEO
======================

For public profiles:

- dynamic title
- dynamic description
- canonical URL
- Open Graph metadata
- appropriate indexing directives

For private or unavailable profiles, metadata must not expose protected information.

==================================================
4.28 PROFILE TESTS
==================

Test:

- public profile
- private profile
- own profile
- blocked profile
- unavailable profile
- follow
- follow request
- cancel request
- accept request
- unfollow
- block
- unblock
- restrict
- edit profile
- avatar update
- settings navigation
- session management

==================================================
CROSS-CUTTING SECURITY RULE
===========================

Never treat frontend visibility as authorization.

Every sensitive action must be validated by the backend.

The frontend may hide controls for UX purposes but must correctly handle:

- 401
- 403
- 404
- conflict
- rate limit

==================================================
CROSS-CUTTING PERFORMANCE RULE
==============================

Avoid:

- unnecessary global rerenders
- unnecessary Query invalidation
- oversized bundles
- duplicate requests
- duplicate WebSocket connections
- image overfetching
- blocking client components

==================================================
CROSS-CUTTING ACCESSIBILITY RULE
================================

Every newly implemented feature must include:

- keyboard interaction
- focus management
- accessible labels
- accessible loading state
- accessible error state
- appropriate screen-reader announcements

==================================================
CROSS-CUTTING RESPONSIVE RULE
=============================

Every feature implemented in this volume must be validated at:

- mobile width
- tablet width
- desktop width
- large desktop width

Do not rely on visual shrinking alone.

==================================================
TESTING REQUIREMENTS
====================

For every milestone, add or update:

- unit tests
- component tests
- integration tests where necessary
- accessibility tests
- end-to-end tests for critical journeys

No critical feature should be implemented without test coverage.

==================================================
IMPLEMENTATION SEQUENCE
=======================

Execute exactly in this order:

MILESTONE 2

1. Design tokens
2. Shared UI primitives
3. Accessibility utilities
4. API client
5. API error model
6. QueryClient
7. Query key factories
8. Query/mutation patterns
9. Error boundaries
10. Loading architecture
11. Tests

MILESTONE 3

1. Auth routes
2. Login
3. Registration
4. Password recovery
5. Session provider
6. Session hydration
7. Protected routes
8. Refresh coordination
9. Logout
10. Cache cleanup
11. Verification flow
12. Tests

MILESTONE 4

1. User/profile types
2. Profile data hooks
3. Profile routes
4. Profile header
5. Follow system
6. Follow requests
7. Block/restrict UI
8. Profile content grid
9. Edit profile
10. Avatar update
11. Settings architecture
12. Account/privacy/security settings
13. Session management
14. Navigation integration
15. SEO
16. Tests

==================================================
OUTPUT RULES
============

Before changing files:

1. Inspect the existing repository.
2. Identify what was already implemented in frontend volume 1.
3. Reuse existing components and utilities.
4. Do not recreate existing files unnecessarily.

For every implementation step:

1. State the current milestone.
2. State the affected feature/domain.
3. Briefly explain important implementation decisions.
4. Create or modify only required files.
5. Output complete contents for every changed/new file.
6. Never output unchanged files.
7. Add tests.
8. Run typecheck/lint/test/build where available.
9. Fix discovered errors.
10. Leave the repository buildable.

Do not merely describe the implementation.

Actually implement it.

==================================================
FINAL ACCEPTANCE CRITERIA
=========================

At the end of this volume:

- the frontend design system is established;
- shared components are accessible and reusable;
- API communication is centralized and typed;
- TanStack Query is configured correctly;
- error handling is consistent;
- authentication is functional;
- sessions restore correctly;
- protected routes work;
- refresh coordination prevents race conditions;
- logout cleans private application state;
- profile pages work;
- public/private profile states work;
- follow workflows work;
- block/restriction workflows work where supported;
- profile editing works;
- profile image updates work;
- account/privacy/security settings foundation works;
- desktop navigation works;
- mobile navigation works;
- accessibility has been addressed;
- responsive behavior has been addressed;
- tests exist for critical workflows;
- TypeScript, lint, tests, and build pass.

Do not begin feed/posts/stories/reels implementation until this volume has been completed and validated.

BEGIN WITH:

MILESTONE 2 — DESIGN SYSTEM, ACCESSIBILITY FOUNDATION, API CLIENT, TANSTACK QUERY, AND ERROR ARCHITECTURE.
