# Multi-Agent Workflows for OpenCode

This directory contains commands, skills, and agents that enable sophisticated multi-agent workflows optimized for fast inference.

## Key Feature: Parallel Multi-Agent Execution

The workflows leverage parallel agent execution to dramatically reduce total processing time. When running on fast inference platforms, multiple specialized agents can analyze code simultaneously, providing comprehensive feedback in seconds instead of minutes.

## Commands

### `/plan` - Feature Planning
Transform feature descriptions into well-structured project plans using parallel research agents.

```
/plan Add user authentication with OAuth support
```

**Features:**
- Detects existing brainstorm documents
- Runs parallel research agents for context gathering
- Creates structured plan documents with multiple detail levels
- Supports integration with GitHub Issues

### `/review` - Multi-Agent Code Review
Run comprehensive code reviews with 5+ specialized reviewer agents in parallel.

```
/review 123          # Review PR #123
/review feature-branch  # Review a branch
```

**Review Agents:**
- `security-sentinel` - Security vulnerabilities and OWASP compliance
- `performance-oracle` - Performance bottlenecks and scalability
- `architecture-strategist` - Architectural patterns and SOLID principles
- `code-simplicity-reviewer` - YAGNI compliance and complexity reduction
- `repo-research-analyst` - Pattern compliance and conventions

### `/work` - Plan Execution
Execute work plans efficiently with quality checks built in.

```
/work docs/plans/2026-01-28-feat-auth-plan.md
```

**Features:**
- Breaks plans into actionable tasks
- Incremental commits at logical checkpoints
- Continuous testing during execution
- Optional reviewer agent integration

### `/brainstorm` - Idea Exploration
Explore requirements and approaches through collaborative dialogue before planning.

```
/brainstorm Real-time notifications system
```

**Features:**
- Guided questioning for requirement clarity
- Approach comparison with pros/cons
- YAGNI-focused recommendations
- Documents decisions for `/plan` to consume

## Skills

### `file-todos`
File-based todo tracking system for managing code review findings, technical debt, and work items.

**Location:** `.opencode/skill/file-todos/`

**Key features:**
- YAML frontmatter for metadata (status, priority, dependencies)
- Structured sections for problem statement, findings, solutions
- Work log for tracking progress
- Integration with `/review` command

### `skill-creator`
Guide for creating new skills that extend agent capabilities.

**Location:** `.opencode/skill/skill-creator/`

### `brainstorming`
Question techniques and approach exploration patterns for effective ideation.

**Location:** `.opencode/skill/brainstorming/`

## Agents

### Review Agents

Located in `.opencode/agent/review/`:

| Agent | Purpose |
|-------|---------|
| `security-sentinel` | Security audits, vulnerability assessments, OWASP compliance |
| `performance-oracle` | Performance analysis, algorithmic complexity, scalability |
| `architecture-strategist` | Architectural patterns, SOLID principles, system design |
| `code-simplicity-reviewer` | YAGNI enforcement, complexity reduction, simplification |

### Research Agents

Located in `.opencode/agent/research/`:

| Agent | Purpose |
|-------|---------|
| `repo-research-analyst` | Repository structure, conventions, pattern discovery |

## Directory Structure

```
.opencode/
├── command/
│   ├── plan.md          # Feature planning workflow
│   ├── review.md        # Multi-agent code review
│   ├── work.md          # Plan execution workflow
│   └── brainstorm.md    # Idea exploration
├── skill/
│   ├── file-todos/      # Todo tracking system
│   │   ├── SKILL.md
│   │   └── assets/
│   │       └── todo-template.md
│   ├── skill-creator/   # Skill creation guide
│   │   └── SKILL.md
│   └── brainstorming/   # Brainstorming techniques
│       └── SKILL.md
└── agent/
    ├── review/          # Code review specialists
    │   ├── security-sentinel.md
    │   ├── performance-oracle.md
    │   ├── architecture-strategist.md
    │   └── code-simplicity-reviewer.md
    └── research/        # Research specialists
        └── repo-research-analyst.md
```

## Typical Workflow

1. **Brainstorm** (optional): `/brainstorm` to explore requirements
2. **Plan**: `/plan` to create structured implementation plan
3. **Review** (optional): `/review` to get pre-implementation feedback
4. **Work**: `/work` to execute the plan
5. **Review**: `/review` to validate implementation

## Performance Advantage

Running 5 review agents sequentially might take 5 minutes. Running them in parallel on a fast inference platform completes in ~30 seconds - a 10x speedup.

This makes comprehensive multi-agent analysis practical for everyday development workflows.
