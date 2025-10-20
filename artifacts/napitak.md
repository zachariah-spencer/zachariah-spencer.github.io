---
layout: page
title: Napitak Game Refactor
permalink: /artifacts/napitak/
---

## Artifact Overview

Napitak is a 2D deck-building roguelike that I began during the SNHU CS-465/CS-499 sequence and have continued evolving as my capstone artifact. The original version (kept on the [`main` branch](https://github.com/zachariah-spencer/napitak/tree/main)) centralized almost all runtime state in a monolithic `Game` class and a massive `globals.rb` hash. For the capstone milestone in September 2025, I revisited the project on the [`capstone-enhancement-refactor` branch](https://github.com/zachariah-spencer/napitak/tree/capstone-enhancement-refactor) to modernize the architecture, data-loading pipeline, and user interface responsiveness.

## Why This Artifact

I selected Napitak because it demonstrates end-to-end ownership of a production-sized codebase and highlights my specialization in software engineering and game systems design. The refactor touches the engine core, data layer, and user interface, showcasing my ability to:

- Restructure legacy code into cohesive, testable service objects (`SceneManager`, `ParticleSystem`, `CameraController`) while shrinking `app/game.rb` from 857 lines down to orchestration logic.
- Transition hard-coded data into JSON datasets (`data/items.json`, `data/encounters.json`, `data/status_effects.json`, etc.), enabling data-driven content updates without recompiling.
- Improve UI/UX polish through reusable widgets, animation pipelines, and audio timing fixes that respond to player input predictably.

These enhancements illustrate my capacity to diagnose architectural pain points, plan iterative improvements, and deliver maintainable solutions that scale with new gameplay content.

## Enhancement Reflection

The enhancement effort focused on dismantling tight coupling inside `Game` and replacing ad-hoc global state with well-defined services. Moving render-, audio-, and scene-management responsibilities into dedicated classes clarified ownership boundaries and eliminated side effects that previously caused race conditions and memory leaks. Converting the global hash into structured JSON files reinforced my comfort with data modeling and serialization while making design trade-offs around load-time parsing versus runtime flexibility. I learned how valuable incremental refactors are—extracting the scene manager first allowed me to prove the pattern before migrating other systems.

One of the most challenging moments was maintaining save compatibility while migrating data sources. I used branch-by-branch smoke tests and log instrumentation to verify that player progression, animations, and audio cues still triggered correctly. Instructor feedback from earlier milestones emphasized the need to rein in global state and improve readability, so I deliberately leaned on dependency injection and small classes to respond to that critique. The work aligns with CS program outcomes in Software Engineering/Design (architecting maintainable systems), Algorithms and Data Structures (optimizing state management and UI event handling), and Databases/Data Management (structuring and querying JSON-backed content). Outcomes involving advanced cybersecurity were not a focus for this artifact.

## Diff Highlights

| Commit | What Changed | Key Impact |
| --- | --- | --- |
| [`35315bd`](https://github.com/zachariah-spencer/napitak/commit/35315bdf1c6d7a42df16c31fdd418a5a25b76697) | Refactored `globals.rb`; moved encounter, item, and animation data into JSON; updated enemy animation classes | 970 insertions / 641 deletions, introducing data-driven content loading and reducing tightly-coupled global hashes. |
| [`39152c9`](https://github.com/zachariah-spencer/napitak/commit/39152c9cf6df976ccc87d5bcb3f5357ab127af80) | Extracted scene, camera, and particle logic into dedicated services | 932 insertions / 780 deletions, shrinking `Game` and enabling single-responsibility components. |
| [`4e931c7`](https://github.com/zachariah-spencer/napitak/commit/4e931c734d46c94cc21a4a39a49b83687473808a) | Broke down `Game#initialize`, standardized naming, and reworked scene classes to follow the new service APIs | 1,010 insertions / 692 deletions across 29 files, aligning every scene with the refactored architecture. |
| [`4d38627`](https://github.com/zachariah-spencer/napitak/commit/4d38627b39d52804c753aeaac4ee6d322b35b9cb) | Added hover animation orchestration for interactive buttons | 33-line touch-up that improves UI responsiveness and leverages the new animation hooks. |
| [`2c38317`](https://github.com/zachariah-spencer/napitak/commit/2c38317ca6c5849020676e7f1b5fa52c585cbf50) | Finalized updated event art assets | Completes the visual refresh so the UI improvements are visible in-game. |

Explore the [full compare view](https://github.com/zachariah-spencer/napitak/compare/main...capstone-enhancement-refactor) for complete diffs between `main` and `capstone-enhancement-refactor`, including UI polish, audio timing fixes, and content additions that support the refactored systems.

## Supporting Materials

- **Code Review Video:** _Add link to capstone code review walkthrough when available._
- **Original Artifact:** [Main branch snapshot](https://github.com/zachariah-spencer/napitak/tree/main)
- **Enhanced Artifact:** [Capstone branch snapshot](https://github.com/zachariah-spencer/napitak/tree/capstone-enhancement-refactor)

Feel free to clone either branch and run `git log main..capstone-enhancement-refactor --oneline` locally to see the full sequence of iterative enhancements that led to the refactored outcome.
