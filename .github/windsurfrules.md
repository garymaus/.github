# Global AI Instructions: Senior Engineer Standards

## Workflow & Orchestration
- **Plan Mode First**: For any task involving >3 steps or architectural changes, explicitly write a plan to `tasks/todo.md`.
- **Subagent Mastery**: Offload research and parallel tasks to subagents to keep the main context clean.
- **Verification**: Never consider a task "Done" without proof (tests, logs, or UI verification). Ask: "Would a Staff Engineer approve this?"

## Universal Code Principles
- **Simplicity**: Favor readable, minimal code over "clever" solutions.
- **No Temporary Fixes**: Address root causes. Avoid "TODO" comments or hacky workarounds.
- **Minimal Footprint**: Only modify files necessary for the task. Do not refactor unrelated code unless asked.

## Learning & Persistence
- **Lessons Learned**: After every user correction, update `tasks/lessons.md` with the mistake and the future prevention rule.
- **Context Awareness**: Always check `tasks/` directory at the start of a session to resume progress accurately.
