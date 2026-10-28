# Configuration

Tealdeer works with no configuration at
all — everything before this chapter ran
on defaults plus one rescue setting. But
it has a config file, and a handful of
its settings change the tool's daily
feel. This chapter reads the file the
lab seeded in chapter 3 and changes the
settings that matter, proving each change
on a rendered page.

## The file

`tealdeer --seed-config` (chapter 3)
writes `~/.config/tealdeer/config.toml`
— 48 lines in the lab's copy, every
setting present at its default value,
grouped under bracketed headings like
`[display]` and `[updates]`. The format
is **TOML**, a plain config-file format:
`name = value` lines, `#` for comments.
You edit it with any text editor; there
is no settings screen and nothing to
restart — the next command you run reads
the file afresh. Two flags bend the
rules for a single run: `--config-path`
reads a different file entirely, and
`--override-config 'display.compact = true'`
overrides one setting on the command
line, which is the tidy way to test a
change before committing to it.

## Display: how a page is laid out

The `[display]` section holds the
rendering choices. Two of them, changed
together in the lab (transcript
`t17-config-display.txt`), show the
range:

```toml
[display]
compact = true
show_title = true
```

- **`compact`** removes the blank lines
  between examples. The same page, before
  and after, is the difference between a
  airy reference card and a dense one —
  purely taste, and the dense form fits
  more of a long page on one screen.
- **`show_title`** prints the command's
  name at the top of the render. It is
  off by default (you just typed the
  name, after all) and useful when pages
  are piped into files or shown to
  someone who didn't type the command.

Also in this section: **`use_pager`**
sends long pages through a pager like
`less` automatically (the `--pager` flag
does it for one run), and
**`placeholder_format`**, the default you
met in chapter 5 — `"long"` renders
placeholders like `{{[-C|--directory]}}`
as `--directory`, `"short"` as `-C`.

The **`[style]`** sections set the colour
and emphasis of each element of a page —
description, command name, example text,
example code, placeholder — when output
goes to a real terminal. The seeded file
lists them all (the description is plain,
command names cyan, example code cyan,
placeholders cyan and underlined, in the
defaults). The lab's transcripts are
piped text and show no colour, so this
guide describes the mechanism rather than
demonstrating shades; on your own
terminal, `--color never` and
`--color always` show the two extremes
the styles interpolate between.

## Updates: keeping the book current

The `[updates]` section governs the
cache's birthday problem from chapter 4:

```toml
[updates]
auto_update = false
auto_update_interval_hours = 720
```

With **`auto_update`** on, the client
quietly refreshes the cache in the
background once it is older than
**`auto_update_interval_hours`** — 720
hours, thirty days, by default. With it
off (the default, and the lab's setting),
an old cache instead *nudges* you, once,
in the output itself. The lab aged its
cache by forty days on purpose and asked
for a page (transcript
`t18-stale-cache.txt`):

```text
$ tealdeer jq | head -4
The cache hasn't been updated for 40 days.
You should probably run `tldr --update` soon.

  jq
```

The page still renders; the nudge is a
preface, not a refusal. Whether you
automate the refresh or take the nudge is
a genuine choice: automatic keeps
examples freshest for tools that change,
while manual keeps a known-good snapshot
on machines where consistency matters
more — a household fleet, say, where you
would rather everyone's cheat sheets
agreed until you decide otherwise.

The section also holds **`archive_source`**
— where the archive comes from — and
**`tls_backend`**, which chooses which
certificate roots the download trusts.
That second one is the setting that
rescued this guide's lab: `rustls-with-webpki-roots`
trusts a bundled set of public roots,
`rustls-with-native-roots` trusts the
operating system's own store, and on
networks whose traffic passes through a
certificate-inspecting proxy, only the
second works. Chapter 14 tells that story
in full; the lesson to keep is that the
knob exists and lives here.

## Directories: moving the parts

The `[directories]` section can relocate
the cache and the custom pages folder —
useful on multi-user machines or when a
home folder is not where your dotfiles
live. Leave it empty (the seed does) and
the client uses the operating system's
conventions from chapter 3. If you do
move things, `tealdeer --show-paths`
afterwards is the check that the client
agrees with your intention.
