# Contributing Guidelines
:tada: **First off, congrats for considering contributing to any project!** :tada:

It took me forever to overcome my fear to contribute to any project for many reasons. 
So, I hope this can help you as well :)


>  This contributing guideline was adapted from [fatiando](https://github.com/fatiando/community/blob/main/CONTRIBUTING.md) and [MetPy](https://github.com/Unidata/MetPy/blob/master/CONTRIBUTING.md)

-------------------------------------------------
## 1.Introduction

GitHub is  community-driven , so it's people like you  that make it useful and successful. 
These are some of the many ways to contribute:

* :bug: Submitting bug reports and feature requests
* :memo: Writing tutorials or examples
* :mag: Fixing typos and improving to the documentation
* :bulb: Writing code for everyone to use

If you get stuck at any point you can create an issue on GitHub (look for the *Issues*
tab in the repository) or contact us at one of the other channels mentioned below.

## 2.What can be done

> **comming soon**


## 3. Some tips before you contribute ... 

### Set up your Python environment

> **comming soon** # add my roadmap + intructions to miniconda

### Set up your Git environment + Examples

> Please, read [Source 1](https://git-scm.com/book/en/v2/GitHub-Contributing-to-a-Project), and watch [Source 2](https://egghead.io/lessons/javascript-how-to-fork-and-clone-a-github-repository), they are very useful!!)

1. **ADD LINK TO MY GITCONFIG HOW2**. See also -> [Check other git configurations](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration)

2. On GitHub website, navigate to the project you like, then click on fork button at the top-right of the page. [Please check these images](https://www.asmeurer.com/git-workflow/)

3. On **YOUR FORKED REPOSITORY** , copy the SSH link (git@github.com:yourgithubaccout/....) 

> *ps*: Have you generated your SSH key? If not, please  [CHECK HERE](https://docs.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) before moving on

+ On terminal, type `git clone` + the ssh link you just copied above
    
    ```sh
    $ git clone git@github.com:yourgithubaccount/forked_repository.git
    ```

+ Navigate to the forked repository
    
    ```sh
    $ cd forked_repository/
    ```
    
+ Check all the remote repositories that you have
    
    ```sh
    $ git remote -v 
    ```

4. Keep your forked repository up-to-date with the up-stream MAIN repository. On Github, navigate back to the main repository project menu. Copy the original SSH link (something like git@github.com:main_repository_that_your_forked_from/forked_repository.git). Go back to terminal and type the following:

+  Make sure you are on `~/path/to/your/forked_reposiroty(master)` folder
    
    ```ssh
    $ git remote add upstream git@github.com:main_repository_that_your_forked_from/forked_repository.git 
    ```

+ If, for some reason, you made a mistake  with the remote URL (copying HTTP instead of SSH) *I did it :(*
    
    ```sh
    $ git remote set-url upstream (write the new link here)
    ```
    
+ Verify that the remote URL has changed
    
    ```sh
    $ git remote -v
    ```
+ Tell *your local* git repository to get information from the *up-stream remote repository* (from the person's owner of the repository)
    
    ```sh
    $ git fetch upstream
    ```

+ Currently, your local copy of the master branch is pointing to your personal remote forked repository. Your remote repository is called *origin*. You want your local copy of master to point up-stream (=to the person's repository not yours), so whatever you pull changes into master, it will get the latest changes from the up-stream repository .
    
    ```sh
    $ git branch --set-upstream-to=upstream/master master
    ```
> Now, your local branch called *master* is tracking the up-stream master. So all the updates we want to get from the original repository can be done by pulling it.

5. Check if the original repository that you forked from has a file CONTRIBUTION.md. This contains intructions to help one making contributions to the project.

6. Create a new branch
    
+ Make sure you are on `~/path/to/your/forked_reposiroty(master)`
    
    ```sh
    $ pwd
    ```
    
+ Call your branch something useful,like `'(r)epository_(i)nicial/fix-bug-x'`. You should make a branch name that is short, descriptive, and unique. Some examples of good branch names are fix-install, docs-cleanup, and add-travis-ci. Some examples of bad branch names are feature, fix, and patch.
  
    ```sh
    $ git checkout -b 'ri/fix-bug-x'
    ```

> You will be automatically switched to that branch (ri/fix-bug-x). your current directory will be something like: ~/path/to/your/forked_reposiroty(ri/fix-bug-x)
 
7. Make your changes in the the file 

8. Added the changes to git 
    
    ```sh
    $ git add 
    ```

9. Commit on your file.  Remember to never commit to **master**. The command git status will tell you what branch you are on. I recommend putting the git branch in your command prompt, so that you will always know what branch you are on. So make sure your are on the correct branch

    ```sh
    $ git commit -am ' xxx xxx xxx xxx xxx '
    ```

10. Push your changes to **YOUR** remote forked repository 

    ```sh
    $ git push origin ri/fix-bug-x
    ```

11. Make a pull request. Please watch [How to create a pull request on Github](https://egghead.io/lessons/javascript-how-to-create-a-pull-request-on-github) and [How to Collaborate on a Pull Request on GitHub](https://egghead.io/lessons/javascript-how-to-collaborate-on-a-pull-request-on-github)

- The following is only if you need to update your branch during the merging waiting process. Sometimes, the original repository has updates, so your branch falls behind. This can cause merge conflicts. So you need to make sure you update the lastest changes.

- Start with fetching.
    
    ```sh
    $ git fetch upstream   	 	# remember that we already set the upstream before. 
					# If you didn't fork any project, just do `git fetch`
    ```
- Rebase your branch. In other words, replay your commits on top of whatever exist on the `master` upstream remote. This means that we are starting from a brand new fresh copy of master and then applying the commits on to the new copy of the master

    ```sh
    $ git rebase upstream/master	# if you are just working on your own original 
					# remote repository just type `git rebase origin/aster
    ```
* If you have any merge conflicts, open your editor, fix the problems, add your changes `git add`, and type:

    ```sh
    $ git rebase --continue
    ```

* If you have any problems just abort the rebase

    ```sh
    $ git rebase --abort
    ```

* Push the change to the remote repository

    ```sh
    $ git push				# if you get reject because of history, run `git push -f`
    ```
    
