---
name: ui-motion-library
description: Reusable micro-interaction specifications for web and app UI. Use when implementing press feedback, elastic toggles, pointer ripples, like bursts, animated checkboxes, or magnetic buttons.
---

# UI Motion Library — V1.0

Use these specifications when the user requests one of the six interactions. Respect existing framework, styling, theme tokens, and accessibility conventions. Do not add all six unless requested. Prefer transforms and opacity for smooth animation. Avoid changing layout dimensions during animations.

## 01. Press & Spring Back（按压回弹）
- Trigger: pointer/touch down; release/cancel.
- Press: `scale: 0.94`; reduce shadow intensity.
- Release: spring back to `scale: 1`, with slight overshoot.
- Spring: `stiffness: 260`, `damping: 12`.
- Keep keyboard activation and focus styles intact.

## 02. Elastic Toggle（弹性开关）
- Trigger: checked state change.
- Knob: translate between ends, stretch horizontally to `scaleX: 1.35` while moving, then spring back to `scaleX: 1`.
- Spring: `stiffness: 200`, `damping: 14`.
- Track background: transition over `280ms` to the project's theme-green token when checked; reverse when unchecked.
- Implement semantic switch/checkbox state and keyboard support.

## 03. Touch Ripple（跟手波纹）
- Trigger: pointer/touch activation; origin at the local click coordinates.
- Ripple: circular, initial opacity `0.28`, fades to `0` in `450ms`.
- Target diameter: `2.4 × button width` (interpretation of original phrase “放大到按钮宽度的2.4倍”; adjust if user intends radius or transform scale).
- Clip to button bounds; support repeated clicks and remove finished ripples.
- For keyboard activation, originate at the center.

## 04. Like Burst（点赞反馈）
- Trigger: transition from unliked to liked.
- Heart: scale to `1.3`, spring back to `1`.
- Particles: eight small dots radiate outward and fade.
- Counter: upward rolling transition by `+1`.
- Spring: `stiffness: 300`, `damping: 10`.
- Define reverse/unlike behavior consistently with product state; avoid double-counting.

## 05. Animated Checkbox（复选框动画）
- Trigger: unchecked → checked.
- Box: begin at `scale: 0.8`, spring to `1` while filling with the theme color.
- Checkmark: SVG stroke drawing animation lasting `300ms`.
- Task text: gray with strikethrough when completed; reverse when unchecked.
- Preserve native checkbox semantics and focus/keyboard behavior.
- Spring parameters unspecified; use project defaults unless requested.

## 06. Magnetic Button（磁吸按钮）
- Trigger: pointer enters a zone within `120px` of the button; follow pointer at `0.35` strength.
- Exit: spring back to original position.
- Spring: `stiffness: 150`, `damping: 15`.
- Recommended implementation: compute displacement relative to button center and cap displacement to prevent overlap; the 120px zone should be defined relative to the button's edge (assumption to confirm if exact geometry matters).
- Enable only on fine-pointer/hover devices; do not interfere with clicking.

## Global requirements
- Respect `prefers-reduced-motion`: remove or greatly simplify motion while retaining state feedback.
- Use theme tokens instead of hard-coded colors; the toggle's green should resolve to the project's theme green.
- Preserve accessible roles, labels, focus indicators, and keyboard interaction.
- Clean up animation callbacks, timers, and pointer listeners when components unmount.
- Keep the animations responsive and avoid layout shifts.
- Validate both checked/unchecked, liked/unliked, mouse/touch/keyboard and rapid repeated interaction.
- If using a spring library, treat stiffness and damping as library-specific parameters, not universal physical values.

## Example invocation
“Use ui-motion-library to add Press & Spring Back and Touch Ripple to the primary action button. Keep existing colors and layout.”

## Source tags
UI设计 · UX设计 · 交互设计 · 动效设计 · 前端开发 · AI提示词