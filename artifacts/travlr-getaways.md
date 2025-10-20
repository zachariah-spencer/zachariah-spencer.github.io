---
layout: page
title: Travlr Getaways Budget Filter
permalink: /artifacts/travlr-getaways/
---

## Artifact Overview

Travlr Getaways is the full-stack travel booking prototype I delivered in SNHU CS-465. The application pairs an Angular admin dashboard with a Node/Express API backed by MongoDB. The original artifact (commit [`4232534`](https://github.com/zachariah-spencer/snhu-cs-465/tree/4232534f1330e653ed958dcc5079d7e340c1d2db), August 2025) provided static trip listings without any user-defined filtering. For my capstone enhancement in October 2025 (commit [`52430c1`](https://github.com/zachariah-spencer/snhu-cs-465/tree/52430c15ce1b59924473066cc9dc428b956309ca)) I implemented a budget-aware query experience that keeps the Angular UI and API in sync.

## Why This Artifact

I included this project because it showcases my specialization in full-stack web development—bridging TypeScript front-ends with resilient Express routes. The enhancement demonstrates:

- A user-facing budget filter that reacts instantly through Angular's two-way binding and shared state management.
- A reusable data-access layer (`TripData`) that now composes HTTP query parameters cleanly with `HttpParams`.
- Hardened API validation in `trips.js`, complete with numeric parsing, graceful error handling, and MongoDB aggregation to compare string-based prices safely.

Together these changes prove my ability to design maintainable REST endpoints, propagate new capabilities through the service layer, and deliver UI feedback that respects UX expectations.

## Enhancement Reflection

Extending the artifact required careful coordination between the Angular component lifecycle and Express controllers. Converting the per-trip price from a stored string into a numeric comparison pushed me to revisit MongoDB's `$convert` and `$expr` operators—reinforcing the importance of defensive data modeling in NoSQL systems. I also learned to streamline Angular messaging by centralizing state updates (`updateMessage`) rather than scattering string concatenation across template bindings.

The largest hurdle was preserving existing behavior while introducing the budget filter. I wrote quick smoke tests against the API to ensure legacy clients still received full result sets, and I instrumented message logging to confirm the new filter states were intuitive. Instructor feedback on earlier iterations urged more robust error responses, which guided the addition of HTTP 400/500 branches and try/catch handling in the controller. This work satisfied CS program outcomes in Software Engineering/Design (modular service abstraction), Algorithms and Data Structures (efficient filtering logic), and Databases (query formulation and validation). Cybersecurity-specific outcomes were not directly addressed in this enhancement.

## Diff Highlights

| Commit | What Changed | Key Impact |
| --- | --- | --- |
| [`52430c1`](https://github.com/zachariah-spencer/snhu-cs-465/commit/52430c15ce1b59924473066cc9dc428b956309ca) | Added Angular budget filter UI (`trip-listing.html`), stateful filtering logic in `TripListing`, and query parameter support in `TripData`. | 144 insertions / 32 deletions across admin UI and service layer; enables real-time filtering and user messaging. |
| [`52430c1`](https://github.com/zachariah-spencer/snhu-cs-465/commit/52430c15ce1b59924473066cc9dc428b956309ca#diff-7e08a5b65787a5395819fb187002046231752e5564c8564a6430ea2cd2a7f04f) | Reworked `trips.js` controller to parse `maxBudget`, validate input, and return targeted MongoDB results. | Introduced defensive error handling and conversion logic so pricing data stored as strings can be filtered numerically. |

Review the [full comparison](https://github.com/zachariah-spencer/snhu-cs-465/compare/4232534f1330e653ed958dcc5079d7e340c1d2db...52430c15ce1b59924473066cc9dc428b956309ca) to explore detailed code differences between the original and enhanced commits.

## Supporting Materials

- **Code Review Video:** _Add link to Travlr Getaways enhancement walkthrough when available._
- **Original Artifact:** [Snapshot at commit 4232534](https://github.com/zachariah-spencer/snhu-cs-465/tree/4232534f1330e653ed958dcc5079d7e340c1d2db)
- **Enhanced Artifact:** [Snapshot at commit 52430c1](https://github.com/zachariah-spencer/snhu-cs-465/tree/52430c15ce1b59924473066cc9dc428b956309ca)
