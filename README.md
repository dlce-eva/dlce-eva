# RDM at DLCE MPI EVA

Research data management at the Department of Linguistic and Cultural Evolution
of the Max-Planck-Institute for Evolutionary Anthropology

One of the main goals of out RDM efforts is making sure researchers can create [reproducible](doc/reproducibility.md)
results.

## Environment

RDM at DLCE is based on a handful of foundational tools and principles:
- [CLDF](https://cldf.clld.org) is used as the standard exchange format for all
  our data - in most cases it is used as storage format as well, and in many
  cases even as primary or raw format.
- Data management tools are typically implemented as Python packages, with the
  functionality provided as Python API or via CLI.
- Curation history for our data is maintained by using the `git` version control
  tool to manage the raw data.

Thus, to make use of this toolset, members of DLCE should be familiar with
- Git - See [doc/git.md](doc/git.md)
- Python - See [doc/python.md](doc/python.md)
- Shell/working on the command line - See [doc/shell.md](doc/shell.md)
- Text encoding and Unicode - See [doc/text-and-encodings.md](doc/text-and-encodings.md)
- CLDF - See [doc/cldf.md](doc/cldf.md)
- Reference catalogs at DLCE - See [doc/catalogs.md](doc/catalogs.md)
- Databases at DLCE - See [doc/databases.md](doc/databases.md)

In particular for working with larger datasets, SQLite can be very useful. See [doc/sql.md](doc/sql.md).

We recommend reading the tutorials and hints in the order they're mentioned in
(i.e. start with Git and Python, then have a look at working on the shell and
lastly, CLDF). Feel free to open an issue in this repository if you have any
questions or if you're experiencing issues with any of the tools/pipelines.

