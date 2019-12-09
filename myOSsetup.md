# macOS Catalina 10.15.1
This is my configuration and set up for macOS Catalina system 

## Table of Contents
1. [Homebrew](#1---homebrew)
    * Free open-source package managements system that simplifies the installation of software on macOS and Linux
    * Similar to apt-get from Ubuntu
1. [CASK](#2---cask)
    * It is an extension to brew to install GUI applications (eg. Google Chrome, dropbox ...
1. [ITERM2](#3---iterm2) 
    * It has better color themes than the built in Terminal.
    1. [ITERM2COLORS](http://iterm2colorschemes.com/)
1. [ZSH](#4---zsh)
    * >*Unix shell that can be used as an interactive login shell and as a command interpreter for shell scripting. Zsh is a  extended Bourne shell with many improvements.* [source](https://en.wikipedia.org/wiki/Z_shell)
    * ZSH is now the default on macOS Catalina. [source](https://support.apple.com/en-us/HT208050)
1. [Oh my ZSH](#5---oh-my-zsh)
    * Open source, community-driven framework for managing your zsh configuration. [source](https://github.com/ohmyzsh/ohmyzsh)
1. [Powerlevel10k](#6---powerlevel10k)
    * Nice theme! [source](https://github.com/romkatv/powerlevel10k/blob/master/README.md#recommended-meslo-nerd-font-patched-for-powerlevel10k)
1. [Fonts](#7---patched-font)
   * Multiple fonts for your terminal
1. [Configuration](#8---configuration)

-----------------------------------------------------------------------------------

  ## 1 - Homebrew
   1. On terminal, type:
      ```sh
      # Download
      /usr/bin/ruby -e "$(curl -fsSL  https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```
  ## 2 - CASK
   1. On terminal, type:
      ```sh
      #Install
      brew install cask 
      ```
  ## 3 - ITERM2
   1. On terminal, type:
      ```sh
      # Install
      brew cask install iterm2
      ``` 
   2. Download ITERM2 color themes by clicking on:
      [iterm2colorschemes](https://github.com/mbadolato/iTerm2-Color-Schemes/zipball/master)

  ## 4 - ZSH
   1. If you dont have **Z shell** already. On terminal, type:
      ```sh
      #Install
      brew install zsh
      ``` 
  ## 5 - Oh My ZSH
   1. On terminal, type:
      ```sh
      #Download
      sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
      ```
      or
      ```sh
      sh -c "$(wget -O https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
      ```
      
  ## 6 - Powerlevel10k
   1. On terminal, type:
      ```sh
      # Clone powerlevel10k
      git clone --depth=1 https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k
      ```
      
   2. Edit the file ~/.zshrc. On terminal, type:
      ```sh
      # Navigate to home
      cd
      # Open the file
      vi .zshrc
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
   1. Recommended: Meslo Nerd Font patched for Powerlevel10k
   2. Download the following four files.
      * [MesloLGS NF Regular.ttf](https://github.com/romkatv/dotfiles-public/raw/master/.local/share/fonts/NerdFonts/MesloLGS%20NF%20Regular.ttf)
      * [MesloLGS NF Bold.ttf](https://github.com/romkatv/dotfiles-public/raw/master/.local/share/fonts/NerdFonts/MesloLGS%20NF%20Bold.ttf
      * [MesloLGS NF Italic.ttf](https://github.com/romkatv/dotfiles-public/raw/master/.local/share/fonts/NerdFonts/MesloLGS%20NF%20Italic.ttf)
      * [MesloLGS NF Bold Italic.ttf](https://github.com/romkatv/dotfiles-public/raw/master/.local/share/fonts/NerdFonts/MesloLGS%20NF%20Bold%20Italic.ttf)
      
   5. Set this font in iTerm2 (iTerm → Preferences → Profiles → Text → Change Font), best to do this for "Font" and for "Non-ASCII Font". Restart iTerm2 for all changes to take effect.
   
  ## 8 - Configuration
   1. Customize your terminal the way you like. For new users. On terminal, type:
      ```sh
         p10k configure
      ```
      


   
   


      


  
    
