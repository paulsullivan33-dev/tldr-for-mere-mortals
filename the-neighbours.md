# The Neighbours

tldr sits in a crowded neighbourhood of
ways to answer *how do I drive this
tool?* This chapter places the neighbours
honestly — including the one that was
there first and still owns the house.

## The man page

The original, the authority, and — since
chapter 6 gave it a chapter of its own —
only summarised here: complete,
version-matched to your installed tool,
always present, and organised for lookup
rather than for the question you actually
have. tldr does not compete with it; every
tldr page links to the manual in its
second breath. The working relationship
is *tldr to remember, man to be sure*.

## The tool's own --help

Nearly every command answers `--help`
(or `-h`) with a summary it wrote about
itself. That text is version-exact like
the man page — it ships inside the binary
— and it is the fastest check when a tldr
example fails: if the flag spelling in
`tool --help` differs from the page, the
page is describing a different vintage of
the tool, and the binary in front of you
wins. Help text is terse to a fault and
rarely shows a complete worked command,
which is precisely the gap tldr fills;
the two are complements, not rivals.

## The tldr website

The same project publishes its pages on
the web (tldr.sh) — the same Markdown,
rendered in a browser, searchable by
humans in a way the client is not
(chapter 7). It is the right door when
you are not at a terminal, or when you
want to check whether a page exists
upstream before blaming your cache. It
needs the network, which the client,
after one update, does not.

## Other clients

Tealdeer is one reader of the pages among
many, all reading the same collection to
a shared client specification — the tldr
project's own page for itself (transcript
`t19-tldr-page.txt`) is mostly a tour of
that interface. There are clients in
Node.js (the original `tldr` package,
whose name most installations borrow),
in Python, in Go, and inside editors and
chat tools. They differ in speed, in
extras — this guide's client is unusually
fast and has the custom-page and patch
machinery of chapter 9 — and in how
current their behaviour is. What they
share matters more: swap clients and your
cache, your habits and this guide's
chapters 1, 2 and 5–8 all still apply.

## The cheat-sheet cousins

Tools that answer the same itch from
different directions, named on the tldr
page's own *See also* line (transcript
`t19`), and characterised here rather
than run — the lab did not exercise them,
and this guide does not pretend
otherwise:

- **cheat** and its web cousin **cheat.sh**
  keep community cheat sheets too, but
  organised around *your own* editable
  sheets first, and cheat.sh answers from
  a server, so it works with nothing
  installed and nothing cached — at the
  price of needing the network for every
  question.
- **navi** takes a set of cheat sheets —
  including ones in tldr's extended
  family — and makes them *interactive*:
  fuzzy-search the sheet, fill in the
  variables by choosing values, and the
  finished command is assembled and
  offered to your shell. Where tldr is a
  page you read, navi is a form you
  complete; people who run long,
  variable-heavy commands from sheets
  often graduate to it.

The differences are of posture, not of
worth: tldr's bet is that a static page,
read at a glance and gone, matches how
the question actually occurs — mid-task,
one hand on the keyboard, the other
holding the rest of the command in your
head.
