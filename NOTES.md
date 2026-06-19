# Teaching Notes

## User Preferences
- Experienced developer — don't over-explain fundamentals
- Prefers depth over breadth
- Angular specialist — can use Angular context for examples when helpful, but focus is on native CSS
- No time pressure — optimise for depth and retention over speed
- First time using this teaching skill — curious about the process itself. Be transparent about how the system works (lessons, learning records, etc.) when it's natural to explain.
- Browser: Chrome 149 (arm64 Mac) — well past the @function support threshold (139+). All modern CSS demos should work.
- Does NOT already use custom properties regularly. Don't assume familiarity — teach from the ground up on CSS-specific topics even though the user is a senior dev. "Senior dev" ≠ "already uses every CSS feature."
- Knows the basics of custom properties (declaration syntax, var()) but doesn't use them day-to-day. Treat custom properties as something to teach properly from first principles, not something to skip over.
- Happy to have refreshers on basics. Would rather move quickly through known material than skip it entirely. Cover everything — the user will self-pace through familiar parts.
- Every code sample must have a rendered demo, and demos + code must be visually grouped together (e.g. inside a shared container/card) so it's unambiguous which code produces which output.
- ONE example per group only. Never stack multiple rendered demos followed by multiple code blocks. Each group = one rendered demo + its code, tightly coupled. If there are multiple examples for a concept, use multiple groups in sequence.
- Each code example must be COMPLETE and self-contained. Show all the HTML, CSS, and JS needed to make the demo work. Never require the reader to cross-reference other parts of the document. Cognitive load is the enemy — every example should stand alone.
- Values mental models over memorisation. Prefers understanding underlying mechanisms so they can infer behaviour rather than recall individual rules. Lead with the "why" and the model, then show the specifics as consequences of that model.
- Include HTML alongside CSS in code examples when classes or structure are involved. The user wants to see how the CSS connects to the markup — don't show CSS in isolation when the selector targets specific classes or elements.
- Body max-width should be 60rem (not 42rem) to give code blocks more room and avoid horizontal scrolling.
