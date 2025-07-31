# Git Debugging and Restoration Task

## Overview

This task demonstrates essential Git commands for debugging and restoring code changes. It simulates a real-world situation where a bug is introduced, good commits follow, and there's uncommitted work in progress.

---

## Learning Objectives

By completing this task, you will:
- Use `git log` and `git diff` to trace commit history and investigate changes.
- Use `git stash` to temporarily save and restore uncommitted work.
- Choose between `git reset` and `git revert` to fix broken commits.
- Understand the safety implications of rewriting Git history.

---
## Git Commands Used (In Order)

```bash
git init
git checkout -b main
git add calculator.py
git commit -m "feat: Add basic calculator functions (add, subtract)"
git add calculator.py
git commit -m "feat: Add multiply function"
git add calculator.py
git commit -m "fix: Optimize subtract function logic (introducing bug)"
git add calculator.py
git commit -m "feat: Add divide function with zero check"
# Uncommitted changes made here
git status
git log --oneline
git diff <bug-commit>~1 <bug-commit> calculator.py
git stash
git revert <bug-commit>
git stash pop
git push origin main
```
---
## Task Summary

### Step 1: Identify the Bug

- Used `git log --oneline` and `git diff` to locate the commit with the bug.

  <img width="838" height="127" alt="Image" src="https://github.com/user-attachments/assets/00d2e0d6-06eb-4322-96e1-bb78ebdb9383" />
  <img width="679" height="350" alt="Image" src="https://github.com/user-attachments/assets/e79e27de-9802-48f7-a6dc-2bdc50cdc5c3" />

---

### Step 2: Save Uncommitted Work

- Checked status and stashed ongoing changes using:

  ```bash
  git stash
  ```

  <img width="899" height="202" alt="Image" src="https://github.com/user-attachments/assets/74ad8cd6-2f08-4f3f-b605-feea2c83fa00" />
  <img width="1061" height="58" alt="Image" src="https://github.com/user-attachments/assets/fad307e4-e29c-4cb7-b8ab-d839344255c6" />

---

### Step 3: Revert the Bug

- Ran:

  ```bash
  git revert <hash-of-buggy-commit>
  ```

  <img width="1186" height="486" alt="Image" src="https://github.com/user-attachments/assets/002fab0c-2252-45f9-85a6-7081f9128503" />
  <img width="863" height="107" alt="Image" src="https://github.com/user-attachments/assets/0c139f48-19ca-4e4d-a606-074a9677b624" />
---

### Step 4: Restore Stashed Work

- Restored changes using:

  ```bash
  git stash pop
  ```

  <img width="858" height="250" alt="Image" src="https://github.com/user-attachments/assets/edc48edc-3927-487b-8982-b8c5a71eb970" />

---

### Step 5: Final Verification

- Ran and confirmed output:

  ```bash
  python calculator.py
  ```

  <img width="570" height="133" alt="Image" src="https://github.com/user-attachments/assets/880ee2af-9870-42fc-b0e7-956ee66245d4" />

---

## Written Explanations

### How `git log` and `git diff` helped?

- `git log --oneline` showed the chronological list of commits.
- `git diff [commit~1] [commit] calculator.py` revealed the exact changes in `subtract()` — helped locate the logic flaw (`a + b` instead of `a - b`).

---

### Why `git stash` was necessary?

- It saved the uncommitted experimental code safely, letting us modify history (via revert) without losing any ongoing work.

---

### Why I chose `git revert` over `git reset --hard`?

- **git revert** is safe for collaborative environments because it *preserves history*.
- It creates a new commit that cancels the buggy commit without deleting anything.
- In contrast, **git reset --hard** deletes history and is dangerous on shared branches (requires force-push and may disrupt others).

---

### Difference between `git stash pop` and `git stash apply`?

- `git stash pop`: Restores the latest stash *and deletes it*.
- `git stash apply`: Restores the stash *without deleting* it.

**I used `pop`** because I only needed the stash once and didn't want to keep it around.

---

## Final Version of `calculator.py`

[calculator.py](https://github.com/Sherif127/my-first-git-project/blob/cb55b2ec090b29af011f122d8fdbb3aa0a241738/calculator.py)

---