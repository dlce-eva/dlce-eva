# CLDF

CLDF (Cross-linguistic Data Formats) is our way of storing (linguistic) data. At
its core, a CLDF dataset is

- a collection of UTF-8 encoded CSV files
- that are described by a metadata file
- and that conforms to a certain type of [CLDF
  module](https://github.com/cldf/cldf#cldf-modules)

A good mental image to keep in mind is that a CLDF dataset is a collection of
tables that are 'glued' together by means of the accompanying JSON metadata
file. This makes it possible to harness the full power of the [relational
model](https://en.wikipedia.org/wiki/Relational_model) for the data. For more
details see the [CLDF specification](https://github.com/cldf/cldf), as well as
the [CLDF cookbook](https://github.com/cldf/cookbook) and the [CLDF
examples](https://github.com/cldf/cldf/tree/master/examples).

## CLDF tools

### pycldf

[`pycldf`](https://github.com/cldf/pycldf) can be used for programmatically
accessing, writing, and verifying CLDF data.

### cldfbench

[`cldfbench`](https://github.com/cldf/cldfbench) is our main tool to create CLDF
data from existing data. Also have a lookt at
[cldf-datasets](https://github.com/cldf-datasets) to see `cldfbench` in action.

### datasette-cldf

Create a locally browsable representation of a CLDF dataset with
[datasette-cldf](https://github.com/cldf/datasette-cldf). Very helpful to
illustrate the relational idea behind CLDF data.

### cldfviz

[cldfviz](https://github.com/cldf/cldfviz) makes it possible to illustrate CLDF
data (and more specifically particular features within a dataset) on a map.

