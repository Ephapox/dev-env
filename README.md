# dev-env

## Setup ~/.bash_profile

```sh
# Prompt
export PS1="__________________________________\n\[\033[36m\]\u\[\033[m\]@\[\033[32m\]\h:\[\033[33;1m\]\w\[\033[m\]\$ \n=> "
export CLICOLOR=1
export LSCOLORS=ExFxBxDxCxegedabagacad

# Aliases
alias ll='ls -FGlAhp' 
alias vim='mvim -v'
alias rm-swp="find . -type f -name \".*.swp\" -exec rm -f {} \\;"
alias ls-swp="find . -type f -name \".*.swp\""
alias shsource="source ~/.bash_profile"
alias shedit="vim ~/.bash_profile"

# Functions
cd() { builtin cd "$@"; ll; }   
ii() {
	echo -e "\nYou are logged on ${RED}$HOST"
	echo -e "\nAdditionnal information:$NC " ; uname -a
	echo -e "\n${RED}Users logged on:$NC " ; w -h
	echo -e "\n${RED}Current date :$NC " ; date
	echo -e "\n${RED}Machine stats :$NC " ; uptime
	echo -e "\n${RED}Current network location :$NC " ; scselect
	echo -e "\n${RED}Public facing IP Address :$NC " ;myip
	#echo -e "\n${RED}DNS Configuration:$NC " ; scutil --dns
	echo
}
parse_git_branch() {
		git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
export FZF_DEFAULT_OPTS='--height 40% --layout=reverse --border'
if [ -f ~/.git-completion.bash ]; then
	. ~/.git-completion.bash
fi

eval "$(direnv hook bash)"

[ -f /usr/local/etc/bash_completion ] && . /usr/local/etc/bash_completion
HISTSIZE=""

fortune | pokemonsay
```

## Install stuff

1. Install Homebrew

```/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"```

2. Install git

`brew install git`

3. Install the silver searcher

`brew install the_silver_searcher`

4. Install fzf

```
brew install fzf

# To install useful key bindings and fuzzy completion:
$(brew --prefix)/opt/fzf/install
```

## Setup GitHub

1. Generate ssh key and add to GitHub

```
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
$ pbcopy < ~/.ssh/id_rsa.pub
```

## Setup vim

1. Install vim Plug

```
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

2. Setup `~/.vimrc`

```vim
" Plugins will be downloaded under the specified directory.
call plug#begin('~/.vim/plugged')

" Declare the list of plugins.
Plug 'tpope/vim-sensible'
Plug 'preservim/nerdtree'
Plug 'junegunn/fzf', { 'do': './install --bin' }
Plug 'junegunn/fzf.vim'

" :PlugInstall
" :PlugUpdate
" :PlugClean

" List ends here. Plugins become visible to Vim after this call.
call plug#end()

"On Mac OSX
"visual mode  copy :w !pbcopy
"copy the whole file :%w !pbcopy
"paste from the clipboard :r !pbpaste

syntax on
filetype plugin indent on
" system clipboard yank
set clipboard=unnamedplus
let mapleader=","

" MAPPING
nmap <silent> <leader>ev :e $MYVIMRC<CR>
" maps ,sv to source .vimrc
nnoremap <leader>sv :source $MYVIMRC
" maps ; to :
nnoremap ; :
" clears search buffer when ,/
nmap <silent> ,/ :nohlsearch<CR>
" // will search that word
vnoremap // y/<C-R>"<CR>

" maps pane navigation to shortcut 
" ctrl-w + j => ctrl-j
nnoremap <C-J> <C-W><C-J>
nnoremap <C-K> <C-W><C-K>
nnoremap <C-L> <C-W><C-L>
nnoremap <C-H> <C-W><C-H>
inoremap jk <esc>`

" OPTIONS
" Add full file path to your existing statusline
set laststatus=2
" Indenting Options
set tabstop=2 shiftwidth=2
set copyindent " copy the previous line's indent

" Buffer Options
set hidden " hides buffers when they are unsaved and a new buffer is opened
" Syntax Options
"
set showmatch " show matching paranthesis
" Search Options
"
set history=1000 " larger search history
set ignorecase " ignore case when searching
set hlsearch " highlight search terms
set incsearch " show search matches as you type
set smartcase " ignore case if pattern is all lowercase only
set backspace=indent,eol,start " backspace everything in insert
set number
set undolevels=1000 " larger undo history
set wildignore=*.swp " ignore swp files
set clipboard=unnamedplus " yank will copy to system clipboard
set pastetoggle=<F5> " F5 in insert allows for pasting w/o indent
set mouse=a
" split panes down for vertical
" split panes right for horizontal
set splitbelow
set splitright

" NERDTREE
map <C-n> :NERDTreeToggle<CR>
let g:NERDTreeNodeDelimiter = "\u00a0"
 
" fzf
set rtp+=/usr/local/opt/fzf

" the silver searcher
let $FZF_DEFAULT_COMMAND = 'ag --hidden --ignore .git -l -g ""'
nnoremap <C-p> :Files<CR>
nnoremap <C-b> :Buffer<CR>
nnoremap <C-f> :Ag<CR>

" Fix tmux colorscheme issues
set background=dark
set t_Co=256
colorscheme wasabi256

" silver searcher preview window
" ? on silver searcher result to preview
" Navigate preview using shift + arrow key
command! -bang -nargs=* Ag
	\ call fzf#vim#ag(<q-args>,
	\					<bang>0 ? fzf#vim#with_preview('up:60%')
	\							: fzf#vim#with_preview('right:50%:hidden', '?'),
	\					<bang>0)
set noexpandtab

```
