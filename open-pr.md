---
description: "Open a pull request with auto-generated title and description"
argument-hint: [base-branch]
allowed-tools:
  [
    "Bash(git push:*)",
    "Bash(gh pr create:*)",
    "Bash(gh pr edit:*)",
    "Bash(gh pr list:*)",
    "Bash(xdg-open:*)",
    "Bash(git rev-parse:*)"
  ]
---

# Claude Command: Open PR

Opens a pull request with auto-generated title and description.

## Usage

```
/open-pr [base-branch]
```

- `base-branch` (optional): The branch to use as the base for the pull request. Defaults to `master` if not provided.

## Process

Always use `gh` or `git` command to interact with github and git.

**Argument handling:**
- Extract the base branch from the arguments (first argument after the command)
- If no base branch is provided, use `master` as the default
- Store this value for use in subsequent steps

**Steps:**

1. Ensure origin branch is up-to-date, push the branch if not the case
2. Analyze diff compared to the base branch (from argument or default to master). It will help to create a title and description.
3. Check if the PR already exists on github
4. Show me the title and description and ask me if I'm ok with them
5. Open (or update if exists) the pull request with title, description, and base branch using `gh pr create --base <base-branch>`
6. Open the link into the default browser

## PR title format

`<emoji> <branch_name>: <title_description>`

**Rules:**

- Imperative mood ("add" not "added")
- <title_description> should be a concise and clear description of the PR's goal
- Title line <82 chars

**Emoji Map**

✨ feat | 🐛 fix | 📝 docs | 💄 style | ♻️ refactor | ⚡ perf | ✅ test | 🔧 chore | 🚀 ci | 🚨 warnings | 🔒️ security | 🧑‍💻 dx | 🩹 minor-fix | 🔥 remove | 🚑️ hotfix | 🚧 wip | 💚 ci-fix | 📌 pin-deps | 👷 ci-build | 📈 analytics | ✏️ typos | ⏪️ revert | 📄 license | 💥 breaking | 🍱 assets | ♿️ accessibility | 💡 comments | 💾 db | 🔊 logs | 🔇 remove-logs | 🙈 gitignore | 📸 snapshots | ⚗️ experiment | 🚩 flags | 💫 animations | ⚰️ dead-code | 🦺 validation

## PR description

Use this template:

```markdown
### Summary

<description>
<bullet_points>

### changes

<explanation_of_changes>
```

- <description>: A description of that the PR brings in the codebase. Compared to the title, the description here is more detailed. Ideally it should take between 1 and 3 lines. If the title is already self-explanatory, you could skip this part.
- <bullet_points>: List of important things done in the PR. Each bullet point should be short and concise. If only 1 point and it's already covered the <description> you can skip this part.
- <explanation_of_changes>: Any useful things for the reviewers. Here is some examples of what can be mentioned, each point should focus on the important things and should not be too long (no more than 10 lines each):
  - How the code is architectured, only inportant choices, no need to detail every added/updated files
  - Details about complex algorithm if any
  - What are the UI/UX changes for the end-users
  - Potential trade-offs

## Open the link in default browser

Use this command: `xdg-open <url>`

## Notes

- **NEVER add Claude signature to commits**
