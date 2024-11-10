## Setup and Startup
---
*To initialize the selected folder as git working directory*
    
    git init 
*Rename master to main (As per new convention)*

    git branch -M main
*Shows status of working tree*

    git status
*Adding files to staging area (index file)*

    git add <file>

    git add .
*Create user config before commiting files*

    git config --global --list
    git config --global user.email "ajaynarayanan11@gmail.com"
    git config --global user.name "AjayN"


## Working with remote repository
---
*To Check remote directory/repo*

    git remote -v
*To add an repo Github as origin*

    git remote add origin https://github.com/<repo_name>.git
*Pulling an existing repo with unrelated commit history*
    
    git pull origin main --allow-unrelated-histories
*For pushing changes to remote repo (Shorthand)*
    
    git push -u origin main
*Or, below is also the same*

    git push --set-upstream origin main
*To remove master branch from origin if master was renamed to main and the main brach has been set Default in Github*

    git push origin --delete master
*To remove remote repo link with the local direcory*
    
    git remote remove origin

## Branching, Logs, Commits, Merge and more
---
### Commiting files (Adding files to object folder, or saving)
*Saves all the staged files(files that are being tracked in the index area)*

    git commit -m "<message>"
*Adds files to staging area if not already added and then commits the change*

    git commit -a -m "" : 

### Git logs

*To view commit history. (q to exit)*

    git log 
To see details about a specific commit, including what changes were made.

    git show 
    git show <id>
*To See last commit*

    git log -1

*View differences between commits:*

    git diff <commit-id1> <commit-id2>

*Shows all activity of the head with its hash value in the current working branch*

    git reflog

### Checkout / branching

*Switches to the branch at that time of commit*

    git checkout <commit id>

*Switches back to master branch*

    git checkout master
*To list all the branches*

    git branch -a
*To create new branch*

    git branch <branch-name>

*Create new branch and switch to that branch*

    git branch -b <branch-name>

### Merging a branch to another

*Switch to target branch to which it be merged*

    git checkout <target branch>
Name of the branch to be merged

    git merge <branch-name>

## Deleting files

To list the files present in staging alreadyi

    git ls-files
To remove file from direcory and staging already

    git rm <file-name>

### To revert the changes in staged files which was not commited

*To revert specific file*

    git checkout <file-name>
    git restore <file>
*To revert all the changes in file to last commit*

    git checkout .
    git restore .
**Note : If file was staged already then  do 'git checkout'**

### Tagging Releases

*Create a new tag*

    git tag -a v1.0 -m "Version 1.0"

*Push tags to remote*

    git push origin --tags

### Git cleanup

*Shows Cleans up details*

    git clean -dn 
Force cleanup without showing details

    git clean -df

### Git reset

Soft resetting current branch head back to one last commits

    git reset --soft HEAD~1

### Deleting branches

Only allows removal of branch if that branch is already merged to master

    git branch -d <branches name space seperated>
Force delete even if it is not merged

    git branch -D <branches name space seperated>

### Detatched head

*When you go to a specific previous commit id, head becomes a detached head.
To save the changes if switching to a different branch, create branch with that detatched head id and then merge*

### Git Ignore

To ignore any file that need not to be tracked by git, create .gitignore file and add the list of files to be ignored inside of it

*.pdf :  Ignores all files with pdf format

web-app/* : Ignores all files in the the folder including folder

