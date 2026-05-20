# agent-skills

A collection of agent skills for Claude and Codex.

## Structure

```
agent-skills/
├── claude/
│   ├── eyu-record/                 # Write content to daily capture file
│   └── eyu-process-daily/          # Process and distill daily captures into knowledge base
└── codex/
    ├── eyu-record/
    ├── eyu-process-daily/
    ├── eyu-business-guide-writer/  # Create business-first module technical guides
    └── eyu-munger-mental-models/   # Apply Charlie Munger-style mental models to decisions
```

## Installation

Install skills via [skill-hub](https://github.com/eyu1988/skill-hub).

### Claude (default)

```bash
# Install skill-hub
npm install -g @eyu1988/skill-hub --registry https://registry.npmjs.org/

# Configure
skill-hub config set DEFAULT_REPO eyu1988/agent-skills
skill-hub config set DEFAULT_AGENT claude
skill-hub config set CAPTURE_DIR "/path/to/your/daily-captures"
skill-hub config set KNOWLEDGE_DIR "/path/to/your/knowledge-base"

# Install all skills
skill-hub install
```

### Codex (primary agent)

```bash
# Install skill-hub
npm install -g @eyu1988/skill-hub --registry https://registry.npmjs.org/

# Configure
skill-hub config set DEFAULT_REPO eyu1988/agent-skills
skill-hub config set DEFAULT_AGENT codex
skill-hub config set CAPTURE_DIR "/path/to/your/daily-captures"
skill-hub config set KNOWLEDGE_DIR "/path/to/your/knowledge-base"

# Install all skills
skill-hub install
```

### Common commands

```bash
skill-hub install --skill record        # Install a single skill
skill-hub update                        # Update all skills
skill-hub update --skill record         # Update a single skill
skill-hub remove --skill record         # Remove a single skill
skill-hub list                          # List installed skills
skill-hub search                        # List available skills in repo
skill-hub config list                   # Show current config
```

## Skills

### record (claude, codex)

Writes content to today's daily capture file.

Trigger: `记录一下：[content]` / `/record [content]`

Required config:
- `CAPTURE_DIR` — path to your daily capture directory

### process-daily (claude, codex)

Reads today's capture file, filters and distills entries into the knowledge base.

Trigger: `处理今天` / `/process-daily`

Required config:
- `CAPTURE_DIR` — path to your daily capture directory
- `KNOWLEDGE_DIR` — path to your knowledge base root directory

### business-guide-writer (codex)

Creates or improves business-first module technical guide documents. Focuses on business concepts, user scenarios, permissions, state transitions, data flow, and troubleshooting entry points.

Trigger: `write a business guide` / `业务导读` / `module guide`

### munger-mental-models (codex)

Applies Charlie Munger-style multidisciplinary mental models to decisions. Use for decision analysis, risk identification, inversion thinking, incentive analysis, and opportunity cost evaluation.

Trigger: `decision analysis` / `mental models` / `munger`

## Placeholders

Skills use `{{VAR}}` placeholders replaced at install time by skill-hub:

| Placeholder | Description |
|-------------|-------------|
| `{{CAPTURE_DIR}}` | Absolute path to daily capture directory |
| `{{KNOWLEDGE_DIR}}` | Absolute path to knowledge base root directory |
