# What tldr Is

Every command line tool keeps two kinds of
knowledge. One kind is *what the tool is
for* — what it does, when you would reach
for it. That kind sticks. The other kind
is *the exact spelling of the thing you
want*: which letters, in which order, with
the file name before the flag or after it.
That kind evaporates. You have extracted a
hundred tar archives, and the hundred and
first still makes you pause: was it `xvf`,
`xfz`, `xvfz`? Does the `z` go before the
`f`? The knowledge is in your machine,
documented completely — in the **man
page**, the built-in manual that Unix has
shipped since the 1970s. But a man page is
a *reference*: it lists every option,
including the ones for tape drives, in the
order the author thought of them. Finding
one everyday incantation inside it is
archaeology.

The name of this tool is the joke about
that experience, worn openly: **tldr**
stands for *too long; didn't read*.

**tldr is a collection of cheat-sheet
pages, one per command, written by a
community of volunteers, that keep only
the examples.** A tldr page for a tool
does not document the tool. It answers a
narrower, more useful question: *what do
people actually type?* For tar, the whole
page is eight examples — create an
archive, create a gzipped archive, extract
one, list one, extract only the files
matching a pattern. That is most of what
most people ever do with tar, and it fits
on one screen.

Here is the page exactly as this guide's
lab rendered it (transcript
`tldr-lab/transcripts/t06-tar-page.txt`):

```text
$ tealdeer tar

  Archiving utility.
  Often combined with a compression method, such as `gzip` or `bzip2`.
  More information: <https://www.gnu.org/software/tar/manual/tar.html>.

  [c]reate an archive and write it to a [f]ile:

      tar cf path/to/target.tar path/to/file1 path/to/file2 ...

  [c]reate a g[z]ipped archive and write it to a [f]ile:

      tar czf path/to/target.tar.gz path/to/file1 path/to/file2 ...

  E[x]tract a (compressed) archive [f]ile into the current directory [v]erbosely:

      tar xvf path/to/source.tar.ext
```

(Three of the eight examples shown; the
rest are in the transcript.) The shape
never changes: a one-line description, a
link to the real documentation, then
examples — each a plain sentence saying
what the command does, followed by the
command itself, with the parts you must
replace written as `path/to/...` stand-ins
instead of real file names. The bracketed
letters — `[c]reate`, `E[x]tract` — are a
mnemonic: they highlight the letter in the
description that ended up in the command.

## Why anyone would do this

- **Recall, not learning.** You already
  know what tar is. You need `xvf` versus
  `xvfz`, once, now. A page that is only
  examples respects that: there is nothing
  to read *through* to get to the answer.
- **The common cases are few.** For most
  tools, most people use a small fraction
  of the options, over and over. The
  project's contributors write down that
  fraction. Everything else still exists —
  in the man page, one command away
  (chapter 6 is about judging which one a
  question deserves).
- **It is the same everywhere.** The pages
  cover thousands of commands across
  Linux, macOS, Windows and more, all in
  the identical format, all fetched the
  same way. One habit replaces a thousand
  half-remembered ones.

## The project, briefly

The pages live in a public project called
**tldr-pages**. Anyone can propose a page
or a fix; volunteers review contributions
against a style guide that keeps pages
short, example-led and plain-spoken —
which is why a page for a tool you have
never used still feels familiar. The pages
are plain text files in a format called
**Markdown** (chapter 2 shows one), and
they are read by small programs called
**clients**. This guide uses **Tealdeer**,
a client written in Rust whose whole
personality is being fast and staying out
of the way; chapter 12 names others. The
client downloads the whole collection
once, as one archive, and afterwards works
entirely from that local copy — no network
is involved in answering you, which is why
answers arrive instantly and why the copy
can grow stale (chapter 10 covers both).

A first taste, after installing
(chapter 3) and updating (chapter 4):

```bash
tealdeer curl
```

Check: you get the curl page — a one-line
description, a *See also* pointing at
related tools, and examples beginning with
the plainest one there is, making a
request and printing the answer
(transcript `t07-curl-page.txt`).

## Who it is for

Anyone who works at a command line and
has ever typed a command, stared at it,
and deleted it to go and check. That is
everyone who works at a command line. It
is especially kind to the occasional user
— the person who administers a home server
on weekends and cannot be expected to keep
forty tools' flag spellings warm in
memory all week.

## What it is not

tldr is not documentation. It will not
explain what a tool's options *mean*, only
show them doing common jobs; when an
example combines four flags, the page does
not owe you four explanations (the man
page does — that is its job, and chapter 6
keeps the boundary honest). It is not
complete: chapter 8 meets real commands
that have no page at all. It is not
official: pages are community writing,
reviewed by volunteers rather than issued
by the tool's authors, and they can lag
behind a tool's newest release (chapter
13). And it is not a search engine: it
knows commands by name, and if you cannot
name the tool, it cannot guess it —
chapter 7 is about the finding it *can*
do.
