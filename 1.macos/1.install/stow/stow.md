# How to manage my configuration dotfiles

- Note:  I'm using  `macos 13.2`

## Reference: 

+ [Jake Wiesler](https://www.jakewiesler.com/blog/managing-dotfiles)   
+ [Geekmasher](https://geekmasher.dev/dotfiles-guide/)

## Next steps:

1. Create an `install.sh` script
2. How to install in other machines... 
    - use nixOS?


## 1. Download stow

```sh 
brew install stow
```


## 2. Create a `.dotfiles` directory

```sh 
mkdir ~/.dotfiles
```

## 3. Create `packages` subdirectories

```sh 
cd ~/.dotfiles/

mkdir nvim
mkdir zsh
mkdir git
```

+  `$HOME` is the the `target` 
+ `.dotfiles` is the the `stow` directory. 
+ `subdirectories` are the packages with dotfile contents.

## 4. Move original and stow it

1. `zsh`

    ```sh
    cd ~
    mv .zshrc ~/.dotfiles/zsh/.zshrc
    mv .p10k.zsh ~/.dotfiles/zsh/.p10k.zsh
    mv .zprofile ~/.dotfiles/zsh/.zprofile
    cd ~/.dotfiles/
    stow zsh 
    ```

+ There is no output but you will see symlinks...

2. `git`

    ```sh 
    mv ~/.gitignore_global ~/.dotfiles/git/.gitignore_global
    mv ~/.gitconfig ~/.dotfiles/git/.gitconfig

    cd  ~/.dotfiles/
    stow git
    ```

3. `nvim`

    ```sh 
    mkdir ~/.dotfiles/nvim/.config/nvim
    mv ~/.config/nvim ~/.dotfiles/nvim/.config/
    cd ~/.dotfiles/
    stow nvim
    ```
    

