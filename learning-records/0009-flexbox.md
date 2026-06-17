# Flexbox understood

The user completed Lesson 8 covering: the flex algorithm (basis → free space → grow/shrink → min constraints), flex-direction, justify-content vs align-items (axis-based mental model, not horizontal/vertical), the capabilities asymmetry table, flex-basis vs width, flex-grow (distributes free space not total), flex-shrink (weighted by basis), the flex shorthand (flex: 1 vs flex: auto distinction), flex-wrap, gap, align-self, order, min-width: auto gotcha, align-content, and practical patterns (sticky footer, sidebar, centering, input+button, equal-height cards).

## Evidence
Asked a deep question about the relationship between justify-content and align-items — whether swapping direction + swapping the property would cancel out. Understood the answer (yes for positioning, no for space distribution/stretch). Reported this was the clearest understanding they've ever had of justify vs align. The axis mental model is solid.

## Implications
- Ready for CSS Grid (Lesson 9) — the two-dimensional layout system.
- The justify/align axis model carries directly into Grid (same property names, same axis logic).
- Can reference flex algorithm, grow/shrink/basis, and min-width: 0 without re-explaining.
