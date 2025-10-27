# Core Tools

> **Note:** Each tool comes with its own multi-step workflow, parameters, and descriptions that consume valuable context window space even when not in use. To optimize performance, some tools are disabled by default. See Tool Configuration below to enable them.

## Collaboration & Planning (Enabled by default)

- **clink** - Bridge requests to external AI CLIs (Gemini planner, codereviewer, etc.)
- **chat** - Brainstorm ideas, get second opinions, validate approaches. With capable models (GPT-5 Pro, Gemini 2.5 Pro), generates complete code/implementation.
- **thinkdeep** - Extended reasoning, edge case analysis, alternative perspectives.
- **planner** - Break down complex projects into structured, actionable plans.
- **consensus** - Get expert opinions from multiple AI models with stance steering.

## Code Analysis & Quality

- **debug** - Systematic investigation and root cause analysis.
- **precommit** - Validate changes before committing, prevent regressions.
- **codereview** - Professional reviews with severity levels and actionable feedback.
- **analyze** - Understand architecture, patterns, dependencies across entire codebases (disabled by default).

## Development Tools (Disabled by default)

- **refactor** - Intelligent code refactoring with decomposition focus.
- **testgen** - Comprehensive test generation with edge cases.
- **secaudit** - Security audits with OWASP Top 10 analysis.
- **docgen** - Generate documentation with complexity analysis.

## Utilities

- **apilookup** - Forces current-year API/SDK documentation lookups in a sub-process, prevents outdated training data responses.
- **challenge** - Prevent "You're absolutely right!" responses with critical analysis.
- **tracer** - Static analysis prompts for call-flow mapping (disabled by default).

## 📺 Watch Tools In Action

### Chat Tool

- Collaborative decision making and multi-turn conversations.

**Picking Redis vs Memcached:**

- Multi-turn conversation with continuation.

### Consensus Tool

- Multi-model debate and decision-making.

**Multi-model consensus debate:**

### PreCommit Tool

- Comprehensive change validation.

**Pre-commit validation workflow:**

### API Lookup Tool

- Current vs outdated API documentation.

**Without Zen - outdated APIs:**

**With Zen - current APIs:**

### Challenge Tool

- Critical thinking vs reflexive agreement.

**Without Zen:**

**With Zen:**

## Key Features

### AI Orchestration

- **Auto model selection** - Claude picks the right AI for each task.
- **Multi-model workflows** - Chain different models in single conversations.
- **Conversation continuity** - Context preserved across tools and models.
- **Context revival** - Continue conversations even after context resets.

### Model Support

- **Multiple providers** - Gemini, OpenAI, Azure, X.AI, OpenRouter, DIAL, Ollama.
- **Latest models** - GPT-5, Gemini 2.5 Pro, O3, Grok-4, local Llama.
- **Thinking modes** - Control reasoning depth vs cost.
- **Vision support** - Analyze images, diagrams, screenshots.

### Developer Experience

- **Guided workflows** - Systematic investigation prevents rushed analysis.
- **Smart file handling** - Auto-expand directories, manage token limits.
- **Web search integration** - Access current documentation and best practices.
- **Large prompt support** - Bypass MCP's 25K token limit.

## Example Workflows

### Multi-model Code Review

- "Perform a codereview using gemini pro and o3, then use planner to create a fix strategy"

→ Claude reviews code systematically → Consults Gemini Pro → Gets O3's perspective → Creates unified action plan

### Collaborative Debugging

- "Debug this race condition with max thinking mode, then validate the fix with precommit"

→ Deep investigation → Expert analysis → Solution implementation → Pre-commit validation

### Architecture Planning

- "Plan our microservices migration, get consensus from pro and o3 on the approach"

→ Structured planning → Multiple expert opinions → Consensus building → Implementation roadmap