# GIT: Workflow and Dealing with conflicts

## Feature Based Development

#### Branches

* MASTER - which keep our live theme and all features on production;

* DEV - which keeps all DEVs work together;

* FEATURES -
    1. include current task;
    2. can be branched from Master or Dev;
    3. needs to be merge into DEV;
    4. naming convention: all (except of master, develop, release-*, или hotfix-*)


**That structure could be different from projects but the main thing here :
All devs work in one branch(Dev/master) at the end of each day/sprint.**

## Commands for merging
```
git checkout dev
```
Switched to branch dev
```
git pull
```
To pull latest changes from our colleagues

```
git merge feature
```

If no conflicts => Branched merged

```
git add . => git commit -m”Merged feature into dev”
```

```
git push -u origin dev
```
Push all changes to the origin

## Conflicts

Conflicts generally arise when **two people have changed the same lines in a file**, or if one developer deleted a file while another developer was modifying it.

Conflicts only affect the developer initiated the merge. The developer has responsibility to resolve the conflict.

When we have a conflict git doesn’t allow us to merge files until resolving.


#### Detect

You will see an error in the terminal with conflicted file name.

```
CONFLICT (content): Merge conflict in OUR_FILE_NAME
Automatic merge failed; fix conflicts
and
then commit the result.
```

#### Check conflict file

Our file was changed to guide us where exactly our conflict is.

```
<<<<<<< HEAD
HERE OUR CURRENT CHANGES IN DEV BRANCH (IN WHICH WE MERGE)
======= CONFLICT DIVIDERS
>>>>>>> new_branch_to_merge_later CONTENT IN OUR MERGING BRANCH.
```

#### Modify manually

Decide which of the changes you want to save and commit.

```
git add .
git commit -m”Merged feature into dev”
git push origin dev

```

#### Other useful commands

```
git merge --abort
```

Executing git merge with the --abort option will exit from the merge process and return the branch to the state before the merge began.

```
git log --merge
```

Passing the --merge argument to the git log command will produce a log with a list of commits that conflict between the merging branches.

```
git status
```

Return git status and more information about conflict if it is.

```
git diff
``

Helps find differences between states of a repository/files to predict conflicts.
