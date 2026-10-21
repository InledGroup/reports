# Reports

A tiny repo for reporting **bugs**, **ideas** and **tasks**.

Open a new issue, pick a template, write a title and a body — that's it.
Everything else is automated:

1. **Discord notification** — when an issue is opened, a message is posted to
   Discord using the organization secret `DISCORD_WEBHOOK`.
2. **Project board** — the issue is automatically added to
   [Inled Issues and Errors](https://github.com/orgs/InledGroup/projects/1/views/1)
   and classified in the **Tipo** field based on its label:

   | Label      | Tipo    |
   | ---------- | ------- |
   | `bug`      | Error   |
   | `idea`     | Idea    |
   | `task`     | Ayuda   |

## Usage

1. Go to **Issues → New issue**.
2. Choose a template: 🐛 Bug Report, 💡 Idea or ✅ Task.
3. Fill in the title and body, and submit.

The issue gets the right label automatically, so it shows up classified on the
project board and the Discord notification shows the correct icon.

## Required secrets

| Secret          | Where        | Used by             | Notes                                                        |
| --------------- | ------------ | ------------------- | ------------------------------------------------------------ |
| `DISCORD_WEBHOOK` | Organization | `notify-discord.yml` | Must be available to this repo (set at org level or added as a repo secret). |
| `PROJECT_PAT`     | Repository   | `add-to-project.yml` | A PAT with `project` scope (and `repo` scope for private repos). `GITHUB_TOKEN` cannot add items to an org project. |

To set `PROJECT_PAT` on this repo:

```bash
gh secret set PROJECT_PAT --repo InledGroup/reports
# then paste a fine-grained/classic PAT with project access
```

## Notes

- Labels `bug`, `idea` and `task` must exist on the repo; they are created
  automatically on setup (see below) or can be created manually:

  ```bash
  gh label create bug --repo InledGroup/reports --color d73a49 --description "Something is broken"
  gh label create idea --repo InledGroup/reports --color 0e8a16 --description "New idea or enhancement"
  gh label create task --repo InledGroup/reports --color 1d76db --description "To-do or maintenance task"
  ```
