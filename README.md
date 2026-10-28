# tldr for Mere Mortals

You know the tool exists. You have used it
before, possibly often. What you cannot
remember is the exact combination of
letters that makes it do the one thing you
want: *extract this archive*, *download
with the headers shown*, *print just the
names out of this JSON*. The manual knows,
but the manual is a reference work — it
documents every option the tool has ever
had, in alphabetical order, whether or not
any living person uses them. **tldr** is
the opposite shape of answer. It is a
collection of short, community-written
**pages**, one per command, each holding
only the handful of examples people
actually run, written in plain words with
the parts you must fill in marked clearly.

This guide explains how those pages work,
how a **client** program — this guide uses
**Tealdeer**, a fast one written in Rust —
fetches them onto your machine and renders
them in your terminal, and how the two of
them divide the work with the man page,
which is not replaced but relieved of a
job it was never good at. It also shows
you writing pages of your own: for the
scripts only your household runs, and as
small **patches** that add your own rules
to a community page.

The lab behind this guide ran the real
thing: **Tealdeer 1.9.1**, the official
static binary, checksummed against the
project's published SHA-256, on a small
Linux machine with a deliberately empty
home folder, so the first-run behaviour a
new user meets is exactly what the
transcripts show. Against it the lab
downloaded the real page cache — 7,602
English pages, about 30 MB unpacked —
rendered pages for everyday tools,
compared one question against the man page
for the same tool, hunted for pages that
do not exist, wrote a personal page and a
patch and watched both take effect, and
changed the configuration and watched the
rendering change. The lab also broke
things in instructive ways, including an
update that failed over a certificate
before it succeeded, and a personal page
that sat ignored until its file was given
the name the client actually looks for.

What the lab could not do, it did not
fake. Its machine had no man-db installed,
so the man page in the comparison chapter
was rendered with groff — the same
formatter the `man` command itself uses —
and the chapter says so where it matters.
Colour output is described rather than
shown, because a transcript file is not a
terminal and the client turns colour off
when its output is piped. Other tldr
clients are named and characterised, not
run. `criteria.md` keeps the full ledger
of what was run and what was only read.

## What this guide covers

- [**What tldr is**](what-tldr-is.md) —
  the gap between knowing a tool and
  remembering its incantations, and the
  community project that fills it
- [**The moving parts**](the-moving-parts.md) —
  the pages, the clients, the cache, and
  which part holds what
- [**Installing tldr**](installing-tldr.md) —
  the Tealdeer binary, checksums, version
  numbers that matter, and the first run
  that refuses until you feed it
- [**Your first page**](your-first-page.md) —
  the cache update, what it downloads,
  and reading your first rendered page
- [**Reading a page**](reading-a-page.md) —
  the anatomy of a page: the description,
  the examples, and the `{{placeholders}}`
  you replace with your own values
- [**tldr and the man page**](tldr-and-the-man-page.md) —
  one question asked of both, side by
  side, and the honest division of labour
  between them
- [**Finding pages**](finding-pages.md) —
  the list of everything, subcommand
  pages, platform variants for other
  operating systems, and languages
- [**When there is no page**](when-there-is-no-page.md) —
  the three shapes of nothing, and where
  to go for each: the man page, the help
  text, and writing the page yourself
- [**Your own pages**](your-own-pages.md) —
  personal pages for your own scripts,
  patches that extend a community page,
  and the file-name trap that hides both
- [**Configuration**](configuration.md) —
  the config file: compact rendering,
  titles, automatic updates, colours, and
  the setting that rescued this guide's
  own lab
- [**Recipes**](recipes.md) — meeting a
  new tool, house rules as patches,
  offline travel, and pages for the
  scripts only you run
- [**The neighbours**](the-neighbours.md) —
  the man page, `--help`, the tldr website,
  other clients, and the cheat-sheet tools
  that solve nearby problems
- [**Limits**](limits.md) — uneven
  coverage, version drift, examples
  without explanations, and the rest,
  stated plainly
- [**Troubleshooting**](troubleshooting.md) —
  the empty cache, the certificate that
  stopped an update, the page that was
  there but named wrong, and the other
  traps this guide's lab fell into
- [**Glossary**](glossary.md) — the
  terms, collected in one place

## What it doesn't cover

tldr is a reminder, not a teacher: this
guide does not try to teach the tools the
pages describe. tar, curl and jq appear as
worked examples because their pages are
good specimens, and each has manuals —
and, for some, whole guides in this series
— of its own. Writing pages good enough to
contribute back to the project is shown up
to the file on your disk; the project's
review process on GitHub is pointed at,
not walked through. And no chapter will
help you memorise anything: the entire
point of the tool is that you should not
have to.

## How to use this guide

Read chapter 1 for the idea and chapter 2
before installing anything — knowing which
part holds what turns later confusion into
a named problem. Chapter 4 fetches the
cache and reads a first page in the same
sitting as the install; do that much and
the tool is already paying rent. Chapter 6
is the judgement chapter: when to trust the
short page and when to walk to the manual.
Chapter 9 is the one that turns a reader
into an author — write the page for one of
your own scripts while the format is small
enough to check by eye. The lab's
transcripts live in `tldr-lab/transcripts/`;
its personal page and patch are
`tldr-lab/pages/`; its notes are in
`criteria.md`.

---

## Part of the series

This guide is one of the [For Mere Mortals](https://paulsullivan33-dev.github.io/mere-mortals/) guides: plain-language guides to the tools programmers and makers use.

Related guides:

- [Linux for Mere Mortals](https://paulsullivan33-dev.github.io/linux-for-mere-mortals/)
- [Bash for Mere Mortals](https://paulsullivan33-dev.github.io/bash-for-mere-mortals/)
- [Text Processing for Mere Mortals](https://paulsullivan33-dev.github.io/text-processing-for-mere-mortals/)

## License

The writing in this guide is licensed under [CC BY 4.0](https://github.com/paulsullivan33-dev/tldr-for-mere-mortals/blob/main/LICENSE). Code examples and lab scripts are licensed under the [MIT License](https://github.com/paulsullivan33-dev/tldr-for-mere-mortals/blob/main/LICENSE-CODE).
