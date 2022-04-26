## Basic Git Primer

*xkcd: Git - Randall Munroe*

<img src="xkcd_git.png" alt="XKCD Git" width="350" />

Git is a crazy powerful tool for version controlling source code and keeping track of changes by yourself or multiple people on a project. That said, you can definitely get yourself into some rough situations if you don't feel confident that you know what you're doing. This document is meant to serve as a primer to help you get started using git.

##### Note:

This is not meant to be a guide to best practice, nor is it meant to tell you everything you need to know. It just covers the basics of what I do most often and should hopefully give you enough information to find whatever else you may need. When you start getting into things like merging, it's best to search for how to handle it and start to grasp how git repositories "look" when you diverge from the main trunk.

---

### Basics

These are the things I use most often and their use cases.
#### Cloning
- Cloning a repo when you know the URL
	- `git clone <URL>`
- What if it has submodules?
	- `git clone --recursive <URL>` (if it has submodules)
- What if I want to give the folder a different name?
	- `git clone <URL> ./<FOLDER_NAME>`
		- I usually do this if I need to be able to look at multiple branches at once. Say I'm on `dev` and I want to see what's currently in `master`, I'll sometimes clone the repo again and just call it `<REPO_NAME>_master`. I'm sure there's a "proper" git way to do this, but I just find it safer as long as it's a short term check.

#### Branching
- Making a new branch and switching to it
	- `git checkout -b <BRANCH_NAME>`
		- This will make a new branch with all of your current changes, the branch you were on before will stay wherever the last commit was.
- Switching to another branch
	- `git checkout <BRANCH_NAME>`
		- If you try to switch to a new branch when you have uncommitted changes, you'll get a warning to either commit or stash those changes. Check the appropriate section for what you want to do.

#### Status
- If you don't know what files have changed since the last commit, this will tell you just about everything you need to know
	- `git status`

#### Adding
- Add files to be committed
	- `git add <FILE_1> <FILE_2> .. <FILE_N>`
- Adding all files in all directories under where you currently are
	- `git add .`
- Adding all matlab files in the current directory to be committed
	- `git add *.m`
		- This is just an example. The point is that you can use wildcards and other Linux terminal structures in git to do fancier things. That said it is ALWAYS safer to just individually add files if you're worried you might screw up.

#### Committing
- Once you have files added (you can always double-check you have the right files with `git status`)
	- `git commit -m "<COMMIT MESSAGE>"`

#### Pushing
*Note: Pushing things to the remote repo that shouldn't be pushed are how things get screwed up. Mistakes that only exist in your local repository might be a pain to fix sometimes but they're rarely that bad. Having to fix mistakes once they get into the remote can be very tedious and difficult. Most of the time this won't be an issue, just know that this section is the proverbial "point of no return".*
- To push to the remote version of your current branch
	- `git push`
		- You might have to enter your credentials here
		- If git yells at you that your remote branch doesn't exist or something similar, it will also usually give you the command to run to fix the problem. Just do what git tells you and it'll be fine.
---
### More advanced stuff

#### Checking Out
- If you've made changes you don't like and saved that file (but not committed) you can revert that file to the most recent committed version
	- `git checkout HEAD -- <FILE>`
- If you want an even older version
	- `git checkout <COMMIT> -- <FILE>`
		- To get the value to put for `<COMMIT>` look at the History section below
- If you want to grab a file from another branch entirely
	- `git checkout <BRANCH> -- <FILE>`

#### Diffing
*Note: Reading a diff can look super weird if you're not used to it. The stuff in red is anything you've gotten rid of from the last commit, the stuff in green is anything you've added.*

- To compare a file you've changed but not committed to the last committed version
	- `git diff <FILE>`
- To compare a file you've changed to an even older version
	- `git diff <COMMIT> -- <FILE>`
- To compare files between two branches
	- `git diff <BRANCH_1> .. <BRANCH_2>`
		- This can get a little weird, so this is a good resource to get what's happening here: https://devconnected.com/how-to-compare-two-git-branches/

#### Stashing
- Stashing allows you to save the changes you've made without committing them. This is mostly used if you want to switch branches to check something but you're not ready to commit your files yet.
	- `git stash`
- Once you're done with the stash you can pull it back into your working copy
	- `git stash apply`
- You can stash multiple times if you end up making changes in multiple places. I try to avoid doing this, but if you do you can list all of your stashes...
	- `git stash list`
- ... and then apply the stash you want back
	- `git stash apply <STASH_NUMBER>`

#### History
- I don't usually have to look at history much on the command line, but if you want to this is in my opinion the most consise way
	- `git log`
- If you don't want to go through the command line for this, you can also just check Gitlab
---

### How I Use Branches
These are just some basic notes that I try to follow. Nothing too complex and quite possibly not real "best practice".
- Only push to `main`/`master` when you've confirmed that the design is WORKING. Most people treat this like a release branch. If you wouldn't give it to someone to actually run in the field, it probably shouldn't be pushed here.
	- On a side note with this, there's a large effort right now by Github and Gitlab and whatnot to rename the `master` branch to `main`. In most cases they mean the same thing. I think APL's Gitlab instance still defaults to `master`.
- I usually keep a main `dev` branch for all of my odds and ends work. This is the branch I spend 90% of my time on, unless there are very specific tasks that need to get done that will be a large effort.
- For those tasks that are going to be a large effort, I usually branch off of `dev` and name the new branch something along the lines of what it's being used to test, i.e. `spi` for building a new SPI interface.
- Merging gets weird, which is why I didn't include it in this document. Most of the time it's not too bad, but if you get multiple people working on a single file things can get messy. To be safe I always just search for the proper merge commands to merge one branch into another and if there are conflicts I sometimes just search for how to solve those as well.
- Once you start getting into diverging from the main trunk of the repo, it's also best to start looking at some diagrams to try to understand what these branches and merges "look" like. You don't need to become an expert, but there are some good visuals that can definitely help make what you're trying to do more clear.

---

### What If I Done Goofed?

Here are some resources I like for getting yourself out of a pickle:

- [Git Flight Rules](https://github.com/k88hudson/git-flight-rules)

- [Fixing Commits Choose Your Own Adventure](https://sethrobertson.github.io/GitFixUm/fixup.html)

- Stack Overflow

    - I've found some really good and thorough expanations of very specific actions on Stack Overflow. Might take some searching to find what you need, but it's definitely a good resource.

    
