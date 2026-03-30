---
name: ascii-diagrams
description: >
  Use when the user asks for a diagram, flowchart, architecture drawing, state machine, tree, table,
  network topology, memory layout, or any text-based visual in code comments, READMEs, ADRs, or technical
  docs. Also use when the user says "draw", "diagram", "illustrate", "visualize", "sketch", "show the
  flow", or "show the architecture", even if they do not explicitly say "ASCII".
---

# ASCII Diagrams

Draw clear ASCII diagrams that fit naturally in code comments, documentation, and reviews. Prefer
patterns that render in plain text, survive diffs, and map directly to real code identifiers.

Base your choices on patterns observed in Linux, Chromium, LLVM, and TensorFlow, not on decorative
ASCII art.

## When to create an ASCII diagram

Create a diagram only when it gives the reader a fast visual model before they dive into the code.
Use it for:

- **Architecture and data flow**: how components connect and data moves between them
- **Data structures and memory layouts**: how bits, bytes, and fields are organized
- **State machines and control flow**: states and transitions in a system
- **Network topology**: how hosts, services, and containers relate
- **Test case visualization**: what a test sets up and expects
- **Algorithms**: step-by-step transformations
- **Before/after comparisons**: showing change over time

Do not add a diagram for something the code already shows clearly in linear form.

## Core principles

### 1. Alignment is everything
Treat monospace text as a grid. Align every vertical line, keep horizontal spans consistent, and fix
misalignment before you ship the diagram.

### 2. Use standard characters that render everywhere
Prefer basic ASCII characters that render in any font, terminal, or tool:

| Purpose | Characters | Notes |
|---------|-----------|-------|
| Horizontal lines | `-` `=` | `=` for emphasis/double borders |
| Vertical lines | `|` | |
| Corners/junctions | `+` | Universal junction character |
| Arrows | `>` `<` `^` `v` | Direction indicators |
| Arrow lines | `-->` `<--` `<-->` | Directional flow |
| Boxes | `+--+` with `|` sides | Standard box drawing |
| Dots/bullets | `*` `.` `o` | For nodes or list items |
| Tree branches | `+--` `|` `\` | Hierarchy |
| Elision | `...` `~~~` | "More of the same" |
| Labels | Text inline or beside | Always label clearly |

Use Unicode box-drawing characters (`─ │ ┌ ┐ └ ┘ ├ ┤ ┬ ┴ ┼`) only when the target context supports
them, such as a GitHub-rendered README. In code comments, stick to ASCII.

### 3. Keep it minimal
Show the essential structure, not every detail. If the diagram grows beyond ~30 lines, split it or
simplify it.

### 4. Connect to the code
Reference real identifiers, constants, and expressions from the surrounding code so the reader can
jump between the diagram and the implementation.

### 5. Show what text cannot
Diagram **spatial relationships** such as hierarchies, networks, layouts, and branched flows. Do not
diagram relationships that plain prose or code already shows clearly.

## Design space — choosing the right form

Before drawing, choose the concept you need to show and the visual form that fits it best:

### Visual encodings (how to draw it)

**Connection** — nodes related by visible lines:
- **Linear**: A chain of steps: `A --> B --> C`
- **Tree**: Hierarchy with parent-child branching
- **Graph (directed)**: Nodes with arrows showing direction of flow
- **Graph (undirected)**: Nodes connected without direction

**Table** — rows and columns for structured/categorical data

**Nested** — visible containment (a box inside a box)

**Sequence** — ordered items showing linear progression
- **Single**: one timeline
- **Aligned**: multiple parallel timelines

**Geometry** — spatial/schematic layouts (e.g., UI sketches, circuit layouts)

**Code annotation** — diagram points at code to elaborate on it

### Annotations (how to label)
- **Point**: arrow from label to one element
- **Multi-point**: one label connecting to multiple elements
- **Range**: bracket/box selecting a span
- **Legend**: key explaining symbols used

### Abstractions (how to abbreviate)
- **Fragment**: show part of a bigger thing with `...` at edges
- **Patterned elision**: show a pattern then `...` (e.g., `1, 2, 3, ... N`)
- **Sequential enumeration**: numbered sequence of scenarios

## Diagram patterns by type

Use the reference file instead of copying examples into this skill:

| Category | Reference file | Use for |
|----------|---------------|---------|
| Flowcharts | `references/flowcharts.md` | Decision flows, pipelines, control flow |
| State machines | `references/state-machines.md` | Protocol states, lifecycles, transitions |
| Trees | `references/trees.md` | File trees, class hierarchies, org charts |
| Data structures | `references/data-structures.md` | Memory layouts, packets, bit fields, linked lists |
| Network/Architecture | `references/network-topology.md` | K8s topology, service mesh, observability stacks |
| Sequences/Tables | `references/sequences-tables.md` | Request flows, timelines, comparison tables |
| Graphs/Annotations | `references/graphs-annotations.md` | DAGs, code annotations, before/after, UI sketches |

When responding:
- Pick the closest reference file first
- Reuse or adapt a pattern from `references/`
- Keep `SKILL.md` as guidance/index, not as the full example catalog

## Writing diagrams in code comments

When placing a diagram in a code comment:

- Preserve the host language comment prefix on every line
- Keep alignment valid after adding `#`, `//`, or `*`
- Pull the base pattern from the matching file in `references/`
- Adapt names to real identifiers from the surrounding code

## Alignment checklist

Before finalizing any diagram, verify:

1. Align all vertical lines (`|`) in the same column
2. Connect every box corner (`+`) to the intended horizontal (`-`) and vertical (`|`) lines
3. Point every arrow head (`>`, `<`, `^`, `v`) in the intended direction
4. Keep labels inside boxes without overflow
5. Render the diagram in a monospace font
6. Recheck alignment after adding comment prefixes such as `//`, `#`, or `*`
7. Keep widths consistent across comparable boxes

## Common mistakes to avoid

- **Broken corners**: `+` must connect to exactly one horizontal and one vertical line segment
- **Floating arrows**: every arrow should clearly connect two elements
- **Over-detail**: if the diagram has more detail than the code, it's too complex
- **No labels**: unlabeled boxes and lines are meaningless — always label
- **Inconsistent spacing**: pick a spacing pattern and stick with it across the whole diagram
- **Proportional font assumptions**: never assume characters have different widths
