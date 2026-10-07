# Initial Architecture Workflow

This repository provides an agent for framing an initial architecture in a new project or early build. The component-tree agent owns the conversation; its linked skill supplies the authoritative workflow, conventions, specialist handoff, and review steps.

## Install

From the target project's root, run:

```sh
git clone https://github.com/danrh55/component-profile-tree-builder-skills.git .component-profile-tree-builder-skills
```

## Start

In a coding-agent session opened at the target project root, select or delegate to the installed component-tree agent and ask it to establish an initial architecture frame. If your harness uses agent files as prompt context, provide `agents/component-tree.md` to the agent. The agent will follow its skill and use the focused problem-framing and component-profile skills as needed.

The workflow does not depend on a particular coding harness, though harnesses differ in how they install and select agents. Architecture artifacts belong in the target project's normal source folders, not in the cloned workflow directory.
