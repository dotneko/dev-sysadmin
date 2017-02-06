References and Links:
- [Vim Official page](http://www.vim.org/)

# Learning Vim

- Starting out: [Learn Vim Progressively](http://yannesposito.com/Scratch/en/blog/Learn-Vim-Progressively/)
- [VIM Adventures](https://vim-adventures.com/)
- Type `vimtutor` at the command line and you'll have an interactive tutorial.

# Vim Configuration

- [VimConfig](http://vimconfig.com/). Web-based generation of .vimrc
- [Vim Wikia: Vimrc file](http://vim.wikia.com/wiki/Open_vimrc_file)
- [Vim Wikia: Indenting source code](http://vim.wikia.com/wiki/Indenting_source_code#Methods_for_automatic_indentation)

# Useful plugins

- [Pathogen.vim](https://github.com/tpope/vim-pathogen). An easy way to install plugins and manage your `runtimepath`.
- [vim-pug](https://github.com/digitaltoad/vim-pug). Vim syntax highlighting for Pug (formerly Jade) templates.

# Simple .VIMRC file

```
set number
set showmatch
set visualbell
set hlsearch
set smartcase
set ignorecase
set incsearch
set autoindent
set expandtab
set shiftwidth=4
set smartindent
set softtabstop=4
set ruler
set backspace=indent,eol,start
```

# Some tips found on the web:
- Indent multiple lines quickly ([Very detailed answer at source]}(http://stackoverflow.com/questions/235839/indent-multiple-lines-quickly-in-vi)]):
    - Enter [num lines] then `>>`: E.g. `8>>` will indent 8 lines.
- Commenting out blocks of code ([Source](http://stackoverflow.com/questions/2561418/how-to-comment-out-a-block-of-python-code-in-vim)):
    - Go to beginning of block, press \<Ctrl-V> to enter visual mode.
    - Move down to the end of the block, then press \<Shift-I> to insert, type `# `, and then \<Esc>
