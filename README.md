Run [Stow](https://www.gnu.org/software/stow/) on multiple stow directories at
the same time, with a minimum amount of configuration and command-line
arguments. Install and update dotfiles with one command, even when they are
organized in multiple repositories in topic directories.

# Usage

1. Put all of your dotfile repositories somewhere, say, `~/dotfiles/`. In each
   repository (`~/dotfiles/everywhere/`), dotfiles should be put into a topic
   directory (`~/dotfiles/everywhere/shells/`), and then organized in the same
   directory hierarchy as you want them in `$HOME`
   (`~/dotfiles/everywhere/shells/.bashrc`).
   
2. Create an empty `.stow` file in each repository
   (`~/dotfiles/everywhere/.stow`).

   Then, 

   ```
   > stows -c ~/dotfiles --target ~
   > # or 
   > cd ~/dotfiles
   > stows --target ~
   ```

3. (Even better) Create a `.stowrc` file in each repository, in which
`--target` is specified. For example, just the first line below is enough, but
you might want to change the default action while you're at it:

   ``` 
   --target=../../ 
   --restow
   ```

   Then,

   ```
   > stows -c ~/dotfiles
   
   > # or
   > cd ~/dotfiles
   > stows
   ```

The Stows help message (`stows -h`) has more details on configuration and
options.

# Motivation

One way of managing dotfiles is to keep them under version control in their own
directory, and then to use Stow to create symlinks in your `$HOME` directory
where the dotfiles are supposed to be. It's also common to organize your
dotfiles into directories that match the application or topic that they belong
to: editors, git, shells, etc.

You might also have multiple bundles of dotfiles, config files, scripts, secret
keys, etc. that you want to store in separate repositories. Stows is helpful if
your dotfiles look like this:

```
~/dotfiles/
    dotfiles-common/ (<- git repo)
        bash/ (.bashrc, .bash_profile, ...)
        git/  (.gitconfig, .gitignore, ...)
        misc/ (.config/ .dircolors, .inputrc, ...)
        tmux/
        unison/
        ...
    dotfiles-work/ (<- git repo)
        docker/
        puppet/
        pylint/
        ...
    dotfiles-secret/ (<- sneakernet, rsync, encrypted git repo, ...)
        ssh/ (.ssh/known_hosts, nonpublic servers in .ssh/config.secret)
        git/ (github key in .gitconfig.secret)
        ...
```

More info on this dotfile setup---and why you might use Stows instead of just
using Stow---can be found in [this blog post](http://www.ohspite.net/).
