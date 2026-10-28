# Finding Pages

Asking works when you know the name. This
chapter is about the three finding jobs
that remain: seeing what exists in bulk,
asking for a tool as it behaves on a
*different* system than your own, and
asking in another language.

## The whole shelf at once

```bash
tealdeer --list
```

prints every page name the client can
currently serve, one per line. The lab's
count (transcript
`t10-list-and-multiword.txt`):

```text
$ tealdeer --list | wc -l
7391
```

That is fewer than the 7,602 English
files in the cache, and the difference is
the lesson: the list shows *your view* of
the collection — the common pages plus
your platform's pages (Linux here), not
the folders for systems you are not
running. A bare list of 7,391 names is
not reading material; its real use is
with a search tool behind it, asking
whether something exists and what it is
called:

```text
$ tealdeer --list | grep -E "^git-(checkout|switch|restore)$"
git-checkout
git-restore
git-switch
```

That one pipeline answers a genuinely
common question — *git has three commands
that all sound like "undo my checkout";
which does tldr cover, and under what
exact names?* — and the same trick finds
families (`--list | grep '^docker-'`),
checks a spelling, or confirms a page
exists before you rely on it in a script
of your own.

What the list cannot do is find a page by
what it *does*. Tealdeer has no
search-the-examples mode and — as the
next chapter shows in transcript `t11b` —
no helpful suggestions when a name is
wrong: a typo earns the same flat
"not found" as an invented command. If
you know what a job is but not which tool
does it, the list will not save you; that
is a question for the web, a colleague,
or this series' topical guides. tldr
begins where the name is known.

## The same command on another system

Pages differ by platform because commands
do. The classic case is `sed`: the GNU
sed on a Linux machine and the BSD sed on
a Mac accept the same scripts but spell
everyday flags differently. Your client
normally serves your own platform's page;
`--platform` asks for another's
(transcript `t12-platform.txt`):

```text
$ tealdeer --platform macos sed | sed -n "1,14p"

  Edit text in a scriptable manner.
  See also: `awk`, `ed`.
  More information: <https://keith.github.io/xcode-man-pages/sed.1.html>.
```

Different description, different manual
link, different examples — and, down the
page, the famous difference in the flesh:
where the Linux page edits in place with
`sed --in-place`, the macOS page's source
spells it `sed -i bak ...`, because BSD
sed insists on being told what backup
suffix to use. If you administer a Mac
from a Linux desk, write scripts that
must run on both, or are following
instructions written for the other system,
one flag translates the cheat sheet.
Several `--platform` values may be given,
in order of preference, and `common` is
always effectively in the running — it is
where most pages live.

## Other languages

The collection is translated, page by
page, by volunteers — and the cache you
downloaded holds only the language your
system asked for (chapter 4's update
named it: `en`). Asking for another
language makes the boundary visible
(transcript `t14-language.txt`):

```text
$ tealdeer --language de tar
Page `tar` not found in cache.
Try updating with `tldr --update`, or submit a pull request to:
https://github.com/tldr-pages/tldr
exit code: 1
```

German pages exist upstream; they are
simply not in this cache, and the client
reports that the same way it reports a
missing page (chapter 8 collects the
shapes of "nothing" and how to tell them
apart). To change the language you read
in, set the system's locale or the
`--language` default through the
configuration and update again, so the
matching archive is fetched. Coverage in
translation is uneven — it trails the
English collection, and a page missing in
your language is a gap in the translation
project, not in the tool.
