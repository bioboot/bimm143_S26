---
layout: page
title: Git Conflict Rescue Cheat Sheet
---

If `git pull` fails, Git is usually **protecting your work** — not breaking.

> **Key idea:** Git will stop if pulling changes from GitHub might overwrite local work on your computer.

---

## What is happening when `git pull` fails?

Think of Git as tracking **three versions** of your project:

- **Local files** = what is in your folder right now
- **Local repo** = what you have committed on your computer
- **Remote repo** = what is on GitHub

If these do not line up cleanly, Git asks you to make a choice before continuing.

---

## Golden Rule

> **Always run this before `git pull`:**

```
git status
```

This tells you whether you have local changes that might cause problems.

---

## Fast Decision Guide

### Case 1: I want to keep my local changes

Save them first, then pull:

```
git add .
git commit -m "Save local work before pull"
git pull
```

---

### Case 2: I do NOT want to keep my local changes

Throw them away, then pull:

```
git restore .
git pull
```

If you also created new untracked files you want to delete:

```
git clean -fd
git restore .
git pull
```

> **Warning:** These commands permanently delete uncommitted local work.

---

### Case 3: I want to keep my changes, but I am not ready to commit

Use stash:

```
git stash
git pull
git stash pop
```

If `git stash pop` creates a conflict, you will need to resolve it manually.

---

## Most Common Error Messages

### 1) `Your local changes would be overwritten by merge`

**Meaning:** You edited a file locally, and GitHub has incoming changes for that same file.

**Fix options:**

**Keep your work:**

```
git add .
git commit -m "Save work before pull"
git pull
```

**Temporarily set it aside:**

```
git stash
git pull
git stash pop
```

**Throw it away:**

```
git restore .
git pull
```

---

### 2) Merge conflict

**Meaning:** Git found changes in the same part of a file in two places and cannot decide what to keep.

You may see markers like this inside the file:

```text
<<<<<<< HEAD
my local version
=======
version from GitHub
>>>>>>> main
```

### How to fix it

1. Open the file
2. Decide what the final version should be
3. Delete the conflict markers
4. Save the file
5. Stage and commit the resolved version

```
git add .
git commit -m "Resolve merge conflict"
```

---

## Simple Rescue Workflow

### Step 1: Check what changed

```
git status
```

### Step 2: Ask yourself — do I want to keep my local changes?

If **yes**:

```
git add .
git commit -m "Save my work"
git pull
```

If **no**:

```
git restore .
git pull
```

### Step 3: If Git shows conflict markers

Open the file and fix them manually.

Then run:

```
git add .
git commit -m "Resolve conflict"
```

---

## Best Habits to Prevent Problems

### Before starting work

```
git pull
```

### While working

```
git add .
git commit -m "Describe what I changed"
```

### After finishing

```
git push
```

> **Recommended workflow:**  
> `status → commit → pull → push`

```
git status
git add .
git commit -m "Save my changes"
git pull
git push
```

---

## Emergency "I Don't Want to Lose My Work" Fix

If you are nervous and want the safest beginner option, use this:

```
git status
git add .
git commit -m "Backup my work before fixing pull"
git pull
```

This works well because your work is saved in a commit before you try to merge anything.

---

## Danger Zone Commands

> **Use these only if you are sure you do not need your local changes.**

### Discard tracked file changes

```
git restore .
```

### Delete untracked files/folders

```
git clean -fd
```

### Reset everything to the last commit

```
git reset --hard HEAD
```

---

## One-Sentence Explanation

> **Git is not broken — it is stopping to avoid overwriting your work.**

---

## Mini FAQ

### Why does `git pull` sometimes work and sometimes fail?

It works when Git can combine local and remote changes safely.  
It fails when local work would be overwritten or when the same lines changed in both places.

### What is a merge conflict?

A merge conflict happens when Git needs **you** to choose the final version of a file.

### Should I edit files both on GitHub and on my computer?

Try not to do both at the same time before syncing. That often creates conflicts.

---

## Ultra-Short Version

If `git pull` fails:

1. Run:

```
git status
```

2. If you want to keep your work:

```
git add .
git commit -m "Save local work"
git pull
```

3. If you do not want to keep your work:

```
git restore .
git pull
```

4. If there is a merge conflict:
   - Open the file
   - Remove conflict markers
   - Keep the final version you want
   - Then run:

```
git add .
git commit -m "Resolve conflict"
```


