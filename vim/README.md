### Swap words (http://vimcasts.org/transcripts/54/en/)

    yiw # on first word
    viwp # on second word
    viwp # on first word

### Basic vimrc

    set hls ruler number list
    set backspace=indent,eol,start
    set lcs=tab:>-,trail:-
    set expandtab tabstop=2 shiftwidth=2
    set modeline
    colorscheme delek
    "colorscheme slate
    "colorscheme elflord
    "colorscheme torte

### Vundle setup

    git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
    mv ~/.vimrc ~/.vim/vimrc
    ln -s ~/.vim/vimrc ~/.vimrc
    
### Vundle vimrc

    set nocompatible              " be iMproved, required
    filetype off                  " required

    set rtp+=~/.vim/bundle/Vundle.vim
    call vundle#begin()

    Plugin 'VundleVim/Vundle.vim'
    Plugin 'tpope/vim-fugitive'
    Plugin 'tpope/vim-surround'
    Plugin 'tpope/vim-commentary'
    Plugin 'fatih/vim-go'
    Plugin 'elzr/vim-json'
    Plugin 'fatih/vim-hclfmt'
    Plugin 'flazz/vim-colorschemes'

    call vundle#end()            " required
    filetype plugin indent on    " required

    set hls ruler number list
    set backspace=indent,eol,start
    set lcs=tab:>-,trail:-
    set expandtab tabstop=2 shiftwidth=2
    set modeline
    set t_Co=256
    colorscheme molokai
