# Theming deep-dive understood

The user completed Lesson 21 covering: three-tier token architecture (primitive → semantic → component), why dark mode swaps the semantic layer (primitives must stay truthful), why multi-brand swaps primitives (or uses separate brand files), light-dark() as a binary convenience function, color-scheme as the single source of truth, class/attribute-based token swapping for multi-theme, scoped theming via inheritance, @scope for structural styles with lower boundaries, Angular integration (theme service + host binding, build-config brand swap, scoped directive), flash-of-wrong-theme fix (blocking head script), token naming conventions, oklch + relative colour syntax for computed palettes, and the brand-as-parameter pattern.

## Evidence
- Correctly challenged that `light-dark()` only supports two modes — identified the attribute approach as superior even for two themes due to locality of change and extensibility.
- Caught the "swap the semantic layer" wording and questioned whether primitives should be swapped instead — demonstrating understanding of which layer is appropriate for which concern.
- Identified that `--blue-500` as a primitive name becomes a lie in multi-brand — applied the "names must stay truthful" principle independently to a case not yet discussed.
- Spotted the demo/code mismatch in the scoped theming section.
- Spotted that @scope wasn't actually used in the "scoped theming" section despite the heading claiming it.
- Asked about `dataset.theme` vs `data-theme` — understood the mapping once explained (spec-defined namespace with convenience API, like `--` in CSS).
- Noted that `from` in relative colour syntax is "destructuring for colours" — strong analogy from JS experience.
- Observed that hue encodes in one number what RGB takes three to express — correct perceptual model insight.
- Raised AI-friendliness of declarative, localised token blocks — architectural thinking beyond just "does it work."

## Implications
- Token architecture deeply understood. Can build a three-tier system with oklch-derived palettes.
- Understands the tradeoffs between light-dark() and attribute-based approaches.
- Ready for responsive design patterns (synthesis of grid, flex, container queries, clamp from earlier lessons).
- May benefit from revisiting relative colour syntax in a hands-on context (recognised the power but hasn't built with it yet).
