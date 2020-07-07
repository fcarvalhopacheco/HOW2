# macOS Catalina 10.15.5
This is my guide to configure a macOS Catalina system.  

## My Iterm2 
![my iterm2](https://github.com/fcarvalhopacheco/HOW2/blob/master/1.macos_catalina_setup/my_iterm2.png)


## Table of Contents
1. [Homebrew](#homebrew)
    * Free open-source package managements system that simplifies the installation of software on macOS and Linux
    * Similar to apt-get from Ubuntu

2. [CASK](#2---cask)
    * It is an extension to brew to install GUI applications (eg. Google Chrome, dropbox ...

3. [ITERM2](#3---iterm2) 
    * It has better color themes than the built in Terminal.
    1. [ITERM2COLORS](http://iterm2colorschemes.com/)

4. [ZSH](#4---zsh)
    * >*Unix shell that can be used as an interactive login shell and as a command interpreter for shell scripting. Zsh is a  extended Bourne shell with many improvements.* [source](https://en.wikipedia.org/wiki/Z_shell)
    * ZSH is now the default on macOS Catalina. [source](https://support.apple.com/en-us/HT208050)

5. [Oh my ZSH](#5---oh-my-zsh)
    * Open source, community-driven framework for managing your zsh configuration. [source](https://github.com/ohmyzsh/ohmyzsh)

6. [Powerlevel10k](#6---powerlevel10k)
    * Nice theme! [source](https://github.com/romkatv/powerlevel10k/blob/master/README.md#recommended-meslo-nerd-font-patched-for-powerlevel10k)

7. [Fonts](#7---patched-font)
   * Multiple fonts for your terminal

8. [Theme and Font configuration](#8---theme-configuration)

9. [Auto Suggestion](#9---auto-suggestion)
   * Did you forget how to type a command ? try to use this auto suggestion...
    
10. [GIT](#10---git)

11. [VirtualBOX](#11---virtualbox)

12. [Python Enviroment](#12---python-enviroment)

-----------------------------------------------------------------------------------

## 1 - Homebrew [](#){name=homebrew}

   1. On terminal, type:
      ```sh
      # Download
      /usr/bin/ruby -e "$(curl -fsSL  https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
## 2 - CASK
   1. On terminal, type:
      ```sh
      #Install
      $brew install cask 
      ```
## 3 - ITERM2
   1. On terminal, type:
      ```sh
      # Install
      $brew cask install iterm2
      ``` 
   2. Download ITERM2 color themes by clicking on:
      [iterm2colorschemes](https://github.com/mbadolato/iTerm2-Color-Schemes/zipball/master)

## 4 - ZSH
   1. If you dont have **Z shell** already. On terminal, type:
      ```sh
      #Install
      $brew install zsh
      ``` 
## 5 - Oh My ZSH
   1. On terminal, type:
      ```sh
      #Download
      $sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
      ```
      or
      ```sh
      $sh -c "$(wget -O https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
      ```
      
## 6 - Powerlevel10k
   1. On terminal, type:
      ```sh
      # Clone powerlevel10k
      $git clone --depth=1 https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k
      ```
      
   2. Edit the file ~/.zshrc. On terminal, type:
      ```sh
      # Navigate to home
      $cd
      # Open the file
      $vi .zshrc
      ```
   3. Navigate to ~line 11, and change ZSH_THEME, then exit the file.
      ```sh
      # Insert the text
      i ZSH_THEME="powerlevel10k/powerlevel10k"
      # Get out of vim
      esc
      :wq
      ```
## 7 - Fonts:
   1. Recommended: Meslo Nerd Font patched for Powerlevel10k. [source](https://awesomeopensource.com/project/romkatv/powerlevel10k)
   2. Download the following four files.
      * [MesloLGS NF Regular.ttf](https://github.com/romkatv/dotfiles-public/raw/master/.local/share/fonts/NerdFonts/MesloLGS%20NF%20Regular.ttf)
      * [MesloLGS NF Bold.ttf](https://github.com/romkatv/dotfiles-public/raw/master/.local/share/fonts/NerdFonts/MesloLGS%20NF%20Bold.ttf)
      * [MesloLGS NF Italic.ttf](https://github.com/romkatv/dotfiles-public/raw/master/.local/share/fonts/NerdFonts/MesloLGS%20NF%20Italic.ttf)
      * [MesloLGS NF Bold Italic.ttf](https://github.com/romkatv/dotfiles-public/raw/master/.local/share/fonts/NerdFonts/MesloLGS%20NF%20Bold%20Italic.ttf)
      
   3. Double-click on each file and press "Install". This will make MesloLGS NF font available to all applications on your system. Configure your terminal to use this font:
      
   
   
## 8 - Theme Configuration
   1. Customize your terminal the way you like. For new users. On terminal, type:
      ```sh
      $p10k configure
      ```
   2. How do I add username and/or hostname to the left sife of the prompt? [source](https://awesomeopensource.com/project/romkatv/powerlevel10k#how-do-i-add-username-andor-hostname-to-prompt)
      ```sh
         # open the following file
         $vi ~/.p10k.zsh
         
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
  ## 9 - Auto Suggestion
   1. [Source](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md#oh-my-zsh)
      ```sh
      # On terminal, clone the following repository into $ZSH_CUSTOM/plugins (by default ~/.oh-my-zsh/custom/plugins)
      $git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

      # Open ~/.zshrc, by typing:
      $vi ~/.zshrc
      
      # Find the line that starts with plugin, and add zsh-autosuggestions inside the parenthesis
      plugins=(git zsh-autosuggestions)
      
      # Save and close the file
      esc
      :wq!
      
      # Open a new terminal to see the changes
      ```
      
## 10 - Git
   1. I already have git on my ubuntu machine and a github account. So I need to link both computers to the same github account
   2. I will be following instructions from [here](https://help.github.com/en/github)
   3. * >*At the heart of GitHub is an open source version control system (VCS) called Git. Git is responsible for everything GitHub-related that happens locally on your computer..* [source](https://help.github.com/en/github/getting-started-with-github/set-up-git)
   4. Setting up GIT
      - Download it!
      ```sh
      # Download the latest version of GIT
      # If you have followed me. you should have git already install at this moment but if not, type:
      $brew install git
      
      # or Update it
      $brew upgrade git
      ```
      
      - Set an username [source](https://help.github.com/en/github/using-git/setting-your-username-in-git)
      ```sh
      # This config set up is useful to track your git commits!
      # Your name will be visible in future commits you push 
      # to GitHub from the command line. By the way, if you 
      # already have an username in other machine, dont worry.
      # It looks like that using git config here will only affect 
      # future commits and will not change anything from past commits.
      
      # USERNAME FOR EVERY REPOSITORY YOU CREATE!
      # On Terminal, type:
      $git config --global user.name "YOUR NAME OR NICKNAME HERE-GLOBAL"
       
      # Check if it is correct by typing:
      $git config --global user.name
      
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
      
      
      - Set your commit email [source](https://help.github.com/en/github/setting-up-and-managing-your-github-user-account/setting-your-commit-email-address)
      
      - Setting your commit email address in Git
      ```sh
      # On Terminal,
      $ git config --global user.email "youremailhere@test.com"

      # Check if your emails is correct
      $ git config --global user.email

      > youremailhere@test.com
      ```
   
  ## 11 - Virtualbox	
   1. I currently use virtual box to process Shipboard ADCP data, but I will soon start playing with LINUX practices and want to have a dedicated computer for it. 
  
      - Download the VirtualBOX by,
      ```sh
      # On Terminal, type:
      $brew cask install virtualbox

      # Check the version:
      $brew cask info virtualbox

      #Clen any old version installed on computer
      $brew clean up

      #Open VirtualBox:
      $virtualbox 

      ```  
   
  ## 12 - Python Enviroment
   1. There are many ways to install/create Python working Enviroments. However, I will be using conda package manager with miniconda and the conda-forge package collection, which provides platform-independent package management for Python and other softwares in self-contained user-specific enviroments. 

   2. Why this way? It seems the science community has adopted Anaconda (=miniconda+150packages) distribution to create and manage python project enviroments. Please check [Introduction to Conda for (Data) Scientists](https://carpentries-incubator.github.io/introduction-to-conda-for-data-scientists/setup/) to learn more about it. Ps. miniconda(=conda+python+basic packages) is the small version of anaconda.  

   3. Other ways? Please check [The definitive guide to setup my Python workspace](https://medium.com/@henriquebastos/the-definitive-guide-to-setup-my-python-workspace-628d68552e14), by Henrique Bastos. Its a great tutorial to config your machine with pyenv, virtualenv ... 

      - Download the Miniconda installer,
      [Miniconda](https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh)
      
      ```sh
      # On Terminal, navigate to:
      $cd Downloads

      # Install Miniconda by typing:
      $zsh Miniconda3-latest-Linux-x86_64.sh  	

      # Follow the instructions on terminal. 
      # If you forget to press NO to auto_activate miniconda every time you open a new sessiong type:
      # conda config --set auto_activate_base false	 

      # Once the install script completes, you can remove it 
      $ rm -rf Miniconda3-latest-MacOSX-x86_64.sh
	
      # Verify your Conda installation:
      $conda help
      $conda -V

      # Check the path by typing:
      $whence -p conda #or 
      $type conda  # For bash terminal, type: which conda -> The equivalent to zsh's which in bash is type. 
      
      # Make sure you have the most recent version
      $conda update --name base --channel defaults --yes conda

      # Initialize your shell for Conda
      $conda init zsh

      ```  
   
   
   
