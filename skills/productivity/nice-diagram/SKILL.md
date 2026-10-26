---
name: nice-diagram
description: Always use this when creating a diagram of any kind (flowchart, architecture, pipeline, loop, sequence of steps), whether the user asks for one or you decide one helps. Draws it in D2 with a monochrome house style, rendered to whatever format the destination needs (PNG, SVG, PDF, PPTX, GIF, ASCII text).
---

# Nice Diagram

Every diagram is D2, in the house style below, whatever the destination. When another diagram language is asked for (Mermaid, hand-written SVG), write D2 and render it to the format that destination can hold.

## 1. Pick the shape

A diagram earns its place for a **directional** system: a control loop, an architecture, a pipeline, a flow. Comparing 3+ items across shared dimensions, or a 2×2 matrix, is a Markdown table instead.

Keep it **flat**: 4 to 7 top-level boxes, no nesting, a short verb phrase on every edge. Dashed edges (`style.stroke-dash: 5`) carry feedback, self-correction, and secondary flows; solid edges carry the main path.

## 2. Write the source

Start every `.d2` file from this template, then add boxes and edges beneath it. The template is the default, not a cage: make small changes when the diagram needs them, such as `direction: down` for a tall pipeline, a different shape for a datastore or actor, or 8 boxes where 7 would split a real step. Keep the look itself (black on white, square corners, monospace italic) fixed.

```d2
direction: right

vars: {
  d2-config: {
    layout-engine: tala
    pad: 40
  }
}

style: {
  fill: "#ffffff"
}

*: {
  style: {
    fill: "#ffffff"
    stroke: "#000000"
    stroke-width: 2
    font-color: "#000000"
    border-radius: 0
    font: mono
    bold: false
    italic: true
  }
}

(* -> *)[*]: {
  style: {
    stroke: "#000000"
    stroke-width: 2
    font-color: "#000000"
    font: mono
    italic: true
  }
}
```

## 3. Render to the destination's format

`d2 <slug>.d2 <slug>.<ext>` picks the format from the output extension. Install with `brew install d2` if it's missing.

| Destination                          | Format | Command                                          |
| ------------------------------------ | ------ | ------------------------------------------------ |
| Markdown, a doc, an image to share   | PNG    | `d2 --scale=2 <slug>.d2 <slug>.png`              |
| A web page or HTML artifact          | SVG    | `d2 --no-xml-tag <slug>.d2 <slug>.svg` (inline it) |
| A terminal reply, code comment, plain text | ASCII | `d2 <slug>.d2 <slug>.txt`                   |
| Print or a PDF                       | PDF    | `d2 <slug>.d2 <slug>.pdf`                        |
| Slides                               | PPTX   | `d2 <slug>.d2 <slug>.pptx`                       |
| Several boards stepped through       | GIF    | `d2 --animate-interval=1500 <slug>.d2 <slug>.gif` |

## 4. Look at it

Inspect what you rendered before handing it over. For ASCII, read the `.txt`. For every other format, also render a PNG copy (`--scale=2`) and read the image.

Done when you have seen the rendered diagram and it shows clean orthogonal routing, every label readable and unclipped, and a sensible aspect ratio. Until then, rework the source (reorder boxes, shorten labels, flip `direction`) and re-render.
