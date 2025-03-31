# Neovim Cheat Sheet
*Optimized for your config as of March 24, 2025*

Your leader key is `<Space>`. Use it to trigger many commands below!

---

## Basics
- **Quit**: `:q` (prompts to save if unsaved changes due to `confirm = true`)
- **Save**: `:w`
- **Save & Quit**: `:wq` or `ZZ`
- **Force Quit**: `:q!`
- **Undo**: `u`
- **Redo**: `<C-r>`

---

## Navigation
### Cursor Movement
- **Left**: `h` (arrows disabled with reminder)
- **Down**: `j`
- **Up**: `k`
- **Right**: `l`
- **Word Forward**: `w`
- **Word Backward**: `b`
- **Line Start**: `0`
- **Line End**: `$`
- **File Top**: `gg`
- **File Bottom**: `G`
- **Scroll Offset**: 10 lines above/below cursor (`scrolloff = 10`)

### Window Splits
- **Move Left**: `<C-h>`
- **Move Right**: `<C-l>`
- **Move Down**: `<C-j>`
- **Move Up**: `<C-k>`
- **New Vertical Split**: `:vsplit` or `<C-w>v`
- **New Horizontal Split**: `:split` or `<C-w>s`
- *Note*: Splits open right/below due to `splitright` and `splitbelow`

---

## Editing
- **Insert Mode**: `i` (before cursor), `a` (after cursor)
- **Append Line**: `o` (below), `O` (above)
- **Delete**: `x` (char), `dd` (line)
- **Copy**: `yy` (yank line, highlights briefly due to autocommand)
- **Paste**: `p` (after), `P` (before)
- **Replace**: `r` (single char), `R` (overwrite mode)
- **Change**: `c` (e.g., `ciw` to change inner word)
- **Format Buffer**: `<Space>f` (via Conform plugin)

### Surround (Mini.Surround)
- **Add**: `sa` (e.g., `saiw)` adds parens around word)
- **Delete**: `sd` (e.g., `sd'` removes quotes)
- **Replace**: `sr` (e.g., `sr)'` replaces ) with ')

---

## Search & Replace
- **Search**: `/` (case-insensitive unless capitals or `\C`, `smartcase = true`)
- **Next**: `n`
- **Previous**: `N`
- **Clear Highlights**: `<Esc>` (custom mapping)
- **Live Replace Preview**: `:s/old/new` (shows in split due to `inccommand = split`)

### Telescope Fuzzy Finder
- **Help Tags**: `<Space>sh` (search Neovim help)
- **Keymaps**: `<Space>sk`
- **Files**: `<Space>sf`
- **Grep Word**: `<Space>sw` (current word)
- **Live Grep**: `<Space>sg`
- **Diagnostics**: `<Space>sd`
- **Resume Last**: `<Space>sr`
- **Recent Files**: `<Space>s.`
- **Buffers**: `<Space><Space>`
- **Current Buffer**: `<Space>/`
- **Open Files Grep**: `<Space>s/`
- **Neovim Config**: `<Space>sn`

---

## Code & LSP
### LSP Commands
- **Go to Definition**: `gd`
- **Go to References**: `gr`
- **Go to Implementation**: `gI`
- **Type Definition**: `<Space>D`
- **Document Symbols**: `<Space>ds`
- **Workspace Symbols**: `<Space>ws`
- **Rename**: `<Space>rn`
- **Code Action**: `<Space>ca` (normal & visual modes)
- **Go to Declaration**: `gD`
- **Toggle Inlay Hints**: `<Space>th` (if supported)

### Diagnostics
- **Quickfix List**: `<Space>q` (opens diagnostic list)
- *Note*: Signs in gutter (`signcolumn = yes`), virtual text if multiple sources

### Language-Specific
- **C/C++ Header/Source Switch**: `<Space>ch` (Clangd)

---

## Plugins
### Lazy.nvim
- **Open Manager**: `:Lazy`
- **Update Plugins**: `:Lazy update`
- *Tip*: Press `?` in Lazy UI for help

### Which-Key
- **Show Keybinds**: Start with `<Space>` (instant due to `delay = 0`)
- **Groups**: 
  - `<Space>c`: [C]ode
  - `<Space>d`: [D]ocument
  - `<Space>r`: [R]ename
  - `<Space>s`: [S]earch
  - `<Space>w`: [W]orkspace
  - `<Space>t`: [T]oggle
  - `<Space>h`: Git [H]unk

### Autocompletion (nvim-cmp)
- **Next Item**: `<C-n>`
- **Previous Item**: `<C-p>`
- **Confirm**: `<C-y>`
- **Scroll Docs**: `<C-b>` (back), `<C-f>` (forward)
- **Trigger**: `<C-Space>`
- **Snippet Jump**: `<C-l>` (forward), `<C-h>` (back)

### Treesitter
- *Enabled*: Syntax highlighting and indentation for many languages

---

## Terminal
- **Enter Terminal**: `:term`
- **Exit Terminal**: `<Esc><Esc>` (custom mapping)

---

## Visuals
- **Cursor Line**: Highlighted (`cursorline = true`)
- **Whitespace**: Tabs `» `, Trailing `·`, NBSP `␣` (`list = true`)
- **Colorscheme**: TokyoNight Night
- **Statusline**: Mini.statusline with line:column

---

## Pro Tips
- **Check Help**: `<Space>sh` for any command details
- **Mouse**: Enabled for resizing splits (`mouse = a`)
- **Clipboard**: Synced with OS (`unnamedplus`)
- **Undo History**: Persistent (`undofile = true`)
- **Experiment**: Try `<Space>` and watch Which-Key for options!

---

*Generated for your Neovim config by Grok 3, xAI - March 24, 2025*
