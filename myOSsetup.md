# macOS Catalina 10.15.1
My configuration and set up for macOS Catalina

- Homebrew
   * Free open-source package managements system that simplifies the installation of software on macOS and Linux
   * Similar to apt-get from Ubuntu
- CASK
  * It is an extension to brew to install GUI applications (eg. Google Chrome, dropbox ....)
  * It is your `one-way` shopping to download/install programs...
- ITERM2 
  * It has better color themes than the built in Terminal.
- ITERM2 color schemes
  * [Check this out](http://iterm2colorschemes.com/)


## Step 1: Download and install Homebrew

1. On terminal, type:

   ```sh
   /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   ```

## Step 2: Download and install CASK

1. On terminal, type:

    ```sh
    brew install cask 
    ````
    
## Step 3: Download and install ITERM2
    
1. On terminal, type:
   
   ```sh
   brew cask install iterm2
   ``` 
2. Download ITERM2 color themes by clicking on:
    * [iterm2colorschemes](https://github.com/mbadolato/iTerm2-Color-Schemes/zipball/master)
    * The theme folder should be on Downloads.
3. Configure the new color. Open Iterm2, click on Preferences -> Click on Profiles -> Click on Colors -> Click Colors preset -> Scroll down and click on Import -> Navigate to the place you just downloaded the themes -> Click on Scheme -> Select all files -> Click Ok -> Choose one that you like! =)
  
    
