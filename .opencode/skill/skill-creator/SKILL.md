---
name: skill-creator
description: This skill should be used when users want to create a new skill (or update an existing skill) that extends the agent's capabilities with specialized knowledge, workflows, or tool integrations.
---

# Skill Creator

This skill provides guidance for creating effective skills.

## About Skills

Skills are modular, self-contained packages that extend the agent's capabilities by providing specialized knowledge, workflows, and tools. Think of them as "onboarding guides" for specific domains or tasks - they transform the agent from a general-purpose assistant into a specialized agent equipped with procedural knowledge.

### What Skills Provide

1. Specialized workflows - Multi-step procedures for specific domains
2. Tool integrations - Instructions for working with specific file formats or APIs
3. Domain expertise - Company-specific knowledge, schemas, business logic
4. Bundled resources - Scripts, references, and assets for complex and repetitive tasks

### Anatomy of a Skill

Every skill consists of a required SKILL.md file and optional bundled resources:

```
skill-name/
|-- SKILL.md (required)
|   |-- YAML frontmatter metadata (required)
|   |   |-- name: (required)
|   |   |-- description: (required)
|   |-- Markdown instructions (required)
|-- Bundled Resources (optional)
    |-- scripts/          - Executable code (Python/Bash/etc.)
    |-- references/       - Documentation intended to be loaded into context as needed
    |-- assets/           - Files used in output (templates, icons, fonts, etc.)
```

#### SKILL.md (required)

**Metadata Quality:** The `name` and `description` in YAML frontmatter determine when the agent will use the skill. Be specific about what the skill does and when to use it. Use the third-person (e.g. "This skill should be used when..." instead of "Use this skill when...").

#### Bundled Resources (optional)

##### Scripts (`scripts/`)

Executable code (Python/Bash/etc.) for tasks that require deterministic reliability or are repeatedly rewritten.

- **When to include**: When the same code is being rewritten repeatedly or deterministic reliability is needed
- **Example**: `scripts/process_data.py` for data transformation tasks
- **Benefits**: Token efficient, deterministic, may be executed without loading into context

##### References (`references/`)

Documentation and reference material intended to be loaded as needed into context to inform the agent's process and thinking.

- **When to include**: For documentation that the agent should reference while working
- **Examples**: `references/api_docs.md` for API specifications, `references/schema.md` for database schemas
- **Benefits**: Keeps SKILL.md lean, loaded only when needed
- **Best practice**: If files are large (>10k words), include grep search patterns in SKILL.md

##### Assets (`assets/`)

Files not intended to be loaded into context, but rather used within the output the agent produces.

- **When to include**: When the skill needs files that will be used in the final output
- **Examples**: `assets/template.md` for document templates, `assets/boilerplate/` for project scaffolding
- **Benefits**: Separates output resources from documentation

### Progressive Disclosure Design Principle

Skills use a three-level loading system to manage context efficiently:

1. **Metadata (name + description)** - Always in context (~100 words)
2. **SKILL.md body** - When skill triggers (<5k words)
3. **Bundled resources** - As needed (Unlimited*)

*Unlimited because scripts can be executed without reading into context window.

## Skill Creation Process

To create a skill, follow the "Skill Creation Process" in order, skipping steps only if there is a clear reason why they are not applicable.

### Step 1: Understanding the Skill with Concrete Examples

Skip this step only when the skill's usage patterns are already clearly understood.

To create an effective skill, clearly understand concrete examples of how the skill will be used. This understanding can come from either direct user examples or generated examples that are validated with user feedback.

For example, when building an image-editor skill, relevant questions include:

- "What functionality should the image-editor skill support? Editing, rotating, anything else?"
- "Can you give some examples of how this skill would be used?"
- "What would a user say that should trigger this skill?"

Conclude this step when there is a clear sense of the functionality the skill should support.

### Step 2: Planning the Reusable Skill Contents

To turn concrete examples into an effective skill, analyze each example by:

1. Considering how to execute on the example from scratch
2. Identifying what scripts, references, and assets would be helpful when executing these workflows repeatedly

Example: When building a `pdf-editor` skill to handle queries like "Help me rotate this PDF," the analysis shows:

1. Rotating a PDF requires re-writing the same code each time
2. A `scripts/rotate_pdf.py` script would be helpful to store in the skill

Example: When building a `data-pipeline` skill for queries like "Process this CSV data" the analysis shows:

1. Processing data requires the same transformation steps each time
2. A `references/schema.md` file documenting the expected data format would be helpful

### Step 3: Initializing the Skill

Create the skill directory structure:

```bash
mkdir -p .opencode/skill/skill-name/{scripts,references,assets}
```

Create the SKILL.md file with proper frontmatter:

```markdown
---
name: skill-name
description: This skill should be used when [describe trigger conditions]
---

# Skill Title

[Instructions and workflows]
```

### Step 4: Edit the Skill

When editing the skill, remember that the skill is being created for the agent to use. Focus on including information that would be beneficial and non-obvious. Consider what procedural knowledge, domain-specific details, or reusable assets would help execute tasks more effectively.

#### Start with Reusable Skill Contents

Begin implementation with the reusable resources identified: `scripts/`, `references/`, and `assets/` files. Note that this step may require user input for domain-specific content.

#### Update SKILL.md

**Writing Style:** Write the entire skill using **imperative/infinitive form** (verb-first instructions), not second person. Use objective, instructional language (e.g., "To accomplish X, do Y" rather than "You should do X").

To complete SKILL.md, answer the following questions:

1. What is the purpose of the skill, in a few sentences?
2. When should the skill be used?
3. In practice, how should the agent use the skill? All reusable skill contents developed above should be referenced so the agent knows how to use them.

### Step 5: Test the Skill

Test the skill by:

1. Loading it and triggering with example queries
2. Verifying all workflows execute correctly
3. Checking that references and assets are properly linked
4. Validating the skill description triggers appropriately

### Step 6: Iterate

After testing the skill, users may request improvements.

**Iteration workflow:**
1. Use the skill on real tasks
2. Notice struggles or inefficiencies
3. Identify how SKILL.md or bundled resources should be updated
4. Implement changes and test again

## Validation Checklist

Before finalizing a skill:

- [ ] YAML frontmatter has `name` and `description`
- [ ] Description uses third-person ("This skill should be used when...")
- [ ] All files in `references/` are linked from SKILL.md
- [ ] All files in `assets/` are linked from SKILL.md
- [ ] Instructions use imperative form, not second person
- [ ] SKILL.md is under 5000 words
- [ ] Large reference files have grep patterns documented
