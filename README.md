# dotsync

Forking dotfiles on github is pretty trendy.  But what if you don't want a full-fledged fork of others' settings?

What if you just want to synchronize your *own* dotfiles, on different machines?

Then you want *two* repositories, not just one.

  1. `dotfiles`:
    - *Your dotfiles*.  The things you want to version and synchronize.
  2. `dotsync`:
    - Dotfile **management** software
    - A github repository just like any other.  Not forked (unless you want to develop it!)

## Philosophy and goals

There's more than one way to put [dotfiles on github](http://dotfiles.github.com/)!  The `dotsync` philosophy is based on [Eli Barzilay's comment](http://www.xxeo.com/archives/2010/02/16/dotfiles-in-git-finally-did-it.html/comment-page-1#comment-126903), summarized below.

Dotfile repositories have to figure out *what to do with the `$HOME` directory*.  Most take one of two approaches:

  1. dotfiles are *__symlinked__ from the repository*
    - **Pro**: *Cleaner setup*.  All the versioned files are in one place!
    - **Con**: *Fragile*. Too easy to whack changes.
  2. `$HOME` *__is__ a repository*
    - **Pro**: *Simple*. Files really do live just where they seem to live.
    - **Con**: *Messy*. Everything you don't version will clutter up your `git status`
    - **Con**: *Dangerous!*  Running `git` commands in the wrong directory could make a mess, instead of a harmless error message

`dotsync` takes a third approach: ***A git alias with predefined options***

  - The dotfiles **live in the HOME directory** (no worries about whacking symlinks)
  - Yet, `$HOME` is **not a repository** (you won't mess it up if you `git` in the wrong directory)

# Getting started

## Install dotsync

These commands install `dotsync` to a directory called `dotsync/`, under your current working directory:

```bash
git clone git://github.com/chiphogg/dotsync.git
./dotsync/install
```

## Setup dotsync

Now that you've got a repository

# Miscellaneous

## Notes

  - Should play nice with `cron`:  the `install` script expands `$HOME` when it writes the `bash` settings file.

# Acknowledgements

  - I owe a lot to [Silas Sewell's original blog post](http://silas.sewell.org/blog/2009/03/08/profile-management-with-git-and-github/).  In fact, at its core, `dotsync` is an attempt to make his approach as automatic and shareable as possible.
  - [Eli Barzilay's blog comment](http://www.xxeo.com/archives/2010/02/16/dotfiles-in-git-finally-did-it.html/comment-page-1#comment-126903) helpfully articulated some philosophical points
  - For help with bash completion (once I implement it!), I'm looking to blog posts by [Chris Lalancette](http://clalance.blogspot.com/2011/10/git-bash-prompts-and-tab-completion.html) and [Robert Escriva](http://robescriva.com/blog/2009/01/06/manage-your-home-with-git/).
  - Note to self: I'll need to [distinguish between `PS1` and `PROMPT_COMMAND`](http://stackoverflow.com/questions/3058325/what-is-the-difference-between-ps1-and-prompt-command) to do fancy things with the `bash` prompt
