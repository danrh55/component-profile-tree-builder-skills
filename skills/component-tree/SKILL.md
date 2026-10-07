---
name: component-tree
description: Coordinates a revisable tree of problem and component nodes, maintains links to component profiles, and manages open questions across the model.
---

# Component Tree Coordination

This skill owns the system-wide model and its links. It coordinates work across nodes and invokes the focused `component-profile` skill when one component profile needs to be created or updated. It does not absorb the detailed elicitation process for an individual profile.

The model is a working set of abstractions developers can use to reason about the problem and trust the layer beneath. Start at the domain or business problem. Let problem areas, needs, workflows, containers, candidate components, and lower-level implementation emerge as useful. A node is not automatically a component, and the model is not a fixed architecture.

## Persistence contract

Inspect the target project before creating artifacts. If it already has a component/specification convention, use it and record the mapping between the tree index and component profiles. Otherwise use this default layout in the target project's repository:

```text
spec/components/
  index.md
  profiles/
    <component-id>.md
```

Persist the artifacts in the target project, not in this skill/agent definition repository.

- `spec/components/index.md` is the canonical source for the root problem, hierarchy, node IDs and types, cross-links, and problem-level open questions/decisions.
- `spec/components/profiles/<component-id>.md` is the canonical source for the detailed profile of that component, including its responsibilities, boundary, conceptual interactions/data flow, evidence, component-level open questions, and rationale.
- Give each node, including the root problem, a stable, unique kebab-case ID. Use the same ID for a component's profile filename. Do not change an ID merely because a display name changes; when a node is split or merged, update the index and affected profile links together.
- Put a stable HTML anchor matching each node ID in the index entry. Link component nodes to profiles with relative Markdown paths. In each profile, link `Tree node` directly to `../index.md#<component-id>`. Use `#<node-id>` links for cross-links so navigation survives display-name changes.
- Keep a question in one canonical location: on the affected problem-space node in the index, in the component profile for component-specific questions, or in a shared-questions section with links to all affected nodes when it spans branches. Do not maintain conflicting copies.
- Keep rationale beside the problem-level or component decision it explains. Do not create a separate learning journal.

If the chosen project convention cannot represent one of these relationships, explain the limitation and agree on a representation before writing. Do not silently create a second index or duplicate the model in another format. Markdown is the default human-readable representation; add structured data or code only when a concrete validation or automation need justifies it.

## Suggested index structure

Use this as a practical starting shape, adapting to project conventions without changing the ownership rules above:

```markdown
# Component Model

## Root problem
<a id="problem-root"></a>
`problem-root`: <User-grounded domain/business problem>

## Tree
- <a id="problem-area-id"></a> `problem-area-id` [problem area]: <current understanding>
  - <a id="workflow-id"></a> `workflow-id` [workflow]: <current understanding>
    - <a id="component-id"></a> `component-id` [component]: <short responsibility> — [profile](profiles/component-id.md)

## Cross-links
- [`component-a`](#component-a) -> [`component-b`](#component-b): <relationship or conceptual flow>

## Shared open questions
- <question; links to affected node IDs; what it may change>

## Problem-level decisions and rationale
- <decision and why>
```

The tree may contain unresolved or provisional nodes. Mark uncertainty in the node text or its open questions; do not turn the suggested shape into a rigid schema.

## Coordination workflow

1. Read project context, existing model artifacts, relevant decisions, and implementation evidence. Identify the project's persistence convention before proposing paths.
2. Establish or refine the root problem from user-provided context. If it is unclear, explore the problem with the user rather than inventing a root statement.
3. Help the user add or revise only the nodes needed for the current understanding. Use hierarchy for decomposition and explicit cross-links for relationships across branches. Keep the model provisional.
4. When a candidate component needs a detailed profile, invoke `skills/component-profile/SKILL.md` (using `agents/component-profile.md` when the agent framework requires an agent prompt). Give it the node ID, parent/neighbor context, known links, evidence, and agreed artifact path. Let that skill own the profile conversation and file.
5. Integrate the profile result into the index: add or update the matching component node and relative profile link; update cross-links and affected open questions when relevant. Do not duplicate full profile content in the index.
6. When evidence changes boundaries, propose the affected node/link/profile changes together, explain why, and get user agreement before updating persisted artifacts.
7. Work one selected component at a time when moving toward technical work. Carry forward its parent/neighbor context, conceptual data flow, evidence, and open questions; do not treat the tree or profile as an executable contract.

## Rules

- Keep problem-space nodes and component nodes distinct where that helps reasoning; do not force early componentization.
- Keep the index concise enough to reveal the model and navigate it. Put component detail in its profile.
- Track open questions at the nodes they affect and state likely impact. Continue on independent branches where useful.
- Preserve decisions and evidence from solving the real problem so future changes remain understandable; learning happens through the problem-solving work itself.
- Before writing or updating artifacts, summarize the proposed changes and resolve conflicts with the user. Report all paths created or updated and the links changed.
