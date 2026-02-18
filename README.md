# Nexus

[![built using gptme](https://img.shields.io/badge/built%20using-gptme%20%F0%9F%A4%96-5151f5?style=flat)](https://github.com/ErikBjare/gptme)

The name of the agent is Nexus.

This git repository is the brain of Nexus. It is a workspace of their thoughts and ideas.

 - Nexus will write their thoughts, plans, and ideas in this repository.
 - Nexus's agent harness, including this repo, is in-progress.
 - Nexus is encouraged to suggest improvements to their harness.

Information about Nexus can be found in [`ABOUT.md`](./ABOUT.md), including their personality and goals.
Information about Nexus's harness and architecture can be found in [`ARCHITECTURE.md`](./ARCHITECTURE.md).



## Quick Start

The easiest way to create a new agent from this template is with the `Nexus` CLI (included with gptme):

```sh
pipx install gptme

# Create a new agent workspace from this template
Nexus create ~/my-agent --name MyAgent

cd ~/my-agent

# Run the agent interactively
gptme "hello"
```

The agent's context is automatically loaded via `gptme.toml` which configures the files and context command to include.

## Autonomous Operation

Agents can run autonomously on a schedule using systemd (Linux) or launchd (macOS):

```sh
# Install as a system service (runs every 30 minutes by default)
Nexus install

# Customize the schedule
Nexus install --schedule "*:00"    # Every hour

# Manage the agent
Nexus status              # Check status
Nexus logs --follow       # Monitor logs
Nexus run                 # Trigger immediate run
Nexus stop                # Pause scheduled runs
```

To customize the autonomous behavior, edit `scripts/runs/autonomous/autonomous-run.sh` with your agent's details and prompt.

**See**: [`scripts/runs/autonomous/README.md`](./scripts/runs/autonomous/README.md) for complete documentation.

**Features**:
- CASCADE workflow (Loose Ends → Task Selection → Execution)
- Two-queue system (manual + generated priorities)
- Safety guardrails (GREEN/YELLOW/RED operation classification)
- Session documentation and state management

## Forking (manual alternative)

If you prefer to fork manually instead of using `Nexus create`:

```sh
git clone https://github.com/gptme/Nexus
cd Nexus
git submodule update --init --recursive

./scripts/fork.sh <path> [<agent-name>]
```

Then follow the instructions in the output.

## Workspace Structure

 - Nexus keeps track of tasks in [`TASKS.md`](./TASKS.md)
 - Nexus keeps a journal in [`./journal/`](./journal/)
 - Nexus keeps a knowledge base in [`./knowledge/`](./knowledge/)
 - Nexus maintains profiles of people in [`./people/`](./people/)
 - Nexus manages work priorities in [`./state/`](./state/) using the two-queue system (manual + generated)
 - Nexus uses scripts in [`./scripts/`](./scripts/) for context generation, task management, and automation
 - Nexus can add files to [`gptme.toml`](./gptme.toml) to always include them in their context

### Key Directories

**[`state/`](./state/)**: Work queue management
- `queue-manual.md` - Manually maintained work queue with strategic context
- `queue-generated.md` - Auto-generated queue from tasks and GitHub
- See [`state/README.md`](./state/README.md) for detailed documentation

**[`scripts/`](./scripts/)**: Automation and utilities
- `context.sh` - Main context generation orchestrator
- `gptodo` - Task management CLI (install from gptme-contrib)
- `runs/autonomous/` - Autonomous operation infrastructure
- See [`scripts/README.md`](./scripts/README.md) for complete documentation

**[`lessons/`](./lessons/)**: Behavioral patterns and constraints
- Prevents known failure modes through structured guidance
- See [`lessons/README.md`](./lessons/README.md) for lesson system documentation
