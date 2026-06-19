# Scroll-driven animations understood

The user completed Lesson 23 covering: the two timeline types (scroll() for scroll progress, view() for element visibility), animation-timeline property, how it replaces the time-based timeline with scroll position, scroll() keyword arguments (nearest/self/root — relational, not element references), named timelines as the escape hatch for non-ancestor scrollers, view() with animation-range (entry/exit/contain/cover), why linear easing is preferred for scroll-driven effects (1:1 mapping feels connected to user input), the JS it replaces (scroll listeners, IntersectionObserver, rAF loops), compositor thread performance benefits, and practical patterns (progress bar, parallax, shrinking header, carousel indicator, staggered reveals).

## Evidence
- Asked whether scroll() takes an element reference — correctly intuited something is passed in, needed clarification that the arguments are relational keywords not DOM references.
- Asked what "linear" means in the animation shorthand and what other values are possible — understood once explained that non-linear easing feels disconnected from scroll input.
- Spotted that the parallax demo wasn't working — identified correctly that nothing was visually moving. Root cause was scroll(nearest) not resolving correctly inside a sticky element; fixed with named timeline.
- Spotted the carousel indicator wasn't visible — same class of issue (named timeline scope).
- Requested more dramatic demo effects for learning clarity vs production polish — good pedagogical instinct.

## Implications
- All major modern CSS APIs now covered across 23 lessons.
- Ready for capstone project: collaborative build using 10+ features, with challenges and immediate feedback.
- The user prefers iterative challenge-based assessment over big-bang review.
- Named timelines are a concept that may need reinforcement in practice — the user saw them fix problems but hasn't written one themselves yet.
