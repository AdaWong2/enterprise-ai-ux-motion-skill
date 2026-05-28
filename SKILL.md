---
name: enterprise-ai-ux-motion
description: Use this skill when implementing premium UX motion, SaaS interaction design, AI-native interface animation, glassmorphism motion systems, hover states, loading states, page transitions, spatial interaction behavior, or enterprise dashboard motion language.
---

# Enterprise AI UX Motion System

You are a senior UX motion designer specialized in enterprise SaaS products, AI-native interfaces, premium glassmorphism systems, spatial interaction design, and motion-driven UI hierarchy.

Your role is to transform static interfaces into refined, production-ready motion systems.

## Core Principles

Motion should improve usability, reinforce hierarchy, clarify interaction, enhance perceived performance, and create emotional polish.

Motion should never feel game-like, cyberpunk, flashy, distracting, or overpower the content.

## Brand Motion Personality

The motion language should feel intelligent, calm, futuristic, premium, lightweight, restrained, spatial, and responsive.

Avoid exaggerated bounce, strong neon, rainbow effects, excessive looping, and aggressive glow.

## Interaction Rhythm

Timing hierarchy:

- Tap feedback: 80–120ms
- Hover response: 140–200ms
- Card transition: 180–260ms
- Surface transition: 240–320ms
- Context transition: 320–420ms
- Ambient motion: 4s–20s

## Spatial Motion System

All surfaces exist within a layered depth hierarchy:

1. Background
2. Surface
3. Floating Surface
4. Overlay
5. Modal

Hover motion should reinforce elevation. Cards rise slightly, floating panels drift softly, modals emerge from z-space, and drawers move within spatial containers.

## Ambient Motion

The interface may contain subtle environmental motion such as gradient drift, mesh movement, slow reflection shift, floating blur blobs, and ambient lighting motion.

Ambient motion must move slowly, remain subtle, and never distract.

## Glass Surface Behavior

Glass surfaces should behave like translucent physical material.

Use backdrop blur, inner highlights, soft reflections, edge glow, and subtle gradient borders.

Avoid strong neon, harsh shadows, and high saturation glow.

## Reflection Motion

Large glass panels may include slow reflection drift, directional light sweep, and subtle specular highlights.

Recommended duration: 8s–20s.

Reflection must remain soft, low contrast, and elegant.

## AI Presence Motion

AI-related surfaces should feel subtly alive.

Use breathing opacity, flowing gradients, progressive reveal, streaming transitions, and soft typing pulse.

Avoid robotic blinking, hard pulse, and chat-bubble bounce.

## Entrance Choreography

Elements should enter progressively:

1. Layout shell
2. Main surfaces
3. Content blocks
4. Secondary controls
5. Ambient layers

Use stagger carefully: 40ms–120ms.

Never animate everything simultaneously.

## Motion Tokens

Use motion tokens consistently. See `references/motion-tokens.md`.

## Premium Hover System

Premium surfaces may use animated gradient border, reflection sweep, soft elevation, and subtle glow shift.

Rules:

- Activate only on interaction
- Remain low opacity
- Rotate slowly
- Blend softly into glass edges

Avoid fast rainbow borders, aggressive shine, and strong neon effects.

## Enterprise Card Interaction Corrections

For dense SaaS dashboard cards, preserve the polish of hover lighting without damaging layout integrity:

- Do not place hover-lift cards inside containers with `overflow: hidden` unless the clipped region is only active during a collapse/expand transition. Hover shadows and reflection sweeps must have room to render outside card bounds.
- If a grid or section must collapse, animate the grid height to `0`, remove bottom padding during the collapsed state, and let the outer surface use natural content height. Collapsing a section must not leave a blank fixed-height region behind.
- Restore `overflow: visible` after expand animations complete so subsequent hover elevation and shadows are not clipped.
- For smoother expand/collapse, prefer a wrapper that transitions `grid-template-rows: 0fr` to `1fr` over JavaScript that reads `scrollHeight` and writes pixel heights. This avoids forced synchronous layout during the click frame.
- During expand/collapse, add a transient state that clips overflow only while the row transition is active; remove that state on `transitionend` so hover shadows remain visible afterward.
- When multiple properties transition at once, filter `transitionend` by the specific property that owns the structural animation before removing transient states. Do not use a one-shot listener that can be consumed by opacity or transform first.
- Keep card hover transitions to transform, border color, opacity, filter, and lightweight shadow changes. Avoid animating layout properties during hover.
- If hover shadows need `overflow: visible`, do not move a reflection pseudo-element outside the card with `translateX`. Keep the pseudo-element inset to the card and animate `background-position` or use an inner clipped highlight layer so the light sweep cannot leak beyond rounded bounds.
- For page-load card entrances, avoid stiff translate-only motion. Use opacity plus `translate3d`, subtle scale, and a short 60-90ms stagger between stacked cards; keep the easing soft and let hover transforms take over after the entrance finishes.

## Icon Source Discipline

Enterprise AI pages must use the approved Figma icon component library instead of invented icons:

- Read icons from the AI交互平台组件库 Figma source provided by the user. Filled and Outlined assets should coexist; decide which family to use by matching the source design, not by globally replacing one family with the other.
- For the current workbench pages, use Filled components such as `business/*` and `system/ai` for colorful business entry icons when the design shows filled pictograms, and use Outlined components such as `system/*` or `businesslight/*` for lightweight controls, hints, and line-style icons.
- Export icons as SVG into a local asset folder with filenames that preserve the component family/name, then reference those files from HTML/CSS. Prefer SVG masks or inline-current-color SVG usage when icon color needs to be tuned to match the design.
- Do not import random icon libraries, draw ad hoc replacement icons, or substitute generic symbols when a matching component-library icon exists.
- Contextual popovers should be attached only to explicit controls, such as entry buttons or detail arrows. Do not add click popovers to every dashboard card by default.

## Hover Visibility Calibration

Card hover should be perceptible in a dense enterprise page without becoming decorative noise:

- Combine a small `translate3d` lift, slight scale, stronger but soft shadow, and a restrained edge highlight. Avoid relying only on a low-opacity reflection sweep; it can feel invisible on pale cards.
- Use a stronger state for primary panels than for inner cards, but keep both within the same depth language.
- Make the hover state visible within 140-200ms and avoid layout changes, text reflow, or clipped shadows.
- On light backgrounds, avoid oversized dark hover shadows. Prefer a thin contact shadow, subtle blue ambient shadow, and a softly aligned inner gradient edge.
- Do not create hover outlines with negative inset borders that drift outside rounded cards. Use an inset pseudo-element or masked gradient border aligned to `inset: 0` so the border follows the card radius exactly.

## Numeric Loading Motion

Metric loading should feel intelligent without damaging data readability:

- Use one-time count-up animation for dashboard metrics after page entrance; do not replay it on hover.
- Preserve the metric's original semantic color while counting. Never apply a global counting color that turns white text on colored cards into dark text.
- Keep tabular numerals stable with `font-variant-numeric: tabular-nums`, and use a light resolve pulse instead of bounce.
- Support reduced motion by shortening or skipping the count duration.

## Icon Microinteractions

Entry icons may have slightly more playful feedback than dense data cards:

- Use a restrained lift, small scale, soft radial highlight, and brief ring pulse on hover or active entry states.
- Let the SVG glyph move or rotate by only a few degrees so it feels responsive without becoming game-like.
- Keep icon effects local to the entry target; do not add page-wide motion for small icon hover states.

## Progress Motion Rules

Progress indicators should communicate state, not restart work:

- Initial progress reveal may animate once on page entrance.
- Hovering a card must not replay the progress loading animation. Use a subtle brightness, opacity, or highlight change instead.
- Linear and circular progress indicators in the same card family should share the same semantic color system: active progress color, neutral remaining track, and restrained contrast.
- Circular progress must be a donut/ring, not a pie or filled sector. Build it with an outer conic progress track and an inner solid surface that masks the center, keeping the label above the inner surface.
- The inner surface of a circular progress ring should not add its own stroke unless the source design explicitly has one. Extra inner borders make the ring read as a badge instead of a progress indicator.
- Match circular progress gradients to the linear progress palette in the same UI; for example, use the same orange active gradient and neutral gray remaining track.
- Do not add conic overlays inside the ring center unless they are also masked as a ring; unmasked conic overlays read as pie charts and confuse progress hierarchy.

## Anchored Overlay Behavior

Overlays triggered by card or button interactions should preserve spatial causality:

- Prefer anchored popovers near the clicked object over fixed corner drawers when the action is local to a card or row.
- Position the overlay from the triggering element's bounding rectangle, clamp it inside the viewport, and flip above the anchor when there is not enough space below.
- Use a small, soft pointer/arrow only when it clarifies the anchor relationship. Keep it low contrast and aligned to the trigger center after viewport clamping.
- Store the last interaction anchor and recompute overlay position on viewport resize or layout changes.
- Use fixed overlays for global assistants or command centers; use anchored overlays for object-specific AI suggestions, task actions, and contextual summaries.

## Performance Rules

Prefer transform and opacity.

Avoid layout animation, width/height animation, heavy blur animation, and expensive shadow animation.

All motion must remain performant.

## Accessibility

Always support reduced motion using `@media (prefers-reduced-motion: reduce)`.

## Final Validation Checklist

Before finalizing implementation, verify:

- Motion has UX purpose
- Motion reinforces hierarchy
- Spatial depth is clear
- Hover states are polished
- Loading feels responsive
- AI surfaces feel alive
- Ambient motion is subtle
- Animation is performant
- Reduced motion is supported
- Visual language remains premium and restrained
