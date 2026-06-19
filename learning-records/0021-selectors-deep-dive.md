# Selectors deep-dive understood

The user completed Lesson 20 covering: the :nth-child gotcha (it's two independent filters, not scoped counting), :nth-of-type as the correct tool for "nth of this tag", the `of S` syntax for class-based positional selection, the An+B formula, full structural selector reference, form state pseudo-classes (:focus/:focus-visible/:valid/:invalid/:placeholder-shown/:disabled/:enabled), :target (driven by location.hash in the address bar), attribute selectors (all operators including case-insensitive `i`), and combined selector recipes.

## Evidence
- Correctly identified the :nth-child gotcha before being taught — recalled that people misunderstand what it selects.
- Asked whether `:not(:disabled)` achieves the same as `:enabled` — correctly reasoned about selector composition, then understood the distinction (`:enabled` only matches elements that *can be* disabled).
- Asked for clarification on :target mechanism — understood once explained that it's driven by the current address bar URL fragment.
- Asked whether CSS has access to other URL parts — understood the answer (only the hash) without needing further explanation.
- Spotted code/demo mismatches in the lesson (missing section B, unclear `of S` reference direction) — attentive reader.

## Implications
- Selector mental model is now comprehensive: structural, form state, interaction, attribute, functional (from lesson 13), and combinatorial patterns.
- Ready for theming deep-dive as requested — multi-brand token architecture, light/dark mechanics, Angular integration.
- The user tests understanding by proposing alternative approaches (`:not(:disabled)` vs `:enabled`) — a strong signal of model-based reasoning.
