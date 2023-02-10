# Neovim RC from scratch with lua (XUBUNTU 22.04)

- [Reference 1](https://www.youtube.com/watch?v=w7i4amO_zaE)
- [Reference 2](https://github.com/nanotee/nvim-lua-guide)



##  Download Neovim.

1. Download ` nvim-linux64.deb` from
[neovim](https://github.com/neovim/neovim/releases/)


2. Run the following command at the correct folder:

    ```sh 
    sudo apt install ./nvim-linux64.deb
    ```

3.  Add alias for nvim if you want...

    ```sh
    vi ~/.bashrc
    alias vim='nvim'
    alias vi='nvim'
    ```


## Initial Configuration

1. Navigate to config folder:

    ```sh
    cd ~/.config 
    ```

2. Create the `/nvim` folder and navigate to it.


    ```sh
    vim .
    
    # Type `d` to create a directory using NetRW listing
    d

    # Type:
    nvim

    ```

3. Create & edit  a `init.lua` file.

    ```sh
    vim .
    
    # Inside the vim NetRW tpye `%` (without ` `)
    %

    # Type the filename
    init.lua
    ```

4. Add the following on your `~/.config/nvim/init.lua` file
    
    ```sh
    print("hello")
    ```
    > once you save/exit and reopen vim, you should be able to see hello in
    > the bottom of the file. 


5. Create some directories/files inside `~/.config/nvim`

    ```sh
    vim .

    # Navigate to ~/.config/nvim/ and type `d` --> without ` `.
    d 

    # Write the foldername:
    lua

    # Enter `lua` and create a new directory called `user` or whatever you want
    d
    user

    # Enter the `user` folder  and create a file named `init.lua` using the `%` sign
    %
    init.lua 
    
    # Edit `init.lua` with the following:
    print("hello from the user folder"

    # Type `:Ex` to get back to the explore page
    :Ex

    # Navigate back to `~/.config/nvim' and add the following on `init.lua`
    require("user")
    print("hello)

    # Quit and open the file
    :wq
    vim .

    ``` 
    > Now when you reopen any file you should see:

    ```sh
    hello from the user
    helo
    Press ENTER or type command to continue:
    ```


## REMAP

1. Navigate to `/.config/nvim/lua/user` directory,

    ```sh
    vim .   # navigate to /.config/nvim/lua/user
    ``` 

2. Create a new file called `remap.lua`

    ```sh
    %
    remap.lua
    ```

3. Edit the `~/.config/nmap/lua/user/remap.lua` file and add the following:

    ```sh
    vim.g.mapleader = " "
    vim.keymap.set("n", "<leader>pv", vim.cmd.Ex)
    ```

4. Save the file and reload 
    
    ```sh
    :wq
    :so
    ```

5. Add `require` in the `/.config/nvim/lua/user/init.lua` file

    ```sh
    require("user.remap")
    print("hello from the user")
    ```

## GETTING PLUGING



- Structure MAP GUIDE :

    ```sh
    📂 ~/.config/nvim
    ├── 📁 after
    ├── 📁 ftplugin
    ├── 📂 lua
    │  └── 📂 user
    │     ├── 🌑 init.lua
    │     ├── 🌑 remap.lua
    │     └── 🌑 init.lua
    ├── 📁 pack
    ├── 📁 plugin
    ├── 📁 syntax
    └── 🇻 init.vim
    ```
