# Contributing to Naevls Studios

This guide applies to **every repository** in the Naevls Studios organization unless a repo has its own `CONTRIBUTING.md`. If you're new, read it once end to end. It takes about 5 minutes.

---

## TL;DR

1. Every change starts from an **issue**.
2. Branch off the default branch: `feat/42-google-sign-in`.
3. Open a **pull request** using the template, linking the issue (`Closes #42`).
4. Get **1 approval from a code owner**, resolve every review thread.
5. **Squash-merge**. The PR title becomes the commit message, so make it a Conventional Commit.

Nobody, including founders, pushes directly to `main`. The ruleset blocks it.

---

## 1. Issues

- Use a template: **Bug report**, **Feature request**, or **Task / chore**. Blank issues are disabled.
- Search before opening, to avoid duplicates.
- Questions and "is this a bug?" go to **Discord** first, not issues.
- **Security problems or leaked secrets: never open a public issue.** Use the private security report link in the "New issue" menu, and ping the CTO on Discord directly.

### Labels

| Label | Meaning |
| --- | --- |
| `needs-triage` | New and not yet reviewed by the repo lead |
| `bug` | Something is broken |
| `enhancement` | New feature or improvement |
| `chore` | Internal work with no user-facing change |
| `blocked` | Waiting on someone or something else |
| `good first issue` | Small and well-defined, good for onboarding |

The **repo lead** triages new issues at least weekly: they set the priority, assign someone, and remove `needs-triage`.

---

## 2. Branches

Always branch from the repo's **default branch** (`main`) and keep branches short-lived (days, not weeks).

```
<type>/<issue-number>-<short-description>
```

| Type | Use for |
| --- | --- |
| `feat/` | New feature |
| `fix/` | Bug fix |
| `refactor/` | Code change with no behaviour change |
| `chore/` | Tooling, deps, CI, config |
| `docs/` | Documentation only |
| `hotfix/` | Urgent production fix |

Examples: `feat/42-google-sign-in`, `fix/108-negative-balance-crash`, `chore/15-setup-ci`.

Keep your branch current by rebasing onto main (or merging main in) before you ask for review:

```bash
git fetch origin
git rebase origin/main
git push --force-with-lease   # only ever force-push your OWN feature branch
```

---

## 3. Commits

We use **[Conventional Commits](https://www.conventionalcommits.org/)**:

```
<type>(<optional scope>): <short summary in imperative mood>
```

```
feat(market): add PSE stock search
fix(auth): handle expired refresh token
chore(deps): bump firebase to 11.2
refactor(lessons): extract offline cache service
```

- Write the summary in the imperative ("add", not "added"), lowercase, no period, under ~72 characters.
- Add `!` for breaking changes: `feat(api)!: rename /users to /accounts`.
- Inside your branch, commit as often as you like. History is squashed on merge, so **the PR title is what counts**.

---

## 4. Pull requests

- Fill in the **PR template** completely. Delete sections that don't apply instead of leaving them empty.
- **Link the issue** with `Closes #123`.
- **Keep PRs small.** Aim for under ~400 changed lines. Big PRs get slow, shallow reviews.
- **UI changes need screenshots or a screen recording.**
- Open a **Draft PR** early if you want feedback before it's done.
- The PR title must be a Conventional Commit, because it becomes the squash-commit message on `main`.

### Merge rules (enforced by the org ruleset)

| Rule | What it means for you |
| --- | --- |
| PR required | No direct pushes to `main` |
| 1 approval | At least one reviewer must approve |
| Code owner approval | The approver must be a **code owner** of the files you changed (see below) |
| Stale approvals dismissed | Pushing new commits after approval resets the approval |
| All conversations resolved | Every review thread must be resolved before merging |
| Squash merge only | One clean commit per PR on `main` |
| No force-push / deletion | `main` can't be rewritten or deleted |

Release tags (`v*`) are also protected: they can't be moved or deleted once pushed.

### After merge

- Delete your branch (GitHub can do this automatically).
- Check that the linked issue closed.

---

## 5. Code review

**For authors**
- Review your own diff first. Catch the debug logs and commented-out code yourself.
- Reply to every comment, either with a fix or with your reasoning. The **reviewer** resolves the thread once satisfied.
- Don't take it personally. We review the code, not the person.

**For reviewers**
- Respond within **1 working day**. If you can't, say so on Discord so the author can ask someone else.
- Prefix optional comments with `nit:` so the author knows they're non-blocking.
- Approve when it's **good enough and safe to ship**, not when it's how you'd have written it.
- Check: does it do what the issue asks? Is it tested? Could it leak data, crash, or break another platform?

---

## 6. Code owners

Each repo has a `.github/CODEOWNERS` file that sets who must approve changes:

| Path | Owners |
| --- | --- |
| Everything (`*`) | The repo's **app lead** and the **CTO**. Either one can approve. |
| `/.github/` (CI, templates, CODEOWNERS) | CTO and app lead |
| `LICENSE`, privacy policy, terms of service | Legal/registration owner and CTO |

You can't approve your own PR, which is why every path has at least two owners. If you're the lead, the CTO (or the backup reviewer) approves your PRs, and vice versa.

---

## 7. Secrets & sensitive data

- **Never commit** API keys, `.env` files, keystores (`.jks`, `.keystore`), signing certificates, or service-account JSON.
- Commit an `.env.example` with placeholder values instead.
- Keep real secrets in GitHub **Actions secrets** or your platform's secret manager.
- If you commit a secret by accident: **tell the CTO immediately and rotate the key.** Deleting the commit is not enough, because it's already in the history and in clones.
- Don't put real user data in issues, PRs, screenshots, or test fixtures. Use fake data.

---

## 8. Definition of done

A change is done when:

- [ ] It does what the issue's acceptance criteria say
- [ ] It's tested (automated where practical, manually on a real device or emulator for UI)
- [ ] CI is green
- [ ] It's reviewed and approved by a code owner
- [ ] Docs, README, and `.env.example` are updated if setup or behaviour changed
- [ ] It's merged and the issue is closed

---

## Questions?

Ask in the team **Discord**. If something in this guide is wrong or outdated, open a PR against the org's [`.github`](https://github.com/Naevls-Studios/.github) repository. The same review rules apply.
