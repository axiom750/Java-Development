# Experimental Case Study of Git

## Experiment 1 : Detached HEAD

### Q) What is Detached HEAD?

* Detached HEAD allows us to temporarily move `HEAD` to any existing commit without switching to or creating a branch.

* It is useful when we want to go back to an older version of our project for debugging, testing, or inspecting previous code.

* If we make new commits while in Detached HEAD state and want to preserve that work permanently, we should create a new branch.

---

## Visual Understanding

Suppose our system has 3 commits:

```text
A ← B ← C (master)
          ↑
        HEAD
```

By default:

* `HEAD` points to a branch.
* The branch points to the latest commit.

The relationship is:

```text
HEAD
 ↓
master
 ↓
A ← B ← C
```

---

## Going to an Older Commit

Suppose we want to go to commit `B` and test that version of the project.

We can run:

```bash
git checkout B
```

or

```bash
git switch --detach B
```

Now the repository becomes:

```text
A ← B ← C (master)
     ↑
    HEAD
```

We are now at commit `B`.

`HEAD` is detached because it points directly to a commit instead of a branch.

---

## What Can We Do in Detached HEAD?

We can:

* Inspect old code.
* Run the application.
* Test older versions.
* Debug issues.
* Experiment safely.

---

## What Happens If We Create a Commit?

Initial state:

```text
A ← B ← C (master)
     ↑
    HEAD
```

If we make changes and run:

```bash
git commit -m "experiment"
```

Git creates a new commit.

```text
A ← B ← E
     ↑
    HEAD

A ← B ← C (master)
```

Notice:

* `master` still points to `C`.
* The new commit `E` is not attached to any branch.

---

## How to Preserve This Work?

Create a branch:

```bash
git switch -c experiment-branch
```

or

```bash
git checkout -b experiment-branch
```

Now:

```text
A ← B ← E (experiment-branch)

A ← B ← C (master)
```

The work is now safely stored in a branch.

---

## Important Note

Detached HEAD does **not** move commits.

Detached HEAD only moves `HEAD` directly to an existing commit without affecting any branch.

Normal state:

```text
HEAD
 ↓
master
 ↓
A ← B ← C
```

Detached HEAD state:

```text
A ← B ← C (master)
     ↑
    HEAD
```

---

## One-Line Definition

> Detached HEAD is a Git state in which `HEAD` points directly to a commit instead of a branch. It allows us to inspect, test, and experiment with older versions of the project without affecting existing branches.
