# Python

Python is the main programming language we use at the DLCE (however, there are
also Java and R projects). Python is a dynamically typed (variables don't need
to be given a type when they're created) programming language with a large
ecosystem and an easy syntax.

## Tutorials and guides

The Software Carpentry Foundation provides two very nice introductions to
Python:

- [Programming with
  Python](https://swcarpentry.github.io/python-novice-inflammation/index.html):
  An introduction to the Python programming language on the basis of a data
  analysis project.
- [Plotting and Programming in
  Python](https://swcarpentry.github.io/python-novice-gapminder/): A slightly
  more advanced introduction to Python concerned with plotting and more advanced
  programming concepts.

## Setting up Python

### Versions

Newer Python versions generally bring with them improvement and fixes.
Unfortunately, sometimes they also introduce incompatibilities with older code.
As of right now, the most recent stable Python version is `3.9.2`. Currently, we
recommend installing Python `3.8.8` as most of our projects should run without
any problems with this version.

### Windows

[The Windows installer for Python](https://www.python.org/downloads/windows/)
can generally be recommended for getting Python to work on Windows. Make sure to
check all settings related to `PATH` modifications during the setup so that
Python is globally available on your system.

If Python is not part of your `PATH`, you can change that using the ‘Set
environment variables for this user account’ dialog.

TODO: Less handwavey description on how to set `PATH` on Windows

The name of the path you need to add is
`%USERPROFILE%\AppData\Local\Python\Python<VERSION>\Scripts`, where `<VERSION>`
needs to be replaced with Python's major and minor version, without the period.

For example, if you are using Python 3.8 (or 3.8.1, 3.8.2, etc.), the folder is
called:

    %USERPROFILE%\AppData\Local\Python\Python38\Scripts

However, if you are using Python 3.9 (or 3.9.1, 3.9.2, etc.), the folder is
called:

    %USERPROFILE%\AppData\Local\Python\Python39\Scripts

### OSX

Even though there is a dedicated Python installer available on the Python
website, we generally recommend installing Python on OSX using
[brew](https://brew.sh/).

Python 3.8 can easily be installed with `brew` with `brew install python@3.8`.
Since OSX still ships with an old Python version (2.7), make sure that you're
calling the correct Python version on OSX after installing it (this can normally
be achieved by using `python3`, i.e. check the output of `python3 --version` on
the command line).

### Linux

Most recent Linux distributions ship with Python out of the box. Should Python
not be available (check with `python --version` on the command line), it is
generally recommend to install Python using your distributions's respective
package manager.

### Virtual environments

Python relies on packages (or modules) to get work done. These consist of code
that provide some functionalities that can be shared between them. Typically,
your system will have a global location for packages. This location is normally
used to provide basic functionalities for Python and your system. In our
everyday research work, we don't want to mess with the global location, which is
why we're using virtual environments.

In contrast to the global package location, virtual environments provide an
encapsulated/local package location that we can work with without risking
damaging our global package location. Virtual environments can be created easily
and on a 'per-project' basis. This also makes it trivial to install different
versions of Python packages at the same time.

Virtual environments can created out of the box with the `venv` module provided
by Python:

```
$ python -m venv YOURVENVNAME
```

This will create a folder `YOURVENVNAME` with a self-contained Python
environment. After creating the virtual environment, it has to be activated in
order to use it:

```
$ source YOURVENVNAME/bin/activate
```

Afterwards, your command line prompt will indicate that you're now working
within the newly created virtual environment:

```
$ (YOURVENVNAME) ...
```

All commands that you'll run after activating the virtual environment will now
be run within the environment. For example, if you'd like to install the
`cldfbench` Python package:

```
$ (YOURVENVNAME) pip install cldfbench
```

This will install `cldfbench` into the virtual environment YOURVENVNAME. Note
that this means that `cldfbench` will only be available after the virtual
environment has been activated.

