# CSS Transitions understood

The user completed Lesson 6 covering: the four transition properties, placement on base state vs hover (and why), asymmetric timing pattern, timing functions (keywords + cubic-bezier), staggered delays, multiple properties with independent timing, transition: all pitfalls, what can/can't be transitioned, transition-behavior: allow-discrete, transitioning registered custom properties, performance tiers (composite/paint/layout), and gotchas (height auto, page load, display none).

## Evidence
Asked a sharp question about WHY placing transition on :hover wouldn't work in both directions. This shows the user is reasoning about selector lifecycle and cascade timing, not just memorising rules.

## Implications
- Ready for CSS animations (@keyframes, animation shorthand, scroll-driven animations).
- Understands the "extract → register → transition" pattern. Future animation lessons can build on this.
- Asks "why" questions — keep explaining the underlying model, not just the syntax.
