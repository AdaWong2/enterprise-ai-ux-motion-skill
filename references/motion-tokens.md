# Motion Tokens

Use these CSS variables as the baseline motion system.

```css
:root {
  --motion-instant: 80ms;
  --motion-fast: 120ms;
  --motion-normal: 220ms;
  --motion-slow: 420ms;
  --motion-ambient: 12s;

  --ease-standard: cubic-bezier(0.2, 0, 0, 1);
  --ease-enter: cubic-bezier(0.16, 1, 0.3, 1);
  --ease-exit: cubic-bezier(0.4, 0, 1, 1);
  --ease-emphasis: cubic-bezier(0.34, 1.56, 0.64, 1);

  --hover-lift-sm: translateY(-2px);
  --hover-lift-md: translateY(-4px);
  --hover-scale-press: scale(0.98);

  --glass-blur: 24px;
  --glass-glow: 0 18px 48px rgba(79, 70, 229, 0.16);
  --glass-border: rgba(255, 255, 255, 0.5);
}
```

## Reduced Motion

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```
