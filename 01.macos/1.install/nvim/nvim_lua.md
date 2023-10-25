# Neovim 

- Reference: 
    - [Effective Neovim Instant IDE](https://www.youtube.com/watch?v=stqUbv-5u2s)
    - [kickstart.nvim](https://github.com/nvim-lua/kickstart.nvim)

## Contents



## Folder structure

- `~/.config/nvim/`

  ```sh
    ├── LICENSE.md
    ├── README.md
    ├── doc
    │   ├── kickstart.txt
    │   └── tags
    ├── init.lua
    ├── lazy-lock.json
    └── lua
        ├── custom
        │   └── plugins
        │       ├── autopairs.lua
        │       ├── harpoon.lua
        │       ├── init.lua
        │       └── markdown.lua
        └── kickstart
            └── plugins
                ├── autoformat.lua
                └── debug.lua
  ```

## 1. Download and Install Neovim

- If necessary, make a backup of your current Neovim files:

  ```sh
  mv ~/.config/nvim{,.bak}
  mv ~/.local/share/nvim{,.bak}
  mv ~/.local/state/nvim{,.bak}
  mv ~/.cache/nvim{,.bak}
  ```

### `xubuntu 22.04`

1. Download ` nvim-linux64.deb` from [neovim](https://github.com/neovim/neovim/releases/)

2. Run the following command at the correct folder:

   ```sh
   sudo apt install ./nvim-linux64.deb
   ```

   - or install from source [Build](https://github.com/neovim/neovim/wiki/Building-Neovim#build-prerequisites)

   ```sh
   #remove first if necessary
   sudo apt-get remove neovim
   sudo apt-get install ninja-build gettext cmake g++ pkg-config unzip curl doxygen
   cd ~/Downloads
   git clone https://github.com/neovim/neovim
   cd neovim
   make
   sudo make install
   ```

3. Add alias for nvim if you want...

   ```sh
   vi ~/.bashrc
   alias vim='nvim'
   alias vi='nvim'
   ```

### `mac ventura 13.4.1`

1. Install with brew:

   ```sh
   brew install neovim
   ```

2. or Install from source:

- [Reference](https://github.com/neovim/neovim/wiki/Building-Neovim#build-prerequisites)

  1. Install Xcode Command Line Tools:

     ```bash
     xcode-select --install
     ```

  2. Install Homebrew (if not already installed):

     ```bash
     /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
     ```

  3. Install Neovim build dependencies:

     ```bash
     brew install ninja libtool gettext automake cmake pkg-config unzip curl
     ```

  4. Clone the nvim repository and build:
    
     ```bash
     git clone https://github.com/neovim/neovim.git
     cd neovim && make CMAKE_BUILD_TYPE=RelWithDebInfo
     ```

  5. Install nvim:

     ```bash
     sudo make install
     ```

## 2. Initial Configuration

1. Create the configuration folder and navigate to it:

   ```sh
   mkdir -p ~/.config/nvim && $_
   ```

2. Clone `kickstart.nvim` repository

- `git clone https://github.com/nvim-lua/kickstart.nvim.git "${XDG_CONFIG_HOME:-$HOME/.config}"/nvim`


    ```sh 
    # This is my folder at .dotfiles, which i use stow to send to ~/.config/nvim
    # I will have my own plugins here...
    git clone https://github.com/nvim-lua/kickstart.nvim.git /Users/fcp/.dotfiles/nvim/.config/nvim
    
    # This is my fork to follow the original project
    git clone git@github.com:fcarvalhopacheco/kickstart.nvim /Users/fcp/Documents/workspace/1.git/gitclones 
    ```

3. Run the following:

    ```sh 
    nvim --headless "+Lazy! sync" +qa
    ```


- For adding plugins, there are 3 primary options:
    
    - Add new configuration in `lua/custom/plugins/*` files, which will be 
    auto sourced using `lazy.nvim` (uncomment the line importing the `custom/plugins` 
    directory in the `init.lua` file to enable this)
    - Modify `init.lua` with additional plugins.
    - Include the `lua/kickstart/plugins/*` files in your configuration.



4. If you want to keep updated with upstream:

- Run:

    ```sh 
    cd /Users/fcp/Documents/workspace/1.git/gitclones/kickstart.nvim 
    git remote add upstream git@github.com:nvim-lua/kickstart.nvim.git 
    git fetch upstream
    git pull upstream
    git push origin master 
    ```

- Check diff between my fork and my .dotfiles

    ```sh 
    git diff /Users/fcp/Documents/workspace/1.git/gitclones/kickstart.nvim/init.lua /Users/fcp/.dotfiles/nvim/.config/nvim/init.lua
    ```

## 3. PLUGINS


### [`harpoon`](https://github.com/ThePrimeagen/harpoon)

1. Create and edit the following `~/.config/nvim/lua/custom/plugins/harpoon.lua`

   ```lua
   return {
   "ThePrimeagen/harpoon",
   lazy = false,
   dependencies = {
       "nvim-lua/plenary.nvim",
   },
   config = true,
   keys = {
       { "<leader>ha", "<cmd>lua require('harpoon.mark').add_file()<cr>",        desc = "[H]arpoon [A]dd file with" },
       { "<leader>hm", "<cmd>lua require('harpoon.ui').toggle_quick_menu()<cr>", desc = "[H]arpoon [M]enu" },
       { "<C-n>",      "<cmd>lua require('harpoon.ui').nav_next()<cr>",          desc = "Go to [N]ext harpoon mark" },
       { "<C-p>",      "<cmd>lua require('harpoon.ui').nav_prev()<cr>",          desc = "Go to [P]revious harpoon mark" },
       -- { "<c-z>",      "<cmd>lua require('harpoon.ui').nav_file(1)<cr>",         desc = "go to file 1" },
       -- { "<C-x>",      "<cmd>lua require('harpoon.ui').nav_file(2)<cr>",         desc = "Go to file 2" },
   },
   }
   ```

- Now press `space + h + m ` to see the harpoon menu. It should be empty
- press `<leader>ha` == `Space + h + a` to add the current file to harpoon menu
- press `<leader>?` == `Space +?` to search for recent opened files.
- Inside the new file press `<leader>a` to add the new file to harpoon
- If you want to switch 1 <--> 2, select 1 or 2 and (j or k), select
  visual mode (V), then (D)elete it, move up (k) and paste (P). save it (:w)

- Now you can type `Ctrl + n` and `Ctrl + p` to move between two files!.


### [`autopairs`](https://github.com/windwp/nvim-autopairs)

1.  Add/edit the following into `~/.config/nvim/custom/plugins/autopairs.lua`

    ```lua
    return {
    "windwp/nvim-autopairs",
    -- Optional dependency
    dependencies = { 'hrsh7th/nvim-cmp' },
    config = function()
        require("nvim-autopairs").setup {}
        -- If you want to automatically add `(` after selecting a function or method
        local cmp_autopairs = require('nvim-autopairs.completion.cmp')
        local cmp = require('cmp')
        cmp.event:on(
        'confirm_done',
        cmp_autopairs.on_confirm_done()
        )

        local npairs = require("nvim-autopairs")
        local Rule = require('nvim-autopairs.rule')
        -- put this to setup function and press <a-e> to use fast_wrap
        npairs.setup({
        fast_wrap = {},
        })
        -- change default fast_wrap
        npairs.setup({
        fast_wrap = {
            map = '<M-e>',
            chars = { '{', '[', '(', '"', "'" },
            pattern = [=[[%'%"%>%]%)%}%,]]=],
            end_key = '$',
            before_key = 'h',
            after_key = 'l',
            cursor_pos_before = true,
            keys = 'qwertyuiopzxcvbnmasdfghjkl',
            manual_position = true,
            highlight = 'Search',
            highlight_grey = 'Comment'
        },
        })
    end,
    }
    ```

### [`markdownpreview`](https://github.com/windwp/nvim-autopairs)

1.  Add/edit the following into `~/.config/nvim/lua/custom/plugins/markdown.lua`

    ```lua 
    return {
    {
        "iamcco/markdown-preview.nvim",
        build = "cd app && npm install",
        ft = "markdown",
        lazy = true,
        -- keys = { { "gm", "<cmd>MarkdownPreviewToggle<cr>", desc = "Markdown Preview" } },
        config = function()
        vim.g.mkdp_auto_close = true
        vim.g.mkdp_open_to_the_world = false
        vim.g.mkdp_open_ip = "127.0.0.1"
        vim.g.mkdp_port = "8888"
        vim.g.mkdp_browser = ""
        vim.g.mkdp_echo_preview_url = true
        vim.g.mkdp_page_title = "${name}"
        end,
    },

    }
    ```

## 4. Options


1. Add the following into `~.config/nvim/init.lua`

   ```lua

    -----------------------------------------------------------
    -- General
    -----------------------------------------------------------
    vim.o.mouse = "a"               -- Enable mouse support
    vim.o.clipboard = "unnamedplus" -- Copy/paste to system clipboard
    vim.o.swapfile = false          -- Don't use swapfile
    vim.o.completeopt = 'menuone,noselect,noinsert'


    -- Make line numbers default
    vim.wo.number = true
    vim.o.showmatch = true      -- Highlight matching parenthesis
    vim.o.foldmethod = "marker" -- Enable folding (default 'foldmarker')
    vim.o.colorcolumn = "79"    -- Line length marker at 80 columns
    vim.o.splitright = true     -- Vertical split to the right
    vim.o.splitbelow = true     -- Horizontal split to the bottom

    -- Case-insensitive searching UNLESS \C or capital in search
    vim.o.ignorecase = true
    vim.o.smartcase = true

    vim.o.linebreak = true          -- Wrap on word boundary
    vim.o.laststatus = 3            -- Set global statusline

    vim.o.guifont = "monospace:h17" -- the font used in graphical neovim applications
    vim.o.cmdheight = 2             -- more space in the neovim command line for displaying messages
    vim.o.cursorline = true         -- highlight the current line
    vim.o.relativenumber = true     -- set relative numbered lines

    -- NOTE: You should make sure your terminal supports this
    vim.o.termguicolors = true

    -- Enable break indent
    vim.o.breakindent = true

    -- Keep signcolumn on by default
    vim.wo.signcolumn = 'yes'


    -----------------------------------------------------------
    -- Tabs, indent and others
    -----------------------------------------------------------
    vim.o.textwidth = 79
    vim.o.expandtab = true   -- Use spaces instead of tabs
    vim.o.shiftwidth = 4     -- Shift 4 spaces when tab
    vim.o.shiftround = true
    vim.o.tabstop = 4        -- 1 tab == 4 spaces
    vim.o.smartindent = true -- Autoindent new lines
    vim.o.softtabstop = 4    -- Tab character that is 4 columns wide.
    vim.o.autoindent = true

    vim.o.numberwidth = 4    -- set number column width to 4 {default 4}
    vim.o.signcolumn = "yes" -- always show the sign column, otherwise it would shift the text each time
    vim.o.wrap = false       -- display lines as one long line
    vim.o.scrolloff = 8      -- Always 8 lines while moving up/down
    vim.o.sidescrolloff = 8
    vim.o.autowrite = true   -- Automatically write buffer before running certain commands, including running Lua code
    vim.o.infercase = false

    -----------------------------------------------------------
    -- Memory, CPU
    -----------------------------------------------------------
    vim.o.timeoutlen = 300
    vim.o.hidden = true     -- Enable background buffers
    vim.o.history = 100     -- Remember N lines in history
    vim.o.lazyredraw = true -- Faster scrolling
    vim.o.synmaxcol = 240   -- Max column for syntax highlight
    vim.o.updatetime = 250  -- ms to wait for trigger an event

    -----------------------------------------------------------
    -- Others
    -----------------------------------------------------------

    vim.o.backup = false         -- creates a backup file
    vim.o.conceallevel = 0       -- so that `` is visible in markdown files
    vim.o.fileencoding = "utf-8" -- the encoding written to a file
    vim.o.hlsearch = false       -- highlight all matches on previous search pattern
    vim.o.incsearch = true
    vim.o.pumheight = 10         -- pop up menu height
    vim.o.timeoutlen = 1000      -- time to wait for a mapped sequence to complete (in milliseconds)
    vim.o.undofile = true        -- enable persistent undo
    vim.o.writebackup = false    -- if a file is being edited by another program (or was written to file while editing with another program), it is not allowed to be edited
    vim.o.undodir = os.getenv("HOME") .. "/.vim/undodir"

    -- Fix markdown indentation settings
    vim.g.markdown_recommended_style = 0
    vim.g.python3_host_prog = '/usr/local/bin/python3'

   ```



## 4. REMAP

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
   -- highlighted word into the void register and then paste it over
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
