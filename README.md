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

git-prompt.sh uses [git-filter-repo](https://github.com/newren/git-filter-repo) because [`git-filter-branch` is slow and dangerous](https://jeffkreeftmeijer.com/git-extract/).
Install it with a [package manager](https://github.com/newren/git-filter-repo/blob/main/INSTALL.md). On a Mac, use Homebrew:

    $ brew install git-filter-repo

### Initial extraction

    git clone git@github.com:git/git.git git-prompt.sh
    cd git-prompt.sh
    git filter-repo --force --subdirectory-filter contrib/completion
    git remote add origin git@github.com:jeffkreeftmeijer/git-prompt.sh.git
    git checkout -b main
    git push origin main
 
 ### Updating git-prompt.sh to upstream master
 
    git clone git@github.com:jeffkreeftmeijer/git-prompt.sh.git
    cd git-prompt.sh
    git checkout -b upstream
    git remote add upstream git@github.com:git/git.git
    git fetch upstream
    git reset --hard upstream/master
    git filter-repo --force --subdirectory-filter contrib/completion
    git filter-repo --path git-prompt.sh
    git remote add origin git@github.com:jeffkreeftmeijer/git-prompt.sh.git
    git checkout -b main
    git fetch main
    git reset --hard origin/main
    git rebase --onto upstream main~3 main
