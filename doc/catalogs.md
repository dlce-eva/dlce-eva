# Reference catalogs

Some of the tools surrounding CLDF make use of datasets such as the Glottolog.
For this to work, you need to have a copy of the datasets on your computer.  To
find the dataset, the tools will refer to a file called `catalog.ini`.

The setup process for a dataset goes as follows:

 * Download the data using `git clone` into a folder of your choice
 * Tell the `catalog.ini` the exact path to where you put the dataset

(Alternatively, you can also use [`cldfbench
catconfig`](#using-cldfbench-catconfig) to automate this process.)

The location of the `catalog.ini` file depends on your operating system:

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

## Glottolog

The glottolog data is kept on Github under [`glottolog/glottolog`][glottolog].
Add the path to your copy of the dataset to the name `glottolog` in your
`catalog.ini`, e.g.:

    [clones]
    glottolog = C:\Users\Alice\Documents\Data\glottolog

*Note for Windows users*:
On Windows `git` might fail to clone the Glottolog repo, due to the length of
some of the file names in the repo.  This is because the support for long file
paths is disabled by default in `git`.  To change this, run the following
command:

    git config --system core.longpaths true

[glottolog]: https://github.com/glottolog/glottolog

## Concepticon

The concepticon data is kept on Github under
[`concepticon/concepticon-data`][concepticon].  Add the path to your copy of the
dataset to the name `concepticon` in your `catalog.ini`, e.g.:

    [clones]
    concepticon = C:\Users\Alice\Documents\Data\concepticon-data

[concepticon]: https://github.com/concepticon/concepticon-data

## CLTS

The CLTS data is kept on Github under [`cldf-clts/clts`][clts].
Add the path to your copy of the dataset to the name `clts` in your
`catalog.ini`, e.g.:

    [clones]
    clts = C:\Users\Alice\Documents\Data\clts

[clts]: https://github.com/cldf-clts/clts

## Using cldfbench catconfig

See [the Python guide](python.md#virtual-environments) for an instruction on
how to create a virtual environment. Having created a new virtual environment
(e.g. `cldfbench`), install the following packages:

```shell script
$ pip install cldfbench
$ pip install pyglottolog
$ pip install pyconcepticon
$ pip install pyclts
```

Afterwards, you can run `cldfbench catconfig` to clone the three catalogs and
automatically create the `config.in` in a location appropriate for your system.

