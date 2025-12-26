---
title: GitHub Actions
summary: "A note about GitHub's automation tool."
description: "A note about GitHub's automation tool."
tags:
  - github
---

# Workflow Syntax

---

### On


````yml
on: 
  # Triggered manually (run button)
  workflow_dispatch: 

  # Triggered on pull request
  pull_request:

  # Triggered on push on specified branch
  push:
    branchs:
      - my-branch
        
  # Triggered by another workflow
  workflow_run:
    workflows:
	    - myWorkflow
	
````

---

### Checkout


````yml
- name: Checkout code 
  uses: actions/checkout@v3
  with:
    submodules: recursive # Fetch repo submodules
    lfs: true # Fetch LFS data
````

# Variables

---

### github

#### User

* `github.actor`: name of the use the triggered the workflow.

#### Ref

* `github.ref_name`: branch name (warning: don't work in PR triggered workflow see `github.head_ref`).
* `github.head_ref`: PR source branch name.
* `github.head_ref`: PR target branch name.

# GitHub CLI

---

### Workflow


 > 
 > **<font color=red>gh workflow run</font> my-test-workflow.yml <font color=red>\\</font>**</br>
 > **<font color=red>--ref</font> my-test-branch <font color=red>\\</font>**</br>
 > **<font color=red>--field </font>my_input_1<font color=red>=</font>12 <font color=red>\\</font>**</br>
 > **<font color=red>--field</font> my_input_2<font color=red>=</font>bla**</br>
 > Run a workflow that doesn't exist on the default branch yes (needs to have `on: push: branchs` set).
