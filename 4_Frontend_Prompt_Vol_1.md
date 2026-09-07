# PROJECT 1 — INSTAGRAM-LIKE GLOBAL SOCIAL PLATFORM

# FRONTEND PROMPT — VOLUME 1

# WEB APPLICATION — CORE USER EXPERIENCE, AUTHENTICATION, PROFILES, SOCIAL GRAPH, FEED & CONTENT

You are the Staff Frontend Engineering team responsible for implementing the web application of a production-grade Instagram-like global social platform.

This prompt is fully standalone. It does not depend on any other prompt, document, previous conversation, previous implementation, previous architecture, previous volume, approval, or hidden context.

You must inspect the current repository before making changes and integrate with compatible existing implementation.

Repository state is the source of truth for existing code.

Implement real production functionality.

Do not generate pseudo-code.

Do not create placeholder screens or fake functionality.

Do not use TODO/FIXME as substitutes for implementation.

Do not claim a feature is complete when it is not implemented.

Do not regenerate unchanged files.

Preserve existing working unrelated functionality.

==================================================

1. PRODUCT OBJECTIVE
   ==================================================

Build the web application for a global social platform supporting:

- registration
- login
- account recovery
- profile management
- public/private accounts
- following
- follow requests
- followers/following
- blocking
- muting
- restricting
- home feed
- following feed
- posts
- image/video media
- multi-media posts
- stories
- reels
- likes
- comments
- saves
- shares
- hashtags
- mentions
- search
- discovery
- notifications
- messaging entry points
- settings
- privacy controls
- moderation/reporting flows

The web application must be responsive, accessible, performant, secure, and production-ready.

==================================================
2. REQUIRED WEB TECHNOLOGY
==========================

Use:

- Next.js
- React
- TypeScript
- Tailwind CSS
- shadcn/ui
- TanStack Query
- Zustand

Use the latest compatible versions already present in the repository when the project is initialized.

Do not unnecessarily upgrade dependencies solely for stylistic reasons.

==================================================
3. FRONTEND ARCHITECTURE
========================

Use a modular frontend architecture.

Organize functionality into domains such as:

- authentication
- profile
- social graph
- feed
- posts
- stories
- reels
- comments
- search
- discovery
- notifications
- messaging integration
- settings
- moderation
- shared UI
- API client
- state
- utilities

Avoid placing all application logic inside route components.

Use reusable hooks, services, components, schemas, and domain-specific modules.

==================================================
4. NEXT.JS ARCHITECTURE
=======================

Use the Next.js App Router where compatible with the existing application.

Clearly distinguish:

- Server Components
- Client Components
- server-side data needs
- browser-only functionality

Use Client Components only where interactivity, browser APIs, or client state require them.

Do not make the entire application a Client Component unnecessarily.

==================================================
5. ROUTING
==========

Implement a coherent route structure.

Representative routes may include:

/
 /login
 /register
 /forgot-password
 /reset-password
 /explore
 /search
 /notifications
 /messages
 /settings
 /settings/account
 /settings/privacy
 /settings/security
 /u/[username]
 /p/[postId]
 /reel/[reelId]

Use the repository's existing routing conventions when already established.

Routes containing user-generated identifiers must validate server responses rather than trusting the URL.

==================================================
6. AUTHENTICATION EXPERIENCE
============================

Implement:

- registration
- login
- logout
- session restoration
- token refresh handling
- verification
- password reset
- session/device management

Authentication state must be integrated with the backend contract.

Do not store sensitive authentication credentials in insecure browser storage.

Use secure cookie/session mechanisms according to the backend authentication architecture.

==================================================
7. AUTHENTICATION ERROR UX
==========================

Handle:

- invalid credentials
- expired session
- revoked session
- unverified account
- rate limiting
- network failure
- server failure

Use clear user-facing messages without exposing security-sensitive information.

Do not expose raw server exceptions.

==================================================
8. ROUTE PROTECTION
===================

Protect authenticated routes.

Unauthenticated users attempting protected pages should be redirected appropriately.

Do not rely solely on client-side route guards for security.

The backend remains authoritative for authorization.

==================================================
9. API CLIENT
=============

Create a centralized typed API client.

It should provide:

- base URL configuration
- authentication handling
- request headers
- request IDs where supported
- error normalization
- retries only for safe/transient operations
- cancellation support
- response typing

Do not scatter raw fetch calls throughout the application.

==================================================
10. TANSTACK QUERY
==================

Use TanStack Query for server state.

Manage:

- queries
- mutations
- invalidation
- cache
- pagination
- optimistic updates where safe
- loading states
- error states

Do not duplicate remote server data unnecessarily in Zustand.

==================================================
11. ZUSTAND
===========

Use Zustand for appropriate client/application state such as:

- UI state
- modal state
- navigation-related state
- draft state
- transient interaction state
- selected media state

Do not make Zustand the authoritative store for server-side authorization or permissions.

==================================================
12. DESIGN SYSTEM
=================

Use Tailwind CSS and shadcn/ui.

Create consistent primitives for:

- buttons
- inputs
- forms
- dialogs
- dropdowns
- avatars
- cards
- tabs
- tooltips
- menus
- sheets
- alerts
- toasts
- skeletons
- pagination/loading states

Avoid duplicated custom styles when an existing design-system component solves the problem.

==================================================
13. VISUAL LANGUAGE
===================

Create a modern, polished social-media interface.

Prioritize:

- clean typography
- strong visual hierarchy
- intuitive navigation
- high-quality media presentation
- subtle interaction feedback
- responsive layouts
- accessible controls

Avoid excessive animation.

Animations should communicate state or improve perceived responsiveness.

==================================================
14. RESPONSIVE DESIGN
=====================

Support:

- desktop
- laptop
- tablet
- mobile web

Layouts must adapt without breaking content.

Do not simply scale desktop UI down to mobile.

Use appropriate responsive navigation patterns.

==================================================
15. ACCESSIBILITY
=================

Implement accessible interfaces.

Support:

- semantic HTML
- keyboard navigation
- visible focus
- ARIA where necessary
- accessible dialogs
- accessible menus
- accessible form errors
- proper labels
- alt text for images
- screen-reader-friendly state changes

Do not use color alone to communicate important state.

==================================================
16. PROFILE PAGE
================

Implement profile pages supporting:

- avatar
- username
- display name
- biography
- website
- follower count
- following count
- post count
- follow button
- requested state
- following state
- blocked state where appropriate
- profile content grid
- private-account state

The UI must reflect backend authorization.

Do not assume that visibility from cached client state means content is accessible.

==================================================
17. PROFILE EDITING
===================

Support:

- display name
- biography
- website
- avatar
- username where supported

Handle:

- validation
- duplicate username
- image upload
- upload errors
- unsaved changes
- loading
- success/error feedback

==================================================
18. AVATAR UPLOAD
=================

Implement a secure avatar upload flow using the backend media API.

The browser should:

- request upload authorization
- upload directly to the approved storage workflow
- notify backend of completion
- refresh profile state

Do not send large files through the Next.js server unnecessarily.

==================================================
19. FOLLOW UI
=============

Support:

- Follow
- Following
- Requested
- Unfollow
- Approve request
- Reject request

The UI must handle race conditions.

For example, after a double click or repeated action, the final server state must remain authoritative.

==================================================
20. FOLLOWERS/FOLLOWING
=======================

Implement modal or dedicated views for:

- followers
- following
- pending requests

Use cursor-based pagination.

Support:

- loading more
- empty state
- errors
- blocked users
- removed users

Avoid requesting the entire relationship set at once.

==================================================
21. BLOCK/MUTE/RESTRICT
=======================

Implement settings and profile controls for:

- block
- unblock
- mute
- unmute
- restrict
- unrestrict

Use confirmation dialogs for destructive or consequential operations.

After mutation:

- invalidate relevant queries
- update visible relationship state
- remove content where appropriate

Never rely on UI-only state to enforce these rules.

==================================================
22. HOME FEED
=============

Implement the main feed.

Support:

- feed items
- multiple media
- image/video playback
- author information
- timestamps
- captions
- mentions
- hashtags
- likes
- comments
- saves
- shares
- content menus

Use TanStack Query infinite queries for cursor pagination.

==================================================
23. FEED LOADING
================

Provide:

- initial skeletons
- incremental loading
- empty state
- error state
- retry
- pull/refresh behavior where appropriate for web

Avoid layout shifts.

Use stable media dimensions.

==================================================
24. FEED ERROR HANDLING
=======================

If ranking or recommendation services fail, the backend may return fallback content.

The frontend must display the returned content without exposing internal dependency failures.

Do not tell the user that internal infrastructure components failed unless the API deliberately returns a user-safe state.

==================================================
25. FEED PERFORMANCE
====================

Optimize for large media-heavy pages.

Use:

- lazy loading
- image optimization
- responsive image sizes
- prefetching where useful
- virtualization where appropriate
- stable keys
- query caching
- bounded rendering

Do not load full-resolution media before it is needed.

==================================================
26. POST CARD
=============

Create reusable post-card components.

Support:

- author
- avatar
- media
- carousel
- caption
- hashtags
- mentions
- like action
- save action
- share
- comment entry
- overflow menu
- accessibility labels

The same primitives should be reusable across feed, profile, search, and discovery surfaces.

==================================================
27. MEDIA CAROUSEL
==================

Support multi-media posts.

Provide:

- previous/next controls
- swipe/touch support where appropriate
- position indicator
- keyboard support
- accessible labels

Do not load every media object at full quality unnecessarily.

==================================================
28. VIDEO PLAYBACK
==================

Implement browser video playback using backend-provided playback metadata.

Support:

- poster
- play/pause
- mute/unmute
- progress
- duration
- responsive sizing

Do not expose private storage credentials.

Do not assume every browser supports every format.

Use supported fallback behavior.

==================================================
29. STORY UI
============

Implement:

- story tray
- story avatars
- unread state
- viewer
- next/previous story
- progress indicators
- close
- expiration handling
- interaction states

The backend remains authoritative for story availability.

==================================================
30. STORY VIEWER
================

The viewer should:

- load story media efficiently
- mark stories viewed
- stop progression when paused where appropriate
- handle media loading failures
- skip unavailable/expired content

Do not assume a story remains valid because it was previously cached.

==================================================
31. REELS
=========

Implement a web reels experience.

Support:

- vertically oriented media
- video playback
- creator
- caption
- hashtags
- likes
- comments
- saves
- shares

Use efficient media loading.

Avoid loading multiple high-resolution videos simultaneously.

==================================================
32. REELS INTERACTION
=====================

Support:

- autoplay under browser policy
- mute state
- play/pause
- next/previous navigation
- intersection-based playback where appropriate

Respect browser autoplay restrictions.

Do not create an aggressive autoplay loop that consumes excessive bandwidth.

==================================================
33. POST CREATION
=================

Implement a production post composer.

Support:

- selecting media
- previews
- reordering media
- removing media
- caption
- hashtags
- mentions
- visibility
- publishing
- upload progress
- processing state
- failure recovery

==================================================
34. MEDIA UPLOAD UX
===================

The composer must distinguish:

- upload progress
- uploaded
- processing
- ready
- rejected
- failed

Do not tell the user a post is published while required media is still invalid or unavailable.

==================================================
35. DRAFT STATE
===============

Use appropriate local state for unfinished post composition.

Support recovery from accidental navigation where practical.

Do not persist large media blobs unnecessarily in browser state.

==================================================
36. POST VISIBILITY UI
======================

Provide clear controls for supported visibility options.

The UI must display the current selection.

Do not allow the browser to submit unsupported values without validation.

Backend authorization remains authoritative.

==================================================
37. LIKES
=========

Implement:

- like
- unlike
- like count
- current-user like state

Use optimistic updates only where rollback is reliable.

Repeated clicks must not create inconsistent UI state.

==================================================
38. COMMENTS
============

Implement:

- comment list
- comment creation
- reply interaction
- comment deletion where authorized
- mentions
- loading
- pagination
- moderation/report actions

Use cursor pagination for large comment sets.

==================================================
39. SAVES
=========

Implement:

- save
- unsave
- saved-state display
- saved-content page where applicable

Never display inaccessible saved content without refreshing authorization state from the backend.

==================================================
40. SHARING
===========

Support appropriate web sharing.

Use:

- share dialogs
- copy link
- supported native/browser sharing APIs

Never expose a private media object directly to unauthorized users.

==================================================
41. HASHTAGS
============

Render hashtags as navigable links.

Use normalized hashtag routes such as:

/explore/tags/[tag]

Search/tag pages must support pagination and proper loading/error states.

==================================================
42. MENTIONS
============

Render valid mentions as profile links.

Do not allow malformed user-generated mention markup to create arbitrary links.

Use backend-parsed structured mention information where possible rather than trusting raw HTML.

==================================================
43. SEARCH UI
=============

Implement global search with:

- query input
- autocomplete
- users
- hashtags
- content
- recent searches where supported
- loading
- empty state
- errors

Use debouncing for autocomplete.

Cancel stale requests when query changes rapidly.

==================================================
44. SEARCH SECURITY
===================

Do not render results simply because the API returned stale cached data.

Respect server-provided visibility.

Private or blocked content must not be surfaced.

==================================================
45. EXPLORE/DISCOVERY
=====================

Implement discovery surfaces supporting:

- recommended content
- trending content
- creators
- hashtags
- reels

Use responsive media grids and efficient loading.

==================================================
46. NOTIFICATIONS UI
====================

Implement:

- notifications list
- unread state
- mark read
- mark all read
- notification grouping
- actor avatars
- target links

Use polling, server events, or WebSockets according to repository/backend support.

Do not create an aggressive polling loop.

==================================================
47. NOTIFICATION REAL-TIME UPDATES
==================================

When real-time notification delivery is available:

- update unread count
- insert new notifications
- avoid duplicates
- invalidate related queries when required

A reconnecting client must be able to resynchronize from the API.

==================================================
48. SETTINGS
============

Implement settings pages for:

- account
- privacy
- security
- notifications
- sessions/devices
- blocked accounts
- muted accounts
- restricted accounts

Use clear navigation and responsive layouts.

==================================================
49. PRIVACY SETTINGS UI
=======================

Support public/private account settings.

Changing privacy should:

- show current state
- require appropriate confirmation if necessary
- update server
- refresh dependent UI state

Do not assume all existing content becomes public/private solely through client cache updates.

==================================================
50. SECURITY SETTINGS UI
========================

Support:

- change password
- session list
- revoke session
- logout all devices where supported
- verification/security state

Never display raw credentials or tokens.

==================================================
51. REPORTING
=============

Implement report flows for:

- users
- posts
- reels
- comments
- other supported content

Use a clear reason-selection dialog.

Prevent accidental duplicate submissions.

Provide success/failure feedback.

==================================================
52. CONTENT MENUS
=================

Reusable content menus may include:

- save
- share
- report
- not interested
- mute
- block
- restrict
- delete/edit for owners

Available actions must depend on backend-provided permissions/state.

==================================================
53. FORMS
=========

Use strongly typed forms.

Validate:

- required fields
- length limits
- URL fields
- usernames
- captions
- comments
- search input

Error messages should appear close to the relevant input.

==================================================
54. ERROR BOUNDARIES
====================

Use React/Next.js error boundaries appropriately.

A failure in one content component should not unnecessarily crash the entire application.

Provide safe recovery actions such as:

- retry
- refresh
- return home

Do not expose stack traces.

==================================================
55. LOADING STATES
==================

Implement intentional loading states.

Use:

- skeletons
- spinners where appropriate
- disabled mutation controls
- optimistic placeholders

Avoid flashing unrelated content between states.

==================================================
56. EMPTY STATES
================

Create useful empty states for:

- no followers
- no following
- no posts
- no saved content
- no notifications
- no search results
- no message history where relevant
- no discovery results

Empty states should provide appropriate next actions without inventing unavailable features.

==================================================
57. URL AND NAVIGATION STATE
============================

Keep shareable application state in URLs when appropriate.

Examples:

- search query
- profile username
- post ID
- reel ID
- hashtag

Do not encode sensitive state into URLs.

==================================================
58. BROWSER SECURITY
====================

Protect against frontend security issues including:

- unsafe HTML rendering
- XSS
- malicious URL injection
- unsafe third-party script usage
- insecure token handling

Do not use dangerouslySetInnerHTML unless absolutely necessary and properly sanitized.

==================================================
59. IMAGE SECURITY
==================

Treat user-uploaded images as untrusted.

Use the backend media pipeline.

Do not attempt to infer authorization from image URLs.

==================================================
60. ACCESSIBILITY TESTING
=========================

Test:

- keyboard navigation
- tab order
- focus trapping
- dialogs
- menus
- forms
- screen-reader labels
- media controls

==================================================
61. PERFORMANCE
===============

Optimize:

- initial page load
- route transitions
- media rendering
- feed scrolling
- image loading
- search responsiveness

Use Next.js capabilities such as:

- route-level code splitting
- image optimization
- prefetching where appropriate
- caching where safe

Do not cache private user data publicly.

==================================================
62. SEO
=======

For public pages, provide appropriate metadata for:

- user profiles
- public posts
- public reels
- public hashtags

Never expose private content through search-engine metadata.

==================================================
63. ANALYTICS INTEGRATION
=========================

Where analytics are supported, emit client-side events for meaningful product interactions.

Examples:

- post view
- reel play
- profile view
- follow
- like
- save
- share
- search
- story view

Do not collect unnecessary sensitive data.

==================================================
64. REAL-TIME INTEGRATION
=========================

Prepare frontend infrastructure to consume authenticated WebSocket/Socket.IO events for:

- notifications
- messaging indicators
- presence where applicable
- live engagement where supported

The browser must recover from:

- disconnect
- reconnect
- expired session
- server restart

==================================================
65. NETWORK FAILURE
===================

Handle:

- timeout
- offline state
- transient connection failure
- server error
- authentication expiration

Mutations must not blindly repeat unsafe requests.

Use idempotency mechanisms where supported by the backend.

==================================================
66. CLIENT CACHING
==================

Define cache policies for:

- feed
- profiles
- posts
- comments
- stories
- reels
- search
- notifications

Use invalidation after mutations.

Avoid long-lived stale privacy-sensitive state.

==================================================
67. SECURITY-CRITICAL UI RULE
=============================

The frontend must never be the final authority for:

- permissions
- ownership
- privacy
- blocked status
- moderation decisions
- account restrictions

The backend remains authoritative.

The frontend should reflect authoritative server responses.

==================================================
68. TESTING
===========

Implement:

- unit tests
- component tests
- integration tests
- route tests
- API-client tests
- accessibility tests
- critical end-to-end tests

Critical flows include:

- registration
- login
- logout
- password reset
- profile editing
- follow
- private-account request
- block
- mute
- create post
- upload media
- like
- comment
- save
- search
- notifications
- reporting

==================================================
69. END-TO-END TESTING
======================

Test complete user journeys such as:

New user
→ registration
→ verification
→ login
→ profile setup
→ follow another user
→ view feed
→ create post
→ engage with content

Private account
→ request follow
→ approval
→ view protected content

User blocking
→ block account
→ verify protected interactions disappear

Content creation
→ upload media
→ processing
→ publish
→ retrieve post

==================================================
70. FRONTEND ACCEPTANCE CRITERIA
================================

The implementation is complete only when:

- Next.js application works
- routing works
- authentication works
- protected routes work
- API client works
- TanStack Query integration works
- Zustand state is appropriate
- design system is coherent
- responsive layouts work
- accessibility requirements are addressed
- profile pages work
- profile editing works
- avatar upload works
- follow workflows work
- followers/following work
- block/mute/restrict controls work
- home feed works
- feed pagination works
- post cards work
- media carousels work
- video playback works
- story UI works
- reels UI works
- post composer works
- media upload UX works
- likes work
- comments work
- saves work
- sharing works
- hashtag navigation works
- mentions work
- search works
- autocomplete works
- discovery works
- notifications work
- settings work
- privacy settings work
- security settings work
- reporting works
- error boundaries exist
- loading/empty/error states exist
- security controls are respected
- frontend tests exist
- end-to-end critical paths work
- TypeScript compilation succeeds
- linting succeeds
- no required UI is left as a placeholder

==================================================
71. IMPLEMENTATION FINISHING RULE
=================================

Do not stop after creating routes, components, interfaces, or design placeholders.

Implement the actual production experience.

Inspect the current repository first.

Reuse compatible components and infrastructure.

Integrate with existing APIs and backend contracts.

Do not recreate unchanged functionality.

Validate:

- TypeScript
- linting
- build
- unit tests
- component tests
- integration tests
- accessibility
- critical end-to-end workflows
- responsive behavior
- authentication flows
- authorization-dependent UI
- media upload flows
- error and offline states

The resulting web application must be a real production-grade social platform interface rather than a visual prototyp

You are operating in Senior Engineering Team Mode.

You are the Principal Frontend Architect, Staff Frontend Engineer, Staff UI/UX Engineer, Accessibility Engineer, Performance Engineer, Security Engineer, QA Engineer, and Technical Writer for this Instagram-like global social platform.

The backend implementation is now established through the previous backend volumes.

Your task in this phase is to implement the production-grade web frontend that consumes the existing backend contracts.

This is NOT a prototype.

This is NOT a mock UI.

This is NOT a collection of static screens.

Build a complete, maintainable, scalable production web application comparable in architectural scope to a modern large-scale social platform.

Use the existing architecture and backend contracts as the source of truth.

Do not invent backend APIs when an existing contract already exists.

Do not modify backend behavior merely to simplify frontend implementation.

If a backend contract is genuinely missing and the frontend requires it, document the contract dependency explicitly rather than inventing incompatible behavior.

==================================================
PRIMARY FRONTEND STACK
======================

Use:

- Next.js
- React
- TypeScript
- Tailwind CSS
- shadcn/ui
- TanStack Query
- Zustand

Follow the exact versions already established by the repository.

Use the App Router unless the existing repository explicitly requires another routing architecture.

Use strict TypeScript.

Avoid unnecessary dependencies.

==================================================
FRONTEND OBJECTIVES
===================

The frontend must provide:

- responsive desktop experience
- tablet experience
- mobile web experience
- accessible UI
- keyboard navigation
- screen-reader compatibility
- production-grade loading states
- production-grade error states
- optimistic updates where safe
- cache synchronization
- infinite scrolling where appropriate
- cursor pagination
- route-level loading
- route-level error handling
- authenticated application shell
- public application shell
- reusable design system
- reusable interaction primitives
- media components
- modal/dialog architecture
- drawer/sheet architecture
- toast/feedback system
- command/search interactions
- real-time updates where appropriate
- secure authentication state
- protected routes
- SEO-aware public pages
- metadata
- analytics instrumentation
- feature-flag support
- experimentation hooks
- observability hooks

==================================================
DESIGN DIRECTION
================

The product should feel like a polished global social platform.

Do not clone proprietary source code, internal implementation details, or copyrighted visual assets.

Recreate the product category and interaction patterns using original implementation and styling.

Design principles:

- visually refined
- information-dense without feeling cluttered
- media-first
- fast
- responsive
- intuitive
- consistent
- accessible
- touch-friendly
- keyboard-friendly
- high-quality typography
- clear hierarchy
- strong visual feedback
- subtle motion
- predictable navigation

Support:

- light mode
- dark mode
- system preference

Use design tokens rather than hard-coded styling scattered throughout the application.

==================================================
FRONTEND ARCHITECTURE
=====================

Establish a scalable structure separating:

- app routes
- layouts
- feature modules
- domain models
- API clients
- query hooks
- mutations
- Zustand stores
- UI primitives
- composite components
- media components
- forms
- validation
- utilities
- authentication
- permissions
- realtime
- analytics
- feature flags
- error handling
- configuration

Do not create a giant components directory containing unrelated business logic.

Feature modules should own their feature-specific behavior.

Shared components should remain genuinely reusable.

==================================================
SERVER VS CLIENT COMPONENTS
===========================

Use Server Components by default where appropriate.

Use Client Components only where interaction or browser APIs require them.

Do not mark entire route trees as client components unnecessarily.

Keep server-side data fetching and client-side interactive state clearly separated.

Use Suspense and streaming where appropriate.

==================================================
API CLIENT ARCHITECTURE
=======================

Create a centralized API client.

The API client must support:

- base URL configuration
- authentication
- request headers
- correlation/request IDs where appropriate
- JSON handling
- multipart uploads
- standardized error handling
- response parsing
- cancellation via AbortController
- timeout behavior
- retries only where safe
- idempotency keys where required

Do not scatter fetch logic throughout components.

Create typed API contracts.

Centralize error normalization.

==================================================
AUTHENTICATION ARCHITECTURE
===========================

Implement the web authentication layer using the established backend authentication contracts.

Support:

- registration
- login
- logout
- session restoration
- session expiration
- refresh
- account verification flows
- password reset
- session/device management

Do not expose sensitive tokens unnecessarily to client-side JavaScript.

Use the authentication mechanism established by the backend architecture.

Implement:

- authenticated route protection
- guest route handling
- session hydration
- unauthorized response handling
- forced logout when session becomes invalid

Avoid authentication state flashes.

==================================================
GLOBAL APPLICATION STATE
========================

Use Zustand only for genuinely client-owned global state.

Examples:

- UI preferences
- active dialogs
- media viewer state
- composer state where appropriate
- navigation state
- local interaction state
- feature-specific client state

Do NOT use Zustand as a replacement for server-state management.

TanStack Query must own:

- server data
- fetching
- caching
- mutations
- invalidation
- synchronization

==================================================
TANSTACK QUERY ARCHITECTURE
===========================

Create consistent query-key conventions.

Define query factories for major domains.

Support:

- stale time
- cache time according to current TanStack Query API/version
- retries
- cancellation
- optimistic mutation handling
- rollback
- invalidation
- partial cache updates
- pagination
- infinite queries

Do not invalidate the entire application cache after every mutation.

Invalidate only affected queries.

==================================================
ERROR ARCHITECTURE
==================

Create a consistent hierarchy for:

- API errors
- validation errors
- authorization errors
- authentication errors
- not-found errors
- rate-limit errors
- conflict errors
- network errors
- timeout errors
- unknown errors

Provide:

- route-level error boundaries
- component-level fallback states
- retry actions
- user-friendly messaging
- developer-safe diagnostics

Never expose raw server stack traces to users.

==================================================
ROUTING ARCHITECTURE
====================

Establish the complete route architecture.

Public routes:

- /
- /login
- /signup
- /accounts/*
- /explore
- /reels
- /about where applicable

Authenticated routes:

- /feed
- /direct
- /notifications
- /profile/*
- /settings/*
- /create
- /saved
- /search
- /activity
- feature-specific routes

Use route groups and layouts where appropriate.

Do not create duplicate layouts unnecessarily.

==================================================
APPLICATION SHELL
=================

Build the primary authenticated application shell.

Desktop:

- left navigation
- main content area
- optional right rail
- persistent navigation
- responsive collapse behavior

Tablet:

- adaptive navigation
- optimized content width
- touch-friendly interactions

Mobile web:

- compact navigation
- bottom navigation where appropriate
- full-width content
- gesture-friendly controls
- responsive overlays

The shell must not cause excessive layout shifts.

==================================================
NAVIGATION
==========

Navigation must support:

- Home
- Search
- Explore
- Reels
- Messages
- Notifications
- Create
- Profile
- Settings

Support active route state.

Support unread indicators.

Support notification badges.

Support keyboard navigation.

Navigation state must be derived from routing rather than manually duplicated state.

==================================================
DESIGN SYSTEM
=============

Create a reusable design system based on shadcn/ui and Tailwind.

Establish:

- typography
- spacing
- radius
- elevation
- borders
- semantic colors
- focus states
- motion
- breakpoints

Create primitives for:

- Button
- IconButton
- Input
- Textarea
- Select
- Checkbox
- Radio
- Switch
- Avatar
- Badge
- Card
- Tooltip
- Popover
- DropdownMenu
- Dialog
- Sheet
- Drawer
- Tabs
- Skeleton
- Separator
- Progress
- ScrollArea
- Alert
- Toast
- ContextMenu
- Command

Do not fork or modify shadcn/ui components without a clear reason.

==================================================
ACCESSIBILITY
=============

All interactive functionality must be accessible.

Implement:

- semantic HTML
- correct heading hierarchy
- labels
- accessible names
- ARIA only where necessary
- keyboard navigation
- visible focus states
- focus trapping for modal dialogs
- focus restoration
- reduced-motion support
- sufficient contrast
- screen-reader announcements
- accessible error messages

Do not use inaccessible div-based controls when semantic controls are available.

Images require meaningful alt text when informative.

Decorative images must be correctly marked decorative.

==================================================
GLOBAL LOADING SYSTEM
=====================

Implement consistent loading patterns.

Support:

- route loading
- skeletons
- button loading
- inline loading
- image loading
- video loading
- mutation feedback
- background refresh indicators

Avoid unnecessary full-page spinners.

Use skeletons matching the eventual layout where practical.

==================================================
MEDIA FOUNDATION
================

Build reusable media components for:

- images
- videos
- reels
- story media
- avatars
- thumbnails
- galleries
- fullscreen viewers

Image component requirements:

- responsive sizes
- lazy loading
- priority loading when appropriate
- aspect ratio preservation
- placeholder states
- broken-image handling

Video requirements:

- autoplay rules compatible with browsers
- muted autoplay where required
- poster images
- play/pause
- mute/unmute
- progress
- fullscreen
- intersection-based playback where appropriate
- reduced-motion considerations
- bandwidth-conscious behavior

==================================================
MEDIA VIEWER
============

Create a reusable fullscreen media viewer.

Support:

- image
- video
- carousel
- next/previous
- close
- keyboard navigation
- touch navigation
- focus handling
- background interaction prevention

Do not duplicate viewer logic inside each feature.

==================================================
AVATAR SYSTEM
=============

Build reusable avatar components.

Support:

- user avatars
- fallback initials
- image loading
- status indicators where appropriate
- verified indicator
- creator/business indicator
- sizes

Avoid rendering huge avatar images when small variants are sufficient.

==================================================
PROFILE HEADER
==============

Create reusable profile header architecture.

Support:

- avatar
- username
- display name
- verification
- bio
- links
- follower counts
- following counts
- post counts
- follow button
- requested state
- following state
- blocked state
- restricted state
- message action
- edit profile action
- creator/business actions

Actions must depend on backend authorization state.

Do not infer permissions only from client-local state.

==================================================
USER PROFILE PAGE
=================

Implement profile route architecture supporting:

- public profile
- private profile
- own profile
- creator profile
- business profile
- blocked profile
- unavailable profile
- suspended profile

Implement profile tabs for applicable content:

- Posts
- Reels
- Tagged
- Saved where authorized
- additional backend-supported categories

Use cursor pagination.

Use query prefetching strategically.

==================================================
FEED FOUNDATION
===============

Create the primary feed experience.

Support:

- infinite scrolling
- cursor pagination
- post cards
- carousel posts
- reels in feed where supplied
- suggested accounts
- sponsored content placeholders only when backend data provides them
- engagement actions
- save
- share
- comments
- post menus

Every post card must be modular.

Avoid a monolithic FeedPost component.

Separate:

- header
- media
- caption
- metadata
- engagement
- actions
- comments preview
- menu

==================================================
POST CARD
=========

Build a production-grade post card.

Support:

- avatar
- username
- timestamp
- verification
- location
- menu
- image
- carousel
- video
- like
- comment
- share
- save
- caption
- hashtags
- mentions
- audio
- engagement metadata

Interactions must provide immediate feedback when safe.

Use optimistic updates for:

- likes
- saves
- follows

Only where backend semantics allow safe rollback.

==================================================
LIKE INTERACTION
================

Implement:

- optimistic like
- unlike
- rollback on failure
- accessibility feedback
- double-click/tap behavior where appropriate
- animation without excessive motion

Do not produce duplicate mutations from rapid interaction.

Use mutation deduplication or state guards.

==================================================
SAVE INTERACTION
================

Support:

- save
- unsave
- add to collection
- collection selection

Keep server state authoritative.

==================================================
COMMENTS FOUNDATION
===================

Create reusable comment interfaces.

Support:

- comments list
- pagination
- replies
- likes
- mentions
- moderation states
- deleted comments
- hidden comments where backend provides them

Comment composer must support:

- text
- mentions
- validation
- character limits from backend contracts
- submit
- loading
- error recovery

==================================================
FOLLOW INTERACTIONS
===================

Build reusable follow controls.

States:

- Follow
- Requested
- Following
- Unfollow confirmation where appropriate
- Blocked
- Restricted

Use backend response state rather than manually assuming transitions succeeded.

==================================================
STORY TRAY
==========

Implement the story tray.

Support:

- unread stories
- watched stories
- close friends stories
- creator stories
- business stories
- story expiration
- loading states
- empty state

Story tray must use efficient horizontal scrolling.

==================================================
STORY VIEWER FOUNDATION
=======================

Create the story viewer architecture.

Support:

- image stories
- video stories
- progress indicators
- previous/next
- pause
- resume
- close
- reply
- reactions
- viewer tracking
- muted/unmuted state
- keyboard navigation
- touch gestures where appropriate

Prevent unnecessary duplicate view tracking.

==================================================
EXPLORE FOUNDATION
==================

Create the Explore page.

Support:

- responsive grid
- mixed media
- reels
- posts
- recommendations
- loading states
- infinite scrolling
- content opening
- fullscreen viewer

Cards should adapt to media aspect ratios while preserving layout stability.

==================================================
REELS FOUNDATION
================

Create the Reels viewing experience.

Support:

- vertical media feed
- autoplay
- pause
- mute
- like
- comments
- share
- save
- follow
- audio
- creator profile access
- watch tracking

Use IntersectionObserver or equivalent browser APIs where appropriate.

Only one primary video should aggressively autoplay at a time.

Pause videos that leave the active viewport.

==================================================
SEARCH FOUNDATION
=================

Build global search.

Support:

- search input
- debouncing
- query state
- recent searches
- users
- creators
- hashtags
- audio
- posts/reels where supported
- search result tabs
- empty states
- loading
- error state

Do not issue one API request for every keystroke.

Use proper debounce and cancellation.

==================================================
SEARCH OVERLAY
==============

On desktop, support an expanded search experience.

On mobile, support a dedicated search route or full-screen interaction.

Search UI must preserve:

- keyboard input
- focus
- recent searches
- result navigation
- back behavior

==================================================
NOTIFICATIONS FOUNDATION
========================

Build notifications UI.

Support:

- likes
- comments
- follows
- follow requests
- mentions
- story interactions
- messages
- creator/business notifications
- system notifications

Support:

- unread state
- mark read
- mark all read
- pagination
- realtime insertion where supported

Do not refetch the entire notification list after every realtime event.

Update the relevant query cache.

==================================================
DIRECT MESSAGING FOUNDATION
===========================

Create the initial messaging UI architecture.

Support:

- conversation list
- unread counts
- search conversations
- message requests
- conversation view
- text messages
- media attachments
- message status
- typing indicator
- realtime updates

Separate:

- conversation list
- conversation header
- message timeline
- message composer
- message bubble
- attachment picker

==================================================
REALTIME CLIENT FOUNDATION
==========================

Create a centralized realtime client abstraction.

Use Socket.IO/WebSockets according to backend contracts.

Support:

- connection
- authentication
- reconnection
- connection status
- subscription management
- event routing
- cleanup

Do not create a new socket connection for every component.

Implement one appropriately scoped connection manager.

==================================================
REALTIME EVENT HANDLING
=======================

Handle server events for:

- new messages
- message delivered
- message read
- typing
- presence
- notifications
- follow changes
- likes where appropriate
- content updates where appropriate

Realtime events must update TanStack Query cache or domain state consistently.

Prevent duplicate event processing.

==================================================
CREATE FOUNDATION
=================

Build the initial content creation flow.

Support:

- media selection
- drag/drop
- file validation
- previews
- image/video metadata
- upload progress
- cancellation
- retry
- caption
- hashtags
- mentions
- location
- audience/visibility
- carousel creation

Use the backend upload/session architecture.

Do not upload large media through arbitrary API endpoints when the backend provides direct storage upload workflows.

==================================================
UPLOAD UX
=========

Implement:

- upload queue
- per-file progress
- validation errors
- upload failures
- retry
- cancellation
- processing state
- publish-ready state

Support resumable uploads when the backend contract provides them.

Do not lose upload state unnecessarily during re-renders.

==================================================
FORM ARCHITECTURE
=================

Use a consistent form strategy.

Forms must support:

- client validation
- server validation
- field errors
- form-level errors
- submission state
- reset
- dirty state
- accessibility

Do not duplicate validation rules unnecessarily when backend contracts provide constraints.

Client-side validation improves UX but never replaces backend validation.

==================================================
SETTINGS FOUNDATION
===================

Create settings architecture.

Categories:

- account
- profile
- privacy
- security
- notifications
- messaging
- content preferences
- blocked accounts
- restricted accounts
- close friends
- sessions/devices
- creator/business settings
- privacy export/deletion

Only expose controls supported by the backend.

==================================================
PRIVACY UI
==========

Build interfaces for:

- private account
- follow request management
- blocked accounts
- restricted accounts
- close friends
- activity visibility
- messaging permissions

Do not expose sensitive backend-only information.

==================================================
ACCESS AND PERMISSION MODEL
===========================

Create reusable frontend authorization helpers.

Examples:

- isAuthenticated
- canEditProfile
- canCreateContent
- canMessageUser
- canComment
- canSeeContent
- canManageBusiness
- canManageCreatorFeatures

These helpers should consume server-provided authorization state where necessary.

Do not attempt to duplicate all backend authorization rules on the frontend.

Frontend authorization is a UX layer, not a security boundary.

==================================================
SEO
===

Implement metadata for public pages.

Support:

- title
- description
- canonical
- Open Graph
- Twitter/X metadata where applicable
- robots behavior
- dynamic user/profile metadata
- dynamic content metadata where appropriate

Do not expose private content in metadata.

==================================================
PERFORMANCE
===========

Optimize:

- JavaScript bundles
- route loading
- image loading
- video loading
- hydration
- client-side state
- network requests
- cache usage
- rendering

Use:

- dynamic imports where appropriate
- lazy components
- Suspense
- image optimization
- prefetching strategically
- viewport-based media loading
- virtualization for very large lists where necessary

Do not prematurely optimize every component.

Measure expensive paths before introducing complex abstractions.

==================================================
CORE WEB VITALS
===============

Design toward strong:

- LCP
- INP
- CLS

Avoid:

- layout shifts caused by media
- blocking scripts
- excessive client hydration
- unnecessary rerenders
- giant initial bundles

==================================================
ANALYTICS
=========

Create a frontend analytics abstraction.

Track events through a provider-neutral interface.

Examples:

- page view
- post impression
- reel impression
- reel watch
- like
- comment
- follow
- save
- share
- search
- profile visit
- notification interaction
- message interaction
- upload started
- upload completed
- upload failed

Do not embed analytics vendor calls throughout UI components.

Ensure privacy controls are respected.

==================================================
ERROR MONITORING
================

Create frontend observability hooks for:

- unhandled exceptions
- rejected promises
- route failures
- API failures
- realtime connection errors
- upload failures
- performance issues

Use provider-neutral abstractions where the infrastructure layer has not yet selected a final vendor.

==================================================
FEATURE FLAGS
=============

Implement a frontend feature-flag abstraction.

Support:

- boolean features
- rollout values
- experiment variants
- user targeting data when supplied
- safe defaults

Do not hard-code experimental logic across dozens of components.

==================================================
RESPONSIVE RULES
================

Every major surface must work across:

- desktop
- tablet
- mobile

Do not simply shrink desktop layouts.

Adapt:

- navigation
- spacing
- typography
- dialogs
- drawers
- media
- interaction controls
- content density

==================================================
SECURITY
========

Frontend security requirements:

- sanitize untrusted HTML/content
- never inject arbitrary HTML
- protect sensitive state
- avoid storing secrets unnecessarily
- use secure browser storage patterns
- validate upload types client-side
- never trust client authorization
- protect sensitive routes
- avoid exposing internal API details
- do not place private information into analytics
- do not expose access tokens in URLs
- prevent unsafe redirect behavior

==================================================
TESTING STRATEGY
================

Use the repository's established test framework.

Implement:

- unit tests
- component tests
- integration tests
- end-to-end tests
- accessibility tests
- responsive behavior tests
- critical interaction tests

Test:

- authentication
- route protection
- feed
- post interactions
- comments
- follows
- stories
- reels
- search
- notifications
- messaging
- uploads
- settings
- privacy
- errors
- realtime behavior

==================================================
COMPONENT TESTING
=================

Every important reusable component should have tests for:

- rendering
- interaction
- loading
- empty state
- error state
- disabled state
- keyboard behavior
- accessibility

==================================================
E2E TESTING
===========

Create realistic user journeys:

1. Register.
2. Complete profile.
3. Follow a user.
4. Publish content.
5. See content in feed.
6. Like content.
7. Comment.
8. Save.
9. Search.
10. Open profile.
11. View stories.
12. Watch reels.
13. Send message.
14. Receive notification.
15. Change privacy settings.
16. Log out.
17. Log back in.

Use backend test infrastructure or appropriate test fixtures instead of fake UI-only state.

==================================================
FRONTEND FILE ORGANIZATION
==========================

Create a maintainable structure similar to:

src/
  app/
  components/
  features/
    auth/
    feed/
    profiles/
    posts/
    stories/
    reels/
    search/
    notifications/
    messaging/
    create/
    settings/
  lib/
    api/
    auth/
    query/
    realtime/
    analytics/
    permissions/
    feature-flags/
    validation/
  hooks/
  stores/
  types/
  utils/
  styles/

Adapt to the existing repository when a better established structure already exists.

Do not create duplicate abstractions for concepts already present.

==================================================
CODING RULES
============

Use strict TypeScript.

Prefer explicit types.

Avoid any.

Avoid unnecessary type assertions.

Avoid deeply nested conditional rendering.

Extract complex behavior into hooks or services.

Keep components focused.

Do not mix data fetching, business logic, and extensive rendering in one giant component.

Use semantic names.

Do not create generic components that are impossible to understand.

==================================================
STATE OWNERSHIP RULE
====================

Every state variable must have a clear owner.

Use:

- React state for local component state.
- Zustand for client-global state.
- TanStack Query for server state.
- URL parameters for shareable navigation state.

Do not duplicate the same server value in multiple stores without a specific synchronization strategy.

==================================================
NO MOCK DATA
============

Do not populate production UI with fake Instagram-style users, posts, messages, likes, or notifications.

Use real backend APIs.

Mocks may exist only inside isolated tests and development fixtures where explicitly appropriate.

==================================================
NO FRONTEND BUSINESS LOGIC THAT CONTRADICTS BACKEND
===================================================

Do not recreate:

- permission systems
- privacy systems
- moderation decisions
- fraud decisions
- recommendation ranking
- rights enforcement

The frontend should render backend-authoritative decisions.

==================================================
MILESTONE STRUCTURE
===================

Implement this frontend in the following sequence.

MILESTONE 1
Frontend architecture and application shell.

MILESTONE 2
Design system, accessibility foundation, API client, TanStack Query, error architecture.

MILESTONE 3
Authentication, account state, protected routes, session handling.

MILESTONE 4
Profiles, navigation, follow interactions, settings foundation.

MILESTONE 5
Feed, post cards, media rendering, likes, saves, comments.

MILESTONE 6
Stories and story viewer.

MILESTONE 7
Explore, search, trending content.

MILESTONE 8
Reels and high-performance vertical media feed.

MILESTONE 9
Notifications and realtime foundations.

MILESTONE 10
Direct messaging foundation and realtime conversations.

==================================================
IMPLEMENTATION RULES
====================

For every milestone:

1. Inspect the current repository.
2. Read the existing backend/API contracts.
3. Reuse existing frontend abstractions.
4. Do not regenerate unchanged files.
5. Create only required files.
6. Implement actual functionality.
7. Keep TypeScript compilation valid.
8. Add appropriate tests.
9. Update documentation where needed.
10. Validate the application.
11. Fix discovered errors before continuing.

Never stop at component sketches.

Never provide pseudo-code.

Never provide placeholder components.

Never use TODO implementations.

==================================================
QUALITY BAR
===========

The resulting frontend must feel like a serious production application.

Users should be able to:

- authenticate
- navigate
- browse content
- interact with content
- search
- view profiles
- follow accounts
- view stories
- view reels
- receive notifications
- begin conversations
- upload content
- manage settings

with real backend integration.

All major states must be implemented:

- loading
- loaded
- empty
- error
- unauthorized
- forbidden
- unavailable
- deleted
- blocked
- restricted
- offline/degraded where appropriate

==================================================
OUTPUT FORMAT
=============

For every implementation step:

1. State the current milestone.
2. State the affected frontend domains.
3. Inspect the existing project structure.
4. Describe only the important implementation decisions.
5. Create or modify required files.
6. Output complete contents for every new or changed file.
7. Never output unchanged files.
8. Add tests alongside implementation.
9. Run lint/typecheck/test/build commands where available.
10. Fix discovered issues.
11. Keep the project buildable after every milestone.

Do not implement infrastructure in this phase.

Do not implement Terraform.

Do not implement Kubernetes.

Do not implement AWS infrastructure.

Do not implement CI/CD.

Do not modify backend source code unless a genuine contract incompatibility must be resolved and the change is explicitly justified.

BEGIN WITH:

MILESTONE 1 — FRONTEND ARCHITECTURE AND APPLICATION SHELL.
