# Shell/working on the command line

While working with the shell or command line might seem intimidating at first,
working in a terminal environment has a number of benefits (e.g. when compared
to working with graphical user interfaces):

- steps to produce certain outputs (for example manipulating data files) are
  much easier to reproduce, thereby leading to more reproducible analyses
- different tools can be combined (keyword: piping)
- support is easier since entering commands in a terminal and getting an output
  is more deterministic than using GUIs

## Tutorials and guides

The Software Carpentry foundation offers [helpful
lessons](https://swcarpentry.github.io/shell-novice/) on getting started with
the shell. Note that even though the lessons mention 'the Unix shell', the
guides are applicable to basically all kinds of shells and terminal
environments, e.g. Linux, OSX, and the Git bash in Windows.

## Essential commands

For the most basic use cases, working in the shell is not much different from
using an Explorer-like application (Finder etc.) and navigating your file system
and calling different applications to manipulate files. Thus, be on the lookout
for the following commands:

- `pwd`: Print where you currently are in your file system.
- `ls`: List the current directory's content.
- `cd`: Change the directory to a new path.
- `mkdir`: Make a new directory.
- `cp`: Copy a file or a directory.
- `mv`: Move a file or a directory.

Remember that you can call `man` (e.g. `man ls`) to get a detailed help page for
the command specified. If `man` is not available for a command (as is the case
for most of our tools as well as many other command line packages), you can try
calling the command with `-h` or `--help`, e.g. `cldfbench -h`.

## csvkit

Having read the [guide on virtual environments](python.md#virtual-environments),
installing [`csvkit`](https://csvkit.readthedocs.io/en/latest/index.html) is a
good first step to familiarize yourself with the shell and, particularly,
piping.

For the sake of this small tutorial, let us create a new virtual environment
into which we can install `csvkit`:

```
$ python -m venv csvtutorial
```

Activate the newly created virtual environment:

```
$ source csvtutorial/bin/activate
```

And install `csvkit`. (I'll omit the (csvtutorial) prefix in the following
snippets, however, make sure that you're working inside the virtual
environment.)

```
$ pip install csvkit
```

`csvkit` offers a number of different commands that can be called directly from
the shell. We'll begin with `csvstat` to get a summary of our CLDF example
dataset (note that we add `-y0` in order to correctly load our CSV file):

```
$ csvstat -y0 examples/halenepal/forms.csv
```

This will give you an overview over all the columns in the CSV file as well as
some basic information regarding their composition. Next, we'll see the piping
operator in action (and we'll leave it to the reader to use `man` to explorer
what `-S` does for the `less` command):

```
$ csvlook -y0 examples/halenepal/forms.csv | less -S
```

Read this from left to right. First we call `csvlook` and give it our
`forms.csv` as input. Then, the piping operator `|` takes the result of this
call and hands it over to the `less` command. What we get is a neatly rendered
table-like view of our CSV file. Piping commands is a powerful technique to hand
over the output of one operation to another application/function/module.

Next, let's see what columns we can work with in our CSV file:

```
$ csvcut -n examples/halenepal/forms.csv
```

We get a list of all the columns (headers) in the file. We can either use their
ID (1, 2, 3, ...) or their name to operate on them:

```
$ csvcut -c Language_ID,Parameter_ID,Form examples/halenepal/forms.csv
```

This gives us the contents of the selected columns (and only the selected
columns). Can you pipe the previous command to `less` in order to get a better
view of the data?

Piping of course works over multiple steps. Here, we first select three columns,
then print them as a table, and then have a look at the first 10 lines (see `man
head`):

```
$ csvcut -c Language_ID,Parameter_ID,Form examples/halenepal/forms.csv | csvlook -y0 | head
```

We can also easily pass this shortened table to `csvstat`:

```
$ csvcut -c Language_ID,Parameter_ID,Form examples/halenepal/forms.csv | csvstat -y0
```

Another powerful command from `csvkit` is `csvgrep`. With this, we can filter
columns using a pattern or a string. Here, we first select three columns and
then filter the `Language_ID` column for the string `Kham` (i.e. the language
name), then pretty-print it as a table and then pipe it to less:

```
$ csvcut -c Language_ID,Parameter_ID,Form examples/halenepal/forms.csv | csvgrep -c Language_ID -m Kham | csvlook -y0 | less -S
```

Since CLDF is a relational data format, data are spread over multiple files
(think of multiple sheets in your favorite spreadsheet software). In the case of
our example dataset, `forms.csv` lists lexemes and `parameters.csv` lists
information with respect to the concepts represented by the individual lexemes.
Using `csvkit`, we can easily create a new table that holds both of these
information (essentially 'glueing' together both tables). Here, we call
`csvjoin` and we give it the name of the columns we want to use to join the data
together. First, `Parameter_ID`, since that is the name of the parameters
columns in `forms.csv` (also the first file we provide as input), then `ID`,
since that is the ID referred to in `Parameter_ID` in `forms.csv` (the second
file we provide as input):

```
$ csvjoin -y0 -c Parameter_ID,ID examples/halenepal/forms.csv examples/halenepal/parameters.csv | csvlook | less -S
```

