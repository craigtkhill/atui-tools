---
name: install-dependencies
description: Guidelines for adding dependencies to projects - critical rule to never specify version numbers, let package managers handle versioning automatically
---

# Install Dependencies

## Overview

Guidelines for adding and managing dependencies across all projects in the workspace.

## Critical Rule: Never Specify Version Numbers

**ALWAYS** let package managers handle versioning automatically.

### ❌ WRONG - Do NOT specify versions:
```toml
# Python (pyproject.toml)
dependencies = [
    "datamodel-code-generator>=0.25.0",  # ❌ NO!
    "pydantic>=2.0",                      # ❌ NO!
]
```

```json
// JavaScript (package.json)
{
  "dependencies": {
    "react": "^18.0.0",  // ❌ NO!
    "axios": "~1.6.0"    // ❌ NO!
  }
}
```

```toml
# Rust (Cargo.toml)
[dependencies]
serde = "1.0"  # ❌ NO!
```

### ✅ CORRECT - Omit versions entirely:
```toml
# Python (pyproject.toml)
dependencies = [
    "datamodel-code-generator",  # ✅ YES!
    "pydantic",                  # ✅ YES!
]
```

```json
// JavaScript (package.json)
{
  "dependencies": {
    "react": "*",     // ✅ YES!
    "axios": "latest" // ✅ YES!
  }
}
```

```toml
# Rust (Cargo.toml)
[dependencies]
serde = "*"  # ✅ YES!
```

## Why This Rule Exists

1. **uv/npm/cargo are smarter**: Package managers resolve compatible versions automatically
2. **Avoid version conflicts**: Manual versions often create dependency hell
3. **Get latest features**: Always use the newest compatible versions
4. **Simpler maintenance**: No need to manually track and update versions

## When Adding Dependencies

1. Add dependency name only (no version)
2. Let the package manager resolve the version
3. Run the appropriate install command:
   - Python: `uv sync`
   - JavaScript: `npm install`
   - Rust: `cargo build`

## Exception

The ONLY time to specify a version is when there's a **known breaking change** or **compatibility issue** that requires pinning to a specific version. This should be:
- Documented with a comment explaining why
- Reviewed in PR/code review
- Treated as temporary until the issue is resolved
