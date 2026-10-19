# Git Cheat Sheet & Quick Revision

A concise reference guide for essential Git operations, workflows, and branching strategies.

---

## 1. Setup & Configuration

Verify installation and configure global identity settings.

```bash
# Check installed Git version
git --version

# Access Git help documentation
git --help

# Set global user identity
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

# List all current global configurations
git config --global --list
```

---

## 2. Core Workflow & Lifecycle

```mermaid
graph LR
    A[Working Directory] -->|git add| B[Staging Area]
    B -->|git commit| C[Repository]
    C -->|git checkout / switch| A
```

### Basic Commands

| Command | Action |
| :--- | :--- |
| `git init` | Initialize a new local Git repository |
| `git status` | Check working directory & staging area state |
| `git add <path>` | Stage specific file/folder (e.g., `git add src/*`) |
| `git commit -m "msg"` | Save staged changes with a descriptive message |

```bash
# Example Workflow:
git init
git status
git add src/*
git add *      # do not add sytem files or hidden file by default like .gitignore in
git add .gitignore # for system file you need to specificy there name explicitly
git commit -m "Initial commit"
```

---

## 3. History & Inspection

Track history and inspect code changes across stages.

### Viewing History

```bash
git log                  # Detailed commit history
git log --oneline        # Compact single-line summary per commit
git log --graph          # Visual branch topology
git log --all --graph --oneline  # Full repository history graph
```

### Inspecting Differences (`git diff`)

```bash
git diff                 # Working directory vs. Staging area
git diff --staged        # Staging area vs. Last commit (HEAD)
git diff HEAD~1          # Current commit vs. Previous commit
git diff src/index.html  # Working directory changes for specific file
git diff --staged src/index.html # Staged changes for specific file
```

---

## 4. Time Travel & Checkout

Switch contexts or restore working directory files to earlier commits.

```bash
# Move to a specific commit
git checkout <commit-id>

# Return to the latest commit on the main branch
git checkout main
```

---

## 5. Branching & Merging

Isolate feature development and combine changes back into target branches.

```bash
# Branch Operations
git branch my-new-feature     # Create a new branch
git checkout my-new-feature   # Switch to the new branch
```

### Merge Types & Topologies

#### 0. Orignal Scenario Before Merge

```mermaid
gitGraph LR:
   commit id: "A"
   commit id: "B"
   branch feature
   commit id: "C"
   commit id: "D"
```

#### A. Fast-Forward Merge
Occurs when target branch has no new commits since branching.

```mermaid
gitGraph
   commit id: "A"
   commit id: "B"
   commit id: "C"
   commit id: "D"
```

#### B. Non-Fast-Forward Merge (`--no-ff`)
Explicitly creates a merge commit to preserve history context.

```mermaid
gitGraph
   commit id: "A"
   commit id: "B"
   branch feature
   commit id: "C"
   commit id: "D"
   checkout main
   merge feature id: "E"
```

```bash
# Combine branch history with an explicit merge commit
git merge --no-ff fix-incomplete-high-score -m "Fix high score tracker"
```

#### C. Squash Merge
Combines all feature branch commits into a single commit on the target branch.

```mermaid
gitGraph
   commit id: "A"
   commit id: "B"
   commit id: "C+D"
```

```bash
# Squash merge feature branch into current branch
git merge --squash <feature-branch>
```

## Sync With Origin

### Pushing a Local Repository to a Remote

Follow these steps to map your local repository to a remote repository and ensure your `main` branch matches without issues.

### 1. Ensure your local branch is named `main`

```bash
git branch -M main

```

* **Verification:** Run `git branch` to confirm that an asterisk `*` appears next to `main`.

---

### 2. Map your local repository to your remote repository URL

```bash
git remote add origin https://github.com/YourUsername/Your-Repo-Name.git

```

* **Verification:** Run `git remote -v` to ensure the correct fetch and push URLs are listed.

---

### 3. Push your local commits and set the remote tracking branch

```bash
git push -u origin main. #Once you use -u the first time,  
                     #you don't need to specify the remote and branch name for future pushes and pulls.
```

* **Verification:** Run `git status` to confirm your branch is up to date with `origin/main` and no errors are returned.