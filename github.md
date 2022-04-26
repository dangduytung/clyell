---
layout: page
title: "Github"
permalink: /github/
---

#### &#35; Tutorial
[https://backlog.com/git-tutorial/vn](https://backlog.com/git-tutorial/vn)

#### &#35; Status
~~~
git status
~~~

#### &#35; Branch
~~~
git branch                                                  # To see local branches
git branch -r                                               # To see remote branches
git branch -a                                               # To see all local and remote branches
git branch | grep \* | cut -d ' ' -f2
git branch [new-branch]                                     # Switch to a branch
git checkout --track origin/my-branch-name                  # Switch to the branch
git checkout -b [new-branch]                                # Create a branch
git checkout - [new-branch]                                 # Create a branch and checkout that branch
git cherry -v master                                        # Check commit history with current branch
git merge [branch]                                          # Merge master from other branch
git merge branch-name --no-commit --no-ff                   # Merge branch not yet commit
git diff [branch]                                           # Check changed between current state with other branch
git diff [branch] [file]
git branch -d [branch]                                      # Delete local branch
git push -d origin <branch-name>                            # To delete the remote branch
git fetch origin                                            # Get all branches
git pull                                                    # To get a list of all branches from the remote
~~~

#### &#35; Other
~~~
git rev-parse --show-toplevel                               # Get root folder
git rm $(git ls-files --deleted)                            # Delete local deleted file at repo
git clean -f                                                # Delete all files untrack     (-d : delete folder)
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

#### &#35; Find conflict
~~~
grep -H -r "<<<" *
grep -H -r ">>>" *
grep -H -r '^=======$' *
~~~

#### &#35; Show log
~~~
git log
git log -2                                                  # View 2 last committed
git log -p -2                                               # View 2 last committed and detail changed
git log --pretty=oneline [filename]
git log --follow -p -- [filename]
gitk [filename]                                             # Graphics interface
git blame [filename]                                        # Show revision and author each line
git gui blame [filename]
git whatchanged
git whatchanged origin/master -n 1                          # Show changes server and local
~~~

#### &#35; Diff change [remote-path] and [local-path] are the same
~~~
git fetch origin master
git ls-files . --ignored --exclude-standard --others        # List ignored files
git ls-files . --exclude-standard --others                  # List untracked files
git diff                                                    # Show file changed but not add
git diff --cached                                           # Show file changed and added
git diff --name-status
git diff origin/master -- [local-path]
git diff --name-only origin/master                          # Show all files changed between repo and local
git diff --name-only [commit_id1] [commit_id2]              # Show all files changed between two commit_id
git diff [commit_id1] [commit_id2]
git diff-tree -no-commit-id --name-only -r [commit_id]      # Show all files changed at commit_id
git show --pretty="format:" --name-only [commit_id]         # Show all files changed at commit_id
git show [commit_id]                                        # Show detail of one commit
git log --branches --not --remotes                          # Show messages committed and unpushed
git log origin/master..HEAD                                 # Show messages committed and unpushed
git diff origin/master..HEAD                                # Show detail files committed and unpushed
git diff --stat --cached origin/master                      # Show a list of files to be pushed
git diff --numstat origin/master                            # Show full file paths of the files will change
~~~

#### &#35; Patch
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

#### &#35; Config
~~~
git config --list (show list config)
git config --global user.name "username"
git config --global user.email "email"
~~~

#### &#35; Init github
~~~
echo "# angular" >> README.md
git init
~~~

#### &#35; Add Git version 2.x
~~~
git add [file]
git add .                                                   # new/modified/deleted files
git add -A                                                  # new/modified/deleted files
git add --ignore-removal                                    # new/modified files
git add -u                                                  # modified/deleted files
git remote add origin https://github.com/dangduytung/angular.git
~~~

#### &#35; Commit
~~~
git commit -m "message"
git commit --amend -m "New commit mesage"                   # Change message of last commit
~~~

#### &#35; Push
~~~
git push origin master (git push -u origin master)
git push origin gh-pages
~~~

#### &#35; Revert (reset) changes to a file if they haven’t been committed yet:
~~~
git checkout -- <file>
git checkout <commit_hash> -- <file>  (to a specific revision)
~~~

#### &#35; Reset
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

#### &#35; Clone
~~~
git clone https://github.com/dangduytung/linux.git
git clone -b mybranch --single-branch git://sub.domain.com/repo.git   (one branch)
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

#### &#35; URL
~~~
git remote -v                                               # Show all remote urls
git remote -v | grep fetch | awk '{print $2}'
git remote show origin
git remote get-url origin
git config --get remote.origin.url
git remote set-url origin [url]                             # Change origin url (eg : https://github.com/USERNAME/REPOSITORY.git)
git remote add remote-name [url]                            # Add remote repo
~~~

#### &#35; Merge branch to master
~~~
git checkout master
git pull origin master
git merge [branch]   #gh-pages
git push origin master
~~~

#### &#35; Change master to gh-pages
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

#### &#35; Files
~~~
git rm [file1] [file2]
git mv file [file_old] [[file_new]]
git commit -m "deleting 2 files, renaming 1"
~~~

#### &#35; Help
~~~
git help [command]
~~~

#### &#35; Quick setup
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

#### &#35; Clear history github
~~~
-- Remove the history from  
rm -rf .git 
-- recreate the repos from the current content only 
git init 
git add . 
git commit -m "Initial commit" 
-- push to the github remote repos ensuring you overwrite history 
git remote add origin git@github.com:<YOUR ACCOUNT>/<YOUR REPOS>.git 
git push -u --force origin master
~~~