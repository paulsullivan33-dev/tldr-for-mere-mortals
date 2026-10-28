# Your Own Pages

The community collection cannot know about
the script you wrote last spring — the one
that backs up the photo card, rebuilds the
media library, or restarts the household
services in the right order. Six months
later, *you* are the person staring at it
wondering which flag was the dry run.
This chapter closes that loop: the client
reserves a folder for pages of your own,
in the same format, rendered the same way.
It also covers **patches**, the smaller
move: adding your own examples to a
community page without replacing it.

## The folder, and the trap in it

Your pages live in the **custom pages
directory** — `tealdeer --show-paths`
names yours; the standard address is
`~/.local/share/tealdeer/pages/`. Nothing
else about it is standard, starting with
the trap this guide's lab fell into
head-first, and which is now the fastest
way to learn the rule (transcript
`t15-custom-page.txt`).

The lab wrote a page for an invented but
representative household script,
`photo-backup`, saved it as
`photo-backup.md` — the name every
community page uses — and asked for it:

```text
$ tealdeer photo-backup    (file named photo-backup.md)
Page `photo-backup` not found in cache.
exit code: 1
```

Silence. No error about the file, no hint
it was seen and rejected — the client
simply never looked at it, because in
Tealdeer 1.9.1 a custom page's file must
be named **`<command>.page.md`**. One
rename later:

```text
$ mv ~/.local/share/tealdeer/pages/photo-backup.md ~/.local/share/tealdeer/pages/photo-backup.page.md

$ tealdeer photo-backup    (file named photo-backup.page.md)

  photo-backup
  Copy new photos from a camera card to the backup drive, sorted into dated folders.
  More information: <https://example.com/photo-backup>.
  Copy all new photos from a card to the backup drive:
      photo-backup --source path/to/card --dest path/to/backup_drive
```

(The tighter spacing is chapter 10's
configuration at work in the lab by then.)
The reliable way to get the name right
without memorising it is to let the
client start the file for you:
`tealdeer --edit-page photo-backup` opens
`photo-backup.page.md` in your editor,
already named correctly. The lab found
the suffix by exactly that route, after
the silent failure above.

## Writing the page

A page is the contract from chapter 2,
and a personal page needs no more than
the tar page's skeleton. The lab's file
(kept in the repository at
`tldr-lab/pages/photo-backup.page.md`):

```markdown
# photo-backup

> Copy new photos from a camera card to the backup drive, sorted into dated folders.
> More information: <https://example.com/photo-backup>.

- Copy all new photos from a card to the backup drive:

`photo-backup --source {{path/to/card}} --dest {{path/to/backup_drive}}`

- Show what would be copied, without copying anything:

`photo-backup --dry-run`

- Check the copies against the originals by checksum:

`photo-backup --verify`
```

Three habits make a personal page earn
its keep. Write the examples as the
*commands you actually run*, including
the dull flags you always add — a page
that only shows the interesting options
will betray you at the boring step. Keep
the dry-run and verification examples
prominent if the tool has them; future
you, tired, will thank present you. And
update the page the day the script
changes, while the change is in your
head: a stale personal page is worse than
none, because you will trust it.

## Patches: your rules on their page

Replacing a community page to add one
example is wasteful — you would inherit
the job of tracking upstream fixes. A
**patch** is the lighter mechanism: a
file named `<command>.patch.md` in the
same folder, containing extra examples
that the client appends to the community
page at render time. The lab's patch for
tar encodes a house rule (kept at
`tldr-lab/pages/tar.patch.md`):

```markdown
# tar

- In this house we always list an archive before extracting it:

`tar tvf {{path/to/source.tar}}`
```

With it in place, the community page
grows a ninth example, at the end
(transcript `t16-patch.txt`):

```text
$ tealdeer tar | tail -6   (with a personal patch in place)

  In this house we always list an archive before extracting it:

      tar tvf path/to/source.tar
```

Patches survive cache updates, because
the folder is never touched by them —
your rules ride on top of whichever
version of the page is current.
`tealdeer --edit-patch tar` opens the
right filename in your editor, as with
pages. The lab also verified the
precedence rules between the three
layers (transcripts `t16b-override.txt`
and `t16c-override-vs-patch.txt`):
a custom page named `tar.page.md`
*replaces* the community tar page
entirely — the patch is not appended to
it either; delete the
custom page and the community page —
with your patch still appended — returns.
So the layers, strongest first: your
page, then your patch on their page, then
their page.

That ordering is the chapter in one
paragraph: patches for opinions about
shared tools, pages for tools that are
yours alone, and the community collection
underneath both, updating quietly.
