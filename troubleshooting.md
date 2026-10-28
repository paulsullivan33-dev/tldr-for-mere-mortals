# Troubleshooting

Every problem below happened in this
guide's lab, or follows directly from one
that did. They are ordered roughly by how
early in the tool's life they strike.

## "Page cache not found"

The client has no pages yet, or no longer
(chapters 3 and 8). Run
`tealdeer --update`. If the update itself
fails, that is the next entry. If the
update *succeeds* and the message
persists, check `tealdeer --show-paths`
against reality: a moved cache directory
(chapter 10's `[directories]`) or a home
folder the client resolves differently
than you expect are the usual stories.

## The update fails with a certificate error

The lab's first update (transcript
`t03-update.txt`) died like this:

```text
Could not download tldr pages from https://github.com/tldr-pages/tldr/releases/latest/download/tldr-pages.en.zip: Err(Io(Custom { kind: InvalidData, error: InvalidCertificate(UnknownIssuer) }))
```

`UnknownIssuer` means the machine that
answered is presenting a certificate the
client's trust store does not recognise.
On an ordinary home network this is rare.
On a network that inspects encrypted
traffic — many workplaces, some schools,
some security software on the machine
itself — a middlebox re-signs connections
with its own certificate, which your
operating system has been taught to trust
but the client's bundled trust store has
not. The client names the cure in its own
error text; set, in the config file's
`[updates]` section:

```toml
tls_backend = "rustls-with-native-roots"
```

so the download trusts the operating
system's roots instead, and update again
(transcript `t04-update-fixed.txt`). If
the error appears on a plain home
connection with no inspecting middlebox,
treat it with suspicion rather than
workarounds: something is re-signing your
traffic, and finding out what is the
actual task.

## "Page not found in cache" for a command that exists

Work the shapes from chapter 8 in order.
Is it every command, or one? Every
command is the entry above. One command:
check the spelling against
`tealdeer --list | grep` — the client
gives no suggestions (transcript `t11b`) —
then accept that the page may genuinely
not exist (transcript `t11`) and go to
the man page. If you asked with
`--language` or `--platform`, ask without
them: a working plain lookup with a
failing variant means the variant is not
in your cache (transcript `t14`).

## Your custom page is ignored

Ninety-nine times in a hundred, the
filename. Custom pages must end in
`.page.md`, patches in `.patch.md`; a
file named plain `tar.md` in the custom
folder is invisible (transcript `t15`).
Create files with `tealdeer --edit-page`
and `tealdeer --edit-patch` so the client
names them itself. If the name is right,
confirm the folder with `--show-paths`,
and remember the cache rule: with no
cache downloaded at all, even custom
pages refuse (chapter 8, shape one).

## The examples look wrong for your tool

Different flags, a missing subcommand,
behaviour that doesn't match the
sentence. Suspect vintage, in this order:
the page's (chapter 13 — check the man
page and `tool --help`, which describe
*your* binary), then the platform's
(a BSD-flavoured page on a GNU system, or
the reverse — chapter 7's `--platform`),
then your cache's age (update). Only
after all three should you suspect your
own typing; the tool's whole design means
its answers are someone else's snapshot.

## A stale-cache remark appears above a page

```text
The cache hasn't been updated for 40 days.
You should probably run `tldr --update` soon.
```

Not an error — the nudge from chapter 10,
shown when `auto_update` is off and the
cache passes its interval. Update, or set
`auto_update = true`, or raise
`auto_update_interval_hours`, according
to the choice chapter 10 lays out.

## Noise about a broken pipe

```text
Could not write to stdout

Caused by:
    0: Failed to print snippet
    1: Broken pipe (os error 32)
```

Piping a page into a command that stops
reading early — `tealdeer git checkout | head`
is the lab's example, at the end of
transcript `t10` — leaves this complaint
*after* the output, on the error stream.
The page arrived whole; nothing is
broken. Ignore it, or read the page into
a pager instead of decapitating it.

## Everything is old-fashioned or a feature is missing

Your client may be older than this guide.
Distribution packages lag the project by
years (chapter 3 met Ubuntu's 1.6.1
against the current 1.9.1), and the
personal-pages machinery — the `.page.md`
names, patches — is newer-client
behaviour. `tealdeer --version` tells you
which client your chapters describe;
the official binary from chapter 3 is the
short way to close the gap.
