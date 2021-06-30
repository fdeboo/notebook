# git

[Ofiicial Docs][git-docs]

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

Initialise as a git repository:

```sh
git init
```

Add file (name) to Staging Area:

```sh
git add list.txt
```

Add all updated files to Staging Area:

```sh
git add -A
```

Creates a local clone of an existing repository including all files and git history of the project.:

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

<!-- Links -->

[git-docs]: https://git-scm.com/doc/
[github-docs-ssh]: https://docs.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
