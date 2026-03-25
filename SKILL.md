---
name: ascii-diagrams
description: >
  Create professional ASCII diagrams for code comments, documentation, architecture docs, and technical
  communication. Based on the CHI'24 research paper "Taking ASCII Drawings Seriously" which analyzed 2,156
  real diagrams from Linux, Chromium, LLVM, and TensorFlow. Use this skill whenever the user asks for a
  diagram, visualization, flowchart, architecture drawing, state machine, data structure illustration,
  memory layout, network topology, table, tree, or any visual representation using ASCII/text art in code
  or documentation. Also trigger when the user says "draw", "diagram", "illustrate", "visualize",
  "sketch", "show the flow", "show the architecture", or wants to add a visual explanation to code
  comments, READMEs, ADRs, or technical docs. Even if they don't say "ASCII" explicitly — if they want
  a text-based diagram, this is the skill to use.
---

# ASCII Diagrams

Create clear, professional ASCII diagrams that live naturally in code comments, documentation, and
technical communication. ASCII diagrams are simultaneously text and visual — they work in every tool
developers already use (editors, terminals, git diffs, code review, commit messages) without external
dependencies.

This skill is grounded in research analyzing 2,156 real diagrams from major open-source codebases
(Linux kernel, Chromium, LLVM, TensorFlow), giving you patterns that real developers actually use and
understand.

## When to create an ASCII diagram

Diagrams are most valuable when they serve as a **thumbnail for code** — less detailed than the code
itself but more approachable, giving readers a mental model before they dive in. The best use cases:

- **Architecture and data flow**: how components connect and data moves between them
- **Data structures and memory layouts**: how bits, bytes, and fields are organized
- **State machines and control flow**: states and transitions in a system
- **Network topology**: how hosts, services, and containers relate
- **Test case visualization**: what a test sets up and expects
- **Algorithms**: step-by-step transformations
- **Before/after comparisons**: showing change over time

A diagram is NOT needed for things that are self-evident from the code. The question to ask: "Would
someone reading this code benefit from a visual overview before diving in?"

## Core principles

### 1. Alignment is everything
Monospace text gives you a grid. Use it. Every character occupies exactly one cell. Vertical lines
must be vertically aligned. Horizontal lines must span consistently. Misaligned diagrams are worse
than no diagram — they confuse rather than clarify.

### 2. Use standard characters that render everywhere
Prefer basic ASCII characters that work in any font, terminal, or tool:

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

Unicode box-drawing characters (`─ │ ┌ ┐ └ ┘ ├ ┤ ┬ ┴ ┼`) produce cleaner output but may break in
some terminals and make diffs harder to read. Use them only when the target context supports it
(e.g., README.md rendered on GitHub). For code comments, stick with ASCII.

### 3. Keep it minimal
A diagram should show the essential structure, not every detail. Real-world diagrams in Linux and
Chromium average 10-20 lines. If your diagram grows beyond ~30 lines, consider splitting it or
simplifying.

### 4. Connect to the code
The best ASCII diagrams reference real identifiers, constants, and expressions from the surrounding
code. When a diagram labels a box `root1`, readers can grep for `root1` in the code. This connection
between diagram and code is what makes ASCII diagrams powerful.

### 5. Show what text cannot
Don't diagram things that are obvious from reading the code linearly. Diagram things that have
**spatial relationships** — hierarchies, networks, layouts, flows with branches — that are hard to
convey in prose.

## Design space — choosing the right form

Before drawing, decide what concept you're showing and which visual form fits it best:

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

For detailed examples, read the reference file for the specific category you need:

| Category | Reference file | Use for |
|----------|---------------|---------|
| Flowcharts | `references/flowcharts.md` | Decision flows, pipelines, control flow |
| State machines | `references/state-machines.md` | Protocol states, lifecycles, transitions |
| Trees | `references/trees.md` | File trees, class hierarchies, org charts |
| Data structures | `references/data-structures.md` | Memory layouts, packets, bit fields, linked lists |
| Network/Architecture | `references/network-topology.md` | K8s topology, service mesh, observability stacks |
| Sequences/Tables | `references/sequences-tables.md` | Request flows, timelines, comparison tables |
| Graphs/Annotations | `references/graphs-annotations.md` | DAGs, code annotations, before/after, UI sketches |

### Flowchart / Control flow
```
  +----------+     +----------+     +----------+
  |  Start   |---->| Process  |---->|   End    |
  +----------+     +----+-----+     +----------+
                        |
                        v
                   +----+-----+
                   | Alternate |
                   +----------+
```

### State machine
```
         +-------+   event_a   +-------+
   ----->| IDLE  |------------>| ACTIVE|
         +---+---+             +---+---+
             ^                     |
             |     event_b         |
             +---------------------+
```

### Tree / Hierarchy
```
    root
    |
    +-- child_a
    |   +-- leaf_1
    |   +-- leaf_2
    |
    +-- child_b
        +-- leaf_3
```

### Data structure / Memory layout
```
  +--------+--------+--------+--------+
  | Header | Type   | Length | Data   |
  | 4 bytes| 2 bytes| 2 bytes| N bytes|
  +--------+--------+--------+--------+
  0        4        6        8        8+N
```

### Network topology
```
  +--------+         +--------+
  | Host A |---eth0--| Switch |---eth1--| Host B |
  +--------+         +--------+         +--------+
                         |
                       eth2
                         |
                     +--------+
                     | Host C |
                     +--------+
```

### Table
```
  Operation    | Time     | Space
  -------------|----------|--------
  Insert       | O(log n) | O(1)
  Search       | O(log n) | O(1)
  Delete       | O(log n) | O(1)
```

### Sequence / Timeline
```
  t0        t1        t2        t3
  |         |         |         |
  v         v         v         v
  [init] -> [load] -> [ready] -> [serve]
```

### Nested containment
```
  +--- Namespace: production --------+
  |                                  |
  |  +--- Pod: api-server -------+  |
  |  |  +--- Container: app --+  |  |
  |  |  |  port: 8080         |  |  |
  |  |  +---------------------+  |  |
  |  +---------------------------+  |
  |                                  |
  +----------------------------------+
```

### Before/After comparison
```
  BEFORE:                    AFTER:
  A --> B --> C              A --> B --> C
        |                         |
        v                         v
        D                    D ---+--> E
```

### Bit field / Register layout
```
  31      24 23    16 15     8 7      0
  +--------+--------+--------+--------+
  | Flags  | Type   | Length | Opcode |
  +--------+--------+--------+--------+
```

## Writing diagrams in code comments

When placing a diagram in a code comment, follow the conventions of the language:

```c
/*
 * Packet structure:
 *
 *  +--------+--------+--------+
 *  | Header | Payload| CRC    |
 *  +--------+--------+--------+
 *  0        8        8+len    8+len+4
 */
```

```python
# Request flow:
#
#   Client --> [Load Balancer] --> [App Server] --> [Database]
#                    |
#                    +-----------> [Cache]
```

```yaml
# Architecture:
#
#   +----------+    +---------+    +--------+
#   | vmagent  |--->| vmtsdb  |--->| vmalert|
#   +----------+    +---------+    +--------+
#                                      |
#                                      v
#                                 +-----------+
#                                 |alertmanager|
#                                 +-----------+
```

## Alignment checklist

Before finalizing any diagram, verify:

1. All vertical lines (`|`) in the same column are aligned
2. All box corners (`+`) connect properly to their horizontal (`-`) and vertical (`|`) lines
3. Arrow heads (`>`, `<`, `^`, `v`) point in the intended direction
4. Labels fit inside boxes without overflow
5. The diagram renders correctly in a monospace font (no proportional font assumptions)
6. If inside a comment block, comment prefixes (`//`, `#`, `*`) don't break alignment
7. Widths are consistent — if one box in a row is 10 chars wide, consider making all boxes in
   that row the same width for visual harmony

## Common mistakes to avoid

- **Broken corners**: `+` must connect to exactly one horizontal and one vertical line segment
- **Floating arrows**: every arrow should clearly connect two elements
- **Over-detail**: if the diagram has more detail than the code, it's too complex
- **No labels**: unlabeled boxes and lines are meaningless — always label
- **Inconsistent spacing**: pick a spacing pattern and stick with it across the whole diagram
- **Proportional font assumptions**: never assume characters have different widths
