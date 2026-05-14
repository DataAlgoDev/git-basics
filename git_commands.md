Git is a distributed version control system used for multi-team collaboration and parallel development. It uses a branching model to allow developers to work in isolated environments. Instead of just isolating files, Git tracks snapshots of the entire project history, enabling individuals to develop features, fix bugs, or experiment independently without affecting the 'Source of Truth' (the main branch) until their code is ready to be merged.
## Git Terms
* **Remote:** A repo URL pointing to a hosted Git server (GitHub/Bitbucket) that allows you to sync local code with a central version of the repo.
* **Fork:** - A copy of someone elses repository under your own account. Public repos are always forkable; private repos require owner permission.
* **Upstream:** The "Source of Truth." In forking, it refers to the original author's repository. In branching, it refers to the remote branch your local branch tracks.
* **Origin:** The default alias for the remote you directly push to. In a fork, `origin` is your copy; in a non-forked project, `origin` and the "Source of Truth" are the same thing.
* **Fork Point:** The specific commit where a branch diverged from its parent. Git uses this during a rebase to identify which unique commits belong to the current branch.
### Git data model
Git is a directed acyclic graph (DAG) of snapshots, where each "commit" is a permanent record of the entire project state linked to its parent history, rather than a simple list of file changes.

```
(feature) [ f1 ]---[ f2 ]---[ f3 ]          ┌────────┐
         /                    \             │  HEAD  │
[ m1 ]---[ m2 ]----------------[ m3 ]-------│ [ m4 ] │ (main)
           ^                    ^           └────────┘
       FORK POINT          MERGE COMMIT

                (Zooming into Node f2)
┌──────────────────────────────────────────────────────────┐
│                    COMMIT: 4a2b8c9                       │
├──────────────────────────────────────────────────────────┤
│ METADATA:                                                │
│  - Author: User Name                                     │
│  - Date:   14-05-2026                                    │
│  - Message: "Update API"                                 │
├──────────────────────────────────────────────────────────┤
│ POINTERS:                                                │
│  - Parent: [Hash of f1]                                  │
│  - Tree:   [Snapshot of root file directory]             │
└──────────────────────────────────────────────────────────┘
```

**Tree**: A directory listing that maps filenames and permissions to their corresponding Blobs or sub-directories.

**Blob**: A binary large object model is a storage object containing only the raw file data (snapshot of a file) and is identified by its hash and not name.

**Tag**: Tag is a permanent, human-readable alias for a specific commit mark some event or state like release or versioning.

**Commit**: A Commit is a node containg a permanent snapshot of the project that links a Root Tree (the files) and metadata (author/message) to its parent commits, creating a traceable chain of history.

**Branch**: Branch is a movable pointer created from a commit that automatically advances as new commits are added. This allows in isolating and tracking unique set of changes.

**main/master** :Main/Master is the default, primary branch that serves as the official "source of truth" for a project, typically holding the stable and production-ready code.

**Head**: HEAD is a special pointer that points to any commit in a branch, typically to the tip of a branch (called an attached head). If pointing to a specific commit its known as a detached head. Head is like a lense that shows the user the snapshot of the commit in real time. All the commits are written where at the point where the head is at.

**Attached head** : When new branch is created or when switches or checks out to a different branch head stays attached as it points to the tip of the branch.
```
git checkout <branch-name> or git switch <branch-name>
```
**Detached head** : Detached head occurs when we move to a specific commit. Any new commits added at this state will be temporary and will be orphaned once you switch to another branch
```
git checkout <commit-hash>
```
**Tip**: Tip is the latest commit of a branch

* reset
* Push, force, with lease
* fast forward
* Merge commit
* Rebase and merge
* Squash and merge
* reflog
* Worktree

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
*Force cleanup without showing details*

    git clean -df

### Git reset

*Soft resetting current branch head back to one last commits*

    git reset --soft HEAD~1

### Deleting branches

*Only allows removal of branch if that branch is already merged to master*

    git branch -d <branches name space seperated>
*Force delete even if it is not merged*

    git branch -D <branches name space seperated>

ith that detatched head id and then merge

### Git Ignore

To ignore any file that need not to be tracked by git, create .gitignore file and add the list of files to be ignored inside of it

*.pdf :  Ignores all files with pdf format

web-app/* : Ignores all files in the the folder including folder

