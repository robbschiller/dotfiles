# .dotfiles

My macOS dotfiles for zsh on Apple Silicon (arm64). Adapted from [Mat Marquis](https://github.com/Wilto/dotfiles) via [Nicolas Gallagher](https://github.com/necolas/dotfiles).

## Install

The installation step requires the [XCode Command Line
Tools](https://developer.apple.com/downloads) and may overwrite existing
dotfiles in your HOME directory.

```
bash -c "$(curl -fsSL raw.github.com/robbschiller/dotfiles/master/bin/dotfiles)"
```

N.B. If you wish to fork this project and maintain your own dotfiles, you must
substitute my username for your own in the above command and the 2 variables
found at the top of the `bin/dotfiles` script.

## How to update

You should run the update when:

* You make a change to `~/.dotfiles/git/gitconfig` (the only file that is
  copied rather than symlinked).
* You want to pull changes from the remote repository.
* You want to update Homebrew formulae.

Run the dotfiles command:

```bash
dotfiles
```

Options:

| Flag | Description |
|------|-------------|
| `-h`, `--help` | Help |
| `-l`, `--list` | List of additional applications to install |
| `--no-packages` | Suppress package updates |
| `--no-sync` | Suppress pulling from the remote repository |

## Features

### Automatic software installation

Homebrew formulae:

* [coreutils](https://www.gnu.org/software/coreutils/) — GNU core utilities
* [git](http://git-scm.com/)
* [tree](http://mama.indstate.edu/users/ice/tree/)
* [jq](https://jqlang.github.io/jq/)
* [ripgrep](https://github.com/BurntSushi/ripgrep)
* [fd](https://github.com/sharkdp/fd)
* [bat](https://github.com/sharkdp/bat)
* [fzf](https://github.com/junegunn/fzf)

### Custom macOS defaults

Custom macOS settings can be applied during the `dotfiles` process. They can
also be applied independently by running the following command:

```bash
osxdefaults
```

### Local and private configurations

Any special-case Vim directives local to a machine should be stored in a
`.vimrc.local` file on that machine. The directives will then be automatically
imported into your master `.vimrc`.

Any private and custom commands should be stored in a `~/.zshrc.local`
file. Any commands included in this file will not be under version control or
committed to a public repository. If `~/.zshrc.local` exists, it will be
sourced for inclusion in `zshrc`.

Here is an example `~/.zshrc.local`:

```zsh
# PATH exports
path=($HOME/.gem/ruby/3.0/bin $path)

# Git credentials
# Not under version control to prevent people from
# accidentally committing with your details
GIT_AUTHOR_NAME="Robb Schiller"
GIT_AUTHOR_EMAIL="robb@example.com"
GIT_COMMITTER_NAME="$GIT_AUTHOR_NAME"
GIT_COMMITTER_EMAIL="$GIT_AUTHOR_EMAIL"
# Set the credentials (modifies ~/.gitconfig)
git config --global user.name "$GIT_AUTHOR_NAME"
git config --global user.email "$GIT_AUTHOR_EMAIL"
```

The `git/gitconfig` file is copied to `~/.gitconfig`, so any private git
configuration specified in `~/.zshrc.local` will not be committed to
your dotfiles repository.

### Apple Silicon support

This setup is designed for Apple Silicon Macs with Homebrew installed at
`/opt/homebrew`. NVM and Bun are automatically detected and initialized
if present.

## Adding new git submodules

If you want to add more git submodules, e.g., Vim plugins to be managed by
pathogen, then follow these steps while in the root of the superproject.

```bash
# Add the new submodule
git submodule add https://example.com/remote/path/to/repo.git vim/bundle/one-submodule
# Initialize and clone the submodule
git submodule update --init
# Stage the changes
git add vim/bundle/one-submodule
# Commit the changes
git commit -m "Add a new submodule: one-submodule"
```

## Updating git submodules

Updating individual submodules within the superproject:

```bash
# Change to the submodule directory
cd vim/bundle/one-submodule
# Checkout the desired branch (of the submodule)
git checkout master
# Pull from the tip of master (of the submodule - could be any sha or pointer)
git pull origin master
# Go back to main dotfiles repo root
cd ../../..
# Stage the submodule changes
git add vim/bundle/one-submodule
# Commit the submodule changes
git commit -m "Update submodule 'one-submodule' to the latest version"
# Push to a remote repository
git push origin master
```

Now, if anyone updates their local repository from the remote repository, then
using `git submodule update` will update the submodules (that have been
initialized) in their local repository. N.B This will wipe away any local
changes made to those submodules.

## Acknowledgements

Inspiration and code was taken from many sources, including:

* [@necolas](https://github.com/necolas/dotfiles) (Nicolas Gallagher)
* [@wilto](https://github.com/Wilto/dotfiles) (Mat Marquis)
* [@tmschl](https://github.com/tmschl/dotfiles) (Tim Schiller)
* [@tjkrusinski](https://github.com/TJkrusinski/dotfiles) (TJ Krusinski)
