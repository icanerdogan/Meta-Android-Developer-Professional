## Working with Git

### What is Git and Github?

Version control systems, specifically Git and GitHub, using the analogy of app updates to illustrate their utility. Git is described as a version control system addressing the challenges of tracking changes in large projects, with benefits including speed, reliability, open-source accessibility, and a command line interface. GitHub is presented as a cloud-based hosting service that extends Git's capabilities, providing a user interface for managing repositories, with features like access control, pull requests, and automation. The text emphasizes GitHub's popularity among web developers, likening it to a social network. It encourages further exploration of Git and GitHub for effective version control in software and web development.

**Git Features**

1. **Version Control System:** Designed to track changes in files within projects.
2. **Created by Linus Torvalds:** Specifically to manage changes in the Linux kernel.
3. **Addressing Challenges:** Designed to overcome challenges in tracking changes in large projects with daily updates.
4. **Advantages of Git:**
    - Better speed and performance.
    - Reliability.
    - Free and open source.
    - Accessible syntax.
5. **Command Line Usage:** Predominantly used via the command line, with developers finding syntax and commands easy to learn.

**GitHub Features**

1. **Cloud-Based Hosting Service:** Manages Git repositories through a user interface.
2. **Git Repository Management:** Tracks changes to files, maintaining a history of modifications.
3. **Extended Features:**
    - Access control: Regulates user access to repositories.
    - Pull requests: Facilitates collaboration and code review.
    - Automation: Automates certain processes within repositories.
4. **Pricing Models:** Features are split into different pricing models to accommodate various team sizes and organizations.
5. **Popularity Among Web Developers:** GitHub is described as popular and likened to a social network.
6. **Public and Private Projects:** Projects can be either public or private, with public projects accepting contributions globally.
7. **User Profiles:** Users have profiles, and others can follow them, enhancing the social aspect.
8. **Additional Features:** GitHub includes tools beyond core development, such as documentation, ticketing, and project management features.

The text concludes by acknowledging the reader's familiarity with Git and GitHub, highlighting that it marks the beginning of their version control journey.

### How Git Works?

In this video, the instructor provided an overview of Git and GitHub, emphasizing the importance of Git as a version control system and GitHub as a cloud-based hosting service. The process of creating and cloning a repository was demonstrated, focusing on the "my-first-repo" directory.

The video then delved into the contents of the repository, highlighting the "[README.md](http://readme.md/)" file and the ".git" hidden folder. The ".git" folder, automatically created by GitHub, serves to track all changes in the repository.

Next, the Git workflow was explained, breaking it down into three states: modified, staged, and committed. Any changes to a file are considered "modified," and to track these changes, they need to be moved to the "staged" area. Once staged, the changes can be committed, creating a snapshot of the current state of the repository.

An example workflow was presented, illustrating the three stages, as well as the inclusion of a remote repository. The steps included adding a file to the working directory, moving it to the staging area, committing the changes, and pushing them to the remote repository. The tutorial hinted at future topics, such as fetching, checking out, and merging changes from the remote repository.

In summary, the tutorial provided a foundational understanding of Git and GitHub, explored the contents of a Git repository, explained the Git workflow, and introduced a practical example to reinforce the concepts learned.

![Ekran Resmi 2023-11-22 22.16.21.png](Meta%20Android%20Developer%20Coursera%20d4e715a2e3674c5baab68e34e9566bf6/Ekran_Resmi_2023-11-22_22.16.21.png)

### Git Terminology

### Add & Commit

In this section of the tutorial, the instructor demonstrates basic Git commands within the context of a Git repository named "my-first-repo."

1. **Checking Current Status:**
    - The instructor starts by using the `pwd` command to identify the current working directory (`my-first-repo`) and then runs `ls -la` to list the contents, revealing a `README.md` file and a hidden `.git` folder.
    - `git status` is introduced to check the current status of the repository. It indicates being on the "main" branch, up to date with the remote repository, and having a clean working tree.
2. **Adding a New File:**
    - The instructor adds a new file, `test.txt`, using the `touch test.txt` command.
    - Running `git status` again reveals an untracked file (`test.txt`), prompting the use of `git add` to stage the file for commit.
3. **Staging and Unstaging:**
    - After using `git add test.txt`, the instructor checks status, confirming the file is staged for commit.
    - Demonstrates using `git restore --stage test.txt` to unstage the file, and again checks status to verify the file is back to an untracked state.
    - Repeats the process of adding the file with `git add test.txt`.
4. **Committing Changes:**
    - The instructor emphasizes the importance of the staged area in preparing files for commit.
    - Introduces the `git commit` command with the `m` flag for adding a commit message.
    - After committing, the response indicates the file change, insertions, deletions, and the creation of `test.txt`.
    - Running `git status` confirms a clean working tree but prompts to use `git push` to upload local commits to the remote repository.

The tutorial concludes by clearing the screen and reiterating that changes made are currently specific to the local machine.

Emphasizes the need to use `git push` to synchronize local commits with the remote server, introducing the concepts of push and pull commands for future lessons.

In summary, this section covers checking status, adding and staging files, committing changes with messages, and underscores the distinction between local changes and the need to push changes to the remote repository.

### Branches

In this tutorial segment, the instructor covers branching and collaboration using Git and GitHub:

1. **Checking Current Status:**
    - Demonstrates using the `pwd` command to verify the current directory (`my-first-repo`) and runs `git status` to ensure there are no outstanding commits.
2. **Creating a New Branch:**
    - Introduces the creation of a new branch using `git checkout -b feature/lesson` or alternatively `git branch feature/lesson` followed by `git checkout feature/lesson`.
    - Emphasizes that any changes made in this new branch will not affect the main branch until a merge occurs.
3. **Adding and Committing Changes in the New Branch:**
    - Creates a new file, `test2.txt`, using the `touch test2.txt` command.
    - Adds and commits the new file to the branch using `git add` and `git commit`.
    - Pushes the changes to the remote repository using `git push -u origin feature/lesson`.
4. **Creating a Pull Request:**
    - Highlights the significance of pull requests for peer reviews, testing, and merging changes back into the main branch.
    - Navigates to GitHub, opens a pull request, and compares changes between the new branch and the main branch.
5. **Merging Changes:**
    - Demonstrates the process of merging the new branch into the main branch after approval.
    - Discusses the option to delete or keep the branch after merging.
6. **Updating the Main Branch Locally:**
    - Switches back to the local main branch using `git checkout main`.
    - Uses `git pull` to fetch and merge changes from the remote repository, including the newly merged branch.
    - Verifies changes in the directory with `ls` and confirms the presence of `test2.txt`.

The tutorial concludes by summarizing the branching workflow, emphasizing the benefits of branching for collaboration, and showcasing the integration of changes through pull requests and merges.

### Remote & Local

In this video tutorial, the instructor explains the concepts of local and remote in the context of Git and GitHub. Here's a summary:

1. **Introduction to Local and Remote:**
    - In the pre-internet era, transferring project files between machines was tedious.
    - The cloud has revolutionized this process, allowing for more efficient collaboration.
    - In Git, "local" refers to a user's machine, while "remote" refers to any external repository (e.g., on GitHub).
2. **Accessing Remote Code:**
    - Remote code is accessed through a URI (Uniform Resource Identifier) unique to the repository.
    - The URI provides access to the project stored on a remote server, such as GitHub.
3. **Cloning and Pulling:**
    - To copy a project from a remote repository to a local machine:
        - Use "clone" for the first time to copy the entire project.
        - Use "pull" to get the latest changes from the server.
4. **Working Offline and Pushing Changes:**
    - Users can make changes to the local copy of the project and push those changes back to the server.
    - Other users won't see these changes until they pull the latest changes from the server.
5. **Example in GitHub:**
    - Demonstrates the process on GitHub, creating a new local repository using commands (`mkdir`, `cd`, `git init`).
    - Explains the absence of a remote connection (`git remote`) since it's a local repository.
6. **Setting Up Remote Connection:**
    - Goes into an existing repository (`my-first-repo`) with an established connection to GitHub.
    - Checks the remote URL using `git remote -v`.
    - Sets up a remote connection for the new repository using `git remote add origin <URL>`.
7. **Pulling Changes from Remote:**
    - Uses `git pull` to connect with the GitHub server and pull down all changes.
    - Explains the need to set up a local branch that matches the remote branch.
8. **Branch Setup and Verification:**
    - Uses `git checkout main` to set up a local branch tracking the remote main branch.
    - Verifies the presence of files in the local directory using `ls`.

Summarizes the key concepts of local and remote in Git and GitHub.

Emphasizes the efficiency gained in exchanging data within development teams through these concepts.

The tutorial provides a practical understanding of how local and remote repositories function in Git and GitHub, offering a foundation for efficient collaboration in software development.

### Push & Pull

In this tutorial, the instructor guides through the process of pushing changes to a remote repository using `git push` and retrieving changes from the remote repository using `git pull`. Here's a summary:

1. **Checking Branch Status:**
    - Using `git status` to check the current branch status.
    - Noting that the local branch is ahead of the origin/main branch by one commit, indicating changes on the local machine.
2. **Pushing Changes to Remote Repository:**
    - Emphasizing the importance of knowing the current branch using `git status` or `git branch`.
    - Using `git push` to push changes to the remote repository (`origin/main`).
    - Providing login information for authentication when pushing via HTTPS.
    - Demonstrating the appearance of changes on the GitHub website.
3. **Preventing Conflicts and Pulling Changes:**
    - Highlighting the importance of running `git pull` before `git push` to reduce the risk of conflicts.
    - Discussing auto-merge in the absence of conflicts.
4. **Working with `git pull`:**
    - Adding a line to `test.txt` directly on the GitHub UI.
    - Committing the change directly to the main branch on GitHub.
    - Demonstrating an empty `test.txt` file on the local machine before running `git pull`.
    - Running `git pull` to retrieve the latest changes from the remote repository.
    - Verifying the updated content in the local `test.txt` file.
5. **Understanding `git pull`:**
    - Explaining that `git pull` fetches changes from the remote server and merges them with the local snapshot.
    - Mentioning that auto-merge occurs if there are no conflicts.
    - Highlighting the completion of the process with the latest changes on the local machine.

In summary, the tutorial covers the crucial Git commands `git push` and `git pull`, emphasizing their significance in collaborating with remote repositories on platforms like GitHub. The importance of checking branch status, avoiding conflicts, and ensuring the synchronization of local and remote repositories is underscored throughout the tutorial.

### Diff

In this tutorial, the instructor covers the usage of the `git diff` command to compare changes across files, branches, and commits. Here's a summary of the key points:

1. **Introduction to Git Status and Git Diff:**
    - `git status` informs you about which files have been changed in your repository.
    - `git diff` goes further, providing a detailed view of the specific changes within the files.
2. **Analogizing Git Status and Git Diff:**
    - Analogously, think of `git status` as providing file names, and `git diff` as opening the file to display content changes.
3. **Example Scenario - Using Git Diff for File Changes:**
    - Consider a scenario where you have a file named `CITIES.txt` documenting cities visited during a tour.
    - After making updates, `git diff` helps compare the current version with the previous one, highlighting additions and removals.
4. **Detailed Example - Git Diff for File, Commits, and Branches:**
    - Demonstrates using `git diff` for file changes by editing the `README` file.
    - Shows how to compare against the `HEAD` using `git diff HEAD <file>`.
    - Introduces the usage of `git log` to display commit history.
    - Compares changes between the most recent and the initial commit using `git diff <commitID1> <commitID2>`.
    - Highlights how to use `git branch` to list available branches and `git diff <branch1> <branch2>` to compare branch changes.
5. **Summary:**
    - `git diff` is a powerful tool for tracking changes across files, commits, and branches.
    - Useful for reviewing updates, avoiding mistakes, and managing code overlap.

This tutorial provides practical examples and insights into leveraging `git diff` for effective version control and collaboration in a Git repository.

### Blame

In this tutorial, the instructor introduces the `git blame` command, which is a powerful tool for tracking changes in a Git repository. Here's a summarized breakdown of the key points:

1. **Purpose of Git Blame:**
    - `git blame` helps in keeping track of who made changes, when the changes were made, and what specific changes were implemented in a file.
2. **Format of Git Blame Output:**
    - Each line in the output starts with:
        - Commit ID
        - Author's name
        - Timestamp of the change
        - Line number in the file
        - Actual content change
3. **Real Example Using `git blame`:**
    - Demonstrates the usage of `git blame` on a specific file (`feature.js`) in a local repository.
    - Explains the breakdown of the output, highlighting commit ID, author, timestamp, line number, and content.
4. **Example with Public Repository (`MK docs`):**
    - Shows how to use `git blame` on a file (`setup.py`) in a public repository (`MK docs`) with multiple contributors.
    - Discusses the output format and details provided, such as commit hash, author, timestamp, line number, and content changes.
5. **Navigating Git Blame Output:**
    - Offers tips on navigating through the blame output, including scrolling through changes and exiting the display.
6. **Limiting Output with Line Range:**
    - Demonstrates how to limit the output by specifying a line range using the `l` flag (e.g., `git blame -l 5,15 setup.py`).
7. **Customizing Output Format:**
    - Explains how to customize the output format using flags such as `l` and provides examples of changes in output style.
8. **Viewing Detailed Changes:**
    - Shows how to view detailed changes for a specific commit using `git blame` in conjunction with `git log -p`.

Offers additional tips, such as changing the display format, controlling the visibility of email addresses, and modifying the date format.

`git blame` is a valuable command for understanding the history of changes in a file, enabling effective collaboration and tracking contributions.

This tutorial provides practical examples and insights into effectively using the `git blame` command to navigate through file histories in a Git repository.

### HEAD

In this tutorial, the instructor explains the concept of the `HEAD` pointer in Git, which is responsible for indicating the current commit in a project. Here's a summary:

1. **Understanding the `HEAD` Pointer:**
    - The `.git` folder in each Git project contains a special pointer called `HEAD`.
    - `HEAD` points to the current commit, indicating the commit you are currently viewing.
2. **Identifying the Current Commit:**
    - Opening the `.git` folder using `cd .git` in the terminal.
    - Using `cat HEAD` to view the contents of the `HEAD` file, which points to the current commit.
    - The file shows a reference to the commit, indicating the branch (e.g., `refs/heads/main`).
3. **Switching Branches and Updating `HEAD`:**
    - Switching branches using `git checkout testing`.
    - Using `git branch` to verify the branch switch and see the updated `HEAD`.
    - Demonstrating that `HEAD` now points to the testing branch.
4. **Checking `HEAD` with a Diagram:**
    - Using a diagram to illustrate how `HEAD` moves when switching branches.
    - When running `git checkout testing`, `HEAD` moves to point to the testing branch.
5. **Viewing `HEAD` Content with `less`:**
    - Using `less .git/HEAD` to check the contents of the `HEAD` file after a branch switch.
    - Verifying that `HEAD` now points to the testing branch.
6. **Making Changes and Updating `HEAD`:**
    - Making a change to a file (e.g., `readme.md`) using an editor or Vim.
    - Checking the commit reference with `cat .git/refs/heads/main` before committing.
    - Adding and committing the changes to see the updated commit reference.
    - Verifying the change in the commit reference using `cat .git/refs/heads/main`.
7. **Summary of `HEAD` Purpose:**
    - `HEAD` is a pointer in the `.git` folder indicating the current commit.
    - It can be switched to point to a different branch, allowing you to work on different branches.
    - Changes to files and commits affect the commit reference pointed to by `HEAD`.
8. **Additional Reading:**
    - Mentioning a link for additional reading to delve deeper into the topic.

In summary, the tutorial provides a clear understanding of how the `HEAD` pointer works in Git, how it points to the current commit, and how it changes when switching branches or making new commits.

### **Forking**

Forking is another type of workflow. The key difference between branching and forking is that the workflow for forking creates a new repository entirely. Branching cuts a new branch from the same repository each time and each member of the team works on the single repository.

Forking in the context of version control systems, especially Git, refers to creating a personal copy of someone else's project. When you fork a repository, you essentially copy the entire repository to your own account on the platform where the original repository is hosted (like GitHub or GitLab). This forked repository is then independent of the original, allowing you to make changes without affecting the original project. Forking is commonly used in collaborative development and open source projects. Here's how the process typically works:

1. **Forking:**
    - You find a project on a platform like GitHub that you want to contribute to or use for your own purposes.
    - Instead of directly modifying the original repository, you fork it. On platforms like GitHub, there is usually a "Fork" button that makes this process easy.
2. **Cloning:**
    - After forking, you clone the forked repository to your local machine using Git. This creates a local copy on your development environment.
3. **Remote:**
    - Git is configured to have two remotes: one pointing to the original repository (upstream) and one pointing to your fork on the platform (origin).
4. **Contributions:**
    - You can make changes to the code in your local copy, create new branches, and experiment freely.
5. **Pull Request:**
    - Once you're ready to contribute your changes or improvements back to the original project, you create a pull request. This is a request to the original project to pull in your changes.
6. **Merging:**
    - The maintainers of the original project review your changes, and if everything is satisfactory, they merge your changes into the main project.

Forking is a fundamental concept in distributed version control systems like Git, enabling collaboration among developers, especially in open source projects. It allows contributors to experiment, make improvements, and propose changes to a project without directly modifying the original codebase.