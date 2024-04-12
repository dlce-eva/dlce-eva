CLDF for dummies
================
Hedvig Skirgård
2023-11-30

# CLDF for dummies

This document outlines some of the very basics of the Cross-Linguistic
Data Formats (CLDF) for researchers who want to use the data sets for
analysis, comparison or plotting. CLDF is a way of organizing language
data, in particular data sets with many different languages in it. The
basic organisation is a set of tables, usually in csv-sheets
(languages.csv, forms.csv etc). These documents are linked to each other
in a specific way which makes it possible to combine them into an
interlinked database. The files are all governed by standards, there are
sanity-checks to make sure all lines up right. Because they are often
just plain csv-sheets they can easily be read in by most data analysis
software programs like Python, R, Julia etc or just regular spreadsheet
programs like LibreOffice or Microsoft Excel. It is not necessary to use
FileMakerPro, Microsoft Access or similar programs.

It’s plain, flat and simpler than you might think. In this document, you
will learn the very basics on how it works.

The data format was first published in 2018 [1] and has since then
been used in a large amount of different data sets. You can see a list of
them [here](https://github.com/cldf-datasets/clld_meta/blob/master/cldf/contributions.csv).

CLDF is well-documented. This document is a very basic intro, for more
advanced queries go to <https://github.com/cldf/cldf/#readme> and
<https://cldf.clld.org/>

## Before we start

Good things to keep in mind:

-   the best way to learn how CLDF looks like is to poke around in an
    existing dataset. Open the files, check what’s in there, form
    assumptions and then check if the assumptions are always true. Below
    are two recommended starter-datasets:
    -   Wordlist: NorthEuraLex v4.0
        <https://github.com/lexibank/northeuralex/tree/v4.0/cldf>
    -   Structure: Grambank v1.0.3
        <https://github.com/grambank/grambank/tree/v1.0.3/cldf>
-   another way to inspect CLDF datasets is to read the
    spec for the dataset. They are the ones that'll tell you what the
    columns really are etc.
    -   <https://github.com/lexibank/northeuralex/blob/v4.0/cldf/README.md>
    -   <https://github.com/grambank/grambank/blob/v1.0.3/cldf/README.md>
-   many CLDF-datasets are continuously released, so make sure to keep
    track of which **version** you are using
-   if you use Python, make sure to check out pycldf
-   if you use R, keep an eye out for rcldf which is in development
-   this document is about how to navigate existing CLDF-datasets as an
    end-user, not how to make one.
-   for more on *making* and *using* CLDF-datasets, have a look in the
    cookbook tutorials
    [here](https://github.com/cldf/cookbook/tree/master#readme)
-   there already exists a lot of documentation on how CLDF works, this
    document is not meant to be exhaustive but just a gentle entry to
    get you going. For more, see:
    -   [the CLDF specification](https://github.com/cldf/cldf/#readme)
    -   [the CLDF website](https://cldf.clld.org/)


## Dictionary
In CLDF, there are some specific terms that are good to know about.

- **property**: column in a table. The property `languageReference` is often realised in a column called `Language_ID`. All CLDF properties are listed in the [CLDF ontology](https://cldf.clld.org/v1.0/terms.html).
-- **component**: table which conforms to specific CLDF-rules. The component "LanguageTable" is often found in a file called "languages.csv". All CLDF components (including their default metadata) are listed at https://github.com/cldf/cldf/tree/master/components

## How to know if you’re dealing with a CLDF-dataset

You are dealing with a CLDF-data set if there is a file ending with the
extension `.json` and at the top it identifies a CLDF-dataset type. For
example, it could be
`dc:conformsTo: http://cldf.clld.org/v1.0/terms.rdf#StructureDataset`.
(There is one exception, see “Good to know” below.)

Often there is a folder called “cldf” with files like “languages.csv”,
“values.csv” and “StructureDataset-metadata.json” in it. The last file
will be different depending on the type of data set.

Here are some examples of data sets that are available in CLDF that you
may have encountered:

-   WALS (World Atlas of Language Structures)

-   PHOIBLE (Phonetics Information Base and Lexicon)

-   D-PLACE (Database of Places, Language, Culture and Environment)

-   Glottolog

-   Lexibank

-   Grambank

> [!TIP]
> Good to know: [It is possible for a CLDF-dataset to only consist of one
> file](https://github.com/cldf/cldf#metadata-free-conformance)! No JSON-file,
> no set of csvs. Just one file, for example `values.csv`. In such cases,
> the file doesn’t have any meta-data specified and just conforms to all
> the default settings for all components, properties etc. You can’t tell
> by a JSON-file that it’s a CLDF-dataset because there isn’t one.
> This type of CLDF-data set is rare, and will not be dealt with further here.

### Types of CLDF-datasets

There are five types of CLDF-datasets. They are also known as [“modules”](https://github.com/cldf/cldf/tree/master/modules).

-   Wordlist (lexicon, has Forms and often Cognates)
-   Structure dataset (grammar or other types of information with one
    value for a Parameter and a Feature, has Values)
-   Dictionary (particular kind of lexicon, has Entries and Senses)
-   Parallel text (collections of paragraphs of the same text in
    different languages, has Forms, Segments and FunctionalEquivalents)
-   TextCorpus (cohesive stretches of discourse in the object language)
-   generic (no specifics)

## Contents

Each CLDF-dataset (except the metadata-free ones) consists minimally of:

-   a set of tables (usually in csv-sheets)
-   a JSON-file

The tables are usually in csv-format and contain the data itself. The
JSON-file has information *about* the dataset, for example the type of
dataset is, what the contents are, what the filenames are etc.

Many CLDF-datasets also contain a bibTeX-file with bibliographic
references for the data. In such cases, each data-point may be tied to a
reference by the key in the bibTeX entry. Usually the key is in a column
called “Source” in the ValueTable or FormTable. The bibTeX file is
usually called “sources.bib”. If it’s called something else, it’ll say
so in the meta-data JSON-file.

## Tables inside the datasets

There are some tables that occur in most CLDF-datasets, and some that
occur only in certain types. For example, there is no table with word
forms for StructureDatasets - that’s for Wordlists and Dictionaries.

The tables have specific names in the CLDF-world and have pre-defined
specifics. The names are different from their filenames. You can see
which name is tied to which file in the json. “LanguageTable” is usually
found in the file languages.csv, “CodeTable” in codes.csv, “ValueTable”
in values.csv, “CognateTable” in cognates.csv etc.

-   LanguageTable -\> languages.csv (contains minimally ID)
-   FormTable -\> forms.csv (contains minimally ID, Form, Language_ID,
    Parameter_ID)
-   ParameterTable -\> parameters.csv (contains minimally ID, Name) etc.

The JSON-file of metadata contains information on which tables (a.k.a components) 
are inside the dataset and in turn what columns (a.k.a properites) the have. 
You can see what type of CLDF-component a table is by inspecting the line in the 
section of the code that contains `dc:conformsTo`, e.g. `dc:conformsTo": 
"http://cldf.clld.org/v1.0/terms.rdf#ValueTable` means that the component being 
described in that section of the code is a ValueTable. Later down in the section 
describing the component, we can find the specific filename in the url-field, 
e.g. `url": "values.csv`. Now we know there's a ValueTable and it's in the file values.csv.

The specific line in the 
meta-data JSON file contains the string 
Types of tables that have special meaning and rules in CLDF are known as `components`. **You can’t 
always bank on LanguageTable being in languages.csv**. SQl, `pycldf` and 
`rcldf` can handle this for you, i.e. look up in the JSON-filewhat component is 
where and set all that up.

Each type of table contains columns which conform to [CLDF-rules
](https://cldf.clld.org/v1.0/terms.html), i.e. properties. For example, FormTables need 
to have columns for the properties “id”, “form” and “Language_ID” and they in turn 
need to look a certain way.

Tables can have more columns than the minimal requirement and can have
columns that don’t map onto CLDF properties at all.


#### Tables in most CLDF-dataset

Here are CLDF-tables that occur in most CLDF-datasets.

-   LanguageTable - list of all of the languages in the dataset. May
    also include things classified by Glottolog as dialects or
    proto-languages. Includes meta-information like longitude, language
    family etc.
-   ParameterTable - contains a definition of the variables. For
    lexicon, these are the concepts, for grammar these are the features.

Wordlist also contain

-   FormTable - the forms for each concept for each language
-   CognateTable (not obligatory) - the cognate classification per form
    per concept per language

Structure data-sets also contain

-   ValueTable - the value for each parameter and language. Usually also
    Comment and Source.
-   CodeTable - The list of possible values for each parameter. For
    example, GB020 in Grambank is a binary feature and can take 0, 1 and
    ? whereas EA016 in the Ethnographic Atlas (D-PLACE) can take 1, 2
    or 9. The options are often exclusive of each other for each
    language. There are examples of languages that are coded for more
    than one value, usually with extra information on proportions.

> [!TIP]
> Good to know: for the CLDF-dataset of D-PLACE (v1 and v2), the
> LanguageTable contains a row per *society* - not per language. There is a column 
> for the Glottocode of the language associated with that society.

> [!TIP]
> Good to know: in the formal CLDF-ontology, "tables" are called "components" 
> and columns within tables are "properties"

#### Columns in tables

Each table consists of a set of columns. The names of these columns are
often for example "ID", "Longitude", "Value" etc. However, they can
vary. The meta-data contains information on which column name maps onto
what property in the CLDF-universe. For example, there is the property
"source"", which has the propertyURL
<http://cldf.clld.org/v1.0/terms.rdf#source> and often is mapped onto a
column called "Source". However, if one CLDF-creator wanted to name this
column "Reference" instead, that's all well and good. The
JSON metadata-file would tell the users that the column "Reference"
corresponds to the standardised property "source" and point to the
property-url. As with filenames of tables, you can often get by with
assuming that bibliographic references are in a column called "Source"
and the LanguageTable is in languages.csv --- but this needn't always be
true! Studying the JSON meta-data file is often worthwhile.

# Example: Wordlist

Below is a tiny Wordlist CLDF-dataset. This dataset contains 3 words in
2 languages. The first two tables, LanguageTable and ParameterTable
contains information about the languages and parameters - in this case
concepts. The FormTable contains the actual forms. For one of the
concepts, one of the languages has two words and both are listed.

The meta-data JSON-fileis not included here. You can see an example of a
Wordlist-metadata JSON-file here:
<https://github.com/lexibank/abvd/blob/master/cldf/cldf-metadata.json>.

**LanguageTable**

One row = one language (or sometimes dialect or proto-language, i.e
above language in a tree). The ID column uniquely identifies each
language in the dataset. In other tables, the column that links to the
ID column here is called “Language_ID”.

| ID  | Name     | Glottocode |
|-----|----------|------------|
| 15  | Bintulu  | bint1246   |
| 18  | Chamorro | cham1312   |

> [!TIP]
> Good to know: Sometimes the IDs in LanguageTable are Glottocodes or ISO
> 639-3 codes, but they don’t have to be. They just have to be unique
> within that dataset. In Grambank, the IDs are Glottocodes, but WALS has
> its own specific unique code-system different from both Glottocodes and
> ISO 639-3. If you want Glottocodes, go look for a column called
> Glottocode in the LanguageTable - don’t use the ID column.

> [!TIP]
> Good to know: Glottocodes contain 4 letters or numbers and then 4
> numbers. The first 4 characters are not always letters. For example,
> `ww2p1234` and `3adt1234` are existing glottocodes.

**ParameterTable**

One row = one parameter. The ID column uniquely identifies each
parameter in the dataset. In other tables, the column that links to the
ID column here is called “Parameter_ID”.

| ID         | Name    | Concepticon_ID |
|------------|---------|----------------|
| 144_toburn | to burn | 2102           |
| 2_left     | left    | 244            |

**FormTable**

One row = one form. The ID column uniquely identifies each form in the
dataset. In other tables, the column that links to the ID column here is
called “Form_ID”. Here we also see Parameter_ID, which links to the
column ID in the ParameterTable and Language_ID which links to the
column ID in the LanguageTable.

| ID              | Parameter_ID | Language_ID | Form   | Source        |
|-----------------|--------------|-------------|--------|---------------|
| 15-144_toburn-1 | 144_toburn   | 15          | pegew  | Blust-15-2005 |
| 15-144_toburn-2 | 144_toburn   | 15          | tinew  | Blust-15-2005 |
| 18-2_left-1     | 2_left       | 18          | akague | 38174         |

In this example, and in several other WordList datasets (but not all),  
the ID column is in fact a combination of the Language_ID, Parameter_ID and
last a number to distinguish if there are more than one form. For
example, because Bintulu has two words for “to burn”, there are two rows
with different Forms but the same Parameter_ID (they both mean “to
burn”). The ID column, which identifies each form has a number at the
end of the string which indicates the different form. If there is only
one form, the string ends with “-1”, but as you can see for “to burn” it
first has “-1” and then “-2”.

**Source**

Optional file, but often present in the form of a bibTeX-file. One entry
= one source. The bibTeX file is usually called “sources.bib”, but not
necessary (check `metadata.json` as usual). The bibTeX Key (the first
string after `@BIBTEXENTRYTYPE{`) maps onto the Source column in the
FormTable above.

```         
@misc{Blust-15-2005,
    author = {Blust},
    date = {2005},
    howpublished = {personal communication}
}

@book{38174,
    author = {Topping, Donald M. and Ogo, Pedro M. and Dungca, Bernadita C.},
    address = {Honolulu},
    publisher = {The University Press of Hawaii},
    title = {Chamorro-English dictionary},
    year = {1975}
}
```

## example: Wordlist - linking together

Now let's turn to joining information from multiple tables into one. The 
information in the different tables are linked to each other via what is called
primary and foreign keys. The primary key in a table is found in the column ID and 
uniquely identifies each row. In a FormTable, it identifies each form, in a ParameterTable, 
each parameter and so on. There are also foreign keys, these are links to rows in other tables. 
For example, in the FormTable in our example there is a column called "Parameter_ID", which
is linking the information it rows in the ParameterTable. Generally, most CLDF-dataset tables 
follow the naming column convention "ID in FormTable = Form_ID in other tables".

-   Langugage_ID in other tables -\> ID column in LanguageTable
-   Parameter_ID in other tables -\> ID column in ParameterTable
-   Form_ID  in other tables -\> ID column in FormTable
-   etc.

These primary and foreign keys make it easy to combine information from many different tables.

As an example, let's list all word forms in our Wordlist with the name of the language they belong to.
This requires adding information from LanguageTable for each row in FormTable - we [*join*](https://swcarpentry.github.io/sql-novice-survey/07-join.html) the
information from two tables to create a new table.

We can do this for example in R, using one of [dplyr's `*_join` functions](https://www.rdocumentation.org/packages/dplyr/versions/0.7.8/topics/join). Since we want to create a joined table with one row for each
row in FormTable, we'll use `left_join` and pass FormTable as first table and LanguageTable as second table. As explained above, the foreign key `Language_ID` in FormTable references the corresponding row in LanguageTable that has information about the language a form belongs to. Thus, for each row in FormTable, we join
information from the row in LanguageTable with `ID` matching the `Language_ID` in FormTable. This
translates to the following code in R (with base R pipes (`|>`)):

```R
library(dplyr)

JoinedTable <- FormTable |>
    dplyr::left_join(LanguageTable, by = c("Language_ID" = "ID"))
```

and the resulting table will look as follows:

| ID         | Parameter_ID | Language_ID | Form      | Source        | Glottocode | Name |
|----------- |-----------   |------------ |---------- |-----------    |----------- |----- |
| 15-144_toburn-1 | 144_toburn   | 15     | pegew     | Blust-15-2005 | bint1246   | Bintulu|
| 15-144_toburn-2 | 144_toburn   | 15     | tinew     | Blust-15-2005 | bint1246   | Bintulu|
| 18-2_left-1     | 2_left       | 18     | akague    | 38174         | cham1312   | Chamorro|



> [!CAUTION]
> Sometimes a LanguageTable contains a column called “Language_ID”, i.e. a key referencing
> another row in the same table. This is called a "self-referential foreign key".
> For the glottolog-cldf dataset the column Language_ID in the LanguageTable 
> contains information on the language that a dialect belongs to. For example, 
> Eastern Low Navarrese is a dialect of the language Basque. The glottocode of
> this dialect is east1470. The glottocode of the language Basque is
> basq1248. In the LanguageTable of glottolog-cldf the row of the dialect has basq1248 
> in the column "Language_ID". This helps when you might want to
> match by the languages rather than the dialect-level. In Grambank, 
> there  is a similar column to glottolog-cldf's "Language_ID", but it is called
> “Language_level_ID” to make the nature of the relation clearer.

# Example: Structure

TBA

# CLLD, clld and CLDF

CLDF is a type of data-format, the set of tables etc described here.
CLLD was a larger project and stands for Cross-Linguistic Linked Data.
CLLD was a project for publishing databases on the web, it ended in
2016. clld is a web app framework - a piece of software. clld and CLDF
came out of the CLLD-project but are distinct from it. CLDF data
interfaces smoothly with clld web applications.

## Advanced

This document is only a very basic intro. If you want to learn more, go
to: 
- [the CLDF specification](https://github.com/cldf/cldf/#readme)
- [the CLDF cookbook](https://github.com/cldf/cookbook/tree/master#readme)
- [the CLDF website](https://cldf.clld.org/)

## References

[1] Forkel, R., List, J. M., Greenhill, S. J., Rzymski, C., Bank, S.,
Cysouw, M. Hammarström, H., Haspelmath, M., Kaiping, G.A. and Gray, R.
D. (2018). Cross-Linguistic Data Formats, advancing data sharing and
re-use in comparative linguistics. Scientific data, 5(1), 1-10.
