---
description: "Read, fix and reply to a comment on a PR"
allowed-tools:
  [
    "Bash(gh pr comment:*)",
    "Bash(gh pr view:*)",
    "Bash(git add:*)",
    "Bash(git status:*)",
    "Bash(git commit:*)",
    "Bash(git diff:*)",
    "Bash(git log:*)"
  ]
---

# Claude command: Fix PR's comment

The aim of the command is to fix a comment on a PR.
Here is the steps you should do:
- read comment
- prepare a plan to fix it
- fix it (need my approval before)
- commit the changes
- push the change (need my approval before)
- reply to the comment explaining what you did

Below you can find more information about some steps.

## Read comment

Read the comment using the `gh` tool only.

If a link to a comment is given in argument, use this link to read the comment with `gh` tool.
https://github.com/:owner/:repo/pull/:pull_number#discussion_r2439188913

If no link is provided in argument, use `gh` to list the comments of the PR, and ask me which comment to work on.

## Commit the changes

**Commit format:**

```
<branch_name>: <short_description>

<description>
```

**Rules:**

- Short description in imperative mood ("add" not "added")
- First line <72 chars
- Stage your changes
- Create a descriptive commit message
- **NEVER add Claude signature to commits**

## Reply to the comment explaining what you did

Use this command to reply to the comment:
`gh api -X POST repos/:owner/:repo/pulls/:pull_number/comments/:comment_id/replies -F body="Your reply text here"`

Use this on the first line of your reply and add a return line:
`✨ Claude ✨`

Explain what you did in the reply.
