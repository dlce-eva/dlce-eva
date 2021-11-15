Working with textual data in Python
===================================


How do computers represent text?
--------------------------------

*Goal:*
We need to store written language in computer memory or on some storage device
(hard drive, usb stick, etc.).

*Problem:*
Computers can only really store binary numbers.

*Solution:*
Actually quite simple:  Just assign a number (a.k.a. *code point*) to each
symbol you need and store those on disk.

*Example:*
[ASCII][ascii] used 7 bits of memory per character and could thus encode 128
symbols – from `0000000` (0) to `1111111` (127), for instance:

 * The upper-case letter `A` is number `1000001` (65)
 * The lower-case letter `a` is number `1100001` (97)
 * The apostrophe `'` is number `0100111` (39)
 * A blank space ` ` is number `0100000` (32)

*Note:*
Many (but not all) other encoding schemes, such as [Latin-1][latin1] or
[Windows-1252][cp1252], are actually backwards-compatible with ASCII.  This
means that they encode the same characters as ASCII for the range 0–127 but
different charaters for code points above that.  This also includes UTF-8 (see
below).

[ascii]: https://en.wikipedia.org/wiki/ASCII
[latin1]: https://en.wikipedia.org/wiki/ISO/IEC_8859-1
[cp1252]: https://en.wikipedia.org/wiki/Windows-1252

### The Unicode standard

*Problem:*
Different languages or regions used different conflicting encoding tables.  What
looked like `Привет!` on one computer might have shown up as `Ïðèâåò!` on
another.

*Solution:*

 * [Unicode][unicode]: An international standard for encoding textual data

 * An ever-growing list of code points for every known symbol used in human
   communication (different writing systems, technical symbols, diacritics,
   mathematical symbols, emoji, etc.)

[unicode]: https://www.unicode.org/main.html

*Tip:*
If you want to find out in Python, what code point is assigned to a symbol, use
the `ord()` function:

```python
>>> ord('a')
97
>>> ord('ä')
228
>>> ord('ы')
1099
>>> ord('家')
23478
```

If you want to convert a code point back into a symbol, use `chr()`:

```python
>>> chr(97)
'a'
>>> chr(228)
'ä'
>>> chr(1099)
'ы'
>>> chr(23478)
'家'
```

If you want to see a human-readable name of a symbol, use `unicodedata.name`:

```python
>>> import unicodedata
>>> unicodedata.name('a')
'LATIN SMALL LETTER A'
>>> unicodedata.name('ä')
'LATIN SMALL LETTER A WITH DIAERESIS'
>>> unicodedata.name('ы')
'CYRILLIC SMALL LETTER YERU'
>>> unicodedata.name('家')
'CJK UNIFIED IDEOGRAPH-5BB6'
```

### UTF-8 encoding

*Problem:*
Since code-points can become quite large, storing the number takes up more space
in memory or on storage -- currently 32 bits (4 bytes) of memory for each
symbol, which is wasteful.

*Solution:*
Variable-width encodings, which use less space for smaller numbers and more for
larger ones.  The most commonly-used encoding is [UTF-8][utf8], which uses up
from one up to four bytes for a single Unicode codepoint.

[utf8]: https://en.wikipedia.org/wiki/UTF-8

```python
>>> list('a'.encode('utf-8'))
[97]
>>> list('ä'.encode('utf-8'))
[195, 164]
>>> list('ы'.encode('utf-8'))
[209, 139]
>>> list('家'.encode('utf-8'))
[229, 174, 182]
>>> list('😐'.encode('utf-8'))
[240, 159, 152, 144]
```

*Note:*
Another, less commonly used, alternative is [UTF-16][utf16], which uses either
two or four bytes of memory per symbol.  Note that, unlike UTF-8, UTF-16 is
*not* backwards-compatible with ASCII.

[utf16]: https://en.wikipedia.org/wiki/UTF-16


Python and text
---------------

*Question:*
How does Python deal with text and text encodings?

*Answer:*
Starting with version 3.0, Python stores all strings internally as Unicode code
points, which makes working with non-English text quite painless.  However, text
files or data downloaded from the internet usually use some sort of text
encoding, so you will have to deal with that.

*Question:*
How does Python represent the difference between Unicode text and encoded text?

*Answer*
Python uses two kind of strings:

 * *Unicode strings* (or just *strings*) are – as mentioned above – lists of
   Unicode code points.  This is the default string you get, when you put text
   in quotation marks (`"` or `'`).

 * *Byte strings* are sequences of raw bytes that are used for encoded text (or
   any other kind of binary data).  They are signified by adding a `b` at the
   front of the string, `b'like so'`.  When displaying bytes strings, Python will
   show printable characters withing the ASCII range (0–127) verbatim.  Bytes that
   fall outside of the ASCII range are displayed with `\x` plus the number
   contained in that byte in hexadecimal.

*Example:*
The UTF-8-encoded version of the Unicode string `'Möwe'` looks as follows.

```python
b'M\xc3\xb3we'
```

Since the letters `M`, `w`, and `e` are part of the ASCII standard, they show up
in human readable form.  The umlaut `ö` however, is encoded using the two-byte
sequence `[195, 179]`, which is shown as two hexadecimal numbers: `\xc3` and
`\xb3`.

*Note:*
Usually, Python programmers work with Unicode strings almost exclusively and
only bother with byte strings if they are working on non-textual data, or if
they *really* need to keep the original encoded data in memory for whatever
reason.

### Encoding and decoding text

*Goal:*
You have a Unicode string and want to apply some encoding.

*Solution:*
To convert a string into an encoded sequence of bytes, call the string's
`encode` method and provide the appropriate encoding:

```python
>>> 'Möwe'.encode('utf-8')
b'M\xc3\xb6we'
```

*Note:*
Python actually supports numerous encodings right out of the box.  If you want
a full list, refer to [the official Python documentation][python-encodings].

[python-encodings]: https://docs.python.org/3/library/codecs.html#standard-encodings

```python
>>> 'Möwe'.encode('latin1')
b'M\xf6we'
```

*Goal:*
You have the reverse: an encoded piece of text that you want to decode into
a string.

*Solution:*
To convert a sequence of bytes into a string, use the `decode` method and
provide the appropriate encoding:

```python
>>> b'M\xc3\xb6we'.decode('utf-8')
'Möwe'
```

### Reading text from a file

*Prelude:*
The `open()` function can open files in one of two ways:  In binary mode and in
text mode.

 * In *binary mode* the contents of the file are read verbatim as a byte string.
 * In *text mode* the contents of the file are decoded and converted into
   a Unicode string.

*Question:*
How do you read binary data from a file?

*Answer:*
Open the file in binary mode using `open()` and pass in `'rb'` (as in **R**ead
**B**inary) as the second argument:

```python
>>> with open('file.txt', 'rb') as f:
...     data = f.read()
>>> type(data)
<class 'bytes'>
>>> # Note: you can always convert the data into Unicode after the fact
>>> unicode_data = data.decode('utf-8')
>>> type(unicode_data)
<class 'str'>
```

*Question:*
How do you read text from a file?

*Answer:*
If you want to read a text file in text mode, you don't need the second argument
at all – reading text data is `open()`'s default mode of operation.  Now you
can use the `encoding` parameter to set the appropriate encoding.

```python
>>> with open('file.txt', encoding='utf-8') as f:
>>>     data = f.read()
>>> type(data)
<class 'str'>
```

*Note:*
*Technically* the `encoding` parameter is optional – but only *technically*.
The reason is that Python's default encoding is actually different depending on
your operating system and system configuration.  Some might use UTF-8, some
might use UTF-16, some might use their own default encoding scheme.  If you
leave `encoding` to the default, your program might behave differently when it's
run on someone else's computer.  So it's a good habit to always specify the
`encoding` parameter when calling `open()`.
*Be safe – be explicit.*


Converting between different encodings on the Unix command-line
---------------------------------------------------------------

*Goal:*
You have a file using a specific encoding (e.g. *Latin 1*) and want to convert
it to another (e.g. *UTF-8*).  Also, you don't want to write your own program
in Python because you've got a limited amount of life-time and other stuff to
do (although writing such a program might be good exercise if you're new to
Python programming).

*Solution:*
To convert a file from one encoding to another, you can use [`iconv`][iconv(1)]:


```sh
$ iconv -f ENC -t ENC INPUT_FILE > OUTPUT_FILE
```

 * `-f ENC`: specifies the source encoding (`-f` stands for ‘*from*’)
 * `-t ENC`: specifies the target encoding (`-t` stands for ‘*to*’)
 * `INPUT_FILE`: path to the original file
 * `> OUTPUT_FILE`: path where you want to save the re-encoded file

[iconv(1)]: https://linux.die.net/man/1/iconv

*Example:*
Convert `original-file.txt` from `latin1` to `utf-8` and save the result to
`new-file.txt`.

```sh
$ iconv -f latin1 -t utf-8 original-file.txt > new-file.txt
```

If you want to know which encodings `iconv` spports, you can also ask it for a
list using the `-l` flag:

```sh
$ iconv -l
```

*Note:*
`INPUT_FILE` and `> OUTPUT_FILE` are actually optional.  If you leave out the
input file `iconv` will read from standard input instead, and if you leave out
the output file `iconv` will print to standard output.  This means you can also
use `iconv` in a good ol' Unix pipe:

```sh
$ printf "Möwe" | wc -c
5
$ printf "Möwe" | iconv -f utf-8 -t latin1 | wc -c
4
$ printf "Möwe" | iconv -f utf-8 -t utf-16 | wc -c
11
```


Common pitfalls
---------------

### Symbols that *look* the same but aren't

*Problem:*

```python
>>> 'Hoc' == 'Нос'
False
```

*Explanation:*
The string to the left is the word `Hoc` in Latin letters, i.e.:

```python
>>> [ord(c) for c in 'Hoc']
[72, 111, 99]
>>> import unicodedata
>>> print('\n'.join(unicodedata.name(c) for c in 'Hoc'))
LATIN CAPITAL LETTER H
LATIN SMALL LETTER O
LATIN SMALL LETTER C
```

The string to the right, on the other hand, is the Russian word `Нос` ‘nose‘,
written in Cyrillic letters, i.e.:

```python
>>> [ord(c) for c in 'Нос']
[1053, 1086, 1089]
>>> import unicodedata
>>> print('\n'.join(unicodedata.name(c) for c in 'Нос'))
CYRILLIC CAPITAL LETTER EN
CYRILLIC SMALL LETTER O
CYRILLIC SMALL LETTER ES
```

Both strings look the same to the naked eye but they are *different symbols*,
that have *different meaning* and got assigned different *Unicode codepoints*.

*Solution:*
Unfortunately, there is no simple catch-all solution for this, as there is no
unified way to normalize text across different writing systems (Do you normalise
Cyrillic `с` to Latin `c` because they look the same, or to Latin `s` because
that's what it sounds like in Russian?).

### Characters with accents on them, combining diacritics, and unicode normalisation

*Problem:*

```python
>>> 'č' == 'č'
False
```

*Explanation:*
The string to the left is just a single Unicode code point:

```python
>>> [ord(c) for c in 'č']
[269]
>>> print('\n'.join(unicodedata.name(c) for c in 'č'))
LATIN SMALL LETTER C WITH CARON
```

However, the string to the right is actually a regular ol' `c`, followed by
a *combining diacritic*, which has its own Unicode code point:

```python
>>> [ord(c) for c in 'č']
[99, 780]
>>> print('\n'.join(unicodedata.name(c) for c in 'č'))
LATIN SMALL LETTER C
COMBINING CARON
```

*Solution:*
This ambiguity can be avoided by normalising the string before working with it.
There are two major ways of normalising combining diacritics:

 * Composing combining diacritics into single characters wherever possible
   (a.k.a. *Normalised Form Composition*, NFC)
 * Decomposing all single characters into combining diacritics
   (a.k.a. *Normalised Form Decomposition*, NFD)

In Python you can achieve this with the `unicodedata.normalize` function:

```python
>>> import unicodedata
>>>
>>> # original string: two different č's
>>> text = 'čč'
>>> print('\n'.join(unicodedata.name(c) for c in text))
LATIN SMALL LETTER C WITH CARON
LATIN SMALL LETTER C
COMBINING CARON
>>>
>>> # Normalised Form Composition
>>> nfc = unicodedata.normalize('NFC', text)
>>> print('\n'.join(unicodedata.name(c) for c in nfc))
LATIN SMALL LETTER C WITH CARON
LATIN SMALL LETTER C WITH CARON
>>>
>>> # Normalised Form Decomposition
>>> nfd = unicodedata.normalize('NFD', text)
>>> print('\n'.join(unicodedata.name(c) for c in nfd))
LATIN SMALL LETTER C
COMBINING CARON
LATIN SMALL LETTER C
COMBINING CARON
```

### File names are text, too

*Problem:*
File names themselves can contain non-English characters.

*Bigger problem:*
The encoding of filenames depends on the filesystem the file saved on (which
could be different for each hard-drive, partition, or USB stick).  Things
*usually* work out, but you might encounter an old CD-ROM or USB stick, where
the filenames are scrambled.

TODO is there a general way to actually fix this problem

*Recommendations for robust file names:*

 * If you can at all help it, try to use ASCII characters only in your filenames
   (`a-z`, `A-Z`, `0-9`, `-`, `_`, and `.`).

 * Some file systems make a difference between capital and small letters, some
   don't, some do sometimes.  It's best to make sure file can be told apart
   regardless whether the system is case-sensitive or not.  For example, you
   should avoid having files like `File.txt` and `file.txt` in the same folder.

 * Spaces ` ` are *usually* not a problem these days, but it might not be a bad
   idea to separate words using `-`, `_`, or `.`, instead, e.g. `todo-list.txt`.
   It also makes your life easier when using the command-line.

These recommendations may seem a bit restrictive at first, but they do greatly
reduce the chance that something breaks in the long run.
