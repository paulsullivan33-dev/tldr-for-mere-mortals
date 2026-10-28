# Your First Page

The install left you an engine with no
book. This chapter fetches the book —
once — and reads three pages from it, so
that by the end the everyday shape of the
tool is in your hands: update rarely,
ask often.

## The update

```bash
tealdeer --update
```

That is the whole ceremony. The client
downloads one compressed archive — the
pages, in the language your system is set
to — from the tldr-pages project's
release page, and unpacks it into the
cache folder from chapter 3. The lab's
successful run (transcript
`t04-update-fixed.txt`):

```text
$ tealdeer --update
Successfully updated cache.
Pages for the following languages were downloaded: en
```

Two details in those two lines reward a
second look. The download is of *pages*,
plural and complete: the entire English
collection, not the one page you are
about to ask for. And the language is
chosen for you, from your machine's
locale settings — an English system gets
`en`; chapter 7 looks at what that means
for other languages. The unpacked result,
measured by the lab (transcript
`t05-cache-anatomy.txt`), is about
30 MB of small text files: the 7,602
English pages counted in chapter 2, plus
the project's licence file. After this
moment the network is out of the loop.
Every page you render from now on is read
from your own disk, which is why answers
are instant and why the tool works
offline — and why the cache carries a
birthday and can go stale, the subject of
chapter 10.

One warning, earned by this guide's own
lab the hard way: the update can fail,
and its failure mode in the lab was a
certificate error that had nothing to do
with tldr itself. If your `--update`
stops with a TLS complaint instead of the
two lines above, do not debug the pages —
chapter 14 has that exact failure, its
cause, and its one-line fix.

## The first page

```bash
tealdeer tar
```

Check: the tar page from chapter 1
appears, all eight examples of it
(transcript `t06-tar-page.txt`). Notice
what is *not* in it: no list of tar's
sixty-odd options, no history of the
format, no tape drives. A description,
a link to the real manual, and the eight
things people do.

Two more pages, to calibrate your sense
of the collection's range. curl's page
(transcript `t07-curl-page.txt`) opens
with a *See also* line — the project's
pages point sideways at sibling tools
(`wcurl`, `wget`) as well as upward at
the manual — and its examples include
sending JSON and working through a proxy:
the page for a deep tool is still one
screen, but it is a denser screen. And
jq's page (transcript `t08-jq-page.txt`)
shows the format bending toward a tool
whose "commands" are little programs in a
language of their own; the examples are
still sentences with commands under them,
just with longer commands.

## Pages for subcommands

Many tools are really families: `git`
alone has well over a hundred
subcommands, and the interesting questions
are usually about one of them. tldr names
those pages with a dash — the page file
is `git-checkout.md` — and Tealdeer lets
you ask with a space instead:

```bash
tealdeer git checkout
```

Check (transcript
`t10-list-and-multiword.txt`): the
git-checkout page renders, about switching
branches and creating them, with nothing
about `git` in general. When you are
unsure whether a subcommand has its own
page, ask for it; the worst case is the
clear "not found" of chapter 8.

From here the tool is in its working
state, and most readers will type
`tealdeer <something>` a few times a week
and never think about chapters 2 and 3
again. The next chapter slows down over
one page and takes it apart — because the
placeholders in the examples have rules,
and knowing them is the difference between
copying a command and *reading* one.
