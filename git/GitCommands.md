# Git Commands

| Command | Description |
| :----- | :---------- |
| git init . | Initializes current directory as a git repository |
| git add <FILE_NAME> | Adds the mentioned file to the staging |
| git add . | Adds all the files to the staging |
| git add * | Adds all the files to the staging |
| git commit -m "<COMMIT_MESSAGE>" | Commits the staged files with information of what changes has done |
| git status | Displays the current status of repository |
| git log | Shows/Outputs logs of current repository |
| git remote add "<REMOTE_REPO_URL>" | Adds remote repo to the local repository |
| git clone <REMOTE_REPO_URL> | Clones the repo into local system directory |
| git pull <REMOTE_NAME> <BRANCH_NAME> | Pulls the changes done in remote repo into local repo |
| git push -u <REMOTE_NAME> <BRANCH_NAME> | Pushes commits to the branch mentioned to remote repo |
| git diff --staged or git diff --staged HEAD | Compares local repo files with staging |
| git diff HEAD | Compares the working directory files with the local repository |
| git diff <COMMIT_ID1> <COMMIT_ID2> | Compares changes between two commits |
| git diff HEAD HEAD~1 | Compares changes between present and previous commit respectively |
| git branch | Shows how many branches are present in the repo |
| git branch <BRANCH_NAME> | To create a new branch at the current commit |
| git checkout <BRANCH_NAME> | Switches to the mentioned branch |
| git checkout -b <BRANCH_NAME> | To create new branch and switch to branch |
| git switch - | Switches to the default branch quickly |
| git mrerge <BRANCH_NAME> | Merges the branch with current branch |
| git merge <SOURCE_BRANCH> <DEST_BRANCH> | Merges the source branch with destination branch |
| git checkout <COMMIT_ID> <FILE_NAME> | Moves to the commit |
| git checkout HEAD~1 | Moves to the previous commit |
| git branch -d <BRANCH_NAME> | To delete a branch |
| git tag | To check the existing tags in the repo |
| git tag <VERSION_RELEASE> | Creates a tag in the repo at the current point/commit |
| git push <REMOTE_NAME> <VERSION_RELEASE> | To push the tag to the remote repository |
| git tag -a <VERSION_RELEASE> <COMMIT_ID> -m "<TAG_MESSAGE>" | To create a tag to a specific commit in the repo |
| git tag -a -f <VERSION_RELEASE> <COMMIT_ID> -m "<TAG_MESSAGE>" | To retag or replace old tags or update the tag, the "-f" FORCE option must be used. |
| git restore <FILE_NAME> or git checkout -- <FILE_NAME> | Reverts changes from working directory |
| git restore --staged <FILE_NAME> | To revert changes from staging area to workinig directory |
| git restore <FILE_NAME> | To restore changes from working directory |
| git reset HEAD~ | Revert changes from local repo to the working directory |
| git reset HEAD . | Unstage all changes |
| git reset HEAD <FILE_NAME> | Unstage the file |
| git reset HEAD~N | Revert commits on local repository (N is number of commits to revert) |
| git rebase -i HEAD~N | To combine multiple comments as a single. (N is number of commits to squash) |
| git config --global user.name "<USER_NAME>" | Adds your username to git |
| git config --global user.email "<USER_NAME@EMAIL.COM>" | Adds your email to git |
| git checkout -- <FILE_NAME> | To revert changes made to the file from git working directory area |
| git checkout -- . | To revert all changes from git working directory area |
| git show <COMMIT_ID>| Shows the deatils of commit |
| git show HEAD | Shows the details of latest commit |
| git show HEAD~1 | Shows the details of last second commit |
| git annotate <FILE_NAME> | Annotate file lines with commit information |
