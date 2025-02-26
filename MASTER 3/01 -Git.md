---
cover: "[[git.jpg]]"
---
# 💠 Table of Contents
```table-of-contents
title: 
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 2 # Include headings up to the specified level
includeLinks: true # Make headings clickable
hideWhenEmpty: false # Hide TOC if no headings are found
debugInConsole: false # Print debug info in Obsidian console
```
---

# 💠 **Fundamental Concepts**

Git is a **distributed version control system (VCS)** designed to track changes in code, collaborate efficiently, and manage project history. Git enables developers to **work independently** on branches, merge changes, and maintain a reliable project history without interfering with each other's work.

Here are some key concepts:

- **Repository (Repo)** – A **version-controlled directory** that stores a project's entire history, including all commits and branches.
- **Commit** – A **snapshot of changes** in the repository, preserving the project's state at a specific point in time. Each commit has a **unique ID (SHA)** and includes a message describing the changes.
- **Branch** – A **separate line of development**, allowing multiple features or fixes to be worked on independently without affecting the main project.
- **Remote** – A **repository hosted on a server** (e.g., GitHub, GitLab) that enables collaboration by allowing users to **push and pull** changes.
- **Working Directory** – The **local state of the project**, reflecting files that are either untracked, modified, staged, or committed.

---

# 💠 **Configuration**

```bash
# Initial configuration (saved in ~/.gitconfig)
git config --global user.name "Your Name"
git config --global user.email "email@example.com"

# Configuration settings
git config --global pull.rebase true        # Rebase by default when pulling
git config --global color.ui auto           # Enable syntax highlighting

# Adding aliases
git config --global alias.st "status"
git config --global alias.cm "commit -m"
git config --global alias.last "log -1 HEAD --stat"
git config --global alias.unstage "reset HEAD --"
git config --global alias.amend "commit --amend"

# Start a project with Git
git init                         # Initialize a new Git repository
git clone [url]                  # Clone an existing repository
git remote add origin [url]       # Add a remote repository

# Cleanup and maintenance
git fetch -p                                # Remove local branches that no longer exist on the remote repository
git gc --prune=now                          # Clean up and optimize the local repository
git reflog expire --expire=now --all        # Remove obsolete references
```

---

# 💠 **Inspection Commands**

## 1. Commands
- `git status`: Displays tracked/untracked files and pending changes.
- `git diff`: Compares local changes.
    - `git diff`: Differences between the working directory and the index.
    - `git diff --staged`: Differences between the index and the last commit.
    - `git diff [commit1] [commit2]`: Compare two commits.
- `git log`: Commit history with options:
    - `oneline`: Condensed format.
    - `graph`: Graphical view.
    - `p`: Shows differences introduced by each commit.
    - `author="name"`: Filter by author.

## 2. git tree

The `git tree` command is not a native Git command, but there are multiple ways to display a tree view of the repository:

```bash
# Handy alias for a tree view
git config --global alias.tree "log \\
--graph --abbrev-commit --decorate \\
--format=format:'%C(bold blue)%h%C(reset) - %C(bold cyan)%aD%C(reset) %C(bold green)(%ar)%C(reset)%C(bold yellow)%d%C(reset)%n''          %C(white)%s%C(reset) %C(dim white)- %an%C(reset)' \\
--all"

# Usage
git tree
```

> *💡For better visibility, you can install graphical tools like GitKraken or SourceTree, which offer a native tree visualization.*

---

# 💠 **Staging & Unstaging**

**Staging** and **unstaging** allow you to manage changes before committing.

## 1. Staging (Adding to the Index)

The index, also known as the _staging area_, is an intermediate zone where changes are prepared before committing.

- `git add [file]`: Adds a specific file.
- `git add .`: Adds all modified files.
- `git add -p`: Interactively adds portions of files.

## 2. Unstaging (Removing a File from the Index)

Unstaging removes a file from the index without deleting local changes.

- `git restore --staged [file]`: Removes a file from the index.
- `git restore [file]`: Reverts local changes.

> 💡*Always check the status with `git status` before committing to ensure the right changes are included.*

---

# 💠 **Branch Management**

- `git branch [name]`: Creates a new branch.
- `git switch [branch]`: Switches to a branch.
- `git switch -c [new-branch]`: Creates and switches to a new branch.

### HEAD (Reference Pointer)

- **Attached HEAD**: `HEAD` follows a branch.
- **Detached HEAD**: `HEAD` points directly to a commit (via its _hash, ID_, or _HEAD~x_).
- Exiting detached mode if modifications were made:
    ```bash
    git branch new-branch-from-detached-head
    git switch new-branch-from-detached-head
    ```
- **Why use a detached HEAD?**
    - To explore a past commit without modifying the branch.
    - To create a branch from a specific commit.

---

# 💠 **Merging Branches**

Merging branches integrates changes from a secondary branch (`feature`) into a main branch (`main`).

## 1. Merge (Classic Merge)

```bash
git merge [branch]       # Simple merge
git merge --no-ff [branch]  # Keeps an explicit merge commit
```
- **Fast-Forward (ff)**: Moves the main branch forward directly if no intermediate commit has been added (default option).
- **Merge with commit (`-no-ff`)**: Keeps an explicit record of the merge.
- **Secure merge (`-ff-only`)**: Ensures Git does not create a merge commit and refuses the merge if a fast-forward is not possible.

> *⚠️ Generally, `--no-ff` is not used, and `--ff-only` is used after a rebase.*

## 2. Rebase (Reapply commits on another base)

```bash
git checkout feature
git rebase main
```
- Rewrites history to maintain a linear commit history.
- Avoid using on shared branches to prevent disrupting other contributors.

## 3. Cherry-pick (Select a specific commit)

```bash
git cherry-pick <commit-id>
```
- Applies a specific commit from another branch without merging everything.

---

# 💠 **Stashing & Undoing Changes**

## 1. Stashing
- `git stash`: Temporarily saves uncommitted changes.
- `git stash pop`: Restores saved changes.
- `git revert HEAD~x`: Reverts a commit without modifying history.
- `git commit --amend -m "New message"`: Amends the last commit.

## 2. Reset (Undo Changes)

```bash
git reset HEAD~2  # Undo the last 2 commits without deleting files
git reset --soft HEAD~2  # Keep changes in the index
git reset --hard HEAD~2  # Permanently delete changes
```

---

# 💠 **Interactive Rebase**

```bash
git rebase -i HEAD~3 # Modify the last 3 commits
```

## 1. Useful Options

- `pick`: Keeps the commit.
- `squash`: Merges with the previous commit.
- `drop`: Deletes a commit.
- `rename`: Renames a commit.

## 2. Special Case for Modifying a Commit

- Use the `edit` option to go back to the edit state of the commit.
- Modify the desired files.
- Run `git commit --amend` to modify the commit.
- Run `git rebase --continue` (or `git rebase --abort` to cancel the entire interactive rebase if needed).
- Run `git push -f` because history has been modified (**ONLY LOCALLY!!**).

---

# 💠 **Two-Person Workflow**

- Everyone works on `main` or `dev`.
- Use `pull --rebase` to keep a linear history.

---

# 💠 **GitHub Workflow**

## 1. Fork and Clone

- Fork the remote repository if necessary.
- Clone the repository on your local machine:
    ```bash
    git clone [url]
    ```

## 2. Create a Feature Branch

Always create a new branch for each new feature or bug fix:
```bash
git switch -c feature/new-feature

```

## 3. Development and Commits

Add and commit regularly following the conventions from [https://www.conventionalcommits.org/en/v1.0.0/:](https://www.conventionalcommits.org/en/v1.0.0/:)
```bash
git add .
git commit -m "feat: Added feature X"
```

## 4. Update with `main`

If the branch becomes outdated, update it with `main`:
```bash
git pull --rebase origin/main
```

## 5. Push Changes

```bash
git push -u origin feature/new-feature  # To link the branch to the remote repository the first time

git push feature/new-feature
```

## 6. Create a Merge Request (MR)

From GitLab, open an MR towards `main`.

- Add a clear description and mention the reviewers.
- Other contributors review the code.
- Apply feedback before merging.

## 7. Final Update and Rebase

Once the MR is approved:

- Update `main` with `origin`:
    ```bash
    git switch main
    git pull --rebase
    ```
    
- Rebase the `feature/new-feature` branch with `main`:
    ```bash
    git switch feature/new-feature
    git rebase main
    ```
    
- Squash the commits into a single one before merging:
    ```bash
    git rebase -i main
    ```
	Mark all commits except the first one as `squash` or `s` to merge them into a single commit)
    
- Force push (because history has changed):
    ```bash
    git push -f
    ```

> ⚠️ *Never use `git push -f` on a shared branch. Use `git push --force-with-lease` if a force push is necessary on a shared branch.*

## 8. Merge and Delete the Branch

- Switch back to `main` and merge cleanly:
    ```bash
    git switch main
    git merge --ff-only feature/new-feature
    git push
    ```
    
- Delete the branch locally and on `origin`:
    ```bash
    git branch -d feature/new-feature
    git push -d origin feature/new-feature
    ```

This workflow ensures a clean integration and a linear Git history.

---

# 💠 **Git Best Practices**

## 1. Commits

- **Write clear commit messages** using Conventional Commits ([https://www.conventionalcommits.org/en/v1.0.0/](https://www.conventionalcommits.org/en/v1.0.0/)) :
    ```
    feat: add error handling in the form
    fix: fix navbar display on mobile
    ```
- **Never commit broken code**.

## 2. Branches & Collaboration

- **Use dedicated branches for each feature/fix** (`feat/authentication`, `fix/navbar-layout`)
- **Sync with `main` regularly : `git pull --rebase main`**

## 3. Merge Requests

- **Keep MRs small and focused**.
- **Ensure validation before merging**.

## 4. History

- **Squash commits before merging a branch**:
    ```bash
    git rebase -i main
    ```
- **Prefer to merge with fast-forward (`-ff-only`)** when possible to prevent useless commits.
- **Don’t rewrite history of already merged branches, except if critical errors.**

# 💠 **Tips and Tricks**

## 1. Tools

- **`zsh` with `oh-my-zsh`**: Enhanced Git CLI.
- **`tig`**: A terminal-based Git UI.
- **`gitkraken`**: A powerful Git GUI.

## 2. Handy Commands

- **Interactive staging**: `git add -p`
- **Find who modified a line**: `git blame file.txt`
- **Find a bug with bisect**:
    ```bash
    git bisect start
    git bisect bad
    git bisect good v1.0.0
    ```
- **Restore a file**: `git checkout -- file.txt`
- **Remove deleted branches locally**: `git fetch -p`