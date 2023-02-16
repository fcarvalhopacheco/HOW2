# Neovim RC from scratch with lua 

- [Reference 1](https://www.youtube.com/watch?v=w7i4amO_zaE)

## Contents

1. [Download](#1-download-neovim)
2. [Initial Configuration](#2-initial-configuration)
3. [Remap(1)](#3-remap1)
4. [Plugins](#4-plugins)
    - [packer](#packer)
    - [telescope](#telescope)
    - [markdown-preview](#markdown-preview)
    - [treesitter](#treesitter)
    - [undotree](#undotree)
    - [lspzero](#lspzero)
    - [harpoon](#harpoon)
    - [autopairs](#autopairs)
    - [comments](#comments)
    - [fugitive](#fugitive)
5. [Options](#5-options)
6. [Colorschemes](#6-colorschemes)
7. [Remap(2)](#7-remap2)

## Folder structure 
- `~/.config/nvim/`

    ```sh 
    ├── after
    │   └── plugin
    │       ├── autopairs.lua
    │       ├── colors.lua
    │       ├── comment.lua
    │       ├── fugitive.lua
    │       ├── harpoon.lua
    │       ├── lsp.lua
    │       ├── telescope.lua
    │       ├── treesitter.lua
    │       └── undotree.lua
    ├── init.lua
    ├── lua
    │   └── user
    │       ├── init.lua
    │       ├── keymaps.lua
    │       ├── options.lua
    │       └── plugins.lua
    └── plugin
        └── packer_compiled.lua
    ```

## 1. Download Neovim

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


## 3. REMAP(1)  

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

    ```python 
    
    ```

## 4. PLUGINS

### [packer](https://github.com/wbthomason/packer.nvim)

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


### [`telescope`](https://github.com/nvim-telescope/telescope.nvim)

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



### [`markdown-preview`](https://github.com/iamcco/markdown-preview.nvim)

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


### [`treesitter`](https://github.com/nvim-treesitter/nvim-treesitter)

1. Go to [Treesitter](https://github.com/nvim-treesitter/nvim-treesitter), and
copy the following:

    ```lua 
    Plug 'nvim-treesitter/nvim-treesitter', {'do': ':TSUpdate'}
    ```

2. Add/Edit the above into `~/.config/nvim/lua/user/plugins.lua` as:

    ```lua
    use('nvim-treesitter/nvim-treesitter', {run = ':TSUpdate'})
    ```
    > :w :so :PackerSync --> if not done automatically yet


3. Create a new filew at `~/.config/nvim/after/plugin/treesitter.lua` and add
following from treesiter website:

    ```lua

    require'nvim-treesitter.configs'.setup {
      -- A list of parser names, or "all" (the four listed parsers should always be installed)
      ensure_installed = { "c", "lua", "vim", "help", "bash", "awk", "bibtex",
      "dockerfile","json", "latex", "markdown", "python" ,"markdown_inline"},

      -- Install parsers synchronously (only applied to `ensure_installed`)
      sync_install = false,

      -- Automatically install missing parsers when entering buffer
      -- Recommendation: set to false if you don't have `tree-sitter` CLI installed locally
      auto_install = true,

      highlight = {
        -- `false` will disable the whole extension
        enable = true,

        -- Setting this to true will run `:h syntax` and tree-sitter at the same time.
        -- Set this to `true` if you depend on 'syntax' being enabled (like for indentation).
        -- Using this option may slow down your editor, and you may see some duplicate highlights.
        -- Instead of true it can also be a list of languages
        additional_vim_regex_highlighting = false,
      },
    }
    ```



### [`undotree`](https://github.com/mbbill/undotree)

1. Go to [Undotree](https://github.com/mbbill/undotree), and copy the following
into `~/.config/nvim/lua/user/plugins.lua`

    ```lua
	use 'mbbill/undotree'
    ```
2. Create and edit the following `~/.config/nvim/after/plugins/undotree.lua`

    ```lua 
    vim.keymap.set("n", "<leader>u", vim.cmd.UndotreeToggle)
    ```

    > Now you can type <leader>u (which is Space + u) to see everthing we have
    done. THIS IS INSAGE GOOD! It is like a realtime controlversion of the files
    with realtime branches like git


### [`lspzero`](https://github.com/VonHeikemen/lsp-zero.nvim#installing)


1. Go to [LSP Zero](https://github.com/VonHeikemen/lsp-zero.nvim#installing),
copy the following and into  `~/.config/nvim/lua/user/plugins.lua`

    ```lua
    use {
      'VonHeikemen/lsp-zero.nvim',
      branch = 'v1.x',
      requires = {
        -- LSP Support
        {'neovim/nvim-lspconfig'},             -- Required
        {'williamboman/mason.nvim'},           -- Optional
        {'williamboman/mason-lspconfig.nvim'}, -- Optional

        -- Autocompletion
        {'hrsh7th/nvim-cmp'},         -- Required
        {'hrsh7th/cmp-nvim-lsp'},     -- Required
        {'hrsh7th/cmp-buffer'},       -- Optional
        {'hrsh7th/cmp-path'},         -- Optional
        {'saadparwaiz1/cmp_luasnip'}, -- Optional
        {'hrsh7th/cmp-nvim-lua'},     -- Optional

        -- Snippets
        {'L3MON4D3/LuaSnip'},             -- Required
        {'rafamadriz/friendly-snippets'}, -- Optional
      }
    }

    ```

2. Create and edit the following file `~/.config/nvim/after/plugin/`.

    ```lua
    local lsp = require('lsp-zero').preset({
      name = 'minimal',
      set_lsp_keymaps = true,
      manage_nvim_cmp = true,
      suggest_lsp_servers = false,
    })

    -- (Optional) Configure lua language server for neovim
    lsp.nvim_workspace()

    lsp.setup()
    ```
    > Type :Mason to install whatever you like

### [`harpoon`](https://github.com/ThePrimeagen/harpoon)

1. Copy and paste the following into `~/.config/nvim/lua/user/plugins.lua`

    ```lua
    use('theprimeagen/harpoon')
    ```

2. Create and edit the following `~/.config/nvim/after/plugin/harpoon.lua`

    ```lua 
    local mark = require("harpoon.mark")
    local ui = require("harpoon.ui")

    vim.keymap.set("n", "<leader>a", mark.add_file)
    vim.keymap.set("n", "<C-e>", ui.toggle_quick_menu)
    vim.keymap.set("n", "<C-g>", function() ui.nav_file(1) end)
    vim.keymap.set("n", "<C-t>", function() ui.nav_file(2) end)
    vim.keymap.set("n", "<C-n>", function() ui.nav_file(3) end)
    vim.keymap.set("n", "<C-s>", function() ui.nav_file(4) end)
    ```

+ Now press `Ctrl + e` to see the harpoon menu. It should be empty
+ press `<leader>a` == `Space + a` to add the current file to harpoon menu
+ press `<leader>pf` == `Space +pf` to project finder files and select and 
load any file you want.
+ Inside the new file press `<leader>a` to add the new file to harpoon
+ If you want to switch 1 <--> 2, select 1 or 2 and (j or k), select 
visual mode (V), then (D)elete it, move up (k) and paste (P). save it (:w)

+ Now you can type `Ctrl + h` and `Ctrl + t` to move between two files!. 

    `--> THIS IS SICKKKKKKKKKK!`


### [`autopairs`](https://github.com/windwp/nvim-autopairs)

1. Go to [nvim-autopairs](https://github.com/windwp/nvim-autopairs) and copy
the following into `~/.config/nvim/lua/user/plugins.lua`.

    ```sh 
    use {
        "windwp/nvim-autopairs",
        config = function() require("nvim-autopairs").setup {} end
    }
    ```
2. Add/edit the following into `~/.config/nvim/after/plugin/autopairs.lua` 

    ```lua 
    require('nvim-autopairs').setup({
      disable_filetype = { "TelescopePrompt" , "vim" },
    })


    -- If you want insert `(` after select function or method item
    local cmp_autopairs = require('nvim-autopairs.completion.cmp')
    local cmp = require('cmp')
    cmp.event:on(
      'confirm_done',
      cmp_autopairs.on_confirm_done()
    )

    local npairs = require("nvim-autopairs")
    local Rule = require('nvim-autopairs.rule')

    npairs.setup({
        check_ts = true,
        ts_config = {
            lua = {'string'},-- it will not add a pair on that treesitter node
            javascript = {'template_string'},
            java = false,-- don't check treesitter on java
        },
        fast_wrap = {
            map = '<M-e>',
            chars = { '{', '[', '(', '"', "'" },
            pattern = [=[[%'%"%>%]%)%}%,]]=],
            end_key = '$',
            keys = 'qwertyuiopzxcvbnmasdfghjkl',
            check_comma = true,
            highlight = 'Search',
            highlight_grey='Comment'
        },

    })

    local ts_conds = require('nvim-autopairs.ts-conds')


    -- press % => %% only while inside a comment or string
    npairs.add_rules({
      Rule("%", "%", "lua")
        :with_pair(ts_conds.is_ts_node({'string','comment'})),
      Rule("$", "$", "lua")
        :with_pair(ts_conds.is_not_ts_node({'function'}))
    })

    ```
    > If you can't perform fast_wrap on your mac, try to do the following:
    > On Iterm2, click on `Iterm2` --> Settings --> Profiles --> Keys -->
    > Left options key: Meta instead of Normal.


### [`comments`](https://github.com/numToStr/Comment.nvim)

1. Go to [comments](https://github.com/numToStr/Comment.nvim) and copy the 
following to `~/.config/nvim/lua/user/plugins.lua`

    ```lua 
    use {
        'numToStr/Comment.nvim',
        config = function()
            require('Comment').setup()
        end
    }
    ```

2. Add/edit the following into `~/.config/nvim/after/plugin/comment.lua` 
    

    ```lua 
    require('Comment').setup()
    ```

+ Now you can use the following commands:

    - Normal mode
    
    ```help
    `gcc` - Toggles the current line using linewise comment
    `gbc` - Toggles the current line using blockwise comment
    `[count]gcc` - Toggles the number of line given as a prefix-count using linewise
    `[count]gbc` - Toggles the number of line given as a prefix-count using blockwise
    `gc[count]{motion}` - (Op-pending) Toggles the region using linewise comment
    `gb[count]{motion}` - (Op-pending) Toggles the region using blockwise comment
    ```

    - VISUAL mode

    ```help
    `gc` - Toggles the region using linewise comment
    `gb` - Toggles the region using blockwise comment
    ```

    - Extra mappings


    - NORMAL mode

    ```help
    `gco` - Insert comment to the next line and enters INSERT mode
    `gcO` - Insert comment to the previous line and enters INSERT mode
    `gcA` - Insert comment to end of the current line and enters INSERT mode
    ```


### [`fugitive`](https://github.com/tpope/vim-fugitive)

1. Add the following to `~/.config/nvim/lua/user/plugins.lua`.

    ```sh 
    use('tpope/vim-fugitive')
    ```
2. Add the following to `~/.config/nvim/after/plugin/fugitive.lua`

    ```sh 
    vim.keymap.set("n", "<leader>gs", vim.cmd.Git)
    ```

3. See some useful commands below:

+ Use  `<leader>gs` to open the Git 
+ Use  `<leader>j or <leader>k` to move between windows/bufers

    ```help
    `:Git`  - calls git status command. if you know some git you know :Git

    `:0Git` - same as begore but full screen

    `:G`    - shortcut for :Git
            - press `g?` to see the help menu with many map/keys
    ```

### `Untracked / Unstaged / Staged`
    
- You can type `:G` to see the  `git status` menu. Then 
move to any Untracked(1) or Unstaged(1) file and press `s`. 
`s` == `git add ..filename..`. Now your file is `Staged` and ready for commit.
You can also type `-` or to `Stage or Unstaged` a file. Another option 
would be `u` == `Unstage` only. 

###  




## 5. Options

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

## 6. Colorschemes

1. Go to [rose-pint](https://github.com/rose-pine/neovim)

2. Copy the following for `packer.nvim`:

    ```lua
     use({
        'rose-pine/neovim',
        as = 'rose-pine',
        config = function()
            require("rose-pine").setup()
            vim.cmd('colorscheme rose-pine')
        end
    })   

    ```


3. Write, source and Packersync.

	```sh
	:w
	:so
	:PackerSync
	```

4. Create and edit the following at `~/.config/nvim/after/plugin/colors.lua`

    ```lua
    require('rose-pine').setup({
        --- @usage 'main' | 'moon'
        dark_variant = 'main',
        bold_vert_split = false,
        dim_nc_background = false,
        disable_background = true,       -- THIS IS FALSE FROM DEFAULT
        disable_float_background = true, -- THIS IS FALSE FROM DEFAULT
        disable_italics = false,

        --- @usage string hex value or named color from rosepinetheme.com/palette
        groups = {
            background = 'base',
            panel = 'surface',
            border = 'highlight_med',
            comment = 'muted',
            link = 'iris',
            punctuation = 'subtle',

            error = 'love',
            hint = 'iris',
            info = 'foam',
            warn = 'gold',

            headings = {
                h1 = 'iris',
                h2 = 'foam',
                h3 = 'rose',
                h4 = 'gold',
                h5 = 'pine',
                h6 = 'foam',
            }
            -- or set all headings at once
            -- headings = 'subtle'
        },

        -- Change specific vim highlight groups
        highlight_groups = {
            ColorColumn = { bg = 'rose' }
        }
    })

    -- set colorscheme after options
    vim.cmd('colorscheme rose-pine')
    ```




## 7. REMAP(2) 
1. Add more remaps to `~/.config/nvim/lua/user/keymaps.lua` 


    ```lua   
    -- Modes
    --   normal_mode = "n",
    --   insert_mode = "i",
    --   visual_mode = "v",
    --   visual_block_mode = "x",
    --   term_mode = "t",
    --   command_mode = "c",
    
    -- Space == <leader>
    vim.g.mapleader = " "

    -- Normal --
    -- Better window navigation
    vim.keymap.set("n", "<C-h>", "<C-w>h", opts)
    vim.keymap.set("n", "<C-j>", "<C-w>j", opts)
    vim.keymap.set("n", "<C-k>", "<C-w>k", opts)
    vim.keymap.set("n", "<C-l>", "<C-w>l", opts)


    -- Space + pv == Netrw 
    vim.keymap.set("n", "<leader>pv", vim.cmd.Ex)

    -- When in (v)isual mode, you can press (J) or (K)
    -- to (m)ove the list down/up 
    -- BONUS: if you have a if/end statementm you can move up/down with the below
    -- command. the program will automatically indent the code!!!! INSANE GOOD
    -- test it!!!
    -- if true then
    --
    -- end
    vim.keymap.set("v", "K", ":m '<-2<CR>gv=gv")
    vim.keymap.set("v", "J", ":m '>+1<CR>gv=gv")

    -- (J) gets the line below and appends to the current line with space. However
    -- the cursor moves to the end of the line. With the remap below, your cursor
    -- will remain in the same place
    vim.keymap.set("n", "J", "mzJ`z")


    -- `Ctrl + d` and `Ctrl + u` are half page jumping + zz, the cursor  will
    -- stay in the middle of the page.
    vim.keymap.set("n", "<C-d>", "<C-d>zz")
    vim.keymap.set("n", "<C-u>", "<C-u>zz")


    -- Allow us to search terms in the middle of the page.
    vim.keymap.set("n", "n", "nzzzv")
    vim.keymap.set("n", "N", "Nzzzv")

    -- Ex: You highlight and copy a word. Then you highlight another word
    -- and you paste the old word over the new word. You will loose the yank from 
    -- the "old" word if you. The following remap <leader>p will delete the new 
    -- higlighted word into the void register and then paste it over
    -- In summary: the old(first) word will be always preserved...
    vim.keymap.set("x", "<leader>p", [["_dP]])


    -- <Space + y> will be "+y   --> This is the +register (system clipboard).
    -- It is like yanking line(s) and saving/registering it(they) into the register
    -- + 
    vim.keymap.set({"n", "v"}, "<leader>y", [["+y]])
    vim.keymap.set("n", "<leader>Y", [["+Y]])

    -- "Black hole register" == "_   
    -- The "_d" command will deleteyping "_d will delete under the cursor without 
    -- changing the unnamed register.
    vim.keymap.set({"n", "v"}, "<leader>d", [["_d]])

    -- `Space + s` will , the overall effect of this code is to remap the n key in 
    -- normal mode to perform a global search and replace operation, using the 
    -- contents of the clipboard as both the search and replacement patterns, 
    -- and then move the cursor to the left to allow you to start typing immediately 
    -- after the replace operation.

    vim.keymap.set("n", "<leader>s", [[:%s/\<<C-r><C-w>\>/<C-r><C-w>/gI<Left><Left><Left>]])
    ```



