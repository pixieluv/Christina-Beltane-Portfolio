# The Architect's Mac Setup Checklist

This is your master blueprint for setting up a new Mac for development. It provides a clear, repeatable process for installing and configuring all the essential tools.

<details open>
<summary><strong>Phase 1: The Foundation</strong></summary>

* [ ] **Install Xcode Command Line Tools**
    * Open the default **Terminal** app (you can find it in `/Applications/Utilities/`).
    * Run the command:
        ```bash
        xcode-select --install
        ```
    * Click `Install` in the pop-up window and agree to the terms.

* [ ] **Install Homebrew (The macOS Package Manager)**
    * After Xcode tools are installed, run this command in your Terminal:
        ```bash
        /bin/bash -c "$(curl -fsSL [https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh](https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh))"
        ```
    > [!IMPORTANT]
    > After the installation finishes, the script will show you "Next steps". You **must** run the two commands it provides to add Homebrew to your PATH.
    > ```bash
    > (echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"') >> ~/.zprofile
    > ```
    > ```bash
    > eval "$(/opt/homebrew/bin/brew shellenv)"
    > ```
    * After running the commands, **close and restart your Terminal.**

* [ ] **Install and Switch to iTerm2 (Your Power Tool)**
    > [!NOTE]
    > iTerm2 is the professional-grade choice. It offers features like split panes and better search that are essential for a productive workflow.
    * Install iTerm2 using Homebrew:
        ```bash
        brew install --cask iterm2
        ```
    * **Close the old Terminal app.** From now on, you will use **iTerm2** for all command line work.

</details>

<details>
<summary><strong>Phase 2: Version Control & Code Editors</strong></summary>

* [ ] **Install Git & GitHub Desktop**
    * [ ] Update Git using Homebrew:
        ```bash
        brew install git
        ```
    * [ ] Install the GitHub Desktop application:
        ```bash
        brew install --cask github
        ```

* [ ] **Install Sublime Text & Sublime Merge**
    * [ ] Install the Sublime Text editor:
        ```bash
        brew install --cask sublime-text
        ```
    * [ ] Install the Sublime Merge Git client:
        ```bash
        brew install --cask sublime-merge
        ```

</details>

<details>
<summary><strong>Phase 3: Programming Languages</strong></summary>

* [ ] **Install Python**
    * Install the latest version of Python 3:
        ```bash
        brew install python3
        ```

* [ ] **Install R & RStudio**
    * [ ] Install the R language:
        ```bash
        brew install --cask r
        ```
    * [ ] Install the RStudio IDE:
        ```bash
        brew install --cask rstudio
        ```

</details>

<details>
<summary><strong>Phase 4: Database Tools</strong></summary>

* [ ] **Install a SQL Client**
    * Install the TablePlus database client (the user interface):
        ```bash
        brew install --cask tableplus
        ```

* [ ] **Install a SQL Server**
    * Install the MySQL database server (the engine that stores the data):
        ```bash
        brew install mysql
        ```

</details>

<details>
<summary><strong>Phase 5: Understand Your Workflow</strong></summary>

This is the process of how all the tools fit together for a typical project.

1.  **Pull:** Use **GitHub Desktop** or the command line in **iTerm2** (`git pull`) to get the latest version of your project.
2.  **Edit:** Open the project folder in **Sublime Text** to write and edit your code (Python, SQL, R, etc.).
3.  **Commit:** Use **Sublime Merge** or **GitHub Desktop** to visually review your changes, write a commit message, and save a snapshot of your work.
4.  **Push:** Use the "Push" button or command (`git push`) to upload your changes to your public GitHub repository.
5.  **Query:** Use **TablePlus** to connect to databases (like your local MySQL server), run SQL queries, and export results for analysis.

</details>