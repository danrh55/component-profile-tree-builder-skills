# Initial Architecture Workflow

This repository provides a portable workflow for framing an initial architecture in a new project or early build. The [component-tree skill](skills/component-tree/SKILL.md) owns the authoritative sequence, layer and folder conventions, specialist handoff, and user review. Read it before starting; it links to the focused problem-framing and component-profile skills it uses.

## Install

From the target project's root, run:

```sh
git clone https://github.com/danrh55/project-framing-agent.git .project-framing-agent
```

## Start

In a coding-agent session opened at the target project root, ask:

> Follow `.project-framing-agent/skills/component-tree/SKILL.md` to establish an initial architecture frame for this project. Inspect the repository and work with me through the workflow. Do not start implementation until I choose the next step.

The workflow does not depend on a particular coding harness. The optional `agents/` files are short role prompts for harnesses that support custom agent definitions; other harnesses can invoke the skills directly. Architecture artifacts belong in the target project's normal source folders, not in the cloned workflow directory.
