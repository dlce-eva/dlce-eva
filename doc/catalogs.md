# Setting up the reference catalogs

Some of the tools surrounding CLDF make use of reference catalogs such as the
Glottolog.  For this to work, you need to have a copy of the datasets on your
computer.  To find the dataset, the tools will refer to a file called
`catalog.ini`.

The recommended way to set up the reference catalogs is by using `cldfbench`.
If you really want to set things up by hand you can find instructions in Section
[*Configuring the catalogs manually*](#configuring-the-catalogs-manually) below.

## Setting up cldfbench and the catalog APIs

First you need to create a virtual environment if you haven't already (see
[the Python guide](python.md#virtual-environments) for instructions on how to do
that on your operating system of choice).

Enter the virtual environment and install the `cldfbench` packages together with
the extras `glottolog`, `concepticon`, and `clts`:

    pip install "cldfbench[glottolog,concepticon,clts]"

## Cloning the git repos for the catalogs

Use [`git`](git.md) to clone the git repos for the three catalogs:

 * Glottolog: <https://github.com/glottolog/glottolog>
 * Concepticon: <https://github.com/concepticon/concepticon-data>
 * CLTS: <https://github.com/cldf-clts/clts>

e.g.:

    git clone https://github.com/glottolog/glottolog C:\Users\Alice\Documents\Data\glottolog
    git clone https://github.com/concepticon/concepticon-data C:\Users\Alice\Documents\Data\concepticon-data
    git clone https://github.com/cldf-clts/clts C:\Users\Alice\Documents\Data\clts

*Note for Windows users*:
On Windows `git` might fail to clone the Glottolog repo, due to the length of
some of the file names in the repo.  This is because the support for long file
paths is disabled by default in `git`.  To change this, run the following
command:

    git config --system core.longpaths true

## Configuring the catalogs using the cldfbench cli

To tell cldfbench where to find the catalogs, use the cldfbench's `catconfig`
sub-command.  Use the command-line arguments `--glottolog`, `--concepticon`, and
`--clts` respectively to point `cldfbench` at the folders you cloned the
catalogs to earlier:

    cldfbench catconfig --glottolog C:\Users\Alice\Documents\Data\glottolog --concepticon C:\Users\Alice\Documents\Data\concepticon-data --clts C:\Users\Alice\Documents\Data\clts

*Note:*  You can also leave out any of the catalogs and *cldfbench* will attempt
to clone the respecitive repos to a default location.  Unfortunately I have seen
that fail on Windows 11 recently, so I'd recommend setting up your clones
beforehand as described above.

## Confirming the setup

In order to confirm whether the set up worked run the `catinfo` command:

    cldfbench catinfo

The output should look something like the following.  It's recommended to read
it and double-check that paths specified under *local clone* are corrent, e.g.:

    glottolog - https://github.com/glottolog/glottolog

    local clone: C:\Users\Alice\Documents\Data\glottolog
    config at: C:\Users\Alice\AppData\Local\cldf\cldf\catalog.ini
    versions:
      v5.1              release 5.1
      v5.0              release 5.0
      v4.8              release 4.8
      v4.7              release 4.7
      v4.6              release 4.6
    API: pyglottolog 3.15.0


    concepticon - https://github.com/concepticon/concepticon-data

    local clone: C:\Users\Alice\Documents\Data\concepticon-data
    config at: C:\Users\Alice\AppData\Local\cldf\cldf\catalog.ini
    versions:
      v3.4.0      release 3.4.0
      v3.3.0      v3.3.0 (#1445)
      v3.2.0      release 3.2.0
      v3.1.0      release 3.1.0
      v3.0.0      release 3.0
    API: pyconcepticon 3.1.0


    clts - https://github.com/cldf-clts/clts

    local clone: C:\Users\Alice\Documents\Data\clts
    config at: C:\Users\Alice\AppData\Local\cldf\cldf\catalog.ini
    versions:
      v2.3.0 2.3.0 release
      v2.2.0 release candidate for v2.2.0 (#128)
      v2.1.0 added CI badge
      v2.0.0 2.0.0 release
      v1.4.1 CLTS recreated with pyclts 2.0
    API: pyclts 3.2.0

## Configuring the catalogs manually

The catalog locations are saved in a configuration file called `catalog.ini`.
The exact location of this file depends on your operating system:

Windows:

    C:\Users\<USERNAME>\AppData\Local\cldf\cldf\catalog.ini

Linux:

    ~/.config/cldf/catalog.ini

(or, if the `XDG_CONFIG_HOME` environment variable is set)

    $XDG_CONFIG_HOME/cldf/catalog.ini

macOS:

    ~/Library/Application Support/cldf/catalog.ini

The format of the file itself is quite simple:  It starts with `[clones]` in
square brackets, followed by a list of catalog names and the respective folders,
e.g.:

    [clones]
    glottolog = C:\Users\Alice\Documents\Data\glottolog
    concepticon = C:\Users\Alice\Documents\Data\concepticon-data
    clts = C:\Users\Alice\Documents\Data\clts

*Note on Windows 11:*
There was an issue recently where `cldfbench` couldn't actually see the config
file even it was well-formed and clearly visible in the Windows file manager.
Even more curiously, the file created by `catconfig` was invisible in the
Windows file manager (but still worked perfectly fine).  Maybe it's a weird file
permission issue.  Who knows.

Should you encounter this problem, you'll have to use `cldfbench catconfig` to
configure your catalogs.
