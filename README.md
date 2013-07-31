# .dotfiles

My OS X dotfiles (Adapted from [Mat Marquis](https://github.com/Wilto/dotfiles) via [Nicolas Gallager](https://github.com/necolas/dotfiles)).

## If you'd like to Install

The installation step requires the [XCode Command Line
Tools](https://developer.apple.com/downloads) and may overwrite existing
dotfiles in your HOME directory.

```
$ bash -c "$(curl -fsSL raw.github.com/robbschiller/dotfiles/master/bin/dotfiles)"
```

N.B. If you wish to fork this project and maintain your own dotfiles, you must
substitute my username for your own in the above command and the 2 variables
found at the top of the `bin/dotfiles` script.

## Changes from Mat's dotfiles

- 2d Dock Disabled
- Default dock item size 36px
- Secure trash emptying disabled
- Showing hard drives on the desktop disabled
- Vim not set as default
- Additional git command line aliasing gc for "git commit", ga for "git add ."
