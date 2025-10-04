---
title: GIT
summary: A free and open source distributed version control system.
description: A free and open source distributed version control system.
tags:
  - git
---

# Resources

* [https://ohshitgit.com/en](https://ohshitgit.com/en)
* [https://learngitbranching.js.org/](https://learngitbranching.js.org/)

# Basis

---

### HEAD

`HEAD` is the location in the commit tree. It's a "pointer" to a commit. It is possible to move it with `git checkout`.

---

### Config


 > 
 > **<font color=red>git config --list</font>**</br>
 > Parameters list.
 > 
 > **<font color=red>git config</font> user.name**</br>
 > Display a parameter (`user.name` here).
 > 
 > **<font color=red>git config --global</font> user.name myName**</br>
 > Change parameter value.

 > 
 > **<font color=red>git config --global credential.helper cache</font>**</br>
 > Save credentials in memory.
 > 
 > **<font color=red>git config --global credential.helper store</font>**</br>
 > Save credentials in plaintext in `~/.git-credentials` (less secure).
 > 
 > **<font color=red>git config --global credential.helper osxkeychain</font>**</br>
 > Save credentials in MacOS Keychain (more secure).
 > 
 > **<font color=red>git config --global credential.helper manager</font>**</br>
 > Save credentials in Windows Keychain (more secure).

 > 
 > **<font color=red>git config --global gpg.format ssh</font>**</br>
 > Set SSH key method to sign commits.
 > 
 > **<font color=red>git config --global user.signingkey</font> /path/to/my/public/key**</br>
 > Specify the public key to used for signing commits (the private key has to be configured in GitHub settings.

 > 
 > **<font color=red>git config --global http.sslBackend schannel</font>**</br>
 > Switch SSL Backend from OpenSSL (default) to Schannel (Windows built-in). This is useful in an organization with enterprise-managed certificates.

---

### Workflow


 > 
 > **<font color=red>git init</font>**</br>
 > Create git repository (local).

 > 
 > **<font color=red>git status</font>**</br>
 > Show status files (modified, added, removed, staged, ...).
 > 
 > **<font color=red>git add</font> myFile**</br>
 > Stage myFile (prepare for commit).
 > 
 > **<font color=red>git add -A</font>**</br>
 > Stage all files (including untracked/new ones).

 > 
 > **<font color=red>git commit -S -m "</font>Commit Message<font color=red>"</font>**</br>
 > Create a commit (`-S` to sign the commit and `-m` to set the commit's message).
 > 
 > **<font color=red>git commit --amend</font>**</br>
 > Modify last commit (only works if commit was not pushed).

---

### Commit History


 > 
 > **<font color=red>git show</font> myCommit**</br>
 > Display commit information.

 > 
 > **<font color=red>git log</font>**</br>
 > Show commit history.
 > 
 > **<font color=red>git log --pretty=fuller</font>**</br>
 > Commit history with more info (Committer name, commit date,...).
 > 
 > **<font color=red>git log --show-signature</font>**</br>
 > Show signature information on commit history.
 > 
 > **<font color=red>git log --oneline --graph --decorate</font>**</br>
 > Show commit history with graph.
 > 
 > **<font color=red>git log -p</font>**</br>
 > Shows difference between commits.
 > 
 > **<font color=red>git reflog</font>**</br>
 > Show local history with IDs.

# Branching

---

### Branch


 > 
 > **<font color=red>git branch</font>**</br>
 > Show local branches.
 > 
 > **<font color=red>git branch -r</font>**</br>
 > Show remote branches.

 > 
 > **<font color=red>git branch</font> myBranch**</br>
 > Create new branch.

 > 
 > **<font color=red>git merge</font> myBranch**</br>
 > Merge myBranch to current branch.

---

### Checkout


 > 
 > **<font color=red>git checkout</font> myBranch**</br>
 > Move HEAD to last commit of myBranch.

 > 
 > **<font color=red>git checkout</font> myBranch<font color=red>^</font>**</br>
 > Move HEAD to penultimate commit of myBranch.

 > 
 > **<font color=red>git checkout</font> HEAD^**</br>
 > Moves HEAD 1 commit back from current HEAD.
 > 
 > **<font color=red>git checkout</font> HEAD^^^**</br>
 > Moves HEAD 3 commits back from current HEAD.
 > 
 > **<font color=red>git checkout</font> HEAD~12**</br>
 > Moves HEAD 12 commits back from current HEAD.

 > 
 > **<font color=red>git checkout</font> HEAD^**</br>
 > Moves HEAD 1 commit back from current HEAD in the 1st parent of a merge.
 > 
 > **<font color=red>git checkout</font> HEAD^2**</br>
 > Moves HEAD 1 commit back from current HEAD in the 2nd parent of a merge.

---

### Tag


 > 
 > **<font color=red>git tag</font> myTag**</br>
 > Create a tag.

 > 
 > **<font color=red>git tag -d</font> myTag**</br>
 > **<font color=red>git push --delete</font> origin myTag**</br>
 > Delete a tag.

# Remote

---

### Remote Workflow


 > 
 > **<font color=red>git clone</font> \[REPO_URL\]**</br>
 > Clone remote repo to local machine.

 > 
 > **<font color=red>git push</font>**</br>
 > Push commits to remote repo.

 > 
 > **<font color=red>git fetch</font>**</br>
 > Get last changes from the remote repo.
 > 
 > **<font color=red>git pull</font>**</br>
 > Get last changes from the remote repo and merge them with local.

---

### Remote Branch


 > 
 > **<font color=red>git remote -v</font>**</br>
 > Display Remote Branches and their URL.

 > 
 > **<font color=red>git remote add</font> origin git@github.com:myUser/myRepo.git**</br>
 > Add Remote Branch (`origin` is the name of the branch, it can be anything).
 > 
 > **<font color=red>git remote set-url</font> origin git@github.com:myUser/myOtherRepo.git**</br>
 > Update URL for the Remote Branch. 
 > 
 > **<font color=red>git remote remove</font> origin**</br>
 > Remove Remote Branch.

 > 
 > **<font color=red>git branch</font> myBranch <font color=red>--set-upstream-to=</font>origin<font color=red>/</font>myBranch**</br>
 > Set Upstream for a Branch.

# Git Tools

---

### Stash


 > 
 > **<font color=red>git stash list</font>**</br>
 > List stashes.

 > 
 > **<font color=red>git stash save</font> myStashName**</br>
 > Put changes in a side working directory for later use.
 > 
 > **<font color=red>git stash apply</font> stashIndex**</br>
 > Add stashed code back into the code.

 > 
 > **<font color=red>git stash drop</font> stashIndex**</br>
 > Delete stash.

---

### Submodule


 > 
 > **<font color=red>git submodule status</font>**</br>
 > Show if any submodules are configured in the current repo. A submodule is a repo in a repo.

 > 
 > **<font color=red>git add submodule</font> \[SUBMODULE_REPO_URL\]**</br>
 > Add a submodule . Use `--recurse-submodule` to include submodule when using git commands.
 > 
 > **<font color=red>git submodule update --init --remote --rebase</font>**</br>
 > Update submodule version (use the last commit of the submodule).

 > 
 > **<font color=red>git clone --recurse-submodule</font>**</br>
 > Clone repo and it's submodules.

---

### LFS


 > 
 > **<font color=red>git count-objects -vH</font>**</br>
 > Show size of the repo. Not directly related to LFS but cans be usefull.

 > 
 > **<font color=red>git lfs ls-files -s</font>**</br>
 > Show LFS files and their size on current branch.
 > 
 > **<font color=red>git lfs ls-files -a</font>**</br>
 > Show LFS files on the full history (after a file is uploaded on LFS it will [still exist](https://docs.github.com/en/repositories/working-with-files/managing-large-files/removing-files-from-git-large-file-storage) on the remote storage even if its reference is removed in the HEAD.

 > 
 > **<font color=red>git lfs install</font>**</br>
 > **<font color=red>git lfs track</font> "\*.png"**</br>
 > **<font color=red>git add .gitattributes</font>**</br>
 > Add LFS to the repo (will track all new PNG files added to the repo).

 > 
 > **<font color=red>git lfs status</font>**</br>
 > Show staged files.

 > 
 > **<font color=red>git lfs untrack</font> "\*.png"**</br>
 > **<font color=red>git add --renormalize .</font>**</br>
 > **<font color=red>git commit -m </font>'Restore file that were previously in LFS'**</br>
 > **<font color=red>git push</font>**</br>
 > Revert files from being on LFS. Do not remove `.gitattributes`, it is required to run `git add --renormalize`.

# Rewrite History

---

### Reset / Revert


 > 
 > **<font color=red>git reset --soft</font> HEAD^**</br>
 > Moves HEAD 1 commit back and puts changes from the commit in staging.</br>
 > Warning: will create a conflict if the commit was previously pushed to remote.
 > 
 > **<font color=red>git reset --mixed</font> HEAD^**</br>
 > Moves HEAD 1 commit back and puts changes from the commit in working directory.</br>
 > Warning: will create a conflict if the commit was previously pushed to remote.
 > 
 > **<font color=red>git reset --hard</font> HEAD^**</br>
 > Moves HEAD 1 commit back and discard all changes (this also removes any unstaged files that were not part of the commit).</br>
 > Warning: will create a conflict if the commit was previously pushed to remote.

 > 
 > **<font color=red>git revert</font> HEAD^**</br>
 > Create new commit that undo last commit changes.

---

### Cherry Pick


 > 
 > **<font color=red>git cherry-pick</font> commit1 commit12 ccommit7**</br>
 > Add commits from other branches after HEAD.

---

### Rebase


 > 
 > **<font color=red>git rebase</font> myBranch**</br>
 > Replays current branch commits on myBranch (from their last common parent).
 > 
 > **<font color=red>git rebase --root</font>**</br>
 > Replays all commits from the root of the repository.
 > 
 > **<font color=red>git rebase --root --committer-date-is-author-date</font>**</br>
 > Replays all commits from the root and keep original commit date.

 > 
 > **<font color=red>git rebase -i</font> myBranch**</br>
 > Use rebase in interactive mode. Select commits to keep (`pick`), to modify (`edit`), squash commits (`squash`), reorder commits, ...
 > 
 > **<font color=red>git rebase --continue</font>**</br>
 > Continue to the next commit marked for edition.
 > 
 > **<font color=red>git commit --amend --no-edit</font>**</br>
 > Make your modification to the code and then issue this command to modify the commit (`--no-edit` to keep the name of the old commit).
 > 
 > **<font color=red>git rebase --abort</font>**</br>
 > Abort the rebase (useful in case of issues).

 > 
 > **<font color=red>git rebase -i $(git merge-base</font> myBranch <font color=red>HEAD)</font>**</br>
 > Rebase from the point it diverged from myBranch (first commit on current branch). Useful for squashing commit before a merge.
