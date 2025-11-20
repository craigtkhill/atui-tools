---
name: create-skill
description: Guide for creating new skills - includes required file structure, YAML frontmatter format, naming conventions, and best practices for skill development
---

# Creating Agent Skills

## Overview

Skills in for Agents provide reusable workflows and guidelines. This skill documents how to properly create new skills.

## Required File Structure

These skills are designed to be Agentic Terminal User Interface (ATUI) agnostic. They live in the dotfolders for the agentic application
examples include.
```
.claude/
.codex/
.gemini/
.opencode/
```

Henceforth, we will use .atui/ as shorthand

Every skill must have:
```
.atui/skills/skill-name/
├── SKILL.md (REQUIRED - main skill file with frontmatter)
├── supporting-file.md (optional)
└── templates/ (optional)
```

## SKILL.md Requirements

### 1. YAML Frontmatter (REQUIRED)

Every SKILL.md **must** start with YAML frontmatter:

```yaml
---
name: skill-name
description: Brief description of what this skill does and when to use it
---
```

**Frontmatter Rules:**
- `name`: Lowercase letters, numbers, hyphens only (max 64 chars)
- `description`: Explain WHAT it does + WHEN to use it (max 1024 chars)
- Critical: ATUIs use description for automatic skill discovery

### 2. Main Content

After frontmatter, elicit the human to add the skill instructions in markdown:


## Skill Naming Conventions

**DO:**
- ✅ Use lowercase letters
- ✅ Use hyphens for word separation
- ✅ Make names descriptive but concise
- ✅ Keep under 64 characters

**DON'T:**
- ❌ Use uppercase letters
- ❌ Use underscores
- ❌ Use spaces
- ❌ Use special characters

**Examples:**
- ✅ `create-skill`
- ✅ `test-driven-development`
- ✅ `write-commit-message`
- ❌ `Create_Skill`
- ❌ `test driven development`

## Description Best Practices

The description is **critical** for skill discovery. Include:

1. **WHAT**: What does the skill do?
2. **WHEN**: When should it be used?
3. **KEY FEATURES**: What are the main capabilities?

## Supporting Files

Skills can include additional files referenced from SKILL.md:

```markdown
For Python testing: See [PYTHON.md](PYTHON.md)
For JavaScript testing: See [JAVASCRIPT.md](JAVASCRIPT.md)
```

**Common Supporting Files:**
- Language-specific guides (`PYTHON.md`, `JAVASCRIPT.md`)
- Templates (`TEMPLATE.md`, `templates/spec-template.md`)
- Examples (`EXAMPLES.md`)
- Scripts (`scripts/helper.py`)

Additionally register skills to the projects AGENTS.md file.

## Creation Checklist

When creating a new skill:

- [ ] Create directory: `.atui/skills/skill-name/`
- [ ] Create `SKILL.md` with YAML frontmatter
- [ ] Add `name` field (lowercase, hyphens, max 64 chars)
- [ ] Add `description` field (WHAT + WHEN, max 1024 chars)
- [ ] Ask human to add more details and and supporting files
- [ ] Reference supporting files with relative paths
- [ ] Test skill discovery with `/help`
- [ ] Regiser skill to AGENTS.md

## Common Mistakes to Avoid

❌ **Forgetting frontmatter** - SKILL.md must start with YAML frontmatter
❌ **Weak descriptions** - Description must explain WHAT and WHEN
❌ **Wrong filename** - Must be `SKILL.md` (uppercase), not `skill.md`
❌ **Bad naming** - Use hyphens, not underscores or spaces
❌ **No examples** - Always include concrete examples
❌ **Too generic** - Be specific about when to use the skill

## Skill Integration

Skills can reference other skills:

```markdown
**Use the `specification` skill for writing specifications.**
**Use the `test-driven-development` skill for writing tests.**
```

This creates workflows that combine multiple skills.

## Testing Your Skill

After creating a skill:

1. Run `/help` to verify it's discovered
2. Check the description appears correctly
3. Test invoking the skill in context
4. Verify supporting files load correctly

## Reference

Official documentation: https://code.claude.com/docs/en/skills.md
