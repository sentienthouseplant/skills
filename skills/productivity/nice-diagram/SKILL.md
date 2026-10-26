---
name: nice-diagram
description: Always use this when creating a diagram of any kind (flowchart, architecture, pipeline, loop, sequence of steps), whether the user asks for one or you decide one helps. Draws it in D2 with a monochrome house style, rendered to whatever format the destination needs (PNG, SVG, PDF, PPTX, GIF, ASCII text).
---

# Nice Diagram

Every diagram is D2, in the house style below, whatever the destination. When another diagram language is asked for (Mermaid, hand-written SVG), write D2 and render it to the format that destination can hold.

## 1. Pick the shape

The default is a **patio**: irregular boxes fitted together like paving stones, packed into a rectangle. It is dense yet clear, and it is what tala produces from a few rich boxes when you leave the placement to it:

- **Boxes sized by content.** Each box is a name plus concrete examples in parentheses (`"Feedback Sensors\n(Linters, Tests,\nFitness Fns)"`), wrapped with `\n` so no line runs past about 20 characters. Big ideas get big boxes.
- **Staggered, never gridded.** Boxes sit offset from their neighbours, and the offsets are where edges and their labels live. Leave positions to tala rather than forcing rows and columns.
- **Fills a rectangle.** 4 to 7 boxes whose overall footprint is close to a filled rectangle: no empty corners, no long tail. When the shape comes out lopsided, flip `direction` or reorder the declarations.
- **Short, labelled edges.** A 2 to 4 word clause on every edge, wrapped with `\n`. Each edge bends at most once. Dashed edges (`style.stroke-dash: 5`) carry feedback, self-correction, and secondary flows; solid edges carry the main path.

Comparing 3+ items across shared dimensions, or a 2×2 matrix, is a Markdown table instead.

## 2. Write the source

Start every `.d2` file from this template, then add the diagram beneath it. The template is the default, not a cage: make small changes when the diagram needs them, such as `direction: down` for a tall pipeline, a different shape for a datastore or actor, or 8 boxes where 7 would split a real step. Keep the look itself (black on white, square corners, monospace italic) fixed.

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

**: {
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

(** -> **)[*]: {
  style: {
    stroke: "#000000"
    stroke-width: 2
    font-color: "#000000"
    font: mono
    italic: true
  }
}
```

The `**` globs style nested boxes too; a single `*` leaves every tile inside a group in D2's default blue.

Use a **grid** (`grid-columns: N`, `grid-gap: 0` at every level) only for strict containment, like a folder tree or a layered stack, where perfect alignment is the point. Give every tile the same `width` and `height` so a wide group title can't inset its column. A grid draws no edges between its own tiles; connect outside boxes to the grid container itself.

## 3. Render to the destination's format

`d2 <slug>.d2 <slug>.<ext>` picks the format from the output extension. Install with `brew install d2` if it's missing. ASCII garbles a grid's packed borders, so a text destination gets a patio, or a PNG path to open.

| Destination                                | Format | Command                                            |
| ------------------------------------------ | ------ | -------------------------------------------------- |
| Markdown, a doc, an image to share         | PNG    | `d2 --scale=2 <slug>.d2 <slug>.png`                |
| A web page or HTML artifact                | SVG    | `d2 --no-xml-tag <slug>.d2 <slug>.svg` (inline it) |
| A terminal reply, code comment, plain text | ASCII  | `d2 <slug>.d2 <slug>.txt`                          |
| Print or a PDF                             | PDF    | `d2 <slug>.d2 <slug>.pdf`                          |
| Slides                                     | PPTX   | `d2 <slug>.d2 <slug>.pptx`                         |
| Several boards stepped through             | GIF    | `d2 --animate-interval=1500 <slug>.d2 <slug>.gif`  |

## 4. Look at it

Inspect what you rendered before handing it over. For ASCII, read the `.txt`. For every other format, also render a PNG copy (`--scale=2`) and read the image.

Done when you have seen the rendered diagram and every box is black on white, every label is readable and clear of lines and other labels, the boxes fill a rectangle with even gaps, and every edge routes short and clean. Until then, rework the source (reorder boxes, shorten labels, flip `direction`, move an edge's endpoint) and re-render.
