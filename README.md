# git-prompt.sh

`git-prompt.sh` extracted from [git/git](https://github.com/git/git), so you
don't need to keep a complete copy of git's source to use `__git_ps1()` in your
terminal prompt.

## Installation

    mkdir -p ~/.config
    git clone https://github.com/jeffkreeftmeijer/git-prompt.sh.git ~/.config/git-prompt.sh

### zsh

    # ~/.zshrc
    source ~/.config/git-prompt.sh/git-prompt.sh
    setopt PROMPT_SUBST
    export PROMPT='%~ $(__git_ps1 "(%s) ")%# '

### bash

    # ~/.bash_profile or ~/.bashrc
    source ~/.config/git-prompt.sh/git-prompt.sh
    export PS1='\w $(__git_ps1 "(%s) ")$ '

## Updating

    cd ~/.config/git-prompt.sh
    git fetch && git reset --hard origin/master

## Contributing

### Initial extraction

    git clone git@github.com:git/git.git git-prompt.sh
    cd git-prompt.sh
    git filter-branch --force --prune-empty --subdirectory-filter contrib/completion
    git remote rename origin upstream
    git branch -m upstream
    git checkout -b master

### Updating git-prompt.sh to upstream master

    git checkout upstream
    git fetch
    git reset --hard upstream/master
    git filter-branch --force --prune-empty --subdirectory-filter contrib/completion
    git checkout master
    git rebase --onto upstream master~3 master
