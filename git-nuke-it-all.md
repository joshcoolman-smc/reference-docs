# Git Nuke It All
## Sometimes you just need to start over. Here's how to do it in a nutshell.

### Step 1: Backup (Optional)
If want to keep from your current project, now's the time to make a backup. Or not, whatever.

### Step 2: Nuke Everything (Except .git)
Open your terminal, navigate to your project's root directory, and unleash the following command:

```
find . -maxdepth 1 ! -name ".git" ! -name "." -exec rm -rf {} +
```

This will mercilessly delete every file and directory in your project, sparing only the `.git` directory. It's like a reset button for your project,keeping your Git history intact. I hope you know what you're doing.

### Step 3: Start Coding Again
It's time to rebuild. Set up your project from scratch. Once you're ready, stage your changes, commit, and push to your repository:

```
git add .
git commit -m "Starting fresh"
git push origin main
```

You've nuked your project and started over, preserving your Git history. It's a fresh start, a new day is dawning, now get back to work. 

happy coding!