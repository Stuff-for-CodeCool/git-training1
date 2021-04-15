I am modifying this file.


# git basics

> Please see [this repo](https://github.com/Stuff-for-CodeCool/git-github-presentation/tree/advanced) for detailed explanations of the commands used

## Cloning a project

You saw how it's done

## Feature branch

Working on a project, it's ideal to keep each feature on its own *branch*.

To **create** a branch, use `git checkout -b <new-branch-name>` to create branch `new-branch-name` and switch to it. Changes made on this branch will *not* appear on master.

To **switch** to a different branch, `git checkout <other-branch-name>`

Has anyone else created a branch? You can check by getting all the data from the origin (github, in our case) with the command `git fetch origin` followed by the command `git branch -r` which will show all branches -- both local and remote.

## Adding, committing and pushing stuff

After adding/modifying/deleting the files you need, git needs to know about them.

`git add .` will add all the files in the current folder. Once this is done, you need to commit your changes, with `git commit -m "<Commit message here>"`

The commit message should contain your name and clear descriptions of what you've done. Thus, `[alex] Modified display function in terminal.py, small bugfix in main.py menu` is an example of a  **good** commit message. `changed stuff` is a **bad** commit message. `sasdkfjgksjad` will kick your dog, disappoint your grandmother and turn all your coffee into decaf.

After all your files have been added and committed, you can push them to the remote site. You do this with the command `git push -u origin <your-current-branch-name>`. Do note that after you've done this once per branch, `git push` should suffice.

## What?

At any point, you can check the status of your files by running `git status`. This will show you how many files are untracked, how many are new, how many have been deleted, and how many have been modified.

## Too many files!

You may have files or folders that you don't need, and nobody else does, either. To make sure these don't litter your repo, add them to a file called `.gitignore`. The simplest way to populate a `.gitignore` file is to go to [gitignore.io](https://gitignore.io/), select your environmant (eg, Python), then copy/paste the result into `.gitignore`.

This file will also need to be added / committed / pushed.

## Conflicts

So you've made your changes, committed them, and want to push, but you keep getting errors about conflicing files. This happens because someone else has mdified the same lines in the same files as you have.

Run `git pull` to get all the new changes on your branch. Conflicting files will contain one or more blocks that look like this:

```
<<<<<<< HEAD
This is the code that you were trying to push
=======
This is the code that someone else pushed before you did
>>>>>> [long string of hexadecimals here -- this is the previous commit's ID]
```

This is a *conflict*. Simplest way to solve it is to delete the lines containing `<<<<<<`, `=======` and `>>>>>>` as well as all extraneous lines of code. Then, `git add .`, `git commit -m "[name] Proper commit massage"`, `git push` and the new changes will be added to the remote.

## Putting it all together

All your team's code is nice and functional, all branches are up-to-date. Time to integrate it all.

First, `git checkout master` will take you to **the branch into which you want to merge**. Then, `git merge <next-feature-branch>` will take **all new files from the other branch** and merge them **into the current one**. Be prepared to solve a lot of conflicts at this stage. Repeat for all needed branches.

Do note that files which exist on the destination branch (ie, master) that are not present on the source branch (ie, feature-branch) will stay as they are; files existing on the source branch will be added to the destination branch.

Once all the code has been merged into master, tested and deemed fit, time to `git add .`, `git commit -m "[name] Proper commit message"` and `git push` again.

Your code should now to be github.
