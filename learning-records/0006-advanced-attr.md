# Advanced attr() understood

The user completed Lesson 5 covering: old attr() limitations (string-only, content-only), new typed syntax with type() and fallbacks, using attr() in any property, composing with calc(), fallback chains with var(), when to use attr() vs custom properties, and limitations (no inheritance, no animated transitions — but IS reactive to DOM changes).

## Evidence
The user asked a sharp clarifying question about whether attr() is reactive to DOM changes or frozen at initial value. This shows they're thinking about runtime behaviour, not just static syntax. Correcting the ambiguity deepened understanding.

## Implications
- The "CSS as a typed expression language" thread is complete: custom properties → @property → value functions → @function → attr().
- Ready to pivot to layout (Flexbox/Grid) or animations.
- The user thinks in terms of runtime reactivity and Angular data binding — future lessons should connect CSS concepts to dynamic/framework contexts where natural.
