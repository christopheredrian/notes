This is my personal cheat sheet on git
=========================================

| Command                    | Description | 
|---------                   |-------------| 
| git init                   | Initialize repository|
| git status                 | Current              |
| git add _filename_         | Add _filename_ to **Staging** | 
| git add **'*.txt'**        | Can also be a wildcard | 
| git commit -m "Add file to repo" | Commit the changes currently on staging|
| git log                    | View all commited changes
| git remote add **origin** **url.git** | Adds a remote | To be able push our local repo to the GitHub we add a remote repository |
| git push -u origin master | Push local changes to our **origin** repo|
| git push | Above the **-u** tells git to remember parameters so we can just use **git push**|
| git pull origin master | Pulls down any changes from the remote repository |
| git diff HEAD | To look at the difference between the last commit |
| git diff --staged | To see changes you **just** staged | 
| git reset notes/todo.txt | To unstage the file |
| git reset | Unstaged all |
| git checkout -- todo.txt | Get rid of changes since last commit of todo.txt |
| git branch _cleanUp_ | Create a new branch |
| git checkout _cleanUp_| Switch branch|
| git rm '*.txt' | Removes and Stages all txt files |
| git commit -m "Removed all .txt files "| After above a commit is needed| 
| git checkout master | Going back to our master branch |
| git merge _cleanUp_ | Merge changes from _cleanUp_ into the master branch |
| git branch -d _cleanUp_ | Deletes the _cleanUp_ branch|
| git push | We can ommit the params if we used `git push -u origin master` before  | 
