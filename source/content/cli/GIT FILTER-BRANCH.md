---
title: GIT FILTER-BRANCH
summary: A Git command for advanced history rewriting.
description: A Git command for advanced history rewriting.
tags:
  - git
---

# Basis

---

### Flags


 > 
 > **<font color=red>--commit-filter</font>**</br>
 >  Specify a custom filter that processes each commit individually.
 > 
 > **<font color=red>--env-filter</font>**</br>
 > Specify a custom filter that to modify environment variables for each commit (e.g. `GIT_AUTHOR_NAME` or `GIT_AUTHOR_EMAIL`.).
 > 
 > **<font color=red>--tag-name-filter cat</font>**</br>
 > Preserve existing tag name.

 > 
 > **<font color=red>-- --all</font>**</br>
 > Apply the filter to all branches and tags in the repository.

 > 
 > **<font color=red>--force</font>**</br>
 > Require when the repo has already been pushed to a remote server.

---

### Apply Filter on all Branches


````bash
# Checkout all branches locally
git branch -r | grep -v '\->' | while read remote; do git branch --track "${remote#origin/}" "$remote"; done

# Apply filter
git filter-branch ...

# Push all branches to origin
git push --all origin --force
````

# Examples

---

### Sets Committer info to Author info

This is useful because Committer and Author info can be different when modifying history (e.g. Committer date).

````bash
git filter-branch --force --tag-name-filter cat --commit-filter '
	GIT_COMMITTER_NAME=$GIT_AUTHOR_NAME;
	GIT_COMMITTER_EMAIL=$GIT_AUTHOR_EMAIL;
	GIT_COMMITTER_DATE=$GIT_AUTHOR_DATE;
	git commit-tree "$@";' -- --all
````

---

### Change Commits Author


````bash
git filter-branch --force --tag-name-filter cat --commit-filter '
	if [ "$GIT_AUTHOR_NAME" = "myOldName" ];
	then
		GIT_AUTHOR_NAME="myNewName";
		GIT_AUTHOR_EMAIL="myEmail@email.com";
		GIT_COMMITTER_NAME="myNewName";
		GIT_COMMITTER_EMAIL="myEmail@email.com";
		GIT_COMMITTER_DATE=$GIT_AUTHOR_DATE;
		git commit-tree "$@";
	else
		git commit-tree "$@";
	fi' -- --all
````

---

### Sign old Commits of a specific Author


````bash
git filter-branch --force --tag-name-filter cat --commit-filter '
	if [ "$GIT_AUTHOR_NAME" = "myName" ];
	then
		git commit-tree -S "$@";
	else
		git commit-tree "$@";
	fi' -- --all
````

---

### Remove Commits older than 90 days


````bash
git filter-branch --force --commit-filter '
	if [ "$(date -d "$(git show -s --format=%ci $GIT_COMMIT)" +%s)" -gt "$(date -d"90 days ago" +%s)" ];
	then
	  git commit-tree "$@";
	else
	  skip_commit "$@";
	fi' -- --all
````
