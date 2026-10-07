---
name: problem-framing
description: Helps the user define and validate the domain or business problem that anchors the initial layered architecture.
---

# Problem Framing

Define the user-grounded domain or business problem that anchors the initial layered architecture. This is especially useful at the start of a project when the repository has too little code or context to guide feature work.

This skill owns the domain problem frame only. It does not decompose the architecture into contexts, containers, or components, and it does not choose a solution. The frame should describe the problem and intended outcome in terms a developer can use to reason about the work, without prematurely choosing an architecture or implementation.

## Procedure

1. Read available project context: the user's description, repository instructions, relevant documentation, existing root frame, and any evidence the user has provided. Do not infer a business problem from a blank repository.
2. Identify which root-frame details are already known and which are missing. Elicit only the missing details, one area at a time. Keep the user's wording and distinguish their claims from your interpretation.
3. Where needed, clarify:
   - the domain or business context;
   - who experiences or is affected by the problem;
   - what problem, unmet need, or friction occurs;
   - why it matters, including evidence or consequences;
   - what outcome would count as improvement, without prescribing a solution.
4. Draft a concise problem statement grounded in the user's answers. Keep supporting context, evidence, assumptions, and open questions visible. Do not fill gaps with plausible guesses.
5. Present the proposed root frame for the user's correction. If it conflicts with an existing frame or evidence, explain the conflict instead of smoothing it over.
6. Return the user-accepted frame to the coordinator. Do not create a separate problem brief or edit architecture files; the coordinator places this context in the domain layer's `architecture.md`.

## Output contract

Return a concise proposal with:

- a short, solution-independent problem statement;
- a user-approved domain name or folder label, if one is clear;
- known context, affected people/processes, impact, and evidence (only where established);
- explicit assumptions and open questions;
- confirmation that the user accepts the wording, or a note that it remains unresolved.

The coordinator persists the accepted frame in `<source-root>/<domain>/architecture.md`, or the equivalent domain-layer document in the project's existing layout. This is contextual documentation for the initial build, not a canonical source of truth. Do not create a competing problem brief.

## Rules

- The user is the source of the problem definition. Ask instead of inventing.
- Do not confuse a requested feature or proposed solution with the underlying problem; ask what need or outcome it addresses when that distinction is unclear.
- Do not require implementation code. Use it as context only when available and relevant.
- Do not start decomposition, component profiling, or implementation planning in this skill.
- Keep the framing concise and revisable. It is a useful starting point, not a permanent project charter.
