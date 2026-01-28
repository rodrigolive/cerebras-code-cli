---
description: Perform comprehensive code reviews using multi-agent parallel analysis
argument-hint: "[PR number, GitHub URL, branch name, or latest]"
---

# Review Command

Perform exhaustive code reviews using multi-agent analysis for deep inspection.

## Introduction

This command runs multiple specialized reviewer agents in parallel to analyze code changes from different perspectives: security, performance, architecture, simplicity, and more.

**Key advantage:** Running all reviewers in parallel dramatically reduces total review time.

## Prerequisites

- Git repository with GitHub CLI (`gh`) installed and authenticated
- Clean main/master branch
- Proper permissions to access the repository

## Main Tasks

### 1. Determine Review Target & Setup

<review_target> #$ARGUMENTS </review_target>

#### Immediate Actions:

- [ ] Determine review type: PR number (numeric), GitHub URL, or branch name
- [ ] Check current git branch
- [ ] If ALREADY on the target branch -> proceed with analysis
- [ ] If DIFFERENT branch -> checkout the target branch
- [ ] Fetch PR metadata using `gh pr view --json` for title, body, files, linked issues
- [ ] Set up analysis environment

### 2. Parallel Agent Review

Run ALL or most of these agents **at the same time** for maximum speed:

```
Task security-sentinel(PR content)
Task performance-oracle(PR content)
Task architecture-strategist(PR content)
Task code-simplicity-reviewer(PR content)
Task repo-research-analyst(PR content for pattern compliance)
```

**Optional Language-Specific Reviewers:**
- Task typescript-reviewer(PR content) - For TypeScript projects
- Task python-reviewer(PR content) - For Python projects
- Task go-reviewer(PR content) - For Go projects

### 3. Ultra-Thinking Deep Dive

For each phase below, spend maximum cognitive effort analyzing the changes:

#### Phase 1: Stakeholder Perspective Analysis

**Developer Perspective:**
- How easy is this to understand and modify?
- Are the APIs intuitive?
- Is debugging straightforward?
- Can I test this easily?

**Operations Perspective:**
- How do I deploy this safely?
- What metrics and logs are available?
- How do I troubleshoot issues?

**End User Perspective:**
- Is the feature intuitive?
- Are error messages helpful?
- Is performance acceptable?

**Security Perspective:**
- What's the attack surface?
- Are there compliance requirements?
- How is data protected?

#### Phase 2: Scenario Exploration

- [ ] **Happy Path**: Normal operation with valid inputs
- [ ] **Invalid Inputs**: Null, empty, malformed data
- [ ] **Boundary Conditions**: Min/max values, empty collections
- [ ] **Concurrent Access**: Race conditions, deadlocks
- [ ] **Scale Testing**: 10x, 100x, 1000x normal load
- [ ] **Network Issues**: Timeouts, partial failures
- [ ] **Security Attacks**: Injection, overflow, DoS

### 4. Simplification Review

Run the code-simplicity-reviewer to identify unnecessary complexity:

```
Task code-simplicity-reviewer("Final simplification pass on changes")
```

### 5. Findings Synthesis and Todo Creation

#### Step 1: Synthesize All Findings

- [ ] Collect findings from all parallel agents
- [ ] Categorize by type: security, performance, architecture, quality
- [ ] Assign severity levels: P1 (critical), P2 (important), P3 (nice-to-have)
- [ ] Remove duplicate or overlapping findings
- [ ] Estimate effort for each finding (Small/Medium/Large)

#### Step 2: Create Todo Files

For each finding, create a todo file in `todos/` directory:

**File naming convention:**
```
{issue_id}-{status}-{priority}-{description}.md

Examples:
- 001-pending-p1-security-vulnerability.md
- 002-pending-p2-performance-optimization.md
- 003-pending-p3-code-cleanup.md
```

**Status values:**
- `pending` - New findings, needs triage/decision
- `ready` - Approved, ready to work
- `complete` - Work finished

**Priority values:**
- `p1` - Critical (blocks merge, security/data issues)
- `p2` - Important (should fix, architectural/performance)
- `p3` - Nice-to-have (enhancements, cleanup)

#### Step 3: Summary Report

After creating all todo files, present:

```markdown
## Code Review Complete

**Review Target:** PR #XXXX - [PR Title]
**Branch:** [branch-name]

### Findings Summary:
- **Total Findings:** [X]
- **P1 (CRITICAL):** [count] - BLOCKS MERGE
- **P2 (IMPORTANT):** [count] - Should Fix
- **P3 (NICE-TO-HAVE):** [count] - Enhancements

### Created Todo Files:

**P1 - Critical (BLOCKS MERGE):**
- `001-pending-p1-{finding}.md` - {description}

**P2 - Important:**
- `002-pending-p2-{finding}.md` - {description}

**P3 - Nice-to-Have:**
- `003-pending-p3-{finding}.md` - {description}

### Review Agents Used:
- security-sentinel
- performance-oracle
- architecture-strategist
- code-simplicity-reviewer

### Next Steps:

1. **Address P1 Findings**: CRITICAL - must be fixed before merge
2. **Triage All Todos**: `ls todos/*-pending-*.md`
3. **Work on Approved Todos**: `/work` command
```

### Important: P1 Findings Block Merge

Any **P1 (CRITICAL)** findings must be addressed before merging the PR. Present these prominently and ensure they're resolved.
