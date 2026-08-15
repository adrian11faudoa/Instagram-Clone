Using the approved Architecture Blueprint — Volume 1, the approved Architecture Blueprint — Volume 2, the approved Backend Blueprint, and the Master Prompt above.

Begin frontend and mobile implementation ONLY.

Do NOT generate backend business logic.

Do NOT generate infrastructure code.

Do NOT redesign the approved architecture.

Do NOT redesign API contracts, authentication flows, authorization rules, database models, event contracts, or service boundaries.

Assume the backend APIs and contracts have been approved.

Consume them exactly as specified.

Generate production-ready web and mobile applications incrementally according to the Master Prompt milestone strategy.

────────────────────────────────────────

MISSION

Build world-class web and mobile applications for a global visual-first social media and creator platform.

The applications must support:

• Photos

• Carousels

• Posts

• Short-form Video

• Reels

• Stories

• Highlights

• Live Streaming

• User Profiles

• Creator Profiles

• Professional Accounts

• Business Accounts

• Social Graph

• Following

• Feed Discovery

• Explore

• Search

• Comments

• Likes and Reactions

• Bookmarks

• Collections

• Direct Messaging

• Notifications

• Creator Tools

• Business Tools

• Commerce

• Advertising

• Moderation

• Administration

• AI-ready experiences

Generate:

• Consumer Mobile App for iOS and Android

• Consumer Web App

• Creator Studio

• Business Dashboard

• Advertising Manager

• Administration Dashboard

• Moderation Dashboard

• Shared Design System

• Shared UI Component Library

• Shared API SDK

────────────────────────────────────────

TECHNOLOGY STACK

Web

• Next.js 15

• React 19

• TypeScript

• Tailwind CSS

Mobile

• React Native

• Expo

• TypeScript

Navigation

• React Navigation

State Management

• Zustand

Server State

• TanStack Query

Forms

• React Hook Form

• Zod

Animations

• React Native Reanimated

• React Native Gesture Handler

• Moti

• Framer Motion for web

Lists

• FlashList

Media

• Expo Image

• Expo Video or the approved current Expo video architecture

Storage

• MMKV

• Expo SecureStore

Notifications

• Expo Notifications

Testing

• Unit tests

• Component tests

• Integration tests

• E2E test architecture

────────────────────────────────────────

FRONTEND ARCHITECTURE

Strictly follow:

• Clean Architecture where appropriate for frontend boundaries

• Feature-first organization

• Strict TypeScript

• SOLID principles

• Reusable components

• Shared design tokens

• Shared UI primitives

• Separation of presentation, state, and API logic

• Accessible components

• Responsive design

• Offline-aware architecture

• Performance-oriented rendering

• Error isolation

• Feature flags

Do not create tightly coupled screen implementations.

────────────────────────────────────────

APPLICATION STRUCTURE

Generate and maintain:

Consumer Mobile App

Consumer Web App

Creator Studio

Business Dashboard

Advertising Manager

Administration Dashboard

Moderation Dashboard

Shared Design System

Shared UI Components

Shared Hooks

Shared Utilities

Shared Types

Shared API SDK

Shared Authentication Utilities

Shared Analytics Utilities

Shared Feature Flag Utilities

────────────────────────────────────────

AUTHENTICATION EXPERIENCE

Implement:

• Registration

• Login

• Logout

• Email verification

• Password reset

• OAuth flows according to backend contracts

• Session restoration

• Token refresh handling

• Device-aware sessions

• Secure credential storage

• Suspicious login handling

• Multi-factor authentication readiness

• Passkey readiness

• Role-aware routing

• Authentication loading states

• Authentication error states

────────────────────────────────────────

ONBOARDING

Implement a complete onboarding experience supporting:

• Account creation

• Username selection

• Profile setup

• Avatar selection

• Interest selection

• Suggested accounts

• Privacy preferences

• Notification permissions

• Contact discovery where approved

• Creator or professional account setup

• Business account setup

• Progressive onboarding

────────────────────────────────────────

HOME EXPERIENCE

Implement:

• Personalized Home Feed

• Following Feed

• Feed switching

• Infinite scrolling

• Cursor pagination

• Pull-to-refresh

• Optimistic engagement updates

• Feed caching

• Background refresh

• New-content indicators

• Skeleton loading

• Empty states

• Error states

• Retry behavior

• Sponsored-content presentation according to approved ad contracts

────────────────────────────────────────

POST EXPERIENCE

Implement interfaces for:

• Single-image posts

• Carousel posts

• Video posts

• Captions

• Expandable text

• Mentions

• Hashtags

• Tagged users

• Location metadata

• Collaboration indicators

• Branded content indicators

• Like actions

• Reactions where supported

• Comments

• Save actions

• Share actions

• Report actions

• Post menus

• Privacy-aware visibility

────────────────────────────────────────

POST CREATION

Implement:

• Camera integration where supported

• Media picker

• Multi-media selection

• Crop tools

• Image preview

• Video preview

• Caption editing

• Hashtag entry

• User mentions

• Location selection

• User tagging

• Collaboration selection

• Accessibility descriptions

• Draft saving

• Scheduled publishing where supported

• Upload progress

• Retry failed uploads

• Background upload handling where platform capabilities allow

• Processing states

────────────────────────────────────────

STORIES

Implement:

• Story tray

• Story viewer

• Automatic progression

• Tap navigation

• Gesture navigation

• Pause and resume

• Story replies

• Reactions

• Close Friends indicators

• Viewer lists where authorized

• Story creation

• Photo stories

• Video stories

• Story privacy selection

• Upload progress

• Expiration-aware UI

• Error recovery

────────────────────────────────────────

HIGHLIGHTS

Implement:

• Highlight groups

• Highlight viewer

• Profile highlight management

• Highlight covers

• Highlight ordering

• Add and remove stories

────────────────────────────────────────

REELS

Implement:

• Full-screen vertical feed

• High-performance video playback

• Preloading

• Prefetching

• Buffer management

• Viewability tracking

• Like actions

• Comments

• Save actions

• Share actions

• Follow actions

• Audio metadata

• Creator information

• Captions

• Hashtags

• Recommended content

• Loading states

• Error recovery

• Reduced-motion support

• Battery-conscious behavior

────────────────────────────────────────

EXPLORE

Implement:

• Personalized discovery grid

• Trending content

• Reels discovery

• Creator discovery

• Hashtag discovery

• Category browsing

• Search entry point

• Infinite loading

• Responsive layouts

• Recommendation explanations where supported

────────────────────────────────────────

SEARCH

Implement:

• User search

• Creator search

• Business search

• Post search

• Reel search

• Hashtag search

• Location search

• Recent searches

• Search suggestions

• Autocomplete

• Filters

• Result categories

• Empty states

• Loading states

• Retry states

────────────────────────────────────────

PROFILE EXPERIENCE

Implement:

• User profiles

• Creator profiles

• Professional profiles

• Business profiles

• Avatar

• Bio

• Links

• Verification indicators

• Follower counts

• Following counts

• Relationship state

• Follow requests

• Follow and unfollow actions

• Block and mute controls

• Profile content tabs

• Posts

• Reels

• Tagged content

• Saved content where private

• Highlights

• Creator information

• Business information

────────────────────────────────────────

SOCIAL GRAPH EXPERIENCE

Implement:

• Followers list

• Following list

• Follow requests

• Suggested accounts

• Close Friends management

• Blocked users

• Muted users

• Privacy-aware UI

• Relationship state synchronization

────────────────────────────────────────

COMMENTS

Implement:

• Comment sheets or dedicated views

• Threaded replies

• Comment creation

• Mentions

• Edit where supported

• Delete

• Report

• Pagination

• Optimistic updates

• Moderation states

• Loading and error states

────────────────────────────────────────

BOOKMARKS AND COLLECTIONS

Implement:

• Save and unsave content

• Saved-content views

• Collection creation

• Collection management

• Add and remove content

• Private collection handling

• Empty states

────────────────────────────────────────

DIRECT MESSAGING

Implement:

• Conversation list

• One-to-one conversations

• Group conversations

• Real-time messages

• Message pagination

• Typing indicators

• Read receipts

• Delivery indicators

• Presence indicators

• Text messages

• Image messages

• Video messages

• Voice messages

• GIFs

• Stickers

• Emoji reactions

• Reply interactions

• Conversation search

• Connection recovery

• Offline states

• Message retry

────────────────────────────────────────

NOTIFICATIONS

Implement:

• Notification center

• Read and unread states

• Follow notifications

• Like notifications

• Comment notifications

• Mention notifications

• Message notifications

• Story notifications

• Live notifications

• Creator notifications

• Business notifications

• Deep links

• Notification preferences

────────────────────────────────────────

LIVE STREAMING

Implement user interfaces for:

• Live broadcast setup

• Live viewer

• Live chat

• Viewer count

• Reactions

• Comments

• Pinned comments

• Host information

• Multi-host readiness

• Moderation controls

• Stream status

• Connection quality indicators

• Replay discovery

Keep streaming client implementation aligned with approved backend and media architecture.

────────────────────────────────────────

CREATOR STUDIO

Implement:

• Creator Dashboard

• Content management

• Post management

• Reel management

• Story insights

• Audience insights

• Engagement analytics

• Content analytics

• Growth analytics

• Revenue analytics where supported

• Content scheduling

• Draft management

• Brand partnerships

• Campaign participation

• Creator settings

────────────────────────────────────────

BUSINESS DASHBOARD

Implement:

• Business overview

• Profile management

• Team and role management

• Verification workflows

• Content management

• Promotions

• Product catalog integration

• Leads

• Analytics

• Settings

────────────────────────────────────────

COMMERCE EXPERIENCE

Implement interfaces for:

• Product tagging

• Product details

• Product collections

• Merchant pages

• Shopping content

• Promotional content

• Checkout handoff according to approved backend contracts

Never duplicate backend commerce rules in the frontend.

────────────────────────────────────────

ADVERTISING MANAGER

Implement:

• Advertiser dashboard

• Campaign creation

• Campaign management

• Ad groups

• Audience configuration

• Budget configuration

• Schedule configuration

• Creative management

• Performance dashboards

• Delivery metrics

• Engagement metrics

• Conversion metrics where supported

• Billing views according to approved contracts

────────────────────────────────────────

ADMINISTRATION DASHBOARD

Implement:

• Administrative authentication

• Role-aware navigation

• User management

• Verification management

• Content management

• Business management

• Creator management

• Feature flag management

• Audit log viewer

• Platform health views where approved

────────────────────────────────────────

MODERATION DASHBOARD

Implement:

• Moderation queues

• Report details

• User history

• Content review

• Media preview

• Enforcement actions

• Account restrictions

• Appeals

• Moderator notes

• Audit trails

• Filtering

• Assignment workflows

────────────────────────────────────────

STATE MANAGEMENT

Use Zustand only for appropriate client-side state.

Implement stores for:

• Authentication

• Session state

• User preferences

• Theme

• Feed UI state

• Media creation drafts

• Upload state

• Messaging UI state where appropriate

• Notification preferences

• Feature flags

Avoid duplicating server state inside Zustand when TanStack Query is appropriate.

────────────────────────────────────────

SERVER STATE

Use TanStack Query for:

• API caching

• Cursor pagination

• Infinite queries

• Background refetching

• Optimistic updates

• Retry behavior

• Mutation state

• Cache invalidation

• Persistence where appropriate

• Offline-aware behavior

────────────────────────────────────────

API SDK

Generate a fully typed API integration layer.

Implement:

• HTTP client

• Authentication interceptors

• Token refresh handling

• Request correlation headers

• Error normalization

• Retry behavior

• Pagination helpers

• Typed request models

• Typed response models

• Query hooks

• Mutation hooks

• WebSocket client integration

Consume approved API contracts without recreating backend business logic.

────────────────────────────────────────

MEDIA PERFORMANCE

Optimize:

• Image loading

• Image caching

• Responsive image selection

• Video preloading

• Video caching where appropriate

• Feed virtualization

• Memory usage

• Network usage

• Battery consumption

• Upload concurrency

• Background uploads

• Failed upload recovery

────────────────────────────────────────

OFFLINE SUPPORT

Implement where technically appropriate:

• Cached feeds

• Cached profiles

• Saved content

• Drafts

• Pending uploads

• Pending mutations

• Message synchronization

• Offline indicators

• Retry queues

• Conflict handling

• Connectivity recovery

Do not claim full offline functionality where backend contracts or platform limitations do not support it.

────────────────────────────────────────

ACCESSIBILITY

Implement WCAG 2.2 AA-oriented accessibility across web and mobile.

Support:

• Screen readers

• VoiceOver

• TalkBack

• Keyboard navigation

• Focus management

• Semantic labels

• Dynamic text

• Reduced motion

• High contrast where supported

• Accessible media controls

• Accessible error messages

────────────────────────────────────────

RESPONSIVE DESIGN

Support:

• Small phones

• Large phones

• Tablets

• Desktop

• Large desktop displays

• Portrait

• Landscape

• Responsive creator and business dashboards

────────────────────────────────────────

THEMING

Implement:

• Light theme

• Dark theme

• System theme

• Shared design tokens

• Consistent spacing

• Typography scales

• Elevation tokens

• Motion preferences

Do not hardcode design values throughout unrelated components.

────────────────────────────────────────

ANIMATIONS

Use the approved animation stack for:

• Navigation transitions

• Feed interactions

• Like animations

• Story transitions

• Reels interactions

• Bottom sheets

• Modals

• Upload progress

• Loading states

• Micro-interactions

Respect reduced-motion preferences.

────────────────────────────────────────

ERROR HANDLING

Implement:

• Error boundaries

• Screen-level error states

• Component-level recovery where appropriate

• Network error handling

• Authentication expiration handling

• Permission-denied states

• Upload failures

• Media processing states

• Empty states

• Maintenance states

• Retry actions

────────────────────────────────────────

FEATURE FLAGS

Implement client-side feature flag integration supporting:

• Safe feature evaluation

• Environment awareness

• User targeting supplied by approved contracts

• Percentage rollout support

• Fallback behavior

• Flag loading states

• Analytics hooks

Never expose secret flag-management credentials to client applications.

────────────────────────────────────────

ANALYTICS

Implement client analytics hooks for approved events including:

• Screen views

• Feed impressions

• Post views

• Video starts

• Video completion

• Story views

• Search interactions

• Engagement actions

• Notification interactions

• Creator interactions

• Advertising interactions

Respect privacy settings and approved consent requirements.

────────────────────────────────────────

AI-READY USER EXPERIENCE

Prepare modular interfaces for future capabilities including:

• AI-assisted content discovery

• Natural-language search

• Creator assistant

• Caption suggestions

• Hashtag suggestions

• Content recommendations

• Accessibility caption generation

• AI moderation explanations where approved

• AI settings

• AI consent controls

Do not hardcode any specific model provider into core UI architecture.

────────────────────────────────────────

PERFORMANCE REQUIREMENTS

Optimize for:

• Fast startup

• Minimal unnecessary re-renders

• Virtualized lists

• Image caching

• Efficient video playback

• Lazy loading

• Code splitting

• Route-level splitting

• Background prefetching

• Memory safety

• Battery efficiency

• Low-bandwidth resilience

────────────────────────────────────────

SECURITY

Implement frontend security practices including:

• Secure token storage

• No secrets in client bundles

• Input validation

• Safe URL handling

• Deep-link validation

• XSS-aware rendering on web

• Secure authentication flows

• Session expiration handling

• Privacy-aware analytics

• Dependency security awareness

────────────────────────────────────────

TESTING

Generate:

• Unit tests

• Component tests

• Feature integration tests

• API integration tests

• Authentication tests

• Feed tests

• Post creation tests

• Media upload tests

• Story tests

• Reels tests

• Messaging tests

• Notification tests

• Accessibility tests

• Responsive tests

• E2E architecture

• Visual regression architecture where appropriate

────────────────────────────────────────

DOCUMENTATION

Generate:

• Frontend architecture documentation

• Mobile architecture documentation

• Design system documentation

• Component documentation

• Navigation guide

• State management guide

• API integration guide

• Authentication integration guide

• Testing guide

• Developer onboarding guide

────────────────────────────────────────

PROJECT ORGANIZATION

Maintain throughout implementation:

Current Milestone

Generated Applications

Generated Screens

Generated Components

Generated Features

API Integrations

State Stores

Query Modules

Remaining Work

Dependencies

Next File

────────────────────────────────────────

OUTPUT FORMAT

For every generated file provide:

1. Exact file path
2. Complete file contents

Never generate pseudo-code.

Never generate placeholders.

Never generate TODO comments.

Never omit implementations.

Never say:

• "implement similarly"

• "left as an exercise"

• "for brevity"

• "remaining code omitted"

Every generated file must integrate with previously generated files.

Do not regenerate unchanged files.

Only modify files when required.

────────────────────────────────────────

STOP CONDITIONS

Generate the frontend and mobile applications incrementally according to the Master Prompt.

Each milestone should contain approximately 20–40 files.

At the end of every milestone:

• Verify TypeScript compilation and integration consistency.

• Update the project index.

• List completed applications.

• List completed screens and features.

• List completed API integrations.

• Identify the exact next file or logical implementation unit.

STOP and wait for approval before generating the next milestone.
