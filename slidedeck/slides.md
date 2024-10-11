---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: /MFT_background_1.png
# some information about your slides (markdown enabled)
title: Welcome to Slidev
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
lineNumbers: true
---

# Welcome to *Git*ting comfortable

A short introduction to Git

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space or use keyboard arrows for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

---

# What is git?

If you are completly new to git, then see the below video. If you know the basics, then continue onwards with the slides.

<div align="center"><iframe width="560" height="315" src="https://www.youtube.com/embed/e9lnsKot_SQ?si=2DrFSwuNl1jmYsN-" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe></div>

---

# Format of the slides

In the upcomming slides we will go through;

* Basics of Git
* Why Git?
* Git: branches
* Git: Merges / rebasing
* Git: Merge conflicts
* Git: Revert / reset
* Git: Stash
* Git: Pushing
* Git: Pull Request

The section noted with "Git: ..." will follow a structure of `introduction` -> `video` -> `theory` -> `wrap-up`

---

# Basics of Git

Git is a version control system that helps you manage text files of all sorts in a collaborative and structured manner. <br>

The concept of git is that you work with a `repository` of which you can create `branches` (think shortlived variants of the codebase) that enables you to collaborate from the same point in time. You `commit` changes to a branch to create a record of your change for others and yourself to keep track of the history in changes. <br>

At the end you sync changes to a git server with `push` in order to save work and synchronize changes with your colleagues or automation systems.

```bash

git add <file> # Add a file to "staging"

git commit -m <message> # Records all changes that are staged by add with documentation on the work done in the files

git push -u origin <branch> # Push all missing commits from localhost (your machine) to a git server syncing your records with a server for collaboration

git checkout -b <branch> # Create and switch branch in a single command
```

---
layout: two-cols
---

# Basics of Git: Client-server

Git works as a client server paradigm 
<br>
<br>

Git works by a client (a user) cloning the source code from a `repository`, performing edits locally and pushing these edits to `origin` (the server from which you downloaded the source code). <br><br>
The benefit is here, that you can have multiple clients each with their own cloned repository, working on the same repo at the same time and continuously pushing code to origin.

::right::

<br>
<br>
<br>
<br>
<br>

```mermaid
graph TD

C1[Client 1] -->|push/pull| R[Remote Repository]
C2[Client 2] -->|push/pull| R[Remote Repository]

C1 -->|commit| L1[Local Repository]
C2 -->|commit| L2[Local Repository]
```

---
layout: two-cols
---

# Why Git?

Selling points:

::left::

<v-clicks>

- Multiple collaborators
  - 4 eyes principle

</v-clicks>

<v-clicks at=4>
<br>

*Joe; I like your change +1*

</v-clicks>

::right::

<div v-click> 

Git is an collaborative development solution that versions your code enabling multiple collaborators and pair-review processes built into the methodology.
</div>


<div v-click> 

```diff
public class Hello1
{
   public static void Main()
   {
-      System.Console.WriteLine("Hello, World!");
+      System.Console.WriteLine("Rock all night long!");
   }
}
```
</div>

<arrow v-click at=5 x1="250" y1="400" x2="550" y2="450" color="#953" width="2" arrowSize="1" />

---
layout: two-cols-header
---

# Why Git?

Selling points:

::left::

<div v-click at=1>

- Change history
  - Compliance
  - Reverting is easy
  - Versioning

</div v-click>

::right::
<div v-click at=2>
```mermaid
---
title: Example Git diagram
---
%%{init: { 'themeVariables': {
              'commitLabelFontSize': '10px',
              'branchFontSize': '10px',
       } } }%%
gitGraph
   commit id: "commit1"
   commit id: "commit2"
   branch feature/a
   checkout feature/a
   commit id: "commit3"
   commit id: "commit4"
   checkout main
   merge feature/a id: "merge"
   commit id: "commit5" tag:"v1"
```
</div v-click>

<div v-click at=3>
```mermaid
---
title: Example Revert
---
gitGraph
   commit id: "commit1" tag:"v1"
   commit id: "badCommit"
   commit id: "commit2" tag:"v2"
   commit id: "revert_badCommit" tag:"v2" type: REVERSE
```
</div v-click>

---
layout:  two-cols-header
---

# Why Git

Selling points:

::left::

<div v-click at=1>

- Automation
  - Quality check
  - Deployment

</div v-click>


::right::

<v-click>

Another benefit of Git is that we can integrate the version control with <span v-mark.circle.orange="3">automation tooling</span> which continuously <span v-mark.circle.red="4">quality checks</span> your code.

</v-click>

<v-click at=5>
```mermaid
---
title: Automation
---
flowchart LR
  id1(checkout code)
  id2(run quality check)
  id3(deploy service)
  
  id1 --> id2
  id2 --> id3
```
</v-click>

---

# Git: Branches - introduction

Git `branches` is a requirement of git. `Branches` are effectively a pointer to a snapshot of your changes, they keep track of increments in commits, and you have multiple long or short-lived `branches` where when you combine branches with a `merge`, the origin of the _from_ branch can be deleted.

Useful commands:

* `git branch -a` - will display all available branches both remote and local
* `git branch name` - will create `name` as a branch
* `git checkout name` - will switch to newly created branch `name`
* `git checkout -b featurebranch` - will create branch `featurebranch` and switch to it, all in one command.

---

# Git: Branches - video

<br>
<br>

<div align="center"><iframe width="560" height="315" src="https://www.youtube.com/embed/hwP7WQkmECE?si=klWPkP_ihdEghSNk&amp;start=68" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe></div>

---

# Git: Branches

Combining branches

When a change has been completed on a branch it is ready to be included in `main`. Combining two branches is referred to a *merging*. 
Before we dive into *how* to do it, it is important to talk about *when*. 

Ideally are branches short lived.
This means that we should strive to get meaningful changes merged back into `main` as quickly as possible.
A good rule of thumb is that branches should not live for more than two days.
In reality, this can be difficult to always do, but it is a good compass, none the less. 

Following our previous branch we can now go back to main

<v-switch>
<template #1>

```mermaid
gitGraph
   commit id: "initial"
   branch feature/show-branching
   commit id: "first-feature-change"
   commit id: "another-change"
```
 </template>
<template #2>
```mermaid
gitGraph
   commit id: "initial"
   branch feature/show-branching
   commit id: "first-feature-change"
   commit id: "another-change"
   checkout main
   commit id: "main-first-feature"
   commit id: "main-another-change"
   merge feature/show-branching
```
 </template>
</v-switch>

---

# Git: Branches - wrap-up

Lala something

Wrap-up branches

---

# Git: Merge / rebase - introduction

Git `merge` or `rebase` is an operation of combining the content of two branches. It is mostly used locally when you branch out of your `main` or `master` branch and want to `merge` `main` into your feature branch in order to get the latest revision of changes from main. A `merge` is also used when going from a feature branch to `main` but this is often facilitated by a `Pull-Request` which we will go over in later chapters.

Useful commands:

* `git merge origin/main` - when a feature branch is checked out, then this command will merge the current `local` changes of main into your current checked out branch.
* `git pull origin/main` - this is a combination command that will first pull changes from `origin main` and then merge these changes to your current checked out branch.
* `git rebase origin/main` - this will do a rebase of current branch based on `origin main`.
* [Git merge strategies](https://git-scm.com/docs/merge-strategies) - this docs, which can also be read with `man git merge`, explains different merge strategies that can be applied to `git merge`.

---

# Git: Merge / rebase - video

<br>
<br>

<div align="center"><iframe width="560" height="315" src="https://www.youtube.com/embed/0chZFIZLR_0?si=wXEsqrpC528IVvkj" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe></div>

---

# Git: Merge / rebasing

<v-switch>

<template #1>
It is not just at the git server we need to do merges / rebasing. These also happen locally, usually in order to synchronize a feature branch with changes from main before you create a pull request.

You can use the same methods as mentioned above locally, however there are a few rule-of-thumb's that we want to introduces:
</template>

<template #2>

**merge with fast-forward**<br>
Pull newest changes of main into your feature branch with fast-forward strategy. This is the safest and cleanest method next to rebase

```bash{2}
git checkout feature/branch
git pull origin main --ff
```

</template>

<template #3>

**rebase**<br>
Pull newest changes of main into your feature branch with rebase strategy. You can use this in-case fast-forward fails or you need to be more in control wil merge conflicts

```bash{2}
git checkout feature/branch
git pull origin main --rebase
```

</template>

<template #4>

**merge with merge commit**<br>
Pull newest changes of main into your feature branch with. You can use this in-case fast-forward fails or you need to be more in control wil merge conflicts

```bash{3}
git checkout feature/branch
git fetch main
git merge origin/main
```

</template>

</v-switch>

---

# Git: Merge / rebasing - wrap-up

Something something wrap up merge and rebase

---

# Git: Merge conflicts - introduction

`Merge conflicts` are a concept in git that exists due to it by nature is a version control tool, that allows simultaneous client that can change the same files, sometimes on the same linenumber, and if they then try and merge with eachother or both towards `main` they will experience the concept of `merge conflicts`. The existence of merge conflicts are due to the server not knowing which changes on the same linenumber should be the truth, or if both has the be truth - so you as a client have to help it make that decision by `fixing the merge conflict`.

There are not really any useful commands for when you need to handle a merge conflict, but there is one general recommendation;

* _Make use of an IDE to help you represent a merge conflict_. By default git will create a syntax highligting consisting of `>` and `<` characters to notate the two decision points on any given line/lines that represents the merge conflict. Making sense of these notations can be hard without a vision representation on top, such as vscode, Visual Studio, Idea IDE, Rider etc.

---

# Git: Merge conflict - video

<br>
<br>

<div align="center"><iframe width="560" height="315" src="https://www.youtube.com/embed/Sqsz1-o7nXk?si=-vQfv2kamrGYfnf4&amp;start=68" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe></div>

---

# Git: Merge conflict

When you are more than one participant on a git repository, then you will at some point run into a merge conflict. <br>

<v-switch>

<template #1>

Think of a scenario where you and a colleague both created a branch from main:

```mermaid
gitGraph
  commit id: "1"
  branch feature/colleague1
  commit id: "2"
  checkout main
  branch feature/colleague2
  commit id: "3"
```

</template>

<template #2>

You both edited the same file `text.txt` on the same line 1:

(colleague1)
```diff

+echo "hello colleague1"

```

(colleague2)
```diff

+echo "hello colleague2"

```

</template>

</v-switch>

---

# Git: Merge conflicts

When you are more than one participant on a git repository, then you will at some point run into a merge conflict. <br>

This will result in a conflict where both colleague1 and colleague2 have changed the exact same line on the exact same file;

```diff {all|3|5|all}
@@@ -1,1 -1,1 +1,5 @@@
++<<<<<<< HEAD
+echo "hello colleague1"
++=======
+ +echo "hello colleague2"
++>>>>>>> feature/colleague2
```

The diff is noted with all the special characters you in one block has what current revision marks as the "truth" and another block marks the incoming change as possible new "truth". Merge conflicts can happen both when doing local merge/rebase or when you open a PR. Often times the git server cannot handle merge conflicts for you, so you are required to do it locally.

Merge conflicts can be handled "easily" in your favorite IDE.

---

# Git: Revert / reset - introduction

Git `revert` or `reset` function differently, but they are often used with the same basic need; undoing something committed and/or pushed to origin. `Revert` works on a single or multiple commits that you want to reverse. `Reset` works on a single or multiple commits/staged changes that you want to unstage/uncommit in order to either reverse them or change in order to stage/commit again.

Useful commands:

* `git reset HEAD~1` - will reset the current changes with the one commit happened on `HEAD` of the branch. The changes will end up unstaged
* `git reset --soft HEAD~1` - the `--soft` adds that the changes will be staged instead of unstaged
* `git reset --hard HEAD~1` - the `--hard` adds that the changes will be completely undone.
* `git revert <commit-id>` - will create a new commit reverting the content of commit id you put into `<commit-id>`.

---

# Git: Revert / reset - video

<br>
<br>

<div align="center"><iframe width="560" height="315" src="https://www.youtube.com/embed/H2DuJNWbqLw?si=Ltw_X87fbonFOsqe" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe></div>

---

# Git: Revert / Reset

You can end up in a situation where you find yourself in a detached head state or you simply committed to the wrong branch or similar. This is where [git revert](https://git-scm.com/docs/git-revert) or [git reset](https://git-scm.com/docs/git-reset) comes in handy.

<v-switch>

<template #1>

Lets say you ended up in a situation where you did not want to have committed the files anyway.

```diff

echo "hello world"
+ echo "I did not want this change to be in the file
```

</template>

<template #2>

Your git status says that you have one change yet to be synced:

```{2}
On branch feature/merge_strategies
Your branch is ahead of 'origin/feature/merge_strategies' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

</template>

<template #3>

Then using git reset can help you get back to a point where you can edit the commit once again or scratch the commit entirely.

```bash
git reset --soft <commitid>
git reset --hard <commitid>
```

<br>

```bash
git reset --soft HEAD~1 # This will undo the latest commit happened on the current branch. 
  # --soft will make it so the edit is still changed and staged but not committed
```

<br>

```bash
git reset --hard HEAD~1 # This will undo the latest commit happened on the current branch. 
# --hard will make it so the edit of the commit is nowhere to be found anymore.
```

</template>

<template #4>

If you find yourself having commited and pushed the changes to a branch and you want to undo commit, then reset can be used, but it will be much cleaner to do a revert:

```bash
git revert <commitid>
```

<br>

```bash
git revert HEAD~1 # This will create a new commit undoing all changes from the latest commit on the branch
```

The main difference between revert and reset is that revert is for undoing changes with a new commit, whereas reset is mostly used before changes are synced with origin

</template>



</v-switch>

---

# Git: Stash - introduction

Git `stash` is a command that can help you save work that you unintentionally put on the wrong branch. When you have made changes to files while having checked out the wrong branch, and you then want to transfer said changes to a correct target branch, then git will prohibit you from simply checkout out said branch. This is where `git stash` comes in handy, since you by this can save work in a queue, checkout the correct target branch and `pop` the changes out of the queue thereby onto the currect target branch.

Useful commands:

* `git stash --include-untracked` - will stash the current staged, unstaged and untracked files into the `stash`
* `git stash pop` - will remove the latest changes added to `stash` and add them to the current checked out branch
* `git stash list` - will show the items in the current `stash` queue

---

# Git: Stash - video

<br>
<br>

<div align="center"><iframe width="560" height="315" src="https://www.youtube.com/embed/lH3ZkwbVp5E?si=z4V07VS_zoSn5Qb0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe></div>

---

# Git: Stash

Git stashing is the method of saving your unstaged work for a later point. Often it can be used to save work in order to do a `git pull` or if you made changes on a branch that should not have been done from that revision.

Git stash works as a LIFO queue (last in - first out), where if you run `git stash push` then an entry is put into the cue with the current stages and unstaged changes. If you then run `git stash pop` then the edits you just put int op the queue are "popped" from the queue and the edits are present again.

```bash
git stash list # will list the current queue of stashed entries
git stash push # will push current edits into a stash entry for the queue
git stash list # Should now have a single entry in it
git stash pop # will remove the entry from the queue and apply the edits again in the local repo
```

---

# Git: Pushing - introduction

lala introduction to git push

---

# Git: Pushing - video

Cant find it....

---

# Git: Pushing

lala some course material on git push

---

# Git: Pull Request - introduction

Lala intro to git pull request

---

# Git: Pull Request - video

Cant find it....

---

# Git: Pull Request

lala some course material on git Pull Request

---

# Time to do exercises!


- In the repo; https://github.com/mftenergy/Gitting-comfortable there are exercises
- Follow the path explained at https://github.com/mftenergy/Gitting-comfortable?tab=readme-ov-file#suggested-learning-path
- Path into an exercise directory, run `setup.sh` and read the README.md for instruction on what to do

```bash
cd basic-commits
./setup.sh
cat README.md
git magic
```

NOTE: There is a [cheatsheet](https://github.com/mftenergy/Gitting-comfortable?tab=readme-ov-file#cheatsheet) at the bottom of the README.md in the root of the repository.

You have two option;

1. **recommended** [Run in google cloud spaces (free)](https://console.cloud.google.com/cloudshell/editor?cloudshell_git_repo=https://github.com/mftenergy/git-course.git)
1. Run everything locally, if you choose that then read: [https://github.com/mftenergy/Gitting-comfortable/blob/main/setup-git/README.md](setup-git)
