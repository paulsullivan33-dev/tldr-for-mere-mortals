# Reading a Page

A tldr page is short enough to take in at
a glance, and that is the point — but it
is written in a small notation, and ten
minutes spent learning the notation pays
back on every page you will ever read.
This chapter takes the notation apart,
using the tar page (transcript
`t06-tar-page.txt`) as the specimen.

## The three bands

Every rendered page has the same three
bands, top to bottom:

1. **The description.** A line or two in
   plain words: *Archiving utility. Often
   combined with a compression method,
   such as gzip or bzip2.* Sometimes a
   *See also* line naming sibling tools,
   and almost always a **More information**
   link — the page telling you, upfront,
   where the real documentation lives.
   That link is the page's honesty about
   its own size: everything not here is
   through that door.
2. **The examples.** The whole payload:
   usually between five and eight of them
   (the lab's three specimen pages hold
   eight, eight and eight), ordered
   roughly from the everyday toward the
   specialised.
3. Nothing else. There is no third band.
   When a page feels thin, it is not
   hiding a continuation — the rest of
   the knowledge is in the manual, and
   chapter 6 is about when to go there.

## An example, read closely

Each example is two parts. First a
sentence, written to be *scanned*: the
bracketed letters are woven into it —
*[c]reate an archive and write it to a
[f]ile* — so that after reading, the
letters in the command below are not
arbitrary. Then the command itself:

```text
  [c]reate an archive and write it to a [f]ile:

      tar cf path/to/target.tar path/to/file1 path/to/file2 ...
```

The command is a *pattern*, not a line to
paste blind. Where your real values go,
the pattern shows a stand-in:
`path/to/target.tar` means *the path of
the archive you are making*. In the page's
source file those stand-ins are wrapped in
`{{double braces}}` and called
**placeholders** (you saw them in chapter
2's raw page). On a terminal, Tealdeer
underlines them; in plain text they print
as ordinary words, and the convention is
that anything shaped like a path, a name
or a value in an example is yours to
replace. The trailing `...` in
`path/to/file1 path/to/file2 ...` means
*and the rest of them, likewise* — tar
takes any number of files; the pattern
shows two and waves at the remainder.

## Placeholders that offer a choice

Some placeholders hold two spellings of
the same thing. In the tar source, one
example's command contains
`{{[-C|--directory]}}` — *either* the
short flag `-C` *or* the long one
`--directory`; they do the same job.
Tealdeer must pick one when it renders,
and its default (set in the configuration,
chapter 10) is the long form, which is
why the lab's tar page reads
`tar czf ... --directory path/to/directory`.
Ask for the other rendering and the same
page changes its mind (transcript
`t13-raw-and-options.txt`):

```text
$ tealdeer --short-options tar | grep -A1 "directory"
  [c]reate a g[z]ipped (compressed) archive from a directory using relative paths:

      tar czf path/to/target.tar.gz -C path/to/directory .
```

`--long-options` flips it back. Neither
rendering is more correct; pick the one
that matches how you think — many people
read long flags while learning a tool and
short ones once their fingers know them.

## Seeing the source, and rendering files

Two flags lift the curtain on chapter 2's
claim that a page is just a text file:

```bash
tealdeer --raw tar
```

prints the page's Markdown exactly as it
sits in the cache, placeholders, braces
and all (transcript `t13-raw-and-options.txt`).
And

```bash
tealdeer --render some-file.md
```

renders *any* file in the page format —
which is how you will preview pages of
your own in chapter 9 before filing them.

## What the rendering quietly does

On a real terminal the output is coloured
by element — command names, example text,
commands and placeholders each get their
own treatment, configurable in chapter
10. When the output is piped into a file
or another program, Tealdeer drops the
colour and prints clean text, which is
why every transcript in this guide is
plain, and why pages compose well with
the rest of the command line: `tealdeer jq`
into a pager, a file, or a search is just
text. One wart, recorded honestly because
the lab's transcripts stepped on it:
piping a page into a command that stops
reading early, like `head`, can leave a
`Could not write to stdout ... Broken pipe`
complaint on the terminal afterwards
(visible at the end of transcript `t10`).
The page itself arrived intact; the noise
is the client objecting to being cut off,
and chapter 14 lists it so you recognise
it rather than debug it.
