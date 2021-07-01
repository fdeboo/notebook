# git

[Official Docs][git-docs]

### Current Directory listing:

```sh
ls
```

### Change to directory (name):

```sh
cd Desktop
cd ..
```

### Make a new directory (name):

```sh
mkdir Shopping
```

### Change to directory (name):

```sh
cd Shopping
```

### Create a new file (name) in current directory:

```sh
touch list.txt
```

### Open file (name):

```sh
open list.txt
```

### Open file (name) in default code editor (example):

```sh
code list.txt
```

### List the files in .ssh directory (if they exist) / Check if existing keys are present:

```sh
ls -al ~/.ssh
```

### Generate a ssh key:

[Generating an ssh key for GitHub][github-docs-ssh]

```sh
ssh-keygen -t ed25519 -C “<email_address>”
```

> `-t` specifies the type of key to create. The possible values are `dsa`, `ecdsa`, `ed25519`, or `rsa`.

> `-C` Provides a new comment.

(Hit enter to save in default location)

(Enter a pass phrase twice to verify)

Start ssh-agent in the background:

```sh
eval “$(ssh-agent -s)”
```

Check if config file exists in the ssh agent:

```sh
open ~/.ssh/config
```

If not, create the file:

```sh
touch ~/.ssh/config
```

Open the file and add:

```sh
Host *
	AddKeysToAgent yes
	UseKeychain yes
	IdentifyFile ~/.ssh/id_ed25519
```

Add key to ssh agent:

```sh
ssh-add -K ~/.ssh/id_ed25519
```

Copy the SSH public key to clipboard:

```sh
pbcopy < ~/.ssh/id_ed25519.pub
```

Go to Github settings and SSH and GPG keys and add new SSH key

Give a Title and Paste the Key in the input containers

## Basic git commands

### Initialise as a git repository:

```sh
git init
```

### Add file (name) to Staging Area:

```sh
git add list.txt
```

### Add all updated files to Staging Area:

```sh
git add -A
```

### Creates a local clone of an existing repository including all files and git history of the project.:

```sh
git clone <url>
```

## Committing

> ### First forward merge
>
> The feature branch being merged back to the original branch (eg master) is several commits ahead while no commits have been made on the original branch since the split. The merge allows the original branch to catch back up with the latest commit.
>
> ### Merge commit
>
> When two branches are merged that both have changes on them since their split but none of the changes result in a conflict, a new commit is made with both branches as parents
>
> ### Merge Conflicts
>
> When two branches are merged that both have changes on them that conflict each other. Can be resolved in VSCode by opening up the affected file and choosing to accept changes from either file or both. THE RESOLVED FILE WILL THEN NEED TO RE-ADDED TO THE STAGING AREA AND COMMITTED.

### Commit staged files with message

(_Message should be written in present tense)_

```sh
git commit -m ‘create shopping list’
```

### Open editor tab to write a longer commit message with title and body:

```sh
git commit -a
```

### Combine add/commit

```sh
git commit -a -m ‘create shopping list’
```

### Configures git (globally) to trigger an editor in VSCode for writing longer commit messages:

```sh
git config --global core.editor "code —wait”
```

### List all commits with shortened snippets of the hash name instead of the full 40-byte hexadecimal unique reference:

```sh
git log —abbrev-commit
```

### A combination of git log —abbrev and —pretty. Display shortened snippets of the unique name hashes and one line summaries rather than commit messages in full:

```sh
git log —oneline
```

### Replace the previous commit with an amended commit (Opens previous commit in VSCode editor):

```sh
(git add <filename>)
git commit —amend
```

## Branching

### List all current branches in the repository (with summary information):

```sh
git branch -v
```

### Create a new named branch (no spaces in name):

```sh
git branch feature/chatbot
```

### Create branch (and switch to it at the same time):

```sh
git switch -c feature/chatbot
```

### Switch branches (name):

```sh
git checkout feature/chatbot
```

### Delete branch (name):

```sh
git branch -d feature/chatbot
```

### Delete branch (name):

```sh
git branch -d feature/chatbot
git branch -D feature/chatbot
```

### Rename / move branch (must be current branch):

```sh
git branch -m feature/messenger
```

### Merge a branch to current branch (HEAD):

```sh
git merge bugfix
```

## Comparing Changes

### List differences between unstaged changes in working directory and staging area:

```sh
git diff
```

### List all staged and unstaged changes in working directory since last commit (HEAD):

```sh
git diff HEAD
```

### List differences between only staged changes and last commit:

```sh
git diff —staged / git diff —cached
```

### As above with a filename specified:

```sh
git diff HEAD style/main.css
```

### Compare differences between the tips of 2 branches (oldest..newest):

```sh
git diff branch1..branch2
```

eg.

```sh
git diff master..develop
```

### Compare differences between 2 commits (using hash (oldest..newest):

```sh
git diff commit1..commit2
```

### Compare latest commit (HEAD) with previous commit:

```sh
git diff HEAD HEAD~1
```

## Stashing

> ### Stashing
>
> A method for storing uncommitted changes so that they can be returned to later without having to make unnecessary commits. Resolves attempts to switch from a branch with uncommitted changes to a branch which has conflicts.

### Stash all changes (staged and unstaged) and revert to working copy

```sh
git stash
```

### Remove the most recently stashed changes from stash and re-apply them to the working directory / staging area

```sh
git stash pop
```

### Remove the most recently stashed changes from stash and re-apply them to the working directory / staging area without removing from stash:

```sh
git stash apply
```

### View all stashes in stash list

```sh
git stash list
```

### Apply specified stash from stash:

```sh
git stash apply stash@{2}
```

### Remove specified stash from stash:

```sh
git stash drop stash@{2}
```

### Clear everything from stash:

```sh
git stash clear
```

## Undoing changes

### Go back in time and view a previous commit on the branch. (Can be used to create a copy of the state into a new branch)

```sh
git restore —source HEAD~2 <filename>

git checkout <commit-hash>
```

### Checkout the commit prior to the HEAD state:

```sh
git checkout HEAD~1
```

### Revert back to the last commit & discard any uncommitted changes (optional: filename)

```sh
git restore <filename>

git checkout HEAD <filename>
```

### Unstage files from staging area:

```sh
git restore —staged <filename>
```

### Reset repo back to a specified commit (hash) from commit history. Unstage any subsequent changes and preserve them in the working directory. Move playhead back:

```sh
git reset <commit-hash>
```

### Reset repo back to a specified commit (hash) from commit history. DOES NOT PRESERVE ANY WORK FROM SUBSEQUENT COMMITS:

```sh
git reset —hard <commit-hash>
```

### Revert repo to a specified commit (hash) from commit history via a new commit in the repo. Preserve all commits in the git history. Move playhead forward:

```sh
git revert <commit-hash>
```

### A record of when the tips of branches and other references were changed

```sh
reflog
```

> ### HEAD
>
> A pointer that refers to the current “location” in your repository. It points to a particular branch reference (such as playhead)

## Github

> ### Remote
>
> The destination that git can push code to

> ### Origin
>
> The default name for the remote destination

> ### Upstream (-u)
>
> Link connecting the local branch to a branch on GitHub.

### Check remote url:

```sh
git remote -v
```

### Add a remote:

```sh
git remote add origin <url>
```

### Rename master branch (eg. to main):

```sh
git branch -M main
```

### Push commits to GitHub:

```sh
git push <remote name> <branch name>
git push origin master
```

### Push commits to GitHub under a different branch name:

```sh
git push <remote name> <local branch>:<remote branch>
git push origin master:main
```

### Set the upstream so that the local branch can track the remote branch (and typing ‘git push’ automatically pushes to it):

```sh
git push <remote name> <local branch>:<remote branch>
```

### View state at the last point in time the local repo communicated with the remote repo / Github

```sh
git checkout origin/main
```

### View all remote branches

```sh
git branch -r
```

### View (named) remote branch in detached HEAD

eg.

```sh
git checkout origin/puppies
```

### Create a local branch from a remote branch of the same name

eg.

```sh
git switch puppies
```

### Download any updates made to a remote repo / remote branch without integrating them into working files:

```sh
git fetch
git fetch origin food
```

### Download any updates made to a remote repo and merge with current branch (may result in conflicts)

```sh
git pull
```

```sh
git pull <remote> <branch>
```

## Gitignore files

- (git)
- Config files containing Secret keys, API Keys, credentials
- Operating System files (.DS_Store on Mac)
- Log files
- Dependencies and packages
  eg.
- .DS_Store
  +folderName/
- \*.log

## Fork a repo

### Clone from forked repo to local

```sh
git clone <url>
```

### Set upstream to original (url)

```sh
git remote add upstream <url>
```

### Pull updates from original (url)

```sh
git pull upstream <url>
```

### Push (main branch) to forked repo

```sh
eg git push origin main
```

### Pull request to original project

(Via Github)

## Rebasing

> ### Rebasing
>
> A method that can be used for merging branches. Rebasing moves the entire feature branch so that it BEGINS at the tip of the master branch. Instead of using a merge commit, rebasing rewrites the commit history by creating new commits for each of the original feature branch commits.

> ### Interactive Rebasing
>
> Enter interactive mode which enables commits to be edited, removed

### Switch to feature branch

```sh
git switch feature
```

### Re-base on the master branch

```sh
git rebase master
```

> **WARNING!**
> Never rebase commits that have been shared with others.

### Re-base on the master branch (after solving conflicts)

```sh
git rebase —continue
```

### Interactively recreate previous commits

```sh
git rebase -i HEAD~4
```

### Include commit:

```sh
pick
```

### Squash to previous commit and lose commit message:

```sh
fixup
```

### Delete commit:

```sh
drop
```

### Rename commit:

```sh
reword
```

## Git Tags

> ### Tags
>
> Labels that refer to notable moments in time. Such as versioning for new releases v3.1.0

> ### Semantic Versioning
>
> The semantic versioning spec outlines a standardised versioning system for software releases. It provides a consistent way for developers to give meaning to their software releases.
>
> #### Example:
>
> **2.1.1**
>
> Major release . Minor release . Patch release

### View tag history:

```sh
git tag
```

### Checkout a tag:

```sh
git tag “<tagname>”
```

```sh
git checkout <tagname>
```

### View changes between 2 tags:

```sh
git diff <tagname1> <tagname2>
```

### Create a basic lightweight tag:

```sh
git tag <tagname>
```

### Create an annotated tag:

```sh
git tag -a <tagname>
```

```sh
git tag -am <tagname>
```

### View tag metadata:

```sh
git show <tagname>
```

### Rename a tag on a previous commit:

```sh
git tag <new_name> <commit_hash>
```

### Switch a tag to a different commit:

```sh
git tag <tag name> <commit_hash> -f
```

### Delete a tag:

```sh
git tag -d <tag name>
```

### Push a tag to Github:

```sh
git push <origin> <tagname>
```

### Push all tags to Github:

```sh
git push <origin> —tags
```

```sh
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

<!-- Links -->

[git-docs]: https://git-scm.com/doc/
[github-docs-ssh]: https://docs.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
