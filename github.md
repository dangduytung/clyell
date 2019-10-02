---
layout: page
title: "Github"
permalink: /github/
---

// Status
~~~
git status
~~~

// Check branch
~~~
git branch
git branch | grep \* | cut -d ' ' -f2
~~~

// Show log
~~~
git log --pretty=oneline
git whatchanged
~~~

// Diff change [remote-path] and [local-path] are the same
~~~
git fetch origin master
git diff origin/master -- [local-path]
git diff --name-status
git diff [log1] [log2]
~~~

// Config
~~~
git config --list (show list config)
git config --global user.name "username"
git config --global user.email "email"
~~~

// Init github
~~~
echo "# angular" >> README.md
git init
~~~

// Add
~~~
git add [file]
git add . (add all files)
git remote add origin https://github.com/dangduytung/angular.git
~~~

// Commit
~~~
git commit -m "message"
~~~

// Push
~~~
git push origin master (git push -u origin master)
git push origin gh-pages
~~~

// Ignore
~~~
git update-index --assume-unchanged <path/to/file>
~~~

// Undo ingnore
~~~
git update-index --no-assume-unchanged <path/to/file>
~~~

// Delete folder
~~~
git rm -r [folder]  (git rm -r --cached [folder])
~~~