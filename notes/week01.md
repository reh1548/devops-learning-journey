# Week 1 notes
## Bug log

### 1. SSH key not found
- **Symptom:** `cat ~/.ssh/id_ed25519.pub` printed "No such file or directory"
- **Cause:** I typed a bare name at the ssh-keygen file prompt, so the key was saved in my current folder instead of ~/.ssh
- **Fix:** `mkdir -p ~/.ssh`, `mv` both files into ~/.ssh with the standard names, `chmod 700 ~/.ssh`, `chmod 600` on the private key
- **Lesson:** press Enter to accept the default path, then confirm with `ls -l ~/.ssh`

### 2. git push said "Repository not found"
- **Symptom:** `ERROR: Repository not found`, and `git remote add` said "remote origin already exists"
- **Cause:** I ran the template with the literal text YOURUSER in the remote URL, so `origin` pointed at a nonexistent repo
- **Fix:** `git remote set-url origin git@github.com:reh1548/devops-learning-journey.git`
- **Lesson:** replace placeholders before running; check with `git remote -v`
