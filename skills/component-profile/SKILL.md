---
name: component-profile
description: Helps the user create or update the profile for one named component, capturing its responsibility, boundary, conceptual interactions, evidence, and open questions.
---

# Component Profile

A component profile captures the user's current understanding of one component. It is a revisable conceptual description, not an implementation plan or technical contract. This skill owns the content of one profile; it does not own or coordinate the system-wide tree.

## Inputs and context

Before asking questions, read the target component's existing profile if present, the parent/tree context provided by the caller, and relevant neighboring profiles or evidence. Use that context to ground the conversation. If the component or its location is unclear, resolve that with the user rather than inventing an identifier or path.

The user owns the content. Ask what is known, draft only from information already provided, and mark gaps as unknowns. Keep the user's vocabulary. Work through one section at a time; do not present the full template as a questionnaire.

## Profile sections

- **Purpose / responsibility** — why it exists, what it owns, and what it leaves to others.
- **Conceptual model** — how it works in plain language.
- **Boundary and role** — how it relates to its parent, children, and neighboring components, and why the boundary is useful.
- **Interactions and data flow** — what information or effects cross the boundary conceptually, and where they come from and go. Do not invent exact interface shapes.
- **Grounding / evidence** — relevant lower-level behavior, decisions, profiles, or code that supports or challenges the current model.
- **Invariants** — what must remain true regardless of implementation.
- **Non-goals** — what the user explicitly wants this component not to do.
- **Open questions** — known unknowns, affected nodes, and what each question could change or block.
- **Decisions and rationale** — choices and reasoning/evidence that help explain the current model as it changes.

## Suggested profile template

```markdown
---
id: <stable-component-id>
---

# <Component name>

Tree node: [<stable-component-id>](../index.md#<stable-component-id>)

## Purpose / responsibility
## Conceptual model
## Boundary and role
## Interactions and data flow
## Grounding / evidence
## Invariants
## Non-goals
## Open questions
## Decisions and rationale
```

## Persistence and coordination

When working within the component-tree workflow, persist component profiles at `spec/components/profiles/<component-id>.md`. The corresponding tree node in `spec/components/index.md` is the canonical record of hierarchy and cross-links; the profile links back to that node by its stable ID. Use the project's existing convention instead if the tree coordinator has identified one, and keep the index/profile links explicit.

This skill writes or updates only the requested component profile. It reports the profile path and a concise summary to the caller, which is responsible for reflecting relevant relationship or status changes in the tree index. Do not create or rewrite the tree index from this skill.

Before updating an existing profile, summarize the proposed changes and incorporate the user's corrections. Do not write until the user accepts the content and a destination path/convention is clear.

## Rules

- Keep this profile conceptual. Exact schemas, executable interfaces, and implementation details belong in a later technical contract.
- Do not infer boundaries from code structure alone; use code as evidence and surface conflicts with the user's model.
- Do not resolve open questions by guessing. State their impact and leave them open.
- Preserve useful rationale from solving the real problem; do not add a separate training or exercise process.
```
