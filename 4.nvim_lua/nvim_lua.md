# Neovim RC from scratch with lua 

- [Reference 1](https://www.youtube.com/watch?v=w7i4amO_zaE)
- [Reference 2](https://github.com/nanotee/nvim-lua-guide)


## 1. Download Neovim.

### `xubuntu 22.04`
1. Download ` nvim-linux64.deb` from [neovim](https://github.com/neovim/neovim/releases/)

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

### `mac ventura 13.2` 
1. Run:

    ```sh
    brew install neovim
    ```

## 2. Initial Configuration

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


## 3. REMAP (1)  

1. Navigate to `/.config/nvim/lua/user` directory,

    ```sh
    vim .   # navigate to /.config/nvim/lua/user
    ``` 

2. Create a new file called `keymaps.lua`

    ```sh
    %
    keymaps.lua
    ```

3. Edit the `~/.config/nmap/lua/user/keymaps.lua` file and add the following:

    ```lua
    vim.g.mapleader = " "
    vim.keymap.set("n", "<leader>pv", vim.cmd.Ex)
    ```

4. Save the file and reload 
    
    ```sh
    :w
    :so
    ```

5. Add `require` in the `/.config/nvim/lua/user/init.lua` file

    ```lua
    require("user.keymaps")
    print("hello from the user")
    ```

## 4. GETTING PLUGING

### `packer.nvim` 

1. Go to your brownser and search for:
    - [Packer nvim](https://github.com/wbthomason/packer.nvim)


2. Copy the following command into your terminal (Make sure you have git installed!:

    ```sh
    git clone --depth 1 https://github.com/wbthomason/packer.nvim\ 
    ~/.local/share/nvim/site/pack/packer/start/packer.nvim
    ```

3. Go back to the [Packer.nvim](https://github.com/wbthomason/packer.nvim#bootstrapping), add the
following commands into a new file `~/.config/nvim/lua/user/plugins.lua`   

    ```lua
    local ensure_packer = function()
      local fn = vim.fn
      local install_path = fn.stdpath('data')..'/site/pack/packer/start/packer.nvim'
      if fn.empty(fn.glob(install_path)) > 0 then
        fn.system({'git', 'clone', '--depth', '1', 'https://github.com/wbthomason/packer.nvim', install_path})
        vim.cmd [[packadd packer.nvim]]
        return true
      end
      return false
    end

    local packer_bootstrap = ensure_packer()

	-- Autocommand that reloads neovim whenever you save the plugins.lua file
	vim.cmd([[
	  augroup packer_user_config
	    autocmd!
	    autocmd BufWritePost plugins.lua source <afile> | PackerSync
	  augroup end
	]])

	-- Use a protected call so we don't error out on first use
	local status_ok, packer = pcall(require, "packer")
	if not status_ok then
	  return
	end

	-- Have packer use a popup window
	packer.init({
	    display = {
	      open_fn = function()
		return require('packer.util').float({ border = 'single' })
	      end
	    }
	  }
	)

    -- Use a protected call so we don't error out on first use
    local status_ok, packer = pcall(require, "packer")
    if not status_ok then
        return
    end

    -- Have packer use a popup window
    packer.init({
        display = {
            open_fn = function()
                return require("packer.util").float({ border = "rounded" })
            end,
        },
    }) 

    return require('packer').startup(function(use)
      use 'wbthomason/packer.nvim'
      -- My plugins here
      -- use 'foo1/bar1.nvim'
      -- use 'foo2/bar2.nvim'

      -- Automatically set up your configuration after cloning packer.nvim
      -- Put this at the end after all plugins
      if packer_bootstrap then
        require('packer').sync()
      end
    end)
    ```



4. Write, and source and reopen `plugins.lua` file
    
    ```sh
    :w
    :so
    :PackerSync
    ```

### `telescope.nvim`

+ Requirement! Please install the following :

    ```sh
    # XUBUNTU
    sudo apt-get install ripgrep
    
    # MACBOOK
    brew install ripgrep
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
3. Insert the above into `plugins.lua` before the `end)`. you should have
something like: 

    ```lua
    
    return require('packer').startup(function(use)
        use 'wbthomason/packer.nvim'
        use {
            'nvim-telescope/telescope.nvim', tag = '0.1.1',
            -- or                            , branch = '0.1.x',
            requires = { {'nvim-lua/plenary.nvim'} }
        }
        -- My plugins here
        -- use 'foo1/bar1.nvim'
        -- use 'foo2/bar2.nvim'

        -- Automatically set up your configuration after cloning packer.nvim
        -- Put this at the end after all plugins
        if packer_bootstrap then
            require('packer').sync()
        end
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

5. Create new directories/files at `~/.config/nvim/after`:

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

6. Go to [telescope.vim usage](https://github.com/nvim-telescope/telescope.nvim/blob/master/README.md#usage)
and copy the following:

    ```lua
    local builtin = require('telescope.builtin')
    vim.keymap.set('n', '<leader>pf', builtin.find_files, {})
    ```

7. Paste the above into `~/.config/nvim/after/plugin/telescope.lua`

8. Edit `~/.config/nvim/after/plugin/telescope.lua` with some new remaps...
    
    + Check [here](https://github.com/nvim-telescope/telescope.nvim/blob/master/README.md#pickers) for more reference 

    ```lua
    local builtin = require('telescope.builtin')
    vim.keymap.set('n', '<leader>pf', builtin.find_files, {})
    vim.keymap.set('n', '<C-p>', builtin.git_files, {})
    vim.keymap.set('n', '<leader>ps', function() 
		    builtin.grep_string({ search = vim.fn.input("Grep > ") });
		    end)
    ```



## `markdown preview`

+ Requirements:

    ```sh
    # XUBUNTU
    sudo apt update
    sudo apt install npm

    # MACBOOK
    brew install npm
    ```

1. Copy the following into `~/.config/nvim/lua/user/plugins.lua`

    ```lua
    use({ "iamcco/markdown-preview.nvim", run = "cd app && npm install", setup = function() vim.g.mkdp_filetypes = { "markdown" } end, ft = { "markdown" }, })
    ```


## 6. Options

+ Now you can remove `print("hello")` from `~/.config/nvim/init.lua`
+ Now you can remove `print("hello from the user")` from `~/.config/nvim/user/init.lua`

1. Added the following into `~/.config/nvim/lua/user/init.lua`
    ```sh
    require("user.options")
    ```
 
2. Create a new file at `~/.config/nvim/lua/user/options.lua`
    
    ```sh
    vim .
    %
    options.lua
    ```

3. Add the following into `options.lua`

    ```lua
    -----------------------------------------------------------
    -- General Neovim settings and configuration
    -----------------------------------------------------------

    -- Default options are not included
    -- See: https://neovim.io/doc/user/vim_diff.html
    -- [2] Defaults - *nvim-defaults*

    local g = vim.g       -- Global variables
    local opt = vim.opt   -- Set options (global/buffer/windows-scoped)

    -----------------------------------------------------------
    -- General
    -----------------------------------------------------------
    opt.mouse = 'a'                       -- Enable mouse support
    opt.clipboard = 'unnamedplus'         -- Copy/paste to system clipboard
    opt.swapfile = false                  -- Don't use swapfile
    opt.completeopt = {'menuone,noinsert,noselect'}  -- Autocomplete options

    -----------------------------------------------------------
    -- Neovim UI
    -----------------------------------------------------------
    opt.number = true           -- Show line number
    opt.showmatch = true        -- Highlight matching parenthesis

    opt.foldmethod = 'marker'   -- Enable folding (default 'foldmarker')
    opt.colorcolumn = '79'      -- Line lenght marker at 80 columns
    opt.splitright = true       -- Vertical split to the right
    opt.splitbelow = true       -- Horizontal split to the bottom
    opt.ignorecase = true       -- Ignore case letters when search
    opt.smartcase = true        -- Ignore lowercase for the whole pattern
    opt.linebreak = true        -- Wrap on word boundary
    opt.termguicolors = true    -- Enable 24-bit RGB colors
    opt.laststatus=3            -- Set global statusline
    opt.guifont = "monospace:h17" -- the font used in graphical neovim applications
    opt.cmdheight = 2           -- more space in the neovim command line for displaying messages
    opt.cursorline = true       -- highlight the current line
    opt.relativenumber = true   -- set relative numbered lines

    -----------------------------------------------------------
    -- Tabs, indent and others
    -----------------------------------------------------------
    opt.expandtab = true        -- Use spaces instead of tabs
    opt.shiftwidth = 4          -- Shift 4 spaces when tab
    opt.tabstop = 4             -- 1 tab == 4 spaces
    opt.smartindent = true      -- Autoindent new lines

    opt.numberwidth = 4         -- set number column width to 2 {default 4}
    opt.signcolumn = "yes"      -- always show the sign column, otherwise it would shift the text each time
    opt.wrap = false            -- display lines as one long line
    opt.scrolloff = 8           -- is one of my fav
    opt.sidescrolloff = 8 
    opt.expandtab = true        -- convert tabs to spaces
    -----------------------------------------------------------
    -- Memory, CPU
    -----------------------------------------------------------
    opt.hidden = true           -- Enable background buffers
    opt.history = 100           -- Remember N lines in history
    opt.lazyredraw = true       -- Faster scrolling
    opt.synmaxcol = 240         -- Max column for syntax highlight
    opt.updatetime = 250        -- ms to wait for trigger an event

    -----------------------------------------------------------
    -- Others
    -----------------------------------------------------------

    opt.backup = false          -- creates a backup file
    opt.conceallevel = 0        -- so that `` is visible in markdown files
    opt.fileencoding = "utf-8"  -- the encoding written to a file
    opt.hlsearch = false        -- highlight all matches on previous search pattern
    opt.incsearch = true
    opt.pumheight = 10          -- pop up menu height
    opt.timeoutlen = 1000       -- time to wait for a mapped sequence to complete (in milliseconds)
    opt.undofile = true         -- enable persistent undo
    opt.writebackup = false     -- if a file is being edited by another program (or was written to file while editing with another program), it is not allowed to be edited
    opt.undodir = os.getenv("HOME") .. "/.vim/undodir" 

    g.mapleader = " "
    opt.shortmess:append "c"

    ```


## 7. Colorschemes

1. Go to [ ]()

2. Copy the following for `packer.nvim`:

    ```lua
    

    ```

3. Paste the above into `~/.config/nvim/lua/user/plugins.lua`. You should have shomething like:

	```lua

	```

4. Write, source and Packersync.

	```sh
	:w
	:so
	:PackerSync
	```




- Structure MAP GUIDE :

    ```sh
    📂 ~/.config/nvim
    ├── 📁 after
    ├── 📁 ftplugin
    ├── 📂 lua
    │  └── 📂 user
    │     ├── 🌑 init.lua
    │     ├── 🌑 keymaps.lua
    │     └── 🌑 init.lua
    ├── 📁 pack
    ├── 📁 plugin
    ├── 📁 syntax
    └── 🇻 init.vim
    ```
