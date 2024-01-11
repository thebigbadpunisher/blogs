These are all my vimrc files.These are all my vimrc files. These are all my vimrc files. These are all my vimrc files. These are all my vimrc files. These are all my vimrc files.
These are all my vimrc files. These are all my vimrc files. These are all my vimrc files.

" Plugins For Vim
call plug#begin()

Plug 'preservim/nerdtree'
Plug 'jiangmiao/auto-pairs'
Plug 'vim-airline/vim-airline'
Plug 'adrian5/oceanic-next-vim'
Plug 'vim-airline/vim-airline-themes'
Plug 'altercation/vim-colors-solarized'
Plug 'catppuccin/vim', { 'as': 'catppuccin' }
Plug 'neoclide/coc.nvim', {'branch': 'release'}

" Plugin for languages
Plug 'rust-lang/rust.vim'

" Colorschemes Plugins
Plug 'nordtheme/vim'
Plug 'TomNomNom/xoria256.vim'
Plug 'loctvl842/monokai-pro.nvim'
Plug 'chriskempson/tomorrow-theme'
Plug 'dracula/vim', { 'as': 'dracula' }

" Tpope Plugins
Plug 'tpope/vim-fugitive'
Plug 'tpope/vim-commentary'

" Add clangd extension
Plug 'clangd/coc-clangd', {'do': { -> coc#util#install()}}

" Emmet Plugin
Plug 'mattn/emmet-vim'

" Tmux Plugins
Plug 'christoomey/vim-tmux-navigator'

call plug#end()

" coc config
let g:coc_global_extensions = [
  \ 'coc-snippets',
  \ 'coc-tsserver',
  \ 'coc-eslint',
  \ 'coc-json',
  \ ]

" Remap for rename current word
nmap <F2> <Plug>(coc-rename)

" Use <C-l> for trigger snippet expand
imap <C-l> <Plug>(coc-snippets-expand)

" Using <Tab> to go to selection options
inoremap <expr> <Tab> coc#pum#visible() ? coc#pum#next(1) : "\<Tab>"
inoremap <expr> <S-Tab> coc#pum#visible() ? coc#pum#prev(1) : "\<S-Tab>"

" remapping some keys
" Move line up
nnoremap <A-Up> :m-2<CR>==
vnoremap <A-Up> :m-2<CR>gv=gv

" Move line down
nnoremap <A-Down> :m+<CR>==
vnoremap <A-Down> :m+<CR>gv=gv

" Duplicate line up
nnoremap <C-A-Up> :t.<CR>==
vnoremap <C-A-Up> :t.<CR>gv=gv

" Duplicate line down
nnoremap <C-A-Down> :t.<CR>==
vnoremap <C-A-Down> :t.<CR>gv=gv

" Move visually selected lines up
xmap <A-Up> :move '<-2<CR>gv=gv

" Move visually selected lines down
xmap <A-Down> :move '>+1<CR>gv=gv

" changing esc to fk to go to normal mode
inoremap fk <ESC>

" ctrl + t to open nerd tree window
nnoremap <C-t> :NERDTreeToggle<CR>

" shift + i (showing hidden files in nerdtree)
let NERDTreeShowHidden=1

" packloadall for plugins
packloadall

" emmet shortcuts
let g:user_emmet_mode='n'
let g:user_emmet_leader_key=','

" Other commands
syntax on " highlight syntax
set number " show line numbers
set noswapfile " disable the swapfile
set hlsearch " highlight all results
set ignorecase " ignore case in search
set incsearch " show search results as you type

" Colorscheme for vim and highlight color
colorscheme oceanicnext
highlight Search ctermfg=red

" Setting relative number
set relativenumber

" Cursor for normal mode and edit mode
let &t_SI = "\e[6 q"
let &t_EI = "\e[2 q"

" When leaving vim change it to default mode
autocmd VimLeave * silent !echo -ne "\e[6 q"

" Disable compatibility with vi which can cause unexpected issues.
set nocompatible

" Enable type file detection. Vim will be able to try to detect the type of file in use.
filetype on

" Enable plugins and load plugin for the detected file type.
filetype plugin on

" Load an indent file for the detected file type.
filetype indent on

" Ignore capital letters during search.
set ignorecase

" Show matching words during a search.
set showmatch

" Set the commands to save in history default number is 20.
set history=1000

" Display
set ls=2
set showmode
set showcmd
set modeline
set ruler
set title
set nu

" Line wrapping
set nowrap
set linebreak
set showbreak=▹

" Auto indent what you can
set autoindent

" Searching
set ignorecase
set smartcase
set gdefault
set hlsearch
set showmatch

" Enable jumping into files in a search buffer
set hidden

" Make backspace a bit nicer
set backspace=eol,start,indent

" Indentation
set shiftwidth=4
set tabstop=4
set softtabstop=4
set shiftround
set expandtab

" For Autocomplete Html
autocmd FileType html set omnifunc=htmlcomplete#CompleteTags

" Airline config
let g:airline_powerline_fonts = 1
let g:airline#extensions#tabline#enabled = 1
let g:airline_theme='powerlineish'

" multiple lines macros visually
xnoremap @ :<C-u>call ExecuteMacroOverVisualRange()<CR>
function! ExecuteMacroOverVisualRange()
  echo "@".getcmdline()
  execute ":'<,'>normal @".nr2char(getchar())
endfunction
