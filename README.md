# Git Technical Concepts & FAQ

### 1. The `.git` Folder
**What is it?**  
The `.git` folder is the "heart" of a repository. It is a hidden directory that turns a regular folder into a Git-managed project.

**What information is stored there?**  
*   **Objects:** All your file contents (blobs), directory structures (trees), and commit metadata.
*   **Refs:** Pointers to commits (branches, tags, and HEAD).
*   **Config:** Repository-specific settings (like remote URLs or local user info).
*   **Hooks:** Scripts that run automatically during certain actions (like pre-commit).
*   **Index:** The staging area information.

**How is it created?**  
It is created using the command:  
`git init` (for new local projects) or `git clone` (when downloading an existing project).

---

### 2. Atomic Commits and Atomic Pull Requests
**Atomic** means "indivisible."
*   **Atomic Commit:** A commit should contain only one logical change (e.g., one bug fix or one small feature). If a change involves 5 files for one feature, they go in one commit. If you fix two unrelated bugs, they should be two separate commits. This makes it easier to track bugs and revert changes if something goes wrong.
*   **Atomic Pull Request:** A PR should be focused on a single task or goal. Large PRs are hard to review and prone to conflicts. An atomic PR ensures the reviewer can focus on one specific implementation.

---

### 3. Comparing Commands: Fetch, Pull, Merge, Rebase, and Cherry-pick
*   **`git fetch`:** Downloads new data from a remote repository but **does not** integrate it into your working files. It only updates your remote-tracking branches.
*   **`git pull`:** A combination of `git fetch` followed by `git merge`. It downloads data and immediately tries to update your current branch.
*   **`git merge`:** Combines the history of two branches by creating a new "merge commit." It preserves the chronological order of how things happened.
*   **`git rebase`:** Moves the entire history of a branch to begin from the tip of another branch. It "rewrites history" to create a clean, linear line of commits.
*   **`git cherry-pick`:** Allows you to pick a specific commit from one branch and apply it to another without merging the whole branch.

---

### 4. Comparing Commands: Reset, Revert, Restore, Switch, and Checkout
*   **`git reset`:** Moves the current branch pointer to a previous commit. It is used to undo local changes (can be "hard" to delete files or "soft" to keep changes in staging).
*   **`git revert`:** Creates a **new commit** that does the exact opposite of a previous commit. It is the safe way to undo changes on a shared remote branch because it doesn't rewrite history.
*   **`git restore`:** A modern command used specifically to undo changes in your working directory or staging area (unstage a file).
*   **`git switch`:** A modern, dedicated command for moving between branches.
*   **`git checkout`:** An older, "all-in-one" command. It can switch branches (like `switch`) OR restore files (like `restore`). It is now recommended to use the specialized commands above.

---

### 5. Staging (Index) and Stash
*   **Staging Area (Index):** This is the "middle ground" between your working directory and the repository history. When you run `git add`, you are placing changes into the Index. It allows you to prepare exactly what you want to include in the next commit.
*   **`git stash`:** If you have unfinished changes but need to switch branches quickly, `stash` temporarily "hides" or saves your uncommitted changes in a stack. You can later use `git stash pop` to bring them back.

---

### 6. Snapshots and Commits
**What is a Snapshot?**  
Unlike other version control systems that store "diffs" (lists of changes between files), Git thinks of its data like a series of **snapshots**. Every time you commit, Git takes a "picture" of what all your files look like at that exact moment.

**Relationship with Commit:**  
A commit is a wrapper around a snapshot. It contains:
1.  A pointer to the snapshot of the project.
2.  Metadata (Author, Date, Message).
3.  A pointer to the parent commit (the previous snapshot).

---

### 7. Local vs. Remote Repository
*   **Local Repository:** This is the copy of the database stored on your own computer (inside the `.git` folder). You can commit, branch, and view history here without an internet connection.
*   **Remote Repository:** This is the version of your project hosted on a server (like GitHub or GitLab). It allows team members to share their local changes by `pushing` to and `pulling` from this central source.

---