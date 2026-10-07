---
name: component-tree
description: Coordinates a revisable tree of problem and component nodes, maintains links to component profiles, and manages open questions across the model.
---

# Component Tree Coordination

This skill is a project-start workflow for a coding agent. Use it when a project is new, its repository has little code or context, or ordinary feature prompts would force the agent to guess the system structure. It creates a predictable starting model before implementation work begins.

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

## Workflow state
- Stage: framing | tree | profiles | review | handoff
- Next action: <one concrete action or "awaiting user input">

## Root problem
<a id="problem-root"></a>
`problem-root`: <concise, user-accepted, solution-independent problem statement>
- Context / affected people or processes: <known details>
- Impact / evidence: <known details>
- Desired outcome: <solution-independent outcome>
- Assumptions / open questions: <known unknowns>

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

Run these stages in order. Persist the current stage and one concrete next action in the index so another coding-agent session can resume without reconstructing progress. A stage is complete only when its exit condition is met; if new information invalidates an earlier result, return to that stage and update affected artifacts.

1. **Frame** — Inspect available repository files, instructions, documentation, and code for context. Invoke `skills/problem-framing/SKILL.md` (or `agents/problem-framing.md` when the framework requires an agent prompt) to elicit and validate the user-grounded domain/business problem. Carry its accepted root statement, context, evidence, assumptions, and open questions into the `## Root problem` section of the index. Exit when the user accepts the root statement. Do not infer the product problem from a blank repo.
2. **Build the tree** — Create the index with the root, useful problem-space nodes, known relationships, and open questions. Nodes may remain provisional and need not be components. Exit when the user accepts this as a useful starting frame; completeness is not required.
3. **Profile components** — With the user, select one candidate component at a time. Invoke `skills/component-profile/SKILL.md` (or `agents/component-profile.md` when the framework requires an agent prompt), providing its node ID, parent/neighbor context, known links, evidence, and agreed path. Integrate the accepted profile link into the index. Repeat only for components the user wants to clarify now.
4. **Review the model** — Check that every profiled component has a matching index node and stable ID, profile links resolve in both directions, cross-links are understandable, and open questions are attached to the affected nodes. Surface conflicts and missing context; do not resolve them by guessing. Exit when the user has reviewed the proposed model and remaining gaps are visible.
5. **Handoff** — Summarize the problem frame, current tree, profiled components, important interactions/data flows, and open questions. Identify a possible next component for technical-contract work, but let the user choose whether and where to proceed. Mark the workflow as handed off; do not start implementation as part of this workflow.

Before persisting a stage's result, show the proposed changes and incorporate the user's corrections. If the user wants to stop early, save the current stage and next action when they authorize persistence. When new evidence changes boundaries, propose affected node/link/profile changes together and update only after agreement.

Do not require source code to begin. Use code as grounding evidence when it exists; when it does not, mark implementation-level details unknown and continue with the problem model.

## Rules

- Keep problem-space nodes and component nodes distinct where that helps reasoning; do not force early componentization.
- Keep the index concise enough to reveal the model and navigate it. Put component detail in its profile.
- Treat the ordered stages and their exit conditions as the predictable workflow; keep the model itself revisable.
- Track open questions at the nodes they affect and state likely impact. Continue on independent branches where useful.
- Preserve decisions and evidence from solving the real problem so future changes remain understandable; learning happens through the problem-solving work itself.
- Before writing or updating artifacts, summarize the proposed changes and resolve conflicts with the user. Report all paths created or updated and the links changed.
