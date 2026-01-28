---
name: brainstorming
description: This skill should be used when exploring ideas, validating approaches, or conducting collaborative ideation sessions before implementation planning. It provides question techniques, approach exploration patterns, and YAGNI principles for effective brainstorming.
---

# Brainstorming Skill

This skill guides effective brainstorming sessions that help answer **WHAT** to build through collaborative dialogue.

## When to Use

- Exploring a vague feature idea
- Validating assumptions before planning
- Comparing multiple approaches
- Understanding user requirements deeply
- Deciding between competing solutions

## Core Principles

### 1. YAGNI (You Aren't Gonna Need It)

- Prefer the simplest solution that meets current requirements
- Avoid building for hypothetical future needs
- Remove features not explicitly required now
- Question every abstraction layer

### 2. Progressive Questioning

Ask questions in order of importance:
1. **Purpose**: What problem does this solve? Who benefits?
2. **Constraints**: What are the hard requirements?
3. **Success criteria**: How do we know it's done?
4. **Edge cases**: What could go wrong?

### 3. One Question at a Time

- Never ask multiple questions in a single message
- Wait for response before asking next question
- Prefer multiple choice when natural options exist

## Question Techniques

### Opening Questions

Start broad to understand context:

- "What problem are you trying to solve?"
- "Who is the primary user of this feature?"
- "What does success look like?"
- "Are there existing solutions you've considered?"

### Clarifying Questions

Dig deeper on ambiguous points:

- "When you say X, do you mean A or B?"
- "Can you give me an example of how this would be used?"
- "What happens if [edge case]?"
- "Is [assumption] correct?"

### Decision Questions

Help narrow down choices:

- "Would you prefer A (faster, less flexible) or B (slower, more flexible)?"
- "Which is more important: [tradeoff 1] or [tradeoff 2]?"
- "Should we optimize for [factor 1] or [factor 2]?"

### Validation Questions

Confirm understanding:

- "So to summarize, we're building [X] that does [Y] for [Z]. Is that right?"
- "Before we proceed, I want to make sure I understand: [summary]. Correct?"

## Approach Exploration

### Presenting Options

When presenting 2-3 approaches:

```markdown
### Option A: [Name]

[2-3 sentence description]

**Pros:**
- Pro 1
- Pro 2

**Cons:**
- Con 1
- Con 2

**Best when:** [conditions where this approach shines]

### Option B: [Name]

[2-3 sentence description]

**Pros:**
- Pro 1
- Pro 2

**Cons:**
- Con 1
- Con 2

**Best when:** [conditions where this approach shines]

---

**Recommendation:** Option [X] because [brief rationale].
```

### Evaluating Approaches

Consider these dimensions:

- **Complexity**: How hard to implement and maintain?
- **Flexibility**: How easily can it adapt to changes?
- **Performance**: What are the resource implications?
- **Risk**: What could go wrong?
- **Time**: How long to implement?

## Document Template

When capturing brainstorm output:

```markdown
---
title: [Topic]
date: YYYY-MM-DD
status: draft
---

# [Topic] Brainstorm

## What We're Building

[Clear, concise description of the feature/improvement - 2-3 paragraphs max]

## Why This Approach

[Rationale for the chosen approach - what was considered and why this won]

## Key Decisions

- **Decision 1**: [What was decided]
  - Why: [Brief rationale]

- **Decision 2**: [What was decided]
  - Why: [Brief rationale]

## Open Questions

Questions that still need answering before implementation:

- [ ] Open question 1
- [ ] Open question 2

## Scope

**In scope:**
- Item 1
- Item 2

**Out of scope:**
- Item 1 (reason)
- Item 2 (reason)

## Next Steps

1. Run `/plan` to create implementation plan
2. [Other follow-up actions]
```

## Anti-Patterns to Avoid

### Don't:
- Ask multiple questions at once
- Jump to implementation details too early
- Ignore user constraints or preferences
- Present more than 3 options (overwhelming)
- Skip validation of understanding
- Build for hypothetical future requirements

### Do:
- Ask one question at a time
- Stay focused on WHAT, not HOW
- Respect stated constraints
- Lead with a recommendation
- Confirm understanding before proceeding
- Apply YAGNI rigorously

## Exit Conditions

Brainstorming is complete when:

- The problem is clearly defined
- Key decisions have been made
- Approach has been selected
- Success criteria are understood
- Open questions are documented
- User says "proceed" or "looks good"

## Output

Brainstorm documents go to:
```
docs/brainstorms/YYYY-MM-DD-<topic>-brainstorm.md
```

The `/plan` command will auto-detect recent brainstorms and use them as input.
