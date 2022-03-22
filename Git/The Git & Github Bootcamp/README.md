## Udemy - Git&Github course
회사에서 소스트리를 이용하는데 터미널환경 및 깃을 이해하기 위해 공부하기 시작  
유데미의 깃 강의를 바탕으로 정리중  

</br>

## Paste in Git Bash
shift + insert


## Configure

Notes |	Git commands
------|-------------------
Configure the author name to be used with your commits | `git config --global user.name "Sam Smith"`
Configure the email address to be used with your commits | `git config --global user.email sam@example.com`
Configure gitignore global | `git config --global core.excludesfile "~/.gitignore_global"`

## Init

Notes |	Git commands
------|-------------------
Create a new local repository | `git init`

## Clone

Notes |	Git commands
------|-------------------
Create a working copy of a local repository | `git clone /path/to/repository`
For a remote server | `git clone username@host:/path/to/repository`

## Status

Notes |	Git commands
------|-------------------
List the files you've changed and those you still need to add or commit | `git status`

## Add to staging (index)

Notes |	Git commands
------|-------------------
Add one files to staging (index) | `git add <filename>`
Add more files to staging  | `git add .`

## Commit

Notes |	Git commands
------|-------------------
Commit changes to head (but not yet to the remote repository) | `git commit -m "Commit message"`
Commit any files you've added with git add, and also commit any files you've changed since then	| `git commit -a`

## Remote repository

Notes |	Git commands
------|-------------------
Connect to a remote repository | `git remote add origin <server>`
List all currently configured remote repositories | `git remote -v`

## Checkout

Notes |	Git commands
------|-------------------
Create a new branch and switch to it | `git checkout -b <branchname>`
Switch from one branch to another | `git checkout <branchname>`

## Branches

Notes |	Git commands
------|-------------------
List all the branches in your repo, and also tell you what branch you're currently in | `git branch`
List all the branches in remote | `git branch -a`
Delete the feature branch	| `git branch -d <branchname>`
Delete remote branch | `git push -d <remote_name> <branch_name>`
Delete branche merged | `git branch --merged | egrep -v "(^\*|master|develop|main)" | xargs git branch -d`

## Push

Notes |	Git commands
------|-------------------
Send changes to the master branch of your remote repository | `git push origin master`
Push the branch to your remote repository, so others can use it:	| `git push origin <branchname>`
Delete a branch on your remote repository | `git push origin <branchname>`
Push all branches to your remote repository | `git push --all origin`
Push all tags to remote repository | `git push --tags origin`

## Pull

Notes |	Git commands
------|-------------------
Update from the remote repository	Fetch and merge changes on the remote server to your working directory | `git pull`

## Update local repository
Notes | Git commands
------|-------------------
Update | `git remote prune origin`

## Merge

Notes |	Git commands
------|-------------------
To merge a different branch into your active branch | `git merge <branchname>`

## Different

Notes |	Git commands
------|-------------------
View all the merge conflicts | `git diff`
View the conflicts against the base file | `git diff --base <filename>`
Preview changes, before merging | `git diff <sourcebranch> <targetbranch>`

## Tags

Notes |	Git commands
------|-------------------
Tags	You can use tagging to mark a significant changeset, such as a release | `git tag 1.0.0 <commitID>``

## Log

Notes |	Git commands
------|-------------------
CommitId is the leading characters of the changeset ID, up to 10, but must be unique | `git log`

## Undo changes

Notes |	Git commands
------|-------------------
Undo local changes. You can replace the changes in your working tree with the last content in head | `git checkout -- <filename>`
Instead, to drop all your local changes and commits, fetch the latest history from the server and point your local master branch at it, do this |  `git reset --hard origin/master`
Remove the last commit keeping changes | `git reset HEAD~1`

## Stash

Notes |	Git commands
------|-------------------
Stash list | `git stash list`
List the changes in <stash> | `git stash show <stash>` 
Save working directory and index state | `git stash`
Apply the changes in branch actual | `git stash (pop/apply) <stash>`
Drop the stash | `git stash drop <stash>`
  
  
## Alias
```
git config --global alias.s status
git config --global alias.ch checkout
git config --global alias.co commit
git config --global alias.a add
git config --global alias.l "log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all"
