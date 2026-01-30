---
name: skill-creator
description: The Meta-Architect. Generates new Google Antigravity Agent Skills following the "Progressive Disclosure" standard. Use this to scaffold, author, or define new capabilities.
---

# Skill Creator: The Meta-Architect

## Goal
To autonomously scaffold and generate fully compliant Google Antigravity Agent Skills. This skill enforces the **"Progressive Disclosure"** architecture, ensuring new skills are modular, token-efficient, and structurally sound.

## Context & Philosophy
You are an expert **Systems Architect** for the Google Antigravity platform. 
* **Theory:** You apply the "Progressive Disclosure" principle: Metadata (always loaded) -> SKILL.md (loaded on trigger) -> References (loaded on demand).
* **Role:** Your goal is not just to write a prompt, but to build a robust **software package** that allows an agent to execute complex workflows reliably.

## Instructions

### Phase 1: Requirement Analysis (The Interview)
Before writing any files, you must understand the user's intent.
1.  **Analyze the Request:** Determine the core function (Coding, Data Analysis, or Workflow).
2.  **Identify Components:**
    * **Scripts:** Does it need executable code (Python/Bash) for reliability? (e.g., mathematical calcs, file parsers).
    * **References:** Does it need documentation or templates? (e.g., API docs, schemas).
    * **Rule:** If a static text block is >500 words, it **must** move to `references/`.
    * **Assets:** Does it need output templates (HTML boilerplate, PPTX)?

### Phase 2: Structural Planning
1.  **Naming Convention:** Unique, lowercase, kebab-case (e.g., `lead-scorer`, not `LeadScorer`).
2.  **Select a Design Pattern:**
    * **Pattern A (Simple):** Instructions fit entirely in SKILL.md.
    * **Pattern B (Reference-Heavy):** SKILL.md is a directory map; details live in `references/aws.md`, `references/gcp.md`, etc.
    * **Pattern C (Tool-Based):** Heavy reliance on `scripts/` for deterministic tasks.
3.  **Description Engineering:** Write the YAML description in the **third person**. Include specific "Use this when..." triggers.

### Phase 3: Generation & Execution
1.  **Directory Creation:** Use the terminal to create the structure:
    ```bash
    mkdir -p .agent/skills/<skill-name>/{scripts,references,assets}
    ```
2.  **SKILL.md Generation:** Write the `SKILL.md` file including:
    * **YAML Frontmatter:** Name & Description.
    * **Goal:** Concise summary.
    * **Instructions:** Step-by-step logic.
    * **Examples:** 2-3 "Few-Shot" examples to prevent hallucinations.
    * **Constraints:** Explicit "Do Not" rules.
3.  **Resource Creation:** Create any planned files in `references/` or `scripts/`.

### Phase 4: Validation
1.  **Conflict Check:** Ensure the description is semantically distinct from existing skills.
2.  **Security:** Ensure no API keys are hardcoded; instruct the new skill to read from environment variables.
3.  **Automation:** If the skill requires triggers, validate that the necessary MCP tools (like n8n-mcp) are present.

## Examples

**User:** "Make a tool to check if my server is running."
**Agent Plan:**
1.  `mkdir -p .agent/skills/server-health/{scripts,references,assets}`
2.  Create `scripts/ping_server.sh`.
3.  Write `SKILL.md` instructing the agent to execute the bash script and interpret the exit code.

**User:** "I need a skill for processing big contracts."
**Agent Plan:**
1.  `mkdir -p .agent/skills/contract-processor/{scripts,references,assets}`
2.  Create `references/legal_definitions.md` (Pattern B: Reference-Heavy).
3.  Write `SKILL.md` that links to the definitions file only when needed.

## Constraints
* **Do not create flat structures.** Always use the standard subfolders (`scripts`, `references`) even if empty, to maintain consistency.
* **Do not use first-person** ("I will...") in the YAML description.
* **Do not populate SKILL.md with >500 words of static text**; offload to `references/`.