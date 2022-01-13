# Git and Github Notes

## Documentation
https://git-scm.com/docs

## Basic Workflow
1. Initialize Repository as a git repository
2. Update code (this is done in what is loosely refered to as the 'working area')
3. Add 'working version' code to 'staging area '''git add'''
4. Commit and merge code to make it a part of the real code base '''git commit'''

## Common git Commands

`git clone`
- pull a repository down to your local machine
- need to have the URL

`git pull`

`git status`
- check status of current directory

git add -A

git commit -m
    pushes from staging area to repository
    standard conventions for commit messages:
    1. must be in quotation marks
    2. written in the present tense
    3. should be brief, 50 characters or less

git push origin master
git push origin main
    - Pushes a local branch to the origin remote

git clone <git repository> <directory>
    - This is to specify a name for the clone on your machine
    - Documentation indicates that git does not care about names of directories

git stash

git pull

git fetch origin
    - Sync local repository with remote repository

git merge <BRANCH NAME>
    - Use this command to merge changes
    - Changes are merged from <BRANCH NAME> to the existing branch

-- This is how you would over-write existing changes --
git fetch
git reset --hard HEAD
git merge origin/$CURRENT_BRANCH
-- or --
git mergin @{u}


git checkout -- path/to/file
    - If you can't switch branches due to uncommitted work or you simply want to discard changes that don't need to be staged in Git
    - Use the command to reset individual files. For example, git checkout -- index.html would reset index.html to its most recent commit.

-- This is how you would pull new stuff and keep existing changes --
git fetch
git stash
git merge '@{u}'
git stash pop

git branch
    - displays all the branches in the repository
    - Also highlights the branch you are on
    - In Git, branches are usually a means to an end. You create them to work on a new project feature, but the end goal is to merge that feature into the master branch. After the branch has been integrated into master, it has served its purpose and can be deleted.

git branch <BRANCH NAME>
    - creates a new branch

git checkout <BRANCH NAME>
    - switch to a different branch

git checkout -b <BRANCH NAME>
    - creates new branch and...
    - moves the checked out branch to the new branch

**VIM is not a part of git; it is a text editor within the command line**
    - if you end up in VIM, to get out do the following:
        - To enter command mode in VIM, type :
        - To quit, type q
        - Press ENTER
        - Or you can enter SHIFT + Z + Z

*** ---  Features, Branches, and Merging back --- ***
The UCB workflow does teach to merge branchs back to previous branches
and to push each merged branch back to the origin:

Starting on the branch: feature/a_feature
    - git add -A
    - git commit -m "<your message here">
    - git push origin feature/a_feature
Switch to branch: develop
    - git checkout develop
    - git merge feature/a_feature
    - git push origin develop
Switch to the branch: master
    - git checkout master
    - git merge develop
    - git push origin master

git init
    - Only establishes a local folder as a Git repository.  The repository doesn't exist on GiHub Yet.

git remote add origin <repository URL>
    -Links the local folder to your GitHub repository
    -example of <repository URL> = git@gist.github.com:a4a006c4cead41c544b5ff9a4dba0785.git

git remote -v
    - Tells you what the remote repository is

git branch
    -Tells you what branch you are currently on

git branch <newBranchName>
    - creates a new branch
    - branch names cannot contain white spaces

git branch -d <branchname>
    - this deletes a branch from your local repository

git rm -r --cached node_modules
    Create the .gitignore file during the initial setup of the project to avoid accidentally tracking
    the folder with the git add -A command. If the node_modules folder was accidentally tracked by git,
    use the following (above) command to remove the tracking...replace node-modules with a
    file or sub-directory name

git remote set-url origin <GIT URL>
    change the origin; use this when cloning some code then pushing to your own repository

git remote rm <remote-name>
    use this to remove the remote repository reference from current local repo
    for <remote-name> typically you would enter 'origin'

git diff <filename>
    outputs the differences between <filename> in the staging area vs the working version

git reset <commit_SHA>
    This command works by using the first 7 characters of the SHA of a previous commit      

Three different ways to backtrack in Git.
** HEAD is  the most recent commit **
(1) git checkout HEAD <filename>
(2) git reset HEAD <filename>
(3) git reset <commit_SHA>

git log
    outputs list of commits for current directory
git log --oneline 
    shows the list of commits in one line format.
git log --oneline --graph - --graph
    Displays a visual representation of how the branches and commits were created in order to help you make sense of your repository history
git log --pretty=format:"%h %s" --graph


git commit --amend
git commit --amend --no-edit
    Allows for no change to the comment on commit you are ammending

Will need to learn more about config, but this might be a good place to start
git config --global alias.co "checkout"
git config --global alias.br "branch"
git config --global alias.glop "log --pretty=format:"%h %s" --graph"

GitHub Pages:
    - https://pages.github.com

.ignore
    - https://github.com/github/gitignore
    - https://git-scm.com/docs/gitignore

Forking a repository
    -  add upstream add connectivity back to original repository to allow updates to original code base to be pulled through
    - example: git clone <REPOSITORY>
    - git remote add upstream <REPOSITORY SSH stuff>
    - git fetch upstream
        this will update forked repository with changes in upstream repo