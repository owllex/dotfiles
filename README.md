# owllex's config directory

This directory tracks my common linux home directory config, and is meant to cloned into a bare git repo.

# How to install onto a new system.

```
alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'
echo ".cfg" >> .gitignore
git clone --bare --recurse-submodules https://github.com/owllex/dotfiles.git $HOME/.cfg
config checkout
```

This step may fail if there is already a .bashrc or other config file collision. If so, delete or merge the collisions.
One way to do this is:

```
mkdir -p .config-backup && \
config checkout 2>&1 | egrep "\s+\." | awk {'print $1'} | \
xargs -I{} mv {} .config-backup/{}
```

Now, continue on.

```
config checkout
config config --local status.showUntrackedFiles no
```

All done! From here you can do regular things with git, but using the special `config` alias to make working with this repo easier.

```
config status
config add .vimrc
config commit -m "Add vimrc"
config add .bashrc
config commit -m "Add bashrc"
config push
```
