# View transitions understood

The user completed Lesson 16 covering: the view transition mental model (snapshot → DOM update → animate), same-document vs cross-document transitions, the full 5-phase timeline, view-transition-name (uniqueness rule, dynamic assignment), the pseudo-element tree (::view-transition-old/new/group), pseudo-elements vs pseudo-classes distinction, the (name) parenthesised filter, custom animations on pseudo-elements, shared element morphing, Angular's withViewTransitions() in detail (standalone bootstrap, onViewTransitionCreated callback, directional slides, global styles requirement, dynamic names via [style.view-transition-name] and .active class pattern), list reordering, dark mode circular reveal, tab switching, and reduced motion.

## Evidence
- Asked for detailed Angular coverage — understood the standalone bootstrap config and onViewTransitionCreated callback.
- Caught the inline style anti-pattern and asked for a cleaner approach — refactored to .active class pattern (CSS owns the name, JS owns the state).
- Asked to clarify pseudo-elements vs pseudo-classes, and what the parenthesised argument is.
- Identified non-working demos and incomplete code — engaged deeply with the material.

## Implications
- View transitions deeply understood, including Angular integration.
- Remaining mission topics: @scope, advanced colour (oklch, relative colour syntax), anchor positioning.
- The user has now covered 16 substantial lessons. Consider whether a project/practice exercise would consolidate knowledge.
