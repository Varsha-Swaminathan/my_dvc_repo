What actually happens when you use DVC
When you run:
dvc add images/
DVC does two things:
Creates images.dvc
This file contains metadata (hashes, size, path)
This must be committed to Git
Updates .gitignore automatically
DVC adds a line like:
/images
This prevents Git from tracking the actual data files
The data is tracked by DVC, not Git
So now:
images.dvc → new file
.gitignore → modified file
Why you MUST commit .gitignore
If you don’t commit .gitignore:
❌ Git may accidentally track large data
❌ Teammates won’t ignore the data folder
❌ CI/CD may break
❌ Your repo becomes inconsistent
DVC assumes .gitignore changes are versioned.
What git status would show
After dvc add images/, you’ll see:
modified: .gitignore
new file: images.dvc
That’s your signal to commit both.
Correct workflow (always)
git add images.dvc .gitignore
git commit -m "Track images dataset with DVC"
dvc push
Mental model (this is the key insight)
Thing	Who tracks it
images/ (actual data)	DVC + remote storage
images.dvc	Git
.gitignore	Git
Git tracks instructions, not data.


Rule of thumb (memorize this)
If you are configuring DVC → .dvc/config changes
If you are tracking data → .dvc files & .gitignore change

.dvc/config is modified only when you change DVC settings, not when you add or update data.