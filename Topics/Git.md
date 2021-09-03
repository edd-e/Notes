# Git<!-- omit in toc -->

An open source distributed version control system.

## Table of contents<!-- omit in toc -->

- [Official website](#official-website)
- [Help](#help)
- [Setting up git with visual studio code](#setting-up-git-with-visual-studio-code)
  - [Git configuration](#git-configuration)
  - [VSCode configuration](#vscode-configuration)
- [Initializing git repositories](#initializing-git-repositories)
- [Staging files](#staging-files)
- [Committing changes](#committing-changes)
- [Git ignore](#git-ignore)
- [History](#history)
- [Alias](#alias)
- [Diff](#diff)
- [Reverting changes](#reverting-changes)
- [Renaming or deleting files](#renaming-or-deleting-files)
- [Branching](#branching)
- [Merging branches](#merging-branches)
  - [Fast-forward merge](#fast-forward-merge)
  - [Automatic merge](#automatic-merge)
  - [Manual merge](#manual-merge)
- [Tags](#tags)
- [Stashing](#stashing)
- [GitHub (remote repositories)](#github-remote-repositories)
  - [Linking repositories](#linking-repositories)
  - [Pushing changes](#pushing-changes)
  - [Fetch and pull](#fetch-and-pull)
  - [Cloning remote repositories](#cloning-remote-repositories)
  - [Updating the remote reference](#updating-the-remote-reference)

## Official website

For more information see: <https://git-scm.com>.

## Help

To open the git manual use the git help command:

```sh
git help config
```

To open a short list of help options use `-h`:

```sh
git init -h
```

## Setting up git with visual studio code

### Git configuration

Make sure Git is installed:

```sh
git --version
```

Set your user credentials:

```sh
git config --global user.name "My Name"
git config --global user.email mail@example.com
```

### VSCode configuration

Configure the default text editor (vscode for macOS):

```sh
git config --global core.editor "code --wait"
```

Test the editor by running this command to open your `.gitconfig` file:

```sh
git config --global -e
```

To set vscode as the default diff and merge tool the `.gitconfig` should look like this:

```text
[user]
    name = My Name
    email = mail@example.com
[core]
    editor = code --wait
[diff]
    tool = default-difftool
[difftool "default-difftool"]
    cmd = code --wait --diff $LOCAL $REMOTE
[merge]
    tool = vscode
[mergetool "vscode"]
    cmd = code --wait $MERGED
```

To see a list of all your modifications use this command:

```sh
git config --global --list
```

## Initializing git repositories

To initialize a repository in an existing project, use this command in the root level folder:

```sh
git init
```

To create a new project and initialize a repository in that folder use:

```sh
git init NewProjectName
```

## Staging files

A git repository saves commits (snapshots) of files in a working directory. Each file can be in one of two states; tracked or untracked. Git will only save tracked files into the repository and ignore any untracked files. Furthermore, tracked files can be unmodified or modified (from the last commit).

To check the status of all files in the repository use the `status` command:

```sh
git status
```

To begin tracking a file, use the `add` command:

```sh
git add someFile.txt
```

To track everything in the directory use:

```sh
git add .
```

Before any commit, all pending changes (modified tracked files) must be added to the git staging area using the `add` command.

To stage all tracked files that have been modified use:

```sh
git add -u
```

To stage everything use:

```sh
git add -A
```

## Committing changes

To commit, use the command:

```sh
git commit
```

This command launches the default text editor configured for git. Write a message and save the file to finalize the commit.

Commit messages can also be specified in-line:

```sh
git commit -m "A commit message."
```

You can also stage and commit files at the same time, this command will stage modified files and commit at the same time, while ignoring any new and/or modified untracked files:

```sh
git commit -am "A commit message."
```

## Git ignore

Files and folders that git should ignore may be specified in a `.gitignore` file. These files remain untracked by git and are not included in the repository. Sample contents of `.gitignore`:

```text
# This is a sample comment.

# To ignore all log files:

*.log

# To ignore a specific file:

testData.csv
```

## History

To bring up the list of all commits to the repository use the log command:

```sh
git log
```

To see a graph of the commit history and brach structure, use:

```sh
git log --oneline --graph --decorate --all
```

## Alias

To save a specific commands under an alias name, such as `hist` as an alias of the log command above, use:

```sh
git config --global alias.hist "log --oneline --graph --decorate --all"
```

Call the alias to execute the original command:

```sh
git hist
```

Additional flags and parameters can be added as if the full command was typed. For example; to only list the last 5 commits:

```sh
git hist -5
```

## Diff

The diff command shows what changed relative to another commit or branch:

```sh
git diff
```

You can also use the show command to see a diff summary of the last commit:

```sh
git show
```

To compare differences between previous commits, branches, or with the current changes (use the special marker `HEAD`) use the `diff` command:

```sh
git diff someCommitID HEAD
```

The can replace `diff` with `difftool` to compare the changes inside the pre-configured diff tool (vscode):

```sh
git difftool someCommitID anotherCommitID
```

## Reverting changes

To unstage a modified file use:

```sh
git reset HEAD someFile.txt
```

To restore the unstaged file to the previous commit use:

```sh
git checkout someFile.txt
```

## Renaming or deleting files

To rename a file use:

```sh
git mv someFile.txt newName.txt
```

To move a file into a subdirectory use:

```sh
git mv someFile.txt NewFolder
```

To delete a file use:

```sh
git rm someFile.txt
```

For any files that are updated or removed outside of git, remember to stage the changes.

## Branching

A branch can represent an independent line of development. In git, branch names are like labels. Creating a branch will label commits and deleting a branch removes the label only.

The default branch is the master branch.

To see a list of all the branch names in the repository use:

```sh
git branch
```

To create a new branch use:

```sh
git branch newBranch
```

To delete or rename a branch use `-d` or `-m` respectively:

```sh
git branch  -d someBranch
```

To switch to another branch use:

```sh
git checkout newBranch
```

To create a new branch and switch to it immediately use:

```sh
git checkout -b newBranch
```

## Merging branches

Merging lets you integrate independent branches into a single branch. There are three types of merging:

### Fast-forward merge

A fast-forward merge occurs when an independent branch is merged back to a main, or master, branch where no changes were made, e.g., as if the branching never happened.

### Automatic merge

An automatic merge is possible when merging branches where all modifications are non-conflicting.

### Manual merge

When automatic merge is not possible, git enters the manual merge state and conflicting modifications must be manually resolved before continuing.

If you were working on some branch and you wanted to merge it into master, use `checkout` to return to master:

```sh
git checkout master
```

Use the `merge` command to merge the current branch and `someBranch`:

```sh
git merge someBranch
```

After a successful merge, `someBranch` will still exist. To delete the branch use:

```sh
git branch -d someBranch
```

## Tags

Tags allow users mark specific points in the repository. There are lightweight tags and annotated tags.

A lightweight tag is just a label added to a specific commit:

```sh
git tag someTagTitle
```

An annotated tags contain a title and message, as well as the taggers name, email, and date:

```sh
git tag -a someTagTitle -m "A tag message here"
```

## Stashing

Stashing is a method of temporarily suspending the current modifications by saving them for a later time.

```sh
git status
git stash
```

At this point you could checkout another branch and work on something else.

To return to the stash, there are two options to finalize the changes:

The `apply` command takes the stashed changes and applies them to the current working directory leaving the stash in tact:

```sh
git stash apply
```

The `pop` command does the same thing but permanently deletes the stash:

```sh
git stash pop
```

## GitHub (remote repositories)

### Linking repositories

To add a local repository to GitHub, create a new repository on GitHub. When creating the repository be careful not to initialize it with any content, such as; README, license, gitignore, or other files. Find and copy the repository's URL, which is given during initialization or can be found in the repository's page.

To check if a local repository has any remote connections use the `remote` command:

```sh
git remote -v
```

To link the local repository to the new GitHub repository, use the `add` command:

```sh
git remote add origin URL
```

By convention, the name `origin` refers to the remote repository hosted on GitHub.

### Pushing changes

To publish the local repository to the remote repository use the `push` command.

```sh
git push -u origin master --tags
```

The `-u` establishes the tracking branch relationship between the local and remote repositories. The `-u` will no longer be required for future pushes. The optional `--tags` flag is used to send all tags to the remote repository.

To push commits on a new branch specify the branch name instead:

```sh
git push -u origin branchName
```

The default `git push` shorthand behavior, "simple", is to only push the current branch to the remote. The alternative is "matching", where git will push all branches that already exist on the remote with the same name. To set the default behavior to simple run this command:

```sh
git config --global push.default simple
```

### Fetch and pull

When the remote repository is updated, the local repository will need to synchronize. The `fetch` command brings in any changes from the remote and you can then merge the changes with the local repository. Alternatively, you can use the `pull` command, a pull executes both fetch and merge.

```sh
git pull
```

In practice, be sure to pull or fetch before pushing when working with active repositories.

### Cloning remote repositories

To clone a GitHub repository, use the `clone` command:

```sh
git clone URL folderName
```

The clone command will download a repository at the specified URL into a new folder in the current directory. If `folderName` is not specified the new folder is named after the repository by default. When cloning a repository, git automatically sets up `origin` to be the name of the remote reference.

### Updating the remote reference

If the remote repository is moved or renamed, you can update the local repository's remote reference with:

```sh
git remote set-url origin newURL
```
