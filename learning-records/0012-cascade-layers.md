# Cascade layers understood

The user completed Lesson 11 covering: where layers sit in the cascade (above specificity), declaration order vs definition order (critical distinction — declaration locks priority, definitions can be anywhere), the !important inversion, unlayered styles as the ultimate override, practical layer architectures, importing third-party CSS into layers, nested layers, and anonymous layers.

## Evidence
Asked to confirm the declaration vs definition distinction — correctly identified that it's declaration order that matters, not where styles are authored. This is the key conceptual point of @layer.

## Implications
- Cascade management understood. Can now reason about: layers > specificity > source order.
- Ready for: CSS nesting (how it interacts with specificity), modern selectors (:has, :is, :where and their specificity behaviour), or the full cascade algorithm deep-dive.
- Include HTML in code examples going forward (user preference confirmed).
