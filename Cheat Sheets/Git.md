# Git
[YouTube tutorial on Git and Github usage](https://youtu.be/RGOj5yH7evk)

## [Conventional commits](https://www.conventionalcommits.org/)


## Set global variables
`git config --global user.name "2Cheetah"`
`git config --global user.email "fckninja@gmail.com"`
`git config --global color.ui auto`

## Check configuration
`git config --list`

## Initialize a repository in the current directory
`git init`

## Clone a remote repository in the current directory
`git clone <URL or path to remote repository> .`

## Check status of the repository
`git status`

## Check merged status
`git branch --merged`

## Check all the branches together - local and remote
`git branch -a`

## General workflow to add features or work out bugs
1. Clone a repository to the local machine
`git clone <repo path> .`
2. Fork the master branch of local repo
`git branch feature_1`
3. Switch to the created repo
`git checkout feature_1`
4. Do the work with the code and commit the changes
`git add -A`
or
`git add .`
`git commit -m "Some meaningful message, describing the work done"`
5. Push the forked branch to the remote repo
`git push -u origin feature_1`
`-u` creates a link between origin and feature_1, that means that next time to push changes from feature_1 to origin it will be needed only type `git push`
6. Pull changes from remote repo to master local repo
`git checkout master`
`git pull origin master`
7. Merge feature_1 branch with master locally
`git merge feature_1`
8. Merge local master branch to remote master branch
`git push origin master`
In case there's an error, it's needed to checkout from remote master branch to another remote branch, e.g. feature_1 branch on remote repo, then go to local repo and repeat git push origin master
9. Remove feature_1 branch locally
`git branch -d feature_1`
10. Remove feature_1 branch remotely
`git push origin --delete feature_1`

## Add remote repo to the current local project. It's needed first to create empty repo on Github
`git remote add origin PATH_TO_REMOTE_REPO`

## Check connected remote repo
`git remote -v`

## Check differences between a master branch and the forked branch
`git diff NAME_OF_BRANCH_TO_COMPARE`

## You can check implemented changes with before committing them with just:
`git diff`

## Create a branch and check it out
`git checkout -b feature`

## Go one commit before
`git reset HEAD~1`

## Go to a specific commit. First it's needed to get a hash of the commit with command
`git log`

Oneliner:
```bash
git log --oneline
```

## Then with the hash it's needed to use the command
`git reset HASH`

## Restore

### From staged state

```bash
nvim README.md
git add README.md
git status
git restore --staged README.md
or
git restore -S README.md
```

### To initial state (the file changed, but is not staged)

```bash
nvim README.md
git status
git restore README.md
```

To restore the folder to the initial state:
```bash
git restore .
```

## .gitignore

Example of its content:
```text
.DS_Store
.vscode/
authentication.js
node_modules
notes/
**/*-todo.md
```

In case `.gitignore` file added after files which are to be excluded from tracking, cache must be cleared:
```bash
git rm -r --cached .
```

### Global Ignore File

```bash
git config --global core.excludesfile [file]
```

## Deleting and Renaming files

```bash
git rm README.md
```

With the removing of the `README.md` file from the folder the command as well adds changes to staging area.

In case a file is renamed, git understands it as remove of initial file and creation of new one. To revert back renaming operation:
```bash
mv README.md README.txt
git restore README.md
rm README.txt
```

Renaming can be done with `git` help:
```bash
git mv README.md README.txt
git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	renamed:    README.md -> README.txt
```

To restore that changes:
```bash
git mv README.txt README.md
```

## Check differences

```bash
git diff
```

To check difference with some exact commit:
```bash
git log --oneline
# 226b46e (HEAD -> main, origin/main, origin/HEAD) Update NOTICE
# 1c64340 Update README.md
# bd107b0 (tag: start) Changes to README
# e32b1f9 Initial commit
git diff bd107b0
```

## Amending

To add a file to a commit after changes were already commited:
```bash
nvim README.md
git add README.md
git commit -m "README.md"
nvim README.md
nvim LICENSE
git commit --amend --no-edit
# or with new commit message
git commit --amend
```

