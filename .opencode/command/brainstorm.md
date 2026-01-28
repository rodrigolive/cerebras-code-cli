---
description: Explore requirements and approaches through collaborative dialogue before planning
argument-hint: "[feature idea or problem to explore]"
---

# Brainstorm a Feature or Improvement

Brainstorming helps answer **WHAT** to build through collaborative dialogue. It precedes `/plan`, which answers **HOW** to build it.

**Process knowledge:** Load the `brainstorming` skill for detailed question techniques and approach exploration patterns.

## Feature Description

<feature_description> #$ARGUMENTS </feature_description>

**If the feature description above is empty, ask the user:** "What would you like to explore? Please describe the feature, problem, or improvement you're thinking about."

Do not proceed until you have a feature description from the user.

## Execution Flow

### Phase 0: Assess Requirements Clarity

Evaluate whether brainstorming is needed based on the feature description.

**Clear requirements indicators:**
- Specific acceptance criteria provided
- Referenced existing patterns to follow
- Described exact expected behavior
- Constrained, well-defined scope

**If requirements are already clear:**
Suggest: "Your requirements seem detailed enough to proceed directly to planning. Should I run `/plan` instead, or would you like to explore the idea further?"

### Phase 1: Understand the Idea

#### 1.1 Repository Research (Lightweight)

Run a quick repo scan to understand existing patterns:

- Task repo-research-analyst("Understand existing patterns related to: <feature_description>")

Focus on: similar features, established patterns, AGENTS.md guidance.

#### 1.2 Collaborative Dialogue

Ask questions **one at a time** using multiple choice when natural options exist.

**Guidelines:**
- Start broad (purpose, users) then narrow (constraints, edge cases)
- Validate assumptions explicitly
- Ask about success criteria

**Exit condition:** Continue until the idea is clear OR user says "proceed"

### Phase 2: Explore Approaches

Propose **2-3 concrete approaches** based on research and conversation.

For each approach, provide:
- Brief description (2-3 sentences)
- Pros and cons
- When it's best suited

Lead with your recommendation and explain why. Apply YAGNI - prefer simpler solutions.

Ask which approach the user prefers.

### Phase 3: Capture the Design

Write a brainstorm document to `docs/brainstorms/YYYY-MM-DD-<topic>-brainstorm.md`.

**Document structure:**

```markdown
---
title: [Topic]
date: YYYY-MM-DD
status: draft
---

# [Topic] Brainstorm

## What We're Building

[Clear description of the feature/improvement]

## Why This Approach

[Rationale for the chosen approach]

## Key Decisions

- Decision 1: [What was decided and why]
- Decision 2: [What was decided and why]

## Open Questions

- [ ] Question that still needs answering
- [ ] Another open question

## Next Steps

1. Run `/plan` to create implementation plan
2. Other follow-up actions
```

Ensure `docs/brainstorms/` directory exists before writing.

### Phase 4: Handoff

Present next steps:

**Question:** "Brainstorm captured. What would you like to do next?"

**Options:**
1. **Proceed to planning** - Run `/plan` (will auto-detect this brainstorm)
2. **Refine design further** - Continue exploring
3. **Done for now** - Return later

## Output Summary

When complete, display:

```
Brainstorm complete!

Document: docs/brainstorms/YYYY-MM-DD-<topic>-brainstorm.md

Key decisions:
- [Decision 1]
- [Decision 2]

Next: Run `/plan` when ready to implement.
```

## Important Guidelines

- **Stay focused on WHAT, not HOW** - Implementation details belong in the plan
- **Ask one question at a time** - Don't overwhelm
- **Apply YAGNI** - Prefer simpler approaches
- **Keep outputs concise** - 200-300 words per section max

NEVER CODE! Just explore and document decisions.
