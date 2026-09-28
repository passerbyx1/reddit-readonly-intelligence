# Reddit Read-Only Intelligence

A personal, non-commercial, single-user, read-only local intelligence tool for organizing and reviewing relevant public Reddit discussions.

> **Current status:** Reddit online API access is **not yet enabled**. The Reddit integration is currently limited to offline schemas, normalization adapters, synthetic test fixtures, and local data-handling logic while official Reddit Data API access is being requested.

## Purpose

The project is designed to reduce repetitive manual searching by organizing a small amount of relevant public Reddit content in a local dashboard.

Reddit is intended to be one optional source in a broader multi-source intelligence workflow. The system may eventually organize information from multiple public sources while preserving the original source identity of each item.

The project is currently:

- Personal
- Non-commercial
- Single-user
- Local-first
- Read-only
- Low-volume
- Not a public search engine
- Not a data resale service
- Not an engagement automation tool

## Intended Reddit Usage

If official access is approved, the application is intended to:

1. Let the user manually define a limited set of topics, keywords, or public subreddits.
2. Retrieve a bounded number of relevant public posts through approved Reddit API endpoints.
3. Normalize public post information into a local structured format.
4. Observe selected publicly available engagement metrics at limited intervals.
5. Cache and deduplicate previously retrieved information locally to reduce unnecessary API requests.
6. Display the resulting information in a local, single-user dashboard.

Initial communities of interest are expected to include a small number of public technology and AI communities, such as:

- `r/artificial`
- `r/LocalLLaMA`
- `r/MachineLearning`

The exact set may change based on the user's personal interests, but the intended scope is narrow rather than site-wide.

## Read-Only by Design

The application will **not** automatically:

- Create posts
- Create comments
- Vote or manipulate karma
- Send direct messages
- Create Reddit accounts
- Perform moderation actions
- Follow or target individual users
- Automate participation in Reddit communities
- Perform unsolicited outreach

Any participation in Reddit discussions will remain a manual action performed by the user directly through Reddit.

## Why Devvit Is Not a Natural Fit

This project is not designed to run inside a subreddit or provide a Reddit-native interactive experience.

It is an external, local, single-user information dashboard with its own:

- Local data organization
- Historical observation model
- Source-independent content model
- Local analytics
- Multi-source architecture

The application does not require subreddit installation, Reddit-hosted UI components, moderator capabilities, custom Reddit buttons, or automated Reddit actions.

For that reason, the intended architecture is better suited to limited, read-only official Reddit Data API access than to an in-Reddit application model.

## High-Level Architecture

```text
Approved Reddit API Access
        ↓
Read-Only Reddit Client
        ↓
Request Queue
        ↓
Rate-Limit Guard
        ↓
Cache / Deduplication
        ↓
Reddit Adapter
        ↓
Local Reddit Dataset
        ↓
Unified Signal Layer
        ↓
Local Intelligence Dashboard
```

The online Reddit client is **not implemented yet**.

## Local Data Model

The project separates stable content identity from changing engagement metrics.

```text
Reddit Post
    ↓
Signal
(content identity and text)

Reddit Metrics
    ↓
Observation
(metric snapshot at a specific time)
```

Examples of planned public metrics include:

- Post score
- Comment count
- Upvote ratio

Changing metrics are stored as observations rather than being treated as permanent content fields.

## Low-Volume API Design

The project is intentionally designed around conservative request behavior.

Planned protections include:

- Bounded collection runs
- Local caching
- Deduplication
- Serialized or conservative request scheduling
- Rate-limit awareness
- Stop/backoff behavior for authorization and rate-limit errors
- No proxy rotation
- No multi-account rotation
- No client rotation intended to bypass limits
- No browser-scraping fallback if official API access fails

Expected initial use is below approximately **500 API requests per day**, with most days expected to be substantially lower.

## Data Handling

Reddit data will be used only for the approved local application purpose.

The project is not intended to:

- Sell Reddit data
- License Reddit data
- Redistribute Reddit data as a bulk dataset
- Build advertising audiences
- Build individual user profiles
- Train machine learning or AI models on Reddit content

Sensitive credentials are never intended to be stored in content datasets.

The following types of information must not be written into Signals, Observations, reports, or dashboard API responses:

- OAuth access tokens
- OAuth refresh tokens
- Client secrets
- Authorization headers
- Cookies
- Passwords
- API keys

## Deleted and Removed Content

The project is designed to be deletion-aware rather than act as a permanent archive of deleted Reddit content.

When content is confirmed as deleted or removed, the intended design is to:

- Stop treating the original content as active
- Remove or redact content fields that should no longer be retained
- Avoid preserving deleted post text or author identity as a hidden archive
- Preserve only minimal, policy-appropriate deletion metadata where permitted
- Keep aggregate deletion statistics where permitted

The project contains an offline **Deletion Intelligence** foundation for studying aggregate deletion behavior without keeping recoverable copies of deleted content.

Examples of aggregate analysis may include:

- Deletion count
- Deletion rate
- Approximate time until deletion detection
- Topic-level deletion trends
- Pre-deletion engagement buckets

The implementation does not create individual user deletion profiles.

## AI Use

The project currently does **not** use Reddit content for production AI processing.

Reddit content will **not** be used to train machine learning or artificial intelligence models.

If future functionality introduces limited summarization, classification, or topic analysis, that functionality will only be introduced after reviewing the applicable Reddit policies and the approved scope of access.

## Current Implementation Status

Completed offline components include:

- Unified Signal schema
- Unified Observation schema
- Metric definitions
- Source registry
- X-to-Signal compatibility adapter
- Offline Reddit Post adapter
- Reddit Observation normalization
- Deletion Event schema
- Tombstone schema
- Deletion policy foundation
- Deletion analytics foundation
- Synthetic fixtures and offline regression tests

Not implemented:

- Reddit OAuth
- Reddit Data API client
- Reddit Search
- Reddit online ingestion
- Reddit background polling
- Reddit comment crawling
- Public Reddit-facing product
- Commercial Reddit data service

## Development Approach

Development intentionally proceeds offline first.

The project uses synthetic fixtures to validate:

- Data normalization
- Missing values
- Deleted/removed states
- Crossposts
- Negative post scores
- Observation semantics
- Deletion handling
- Security boundaries

No production Reddit data collection is required for these tests.

## Privacy and Security Principles

The project follows these design principles:

- Data minimization
- Read-only access
- Narrow scope
- Local-first storage
- Explicit handling of deleted/removed content
- No automated user engagement
- No credential leakage into logs or datasets
- No attempts to bypass Reddit access controls or rate limits

## License / Project Status

This repository currently exists primarily to document the intended Reddit integration and support review of the Data API access request.

The project is personal and non-commercial at this stage.

Any future commercial use, redistribution, or materially expanded Reddit data access would require a separate review of Reddit's applicable policies and permissions.

## Contact

Reddit account: `u/Signal_Use_8060`

For the current Data API request, the project owner is requesting limited, read-only, low-volume access for this local single-user application.
