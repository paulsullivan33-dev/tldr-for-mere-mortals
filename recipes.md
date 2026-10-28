# Recipes

Short, complete jobs, each built only
from behaviour the earlier chapters
verified. The pattern in most of them:
tldr is rarely the whole job — it is the
ten seconds at the start that make the
rest of the job go right.

## Meet a tool you have just installed

You installed something new and know
nothing but its name:

```bash
tealdeer <tool>
```

Read the description line and the *More
information* link for what it is, then
work down the examples: they are ordered
roughly everyday-first, so the top three
are usually a safe apprenticeship. When
an example's flags puzzle you, that
example has done its teaching job — it
has told you which option to look up in
the man page (chapter 6's two-step).

## Remember a subcommand, not the tool

```bash
tealdeer git rebase
tealdeer docker compose
```

Ask for the subcommand page directly
rather than skimming the parent tool's
page hoping it mentions your case
(chapter 4). If the answer is "not
found", try the parent (`tealdeer git`)
and the list (`tealdeer --list | grep
'^git-'`) before concluding anything
(chapter 8's shapes of nothing).

## Work on the other system's rules

You are on Linux; the server, the
colleague, or the tutorial is on a Mac:

```bash
tealdeer --platform macos sed
```

Read the other platform's page before
running the command there — chapter 7's
sed pair shows how an everyday flag
(`-i`) changes its contract across the
border. The same trick checks a page for
a Windows tool (`--platform windows`)
before you sit down at that machine.

## Put a house rule where hands will meet it

Your household always lists an archive
before extracting it; your team always
dry-runs a sync before the real one.
Don't rely on memory — patch the page
(chapter 9):

```bash
tealdeer --edit-patch tar
```

and add the rule as an example in the
format of chapter 2. From then on, the
rule appears at the end of the page every
time anyone on that machine asks — the
cheat sheet itself carries the custom.

## Give your own scripts a memory

For each script you maintain, one page in
the custom pages folder (chapter 9),
named with `--edit-page` so the filename
is right:

```bash
tealdeer --edit-page photo-backup
```

Write the commands you actually run,
dry-run first. Review the page whenever
you change the script; the two files
drift apart exactly as fast as you let
them.

## Travel offline

Before a trip, a site visit, or any day
on someone else's network:

```bash
tealdeer --update
```

Everything after that works with the
network cable pulled — pages are local
files (chapter 2). The cache's size,
about 30 MB, is small enough that
"download the whole library" is a
reasonable thing to do on a laptop and a
phone-hotspot alike.

## Keep the answer

Pages are plain text when piped
(chapter 5), so they file away cleanly:

```bash
tealdeer rsync > ~/notes/rsync-cheatsheet.txt
tealdeer ffmpeg | grep -i 'extract'
```

The first keeps a page with your project
notes; the second asks the page a
question — *which example was the audio
one?* — with the ordinary text tools,
because a page is, in the end, ordinary
text.
