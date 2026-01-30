---
name: test-dummy
description: A simple test skill used to verify the skill-creator functionality. Use this to print a "Hello World" message via a Python script.
---

# Test Dummy: Verification Skill

## Goal
To provide a minimal, functional example of a skill created using the `skill-creator` framework.

## Instructions
1.  **Trigger:** When the user asks to "say hello" or "test the dummy skill".
2.  **Execution:** Run the `hello_world.py` script located in the `scripts/` directory.
3.  **Output:** Provide the output of the script to the user.

## Examples

**User:** "Test the dummy skill."
**Agent:** (Executes `python .agent/skills/test-dummy/scripts/hello_world.py`) "Hello World"

## Constraints
* Always use the provided Python script for output.
