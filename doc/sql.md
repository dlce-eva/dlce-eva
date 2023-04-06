# SQL - the Structured Query Language

Thanks to [cldf createdb](https://github.com/cldf/pycldf#converting-a-cldf-dataset-to-an-sqlite-database) each
CLDF dataset can be loaded into a [SQLite database](https://sqlite.com/index.html), i.e. made amenable to querying
with [SQL](https://en.wikipedia.org/wiki/SQL).

SQL is a rather big standard, but a small subset of it will get you a long way towards aggregating data for analysis
on the fly - rather than spending time and effort with reading and writing data from/to files. A good introduction 
is provided by the Software Carpentry lesson on [Databases and SQL](https://swcarpentry.github.io/sql-novice-survey/).
Diving deeper can be guided by the content on the [SQLite tutorial site](https://www.sqlitetutorial.net/).
Make sure to have look at [how CLDF is translated to SQL schema objects](https://github.com/cldf/cldf/blob/master/extensions/sql.md)
before you start exploring CLDF data in SQLite. And if you plan to work with a dataset with many tables (e.g. the 
[Austronesian Comparative Dictionary](https://clld.org/2023/03/17/acd.html)), you may want to [create an entity relationship diagram](https://github.com/cldf/cldfviz/blob/main/docs/erd.md)
first, to inform your exploration.

SQL is also quite old, which doesn't translate to out-dated but to having excellent tool support. A good GUI tool
to work with SQLite databases is [DBeaver](https://dbeaver.io/). For other options (and a guide on installing the basic
SQLite tools), see [the SQLite tutorial page](https://www.sqlitetutorial.net/download-install-sqlite/).

The [sqlite3 shell command](https://sqlite.org) itself provides a "SQL shell", i.e. an interactive [REPL](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop)
to interact with SQLite databases. You can try it out without installing anything in your browser by visiting
https://sqlite.org/fiddle/index.html 


## Working with SQLite databases in R or Python

While the above listed tools are good for exploration, analysing data will typically happen in a computing environent like
a Python or R program. Due to its ubiquity, SQLite has excellent support in both.

For R, the [RSQLite package](https://cran.r-project.org/web/packages/RSQLite/vignettes/RSQLite.html) provides basic
support, while [tidyverse's dbplyr](https://dbplyr.tidyverse.org/) provides an abstraction layer to create SQL
queries in a way that might be more familiar (and can be used with backends other than SQLite).

Python comes "with batteries", so [sqlite3 support is in the standard library](https://docs.python.org/3/library/sqlite3.html).
