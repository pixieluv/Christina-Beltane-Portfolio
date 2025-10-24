# Git Command Cheatsheet

This cheatsheet provides essential Git commands and workflows, tailored for managing your portfolio using GitHub Desktop, the command line (iTerm2), and Sublime Text/Merge.

---

### **Core Concepts**

* **Repository (Repo):** Your project folder (e.g., `Christina-Beltane-Portfolio`).
* **Local Repository:** The copy of the repo on your Mac.
* **Remote Repository:** The copy of the repo hosted on GitHub.com.
* **Commit:** A saved snapshot of your changes.
* **Branch:** An independent line of development (e.g., `main` is the primary branch).
* **Pull:** Download changes from the remote repo to your local repo.
* **Push:** Upload your local commits to the remote repo.
* **Fetch:** Download changes from the remote repo *without* merging them yet (lets you see what's new).
* **Merge:** Combine changes from one branch into another.

---

### **Workflow 1: Using GitHub Desktop (Recommended for Simplicity)**

GitHub Desktop provides a visual interface for most common Git operations.

1.  **Open GitHub Desktop:** Select your `Christina-Beltane-Portfolio` repository.
2.  **Fetch Origin:** Click the `Fetch origin` button (top right). This downloads any changes from GitHub.com without applying them yet. If there are changes, the button will change to `Pull origin`.
3.  **Pull Changes (If Necessary):** If the button says `Pull origin`, click it to download and merge changes from GitHub.com into your local files. **Always do this before making new edits.**
4.  **Make Changes:** Edit your files (e.g., add a new template) using **Sublime Text**. Save your changes.
5.  **Review Changes:** Go back to **GitHub Desktop**. The changed files will appear in the "Changes" tab on the left. Click on a file to see the specific lines you added or modified (the "diff").
6.  **Commit Changes:**
    * Enter a concise **Summary** message in the bottom-left corner (e.g., "Add Statement of Work template").
    * (Optional) Add a more detailed **Description**.
    * Click the **`Commit to main`** button. This saves a snapshot of your changes *locally*.
7.  **Push Changes:** Click the **`Push origin`** button (top right). This uploads your local commit(s) to GitHub.com, making them visible to others.

---

### **Workflow 2: Using the Command Line (iTerm2)**

This workflow provides more control but requires memorizing commands.

1.  **Navigate to Repository:**
    * Open **iTerm2**.
    * Use the `cd` (change directory) command to navigate to your project folder. Example:
        ```bash
        cd ~/Documents/GitHub/Christina-Beltane-Portfolio 
        # Adjust path as needed
        ```
2.  **Check Status:** See what files have changed:
    ```bash
    git status
    ```
3.  **Pull Changes:** Download and merge changes from GitHub.com. **Always do this before making new edits.**
    ```bash
    git pull origin main 
    # 'origin' is the default name for your remote repo
    # 'main' is the default branch name
    ```
4.  **Make Changes:** Edit your files using **Sublime Text**. Save your changes.
5.  **Stage Changes:** Tell Git which changed files you want to include in your *next* commit.
    * To stage a specific file:
        ```bash
        git add path/to/your/file.md 
        ```
    * To stage *all* changed files (use with caution):
        ```bash
        git add .
        ```
    * Run `git status` again to see which files are staged ("Changes to be committed").
6.  **Commit Changes:** Save a snapshot of the *staged* changes locally.
    ```bash
    git commit -m "Your concise commit message here" 
    # Example: git commit -m "Add SoW and RACI templates"
    ```
    * (Optional) For a longer message, just run `git commit` and it will open your default text editor.
7.  **Push Changes:** Upload your local commit(s) to GitHub.com.
    ```bash
    git push origin main
    ```

---

### **Workflow 3: Using Sublime Merge (Visual Git Client)**

Sublime Merge is a powerful visual tool focused specifically on Git operations, often used alongside Sublime Text.

1.  **Open Repository:** Open your `Christina-Beltane-Portfolio` folder in Sublime Merge.
2.  **Fetch/Pull:** Use the `Fetch` or `Pull` buttons/menu options (often near the top) to sync with the remote repository on GitHub.com. **Do this before making edits.**
3.  **Make Changes:** Edit files in **Sublime Text**.
4.  **Stage Changes:** In **Sublime Merge**, the changed files will appear. You can view the diffs. Select the files or specific lines ("hunks") you want to include in the next commit and click the `Stage` button.
5.  **Commit Changes:** Enter your commit message in the designated area and click the `Commit` button.
6.  **Push Changes:** Use the `Push` button/menu option to upload your commit(s) to GitHub.com.

---

### **Common Useful Commands (Command Line)**

* **`git status`**: Show the status of changes (modified, staged, untracked).
* **`git log`**: Show the history of commits.
* **`git diff`**: Show unstaged changes compared to the last commit.
* **`git diff --staged`**: Show staged changes compared to the last commit.
* **`git checkout <filename>`**: Discard unstaged changes in a specific file.
* **`git reset HEAD <filename>`**: Unstage a file (move it from staged back to unstaged).

> [!TIP]
> Choose the workflow you find most comfortable. GitHub Desktop is great for simplicity. The command line offers the most power. Sublime Merge is a good visual alternative for those who prefer it.