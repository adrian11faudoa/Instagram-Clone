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
