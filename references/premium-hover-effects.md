# Premium Hover Effects

## Glass Card Hover

```css
.motion-glass-card {
  position: relative;
  overflow: hidden;
  transition:
    transform 220ms cubic-bezier(0.2, 0, 0, 1),
    border-color 220ms cubic-bezier(0.2, 0, 0, 1),
    box-shadow 220ms cubic-bezier(0.2, 0, 0, 1);
}

.motion-glass-card:hover {
  transform: translateY(-4px);
  border-color: rgba(129, 140, 248, 0.45);
  box-shadow: 0 18px 48px rgba(79, 70, 229, 0.16);
}

.motion-glass-card::before {
  content: "";
  position: absolute;
  inset: -1px;
  border-radius: inherit;
  padding: 1px;
  background: linear-gradient(
    120deg,
    rgba(96, 165, 250, 0),
    rgba(129, 140, 248, 0.75),
    rgba(168, 85, 247, 0.65),
    rgba(96, 165, 250, 0)
  );
  opacity: 0;
  transition: opacity 220ms ease;
  pointer-events: none;
}

.motion-glass-card:hover::before {
  opacity: 1;
}
```

## Animated Border Rule

Animated gradient borders should only appear on premium interactive surfaces and should activate on hover or focus.

Avoid always-on fast animated borders.
