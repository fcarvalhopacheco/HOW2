# macOS Ventura 13.2

## My Iterm2 
![my iterm2](https://github.com/fcarvalhopacheco/HOW2/blob/master/1.macos/my_iterm2.png)


## Table of Contents

1. [Homebrew](#1---homebrew)

2. [CASK](#2---cask)
   
3. [ITERM2](#3---iterm2) 
    
4. [ZSH](#4---zsh)

5. [Oh my ZSH](#5---oh-my-zsh)

6. [Powerlevel10k](#6---powerlevel10k)
    
7. [Fonts](#7---patched-font)
   
8. [Theme and Font configuration](#8---theme-configuration)

9. [Auto Suggestion + other plugins](#9---auto-suggestion)
    
10. [GIT](#10---git)

11. [VirtualBOX](#11---virtualbox)

12. [Python Enviroment](#12---python-enviroment)

13. [Cookiecutter](#13---cookiecutter)

14. [Vim-commandsl](#14---vim-commands)

15. [NeoVim + lua](#15---neovim-lua)

-----------------------------------------------------------------------------------

## 1 - Homebrew

    
* Download homebrew.  
    
    ```zsh
    $ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```

## 2 - CASK
   
* Download cask.  

    ```sh
    $ brew install cask 
    ```

## 3 - ITERM2

* Download ITERM2.  
   
    ```sh
    $ brew install --cask iterm2
    ``` 

* Download ITERM2 color themes by clicking on:
    
    + [iterm2colorschemes](https://github.com/mbadolato/iTerm2-Color-Schemes/zipball/master)

## 4 - ZSH
   
* If you dont have **Z shell**. On terminal, type:
    
    ```sh
    $ brew install zsh
    ``` 

## 5 - Oh My ZSH
 
* Download zsh
      
    ```sh
    $ sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
    ```
    >or
    
    ```sh
    $ sh -c "$(wget -O https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
    ```
      
## 6 - Powerlevel10k
   
* Clone power10k
      
    ```sh
    $ git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
    ```
      
* Edit the file ~/.zshrc. On terminal, type:
      
    ```sh
    # Navigate to home
    $ cd
    
    # Open the file
    $ vi .zshrc
    ```

* Navigate to ~line 11 and change ZSH_THEME, then exit the file.
  
    ```sh
    # Insert the text
    ZSH_THEME="powerlevel10k/powerlevel10k"
    
    # Get out of vim
    esc
    :wq
    ```

## 7 - Fonts

* Recommended: Meslo Nerd Font patched for Powerlevel10k. [source](https://awesomeopensource.com/project/romkatv/powerlevel10k)

* Download the following four files.
    + [MesloLGS NF Regular.ttf](https://github.com/romkatv/dotfiles-public/raw/master/.local/share/fonts/NerdFonts/MesloLGS%20NF%20Regular.ttf)
    + [MesloLGS NF Bold.ttf](https://github.com/romkatv/dotfiles-public/raw/master/.local/share/fonts/NerdFonts/MesloLGS%20NF%20Bold.ttf)
    + [MesloLGS NF Italic.ttf](https://github.com/romkatv/dotfiles-public/raw/master/.local/share/fonts/NerdFonts/MesloLGS%20NF%20Italic.ttf)
    + [MesloLGS NF Bold Italic.ttf](https://github.com/romkatv/dotfiles-public/raw/master/.local/share/fonts/NerdFonts/MesloLGS%20NF%20Bold%20Italic.ttf)
      
* Double-click on each file and press "Install". This will make MesloLGS NF font available to all applications on your system. Configure your terminal to use this font:
      
      
## 8 - Theme Configuration
 
* Customize your terminal the way you like. For new users. On terminal, type:
      
    ```sh
    $ p10k configure
    ```

* How do I add username and/or hostname to the left sife of the prompt? [source](https://awesomeopensource.com/project/romkatv/powerlevel10k#how-do-i-add-username-andor-hostname-to-prompt)

    ```sh
    # open the following file
    $ vi ~/.p10k.zsh
    
    # Remove the # behind context to activate username@hostname 
         
    typeset -g POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(
    status                  # exit code of the last command
    command_execution_time  # duration of the last command
    background_jobs         # presence of background jobs
    direnv                  # direnv status (https://direnv.net/)
    virtualenv              # python virtual environment (https://docs.python.org/3/library/venv.html)
    anaconda                # conda environment (https://conda.io/)
    pyenv                   # python environment (https://github.com/pyenv/pyenv)
    goenv                   # go environment (https://github.com/syndbg/goenv)
    nodenv                  # node.js version from nodenv (https://github.com/nodenv/nodenv)
    nvm                     # node.js version from nvm (https://github.com/nvm-sh/nvm)
    nodeenv                 # node.js environment (https://github.com/ekalinin/nodeenv)
    # node_version          # node.js version
    # go_version            # go version (https://golang.org)
    # rust_version          # rustc version (https://www.rust-lang.org)
    # dotnet_version        # .NET version (https://dotnet.microsoft.com)
    rbenv                   # ruby version from rbenv (https://github.com/rbenv/rbenv)
    rvm                     # ruby version from rvm (https://rvm.io)
    fvm                     # flutter version management (https://github.com/leoafarias/fvm)
    kubecontext             # current kubernetes context (https://kubernetes.io/)
    terraform               # terraform workspace (https://www.terraform.io)
    aws                     # aws profile (https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html)
    # aws_eb_env            # aws elastic beanstalk environment (https://aws.amazon.com/elasticbeanstalk/)
    # azure                 # azure account name (https://docs.microsoft.com/en-us/cli/azure)
    # gcloud                # google cloud acccount and project (https://cloud.google.com/)
         
    context                 # user@hostname
    
    nordvpn                 # nordvpn connection status, linux only (https://nordvpn.com/)
    ranger                  # ranger shell (https://github.com/ranger/ranger)
    vim_shell               # vim shell indicator (:sh)
    # midnight_commander    # midnight commander shell (https://midnight-commander.org/)
    vi_mode                 # vi mode (you don't need this if you've enabled prompt_char)
    # vpn_ip                # virtual private network indicator
    # ram                   # free RAM
    # load                  # CPU load
    time                    # current time
    # public_ip             # public IP address
    # proxy                 # system-wide http/https/ftp proxy
    # battery               # internal battery
    # example               # example user-defined segment (see prompt_example function below)
    )
         
    # ADD a # behind the the following text
    #typeset -g POWERLEVEL9K_CONTEXT_{DEFAULT,SUDO}_{CONTENT,VISUAL_IDENTIFIER}_EXPANSION=
    
    # ADD context on the list below to show username@hostname on the left lide
    # The list of segments shown on the left. Fill it with the most important segments.
    typeset -g POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(
	    context
        os_icon                 # os identifier
        dir                     # current directory
        vcs                     # git status
        # prompt_char           # prompt symbol
    )
          
    # ADD the # behind context on the list below to stop showing the username@hostname on the right side 
    typeset -g POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(
	...
        #context
        ...
    )

    ```

## 9 - Auto Suggestion + zsh-syntax-highlighting + web-search

### `zsh-autosuggestions`

* Check the [Source](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md#oh-my-zsh)
      
    ```sh
    # On terminal, clone the following repository into $ZSH_CUSTOM/plugins (by default ~/.oh-my-zsh/custom/plugins)
    $ git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

    # Open ~/.zshrc, by typing:
    $ vi ~/.zshrc
      
    # Find the line that starts with plugin, and add zsh-autosuggestions inside the parenthesis
    plugins=(git zsh-autosuggestions)
      
    # Save and close the file
    esc
    :wq!
      
    # Open a new terminal to see the changes
    ```

### `zsh-syntax-highlighting`
+ Check [here](https://github.com/zsh-users/zsh-syntax-highlighting)
      
### `web-search`

+ Just added the following into `~/.zshrc`

    ```sh
    plugins=( 
        git
        zsh-autosuggestions
        zsh-syntax-highlighting
        web-search
    )
    
    export ZSH=/Users/<user>/.oh-my-zsh
    source $ZSH/oh-my-zsh.sh
    ```

## 10 - Git

* I already have git on my ubuntu machine and a github account. So I need to link both computers to the same github account

* I will be following instructions from [here](https://help.github.com/en/github)

* >*At the heart of GitHub is an open source version control system (VCS) called Git. Git is responsible for everything GitHub-related that happens locally on your computer..* [source](https://help.github.com/en/github/getting-started-with-github/set-up-git)

    
* Download it!
    
    ```sh
    # Download the latest version of GIT
    # If you have followed me. you should have git already install at this moment but if not, type:
    $ brew install git
      
    # or Update it
    $ brew upgrade git
    ```
    
* Set an username [source](https://help.github.com/en/github/using-git/setting-your-username-in-git)
    
    ```ssh
    # This config set up is useful to track your git commits!
    # Your name will be visible in future commits you push 
    # to GitHub from the command line. By the way, if you 
    # already have an username in other machine, dont worry.
    # It looks like that using git config here will only affect 
    # future commits and will not change anything from past commits.
      
    # USERNAME FOR EVERY REPOSITORY YOU CREATE!
    # On Terminal, type:
    $ git config --global user.name "YOUR NAME OR NICKNAME HERE-GLOBAL"
       
    # Check if it is correct by typing:
    $ git config --global user.name
      
    # you should see
    >YOUR NAME OR NICKNAME HERE-GLOBAL
      
    # USERNAME FOR A SINGLE REPOSITORY
    # Change the current working directory to the local repository 
    # where you want to configure the name that is associated with your Git commits.
         
    # On Terminal, type:
    $ git config user.name "YOUR NAME OR NICKNAME HERE-LOCAL"
      
    # Check if it is correct by typing:
    $git config user.name
      
    # you should see
    >YOUR NAME OR NICKNAME HERE-LOCAL
    ```
      
* Setting your commit  address in Git [source](https://help.github.com/en/github/setting-up-and-managing-your-github-user-account/setting-your-commit-email-address)
    
    ```sh
    # On Terminal,
    $ git config --global user.email "email@example.com"

    # Check if your s is correct
    $ git config --global user.email

    > yourhere@test.com
    ```

* Set a global ignore file 
    
    ```sh
    # navigate to home directory
    $ cd
    $ vi .gitignore_global
    ```
>	I am using macOS, so i will be adding [macOS.gitignore](https://github.com/github/gitignore/blob/master/Global/macOS.gitignore) on my .gitignore_global
  

* How to create a repository ? [Click here](https://docs.github.com/en/get-started/quickstart/create-a-repo)

* How to clone a repository? [Click here](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository-from-github/cloning-a-repository)

## 11 - Virtualbox	

* I currently use virtual box to process Shipboard ADCP data, but I will soon start playing with LINUX practices and want to have a dedicated computer for it. 
  
* Download the VirtualBOX by,

    ```sh
    # On Terminal, type:
    $ brew install --cask virtualbox

    # Check the version:
    $ brew cask info virtualbox

    #Clen any old version installed on computer
    $brew clean up

    #Open VirtualBox:
    $virtualbox 
    ```   
   
## 12 - Python Environment

* There are many ways to install/create Python working Enviroments. However, I will be using conda package manager with miniconda and the conda-forge package collection, which provides platform-independent package management for Python and other softwares in self-contained user-specific enviroments. 

* Why this way? It seems the science community has adopted Anaconda (=miniconda+150packages) distribution to create and manage python project enviroments. Please check [Introduction to Conda for (Data) Scientists](https://carpentries-incubator.github.io/introduction-to-conda-for-data-scientists/setup/) to learn more about it. Ps. miniconda(=conda+python+basic packages) is the small version of anaconda.  

* Other ways? Please check [The definitive guide to setup my Python workspace](https://medium.com/@henriquebastos/the-definitive-guide-to-setup-my-python-workspace-628d68552e14), by Henrique Bastos. Its a great tutorial to config your machine with pyenv, virtualenv ... 

* Download the Miniconda installer,[Miniconda](https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh)
      
    ```sh
    # On Terminal, navigate to:
    $ cd Downloads

    # Install Miniconda by typing:
    $ zsh Miniconda3-latest-Linux-x86_64.sh  	

    # Follow the instructions on terminal. 
    # If you forget to press NO to auto_activate miniconda every time you open a new sessiong type:
    # conda config --set auto_activate_base false	 
    
    # Once the install script completes, you can remove it 
    $ rm -rf Miniconda3-latest-MacOSX-x86_64.sh
	
    # Verify your Conda installation:
    $ conda help
    $ conda -V

    # Check the path by typing:
    $ whence -p conda #or 
    $ type conda  # For bash terminal, type: which conda -> The equivalent to zsh's which in bash is type. 
      
    # Make sure you have the most recent version
    $ conda update --name base --channel defaults --yes conda

    # Initialize your shell for Conda
    $ conda init zsh
    ```  

## 13 - Cookiecutter

> A cross-platform command-line utility that creates projects from cookiecutters (project templates), e.g. 
> Python package projects, C projects.
   
* Original project: [https://github.com/cookiecutter/cookiecutter](https://github.com/cookiecutter/cookiecutter)
* [Check my quick tutorial here](https://github.com/fcarvalhopacheco/HOW2/blob/6269bee581763cc760bf6ce778f8d7136350ee26/1.macos_catalina_setup/cookiecutter-guide.md) 


## 14 - Vim-commands 

1. General navigation
    
    ```
    <shift> + O = insert mode above
    <shift> + P = paste above
    <shift> + I = insert mode start at the beginning of the line 
    <shift> + A = insert mode start at the end of the line  
    ? =  Search mode 
        - Press `n` to look for the next result 
        - Press <shift> + N to jump reverse through results
        - Press * to jump to the next occurence of whatever is underneath your cursor
        - Press # to jump backwards 
    ```

2. Horizontal speed
   
    ```
    f* = jumps to character
    t* = jumps to behind character
    F* and T* = jump backwards through results
    ; = to jump forward
    , = to jump backwards through results
    x = to delete a character
    s = to delete a character and enter insert mode
    dt) = delete up to the character closing 
    cw = delete a word and enter insert mode
    D = delete rest of line
    C = delete rest of line and enter insert mode
    ``` 

3. Vertical speed
   
    ```
    G = jumps to the bottom
    gg = jumps to the begninning 
    :100 or 100G  = goes to line 100 
    relative numbers = * you need to 'set number relativenumber' on .vimrc 
        12k = up 12 lines
        12j = down 12 lines

    ctrl+u = goes up by a half page
    ctrl+d = goes down by a half page
    { = goes up by empty lines
    } = goes down by empty lines
    ci} = delete everything inside { } and start insert mode
    di} = delete everything inside { }
    di) = delete everything inside ( ) 
    vi] = select everything inside [ ]  
    diw = delete the surrounding letter of the current word 
    ```

4. Full vim movements 
   
    ```
    :e + <path> = open a new file
    ctrl + ^ = move between 2 files 
    :Ex = explore folders/files    
    ctrl + w = window control 
    ctrl + w + v = split vertically
    ctrl + w + s = splot horizontally
    ctrl + w + o = close all but your current buffer
    :resize 10 = resize horizontally
    :vertical resize 20 = resize vertically 
    ctrl + w += =  resize evenly spread
    ctrl + w + l = goes to the right window
    ctrl + w + h = goes to the left window
    
    #Say you want a file tree + another tab, follow this
    vi
    ctrl + w + v 
    :Ex
    :vertical resize 20

    ```

## 15 - NeoVim-lua 

+ Check tutorial [here](https://github.com/fcarvalhopacheco/HOW2/blob/master/4.nvim_lua/nvim_lua.md)
