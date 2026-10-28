# tldr and the Man Page

This is the judgement chapter, and it
starts with a fair fight: one ordinary
question, asked of both books.

**The question:** *I have a file called
`backup.tar.gz`. How do I get my files
back out of it?*

**The tldr answer** is on one screen
(transcript `t06-tar-page.txt`). The
fourth example says *Extract a (compressed)
archive file into the current directory
verbosely* and gives `tar xvf
path/to/source.tar.ext`; the fifth covers
extracting into a chosen directory. You
are done in seconds, and — just as
important — you can *see* the whole
remaining page at the same time, so you
also absorb, for free, that listing an
archive before extracting it is a normal
thing people do (example seven), a habit
chapter 9 will put to work.

**The man answer** is complete in a way
the page never tries to be. It is also
1,164 lines long. The lab measured it
directly (transcript `t06b-man-hunt.txt`).
Two honest disclosures about that number:
the lab's machine had no `man` program
installed, so the lab rendered the very
same Ubuntu tar(1) page with groff — the
formatter the `man` command itself drives
— and counted the rendering; on your
machine the command is simply `man tar |
wc -l` and the count will be in the same
neighbourhood, varying a little with
terminal width and tar version. And the
second disclosure is the finding itself:
grep the whole 1,164 lines for worked
examples and the single hit is the page's
own NOTE near the top, which reads, in
part:

```text
NOTE
       This manpage is a short description of GNU tar.  For a detailed discus-
       sion, including examples and usage recommendations, refer to the GNU
       Tar Manual available in texinfo format.
```

The tar man page is a fine reference that
contains, by its own cheerful admission,
*no examples to speak of* — for those it
sends you to a third book. Our question is
answered inside it, of course: the `-x`
option is documented at line 185, the
compression flags around line 717, and a
patient reader can assemble `tar xvf`
from the parts. But assembly is the work
the tldr page exists to do for you.

## What each book is for

| | tldr page | man page |
|---|---|---|
| Shape | The common examples, one screen | Every option, alphabetical, 1,164 lines for tar |
| Best question | "What do people type to...?" | "What exactly does this option do?" |
| Source | Community volunteers | The tool's own authors |
| Version | Describes the tool as the page's authors knew it | Matches the tool installed on *your* machine |
| Availability | After one download; then offline | Already on the machine, always |
| Failure shape | Missing entirely for some tools (chapter 8) | Present but silent about examples |

That version row deserves emphasis,
because it is the man page's strongest
card and the one people forget: the man
page on your machine documents *the tar
you have*. The tldr page documents the
tar its author had. Usually those agree.
When a tool changes its flags — as tools
occasionally do — the man page is the one
that cannot be wrong about your copy, and
a tldr example that fails is a sign to
check the man page before blaming your
typing (chapter 14 returns to this).

## A working rule

Reach for tldr **first** when you know
the tool and roughly the job, and need
the spelling. It answers in seconds, and
its *More information* link points at the
manual for when it isn't enough. Walk to
the man page when:

- the job is not among the page's handful
  of examples — the page's silence about
  a job means *uncommon*, not
  *impossible*;
- an example failed, or behaved
  differently than its sentence promised;
- you need to know what an option *means*
  rather than watch it used — meanings,
  edge cases and warnings are the man
  page's whole trade;
- the stakes are high. A command that
  deletes, overwrites or rewrites deserves
  a reading of its actual documentation,
  not a stranger's summary of it.

Neither book is the other's enemy. The
tldr project itself treats the man page
as the authority — every page links to
it — and the healthiest habit this guide
can leave you with is a two-step one:
*tldr to remember, man to be sure.*
