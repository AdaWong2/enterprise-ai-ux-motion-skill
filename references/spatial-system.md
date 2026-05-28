# Spatial Motion System

All UI surfaces should follow a consistent spatial hierarchy.

## Depth Levels

1. Background
2. Base Surface
3. Floating Surface
4. Overlay
5. Modal

## Motion Rules

- Background moves slowest.
- Base surfaces remain stable.
- Floating surfaces may lift subtly on interaction.
- Overlays fade and slide from their spatial source.
- Modals emerge forward with opacity and scale.

## Recommended Patterns

### Card Hover

- translateY(-2px) to translateY(-4px)
- slight border highlight
- soft shadow increase

### Modal Enter

- opacity 0 to 1
- scale 0.96 to 1
- translateY(8px) to 0

### Drawer Enter

- translateX within its container
- opacity 0.85 to 1
- avoid harsh full-screen sliding
