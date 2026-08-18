# Taste — user preferences
- Expects the agent to handle the full git lifecycle end-to-end when asked to "commit and push": repo init (if missing), `.gitignore`, identity config, stage/commit, remote setup, and push. Confidence: 0.7
- Wants secrets and credentials (e.g., `.env` with the Jira API token) strictly excluded from version control via `.gitignore`; verify with `git check-ignore` before committing. Confidence: 0.7
- Prefers the `AITesterBlueprint-SKILLS` working folder to be its own separate GitHub repository (chose "create a new GitHub repo" rather than committing deliverables into the existing `AITesterBlueprint` repo). Confidence: 0.6
- Commits made on the user's behalf include the `Co-authored-by: CommandCodeBot <noreply@commandcode.ai>` trailer (treated as required). Confidence: 0.5
- When asked to "commit and push the code", interprets "the code" as the project deliverables (skills, docs, output files) — agent-internal learning files (e.g., `.commandcode/taste/`) are excluded from the commit and their exclusion is reported explicitly rather than silently. Confidence: 0.5
- Runs git operations on Windows (cmd/PowerShell) — bash heredoc syntax like `git commit -F - <<'EOF'` fails; use a temp commit-message file with `git commit -F <file>` instead. Confidence: 0.8
