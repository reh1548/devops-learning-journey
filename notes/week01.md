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
## Bug log

### 3. Forgot the SSH key passphrase
- **Symptom:** the prompt `Enter passphrase for key '/home/rahmed/.ssh/id_ed25519':` appears on `ssh -T` and `git push`, and I could not remember the passphrase
- **Cause:** I set a passphrase on the key without recording it, and a passphrase cannot be recovered
- **Fix:** test guesses with `ssh-keygen -y -f ~/.ssh/id_ed25519`; if it stays lost, run `ssh-keygen -t ed25519 -C 'devops-learning-wsl'`, add the new .pub key on GitHub, delete the old key there, and test with `ssh -T git@github.com`
- **Lesson:** save the passphrase in a password manager the moment I create the key

### 4. Could not copy and paste into the VM
- **Symptom:** text copied in Windows would not paste into the VMware console, and nothing from the console could be copied out
- **Cause:** the minimal Rocky install has no desktop, so the text console has no clipboard integration
- **Fix:** `ip -br a` on the VM to get its address, `sudo systemctl enable --now sshd`, then `ssh rahmed@192.168.57.131` from a Windows terminal
- **Lesson:** work on Linux servers over SSH, not in the hypervisor window

### 5. vmtoolsd inactive on the VM
- **Symptom:** `systemctl is-active vmtoolsd` printed `inactive`
- **Cause:** the VMware guest tools service was not installed or running
- **Fix:** `sudo dnf -y install open-vm-tools` then `sudo systemctl enable --now vmtoolsd`, and check with `systemctl is-active vmtoolsd`
- **Lesson:** after installing anything, verify the service with `systemctl is-active NAME`

