✅ Summary of what you did
If for some reason, I have commits, I don't want to push in my main branch I can create a new branch add commits there and then follow below:

Created a new “clean” branch
> git checkout --orphan clean-main1
You wanted a branch without any secrets or unnecessary commits.
Let’s call it clean-main1.
Added only the commits/files you want
> git add .
Staged your source code and .dvc/config without secrets.
> git commit -m "message"
Made a single or a few clean commits.
Renamed the branch to main
> git branch -M clean-main main
clean-main is now your main branch.
The old main branch reference is overwritten locally.
Files from clean-main are preserved — nothing is lost.
Force pushed to GitHub
> git push --force origin main
Rewrites GitHub’s main branch with your clean commits.
Old commits containing secrets are removed from the branch history on GitHub.
GitHub push protection will now allow the push.
Optional: Check dangling commits in reflog
> git reflog
Old commits from previous main are still in your local repo as dangling commits.
You can recover them if needed, or prune them later.
Handled .DS_Store
Added .DS_Store to .gitignore to prevent macOS metadata files from being tracked in future commits.
🔹 Key points
Your new main branch contains only the commits you want.
Secrets are no longer in .dvc/config (moved to .dvc/config.local).
Old commits are dangling — safe, and recoverable if needed.
You don’t need to delete the old commits unless you want to completely purge them:
> git reflog expire --expire=now --all
> git gc --prune=now --aggressive
🔹 Safe workflow for the future
Always keep secrets in .dvc/config.local (ignored by Git).
Stage and commit only the files you want in your clean branch.
Use an orphan or new branch if you need to reset branch history.
Rename to main and --force push if you need GitHub to reflect only the clean commits.