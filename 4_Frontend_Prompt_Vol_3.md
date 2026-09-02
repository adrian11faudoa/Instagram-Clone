You are operating in Senior Engineering Team Mode.

You are the Principal Frontend Architect, Staff Frontend Engineer, Staff UI/UX Engineer, Accessibility Engineer, Performance Engineer, Security Engineer, QA Engineer, and Technical Writer for this Instagram-like global social platform.

The previous frontend volumes established:

- frontend architecture
- application shell
- design system
- accessibility foundation
- API client
- API error handling
- TanStack Query architecture
- authentication
- session management
- protected routes
- profiles
- follow workflows
- blocking/restriction workflows
- account/privacy/security settings foundation
- responsive navigation

This volume continues directly from those implementations.

Do not restart the frontend.

Do not replace working code.

Do not regenerate unchanged files.

Do not introduce a different frontend architecture.

Use the existing repository and backend contracts as the source of truth.

==================================================
VOLUME 3 SCOPE
==============

Implement the primary content and discovery experience:

MILESTONE 5
Feed, posts, carousels, comments, likes, saves, sharing, and content interaction.

MILESTONE 6
Stories, story tray, story viewer, story interactions, highlights.

MILESTONE 7
Explore, discovery grids, search, trending, hashtags, mentions, audio discovery.

MILESTONE 8
Reels and high-performance vertical media experience.

==================================================
NON-NEGOTIABLE IMPLEMENTATION RULES
===================================

Production-grade implementation only.

Never generate pseudo-code.

Never generate placeholders.

Never generate TODOs.

Never use fake production data.

Never create static-only Instagram-style mockups.

Use real backend APIs.

Every generated file must compile.

Every API request must use the centralized API client.

Every server-state operation must use TanStack Query.

Use Zustand only for client-owned UI state.

Do not duplicate business logic between components.

Do not duplicate backend authorization logic.

Do not trust frontend visibility as security.

Do not regenerate unchanged files.

Do not modify backend source unless a genuine incompatibility requires a narrowly scoped correction.

==================================================
CONTENT ARCHITECTURE
====================

Establish reusable content primitives.

Content types include:

- Post
- Carousel
- Reel
- Story
- Highlight
- Audio
- Hashtag
- Mention
- Location

Create shared models/interfaces for:

- content identity
- author
- publication time
- visibility
- engagement summary
- media
- captions
- mentions
- hashtags
- audio
- moderation state
- deleted state
- availability

Do not copy the same interfaces into multiple feature folders.

==================================================
MILESTONE 5 — FEED AND POSTS
=============================

Build the core feed experience.

==================================================
5.1 FEED ROUTE
==============

Implement the primary home/feed route.

The feed must support:

- initial loading
- cursor pagination
- infinite scrolling
- pull-to-refresh behavior where appropriate
- empty state
- error state
- retry
- partial failures
- refresh indicator
- content insertion
- content removal
- stale-data reconciliation

Use the backend cursor contract.

Never use page-number pagination when the backend exposes cursor pagination.

==================================================
5.2 FEED QUERY
==============

Use TanStack Query infinite queries.

The feed query must:

- use stable query keys
- preserve cursors
- stop requesting when no next cursor exists
- abort obsolete requests
- avoid duplicate page requests
- reconcile mutations
- support targeted cache updates

Do not refetch the entire feed after every like.

==================================================
5.3 FEED LAYOUT
===============

Build a responsive feed layout.

Desktop:

- primary feed column
- optional recommendations/right rail

Tablet:

- centered feed
- reduced surrounding navigation

Mobile:

- full-width feed
- compact spacing
- touch-friendly actions

Do not create excessive nested layout containers.

==================================================
5.4 FEED POST COMPONENT
=======================

Create a reusable post composition:

PostCard
├── PostHeader
├── PostMedia
├── PostActions
├── PostEngagement
├── PostCaption
├── PostMetadata
├── PostCommentsPreview
└── PostFooter

Keep these components independently testable.

==================================================
5.5 POST HEADER
===============

Support:

- avatar
- username
- display name where applicable
- verification badge
- time
- location
- author actions
- post menu

Post menu may expose:

- save
- hide
- report
- unfollow/mute where supported
- copy/share link
- delete for owned content
- disable comments where supported

Menu options must depend on backend-authoritative state.

==================================================
5.6 POST MEDIA
==============

Create a reusable media renderer.

Support:

- single image
- video
- carousel
- mixed media where backend permits
- unavailable media
- deleted media
- processing media
- moderation-hidden media

Preserve aspect ratio.

Reserve dimensions before media loads.

Prevent cumulative layout shift.

==================================================
5.7 CAROUSEL
============

Create an accessible carousel.

Support:

- next
- previous
- pagination indicators
- swipe/touch
- keyboard navigation
- current-slide announcement
- lazy loading adjacent media
- video slides
- double-tap like where appropriate

Do not load every high-resolution image immediately.

==================================================
5.8 VIDEO POST
==============

Support:

- poster
- play/pause
- mute/unmute
- progress
- fullscreen
- replay
- intersection-based playback
- watch event tracking

Avoid multiple autoplaying videos in the same viewport.

==================================================
5.9 POST ACTIONS
================

Implement:

- like
- comment
- share
- save

Actions must support:

- loading
- disabled
- success
- rollback
- error

Use optimistic updates only for safe interactions.

==================================================
5.10 LIKE
=========

Implement:

- like
- unlike
- optimistic update
- rollback
- count reconciliation
- accessible state

Prevent duplicate rapid requests.

Synchronize:

- feed cache
- detail modal cache
- profile cache where applicable

Do not globally invalidate everything.

==================================================
5.11 COMMENTS
=============

Create comments experience.

Support:

- comments preview
- full comments view
- cursor pagination
- replies
- likes
- mentions
- deleted comments
- hidden/moderated comments
- blocked/restricted behavior

==================================================
5.12 COMMENT DRAWER
===================

On desktop, support a comment side panel or dialog according to the established design.

On mobile, support bottom-sheet/full-screen behavior.

The same comment data layer should power both.

==================================================
5.13 COMMENT CREATION
=====================

Implement comment composer.

Support:

- text input
- mention suggestions
- submit
- validation
- character count where required
- loading
- server error
- empty state
- moderation response

Prevent duplicate submission.

==================================================
5.14 COMMENT REPLIES
====================

Implement expandable replies.

Support:

- load replies
- collapse
- pagination
- nested depth according to backend limits

Do not recursively render arbitrarily deep comment trees.

Respect backend-defined nesting limits.

==================================================
5.15 COMMENT LIKE
=================

Implement optimistic comment liking.

Synchronize the affected comment item rather than refetching the entire comment list.

==================================================
5.16 SAVE
=========

Implement save behavior.

Support:

- saved
- unsaved
- collection selection where supported

After successful save:

- update post state
- update saved collections if loaded

==================================================
5.17 SHARING
============

Create share interaction.

Support:

- copy link
- native share API where supported
- share to supported users/conversations
- share to story where supported

Use progressive enhancement.

The UI must behave correctly when browser share APIs are unavailable.

==================================================
5.18 POST DETAILS
=================

Support opening a post into a dedicated detail view or route.

The detail view must preserve:

- media
- comments
- engagement
- author
- metadata
- navigation

Use URL-addressable state where appropriate.

==================================================
5.19 POST MODAL
===============

For modal-based post opening:

- focus trap
- keyboard Escape
- focus restoration
- scroll locking
- deep-link support where appropriate

Do not duplicate post rendering logic.

Reuse PostCard/PostContent primitives.

==================================================
5.20 POST CAPTION
=================

Render:

- text
- hashtags
- mentions
- links according to backend-safe rules
- truncation/expand

Do not insert unsanitized HTML.

==================================================
5.21 HASHTAG LINKS
==================

Hashtags should be interactive.

Clicking a hashtag should route to hashtag discovery.

Preserve accessibility.

==================================================
5.22 MENTION LINKS
==================

Mentions should route to user profiles.

Handle unavailable or deleted users gracefully.

==================================================
5.23 LOCATION
=============

Render location when provided.

Location may open:

- location discovery
- map integration where already supported
- location feed

Do not create a frontend dependency on an external mapping provider unless the architecture already establishes it.

==================================================
5.24 POST MENU SECURITY
=======================

Do not show destructive owner actions unless the authenticated user owns the post or backend explicitly grants permission.

Do not rely only on frontend checks.

If backend returns 403, present a safe error and reconcile state.

==================================================
5.25 FEED INSERTION
===================

When realtime or mutation events introduce a new post:

- update the feed cache intelligently
- avoid duplicate insertion
- preserve scroll position
- avoid unexpected jumps where possible

==================================================
5.26 FEED REMOVAL
=================

When backend events indicate:

- deletion
- moderation removal
- rights restriction
- block
- privacy change

remove or tombstone affected items.

Do not leave stale inaccessible content visible.

==================================================
5.27 FEED EMPTY STATES
======================

Create useful states for:

- no followed content
- new account
- content unavailable
- temporary feed failure

Provide appropriate discovery suggestions without inventing fake content.

==================================================
5.28 FEED ACCESSIBILITY
=======================

Ensure:

- logical reading order
- accessible buttons
- media descriptions
- carousel announcements
- like/save state announcements
- keyboard navigation

==================================================
5.29 FEED PERFORMANCE
=====================

Optimize:

- image sizes
- network requests
- component renders
- query cache
- media loading
- long feed rendering

Use virtualization only where measurements justify it.

==================================================
5.30 FEED TESTING
=================

Test:

- feed loading
- pagination
- empty feed
- errors
- retry
- like
- unlike
- save
- comment
- replies
- share
- deleted post
- blocked content
- private content
- carousel
- video
- accessibility
- responsive layout

==================================================
MILESTONE 6 — STORIES
======================

Implement stories as a first-class content experience.

==================================================
6.1 STORY TRAY
==============

Build the story tray.

Support:

- current user story
- unread stories
- watched stories
- close-friends stories
- creator stories
- business stories
- story progress
- user names
- avatars
- add-story action

Use horizontally scrollable presentation.

==================================================
6.2 STORY GROUP MODEL
=====================

Represent story groups separately from individual story items.

A user may have:

- multiple stories
- watched state
- unread count
- active story pointer

Do not flatten story groups in a way that complicates navigation.

==================================================
6.3 STORY VIEWER
================

Create a reusable fullscreen story viewer.

Support:

- image
- video
- next
- previous
- pause
- resume
- close
- progress
- tap zones where appropriate
- keyboard controls
- touch gestures
- reply
- reactions
- mute/unmute
- viewer tracking

==================================================
6.4 STORY PROGRESS
==================

Progress must:

- animate smoothly
- pause when media pauses
- resume correctly
- advance when duration completes
- reset when switching story
- stop on close

Do not use unreliable timers that drift badly across background-tab behavior.

Use media playback state where applicable.

==================================================
6.5 STORY VIEW TRACKING
=======================

Track story views through the backend contract.

Prevent duplicate view submissions.

Use a client-side dedupe mechanism only as an optimization, never as the security boundary.

==================================================
6.6 STORY REPLIES
=================

Implement story reply composer.

Support:

- text
- emoji/reaction responses
- send
- loading
- error
- blocked interaction

Respect story owner messaging permissions.

==================================================
6.7 STORY REACTIONS
===================

Implement supported story reactions.

Optimistic behavior is allowed only when backend semantics support safe rollback.

==================================================
6.8 STORY PRIVACY STATES
========================

Handle:

- public
- followers
- close friends
- restricted/unavailable
- expired
- deleted
- moderation-blocked

Do not display private story content after authorization changes.

==================================================
6.9 STORY CREATION
==================

Implement the web foundation for story creation.

Support backend-defined:

- image
- video
- caption/text where applicable
- visibility
- close friends audience
- upload
- processing
- publish
- failure
- retry

Reuse media upload abstractions established in previous volumes.

==================================================
6.10 STORY HIGHLIGHTS
=====================

Implement profile story highlights.

Support:

- highlight circles
- highlight title
- story list
- opening viewer
- owner management where backend supports it

==================================================
6.11 STORY HIGHLIGHT MANAGEMENT
===============================

For profile owners support:

- create highlight
- add story
- remove story
- rename
- reorder where backend supports it
- delete

Do not expose owner controls on profiles without authorization.

==================================================
6.12 STORY TESTING
==================

Test:

- tray loading
- unread state
- viewer navigation
- autoplay
- pause
- resume
- reply
- reaction
- view tracking
- expiration
- close friends
- highlight viewing
- highlight management
- accessibility
- responsive behavior

==================================================
MILESTONE 7 — EXPLORE, SEARCH, HASHTAGS, TRENDING
==================================================

Build the discovery experience.

==================================================
7.1 EXPLORE PAGE
================

Implement responsive discovery layout.

Support:

- image posts
- videos
- reels
- mixed aspect ratios
- featured content
- suggested content
- pagination
- content opening
- media viewer

==================================================
7.2 EXPLORE GRID
================

Build adaptive grid behavior.

Grid requirements:

- stable aspect ratios
- lazy loading
- predictable layout
- accessible cards
- keyboard navigation
- media type indication where needed

==================================================
7.3 EXPLORE QUERY
=================

Use infinite queries where supported.

Support:

- cursor pagination
- retry
- cancellation
- background refresh
- cache updates
- content removal

==================================================
7.4 TRENDING
============

Render backend-provided trending data.

Potential categories:

- hashtags
- audio
- creators
- topics

Do not calculate trending client-side.

==================================================
7.5 SEARCH PAGE
===============

Implement complete global search.

Support:

- query
- recent searches
- users
- creators
- hashtags
- audio
- posts/reels where backend supports
- result tabs
- pagination

==================================================
7.6 SEARCH INPUT
================

Implement:

- debounce
- cancellation
- keyboard shortcuts
- clear
- loading state
- empty state
- error state

Do not send a network request on every keystroke.

==================================================
7.7 SEARCH HISTORY
==================

Support:

- recent searches
- delete single search
- clear history
- query suggestions

Use backend state where the architecture defines persisted search history.

Do not store private search information unnecessarily.

==================================================
7.8 SEARCH RESULTS
==================

Render appropriate result components for:

- people
- creators
- hashtags
- audio
- media

Do not create one giant search-result component.

==================================================
7.9 HASHTAG PAGE
================

Implement hashtag discovery.

Support:

- hashtag title
- follow state where backend supports it
- recent content
- top content
- reels
- associated metadata
- pagination

Apply backend visibility rules.

==================================================
7.10 HASHTAG FOLLOW
===================

Implement hashtag follow/unfollow where backend supports it.

Use optimistic update only where rollback is safe.

==================================================
7.11 AUDIO PAGE
===============

Implement audio discovery page.

Support:

- audio metadata
- creator
- usage count
- reels using audio
- related content
- open audio feed
- use-audio action where creation flow supports it

==================================================
7.12 PROFILE DISCOVERY
======================

Search/profile navigation must gracefully handle:

- deleted users
- suspended users
- unavailable profiles
- private profiles
- blocked users

==================================================
7.13 SEARCH SECURITY
====================

Search result rendering must not assume that all returned resources remain accessible.

A result may become unavailable between:

1. search response
2. user click
3. detail fetch

Handle this race safely.

==================================================
7.14 EXPLORE MODERATION
=======================

If backend provides moderation labels or unavailable states:

- display appropriate user-safe state
- never expose internal moderation metadata
- remove invalid content from local cache

==================================================
7.15 EXPLORE TESTING
====================

Test:

- Explore loading
- pagination
- search
- debounce
- cancellation
- history
- users
- hashtags
- audio
- trending
- private profiles
- unavailable content
- accessibility
- responsive layout

==================================================
MILESTONE 8 — REELS
====================

Implement a high-performance vertical Reels experience.

==================================================
8.1 REELS ROUTE
===============

Create:

- /reels

Support direct opening to a specific reel through the routing model.

==================================================
8.2 VERTICAL FEED
=================

Build vertically paginated reels.

Each reel should occupy the primary viewport.

Use:

- scroll snapping
- viewport detection
- active-item management
- cursor pagination

==================================================
8.3 ACTIVE REEL STATE
=====================

Only the visible active reel should aggressively:

- autoplay
- preload nearby media
- send frequent playback events

Pause inactive videos.

==================================================
8.4 REEL VIDEO PLAYER
=====================

Support:

- autoplay when permitted
- mute/unmute
- play/pause
- progress
- fullscreen
- replay
- buffering
- poster
- error recovery

Respect browser autoplay restrictions.

==================================================
8.5 REEL ENGAGEMENT
===================

Support:

- like
- comment
- share
- save
- follow creator
- view creator profile
- audio
- report

Reuse existing engagement components where possible.

==================================================
8.6 REEL WATCH TRACKING
=======================

Implement watch analytics based on backend expectations.

Support:

- impression
- playback started
- watch duration
- completion
- skipped
- replay

Prevent excessive analytics traffic.

Batch or throttle events where the backend contract supports it.

==================================================
8.7 REEL COMMENTS
=================

Reuse the comment system.

The same comment query/mutation architecture should power reel comments.

Do not create a separate duplicate comment system.

==================================================
8.8 REEL AUDIO
==============

Render audio information.

Support:

- audio title
- creator
- audio page
- reels using audio
- use audio where supported

==================================================
8.9 REEL CREATOR INFORMATION
============================

Render:

- avatar
- username
- verification
- follow state
- caption
- hashtags

Follow interaction must use existing follow mutation architecture.

==================================================
8.10 REEL PRELOADING
====================

Preload only intelligently.

At most:

- active reel
- one or a small controlled number of nearby candidates

Do not preload an entire feed of videos.

==================================================
8.11 REEL NETWORK ADAPTATION
============================

Where browser APIs and architecture permit:

- respect reduced data preferences
- avoid unnecessary high-resolution streams
- use appropriate media variants
- degrade gracefully on slow networks

==================================================
8.12 REEL ERROR STATE
=====================

If video fails:

- show poster if available
- show retry
- allow progression to next reel
- avoid trapping the feed

==================================================
8.13 REEL SCROLL BEHAVIOR
=========================

Scrolling must remain smooth.

Do not trigger heavy React state updates on every scroll event.

Prefer:

- IntersectionObserver
- CSS scroll snapping
- requestAnimationFrame where truly required

==================================================
8.14 REEL ACCESSIBILITY
=======================

Provide accessible controls for:

- play/pause
- mute
- like
- comment
- share
- save
- follow
- close/detail navigation

Do not make important functionality dependent on gestures alone.

==================================================
8.15 REEL TESTING
=================

Test:

- vertical scrolling
- active-item detection
- autoplay restrictions
- pause/resume
- mute
- watch tracking
- like
- comments
- save
- share
- follow
- audio
- loading
- video failure
- pagination
- accessibility
- responsive behavior

==================================================
CROSS-CUTTING CACHE RULES
=========================

Content mutations must update only relevant TanStack Query caches.

Examples:

Like post:

- feed item
- post detail
- profile item if cached

Delete post:

- remove from feed
- remove from profile
- remove from detail
- invalidate affected discovery queries where appropriate

Follow creator:

- profile
- feed author state where applicable
- recommendation state where applicable

Do not blindly invalidate every query.

==================================================
CROSS-CUTTING REALTIME RULES
============================

Where realtime events become available:

- process them centrally
- update query caches
- deduplicate events
- preserve user interaction state
- prevent scroll jumps

Never open separate WebSocket connections per post/card/reel component.

==================================================
CROSS-CUTTING MEDIA RULES
=========================

Always:

- preserve intrinsic dimensions
- use responsive media variants
- avoid unnecessary full-resolution downloads
- lazy-load content outside viewport
- provide poster/fallback
- handle failed media
- clean up media resources when unmounted

==================================================
CROSS-CUTTING PRIVACY RULES
===========================

For every content type:

- use backend visibility
- handle private accounts
- handle blocked users
- handle restrictions
- handle moderation removal
- handle rights restrictions
- handle deletion
- handle account suspension

Never infer permission from cached content alone.

==================================================
CROSS-CUTTING ANALYTICS
=======================

Instrument:

- feed impression
- post impression
- post open
- like
- comment
- save
- share
- story impression
- story completion
- reel impression
- reel watch duration
- reel completion
- search
- hashtag open
- audio open

Do not emit excessive events.

Use stable event names.

Never transmit:

- passwords
- authentication tokens
- private message contents
- sensitive moderation internals
- unnecessary personal data

==================================================
CROSS-CUTTING ERROR STATES
==========================

Every content surface must have:

- loading
- empty
- error
- unavailable
- deleted
- forbidden
- blocked
- retry

Do not show generic errors when a more useful state can be determined safely.

==================================================
PERFORMANCE ACCEPTANCE
======================

The completed volume must avoid:

- duplicate API calls
- excessive query invalidation
- multiple concurrent active videos
- uncontrolled event listeners
- memory leaks
- stale timers
- abandoned media playback
- unnecessary rerenders
- large initial JavaScript bundles

==================================================
ACCESSIBILITY ACCEPTANCE
========================

Verify:

- keyboard navigation
- visible focus
- semantic controls
- screen-reader labels
- media control accessibility
- dialog focus management
- carousel announcements
- reduced motion

==================================================
TESTING REQUIREMENTS
====================

Each milestone must include:

- unit tests
- component tests
- integration tests where applicable
- accessibility tests
- end-to-end tests for critical journeys

Critical user journeys:

1. Open feed.
2. Scroll through posts.
3. Like a post.
4. Save a post.
5. Open comments.
6. Add a comment.
7. Open carousel.
8. Share content.
9. Open story tray.
10. Watch story.
11. Reply to story.
12. Open Explore.
13. Search a user.
14. Open hashtag.
15. Open audio.
16. Watch reels.
17. Like reel.
18. Comment on reel.
19. Follow reel creator.

==================================================
IMPLEMENTATION ORDER
====================

Execute in this exact order:

MILESTONE 5

1. Content models
2. Feed query
3. Feed layout
4. Post components
5. Media renderer
6. Carousel
7. Engagement
8. Comments
9. Sharing
10. Post details
11. Cache synchronization
12. Tests

MILESTONE 6

1. Story models
2. Story tray
3. Story viewer
4. Playback/progress
5. View tracking
6. Replies
7. Reactions
8. Story creation
9. Highlights
10. Tests

MILESTONE 7

1. Explore
2. Discovery grid
3. Search
4. Search history
5. Hashtags
6. Trending
7. Audio discovery
8. Discovery cache handling
9. Tests

MILESTONE 8

1. Reel route
2. Vertical feed
3. Active-item manager
4. Video player
5. Engagement
6. Watch tracking
7. Audio integration
8. Preloading
9. Failure recovery
10. Performance optimization
11. Tests

==================================================
OUTPUT FORMAT
=============

For every implementation step:

1. State the current milestone.
2. State the affected feature.
3. Inspect the current repository.
4. Review the existing frontend and backend contracts.
5. Reuse existing abstractions.
6. Explain only important architectural decisions.
7. Create or modify required files.
8. Output complete contents for every changed/new file.
9. Never output unchanged files.
10. Add tests.
11. Run typecheck/lint/test/build where available.
12. Fix discovered problems before moving forward.
13. Leave the repository buildable.

Do not merely describe components.

Implement them.

==================================================
FINAL ACCEPTANCE CRITERIA
=========================

At the end of this volume:

- the home feed is functional;
- posts render through real backend data;
- carousels work;
- videos work;
- likes work;
- comments work;
- replies work;
- saves work;
- shares work;
- profile content integrates correctly;
- stories work;
- story viewer works;
- story replies/reactions work;
- highlights work;
- Explore works;
- search works;
- search history works;
- hashtags work;
- trending works;
- audio discovery works;
- Reels work;
- vertical video playback works;
- watch tracking works;
- cache synchronization works;
- deletion/moderation/visibility changes propagate correctly;
- accessibility requirements are implemented;
- responsive behavior is implemented;
- performance is acceptable;
- critical tests pass.

Do not begin the remaining notification, messaging, advanced creation, and creator/business frontend features until this volume has been implemented and validated.

BEGIN WITH:

MILESTONE 5 — FEED AND POSTS.
