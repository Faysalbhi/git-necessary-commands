# Git Beginner → Intermediate → Advanced

## 🟢 Beginner Level 
**Goal:** Learn basic repository operations, making changes, and simple collaboration
### Initialize & Clone Repositories
```bash
   git init # Start a new repository in current folder
   git clone <url> # Copy a remote repository to local machine
   git clone <url> <folder>   # Clone into specific folder name
```

### Check Status & Stage Changes``
  ```bash
   git status                # Check which files are changed/staged/untracked
   git status -s             # Short status format
   git add <file>           # Stage a specific file
   git add .                 # Stage all files in current directory
   git add -A               # Stage all changes (including deletions)
   git add -p              # Stage changes interactively (patch mode)
```

### Create Commits
  ```bash
  git commit -m "message"   # Commit staged changes with message
  git commit -am "message"   # Add tracked files and commit in one step
  git commit --amend       # Modify the most recent commit
```
### View History & Differences

  ```bash
  # Show commit history
  git log                    
  
  # Compact one-line commit history
  git log --oneline          
  
  # Visual history with branches
  git log --graph --oneline --decorate --all  
  
  # Show unstaged changes
  git diff                   
  
  # Show staged changes vs last commit
  git diff --staged          
  
  # Compare two commits
  git diff <commit1> <commit2> 
  
  # Show changes in a specific commit
  git show <commit>          
  ```
    
### Basic Remote Operations
  ```bash
    git push origin main       # Push commits to remote main branch
    git pull origin main       # Fetch and merge changes from remote
    git fetch                 # Download objects/refs from remote
  ```
### Beginner Daily Workflow Example
  ```bash
    # Start working on a new feature
    git clone https://github.com/user/repo.git
    cd repo
    git checkout -b feature/new-feature
    
    ### Make changes
    echo "New code" > file.txt
    git status
    git add .
    git commit -m "feat: add new feature"
    
    ### Share changes
    git push origin feature/new-feature
  ```

# 🟡 Intermediate Level — Branching, Merging & Collaboration
**Goal:** Master branch management, merging strategies, and team collaboration

### Branch Management
    ```bash
      git branch                 # List all local branches
      git branch -r              # List remote branches
      git branch -a              # List all branches (local + remote)
      git branch <name>          # Create new branch
      git branch -d <name>       # Delete branch (safe check)
      git branch -D <name>       # Force delete branch
      git checkout <name>        # Switch to existing branch
      git checkout -b <name>     # Create and switch to new branch
      git switch <name>          # Newer way to switch branches
      git switch -c <name>       # Create and switch (newer syntax)
    ```
### Merging Strategies
  ```bash
  git merge <branch>         # Merge branch into current branch
  git merge --no-ff <branch> # Merge with commit (even if fast-forward)
  git merge --squash <branch> # Squash all commits into one
  git mergetool              # Use configured merge tool to resolve conflicts
  ```
### Advanced Remote Operations
    ```bash
      git fetch --all           # Fetch from all remotes
      git pull --rebase         # Fetch and rebase instead of merge
      git push -u origin <branch> # Push and set upstream (first time)
      git push --force-with-lease # Force push more safely
      git remote -v             # Show remote URLs
      git remote show origin    # Detailed remote information
      git remote add <name> <url> # Add new remote
    ```

### Stash Changes Temporarily
    ```bash
        git stash                  # Save uncommitted changes
        git stash push -m "message" # Stash with descriptive message
        git stash list             # List all stashes
        git stash pop              # Apply and remove latest stash
        git stash apply            # Apply but keep in stash
        git stash apply stash@{1}  # Apply specific stash
        git stash drop             # Delete latest stash
        git stash clear            # Remove all stashes
    ```
### Undo Changes Safely
   ```bash
        git reset --soft HEAD~1    # Undo commit, keep changes staged
        git reset --mixed HEAD~1   # Undo commit, keep changes unstaged (default)
        git reset --hard HEAD~1    # Discard commit and changes (dangerous)
        git revert <commit>        # Create new commit that undoes changes (safe)
        git clean -fd              # Remove untracked files/directories
   ```
### Intermediate Workflow Example
  ```bash
    # Working on multiple features
    git switch main
    git pull origin main
    git switch -c feature/login
    
    # Develop feature
    git add .
    git commit -m "feat: add login functionality"
    
    # Emergency bug fix needed
    git stash push -m "login WIP"
    git switch main
    git switch -c hotfix/critical-bug
    # Fix bug, commit, push
    git switch feature/login
    git stash pop`
  ```
# 🔴 Advanced Level — History Manipulation & Complex Scenarios
**Goal:** Master history rewriting, advanced recovery, and complex workflows
### Rebase for Clean History
  ```bash
    git rebase <branch>        # Replay current branch commits onto another branch
    git rebase -i HEAD~3       # Interactive rebase (squash, edit, reorder)
    git rebase --continue      # Continue after resolving conflicts
    git rebase --abort         # Abort rebase operation
    git rebase --skip          # Skip current commit (use with caution)`
  ```
### Cherry-pick Specific Changes
```bash
    git cherry-pick <commit>   # Apply specific commit to current branch
    git cherry-pick <commit1> <commit2> # Pick multiple commits
    git cherry-pick <start>..<end> # Pick range of commits (exclusive)
    git cherry-pick <start>^..<end> # Pick range inclusive of start`
 ```
### Safe History Modification
    ```bash
        git revert <commit>        # Create undo commit (safe for shared history)
        git revert --no-commit <commit> # Revert without auto-commit
        git revert -m 1 <merge-commit> # Revert a merge commit`
    ```

### Recovery & Investigation
    ```bash
        git reflog                 # Show all HEAD movements (recovery tool)
        git checkout -b recovery <sha> # Recover lost commits from reflog
        git bisect start           # Start binary search for bug introduction
        git bisect bad             # Mark current commit as bad
        git bisect good <commit>   # Mark known good commit
        git bisect reset           # End bisect session
    ```
### Code Investigation Tools
    ```bash
        git blame <file>           # Show author for each line
        git blame -L 10,20 <file>  # Blame specific lines (10 to 20)
        git blame -C <file>        # Detect moved/copied lines
        git log -S "string"        # Search commits that added/removed string
        git log -p <file>          # Show history with changes for specific file`
    ```
### Tagging & Releases
    ```bash
        git tag                    # List all tags
        git tag v1.0.0            # Create lightweight tag
        git tag -a v1.0.0 -m "Release version 1.0.0" # Annotated tag
        git tag -d v1.0.0         # Delete tag locally
        git push origin v1.0.0     # Push specific tag to remote
        git push origin --tags     # Push all tags to remote
        git checkout v1.0.0        # Checkout specific tag`
    ```

### Advanced Configuration
  ```bash
      git config --global alias.co checkout  # Create shortcut
      git config --global core.editor "code --wait" # Set VS Code as editor
      git config --global pull.rebase true   # Default to rebase on pull
      git config --global init.defaultBranch main # Set default branch name`
  ```

- Advanced Workflow Example
    ```bash
        # Clean up feature branch before merge
        git switch feature/complex-feature
        git rebase -i main
        # Squash commits, reword messages
        
        # Cherry-pick hotfix to multiple branches
        git switch main
        git cherry-pick <hotfix-commit>
        git switch development
        git cherry-pick <hotfix-commit>
        
        # Create release
        git tag -a v1.2.0 -m "Release version 1.2.0"
        git push origin v1.2.0
    ```
    ⚡ Quick Reference — Most Used Commands
    ### Essential Daily Commands
    ```bash
      git status                 # What's the current state?
      git add .                  # Stage all changes
      git commit -m "message"    # Commit changes
      git push                   # Share changes
      git pull                   # Get latest changes
    ```
   ### Branch Operations
    ```bash
      git switch -c new-feature  # Create and switch to new branch
      git branch -d old-branch   # Clean up merged branches
      git merge feature-branch   # Integrate completed feature`
    ```
    ### Undo & Recovery
    ```bash
      git reset --soft HEAD~1    # Undo last commit, keep changes
      git stash                  # Temporary save changes
      git reflog                 # Find lost commits`
    ```
    
    ### History & Inspection
    ```bash
      git log --oneline --graph --all  # Visualize project history
      git diff                   # See what changed
      git blame <file>           # Who changed what?
    ```
    
# 🎯 Pro Tips & Best Practices
  - Commit Message Convention
    
    feat:     New feature
    fix:      Bug fix
    docs:     Documentation
    style:    Formatting changes
    refactor: Code restructuring
    test:     Add tests
    chore:    Maintenance tasks
    Gitignore Patterns
    gitignore
  # Common patterns
    node_modules/
    *.log
    .DS_Store
    .env
    dist/
    build/
    Useful Aliases
    bash
    git config --global alias.l "log --oneline --graph --decorate --all"
    git config --global alias.s "status -s"
    git config --global alias.co "checkout"
    git config --global alias.cm "commit -m"
  
  This cheatsheet covers Git from basic to advanced levels. Bookmark this page for quick reference!
  
  Remember: Always use --force-with-lease instead of --force for safer pushing, and prefer revert over reset for shared branches.

