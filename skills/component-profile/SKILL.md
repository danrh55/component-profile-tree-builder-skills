---
name: component-profile
description: Helps the user create or refine one component's concise architecture context within an initial layered project model.
---

# Component Architecture Context

This skill helps document one component's place in the initial architecture frame. Its output is context for the user, coordinator, and later coding/spec agents; it is not the component's detailed technical spec and is not a permanent contract.

## Inputs

Read the component's parent-layer document, relevant neighboring documents, project conventions, and code/evidence when available. The coordinator should provide the component's folder path and any specialist-spec context. If the component boundary or destination is unclear, surface that rather than inventing it.

The user owns the model. Ask about one area at a time, use their terminology, and keep known facts, assumptions, and open questions distinct. A profile can be useful while details remain unresolved.

## Useful prompts

Use only the prompts that help explain this component's role and connections:

- **Responsibility** — what it does and what belongs elsewhere.
- **Boundary** — why the component is a useful unit and how it relates to its parent container and neighboring components.
- **Interactions and data flow** — what crosses its boundary conceptually and where that information or effect goes.
- **Grounding** — relevant parent/neighbor documents, decisions, evidence, code modules, or specialist spec.
- **Questions and rationale** — what remains unclear and why current boundaries or relationships were chosen.

Do not force a fixed form when a short diagram, bullets, or links explain the component more clearly. When a template helps, use:

```markdown
# <Component name>

## Responsibility and boundary
## Relationships and data flow
## Code mapping (when code exists)
## Grounding / rationale
## Open questions
```

## Persistence and coordination

Write the component architecture context into the component's `architecture.md` at the path provided by the coordinator. In a greenfield layout this will be under `<source-root>/<domain>/<context>/<container>/<component>/architecture.md`; follow existing repository conventions when present.

This skill owns only the component's concise architecture context. It does not maintain a tree, create a second component spec, or require the initial folder organization to remain fixed. If a specialist spec is provided, summarize only the architectural implications and link to the specialist's durable output when available; do not duplicate its contents.

Before changing an existing document, summarize the proposed change and resolve conflicts with the user. Return the file path, a short summary, related components/documents, and any unresolved questions to the coordinator.

## Rules

- Do not invent exact interface shapes, implementation plans, or test requirements; those belong in a detailed component spec.
- Use code as evidence when it exists, not as the sole definition of component boundaries.
- A folder path is an initial navigation cue, not proof of runtime relationships.
- Keep the document useful for understanding and review. Avoid speculative detail and preserve useful rationale as the real problem is solved.
