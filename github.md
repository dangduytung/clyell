---
layout: page
title: "Github"
permalink: /github/
---

## &#35; Tutorial
* [https://backlog.com/git-tutorial/vn](https://backlog.com/git-tutorial/vn)

## &#35; Main
~~~
git help [command]                                          # git [command] --help 
git status
~~~

### &#35; Config
~~~
git config --list (show list config)
git config --global user.name "username"
git config --global user.email "email"
~~~

### &#35; Clone
~~~
git clone https://github.com/dangduytung/linux.git
git clone -b mybranch --single-branch git://sub.domain.com/repo.git   (one branch)
~~~

### &#35; Submodule
~~~
git clone --recursive <repository>                          # If clone main repo, so add --recursive for get all submodules
git submodule add <repository> [<path>]                     # Add submodule (create file `.gitmodules`)
git submodule update                                        # Update submodule (If not exist, need add --init)
git submodule foreach git pull origin master                # Pull newest all submodules
git rm -rf [<sub-module>]                                   # Delete submodule at remote
rm -rf .git/modules/[<sub-module>]                          # Delete submodule at local
~~~

### &#35; Branch
~~~
git branch                                                  # Local branches
git branch | grep \*                                        # Current branch (git branch|grep "*")
git branch | grep \* | cut -d ' ' -f2                       # Current branch
git branch --show-current                                   # Current branch
cat .git/HEAD                                               # Current (active) branch
git branch -r                                               # Remote branches
git branch -a                                               # All local and remote branches
git branch [new-branch]                                     # Create branch without switching
git branch -m <new_branch>                                  # Rename your current local branch
git branch -m <old_branch> <new_branch>                     # Re-name other local branch

# Find the current git branch in detached HEAD state
git branch --contains HEAD
git branch --remote --contains
git branch --remote --contains | sed "s|[[:space:]]*origin/||"      

# Rename remote branch
git push origin :<old_branch> <new_branch>
git push --set-upstream origin <new_branch>

git branch -d [branch]                                      # Delete a local branch
git push -d origin [branch]                                 # Delete a remote branch
~~~
* [Guide delete branch](https://stackoverflow.com/a/23961231/2506126){:target="_blank"}

### &#35; Checkout
~~~
git checkout [<branch>]                                     # Switch to the branch
git checkout -b|-B <new-branch> [<start-point>]             # Create branch and switch to branch (start-point: commit, tag)
git checkout <commit>                                       # Checkout at commit and state is detached HEAD
git checkout -b [new-branch]                                
git checkout --track origin/[branch]                        # Switch to the branch
git checkout -- <file>                                      # Revert (reset) changes to a file if they haven’t been committed yet
git checkout <commit_hash> -- <file>                        # Revert (reset) changes to a file if they haven’t been committed yet (to a specific revision)
~~~

### &#35; Fetch
~~~
git fetch <remote>
git fetch origin master
~~~

### &#35; Pull
~~~
git pull                                                    # To get a list of all branches from the remote
git pull origin master
git pull origin <branch_name> --allow-unrelated-histories   # For error fatal: refusing to merge unrelated histories
git pull <remote>                                           # Like: git fetch origin/git merge origin .
git pull –no-commit                                         # Just pull and no create new merge commit
git pull –rebase                                            # Pull rebase
git pull –verbose                                           # Pull with show details
~~~

### &#35; Add
~~~
git add [file]
git add .                                                   # new/modified/deleted files
git add -A                                                  # new/modified/deleted files
git add --ignore-removal                                    # new/modified files
git add -u                                                  # modified/deleted files
git remote add origin https://github.com/dangduytung/angular.git
~~~

### &#35; Merge
~~~
git merge origin/master
git merge [branch]                                          # Merge master from other branch
git merge branch-name --no-commit --no-ff                   # Merge branch not yet commit

# Example merge branch to master
git checkout master
git merge [branch]                                          # Example: gh-pages
git push origin master
~~~

### &#35; Commit
~~~
git commit -m "message"
git commit --amend -m "New commit mesage"                   # Change message of last commit
~~~

### &#35; Push
~~~
git push origin master (git push -u origin master)
git push origin gh-pages
~~~

### &#35; File
~~~
git ls-files . --ignored --exclude-standard --others        # List ignored files
git ls-files . --exclude-standard --others                  # List untracked files

git ls-tree --full-name --name-only -r HEAD                 # List name all files of all folders
git ls-tree --full-name --name-only -r HEAD | head          # List name all files of first folder
git ls-tree --full-name --name-only -r HEAD | tail
git ls-tree -r HEAD | wc -l                                 # Get number of files
git ls-tree -l -r HEAD | awk '/^[^-]/ {s+=$4} END {print s}'    # Get total file size

git rm [file1] [file2]
git mv file [file_old] [[file_new]]
git commit -m "deleting 2 files, renaming 1"
git show --pretty="format:" --name-only [commit_id]         # Show all files changed at commit_id
git show [commit_id]                                        # Show detail of one commit
git cat-file -e <remote>:<filename>                         # Check a file exists in a remote
git cat-file -e origin/master:README && echo README exists
~~~

### &#35; Remote
~~~
git remote -v                                               # Show all remote urls
git remote -v | grep fetch | awk '{print $2}'
git remote show origin
git remote get-url origin
git config --get remote.origin.url
git remote set-url origin [url]                             # Change origin url (eg : https://github.com/USERNAME/REPOSITORY.git)
git remote add remote-name [url]                            # Add remote repo
~~~

### &#35; Log
~~~
git reflog                                                  # See recent actions
git log
git log -2                                                  # View 2 last committed
git log -p -2                                               # View 2 last committed and detail changed
git log --pretty=oneline [filename]
git log --follow -p -- [filename]
git log --oneline --graph                                   # To get commits SHA from your history
git log --oneline main..origin/main
git log --oneline origin/master
git log --branches --not --remotes                          # Show messages committed and unpushed
git log origin/master..HEAD                                 # Show messages committed and unpushed
gitk [filename]                                             # Graphics interface
git blame [filename]                                        # Show revision and author each line
git gui blame [filename]
git whatchanged
git whatchanged origin/master -n 1                          # Show changes server and local
~~~

### &#35; Diff
~~~
git diff                                                    # Show file changed but not add
git diff --cached                                           # Show file changed and added
git diff --name-status
git diff [remote-path] -- [local-path]                      # Diff change [remote-path] and [local-path] are the same
git diff origin/master..HEAD                                # Show detail files committed and unpushed
git diff origin/master -- [local-path]
git diff --name-only origin/master                          # Show all files changed between repo and local
git diff --name-only [commit_id1] [commit_id2]              # Show all files changed between two commit_id
git diff [commit_id1] [commit_id2]
git diff-tree -no-commit-id --name-only -r [commit_id]      # Show all files changed at commit_id
git diff --stat --cached origin/master                      # Show a list of files to be pushed
git diff --numstat origin/master                            # Show full file paths of the files will change
git diff [branch]                                           # Check changed between current state with other branch
git diff [branch] [file]
~~~

### &#35; Diff tools (Gui)
[http://meldmerge.org](http://meldmerge.org){:target="_blank"}
~~~
# Tool MELD
## Download at http://meldmerge.org
git mergetool --tool-help                                   # List tools
git difftool --tool-help
git config --global diff.tool meld
git config --global merge.tool meld
git config --global mergetool.meld.path "/c/Program Files (x86)/meld/meld.exe"      # For windows
git difftool --tool=meld [optional_filename]                # Command run GUI to view diff file
~~~

### &#35; Patch
~~~
git diff > path-issue-1.patch                               # Create patch
git add [patch] => git diff --staged > path-issue-2.patch   # Add a file and then create patch
git diff HEAD > patch-issue-2.patch                                    
git format-patch [commit_id]
git format-patch HEAD~2                                     # Create patch from 2 last committed
git format-patch origin/master                              # Create patch from all commits but not yet push
git format-patch --binary --full-index origin/master        # Create patch binary
git apply -v patch-name.patch                               # Apply patch
git am patch1.patch                                         # Apply patch by format-patch
patch < file.patch                                          # Apply patch not use git
~~~

### &#35; Reset
~~~
git reset [commit_id]
git commit -m "Revert to commit_id"
git reset --hard
git reset --soft HEAD@{1}
git reset --soft HEAD~1                                     # Undo commit last, keep changed at local
git reset --hard HEAD~1                                     # Undo commit last, don't keep changed at local
git reset --mixed HEAD~1                                    # Undo commit last, keep changed at index
git reset HEAD~1                                            # Undo commit last, keep changed at index
git reset origin/master                                     # Undo commits not yet push
git fetch origin                                            # Reset to status of remote
git reset --hard origin/master                              # Reset to status of remote 
~~~

### &#35; Find conflict
~~~
grep -H -r "<<<" *
grep -H -r ">>>" *
grep -H -r '^=======$' *
~~~

### &#35; Other
~~~
git rev-parse --show-toplevel                               # Get root folder
git rm $(git ls-files --deleted)                            # Delete local deleted file at repo
git clean -f                                                # Delete all files untrack (-d : delete folder)
git clean -n -f -d                                          # View files before delete
git reset HEAD [file]                                       # Unstage files
git describe --tags `git rev-list --tag --max-count=1`      # View last tag
git for-each-ref --sort=-committerdate refs/heads/ | head   # List branches last usaged
tar cJf project.tar.xz project/ --exclude-vcs               # Tar project except .git folder
git diff --name-only | xargs tar -cf project.tar -T -       # Tar all files which changed at local
git stash                                                           
git ls-tree HEAD                                            # Tree object
git cat-file –p [commit_id]
git grep "search"
git instaweb –httpd=webrick
git gc
git archive --format=tar master                             # Create file tar
git prune                                                   # Delete objects has not pointers
git fsck                                                    # Integrity check
~~~

#### &#35; Ignore
~~~
git update-index --assume-unchanged <path/to/file>
~~~

#### &#35; Undo ingnore
~~~
git update-index --no-assume-unchanged <path/to/file>
~~~

#### &#35; Delete folder
~~~
git rm -r [folder]  (git rm -r --cached [folder])
~~~

##### &#35; Change master to gh-pages
~~~
# Github's web hosting looks for a branch called "gh-pages"
# Git by names the default branch "master" so we need rename
# it to "gh-pages" so that Github can find the website files.

# In terminal/cmd
git checkout -b gh-pages                                    # Create a new branch called gh-pages
git push origin gh-pages                                    # Push the gh-pages repo to github

#git branch -D master
#git push --set-upstream origin gh-pages

# On Github
Settings (Repo settings) --> Branches --> Default Branch --> gh-pages --> Update

# In terminal/cmd
git push origin :master                                     # Delete the old branch    
~~~

##### &#35; Quick setup
~~~
# Create a new repository on the command line 
echo "# BTC" >> README.md 
git init 
git add README.md 
git commit -m "first commit" 
git branch -M main 
git remote add origin https://github.com/dangduytung/Repo.git 
git push -u origin main 

# Or push an existing repository from the command line 
git remote add origin https://github.com/dangduytung/Repo.git 
git branch -M main 
git push -u origin main
~~~

##### &#35; Clear history github
~~~
# Remove the history from  
rm -rf .git 
# Recreate the repos from the current content only 
git init 
git add . 
git commit -m "Initial commit" 
# Push to the github remote repos ensuring you overwrite history 
git remote add origin git@github.com:<YOUR ACCOUNT>/<YOUR REPOS>.git 
git push -u --force origin master
~~~