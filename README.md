# agent-skills

A collection of agent skills for Claude and Codex.

## Structure

```
agent-skills/
├── claude/
│   ├── record/         # Write content to daily capture file
│   └── process-daily/  # Process and distill daily captures into knowledge base
└── codex/
    ├── record/
    └── process-daily/
```

## Installation

Install skills via [skill-hub](https://github.com/eyu1988/skill-hub):

```bash
# Install skill-hub
npm install -g skill-hub

# Set default repo
skill-hub config set DEFAULT_REPO eyu1988/agent-skills

# Configure paths (prompted automatically on first install)
skill-hub config set CAPTURE_DIR "/path/to/your/daily-captures"
skill-hub config set KNOWLEDGE_DIR "/path/to/your/knowledge-base"

# Install all Claude skills
skill-hub install --agent claude

# Install all Codex skills
skill-hub install --agent codex

# Install a single skill
skill-hub install --agent claude --skill record
```

## Skills

### record

Writes content to today's daily capture file.

Trigger: `记录一下：[content]` / `/record [content]`

Required config:
- `CAPTURE_DIR` — path to your daily capture directory

### process-daily

Reads today's capture file, filters and distills entries into the knowledge base.

Trigger: `处理今天` / `/process-daily`

Required config:
- `CAPTURE_DIR` — path to your daily capture directory
- `KNOWLEDGE_DIR` — path to your knowledge base root directory

## Placeholders

Skills use `{{VAR}}` placeholders replaced at install time by skill-hub:

| Placeholder | Description |
|-------------|-------------|
| `{{CAPTURE_DIR}}` | Absolute path to daily capture directory |
| `{{KNOWLEDGE_DIR}}` | Absolute path to knowledge base root directory |
