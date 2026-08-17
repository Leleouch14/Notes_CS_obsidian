A practical guide to essential Git terminal commands, daily workflows, repository maintenance, and `.gitignore`configurations.

## 1. Initial Setup & Identity Configuration

Run these once when setting up Git on a new machine.

```
# Set your global username and email (attached to all commits)
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"

# Save login credentials locally so you don't type your token on every push
# macOS:
git config --global credential.helper osxkeychain

# Windows:
git config --global credential.helper wincred

# Linux / WSL:
git config --global credential.helper store
```

## 2. Linking a Local Folder to GitHub

Use these steps to turn an existing local folder into a GitHub repository.

```
# 1. Navigate to your folder
cd /path/to/your/folder

# 2. Initialize Git tracking inside the folder
git init

# 3. Stage all files in the current folder
git add .

# 4. Save the initial snapshot
git commit -m "Initial commit"

# 5. Rename the default branch to 'main'
git branch -M main

# 6. Link your local repository to GitHub
git remote add origin https://github.com/YourUsername/your-repo-name.git

# 7. Push local files to GitHub and set tracking upstream
git push -u origin main
```

## 3. Daily Workflow (Making & Uploading Changes)

Execute these three commands whenever you add, edit, or delete files.

```
# Step 1: Stage changes (select modified/new files to track)
git add .                  # Stage EVERYTHING in the current directory
git add filename.cpp       # Stage a SPECIFIC file only

# Step 2: Commit staged changes locally with a descriptive message
git commit -m "feat: add vector operations example"

# Step 3: Upload committed changes to GitHub
git push origin main       # Or simply 'git push'
```

## 4. Inspection & Version History

Check status, view commit logs, or verify your current folder location.

```
# Check modified, untracked, or staged files
git status

# View commit timeline (clean single-line format)
git log --oneline

# View full detailed commit history with timestamps
git log

# View visual branch and commit history tree
git log --oneline --graph --all

# Print current working terminal directory path
pwd
```

## 5. Working with `.gitignore` & File Management

### Understanding `.gitignore` Rules

The `.gitignore` file tells Git which files or folders to completely ignore.

- `filename.ext` : Ignores a specific file in the root.
    
- `*.out` : Ignores any file ending with `.out` anywhere.
    
- `.vscode/` : Ignores a folder named `.vscode` in the root directory.
    
- `**/.obsidian/` : Ignores any folder named `.obsidian` at **any depth level** inside subdirectories.
    

### Common `.gitignore` Setup Commands

```
# Create/append rules to .gitignore directly from terminal
echo ".DS_Store" >> .gitignore
echo "*.out" >> .gitignore
echo ".vscode/" >> .gitignore
echo "**/.obsidian/" >> .gitignore

# Append multiple C/C++ build rules at once
cat << 'EOF' >> .gitignore

# C/C++ Binaries & Objects
*.o
*.obj
*.out
*.exe
*.app

# Debug symbols & build folders
*.dSYM/
build/
bin/

# macOS Junk
.DS_Store
EOF
```

## 6. Removing Tracked Junk Files (Cleanup Commands)

If a file or folder was accidentally pushed to GitHub, use `git rm --cached` to **remove it from GitHub tracking without deleting the file from your computer**.

### Removing Specific Folders / Files

```
# Remove .vscode folder from tracking
git rm -r --cached .vscode/

# Remove macOS .DS_Store from tracking
git rm --cached .DS_Store

# Remove an extensionless compiled binary (e.g., Relation_OP)
git rm --cached Relation_OP

# Remove .obsidian folders from root AND all subfolders recursively
git rm -r --cached "**/.obsidian" .obsidian/ 2>/dev/null || git rm -r --cached .obsidian/
```

### Complete Untrack & Reset (Re-evaluate `.gitignore`)

If Git is tracking many ignored files, purge the cache and re-stage everything according to your updated `.gitignore`:

```
# 1. Untrack all files from the index
git rm -r --cached .

# 2. Re-stage everything (respects new .gitignore rules)
git add .

# 3. Commit and push clean state
git commit -m "fix: purge untracked files based on updated .gitignore"
git push origin main
```

## 7. Useful Terminal & macOS Shortcuts

```
# Find a folder named 'cs' inside iCloud Drive automatically
find ~/Library/Mobile\ Documents -maxdepth 3 -type d -name "cs"

# Drag-and-Drop Pathing Trick:
# Type 'cd ' in Terminal, drag any folder from Finder into the terminal window, then hit Enter.
```