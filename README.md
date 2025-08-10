# Neovim Tips Plugin

A Lua plugin for Neovim that helps you organize and search helpful tips, tricks, and shortcuts via a fuzzy search interface.

## ✨ Features
- Search tips using ultra-fast `fzf-lua` plugin
- Preview rendered descriptions in markdown format
- No additional utilities: you don't need `glow` or `bat` to render the tip
- Support for categories, tags, and rich text
- The plugin comes with a starting set of basic, predefined tips
- You can add/edit unlimited number of personal tips stored in a configurable file

## 📦 Installation

### Lazy.nvim

```lua
{
  "saxon1964/neovim-tips",
  dependencies = { "ibhagwan/fzf-lua" },
  opts = {
    -- OPTIONAL: Location of user defined tips (default value shown below)
    user_file = vim.fn.stdpath("config") .. "/neovim_tips/user_tips.txt",
  },
  init = function()
    -- OPTIONAL: Change to your liking or drop completely 
    -- The plugin does not provide default key mappings, only commands
    local map = vim.keymap.set
    map("n", "<leader>nto", ":NeovimTips<CR>", { desc = "Neovim tips", noremap = true, silent = true })
    map("n", "<leader>nte", ":NeovimTipsEdit<CR>", { desc = "Edit your Neovim tips", noremap = true, silent = true })
    map("n", "<leader>nta", ":NeovimTipsAdd<CR>", { desc = "Add your Neovim tip", noremap = true, silent = true })
  end
}
```

### packer.nvim

```lua
use {
  "saxon1964/neovim-tips",
  requires = { "ibhagwan/fzf-lua" },
  config = function()
    require("neovim-tips").setup {
      user_file = vim.fn.stdpath("config") .. "/neovim_tips/user_tips.txt",
    }

    local map = vim.keymap.set
    map("n", "<leader>nto", ":NeovimTips<CR>", { desc = "Neovim tips", noremap = true, silent = true })
    map("n", "<leader>nte", ":NeovimTipsEdit<CR>", { desc = "Edit your Neovim tips", noremap = true, silent = true })
    map("n", "<leader>nta", ":NeovimTipsAdd<CR>", { desc = "Add your Neovim tip", noremap = true, silent = true })
  end
}
```

### vim-plug

```vim
Plug 'ibhagwan/fzf-lua'
Plug 'saxon1964/neovim-tips'

lua << EOF
require("neovim-tips").setup {
  user_file = vim.fn.stdpath("config") .. "/neovim_tips/user_tips.txt",
}

local map = vim.keymap.set
map("n", "<leader>nto", ":NeovimTips<CR>", { desc = "Neovim tips", noremap = true, silent = true })
map("n", "<leader>nte", ":NeovimTipsEdit<CR>", { desc = "Edit your Neovim tips", noremap = true, silent = true })
map("n", "<leader>nta", ":NeovimTipsAdd<CR>", { desc = "Add your Neovim tip", noremap = true, silent = true })
EOF
```

### minpac

```vim
call minpac#init()
call minpac#add('ibhagwan/fzf-lua')
call minpac#add('saxon1964/neovim-tips')

lua << EOF
require("neovim-tips").setup {
  user_file = vim.fn.stdpath("config") .. "/neovim_tips/user_tips.txt",
}

local map = vim.keymap.set
map("n", "<leader>nto", ":NeovimTips<CR>", { desc = "Neovim tips", noremap = true, silent = true })
map("n", "<leader>nte", ":NeovimTipsEdit<CR>", { desc = "Edit your Neovim tips", noremap = true, silent = true })
map("n", "<leader>nta", ":NeovimTipsAdd<CR>", { desc = "Add your Neovim tip", noremap = true, silent = true })
EOF
```

### paq-nvim

```lua
require "paq" {
  "ibhagwan/fzf-lua";
  "saxon1964/neovim-tips";
}

require("neovim-tips").setup {
  user_file = vim.fn.stdpath("config") .. "/neovim_tips/user_tips.txt",
}

local map = vim.keymap.set
map("n", "<leader>nto", ":NeovimTips<CR>", { desc = "Neovim tips", noremap = true, silent = true })
map("n", "<leader>nte", ":NeovimTipsEdit<CR>", { desc = "Edit your Neovim tips", noremap = true, silent = true })
map("n", "<leader>nta", ":NeovimTipsAdd<CR>", { desc = "Add your Neovim tip", noremap = true, silent = true })
```

### dein.vim

```vim
call dein#begin('~/.cache/dein')

call dein#add('ibhagwan/fzf-lua')
call dein#add('saxon1964/neovim-tips')

call dein#end()

lua << EOF
require("neovim-tips").setup {
  user_file = vim.fn.stdpath("config") .. "/neovim_tips/user_tips.txt",
}

local map = vim.keymap.set
map("n", "<leader>nto", ":NeovimTips<CR>", { desc = "Neovim tips", noremap = true, silent = true })
map("n", "<leader>nte", ":NeovimTipsEdit<CR>", { desc = "Edit your Neovim tips", noremap = true, silent = true })
map("n", "<leader>nta", ":NeovimTipsAdd<CR>", { desc = "Add your Neovim tip", noremap = true, silent = true })
EOF

```

### kickstart.nvim

```lua
require("lazy").setup({
  {
    "saxon1964/neovim-tips",
    dependencies = { "ibhagwan/fzf-lua" },
    opts = {
      user_file = vim.fn.stdpath("config") .. "/neovim_tips/user_tips.txt",
    },
    init = function()
      local map = vim.keymap.set
      map("n", "<leader>nto", ":NeovimTips<CR>", { desc = "Neovim tips", noremap = true, silent = true })
      map("n", "<leader>nte", ":NeovimTipsEdit<CR>", { desc = "Edit your Neovim tips", noremap = true, silent = true })
      map("n", "<leader>nta", ":NeovimTipsAdd<CR>", { desc = "Add your Neovim tip", noremap = true, silent = true })
    end,
  },
})
```

### AstroNvim

File `lua/user/plugins/neovim_tips.lua`:

```lua
return {
  {
    "saxon1964/neovim-tips",
    dependencies = { "ibhagwan/fzf-lua" },
    opts = {
      user_file = vim.fn.stdpath("config") .. "/neovim_tips/user_tips.txt",
    },
  },
}
```

File `lua/user/mappings.lua`

```lua
return {
  n = {
    ["<leader>nto"] = { "<cmd>NeovimTips<cr>", desc = "Neovim tips" },
    ["<leader>nte"] = { "<cmd>NeovimTipsEdit<cr>", desc = "Edit your Neovim tips" },
    ["<leader>nta"] = { "<cmd>NeovimTipsAdd<cr>", desc = "Add your Neovim tip" },
  },
}
```

## 🔧 Commands

- `:NeovimTips` — Open searchable list of tips
- `:NeovimTipsEdit` — Edit your personal tips file
- `:NeovimTipsAdd` — Insert a new tip template into your personal file and start editing

## 📝 Tips

Each tip should follow this format in your tips file:

````markdown
# Title: My tip title
# Category: My category name
# Tags: tag1, tag2, tag3
---
This is a description of what the tip does.

```vim
normal-mode-command
```
===
````

Description of the tip starts with --- and ends with ===. There is **NO** predefined format for description. Anything between the starting and ending marker will be interpreted as a text in markdown (.md) format. Fzf-lua will render the markdown description in the right FZF panel. 

## ✅ Example

````markdown
# Title: Delete word under the cursor
# Category: Edit
# Tags: delete, word, cursor
---
In normal mode use `:diw` to delete the word under the cursor.

```vim
:diw
```
===
````

Initial tips were collected from an excellent vim cheat sheet that can be found [here](https://vim.rtorr.com/). 

## 📁 Default File Locations

- Built-in tips: `<plugin_directory>/data/builtin_tips.txt`
- User tips: `~/.config/nvim/neovim_tips/user_tips.txt`

## 🔄 Roadmap Ideas

- Category filtering
- Search descriptions
- Multiple tip sources

**All ideas and pull requests are welcome!** Send me your tips and I will add them to built-in tips collection with proper credits.

## ⚖️ License

- Unlicense. You can find more details in the license file or [here](https://unlicense.org) 

