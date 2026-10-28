# When There Is No Page

Sooner or later you will ask for a page
and get nothing. The nothing comes in
three shapes, and they have different
causes and different cures — telling them
apart is the whole skill of this chapter.

## Shape one: no book at all

```text
Page cache not found. Please run `tldr --update` to download the cache.
```

You met this in chapter 3, on a fresh
install, and it returns if the cache is
deleted (`tealdeer --clear-cache` brings
it back on demand — transcript `t20`).
The client cannot serve *anything* in
this state — the lab verified that even
your own custom pages from chapter 9
refuse while the cache is absent. The
cure is the one the message names: an
update, and chapter 14 if the update
itself fails.

## Shape two: the tool is real, the page is not

The collection is large, not complete,
and its gaps are not where you would
predict. The lab probed its own machine's
commands: `unshare`, `ldconfig`,
`dpkg-query`, `lsblk`, `flock` — all have
pages. And then (transcript
`t11-no-page.txt`):

```text
$ tealdeer start-stop-daemon
Page `start-stop-daemon` not found in cache.
Try updating with `tldr --update`, or submit a pull request to:
https://github.com/tldr-pages/tldr
exit code: 1
```

`start-stop-daemon` is a real command,
installed on the lab machine at
`/usr/sbin/start-stop-daemon`, used by
service scripts across Debian and Ubuntu.
Two of its neighbours from the same
probe, `run-parts` and `savelog`, are
missing too — while far more obscure
tools have polished pages. Coverage
follows contributors' interests, and the
plumbing of service management has had
fewer interested contributors than the
shiny parts of the command line. The
client's exit code is 1, so scripts can
tell the difference between an answer and
this.

The cure for shape two is the old book:
this command has a perfectly good man
page — the lab rendered it at 308 lines —
and `man start-stop-daemon`, plus the
tool's own `--help`, are where its
knowledge lives. This is chapter 6's
division of labour working as designed:
tldr is the first stop, never the only
one.

Two smaller observations from the same
transcript file's companion (`t11b`).
An invented command and a mere typo —

```text
$ tealdeer gti    (a typo for git)
Page `gti` not found in cache.
```

— get exactly the same message as the
real-but-uncovered tool. Tealdeer 1.9.1
offers **no suggestions**: it will not
whisper *did you mean git?* If the name
might be spelled differently, chapter 7's
`--list | grep` is the finding tool you
have. And a curiosity in the other
direction: the lab's client happily
served a page for `mkdocs`, a tool that
is *not installed* on the lab machine.
Pages describe commands, not your
installation of them; a page is not a
promise the tool is present.

## Shape three: the variant is missing

A page can exist and still be out of
reach because the *variant* you asked
for is not in your cache: another
language (chapter 7's German tar), or a
page that exists only for a different
platform. The message is the same flat
"not found in cache", so the diagnosis is
yours to make: if plain `tealdeer tar`
works, your cache is fine, and the gap is
in the variant — fetch the right language
with an update, or check the platform
spelling against `--show-paths` and the
platform list in `--help`.

## The message's own suggestion

Every not-found ends with the same
invitation: *submit a pull request to
github.com/tldr-pages/tldr*. That is not
boilerplate. The collection is exactly
the sum of people who met a gap and
filled it, and a page is a small file in
the format of chapter 2 — the next
chapter teaches you to write one for
yourself, and a page written for yourself
is most of the way to a page contributed
to everyone.
