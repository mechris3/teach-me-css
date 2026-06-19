# Container queries understood

The user completed Lesson 10 covering: the mental model (responsive to parent not viewport), container-type (inline-size vs size vs normal, and the circular dependency reason), container-name and the shorthand, @container size queries, container query units (cqi etc.), style queries on custom properties, the "mirror" workaround for standard properties, and media vs container queries decision table.

## Evidence
Asked clarifying questions about: whether --theme is a property name or variable usage (connected back to Lesson 1 understanding), whether standard properties can be queried (no — specced but unimplemented), and whether you can mirror standard properties into custom ones as a workaround (yes, with manual sync limitation). Shows deep reasoning about the edges of the feature.

## Implications
- Container queries understood alongside media queries — responsive design toolkit is complete.
- The style query discussion connects directly to cascade/specificity concepts (how custom properties inherit, how values resolve). A cascade deep-dive or @layer lesson would build on this naturally.
