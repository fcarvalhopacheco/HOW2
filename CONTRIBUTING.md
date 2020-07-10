# Contributing Guidelines
:tada: **First off, congrats for considering contributing to any project!** :tada:

It took me forever to overcome my fear for contributing to any project for many reasons. 
So, I hope this can help you as well :)


>  This contributing guideline was adapted from [fatiando](https://github.com/fatiando/contributing/edit/master/CONTRIBUTING.md) and [MetPy](https://github.com/Unidata/MetPy/blob/master/CONTRIBUTING.md)

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


## 3. Make sure you ... 

+ Set up your Python environment
> **comming soon** # add my roadmap + intructions to miniconda

+ Set up your Git environment ( Plese, read [Source 1](https://git-scm.com/book/en/v2/GitHub-Contributing-to-a-Project), and watch [Source 2](https://egghead.io/lessons/javascript-how-to-fork-and-clone-a-github-repository), they are very useful!!)

    1. **ADD LINK TO MY GITCONFIG HOW2** [Check other git configurations](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration)

    2. On GitHub website, navigate to the project you like, then click on fork button at the top-right of the page [Please check this images](https://www.asmeurer.com/git-workflow/)

    3. On your forked repository, copy the SSH link (something like git@github.com:yourgithubaccout/....). ps. you need to first generate your SSH key if havent done yet [CHECK HERE](https://docs.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

    ```sh
    # On terminal, type `git clone` + the ssh link u just copied above:
    $ git clone git@github.com:yourgithubaccount/forked_repository.git

    # Navigate to the forked repository
    $ cd forked_repository/
    ```

    4. Keep your forked repository up-to-date with the up-stream MAIN repository. On Github, navigate back to the main repository project menu. Make a copy of the original SSH link (something like git@github.com:main_repository_that_your_forked_from/forked_repository.git). Go back to terminal and type the following

    ```ssh
    # Make sure you are on ~/path/to/your/forked_reposiroty(master) folder
    $ git remote add upstream git@github.com:main_repository_that_your_forked_from/forked_repository.git 

    # Tell your local git repository to get information from the up-stream remote repository
    $ git fetch upstream

    # Currently, your local copy of the master branch is pointing to your personal remote forked repository. Your repository is called origin. You want your local copy of master to point up-stream (=to the person's repository not yours), so whatever you pull changes into master, it will get the latest changes from the up-stream repository .
    $ git branch --set-upstream-to=upstream/master master

    # Now, your branch called master is tracking the up-stream master. So all the updates we want to get from the original repository can be done by pulling it.
    ```

    5. Check if the original repository that you forked from has a file CONTRIBUTION.md. This contains intructions to help one making contributions to the project.

    6. Create a new branch
    
    ```sh
    # Make sure you are on ~/path/to/your/forked_reposiroty(master)
    # Call your branch something useful and related to the contribution you are making to
    $ git checkout -b 'fix/someissue'
    
    # You will be automatically switched to that branch (fix/someissue). your current directory will be something like: ~/path/to/your/forked_reposiroty(fix/someissue)
    ```
 
    7. Make your changes, add + commit and push it 

    ```sh
    # add the file you just changed
    $ git add 

    # commit on it
    $ git commit -am ' xxx xxx xxx xxx xxx '
    ```


