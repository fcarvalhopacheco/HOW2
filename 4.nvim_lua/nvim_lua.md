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


## REMAP (1)  

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

    ```lua
    vim.g.mapleader = " "
    vim.keymap.set("n", "<leader>pv", vim.cmd.Ex)
    ```

4. Save the file and reload 
    
    ```sh
    :wq
    :so
    ```

5. Add `require` in the `/.config/nvim/lua/user/init.lua` file

    ```lua
    require("user.remap")
    print("hello from the user")
    ```

## GETTING PLUGING

### `packer.nvim` 

1. Go to your brownser and search for:
    - [Packer.nvim](github.com/wbthomason/packer.nvim)


2. Copy the following command into your terminal (Make sure you have git installed!:

    ```sh
    git clone --depth 1 https://github.com/wbthomason/packer.nvim\
 ~/.local/share/nvim/site/pack/packer/start/packer.nvim
    ```

3. Go back to the [Packer.nvim](github.com/wbthomason/packer.nvim), add the
following commands into a new file `~/.config/nvim/lua/user/packer.lua`   

    ```lua
    -- This file can be loaded by calling `lua require('plugins')` from your init.vim

    -- Only required if you have packer configured as `opt`
    vim.cmd [[packadd packer.nvim]]

    return require('packer').startup(function(use)
      -- Packer can manage itself
      use 'wbthomason/packer.nvim'
    end)
    ```

4. Exit nvim, and reopen `packer.lua` file
5. Type `:PackerSync` to see the packer in action. It should give you a split
window telling you `Everhing already up to date!`. Then type `:q` to close it.

### `telescope.nvim`

+ Requirement! Please install the following 

	```sh
	sudo apt-get install ripgrep
	```

	> BurntSushi/ripgrep is required for live_grep and grep_string and is the first priority for find_files.


1. Go to your brownser and search for:
    - [telescope.nvim](https://github.com/nvim-telescope/telescope.nvim)

2. Copy the following:

    ```lua
    use {
        'nvim-telescope/telescope.nvim', tag = '0.1.1',
    --or                               , branch = '0.1.x',
        requires = { {'nvim-lua/plenary.nvim'} }
    }
    ```
3. Insert the above into `packer.lua` before the `end)`. you should have
something like: 

    ```lua
    -- This file can be loaded by calling `lua require('plugins')` from your init.vim

    -- Only required if you have packer configured as `opt`
    vim.cmd [[packadd packer.nvim]]

    return require('packer').startup(function(use)
            -- Packer can manage itself
            use 'wbthomason/packer.nvim'

            use {
            'nvim-telescope/telescope.nvim', tag = '0.1.1',
            -- or                            , branch = '0.1.x',
            requires = { {'nvim-lua/plenary.nvim'} }
            }

    end)
    ```
    > Pressing '=' in Normal mode alignes the current line with those above, plus indenting.



4. Write and source the file:
    
    ```sh
    :w
    :so
    :PackerSync
    :q
    ```

## REMAP (2)

1. Create new directories/files at `~/.config/nvim/after`:

    ```sh 
    vim . # or <leader>pv, if you were inside of any file
          # or just use `mkdir ~/.config/nvim/after`
   
    # Create directory from Netrw --> "vim ."
    d
    after 

    # Navigate to `~/.config/nvim/after` and create another directory called `plugin`.
    d
    plugin

    # Create a file called `telescope.lua`
    ```

2. Go to [telescope.vim usage](https://github.com/nvim-telescope/telescope.nvim/blob/master/README.md#usage)
and copy the following:

    ```lua
    local builtin = require('telescope.builtin')
    vim.keymap.set('n', '<leader>ff', builtin.find_files, {})
    ```

3. Paste the above into `~/.config/nvim/after/plugin/telescope.lua`

4. Edit `~/.config/nvim/after/plugin/telescope.lua` with some new remaps...
    
    + Check [here](https://github.com/nvim-telescope/telescope.nvim/blob/master/README.md#pickers) for more reference 

    ```lua
    local builtin = require('telescope.builtin')
    vim.keymap.set('n', '<leader>pf', builtin.find_files, {})

    ```





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
