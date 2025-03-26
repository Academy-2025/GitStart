# Git Cheatsheet

## Setup and Configuration

```bash
# Set username and email
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Check configuration
git config --list

# Set default editor
git config --global core.editor "code --wait"  # VS Code example
```

## Repository Setup

```bash
# Initialize new repository
git init

# Clone existing repository
git clone <repository-url>

# Clone repository to specific folder
git clone <repository-url> <directory>
```

## Basic Operations

```bash
# Check status of working directory
git status

# Add files to staging area
git add <file>         # Add specific file
git add .              # Add all files
git add *.js           # Add all JavaScript files
git add -p             # Add files interactively (in patches)

# Commit changes
git commit -m "Commit message"
git commit -am "Commit message"  # Add and commit in one step (tracked files only)

# View commit history
git log                # Full log
git log --oneline      # Compact view
git log --graph        # Visual representation of branches
```

## Branching and Merging

```bash
# List branches
git branch             # Local branches
git branch -r          # Remote branches
git branch -a          # All branches

# Create branch
git branch <branch-name>
git checkout -b <branch-name>  # Create and switch to new branch

# Switch branches
git checkout <branch-name>
git switch <branch-name>       # Modern alternative

# Merge branches
git merge <branch-name>        # Merge specified branch into current branch

# Delete branch
git branch -d <branch-name>    # Safe delete (won't delete unmerged branch)
git branch -D <branch-name>    # Force delete

# Rename branch
git branch -m <new-branch-name>  # Rename current branch
```

## Remote Repositories

```bash
# List remotes
git remote -v

# Add remote
git remote add <name> <url>

# Remove remote
git remote remove <name>

# Fetch changes from remote
git fetch                      # All remotes
git fetch <remote-name>        # Specific remote

# Pull changes (fetch + merge)
git pull
git pull <remote> <branch>

# Push changes
git push <remote> <branch>
git push -u origin <branch>    # Set upstream and push

# Push or pull all branches
git push --all
git pull --all
```

## Inspection and Comparison

```bash
# Show changes between commits
git diff                       # Unstaged changes
git diff --staged              # Staged changes
git diff <commit> <commit>     # Between specific commits

# Show commit details
git show <commit>

# Track changes to a file
git blame <file>

# List all tags
git tag
git tag -l "v1.*"              # Search for specific tags
```

## Undoing Changes

```bash
# Unstage files
git restore --staged <file>    # Modern syntax
git reset HEAD <file>          # Old syntax

# Discard changes in working directory
git restore <file>             # Modern syntax
git checkout -- <file>         # Old syntax

# Amend last commit
git commit --amend -m "New message"

# Reset to specific commit
git reset --soft <commit>      # Keep changes staged
git reset --mixed <commit>     # Keep changes unstaged (default)
git reset --hard <commit>      # Discard all changes (DANGER)

# Revert a commit (safer than reset)
git revert <commit>            # Creates new commit that undoes changes
```

## Stashing

```bash
# Save changes temporarily
git stash
git stash save "description"

# List stashes
git stash list

# Apply stashed changes
git stash apply                # Keep stash
git stash pop                  # Remove stash after applying

# Remove stash
git stash drop stash@{n}       # n is the stash index
git stash clear                # Remove all stashes
```

## Advanced Operations

```bash
# Rebase branch
git rebase <branch>
git rebase -i HEAD~3           # Interactive rebase for last 3 commits

# Cherry-pick commits
git cherry-pick <commit>

# Create tag
git tag <tag-name>             # Lightweight tag
git tag -a <tag-name> -m "Tag message"  # Annotated tag

# Clean untracked files
git clean -n                   # Dry run (shows what would be deleted)
git clean -f                   # Force delete untracked files
git clean -fd                  # Delete untracked files and directories

# Garbage collection
git gc
```

## Useful Aliases

Add these to your global Git config for shortcuts:

```bash
# ~/.gitconfig
[alias]
  co = checkout
  br = branch
  ci = commit
  st = status
  unstage = reset HEAD --
  last = log -1 HEAD
  visual = !gitk
  hist = log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
```

## Tips and Tricks

- Use `.gitignore` to exclude files from versioning
- Use `git commit --amend` to modify the last commit
- Set up SSH keys for secure, password-free repository access
- Remember that `git reset --hard` and `git clean -f` are destructive and unrecoverable
- Use `git merge --no-ff` to create a merge commit even for fast-forward merges
- When in doubt, create a branch
