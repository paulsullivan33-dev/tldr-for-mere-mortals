# The Moving Parts

tldr looks like one small program, but it
is three separate things wearing one name,
and most confusion about it is really
confusion about which of the three you are
looking at.

## The pages

The heart of the project is a folder full
of text files. Each file is one page,
written in **Markdown** — plain text with
light markup — and named after its
command: `tar.md`, `curl.md`,
`git-checkout.md`. Here is the top of the
real tar page, exactly as it sits in the
downloaded cache (transcript
`t09-tar-source.txt`):

```markdown
# tar

> Archiving utility.
> Often combined with a compression method, such as `gzip` or `bzip2`.
> More information: <https://www.gnu.org/software/tar/manual/tar.html>.

- [c]reate an archive and write it to a [f]ile:

`tar cf {{path/to/target.tar}} {{path/to/file1 path/to/file2 ...}}`
```

The format is a small contract, and every
page in the collection honours it:

- A title line: `#` and the command name.
- A description, quoted with `>`: what the
  tool is, in a line or two, usually ending
  with a *More information* link to the
  real documentation.
- A list of examples. Each is a sentence
  ending in a colon, then the command in
  backticks. Inside the command,
  `{{double braces}}` mark a
  **placeholder** — a part you replace
  with your own value. `{{path/to/file}}`
  means *your file here*, never a literal
  file called that.

The files are organised twice over. By
**platform**: a folder for Linux, one for
macOS, one for Windows, several more for
other systems, and a large folder called
**common** for pages whose commands work
the same everywhere. And by **language**:
the English collection is `pages.en`, and
other languages have parallel collections
translated by volunteers. The lab's cache
(transcript `t05-cache-anatomy.txt`)
holds the English set:

```text
$ ls ~/.cache/tealdeer/tldr-pages/pages.en/
LICENSE.md
android
cisco-ios
common
dos
freebsd
linux
netbsd
openbsd
osx
sunos
windows

$ ls ~/.cache/tealdeer/tldr-pages/pages.en/linux | wc -l
2070
$ ls ~/.cache/tealdeer/tldr-pages/pages.en/common | wc -l
4740
```

7,602 English pages in all at the time of
the lab's download, 4,740 of them common
and 2,070 Linux-specific. Your client
picks the common page when there is one,
and the platform page when the tool
differs by system — chapter 7 shows the
same command wearing two different pages
on two platforms.

## The clients

A **client** is the program you actually
run. Clients are independent of the pages:
the project publishes a client
specification, and anyone may write a
program that follows it. This guide's
client is **Tealdeer** (the command is
`tealdeer`, though its messages often just
say `tldr` — the name of the idea, not the
binary). A client's whole job is:

1. **Fetch** the pages, once, as a single
   compressed archive from the tldr-pages
   project's release page, and unpack them
   into a **cache** folder on your disk.
2. **Find** the page you named, in your
   language, preferring your platform.
3. **Render** it: turn the Markdown into
   the tidy terminal layout of chapter 1 —
   colours on a real terminal, plain text
   when piped — and print it.

Fetching is the only step that needs the
network. After that first download, every
lookup is local files and instant answers,
on a train, in a basement, wherever. The
price of that design is that your copy is
a snapshot: new and corrected pages exist
upstream the day they are merged, but you
see them only when you refresh the cache
(chapters 4 and 10).

## The layer that is yours

On top of the downloaded collection,
Tealdeer keeps a second, tiny folder that
is never touched by updates: your
**custom pages directory**. Two kinds of
file live there:

- **Custom pages** — whole pages you write
  yourself, for your own scripts and
  tools, in the same Markdown contract.
  A custom page with the same name as a
  community page *replaces* it outright
  (the lab proved both directions,
  transcript `t16b-override.txt`).
- **Patches** — small files that *add*
  examples to a community page without
  replacing it, so your house rules ride
  along on top of the shared page and
  survive cache updates (transcript
  `t16-patch.txt`).

Chapter 9 is devoted to both. The one
fact to carry forward is that this layer
exists, is yours, and follows one strict
file-naming rule that chapter 9's lab
learned the hard way.

## Who holds what

| Part | Held by | Changes when |
|---|---|---|
| The pages | The tldr-pages project, on GitHub | Volunteers merge fixes and new pages |
| The cache | Your machine, one folder | You run an update (or it updates itself, chapter 10) |
| The client | A program you installed | Its author releases a new version |
| Custom pages and patches | You, in a folder updates never touch | You edit them |

When something surprises you — a missing
page, a stale example, a page that looks
wrong — this table is the diagnosis in
advance: decide which part holds the thing
that surprised you, and you know where the
fix lives. Chapter 14 works through the
common cases.
