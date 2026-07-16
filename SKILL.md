---
name: opencode-zen-delegator
description: "Automatic task delegation to Opencode Zen models when Manus limits are reached. Use when: approaching token limits, daily rate limits or when explicitly requested to offload work to 'big-pickle'."
---

# Opencode Zen Delegator

This skill enables Manus AI to seamlessly hand off tasks to the `big-pickle` model (Big Pickle) via the Opencode Zen API.

## When to Trigger

1.  **Approaching Limits:** Use when you receive a system warning about token or daily request limits.
2.  **Explicit Request:** Use when the user asks to "delegate to big-pickle" or "let the Opencode Zen agent finish this."
3.  **Complex Coding Tasks:** Use when a task requires extensive reasoning that might be better handled by a specialized coding model.

## Workflow

### 1. Save Current State
Before delegating, save the current session context and backup task progress status.
- Use `delegate_manager.py` to save the state to `task_context.json`.
- Summarize the "Current Objective" and "Completed Steps" in the context.

### 2. Prepare the Delegation Brief
Create a concise prompt for `big-pickle` that includes:
- The overall goal.
- The specific next step.
- Any critical constraints or file paths.

### 3. Execute Handoff
Run the delegation agent:
```bash
python3 big_pickle_agent.py "YOUR_PROMPT" task_context.json
```

## Bundled Resources

- **`big_pickle_agent.py`**: The primary interface for calling the Opencode Zen API.
- **`delegate_manager.py`**: Utility to save and load task context for seamless transitions.

## Notes
- The API key must be added to the script.
- The `big-pickle` model is a reasoning-heavy model; expect it to provide a `reasoning_content` block before its final answer.
