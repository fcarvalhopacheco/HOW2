# macOS Ventura 13.2


[toc]

## My Iterm2 

![my iterm2](https://github.com/fcarvalhopacheco/HOW2/blob/master/01.macos/my_iterm2.png)


## Homebrew
    
1. Download homebrew.  
    
    ```sh
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```

## CASK
   
1. Download/install cask.  

    ```sh
    brew install cask 
    ```

## ZSH

1. Download/install zsh.

    ```sh 
    brew install zsh
    ```

2. Follow [ZSH-INSTALL-CONFIGURE](https://thevaluable.dev/zsh-install-configure-mouseless/)
tutorial for further zsh-configuration (without oh-my-zsh)


3. Check out [my zsh-dotfiles](https://github.com/fcarvalhopacheco/dotfiles/tree/main/zsh/.config/zsh)

- You might want to start with [.zshrc](https://github.com/fcarvalhopacheco/dotfiles/blob/main/zsh/.config/zsh/.zshrc)
to understand my file organization...



## ALACRITTY

+ Webpage: [alacritty](https://alacritty.org)

1. Download/install rust compiler + alacritty (MANUALLY):
   
    ```sh
    git clone https://github.com/alacritty/alacritty.git
    cd alacritty
    
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
    
    make app
    cp -r target/release/osx/Alacritty.app /Applications/
    ``` 

    > or just use `brew install --cask alacritty`

2. Download/install [`font`](https://www.nerdfonts.com):

    ```sh 
    brew tap epk/epk
    brew install --cask font-sf-mono-nerd-font
    ```

3. Post build:

    ```sh
    # cd into gitclone alacritty folder
    cd alacritty
    sudo tic -xe alacritty,alacritty-direct extra/alacritty.info

    cp ~/Documents/workspace/1.git/gitclones/alacritty/extra/completions/_alacritty /usr/local/share/zsh/site-functions
    ```

4. Create `~/.dotfiles/alacritty/.config/alacritty/` file:

    ```sh 
    mkdir -p ~/.dotfiles/alacritty/.config/alacritty/
    touch alacritty.yml
    ```

5. Edit the above:

+ See my configuration file [here](https://github.com/fcarvalhopacheco/dotfiles/blob/main/alacritty/.config/alacritty/alacritty.yml)
+ This is the original example [alacritty.yml](https://github.com/alacritty/alacritty/blob/master/alacritty.yml)


6. Download/install `color-scheme` [from here](https://github.com/alacritty/alacritty-theme)

    ```sh 
    mkdir -p ~/.dotfiles/alacritty/.config/alacritty/themes/
    git clone https://github.com/alacritty/alacritty-theme ~/.dotfiles/alacritty/.config/alacritty/themes/
    ```

    + Add an import to your alacritty.yml (Replace {theme} with your 
    desired colorscheme):

    ```yaml 
    import:
      - ~/.config/alacritty/themes/themes/{theme}.yaml
    ```

7. Stow alacritty:

    ```sh 
    cd ~/.dotfiles | stow alacritty
    ```


## TMUX

+ GitHub repository [tmux](https://github.com/tmux/tmux/wiki)

+ References: 
    
    - [How I Use Tmux With Neovim For An Awesome Dev Workflow On My Mac
](https://www.youtube.com/watch?v=U-omALWIBos)

    - [Writing Your tmux Config: a Detailed Guide](https://thevaluable.dev/tmux-config-mouseless/)

1. Download/install:

    ```sh 
    brew install tmux
    ```

2. Tips 

    ``` 
    tmux attach-session -t <session name>    # to get back to a previous session
    tmux kill-server                         # kill server + every session 
    tmux kill-session -t <session name>      # kill the session <session name>
    tmux list-sessions                       # list tmux sessions
    tmux new-session -s <session name>       # create a new session <session name>

    # Default 
    CTRL+b + "                               # split horizontally
    CTRL+d                                   # close pane
    :split-window                            # split horizontally

    # NEW MAPPING
    CTRL+a                                   = prefix key
    
    CTRL+a + r                               = reload the tmux config file
    CTRl+a + |                               = split horizontally/RIGHT 
    CTRl+a + -                               = split vertically/BELOW CTRL+a + ALT + arrow key                 = resize pane
    CTRL+a +[                                = switch to COPY MODE (q = quit)
    CTRL+a + d                               = detach from sesssion
    ```

3. Install [tmux plugin manager](https://github.com/tmux-plugins/tpm)

    ```sh 
    git clone https://github.com/tmux-plugins/tpm ~$XDG_CONFIG_HOME/tmux/plugins/tpm
    ```

+ Follow instructions from the tmux-plugin/tpm repository   


4. Create `~/.config/tmux/.tmux.conf`, and edit the file:


+ Check my configuration file [here](https://github.com/fcarvalhopacheco/dotfiles/blob/main/tmux/.config/tmux/tmux.conf)


5. Stow tmux:

    ```sh 
    cd ~/.dotfiles | stow tmux
    ```

## YABAI and SKHD

- References:

    - [How To Set up And Use The Yabai Tiling Window Manager On Mac](https://www.youtube.com/watch?v=k94qImbFKWE)
    - [YABAI](https://github.com/koekeishiya/yabai/wiki/Installing-yabai-(latest-release))
    - [SKHD](https://github.com/koekeishiya/skhd)


1. Download/install yabai and skhd:

    ```sh 
    brew install koekeishiya/formulae/yabai
    brew install koekeishiya/formulae/skhd
    ```

2. Create the following:

    ```sh
    mkdir -p ~/.dotfiles/yabai/.config/yabai
    mkdir -p ~/.dotfiles/skhd/.config/skhd
    ```

3. Create/Edit `yabairc`

- [Here is my file](https://github.com/fcarvalhopacheco/dotfiles/blob/main/yabai/.config/yabai/yabairc)

    ```sh 
    cd ~/.dotfiles/yabai/.config/yabai/ | vi yabairc
    ```
    
4. Stow the files and restart service    

    ```sh
    cd ~/.dotfiles | stow yabai
    brew services start yabai
    brew services restart yabai
    ```

5. Create/Edit `skhd`

- [Here is my file](https://github.com/fcarvalhopacheco/dotfiles/blob/main/skhd/.config/skhd/skhdrc)


    ```sh 
    cd ~/.dotfiles/skhd/.config/skhd/ | vi skhd
    ```

6. Stow the files and restart service    

    ```sh
    cd ~/.dotfiles | stow skhd
    brew services start skhd
    brew services restart skhd
    ```



## Git

* I already have git on my ubuntu machine, and a GitHub account. So I need to
link both computers to the same GitHub account

* I will be following instructions from [here](https://help.github.com/en/github)

    
1. Download git.
    
    ```sh
    $ brew install git
      
    # or Update it
    $ brew upgrade git
    ```
    
2. Setting an username [source](https://help.github.com/en/github/using-git/setting-your-username-in-git)
    
+ This config set up is useful to track your git commits! 
Your name will be visible in future commits you push 
to GitHub from the command line. By the way, if you 
already have an username in other machine, dont worry.
It looks like that using git config here will only affect 
future commits and will not change anything from past commits.

    ```sh
    # On terminal, type:
    $ git config --global user.name "YOUR NAME OR NICKNAME HERE-GLOBAL"
       
    # Check if it is correct by typing:
    $ git config --global user.name
      
    # you should see
    >YOUR NAME OR NICKNAME HERE-GLOBAL
    ```
      
3. Setting your commit address in Git [source](https://help.github.com/en/github/setting-up-and-managing-your-github-user-account/setting-your-commit-email-address)
    
    ```sh
    # On Terminal,
    $ git config --global user.email "email@example.com"

    # Check if your s is correct
    $ git config --global user.email

    > yourhere@test.com
    ```

4. Set a global ignore file 
    
    ```sh
    # navigate to home directory
    $ cd
    $ vi .gitignore_global
    ```
    >	I am using macOS, so I will be adding [macOS.gitignore](https://github.com/github/gitignore/blob/master/Global/macOS.gitignore) on my .gitignore_global
  

5. How to create a repository ? [Click here](https://docs.github.com/en/get-started/quickstart/create-a-repo)

6. How to clone a repository? [Click here](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository-from-github/cloning-a-repository)


7. How to manage a `GPG Key`: 

    + Following instructions from [here](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key)

        ```sh
        # Run the following:
        $ gpg --full-generate-key                                                                       ─╯

        gpg (GnuPG/MacGPG2) 2.2.40; Copyright (C) 2022 g10 Code GmbH
        This is free software: you are free to change and redistribute it.
        There is NO WARRANTY, to the extent permitted by law.

        Please select what kind of key you want:
        (1) RSA and RSA (default)
            (2) DSA and Elgamal
            (3) DSA (sign only)
        (4) RSA (sign only)
            (14) Existing key from card
            Your selection? 1
            RSA keys may be between 1024 and 4096 bits long.
            What keysize do you want? (3072) 4096
            Requested keysize is 4096 bits
            Please specify how long the key should be valid.
            0 = key does not expire
            <n>  = key expires in n days
            <n>w = key expires in n weeks
            <n>m = key expires in n months
            <n>y = key expires in n years
            Key is valid for? (0) 0
            Key does not expire at all
            Is this correct? (y/N) y

            GnuPG needs to construct a user ID to identify your key.

            Real name: Fernando Carvalho Pacheco
            Email address: fcarvalho.pacheco@gmail.com
        ```

    + Run: 
        ```sh
        $ gpg --list-secret-keys --keyid-format=long
        $ gpg --armor --export xxxxxxxxxxxxxxxx
        # copy the key to github.
        ```

    + Now follow [here](https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key)

        ```sh
        $ git config --global --unset gpg.format
        $ gpg --list-secret-keys --keyid-format=long
        $ git config --global user.signingkey xxxxxxxxxxxxxxxxxxx
        $ git config --global commit.gpgsign true
        ```

## Virtualbox	

* I now use virtual box to process Shipboard ADCP data, but I will soon start
  playing with LINUX practices and want to have a dedicated computer for it. 
  
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
   
## Python Environment

- There are many ways to install/create Python working Enviroments. Choose 
one from below (ps. I m using `mambaforge`):

1. `MINICONDA`

    - Miniconda is a lightweight version of the Anaconda Python distribution. 
    It is a package manager that allows users to easily install, uninstall, 
    and update Python packages and their dependencies. Miniconda comes with
    the conda package manager, a command-line tool that helps users create 
    and manage Python environments [Source: ChatGPT].

    - Why this? It seems the science community has adopted `Anaconda` 
    (=miniconda+150packages) distribution to create and manage python project 
    enviroments. Please check 
    [Introduction to Conda for (Data) Scientists](https://carpentries-incubator.github.io/introduction-to-conda-for-data-scientists/setup/) 
    to learn more about it. Miniconda is a minor version of Anaconda.
    `Miniconda`(=conda+python+basic packages) 

    * Download the Miniconda installer, [Miniconda](https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh)
          
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

2. [`MAMBA`](https://mamba.readthedocs.io/en/latest/index.html)

    - Mamba is a high-performance package manager for the Python programming 
    language, and it is an open-source project. It is designed to be a faster 
    and more efficient replacement for the conda package manager that comes 
    with the Anaconda and Miniconda Python distributions. Mamba uses the same
    package format and repository as conda, so it is fully compatible with 
    conda-managed environments and packages [Source: ChatGPT].


    - Installation Guide:

        ```sh 
        # On Terminal, navigate to:
        cd Downloads

        # Download:
        curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-$(uname)-$(uname -m).sh"

        # Install:
        # Follow the instructions on terminal. 
        sh Mambaforge-$(uname)-$(uname -m).sh

        # Once the install script completes, you can remove it 
        rm -rf Mambaforge-*
        
        # Run:
        ~/mambaforge/condabin/conda init zsh
        ~/mambaforge/condabin/mamba init zsh

        # Remove the auto_activate_base funtion:
        # This will stop terminal to Initialize the base whenever you start
        # a terminal. 
        conda config --set auto_activate_base false

        # Verify your Conda installation:
        conda -V

        # Check the path by typing:
        whence -p conda #or 
        type conda  # For bash terminal, type: which conda -> The equivalent to zsh's which in bash is type. 
          
        # Make sure you have the most recent version
        conda update --name base --channel conda-forge --yes conda

        # Initialize your shell for Conda
        conda init zsh
        ```


3. `PYENV`

    - Please check [The definitive guide to set up my Python workspace](https://medium.com/@henriquebastos/the-definitive-guide-to-setup-my-python-workspace-628d68552e14), 
    by [Henrique Bastos](https://henriquebastos.net/sobre/). It is a great 
    tutorial to config your machine with pyenv, pyenv-virtualenv and 
    pyenv-virtualenvwrapper.


## Cookiecutter

> A cross-platform command-line utility that creates projects from cookiecutters (project templates), e.g. 
> Python package projects, C projects.
   
* Original project: [https://github.com/cookiecutter/cookiecutter](https://github.com/cookiecutter/cookiecutter)
* [Check my quick tutorial here](https://github.com/fcarvalhopacheco/HOW2/blob/master/01.macos/1.install/cookiecutter/cookiecutter-guide.md) 


## Vim-commands 

1. General navigation
    
    ```
    <shift> + O = insert mode above
    <shift> + P = paste above
    <shift> + I = insert mode start at the beginning of the line 
    <shift> + A = insert mode start at the end of the line  
    ? =  Search mode -->backwards 
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

    # ILOVE THE FOLLOWING ONES:
    ci} = delete everything inside { } and start insert mode  
    di} = delete everything inside { }
    di) = delete everything inside ( ) 
    vi] = select everything inside [ ]  
    diw = delete the surrounding letter of the current word 
    ciw = delete the surrounding letter of the current word and start insert
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

## NeoVim-lua 

+ Check tutorial [here](https://github.com/fcarvalhopacheco/HOW2/blob/master/01.macos/1.install/nvim/nvim_lua.md)

## Dotfiles

+ Check tutorial [here](https://github.com/fcarvalhopacheco/HOW2/blob/master/01.macos/1.install/stow/stow.md)
