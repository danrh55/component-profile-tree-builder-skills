---
name: component-tree
description: Coordinates an initial domain-to-code architecture frame, layer documents, and optional specialist component specs for a new project or early build.
---

# Initial Architecture Coordination

Use this workflow inside a coding agent when a project is new or has too little code and context for feature work to be grounded. Its purpose is to reduce cognitive overload by helping the developer and coding agent form a useful initial picture of how the system connects.

This is an initial-build coordination workflow, not a permanent architecture authority. The folder layout and documents are contextual aids for the user and agents. As the project grows, its composition and code organization may change; do not treat this first model as a constraint or promise to keep every document synchronized indefinitely.

The initial layer progression is **domain → context → containers → components → code**. Use the folders to show parent/child decomposition and documents to describe relationships and flows. This is a useful starting shape, not a complete representation of every dependency: allow cross-links and explanations where the structure is more complex than a tree.

## Folder and document convention

Inspect the target repository first. Follow its source-root and naming conventions when present. For a greenfield project without a source layout, use:

```text
src/<domain>/
  architecture.md
  <context>/
    architecture.md
    <container>/
      architecture.md
      <component>/
        architecture.md
        <implementation files as they are built>
```

Create folders and documents as layers are understood; do not scaffold speculative branches. Every layer/node included in the initial model gets a flexible `architecture.md`; if a conventional layer (such as a distinct context or container) does not fit, explain that in the nearest useful document rather than creating an empty directory. The domain document contains the problem frame. A component document describes its architecture context and, when code exists, points to the relevant modules or files. Do not create a document for every code file.

These documents are not a canonical source of truth. Do not create a mandatory central index or duplicate all relationships in a registry. Use directory nesting to make the initial decomposition visible, and use relative links in layer documents for parent/child references and relationships that cross branches. The coordinator can summarize the current structure from the files when an agent or user needs a compact view.

Keep each document proportionate to the understanding available. Prompt the user to explain why the layer exists, what it breaks into, and how its children relate or move information. Also capture conceptual interactions/data flow, evidence or rationale, assumptions, and open questions where useful. Make unknown connections explicit before moving down a layer; do not require exhaustive detail or force a settled answer when the user is uncertain. Architecture documents provide context; they are not technical contracts or a requirement to preserve the initial organization as the project evolves.

## Coordination workflow

Run these stages in order, one layer at a time. Determine progress by inspecting the target folders and documents; do not require a separate workflow-state file. A stage may contain explicit unknowns and still be useful. Return to an earlier layer when new information changes the frame.

1. **Discover** — Read repository instructions, source layout, existing architecture notes, code, and terminology. Identify the source root and any conventions to preserve. Do not reorganize established code as a side effect of creating an initial model.
2. **Domain** — Invoke `skills/problem-framing/SKILL.md` (or `agents/problem-framing.md` when an agent prompt is required). Carry the user-accepted problem frame into `<source-root>/<domain>/architecture.md`. Do not create a separate problem brief.
3. **Context** — Identify the system boundary, important people or external systems, and how the domain is realized in the product. If context is a useful distinct layer, create a context folder and `architecture.md` for each modeled context; otherwise note why it is folded into the domain or container layer.
4. **Containers** — Describe the major runtime/deployment or responsibility groupings that help explain the system. Create one container directory and layer document for each understood container. Do not force an unfamiliar architecture pattern if it does not fit the project.
5. **Components** — Identify candidate components within a container and work on one at a time. Use `skills/component-profile/SKILL.md` for the concise architectural context of a component. Then, when a compatible specialist skill or subagent is available and appropriate, pass it a component context packet and request its detailed spec. Do not install external skills automatically or reproduce their detailed workflow.
6. **Reconcile** — Receive the specialist's spec or findings in the coordinator context. Update the relevant layer documents with architectural implications, connections, conflicts, and open questions. Do not copy the entire specialist spec into architecture documents. Link to a durable specialist artifact only when the specialist provides a stable reference; otherwise use its returned context in this coordination session.
7. **Code context and handoff** — Code is the layer beneath components. When implementation exists, map component documents to actual modules/files and explain important runtime flows; do not create per-file architecture documents. Do not invent code paths or define the later implementation endpoint in advance. Summarize the current folder frame, documents created, cross-layer relationships, unresolved questions, and any specialist outputs; let the user choose the next build step.

Before writing project artifacts, show the proposed folder/document changes and incorporate the user's corrections. Keep the workflow's structure predictable, but allow the user to stop after any layer. Existing files and later architectural changes take precedence over the initial frame.

## Optional specialist interface

When delegating a component spec, give the specialist:

- the component's role and boundary in the current layer model;
- its parent container/context and relevant neighboring components;
- known interactions/data flows, evidence, assumptions, and open questions;
- the user's intended outcome and any existing project conventions.

Ask the specialist to return its spec or a useful summary, unresolved decisions, architectural impacts, and a durable artifact reference if one exists. The specialist may use its own configured persistence destination. The coordinator consumes the returned context; it does not require or create a duplicate copy. Matt Pocock's `to-spec`, domain-modeling, or codebase-design workflows are possible integrations when installed, but this workflow must remain usable without them.

## Rules

- The user's problem and current understanding define the initial frame; do not infer missing architecture from folder names alone.
- Require enough connection detail to make the model useful, but do not demand exhaustive or settled relationships. Open questions are acceptable and should remain visible.
- A folder path suggests initial decomposition; it does not prove ownership, dependency, or runtime flow. Explain those in the relevant documents.
- Preserve terminology and rationale that help the developer understand the problem and trust the layer below. Learning comes from solving the real problem, not from adding separate exercises or journals.
- Do not keep running this bootstrap workflow as a general large-project architecture governance process. When the initial frame no longer fits, acknowledge it and let the user choose a suitable redesign workflow.
