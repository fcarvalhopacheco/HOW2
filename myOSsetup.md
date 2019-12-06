# macOS Catalina 10.15.1
This is my configuration and set up for macOS Catalina

## Table of Contents

1. [Homebrew](#homebrew)
    * I Free open-source package managements system that simplifies the installation of software on macOS and Linux
    * Similar to apt-get from Ubuntu
2. [CASK](#cask)
    * It is an extension to brew to install GUI applications (eg. Google Chrome, dropbox ...
3. [ITERM2](#iterm2) 
    * It has better color themes than the built in Terminal.
    1. [ITERM2COLORS](http://iterm2colorschemes.com/)
4. [ZSH](#zsh)
    * >*Unix shell that can be used as an interactive login shell and as a command interpreter for shell scripting. Zsh is a extended Bourne shell with many improvements.* [source](https://en.wikipedia.org/wiki/Z_shell)
    * ZSH is now the default on macOS Catalina. [source](https://support.apple.com/en-us/HT208050)
5. [Oh my ZSH](#oh-my-zsh)
    * Open source, community-driven framework for managing your zsh configuration. [source](https://github.com/ohmyzsh/ohmyzsh)
6. [Powerlevel10k](#powerlevel10k)


-----------------------------------------------------------------------------------

## Step 1: Downloading and installing
  ### Homebrew
  1. On terminal, type:
      ```sh
      /usr/bin/ruby -e "$(curl -fsSL  https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
  ### CASK
  1. On terminal, type:
      ```sh
      brew install cask 
      ```
  ### ITERM2
  1. On terminal, type:
      ```sh
      brew cask install iterm2
      ``` 
  2. Download ITERM2 color themes by clicking on:
      [iterm2colorschemes](https://github.com/mbadolato/iTerm2-Color-Schemes/zipball/master)

  ### ZSH
  1. If you dont have **Z shell** already. On terminal, type:
      ```sh
      brew install zsh
      ``` 
  ### Oh My ZSH
  1. On terminal, type:
      ```sh
      sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
      ```
      or
      ```sh
      sh -c "$(wget -O https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
      ```
      
   ### Powerlevel10k
   1. On terminal, type:
      ```sh
      git clone --depth=1 https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k
      ```
      
   2. Edit the file ~/.zshrc. On terminal, type:
      ```sh
      cd
      vi .zshrc
      ```
   3. Navigate to ~line 11, and change ZSH_THEME, then exit the file.
      ```sh
      i ZSH_THEME="powerlevel10k/powerlevel10k"
      esc
      :wq
      ```


      


  
    
