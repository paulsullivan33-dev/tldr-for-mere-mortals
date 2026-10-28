# Limits

What tldr cannot do, collected in one
place — most of these have already been
met in passing; here they are stated as
plainly as the tool's strengths were.

**Coverage is uneven, and the gaps are
not announced.** Seven and a half
thousand English pages sounds like
everything, until a real, installed,
man-paged command — `start-stop-daemon`,
chapter 8 — has none. The gaps follow
contributor interest, not importance, and
the only way to learn a tool has no page
is to ask and be refused. Popular,
modern, cross-platform tools are covered
richly; old system plumbing and niche
professional tools thinly.

**Pages can lag the tool.** A page
describes the tool as its author last
checked it. Tools rename flags, change
defaults and grow subcommands between
releases; the page follows when a
volunteer notices. The man page on your
machine cannot lag your machine — it
*is* your version's documentation — so
when the two disagree, believe the man
page and the tool's own `--help`
(chapters 6 and 12), and treat the
disagreement as the page asking for a
fix.

**Examples are not explanations.** A page
shows a flag doing a job; it does not
define the flag, warn about its edge
cases, or explain the concept underneath.
Some of those warnings matter: the tar
page will show you how to extract an
archive without once mentioning that a
hostile archive can write files outside
the folder you extract into — that sermon
lives in the manual and in this series'
tar guide, not in a cheat sheet. The
patch mechanism (chapter 9) exists
partly so your own hard-won warnings can
ride on the page; the underlying limit
stands.

**It answers names, not needs.**
Tealdeer looks pages up by exact command
name. It has no topical search, no
browsing by task, and — in this client —
no *did you mean* when the name is
wrong (chapter 8). If you cannot name
the tool, tldr cannot start.

**The first answer needs the network.**
A fresh client knows nothing until it
downloads its cache (chapter 3). On an
air-gapped machine, a new install is a
promise, not a tool, until someone
carries the archive to it. After that,
the dependence inverts — the man page
needs nothing and tldr needs nothing —
but the bootstrap is real.

**Languages trail.** Translations are
volunteer work layered on the English
collection; they are fewer, older, and
uneven across languages, and your cache
holds only the language you fetched
(chapter 7). A page missing in your
language may exist in English — and the
client's flat "not found" will not tell
you which kind of missing it was.

**One page, one depth.** The format caps
a page at a screenful of the common
cases. For tools whose *common* use is
itself deep — a query language, a build
system — the page is a phrasebook, useful
exactly as far as phrasebooks are, and
the real learning still waits in the
manual and in practice.
