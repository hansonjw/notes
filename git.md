# Git and Github Notes

## Documentation
https://git-scm.com/docs

## Basic Workflow
1. Initialize Repository as a git repository
2. Create GitHub Repository
3. link remote repo to local repo
4. Update code (this is done in what is loosely,  or perhaps officially,  refered to as the 'working area')
5. Add 'working version' code to 'staging area '''git add'''
6. Commit and merge code to make it a part of the real code base '''git commit'''
7. Push

## Basic/Common git Commands

`git init`
- Establishes a local folder as a Git repository
- The repository doesn't exist on GiHub Yet
- Typically this is one of the first things you do

`git remote add origin <REMOTE REPOSITORY URL>`
- Links the local folder to your GitHub repository
- example of <REPOSITORY URL> = git@gist.github.com:a4a006c4cead41c544b5ff9a4dba0785.git
- This is typically the 3rd step in the following sequence...
    1. `git init`
    2. create GitHub repo
    3. `git remote add origin <REMOTE REPOSITORY URL>`

`git remote -v`
    - Tells you what the remote repository is

`git clone`
- pull a repository down to your local machine
- need to have the URL

`git pull`
- pull latest remote repository upates into local version

`git status`
- check status of current directory
- lists files that have changes that have not been staged `git add`

`git add -A`
- Essentially adds all files to the stage
- From the git documentation:
    >*Adds, modifies, and removes index entries to match the working tree.*

`git commit -m`
- Records changes to the repository
- Moves changes from the staging area to repository
- Suggested/percieved standard conventions for commit messages:
    1. must be in quotation marks
    2. written in the present tense
    3. should be brief, 50 characters or less

`git push origin master`
- Update remote repository with changes that have been commited committed in local repo
- <origin> is the reference to the repo
- <master> represents current branch in local repo...typically for personal projects you would only want to push the main branch as ultimately the objective is to have all code on the main branch
- This is different when working in teams and pull requests
- Pushes a local branch to the origin remote

`git clone <GIT REPOSITORY> <LOCAL DIRECTORY TO CREATE>`
- Clones a repository into a newly created directory
- `<LOCAL DIRECTORY TO CREATE>` is to specify a name/directory on your machine/local copy
- Documentation indicates that git does not care about names of directories

`git stash`
- From the documentation:
    >*Use git stash when you want to record the current state of the working directory and the index, but want to go back to a clean working directory. The command saves your local modifications away and reverts the working directory to match the HEAD commit.*

    >*When you are in the middle of something, you learn that there are upstream changes that are possibly relevant to what you are doing. When your local changes do not conflict with the changes in the upstream, a simple git pull will let you move forward.*

    >*However, there are cases in which your local changes do conflict with the upstream changes, and git pull refuses to overwrite your changes. In such a case, you can stash your changes away, perform a pull, and then unstash, like this:*
    ```$ git pull
    ...
    file foobar not up to date, cannot merge.
    $ git stash
    $ git pull
    $ git stash pop
    ```
- This is how you would over-write existing changes:
    ```
    git fetch
    git reset --hard HEAD
    git merge origin/$CURRENT_BRANCH
    -- or --
    git mergin @{u}
    ```
- This is how you would pull new stuff and keep existing changes --
    ```
    git fetch
    git stash
    git merge '@{u}'
    git stash pop
    ```
- [ ] *_I should go back and work a example of this in with git and GitHub_*

`git fetch origin`
- Sync local repository with remote repository
- [ ] *_I need to study this topic more in depth, examples would be helpful_*
- [ ] What is the difference between git fetch and git pull?

## Branches and Merging back

`git branch`
- displays all the branches in the repository
- Also highlights the branch you are on
- In Git, branches are usually a means to an end. You create them to work on a new project feature, but the end goal is to merge that feature into the master branch. After the branch has been integrated into master, it has served its purpose and can be deleted.

`git branch -d <BRANCH_NAME>`
- this deletes a branch from your local repository
- Codecademy states that good practice is to delete branches when no long needed and when they have served thier purpose

`git branch <BRANCH_NAME>`
- creates a new branch
- branch names cannot contain white space
- Note: you will still 'be on' the previous branch when the new branch is created.  See below.

`git checkout <BRANCH_NAME>`
- switch to a different branch

`git checkout -b <BRANCH_NAME>`
- creates new branch and...
- moves the checked out branch to the new branch

`git merge <BRANCH_NAME>`
- Use this command to merge changes
- Changes are merged from <BRANCH NAME> to the existing branch

`git checkout -- path/to/file`
- If you can't switch branches due to uncommitted work or you simply want to discard changes that don't need to be staged in Git
- Use the command to reset individual files. For example, git checkout -- index.html would reset index.html to its most recent commit.
- [ ] Go back and reaquaint myself with an example...

*_The UCB workflow does teach to merge branches back to previous branches
and to push each merged branch back to the origin:_*
- Starting on the branch: features/feature_a
    ```
    git add -A
    git commit -m "<YOUR MESSAGE HERE>"
    git push origin features/feature_a
    ```
- Switch to branch: develop
    ```
    git checkout develop
    git merge features/feature_a
    git push origin develop
    ```
- Switch to the branch: master
    ```
    git checkout master
    git merge develop
    git push origin master
    ```


`git rm -r --cached <FILE_OR_DIRECTORY_TO_EXCLUDE>`
>Create the .gitignore file during the initial setup of the project to avoid accidentally tracking the folder with the git add -A command. If the <FILE_OR_DIRECTORY_TO_EXCLUDE> folder was accidentally tracked by git, use the following (above) command to remove the tracking...replace node-modules with a file or sub-directory name

`git remote set-url origin <GIT_URL>`
- change the origin; use this when cloning some code then pushing to your own repository

`git remote rm <remote-name>`
- use this to remove the remote repository reference from current local repo
- for <remote-name> typically you would enter 'origin'

`git diff <filename>`
- outputs the differences between <filename> in the staging area vs the working version

Three different ways to backtrack in Git.
** HEAD is  the most recent commit **
1. git checkout HEAD <filename>
2. git reset HEAD <filename>
3. git reset <commit_SHA>

`git reset <commit_SHA>`
- This command works by using the first 7 characters of the SHA of a previous commit   

`git log`
- outputs list of commits for current directory

`git log --oneline` 
- shows the list of commits in one line format.

`git log --oneline --graph - --graph`
- Displays a visual representation of how the branches and commits were created in order to help you make sense of your repository history

`git log --pretty=format:"%h %s" --graph`
- A clean way to print out the commit log

`git commit --amend`
- ??

`git commit --amend --no-edit`
- Allows for no change to the comment on commit you are ammending

## config
`git config --global alias.co "checkout"`
`git config --global alias.br "branch"`
`git config --global alias.glop "log --pretty=format:"%h %s" --graph"`
- [ ] Need to learn more about this

## GitHub Pages:
- https://pages.github.com

## .ignore
- https://github.com/github/gitignore
- https://git-scm.com/docs/gitignore

## Forking a repository
- Add upstream and connectivity back to original repository to allow updates to original code base to be pulled through
- Example: git clone <REPOSITORY>
- Git remote add upstream <REPOSITORY SSH stuff>
- Git fetch upstream - this will update forked repository with changes in upstream repo
- Forking a repo is something done in GitHub, essentially copying a repo from another user/source
- Once forked adding upstream allows you to pull through latest changes to original repo
- The forked repo is not connected in this fashion when cloned
- Cloning is something you do in GitHub

# VIM is not a part of git; it is a text editor within the command line
- If you end up in VIM, to get out do the following:
    - To enter command mode in VIM, type :
    - To quit, type q
    - Press ENTER
    - Or you can enter SHIFT + Z + Z
- It is not uncommon to end up in VIM when working the command line
- A common time this happens to me is when I am committing fail to type the closing quote on the commit message