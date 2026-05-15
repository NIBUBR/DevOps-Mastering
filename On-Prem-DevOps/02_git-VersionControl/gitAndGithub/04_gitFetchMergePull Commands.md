# Git Fetch, Merge, and Pull Explained

These three commands are closely related and are fundamental to synchronizing your local repository with a remote repository such as [GitHub](https://github.com?utm_source=chatgpt.com).

---

# 1. `git fetch`

```bash
git fetch origin
```

`git fetch` downloads new commits, branches, and tags from the remote repository, but it does **not** modify your current branch or working files.

### Example

Before fetch:

```text
Local main:   A → B
origin/main:  A → B
Remote main:  A → B → C → D
```

After `git fetch origin`:

```text
Local main:   A → B
origin/main:  A → B → C → D
Remote main:  A → B → C → D
```

Your working branch is unchanged, but Git updates the remote-tracking branch `origin/main`.

### Useful Commands

```bash
git fetch origin
git log --oneline main..origin/main
git diff main origin/main
```

---

# 2. `git merge`

```bash
git merge origin/main
```

`git merge` combines changes from another branch into your current branch.

### Example

After fetching, if you are on `main`:

```bash
git merge origin/main
```

Before merge:

```text
main:         A → B
origin/main:  A → B → C → D
```

After merge (fast-forward case):

```text
main:         A → B → C → D
```

---

# 3. `git pull`

```bash
git pull origin main
```

`git pull` is a shortcut for:

```bash
git fetch origin
git merge origin/main
```

It downloads changes and immediately merges them into your current branch.

---

# Comparison Table

| Command     | Downloads Changes | Updates Working Branch |
| ----------- | ----------------- | ---------------------- |
| `git fetch` | Yes               | No                     |
| `git merge` | No                | Yes                    |
| `git pull`  | Yes               | Yes                    |

---

# Recommended Workflow

Many developers prefer:

```bash
git fetch origin
git log --oneline main..origin/main
git merge origin/main
```

This allows them to inspect incoming changes before applying them.

---

# Pull with Rebase

```bash
git pull --rebase
```

Equivalent to:

```bash
git fetch
git rebase
```

This keeps history more linear by replaying local commits on top of the updated remote branch.

---

# Visual Example

Initial state:

```text
Remote main: A → B → C
Local main:  A → B
```

### After `git fetch`

```text
origin/main: A → B → C
Local main:  A → B
```

### After `git merge origin/main`

```text
Local main:  A → B → C
```

### After `git pull`

```text
Local main:  A → B → C
```

---

# Real-World Usage

In collaborative development, teammates push changes to GitHub. You run `git fetch` or `git pull` to obtain those updates before continuing your work or resolving conflicts.

---

# Summary

| Command                 | Description                                             |
| ----------------------- | ------------------------------------------------------- |
| `git fetch origin`      | Download updates without modifying your current branch  |
| `git merge origin/main` | Integrate downloaded updates into the current branch    |
| `git pull origin main`  | Fetch and merge in one step                             |
| `git pull --rebase`     | Fetch and rebase local commits on top of remote updates |

---

# Most Common Commands

```bash
git fetch origin
git merge origin/main
```

or simply:

```bash
git pull
```

Use `git fetch` when you want to review incoming changes first, and `git pull` when you want Git to update your branch immediately.
