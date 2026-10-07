# Initial Architecture Workflow

Clone this repository into a new project, then ask your coding agent to follow the component-tree workflow. The workflow is a set of portable instructions and does not require a particular coding harness.

## Install

From the target project's root, run:

```sh
git clone https://github.com/danrh55/project-framing-agent.git .project-framing-agent
```

This adds the workflow to `.project-framing-agent/` in your project. The architecture artifacts it creates belong in your project’s normal source folders, not inside the cloned workflow directory.

## Start

In a session opened at the target project root, ask your coding agent:

> Use the component-tree workflow in `.project-framing-agent/skills/component-tree/SKILL.md` to establish an initial architecture frame for this project. Inspect the repository first. Then work with me through the domain, context, containers, and components one layer at a time. Ask focused questions, keep unknowns visible, and explain how each layer connects to the next. Propose folders and `architecture.md` files before writing them. For detailed component specs, use an installed specialist skill if available, then bring its output back and reconcile the architectural implications. Do not start implementation until I choose the next step.

Answer the framing questions and review the proposed folders and documents. You can stop after any layer. To resume later, ask your coding agent to inspect the existing layer folders and continue from there.

## What it creates

For a greenfield project, the starting layout is:

```text
src/
└── <domain>/
    ├── architecture.md
    └── <context>/
        ├── architecture.md
        └── <container>/
            ├── architecture.md
            └── <component>/
                ├── architecture.md
                └── <implementation files later>
```

The workflow creates folders only as the model develops. Existing project conventions take precedence. Each layer document gives the user and agents context about that layer's responsibility, decomposition, relationships/data flow, and open questions. Folder nesting shows the initial decomposition; document links explain connections that cross branches.

These documents are working context, not a permanent source of truth. The project may outgrow the initial composition or change its code organization. Revise or replace the initial frame when that becomes more useful than preserving it.

## Component specs

The component `architecture.md` is a short explanation of where that component fits. For a detailed spec, use a compatible specialist skill or subagent if available. Pass it the component context and have it return the spec or findings, unresolved decisions, and architectural implications to the coordinator. The specialist may save its output to its configured destination; the coordinator does not copy the full spec into the architecture documents.

If no specialist is available, the coordinator can still capture the initial architecture context and leave detailed specs as follow-up work.

The `skills/` directory contains reusable workflows for defining the problem, coordinating the tree, and profiling a component. Read the relevant `SKILL.md` when needed. The optional `agents/` files are role prompts for harnesses that support custom agent definitions; the core workflow does not depend on a particular agent format.
