# Responsive design patterns understood

The user completed Lesson 22 covering: the intrinsic vs extrinsic design mental model, fluid typography with clamp() (rem + vw in preferred slot), auto-fill grid for breakpoint-free card layouts, container-query-responsive cards, the pancake stack (auto 1fr auto), holy grail with named grid areas, flex-wrap sidebar collapse, fluid spacing, and the decision framework (intrinsic first → container queries second → media queries last).

## Evidence
- Needed a refresher on how clamp() achieves fluid scaling — correctly identified that it's the vw unit in the preferred slot that creates the continuous variation, not clamp itself doing interpolation.
- Confirmed understanding that clamp() with all fixed units would be pointless — the function is only useful when the preferred value contains a variable unit.
- Noted that these patterns are worth memorising as recipes rather than reconstructing from first principles every time — practical instinct.
- Observed that the mental model's value is in being able to articulate modifications to an AI rather than implementing from scratch — accurate assessment of modern workflow.

## Implications
- Responsive layout toolkit complete. Can compose grid, flex, container queries, and clamp into real layouts.
- Ready for scroll-driven animations — the last major modern CSS API not yet covered.
- The user's learning posture has shifted from "understand everything deeply" to "understand the model, know where to find the recipes" — appropriate for this stage of mastery.
