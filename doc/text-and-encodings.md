Text encoding and the Unicode standard
======================================
### What's between the lines?

*Question:*
If text is just a list of code points under the hood, how do I get this effect,
where a text file or text box splits things into multiple lines?

*Answer:*
In theory the solution is quite simple:
Just assign a specific code point that means ‘this is where one line ends and
another one begins’.

*Question:*
I'm afraid to ask but, *‘in theory’*?

*Answer:*
Well, in practice there are different traditions using different codepoints:

| Codepoint(s) | Name                                           | Escape sequence | Usage |
| ------------ | ---------------------------------------------- | --------------- | ----- |
| 10           | LF (*line feed*)                               | `\n`            | Unix and its derivatives (GNU/Linux, \*BSD, macOS, etc.) |
| 13           | CR (*carriage return*)                         | `\r`            | Commodore 64, old Apple OS's (like, pre-iPhone old) |
| 13, 10       | CRLF (*carriage return followed by line feed*) | `\r\n`          | MS DOS, Windows |

CR is pretty rare these days but LF and CRLF are widely used.

*Question:*
So, does CRLF mean that starting a new line requires two separate ‘characters’
in a row?

*Answer:*
Yes, this is precisely what it means.  CR and LF are separate codepoints and are
encoded separately, which means a CRLF newline takes up two bytes in UTF-8 (or
4 bytes in UTF-16).

```python
>>> list(ord(c) for c in '\r')
[13]
>>> list(ord(c) for c in '\n')
[10]
>>> list(ord(c) for c in '\r\n')
[13, 10]
```

I don't know if that's *exactly* how this came about but I like to imagine CRLF
like an old-timey typewriter:

 1. Carriage Return moves the page back horizontally until the little stamp that
    punches the letters onto the paper hovers over the beginning of the line

 2. Line Feed moves the roller so the page slides up one line.

*Note to [git][git] users:*
Git supports automatic conversion of newlines.  On Unix-like systems people
usually just checkout and commit newlines verbatim.  On Windows the installation
program asks about the desired behaviour.  It is recommended to go with the
option that says ‘checkout Windows-style, commit Unix-style line endings’.
With this all files in your local working copies contain Windows-friendly CRLF
newlines, while git uses LF newlines internally.

Git's newline behaviour can be configured via the `core.autocrlf` setting.  See
[GitHub's documentation][gh-newlines] for more details.

[git]: https://git-scm.com/
[gh-newlines]: https://docs.github.com/en/get-started/getting-started-with-git/configuring-git-to-handle-line-endings

### How does Python deal with newlines?

In most scenarios Python tries its best to just Do the Right Thing™.  It seems
to prefer LF newlines internally, but recognises all three newline schemes in
input data, referring them as [Universal Newlines][unl] collectively.  Some
methods like [`''.splitlines()`][splitlines] add support for some less common
newlines as well.

[unl]: https://docs.python.org/3/glossary.html#term-universal-newlines
[splitlines]: https://docs.python.org/3/library/stdtypes.html#str.splitlines

When Python reads from a file in text mode, Universal Newlines are converted to
LF.  Writing to a file in text mode will output the default newlines for the
operating system (CRLF on Windows, LF on Unix).  This behaviour can be changed
using [`open()`'s optional `newline` parameter][open-func].

[open-func]: https://docs.python.org/3/library/functions.html?highlight=newline#open

In binary mode `open()` loads the contents of the file verbatim into a `bytes()`
object, preserving any newline characters.

The `.decode()` and `.encode()` methods also leave newlines unchanged.  They
don't have an equivalent of the `newline` parameter from `open()`, so if you
need your data to use a specific newline character, you have to do the
conversion manually:

```python
>>> 'Line 1\nLine 2\r\nLine 3\rLine 4'.encode('utf-8')
b'Line 1\nLine 2\r\nLine 3\rLine 4'
>>> b'Line 1\nLine 2\r\nLine 3\rLine 4'.decode('utf-8')
'Line 1\nLine 2\r\nLine 3\rLine 4'
>>> 'Line 1\nLine 2\r\nLine 3\rLine 4'.replace('\r\n', '\n').replace('\r', '\n')
'Line 1\nLine 2\nLine 3\nLine 4'
```

### Converting between different encodings using `iconv`
### Unicode normalisation using `uconv`
[International Components for Unicode library (ICU)][icu].
 * On Debian/Ubuntu `uconv` is part of the [`icu-devtools`][icu-debian] package
 * On macOS you can get it from [homebrew][homebrew] by installing the
   [`icu4c`][icu-homebrew] package
[icu-homebrew]: https://formulae.brew.sh/formula/icu4c#default
[homebrew]: https://brew.sh/

The command syntax for `uconv` is as follows:

### Dealing with newline characters on the command-line

*Goal:*
You got a text file from someone who uses a different operating system and you
need to convert them to your newline scheme.

*Solution:*
The package [`dos2unix`][dos2unix(1)] provides a family of command-line programs
that convert between newline characters.  It is available in the standard
repositories for all major Linux distributions and [on homebrew][dos2unix-brew].
[The official website][dos2unix] also contains binaries for Windows.

[dos2unix]: https://waterlan.home.xs4all.nl/dos2unix.html
[dos2unix(1)]: https://waterlan.home.xs4all.nl/dos2unix/dos2unix.htm
[dos2unix-brew]: https://formulae.brew.sh/formula/dos2unix

`dos2unix` contains the following four programs:

| program    | conversion |
| ---------- | ---------- |
| `dos2unix` | CRLF → LF  |
| `unix2dos` | LF → CRLF  |
| `mac2unix` | CR → LF    |
| `unix2mac` | LF → CR    |

All of these programs take a number of file names as command-line arguments and
convert all of them *in place*:

```sh
dos2unix file-1.txt file-2.txt file-3.txt
```

If you do not want to destructively change files in place, you can use the `-n`
option to put `dos2unix` in *new file mode*:

```sh
dos2unix -n original-file.txt converted-file.txt
```

Also, running `dos2unix` without any file arguments will read data from standard
input and print the converted data to standard output:

```sh
$ printf 'abc\r\ndef' | wc -c
8
$ printf 'abc\r\ndef' | dos2unix | wc -c
7
```