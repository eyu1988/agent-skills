# agent-skills

A collection of agent skills for Claude and Codex.

## Structure

```
agent-skills/
├── claude/
│   ├── eyu-record/                 # Write content to daily capture file
│   ├── eyu-process-daily/          # Process and distill daily captures into knowledge base
│   └── eyu-log-pain/               # Log a new pain point with 5Why analysis and optional deep dive
└── codex/
    ├── eyu-record/
    ├── eyu-process-daily/
    ├── eyu-business-guide-writer/  # Create business-first module technical guides
    ├── eyu-munger-mental-models/   # Apply Charlie Munger-style mental models to decisions
    ├── eyu-claude-style-collab/    # Tune Codex to Claude Code's collaboration style
    └── eyu-log-pain/               # Log a new pain point with 5Why analysis and optional deep dive
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

### log-pain (claude, codex)

Logs a new pain point into the pain management system. Auto-classifies domain and severity, runs a 5Why root cause analysis, appends to the registry, and optionally creates a three-layer solution file set.

Trigger: `录入痛点：[描述]` / `我有个痛点` / `/log-pain [描述]`

Required config:
- `PAIN_DIR` — path to your pain management system directory

### business-guide-writer (codex)

Creates or improves business-first module technical guide documents. Focuses on business concepts, user scenarios, permissions, state transitions, data flow, and troubleshooting entry points.

Trigger: `write a business guide` / `业务导读` / `module guide`

### munger-mental-models (codex)

Applies Charlie Munger-style multidisciplinary mental models to decisions. Use for decision analysis, risk identification, inversion thinking, incentive analysis, and opportunity cost evaluation.

Trigger: `decision analysis` / `mental models` / `munger`

### claude-style-collab (codex)

Tunes Codex to Claude Code's collaboration style: read code before acting, default to execution over discussion, sync progress continuously, self-verify after changes, and close the loop with results.

Trigger: `像 Claude 那样配合` / `按 Claude Code 的方式来` / `不要只分析，直接做完`

## Placeholders

Skills use `{{VAR}}` placeholders replaced at install time by skill-hub:

| Placeholder | Description |
|-------------|-------------|
| `{{CAPTURE_DIR}}` | Absolute path to daily capture directory |
| `{{KNOWLEDGE_DIR}}` | Absolute path to knowledge base root directory |
| `{{PAIN_DIR}}` | Absolute path to pain management system directory |
