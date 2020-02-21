# dev-env

## Setup ~/.bash_profile

```sh
# Prompt
export PS1="__________________________________\n\[\033[36m\]\u\[\033[m\]@\[\033[32m\]\h:\[\033[33;1m\]\w\[\033[m\]\$ \n=> "
export CLICOLOR=1
export LSCOLORS=ExFxBxDxCxegedabagacad

# Aliases
alias ll='ls -FGlAhp' 

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
```

## Install stuff

1. Install Homebrew

```/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"```

2. Install git

`brew install git`

## Setup GitHub

1. Generate ssh key and add to GitHub

```
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
$ pbcopy < ~/.ssh/id_rsa.pub
```

## Setup vim

1. Install Pathogen

```
mkdir -p ~/.vim/autoload ~/.vim/bundle && \
curl -LSso ~/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim
```

2. Setup `~/.vimrc`

```vim

```
