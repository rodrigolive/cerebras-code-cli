---
description: Transform feature descriptions into well-structured project plans with parallel research
argument-hint: "[feature description, bug report, or improvement idea]"
---

# Create a Plan for a New Feature or Bug Fix

Transform feature descriptions, bug reports, or improvement ideas into well-structured markdown plan files that follow project conventions and best practices.

## Feature Description

<feature_description> #$ARGUMENTS </feature_description>

**If the feature description above is empty, ask the user:** "What would you like to plan? Please describe the feature, bug fix, or improvement you have in mind."

Do not proceed until you have a clear feature description from the user.

## Main Tasks

### 0. Idea Refinement

**Check for brainstorm output first:**

Before asking questions, look for recent brainstorm documents in `docs/brainstorms/` that match this feature:

```bash
ls -la docs/brainstorms/*.md 2>/dev/null | head -10
```

**Relevance criteria:** A brainstorm is relevant if:
- The topic (from filename or YAML frontmatter) semantically matches the feature description
- Created within the last 14 days
- If multiple candidates match, use the most recent one

**If a relevant brainstorm exists:**
1. Read the brainstorm document
2. Announce: "Found brainstorm from [date]: [topic]. Using as context for planning."
3. Extract key decisions, chosen approach, and open questions
4. **Skip the idea refinement questions below** - the brainstorm already answered WHAT to build
5. Use brainstorm decisions as input to the research phase

**If no brainstorm found, run idea refinement:**

Refine the idea through collaborative dialogue using the **AskUserQuestion tool**:

- Ask questions one at a time to understand the idea fully
- Prefer multiple choice questions when natural options exist
- Focus on understanding: purpose, constraints and success criteria
- Continue until the idea is clear OR user says "proceed"

**Gather signals for research decision.** During refinement, note:

- **User's familiarity**: Do they know the codebase patterns? Are they pointing to examples?
- **User's intent**: Speed vs thoroughness? Exploration vs execution?
- **Topic risk**: Security, payments, external APIs warrant more caution
- **Uncertainty level**: Is the approach clear or open-ended?

### 1. Local Research (Always Runs - Parallel)

Run these agents **in parallel** to gather local context:

- Task repo-research-analyst(feature_description)

**What to look for:**
- **Repo research:** existing patterns, AGENTS.md guidance, technology familiarity, pattern consistency

### 1.5. Research Decision

Based on signals from Step 0 and findings from Step 1, decide on external research.

**High-risk topics - always research.** Security, payments, external APIs, data privacy. The cost of missing something is too high.

**Strong local context - skip external research.** Codebase has good patterns, AGENTS.md has guidance, user knows what they want.

**Uncertainty or unfamiliar territory - research.** User is exploring, codebase has no examples, new technology.

**Announce the decision and proceed.** Brief explanation, then continue.

### 1.5b. External Research (Conditional)

**Only run if Step 1.5 indicates external research is valuable.**

Use web search tools to research best practices and framework documentation relevant to the feature.

### 1.6. Consolidate Research

After all research steps complete, consolidate findings:

- Document relevant file paths from repo research (e.g., `src/services/example.ts:42`)
- Note external documentation URLs and best practices (if external research was done)
- List related issues or PRs discovered
- Capture AGENTS.md conventions

### 2. Issue Planning & Structure

**Title & Categorization:**

- [ ] Draft clear, searchable issue title using conventional format (e.g., `feat: Add user authentication`, `fix: Cart total calculation`)
- [ ] Determine issue type: enhancement, bug, refactor
- [ ] Convert title to filename: add today's date prefix, strip prefix colon, kebab-case, add `-plan` suffix
  - Example: `feat: Add User Authentication` -> `2026-01-28-feat-add-user-authentication-plan.md`

**Stakeholder Analysis:**

- [ ] Identify who will be affected by this issue (end users, developers, operations)
- [ ] Consider implementation complexity and required expertise

**Content Planning:**

- [ ] Choose appropriate detail level based on issue complexity and audience
- [ ] List all necessary sections for the chosen template
- [ ] Gather supporting materials (error logs, screenshots, design mockups)

### 3. Choose Implementation Detail Level

Select how comprehensive you want the plan to be:

#### MINIMAL (Quick Issue)

**Best for:** Simple bugs, small improvements, clear features

**Includes:**
- Problem statement or feature description
- Basic acceptance criteria
- Essential context only

#### MORE (Standard Issue)

**Best for:** Most features, complex bugs, team collaboration

**Includes everything from MINIMAL plus:**
- Detailed background and motivation
- Technical considerations
- Success metrics
- Dependencies and risks
- Basic implementation suggestions

#### A LOT (Comprehensive Issue)

**Best for:** Major features, architectural changes, complex integrations

**Includes everything from MORE plus:**
- Detailed implementation plan with phases
- Alternative approaches considered
- Extensive technical specifications
- Risk mitigation strategies

### 4. Plan Creation & Formatting

**Content Formatting:**

- [ ] Use clear, descriptive headings with proper hierarchy (##, ###)
- [ ] Include code examples in triple backticks with language syntax highlighting
- [ ] Use task lists (- [ ]) for trackable items that can be checked off
- [ ] Add collapsible sections for lengthy logs using `<details>` tags

**Cross-Referencing:**

- [ ] Link to related issues/PRs using #number format
- [ ] Reference specific code using file:line format
- [ ] Add links to external resources with descriptive text

### 5. Final Review & Output

**Pre-submission Checklist:**

- [ ] Title is searchable and descriptive
- [ ] All template sections are complete
- [ ] Links and references are working
- [ ] Acceptance criteria are measurable

**Filename:**

```
docs/plans/YYYY-MM-DD-<type>-<descriptive-name>-plan.md
```

## Post-Generation Options

After writing the plan file, present these options:

**Question:** "Plan ready at `docs/plans/YYYY-MM-DD-<type>-<name>-plan.md`. What would you like to do next?"

**Options:**
1. **Open plan in editor** - Open the plan file for review
2. **Run `/review`** - Get feedback from multiple reviewer agents in parallel
3. **Start `/work`** - Begin implementing this plan
4. **Create Issue** - Create issue in project tracker (GitHub)
5. **Simplify** - Reduce detail level

NEVER CODE! Just research and write the plan.
