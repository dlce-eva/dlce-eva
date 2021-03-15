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

## csvkit

```
$ csvstat -y0 examples/halenepal/forms.csv
```

```
$ csvlook examples/halenepal/forms.csv | less -S
```

```
$ csvcut -n examples/halenepal/forms.csv
```

```
$ csvcut -c Language_ID,Parameter_ID,Form examples/halenepal/forms.csv
```

```
$ csvcut -c Language_ID,Parameter_ID,Form examples/halenepal/forms.csv | csvlook -y0 | head
```

```
$ csvcut -c Language_ID,Parameter_ID,Form examples/halenepal/forms.csv | csvstat -y0
```

```
$ csvcut -c Language_ID,Parameter_ID,Form examples/halenepal/forms.csv | csvgrep -c Language_ID -m Kham | csvlook -y0 | less -S
```

```
$ csvjoin -y0 -c Parameter_ID,ID examples/halenepal/forms.csv examples/halenepal/parameters.csv | csvlook | less -S
```

