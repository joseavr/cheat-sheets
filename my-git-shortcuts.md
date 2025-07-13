
Open zhrc file config

```bash
code ~/.zshrc
```

# Command Aliases

```zsh
# COMMAND ALIASES -------------------------------------
alias p="npm"
alias px="npx"
alias ll="ls -la"
alias cpdir='pwd|tr -d "\n"|pbcopy'
alias c="clear"
alias path="echo -e ${PATH//:/\\n} ;"
```


# File Aliases

```zsh 
alias vzsh="code ~/.zshrc"
alias szsh="source ~/.zshrc"
```

# Git Aliases

```zsh
alias gg="git"
alias ggi="git init"
alias gga="git add"
alias ggc="git commit -m"
alias ggf="git fetch -all"
alias ggp="git push origin $(git_current_branch)" # push v1
function ggpush {  # push v2
	git add
	git commit -m "$1"
	git push origin $(git_current_branch)
}

alias ggm="git merge" # Merging another-branch($1) to current branch
alias ggcancelmerge="git merge --abort"

# fetch + merge from $(git_current_branch) to current branch
alias ggpull='git pull origin "$(git_current_branch)"' 

# advance merging with rebase
alias ggrebase="git rebase -i"

alias ggs="git status -s" # list files not staged
alias gglog='git log --graph --pretty="%Cred%h%Creset -%C(auto)%d%Creset %s %Cgreen(%ar) %C(bold blue)<%an>%Creset" --all'
alias ggbranch="git branch -a" # list all branches


# travel to another existing branch, or main by default
function ggco {
	if [ "$1" != "" ]
	then
		git checkout "$1"
	else
		git checkout main
	fi
}

# start new feature($1) from branch($2)
function ggfeat {
	git checkout -b "$1" "$2"
}

# Delete branch, ususally used after merge
function ggdelete {
	git branch -d $1
}

# See conflicts to be resolved
function ggconflict {
	git diff
}
```
















