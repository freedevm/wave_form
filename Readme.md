# `index.html` Documentation

## Overview
`index.html` is a standalone HTML/CSS component that renders:
- A rounded dark frame
- Two menu tabs (radio + label toggle)
- A light panel drawn with SVG
- A bubble hump that animates between left and right tabs

No JavaScript is used.

## Structure
1. **State inputs**
- `#tab-1` and `#tab-2` (`.menu-toggle-input`) store selected state.

2. **Tab UI**
- `.nav` contains two `.menu-tab` labels tied to the radios via `for`.
- Active color is controlled by:
  - `#tab-1:checked ~ .nav label[for="tab-1"]`
  - `#tab-2:checked ~ .nav label[for="tab-2"]`

3. **Panel + bubbles**
- `.panel-surface` wraps the SVG.
- SVG elements:
  - `.panel-base`: main panel shape
  - `.bubble-shape-left`: bubble under tab 1
  - `.bubble-shape-right`: bubble under tab 2

## Animation
- Grow keyframes: `bubble-grow`
- Shrink keyframes: `bubble-shrink`

Current tokens in `:root`:
- `--grow-duration: 0.6s`
- `--shrink-duration: 0.3s`
- `--grow-ease: cubic-bezier(.18, .64, .18, 1)`
- `--shrink-ease: cubic-bezier(.22, .62, .18, 1)`

`bubble-grow` flow:
- `0%`: `scale(0, 0)`
- `40%`: `scale(1.15, 1.15)` (overshoot)
- `70%`: `scale(0.9, 0.9)` (undershoot)
- `85%`: `scale(1.05, 1.05)` (rebound)
- `100%`: `scale(1, 1)`

`bubble-shrink` flow:
- `0%`: `scale(1, 1)`
- `100%`: `scale(0, 0)`

## Visual Tokens
- `--bg`: black frame/background
- `--panel`: panel/bubble/border light color
- `--active`: active tab color

## Bubble Path Tuning
Bubble geometry is defined in the two SVG `path` `d` values:
- `.bubble-shape-left`
- `.bubble-shape-right`

Quick tuning rules:
- Wider bubble: decrease start `x`, increase end `x`
- Narrower bubble: increase start `x`, decrease end `x`
- Taller middle: decrease middle `y`
- Flatter middle: increase middle `y`
- Rounder shoulders: smooth neighboring control points toward baseline

## Accessibility / Motion
- Reduced motion is handled with `@media (prefers-reduced-motion: reduce)`.
- Nav has `aria-label="Menu"`.
- Decorative panel container is `aria-hidden="true"`.

## Run
Open `index.html` in a browser.
