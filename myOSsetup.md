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
  1. [ITERM2](http://iterm2colorschemes.com/)
4. [ZSH - Z shell][(#zsh)
   >* Unix shell that can be used as an interactive login shell and as a command interpreter for shell scripting. Zsh is a extended Bourne shell with many improvements.* [source](https://en.wikipedia.org/wiki/Z_shell)
   * ZSH is now the default on macOS Catalina. [source](https://support.apple.com/en-us/HT208050)
5. [Oh my ZSH(#oh-my-zsh)
   * Open source, community-driven framework for managing your zsh configuration. [source](https://github.com/ohmyzsh/ohmyzsh)



-----------------------------------------------------------------------------------

## Step 1: Download and install
  ### Homebrew
  1. On terminal, type:
    
  ```sh
  /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
  ```

  ### CASK
  1. On terminal, type:
  ```sh
  brew install cask 
  ````
    
  ### ITERM2
  1. On terminal, type:
  ```sh
  brew cask install iterm2
  ``` 
  2. Download ITERM2 color themes by clicking on:
    * [iterm2colorschemes](https://github.com/mbadolato/iTerm2-ColorSchemes/zipball/master)

  3. Configure the new color. Open Iterm2, click on Preferences -> Click on Profiles -> Click on Colors -> Click Colors preset -> Scroll down and click on Import -> Navigate to the place you just downloaded the themes -> Click on Scheme -> Select all files -> Click Ok -> Choose one that you like! =)

  ### ZSH
  1. If you dont have **Z shell** already. On terminal, type:
  ```sh
  brew install zsh
  ``` 
   
  ### Oh My ZSH
  ```sh
  sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
  ```
  or
  ```sh
  sh -c "$(wget -O https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
 ```
  1.. Edit the file ~/.zshrc. On terminal, type:
    ```sh
    cd
    vi .zshrc
    ```
    - Navigate to ~line 11, and change ZSH_THEME to ZSH_THEME="agnoster", then exit the file.
    ```sh
    i ZSH_THEME="agnoster"
    :wq
    ```


  
    
