# Setup
Set credential
```bash 
git config --global user.name <name>
git config --global user.email <email>
```

For Windows set core.autocrlf to "true". 
For Mac / Linux set core.autocrlf to "input".
```bash
git config --global core.autocrlf true
git config --global core.autocrlf input
```

### Optional for VSCode users
Set VSCode as default editor.
```bash
git config --global core.editor "code --wait"
```

Set VSCode as default merge tool.
```bash
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd 'code --wait $MERGED'
```

Set VSCode as default diff tool.
```bash
git config --global diff.tool vscode
git config --global difftool.vscode.cmd 'code --wait --diff $LOCAL $REMOTE'
```

# Usefull comands 
Open global config file

```bash
git config --global -e
```

Alias 'git checkout' with 'git co'
```bash
git config --global alias.co checkout
```
but rather use newer `git switch`.


## Clone git repository

Make sure to use the SSH link and not the HTTPS one
```bash
git clone git@github.com:<link_to_the_repo>
```

To switch to SSH from HTTPS use (after cloning with the HTTPS link)
```bash
git remote set-url origin git@github.com:<link_to_the_repo>
```

## Checking local repository status
Check uncomitted changes made to code
```bash
git status
```
Short version
```bash
git status -s
```
## Comitting changes
After implementing complete working piece of code(function, fix, feature) you should add changes to staging area

This adds ALL unignored files in the project, be carefull with this. 
```bash
git add -A
```
Other optin is to use 
```bash
git add <relative_path_to_file>
```
This will only add the chosen files.


Then commit changes from the staging area with a short message
```bash
git commit -m "Desription"
```
You can change message of LAST commit by using '--amend' flag
```bash
git commit --amend -m "New description"
```

You can also add more changes to LAST commit without creating new one
(like last minute fixes)
```bash
git add -A
git commit --amend -m "New description"
```

# Handling branches
List all LOCAL branches
```bash
git branch
```

List all REMOTE branches
```bash
git branch -r
```

List all LOCAL and REMOTE branches
```bash
git branch -a
```

List additional info with each branch (such as last commit)
```bash
git branch -v
```

Create new branch
```bash
git branch branch_name
```

Switch to branch
```bash
git switch branch_name
```

Create new branch and immediately switch to it
```bash
git switch -c branch_name
```

Delete all unstaged and uncommited changes
```bash
git restore :/
```

Download up to date state of repository without overwriting anything (Useful for downloading remote branches from other people)
```bash
git fetch
```
Fetch and merge into current branch (works only with no unstaged and uncomitted changes)
```bash
git pull
```

When pushing new branch to repo for the FIRST time (always call this with the desired branch checked out) (remote_branch_name should be same as current branch name)
```bash
git push -u origin <remote_branch_name>
```
All subsequent pushes from the same branch
```bash
git push
```

## Deleting branches

To delete a branch first switch to main
```bash
git switch main
```

Then delete the remote version of it
```bash
git push origin -d branch_name
```
Then delete local version of it
```bash
git branch -d branch_name
```

## Using stahes to save code changes
To save and revert unstaged and uncomitted changes in tracked files into stash
```bash
git stash
```
To also save changes in newly added files which were never staged before
```bash
git stash -u
```
Created stash will have index 0, all other stashes will have their index incremented by 1


List all current stahes
```bash
git stash list
```
This lists all stashes and their names
For example stash name can be 'stash@{2}' for second newest stash, 'stash@{0}' for newest stash etc. Stash index can also be used instead of the name, like '2' or  '0'

Put back changes that were stashed last (stash index 0)
```bash
git stash apply
```
Or for specific stash
```bash
git stash apply stash_name
```

Put back changes that were stashed last (stash index 0) and delete the stash
```bash
git stash pop
```
Or for specific stash
```bash
git stash pop stash_name
```

To just delete a stash
``` bash
git stash drop stash_name
```

To delete all stashes
```bash
git stash clear
```

## Process for updating a branch from new changes from repository 
If you have some changes, delete or stash them
```bash 
git restore :/
```
or
```bash
git stash
```

If you're not in main branch switch to it
``` bash
git switch main
```

Fetch and merge into main branch
```bash
git pull
```

Switch to the branch which should be updated from main
```bash
git switch branch_name
```

Merge updated main branch into your branch
```bash
git merge main
```

Merge conflicts will open in editor, resolve them then stage all resolved merge conflicts
```bash
git add -A
```

Finish the merge
```bash
git merge --continue
```

Merge message will open up, close it. Merge is now done, optionally do 
```bash
git push origin branch_name
```
to update your branch on GitHub.


