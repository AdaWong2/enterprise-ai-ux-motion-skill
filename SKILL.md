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

## AI Conversation Content Motion

AI chat panels should make conversational authorship, thinking progress, and recency clear:

- Direction should communicate authorship. User input bubbles, especially dark or gradient bubbles aligned to the right, should enter from the right using a small positive `translateX` plus opacity and scale. AI output cards, especially white cards aligned to the left, should enter from the left using a small negative `translateX` plus opacity and scale.
- Keep the directional offset restrained, typically `14-24px` on the x-axis with `8-18px` y-axis lift and `scale(0.90-0.94)` at the start. This creates bubble-like emergence without feeling like a drawer or page transition.
- Use different keyframes for user and AI bubbles, such as `userBubbleIn` and `aiBubbleIn`, rather than a generic card animation. Set `transform-origin` near the bubble tail or leading edge so the motion feels attached to the side it came from.
- Long AI responses should not appear all at once. Reveal them with a streaming or typing effect, chunked by a few characters per frame or short interval, while keeping line height and container width stable to avoid layout jitter.
- Analysis process cards should appear one by one. Before activation, a step should not visually occupy full height; activate it by expanding height, fading in, and using a soft `translate3d` + scale bubble entrance. Let previous steps settle before the next one appears.
- Only the newest AI output card should carry high-attention treatment, such as a blue-purple rotating gradient border. When a newer card appears, previous cards should automatically downgrade to a quiet `1px` neutral gray border and softer shadow.
- Animated borders should be drawn with a masked pseudo-element or inset layer, not by stacking a visible white border plus a colored border. The latest card's real border may be transparent or `0px`; the moving gradient should be the only visible highlight.
- Keep rotating border effects slow and low contrast, around `2.4-3.2s` per loop. It should suggest active AI attention, not an alarm state.
- Step status icons should remain clean and legible. Avoid adding pale circular backgrounds behind every completed icon unless the source design explicitly has them; use larger direct SVG icons when the design needs clarity, and keep all step icons consistent.
- Bubble entrances may start smaller to simulate growth, but should not overshoot above `scale(1)` unless a deliberate playful bounce is required. For enterprise AI chat, prefer monotonic growth such as `scale(0.84-0.90)` to `scale(0.985)` to `scale(1)`; overshoot followed by shrink reads as a bug.
- Always ensure the visible/final state overrides the base hidden transform. For example, if `.user-bubble.message` defines the hidden transform, `.user-bubble.message.is-visible` must explicitly set `transform: translate3d(0, 0, 0) scale(1)`. Otherwise the bubble can shrink back after the animation ends.
- Avoid animating `filter`, `border-radius`, `clip-path`, `max-height`, or other layout/paint-heavy properties in chat bubble entrances. Keep the entrance on `transform` and `opacity`; use fixed-radius styling outside the keyframes.
- Avoid combining height expansion, clip-path reveal, typing, smooth scrolling, animated borders, and ambient loops at the same time. If the panel feels stuttery, first remove layout/crop animation and keep only transform-based bubble entrances.
- Streaming text should throttle DOM writes and scroll updates. Update text in chunks, not per character, and throttle `scrollToBottom()` with `requestAnimationFrame` or a short time gate so typing does not fight the compositor.
- Animated latest-card borders should avoid implementations that rotate a full pseudo-element over the content area; that can create diagonal artifacts. Prefer a masked border layer with background-position movement, or another implementation that only paints the edge.
- Validate conversation motion by sampling early frames: user bubbles should show positive x translation, AI cards should show negative x translation, the scroll container should keep `scrollLeft = 0`, and only one card should have the latest/highlight state at a time.
- Validate the final state after animation completion as well as early frames. User and AI bubbles should end at `scale(1)` and `translate3d(0, 0, 0)`, and frame sampling should show no long frames over roughly `32ms` during the full conversation sequence.
- Avoid tail-frame stutter in bubble entrances. Do not place a late intermediate keyframe such as `76% { scale(0.985); translate: 0; }` before the final `100% { scale(1); }`, because the last correction can read as a visible pause or hitch. Prefer a continuous two-point keyframe from the starting offset/scale directly to the final state, driven by a strong cubic-bezier curve.
- Use `animation-fill-mode: both` for chat bubble entrance animations when the final CSS state and keyframe endpoint are identical. This prevents a visual handoff gap between the animation layer and the static `.is-visible` state after completion.
- Avoid CSS `scroll-behavior: smooth` inside animated chat streams when new bubbles are entering. Smooth scroll can compete with transform-based entrances near the end of the animation; prefer requestAnimationFrame-throttled immediate `scrollTop` updates for deterministic frame timing.

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

## Compact Anchored Popover Motion

For compact contextual popovers with little content, the whole surface should feel like one anchored object:

- Do not stagger inner content when the popover only contains a short notice, one form row, or a small action footer. Let the content appear with the surface as a single unit; internal stagger makes small popovers feel delayed and over-designed.
- When a toolbar action opens a popover, align the popover's leading edge with the trigger button's leading edge unless the source design clearly centers it. The pointer may still align to the trigger center, but the surface edge should feel intentionally attached to the button.
- Use `getBoundingClientRect()` from the trigger, clamp the popover to the viewport, and preserve the chosen edge alignment after clamping. Recompute on resize.
- Keep `transform-origin` stable. If the popover must stay left-aligned throughout the animation, use a left/top origin such as `0px 0px`; a center-based origin can create a few pixels of visual drift during scale animation.
- For a more dynamic pop without shake, use a single continuous keyframe or transition curve: start around `scale(0.88-0.92)` with `translate3d(0, -12px to -16px, 0)`, then settle directly to `scale(1)` and `translate3d(0, 0, 0)`.
- Avoid overshoot above `scale(1)` for enterprise popovers unless the product language explicitly calls for playful feedback. Small overshoots can read as jitter or a final-frame stall.
- Avoid multi-stage keyframes that leave a visible correction in the last frames, such as moving from `scale(0.985)` / `-2px` to the final state. Tail-frame corrections should be near zero, or better, use one continuous cubic-bezier curve.
- Validate motion by sampling computed transforms across the animation. The final frames should approach `scale(1)` and `y: 0` smoothly, the anchored edge should remain stable, and no frame should exceed the intended maximum scale.
- A good compact popover default is `260-320ms` open with a strong but continuous enter curve such as `cubic-bezier(0.08, 0.82, 0.18, 1)`, and `160-220ms` close with a simpler exit curve.

## Announcement Modal Motion

For centered announcement, maintenance, notice, and system-status modals, use a standard modal pattern unless the content itself requires a complex narrative reveal:

- Use exported Figma background assets for page-specific decorative backgrounds. Do not recreate complex background waves, ribbons, glass curves, or brand illustrations with hand-written CSS when the source design provides those elements as image layers.
- Choreograph the environment before the modal. Let background imagery, logo, and footer/legal text begin first, then bring the modal in after a short delay. This makes the modal feel placed into an existing scene instead of appearing in an empty frame.
- Footer or legal text that belongs to the background should animate with the background, not after the modal. If the decorative background starts at `120ms`, start footer text at the same delay or very close to it.
- Avoid excessive internal stagger for static announcement modals. If the modal is a single composed message, do not animate badges, headings, paragraphs, cards, and help bars one by one; it reads as noisy and disorganized. Let content follow the modal surface as one unit, or at most separate only major structural regions when there is a clear hierarchy reason.
- For a common enterprise announcement modal, use a whole-surface entrance: overlay fade plus modal `opacity`, `translate3d(0, 20-28px, 0)`, and `scale(0.96-0.98)` to `scale(1)`. Keep content static inside the surface.
- If background motion is staggered before the modal, a good default is background/logo/footer starting around `120-180ms`, modal entrance delayed around `320-420ms`, modal duration around `560-720ms`, and close around `220-300ms`.
- Do not slow a modal by adding late intermediate opacity/transform keyframes such as `45% { opacity: 0.48; translateY(8px); scale(0.986); }` unless testing confirms it stays smooth. These midpoints can create perceived stutter even when they make opacity changes more visible.
- Prefer two-point continuous modal keyframes for smoothness: start from the hidden transform/opacity and end exactly at `opacity: 1; transform: translate3d(0, 0, 0) scale(1)`. If more visibility is needed, extend duration before adding mid-keyframes.
- When changing modal duration or delay, update JavaScript timers for focus handoff and close-state removal. Focus should occur after the entrance completes, and close-state cleanup should wait until exit animation finishes.
- Validate announcement modals by sampling the sequence: background should be active while modal remains hidden, modal should then progress smoothly to final state, and final computed transform should settle at `matrix(1, 0, 0, 1, 0, 0)` without a tail correction.

## Side Drawer Motion

Side drawers should communicate lateral spatial movement, not just fade into place:

- Keep the scrim as a separate fade/blur layer, but make the drawer panel itself slide from off-canvas using `translate3d(calc(100% + gutter), 0, 0)` to `translate3d(0, 0, 0)`.
- Avoid using opacity and scale as the primary drawer entrance; they can make a side drawer feel like a modal. Use opacity only for inner content or the scrim.
- For large enterprise drawers, a good default is 480-540ms for opening and 280-340ms for closing. Closing should feel slightly faster than opening.
- Stagger drawer contents after the panel begins moving: title first, then tabs/filters, then list cards, then footer actions. Keep delays short so content does not feel late after the panel arrives.
- On empty demo pages, add one explicit trigger button that opens the drawer. Do not auto-open unless the user specifically requests it.

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
