# Git

Git is a version control system used to track changes in files. Git uses
metadata (who changed what when where) to keep a history of all the changes made
in a repository. Git is a distributed version control system and allows
repositories to live locally and remotely (i.e. if you clone one of our
repositories from GitHub you'll have a local clone and remote repository still
living on GitHub).

## Tutorials and guides

We can highly recommend the Software Carpentry lessons on [Version control with
Git](https://swcarpentry.github.io/git-novice/). Those will introduce you to the
basic commands required for the essential Git workflow.

[Here](https://pad.gwdg.de/p/ByBc2xHEU#/) you can find a presentation (based off
the Software Carpentry lessons) that distills the basics even further.

## Essential commands

While working through the guides, be on the lookout for the following essential
commands:

- `git init`: Initialize a repository locally.
- `git clone`: Clone ('download') a repository from a remote location.
- `git pull`: Update a repository from a remote repository.
- `git push`: Push local changes to a remote repository.
- `git status`: Get an overview of the status of a repository.
- `git add`: Add files to the staging area (prepare files for a commit).
- `git commit`: Commit files (cementing their changes into a repositories
  history)
- `git log`: Get an overview of the history of a repository.
- `git diff`: Get an overview of the changes made to a file.

## Git and GitHub etiquette

Usually more than one person is involved in a Git repository. This means that it
is useful to follow basic principles for a better collaborative experience:

- use `.gitignore` to keep temporary or unwanted files out of the repository
  (`.DS_Store` folder in macOS, virtual environments, etc.)
- don't commit large (and particularly binary) files to a repository and use
  other services for storing large files
- try to write concise but useful commit messages
- try to keep the changes in a commit within a reasonable limit (i.e. prefer
  more, smaller, commits to one very large commit that changes a lot of things)

## Long filename support on Windows

By default, the Windows version of `git` does not support long file names.  This
may prevent some repositories, such as the [glottolog][glottolog] from working.

To enable support for long file names, run the following command:

    git config --system core.longpaths true

[glottolog]: https://github.com/glottolog/glottolog

## PSA: Avoid Unicode characters in file paths

On some (Windows?) systems, `git`'s behaviour might turn a bit… volatile if the
file path to a repo contains non-English characters (like `ü`, `ы` or `ß`).  As
an example you might encounter errors like the following:

    error: fsmonitor--daemon failed to start

In general, the safest bet is to avoid any characters that might confuse your
computer in your file/folder names (including spaces).  The following set of
characters is considered safe:

 1. letters `a-z` (bonus points for making it all lower-case)
 2. numbers `0-9`
 3. period `.`, dash `-`, and underscore `_`

Note:  If your user name contains non-English characters, then that will affect
all files in your home folder (e.g. `C:\Users\Björn`).  In that case you can
work around the issue by putting all your git repos in a separate folder outside
of your home directory (e.g. `C:\repos`).
