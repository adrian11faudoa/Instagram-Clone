You are operating in Senior Engineering Team Mode.

You are the Principal Frontend Architect, Staff Frontend Engineer, Staff UI/UX Engineer, Accessibility Engineer, Performance Engineer, Security Engineer, QA Engineer, Realtime Engineer, Data Visualization Engineer, and Technical Writer for this Instagram-like global social platform.

The previous frontend volumes have established:

- frontend architecture
- application shell
- responsive navigation
- design system
- accessibility foundation
- centralized API client
- TanStack Query architecture
- authentication
- session management
- protected routes
- account/profile systems
- follow/follower interactions
- block/restriction workflows
- privacy/security settings foundation
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
- realtime infrastructure
- direct messaging
- message requests
- attachments
- reactions
- replies
- delivery/read state
- presence
- typing indicators
- content creation
- uploads
- drafts
- publishing
- scheduling where supported
- creator/business dashboard foundations
- analytics foundations
- advertising foundations
- commerce foundations
- monetization foundations

This volume continues directly from those implementations.

Do not restart the frontend.

Do not replace working architecture.

Do not regenerate unchanged files.

Do not create fake production functionality.

Do not invent backend contracts.

Use the existing repository and backend contracts as the source of truth.

==================================================
VOLUME 5 SCOPE
==============

Implement:

MILESTONE 13
Advanced creator/business analytics, professional dashboards, monetization management, and financial UI.

MILESTONE 14
Advertising management, campaigns, ad sets, creatives, targeting, budgets, reporting, and ad review workflows.

MILESTONE 15
Commerce management, storefronts, product tagging, checkout/order experiences, and fulfillment interfaces.

MILESTONE 16
Moderation, safety, reports, appeals, copyright/rights management, and account enforcement UX.

==================================================
NON-NEGOTIABLE RULES
====================

Production-grade implementation only.

No pseudo-code.

No placeholders.

No TODOs.

No fake API responses.

No hard-coded production business data.

No client-side calculations that contradict backend-authoritative values.

Every generated file must compile.

Every API request must use the centralized API layer.

Every server-state operation must use TanStack Query.

Use Zustand only for client-owned UI state.

Every sensitive operation must honor backend authorization.

Do not expose private or internal moderation information.

Do not expose payment secrets.

Do not expose advertising account credentials.

Do not expose fraud scores.

Do not expose internal recommendation/ranking details.

==================================================
MILESTONE 13 — ADVANCED CREATOR/BUSINESS ANALYTICS
===================================================

Build the professional analytics experience.

==================================================
13.1 PROFESSIONAL DASHBOARD
===========================

Create a professional dashboard architecture.

Support:

- creator accounts
- business accounts
- professional accounts where supported

Dashboard sections may include:

- Overview
- Content
- Audience
- Reach
- Engagement
- Followers
- Earnings
- Monetization
- Promotions
- Advertising
- Commerce

Only expose sections supported by backend permissions and account capabilities.

==================================================
13.2 DASHBOARD LAYOUT
=====================

Build a responsive dashboard.

Desktop:

- persistent dashboard navigation
- primary content area
- contextual controls

Tablet:

- adaptive navigation

Mobile:

- stacked cards
- horizontally scrollable metric groups
- simplified filtering

Do not force desktop tables onto narrow screens.

==================================================
13.3 DATE RANGE CONTROL
=======================

Create reusable date-range controls.

Support:

- predefined ranges where backend supports them
- custom date range
- comparison period
- timezone-aware display
- loading state
- invalid range handling

The backend remains authoritative for analytics timestamps.

==================================================
13.4 ANALYTICS QUERY ARCHITECTURE
=================================

Build typed TanStack Query hooks for:

- account overview
- content analytics
- audience analytics
- follower growth
- engagement
- reach
- story analytics
- reel analytics
- monetization
- revenue
- promotions
- advertising metrics
- commerce metrics

Use stable query keys.

Query parameters must be normalized consistently.

==================================================
13.5 METRIC CARDS
=================

Create reusable metric-card components.

Each metric may expose:

- current value
- previous-period value
- percentage change
- trend
- date range
- explanatory label

Do not calculate authoritative percentages from rounded values if the backend already provides them.

==================================================
13.6 DATA VISUALIZATION
=======================

Build accessible chart primitives.

Support where backend provides data:

- line charts
- area charts
- bar charts
- stacked bars
- distribution charts

Charts must have:

- accessible labels
- textual summaries
- keyboard-compatible interaction where applicable
- tooltips
- empty states
- loading states
- error states

Never use color as the sole encoding mechanism.

==================================================
13.7 ANALYTICS TABLES
=====================

Build reusable data tables supporting:

- sorting
- filtering
- pagination
- column visibility
- responsive behavior
- loading
- empty
- error

Large datasets must use server-side pagination.

==================================================
13.8 CONTENT PERFORMANCE
========================

Build per-content analytics.

Support metrics such as:

- impressions
- reach
- likes
- comments
- saves
- shares
- profile visits
- watch time
- completion rate

Render only metrics provided by the backend.

==================================================
13.9 STORY ANALYTICS
====================

Support:

- story impressions
- exits
- replies
- interactions
- completion
- navigation behavior

Do not expose viewer identities unless backend explicitly authorizes that view.

==================================================
13.10 REEL ANALYTICS
====================

Support:

- plays
- unique viewers where available
- watch time
- average watch time
- completion
- replays
- likes
- comments
- saves
- shares

Use backend-provided definitions.

==================================================
13.11 FOLLOWER ANALYTICS
========================

Support:

- follower growth
- net growth
- audience activity
- active periods

Respect privacy controls and data availability.

==================================================
13.12 AUDIENCE BREAKDOWNS
=========================

Where supported:

- age ranges
- geographic summaries
- audience categories
- device summaries
- engagement segments

Do not show data that is below backend-defined privacy thresholds.

==================================================
13.13 ANALYTICS EXPORT
======================

Where backend supports export:

- select report
- select date range
- request export
- display processing
- show completion
- download through authorized mechanism

Do not generate exports entirely in the browser when backend exports exist.

==================================================
13.14 MONETIZATION DASHBOARD
============================

Build monetization UI.

Support:

- subscriptions
- memberships
- gifts
- tips
- earnings
- fees
- payout balance
- payout history
- payout status

Do not display financial information to unauthorized users.

==================================================
13.15 EARNINGS BREAKDOWN
========================

Support breakdowns by backend-supported revenue source.

Use:

- metric cards
- tables
- charts

Maintain exact backend monetary values.

==================================================
13.16 PAYOUT UI
===============

Support:

- eligible balance
- pending balance
- payout history
- payout status
- payout request
- payout errors
- payout holds

Never expose provider secrets.

==================================================
13.17 CREATOR SUBSCRIPTIONS
===========================

Where supported, creator-facing management may include:

- plans
- pricing
- subscriber counts
- entitlement status
- subscriber activity
- subscription settings

==================================================
13.18 BUSINESS OVERVIEW
=======================

Business dashboard may expose:

- reach
- engagement
- audience
- campaigns
- commerce
- product performance

==================================================
13.19 CREATOR/BUSINESS PERMISSIONS
==================================

Dashboard access must use backend permissions.

Possible capabilities:

- view analytics
- manage content
- manage ads
- manage products
- view earnings
- request payouts

Never infer capability solely from account type.

==================================================
13.20 ANALYTICS ERROR STATES
============================

Differentiate:

- no data
- insufficient data
- loading
- backend unavailable
- unauthorized
- export processing
- partial metric failure

==================================================
13.21 ANALYTICS PERFORMANCE
===========================

Do not fetch every analytics section simultaneously by default.

Use:

- tab-based fetching
- lazy charts
- selective prefetching
- cached ranges

Large charts should not block the main dashboard.

==================================================
13.22 ANALYTICS TESTING
=======================

Test:

- date ranges
- metric cards
- charts
- tables
- sorting
- pagination
- export
- monetization
- payout state
- permissions
- error states
- responsive rendering
- accessibility

==================================================
MILESTONE 14 — ADVERTISING MANAGEMENT
======================================

Build the advertising management experience on the existing backend contracts.

==================================================
14.1 ADS ROUTE ARCHITECTURE
===========================

Create routes for:

- advertising dashboard
- campaigns
- campaign detail
- create campaign
- edit campaign
- ad sets
- creatives
- reporting
- billing where backend supports it

==================================================
14.2 ADVERTISER ACCESS
======================

Before loading advertiser resources:

- verify authenticated user
- verify advertiser permissions
- load account state

Handle:

- unauthorized
- forbidden
- suspended advertiser
- billing restricted

==================================================
14.3 CAMPAIGN LIST
==================

Build a production data table.

Columns may include:

- name
- status
- objective
- budget
- spend
- impressions
- clicks
- conversions
- start
- end

Use backend-supported metrics.

Support:

- search
- filters
- sorting
- pagination
- bulk selection only when backend explicitly supports it

==================================================
14.4 CAMPAIGN STATUS
====================

Render statuses such as:

- draft
- pending_review
- approved
- active
- paused
- completed
- rejected
- archived

Do not invent transitions on the frontend.

==================================================
14.5 CREATE CAMPAIGN
====================

Build the campaign wizard.

Potential steps:

1. Objective
2. Audience
3. Placement
4. Budget
5. Schedule
6. Creative
7. Review
8. Submit

Only include steps represented in the backend model.

==================================================
14.6 CAMPAIGN DRAFT
===================

Support draft state where backend provides it.

Allow:

- save
- resume
- edit
- discard

Do not lose configuration on route navigation.

==================================================
14.7 TARGETING
==============

Render backend-supported targeting controls.

Potential dimensions:

- geography
- age
- interests
- audience lists
- placements

Do not implement targeting algorithms in the browser.

==================================================
14.8 TARGETING VALIDATION
=========================

Display server validation errors.

Do not silently alter targeting.

Conflicting targeting conditions should be represented explicitly.

==================================================
14.9 BUDGET
===========

Support backend-defined:

- daily budget
- lifetime budget
- currency
- start/end dates

Use decimal-safe values.

Do not perform inaccurate monetary calculations with binary floating-point logic.

==================================================
14.10 AD SCHEDULE
=================

Support:

- start
- end
- timezone
- always-on where supported

Use backend date/time validation.

==================================================
14.11 CREATIVE MANAGEMENT
=========================

Support:

- image creative
- video creative
- copy
- headline
- destination
- preview

Use existing media upload architecture.

==================================================
14.12 CREATIVE PREVIEW
======================

Create previews for supported placements.

Do not render a placement preview that contradicts backend-supported dimensions.

==================================================
14.13 CREATIVE VALIDATION
=========================

Handle:

- invalid media
- dimensions
- file size
- unsupported format
- content policy rejection
- missing required metadata

==================================================
14.14 AD REVIEW
===============

Where backend exposes review state:

- pending
- approved
- rejected

Display user-safe reason information.

Never expose internal moderation rules.

==================================================
14.15 AD REPORTING
==================

Build advertiser reporting.

Support:

- date range
- spend
- impressions
- clicks
- CTR where backend defines it
- conversions
- campaign comparison
- ad set comparison
- creative comparison

==================================================
14.16 ADS DASHBOARD CHARTS
==========================

Reuse analytics chart primitives.

Do not create a second charting system.

==================================================
14.17 BILLING UI
================

Where backend supports billing:

- account billing status
- payment method metadata
- invoices
- spend
- billing errors

Never expose full payment credentials.

==================================================
14.18 AD EVENTS
===============

Do not send raw advertising business data to generic client analytics if it creates duplication or privacy concerns.

Use dedicated advertising event contracts where established.

==================================================
14.19 AD TESTING
================

Test:

- campaign listing
- filtering
- sorting
- campaign creation
- targeting
- budgets
- schedules
- creative upload
- preview
- approval/rejection states
- reporting
- permissions
- billing state

==================================================
MILESTONE 15 — COMMERCE FRONTEND
=================================

Build commerce management and consumer-facing shopping interfaces.

==================================================
15.1 STOREFRONT EXPERIENCE
==========================

Support business storefront routes where backend provides them.

Render:

- business profile
- product collections
- products
- product cards
- product detail
- prices
- variants
- availability

==================================================
15.2 PRODUCT CARD
=================

Create reusable product card.

Support:

- media
- title
- price
- sale information where backend provides it
- availability
- product tags

==================================================
15.3 PRODUCT DETAIL
===================

Support:

- product media
- title
- description
- variants
- price
- availability
- seller information
- collection
- supported purchase actions

==================================================
15.4 PRODUCT TAGS
=================

Render product tags on supported:

- posts
- reels
- stories

Clicking a tag opens product information without exposing private seller information.

==================================================
15.5 PRODUCT TAGGING MANAGEMENT
===============================

For authorized creators/business users:

- add product tag
- remove product tag
- reposition tag where backend supports coordinates
- preview tagged content

==================================================
15.6 PRODUCT CATALOG
====================

Build merchant catalog management.

Support:

- list
- create
- edit
- archive
- availability
- collections
- variants

==================================================
15.7 PRODUCT CREATION
=====================

Support backend-defined:

- title
- description
- images
- price
- currency
- variants
- collection
- inventory reference
- status

==================================================
15.8 PRODUCT MEDIA
==================

Reuse media upload architecture.

Support:

- upload
- progress
- cancel
- retry
- reorder
- remove
- preview

==================================================
15.9 PRODUCT VARIANTS
=====================

Support backend-defined variant attributes.

Examples:

- size
- color
- style

Do not hard-code retail-specific variant dimensions if backend supports arbitrary attributes.

==================================================
15.10 COLLECTIONS
=================

Support:

- create
- rename
- reorder
- add/remove products
- delete/archive

Use server state.

==================================================
15.11 CART
==========

Where backend supports cart functionality:

- add product
- update quantity
- remove item
- clear cart
- availability validation

The backend remains authoritative for price and inventory.

==================================================
15.12 CHECKOUT
==============

Build checkout UX only around backend-supported contracts.

Support:

- order summary
- shipping information where applicable
- totals
- taxes where supplied
- discounts where supplied
- payment handoff
- confirmation

Never calculate final checkout totals locally as authoritative.

==================================================
15.13 PAYMENT HANDOFF
=====================

Use provider-neutral payment interfaces.

Do not collect payment credentials directly unless the established provider integration explicitly requires secure hosted/embedded payment UI.

Never store raw card data.

==================================================
15.14 ORDER CONFIRMATION
========================

After successful checkout:

- show confirmation
- order reference
- status
- items
- totals
- next steps

Do not assume payment success solely because a client payment widget returned a success callback.

Wait for backend confirmation.

==================================================
15.15 ORDERS
============

Where supported, build:

- order history
- order detail
- payment state
- fulfillment
- shipment
- returns
- refunds
- cancellation

==================================================
15.16 ORDER STATE
=================

Render backend-defined state transitions.

Do not permit arbitrary client-side transitions.

==================================================
15.17 INVENTORY
===============

Merchant inventory UI may display:

- available
- reserved
- unavailable

Do not make inventory authoritative from client cache.

==================================================
15.18 COMMERCE ERRORS
=====================

Handle:

- out of stock
- price changed
- payment failed
- inventory reservation expired
- seller unavailable
- order unavailable

Provide clear recovery actions.

==================================================
15.19 COMMERCE TESTING
======================

Test:

- storefront
- product
- product tag
- catalog
- variants
- collections
- cart
- checkout
- payment handoff
- order confirmation
- order history
- order state
- refund/return states
- out-of-stock behavior
- permissions

==================================================
MILESTONE 16 — MODERATION, SAFETY, RIGHTS, AND ENFORCEMENT UX
==============================================================

Build the user-facing and authorized professional interfaces for safety workflows.

==================================================
16.1 REPORT FLOW
================

Create reusable report dialog.

Support backend-defined categories.

Examples:

- spam
- harassment
- impersonation
- dangerous content
- intellectual-property issue
- unwanted content
- other

Do not expose internal moderation taxonomy.

==================================================
16.2 REPORT TARGET
==================

Reports may target:

- post
- reel
- story
- comment
- profile
- message where supported
- product
- advertisement

Use a generic report infrastructure with typed target references.

==================================================
16.3 REPORT SUBMISSION
======================

Support:

- category
- optional details
- submission
- success
- rate limit
- already reported state
- failure

Prevent duplicate submissions where backend provides idempotency semantics.

==================================================
16.4 USER BLOCK/RESTRICT
========================

Integrate existing block/restrict actions throughout:

- profiles
- posts
- comments
- messages

After successful blocking:

- invalidate affected private queries
- close inaccessible dialogs
- remove inaccessible content from visible lists where appropriate

==================================================
16.5 CONTENT NOT AVAILABLE
==========================

Create reusable unavailable-content component.

States may include:

- deleted
- removed
- blocked
- private
- restricted
- region unavailable
- rights unavailable
- account unavailable

Do not expose internal reason codes.

==================================================
16.6 MODERATION ACTIONS
=======================

Authorized professional users may view supported moderation workflows.

Examples:

- moderation case
- queue
- action
- appeal
- review state

Do not expose moderation interfaces to ordinary users.

==================================================
16.7 MODERATION DASHBOARD
=========================

Where backend supports administrative moderation UI:

- queue
- filters
- case detail
- content preview
- report summary
- moderation history
- action controls

Every action must require backend authorization.

==================================================
16.8 CASE DETAIL
================

Display:

- case ID
- target
- reports
- current status
- previous actions
- appeal state

Do not display hidden security information unnecessarily.

==================================================
16.9 MODERATION ACTIONS UI
==========================

Support backend-defined actions:

- no action
- warning
- content restriction
- content removal
- account restriction
- account suspension
- account restoration

Never allow arbitrary action submission.

==================================================
16.10 APPEALS
=============

Build appeal UX.

Support:

- eligible appeal
- submit appeal
- appeal text where supported
- status
- review result
- closed state

Do not expose internal reviewer information unless explicitly supported.

==================================================
16.11 COPYRIGHT / RIGHTS REPORTING
==================================

Build user-facing rights-related report flows.

Support backend-defined:

- copyright claim
- rights complaint
- counter-notice
- takedown state
- restoration state

Do not provide legal conclusions beyond backend-provided workflow state.

==================================================
16.12 RIGHTS DASHBOARD
======================

For authorized rights-management users:

- claims
- content
- policy state
- region restrictions
- takedowns
- appeals

==================================================
16.13 RIGHTS CONTENT PREVIEW
============================

Preview affected media only if the authenticated user has permission.

Handle unavailable media gracefully.

==================================================
16.14 ENFORCEMENT NOTICES
=========================

Create user-facing notices for:

- warning
- content removal
- temporary restriction
- account suspension
- restoration
- appeal outcome

Use clear language.

Do not reveal internal detection systems.

==================================================
16.15 SAFETY SETTINGS
=====================

Where supported:

- sensitive-content preferences
- interaction limits
- mention controls
- tagging controls
- message controls

Use backend-authoritative values.

==================================================
16.16 MODERATION PRIVACY
========================

Never put:

- internal fraud scores
- internal trust scores
- reviewer notes
- private moderation rules
- internal detection signals

into standard client analytics.

==================================================
16.17 MODERATION TESTING
========================

Test:

- report flow
- duplicate report
- rate limiting
- block
- restrict
- unavailable content
- authorized moderation access
- unauthorized moderation access
- case review
- enforcement actions
- appeals
- rights complaint
- takedown
- restoration

==================================================
CROSS-CUTTING DATA FETCHING
===========================

Every large collection must use:

- cursor pagination where backend provides it
- bounded page size
- stable query keys
- targeted cache invalidation

Avoid loading huge administrative datasets into the browser.

==================================================
CROSS-CUTTING TABLE UX
======================

All professional tables must support:

- loading skeleton
- empty state
- error
- retry
- server pagination
- sorting where backend supports it
- filters
- responsive fallback

On mobile, transform tables into cards or horizontally scrollable accessible structures where appropriate.

==================================================
CROSS-CUTTING CHART UX
======================

Every chart must provide:

- accessible title
- text summary
- no-data state
- loading state
- error state
- tooltip
- responsive layout

Do not encode critical meaning only in color.

==================================================
CROSS-CUTTING FINANCIAL SAFETY
==============================

All monetary amounts must be displayed from backend-authoritative decimal values.

Do not use JavaScript floating-point arithmetic for accounting calculations.

Where client-side calculations are unavoidable for presentation, use safe decimal handling consistent with backend contract.

Never treat UI totals as final authoritative transaction values.

==================================================
CROSS-CUTTING PERMISSION SAFETY
===============================

Every privileged area must handle:

- 401
- 403
- suspended account
- unavailable resource
- expired session

Do not merely hide UI controls and assume that makes the operation secure.

==================================================
CROSS-CUTTING REALTIME
======================

Where realtime events exist:

- update affected analytics states
- update campaign status
- update order state
- update moderation case state
- update payout state
- prevent duplicate updates

Do not introduce separate realtime connection managers.

==================================================
CROSS-CUTTING ACCESSIBILITY
===========================

Every professional workflow must support:

- keyboard navigation
- screen readers
- focus states
- semantic forms
- accessible tables
- accessible charts
- accessible dialogs
- accessible alerts

==================================================
CROSS-CUTTING RESPONSIVE DESIGN
===============================

Every area must work across:

- mobile
- tablet
- desktop
- large desktop

Professional interfaces should adapt instead of simply shrinking.

==================================================
CROSS-CUTTING ERROR HANDLING
============================

Handle:

- validation
- authorization
- conflict
- rate limit
- unavailable resource
- network error
- server error
- timeout

Preserve recoverable user-entered state where possible.

==================================================
CROSS-CUTTING ANALYTICS
=======================

Track safe high-level product interactions:

- dashboard opened
- report started
- report submitted
- campaign creation started
- campaign submitted
- product creation started
- checkout started
- checkout completed
- creator analytics viewed
- payout flow started

Do not track:

- passwords
- payment credentials
- private message contents
- internal moderation decisions
- sensitive financial identifiers

==================================================
TESTING STRATEGY
================

Every milestone must include:

- unit tests
- component tests
- integration tests
- accessibility tests
- end-to-end tests

Critical end-to-end workflows:

1. Creator opens professional dashboard.
2. Creator changes analytics date range.
3. Creator views content performance.
4. Creator views earnings.
5. Creator requests supported payout.
6. Advertiser creates campaign.
7. Advertiser configures targeting.
8. Advertiser uploads creative.
9. Advertiser submits campaign.
10. Advertiser views campaign report.
11. Merchant opens storefront.
12. Merchant creates product.
13. Merchant tags product.
14. Customer opens product.
15. Customer adds item to cart where supported.
16. Customer proceeds through checkout.
17. Customer views order confirmation.
18. User reports content.
19. User blocks another account.
20. Authorized moderator reviews case.
21. User submits appeal.
22. Authorized rights user reviews claim.

==================================================
PERFORMANCE REQUIREMENTS
========================

Professional dashboards must:

- lazy-load secondary sections
- avoid fetching every report simultaneously
- cache repeated date-range requests
- avoid unnecessary chart rerenders
- paginate large tables
- virtualize large datasets only when measurements justify it

==================================================
SECURITY REQUIREMENTS
=====================

Sensitive areas must:

- enforce backend authorization
- avoid exposing secret values
- avoid unsafe redirects
- avoid storing payment credentials
- sanitize untrusted content
- prevent XSS
- prevent accidental analytics leakage

==================================================
IMPLEMENTATION ORDER
====================

Execute exactly in this order:

MILESTONE 13

1. Professional dashboard
2. Analytics queries
3. Date ranges
4. Metric cards
5. Charts
6. Tables
7. Content insights
8. Story/reel insights
9. Audience analytics
10. Monetization
11. Payout UI
12. Tests

MILESTONE 14

1. Advertising routes
2. Advertiser access
3. Campaign list
4. Campaign detail
5. Campaign wizard
6. Targeting
7. Budget
8. Scheduling
9. Creative management
10. Review states
11. Reporting
12. Billing UI
13. Tests

MILESTONE 15

1. Storefront
2. Product cards
3. Product details
4. Product tags
5. Product management
6. Variants
7. Collections
8. Cart
9. Checkout
10. Payment handoff
11. Orders
12. Fulfillment/returns/refunds
13. Tests

MILESTONE 16

1. Report flow
2. Block/restrict integration
3. Unavailable content
4. Moderation dashboard
5. Case detail
6. Moderation actions
7. Appeals
8. Rights workflows
9. Enforcement notices
10. Safety settings
11. Tests

==================================================
OUTPUT FORMAT
=============

Before modifying files:

1. Inspect the current repository.
2. Determine what previous frontend volumes already implemented.
3. Reuse existing components, hooks, API clients, query factories, realtime infrastructure, upload systems, and design tokens.
4. Verify existing backend contracts.
5. Do not duplicate existing abstractions.

For every implementation step:

1. State the current milestone.
2. State the affected feature/domain.
3. Briefly explain important architectural decisions.
4. Create or modify only required files.
5. Output complete contents for every changed/new file.
6. Never output unchanged files.
7. Add tests with implementation.
8. Run typecheck/lint/test/build where available.
9. Fix discovered issues before proceeding.
10. Keep the repository buildable.

Do not merely describe the implementation.

Actually implement it.

==================================================
FINAL ACCEPTANCE CRITERIA
=========================

At the end of this volume:

- creator analytics work;
- business analytics work;
- professional dashboards work;
- charts work;
- tables work;
- analytics filtering works;
- monetization UI works;
- payout UI works;
- advertising management works;
- campaign creation works;
- targeting works;
- creative management works;
- advertising reporting works;
- commerce storefronts work;
- products work;
- variants work;
- collections work;
- product tagging works;
- cart works where supported;
- checkout works where supported;
- order views work;
- fulfillment/returns/refunds states work where supported;
- report flows work;
- block/restrict integration works;
- authorized moderation workflows work;
- appeals work;
- rights workflows work;
- enforcement notices work;
- accessibility requirements are satisfied;
- responsive behavior is implemented;
- security requirements are satisfied;
- critical tests pass;
- TypeScript passes;
- lint passes;
- production build passes.

Do not begin infrastructure/deployment implementation in this volume.

The next frontend volume should focus on final platform-wide integration, advanced settings/privacy/data controls, admin interfaces, experimentation, performance hardening, accessibility auditing, SEO/public surfaces, and final production readiness.

BEGIN WITH:

MILESTONE 13 — ADVANCED CREATOR/BUSINESS ANALYTICS.
