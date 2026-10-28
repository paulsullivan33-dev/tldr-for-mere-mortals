# Installing tldr

Installing tldr means installing a
**client** — the pages arrive by
themselves afterwards, in chapter 4. This
guide installs **Tealdeer**, the Rust
client, as a single downloaded program
file. There are other routes (a package
manager, building from source, a different
client entirely); they all end at the same
place: a `tealdeer` command, or in most
installations a command simply called
`tldr`, that answers when you type it.

## The single-binary install

Tealdeer is published as one static
program file per platform — no installer,
no dependencies, nothing else on your
machine touched. On a Linux machine with
an Intel-style processor, the whole
install is:

```bash
curl -LO https://github.com/tealdeer-rs/tealdeer/releases/download/v1.9.1/tealdeer-linux-x86_64-musl
curl -LO https://github.com/tealdeer-rs/tealdeer/releases/download/v1.9.1/tealdeer-linux-x86_64-musl.sha256
sha256sum -c tealdeer-linux-x86_64-musl.sha256
chmod +x tealdeer-linux-x86_64-musl
mkdir -p ~/.local/bin
mv tealdeer-linux-x86_64-musl ~/.local/bin/tealdeer
tealdeer --version
```

The middle step is not decoration. The
project publishes a **checksum** — a
fingerprint of the file — next to the
download; `sha256sum -c` recomputes the
fingerprint of what you actually received
and compares. The lab's download answered
`tealdeer-linux-x86_64-musl: OK`. If it
ever answers anything else, delete the
file and fetch it again: a program you are
about to trust should at least be the
program its authors published.

Check: the lab's version printout
(transcript `t01-first-run.txt`) reads:

```text
$ tealdeer --version
tealdeer 1.9.1
```

Two honest notes about versions. First,
the name of the download varies by
machine: there are builds for ARM
processors and for other operating
systems on the same release page — pick
the one that names yours. Second, version
numbers matter more than usual with this
tool. The lab also checked what its
distribution's package manager offered:

```text
$ apt-cache policy tealdeer
tealdeer:
  Installed: (none)
  Candidate: 1.6.1-4build2
```

Ubuntu's package is Tealdeer **1.6.1** —
same client, three years of development
behind. Most of this guide behaves
identically there, but the personal-pages
machinery of chapter 9 (the `.page.md`
file names, patches) is newer-client
behaviour, described for 1.9.1. If a
chapter ever disagrees with your client,
`tealdeer --version` is the first thing to
check, and the project's own documentation
matches versions to features. However you
install, the command may end up called
`tldr` rather than `tealdeer` — several
packages and the project's own docs use
the short name, and Tealdeer's messages
use it too. They are the same program for
everything in this guide.

## The first run refuses, politely

Ask a fresh install for any page and it
declines (transcript `t01-first-run.txt`):

```text
$ tealdeer tar
Page cache not found. Please run `tldr --update` to download the cache.

Note: You can optionally enable automatic cache updates by adding the
following config to your config file:

  [updates]
  auto_update = true

The path to your config file can be looked up with `tldr --show-paths`.
To create an initial config file, use `tldr --seed-config`.

You can find more tips and tricks in our docs:

  https://docs.tealdeer.org
```

This is the design of chapter 2 made
visible: the client ships with *no pages
at all*. Until it downloads the cache, it
is an engine with no book to read. The
refusal is worth reading once, because it
introduces the two helpers the rest of the
guide leans on:

- **`tealdeer --show-paths`** prints every
  file and folder the client uses. The
  lab's printout (transcript
  `t02-paths-and-seed.txt`) gives absolute
  paths under the lab's home folder;
  shortened to the part that is the same
  on every machine, the layout is:

```text
$ tealdeer --show-paths
Config dir:       ~/.config/tealdeer/
Config path:      ~/.config/tealdeer/config.toml
Cache dir:        ~/.cache/tealdeer
Pages dir:        ~/.cache/tealdeer/tldr-pages/
Custom pages dir: ~/.local/share/tealdeer/pages/
```

  A configuration file in
  `~/.config/tealdeer/`, the cache in
  `~/.cache/tealdeer/`, and your own pages
  in `~/.local/share/tealdeer/pages/`.
  Learn these three addresses and you can
  always find the moving parts again.

- **`tealdeer --seed-config`** writes a
  starter configuration file, fully
  populated with the default settings, for
  you to edit later. Chapter 10 reads it
  properly; for now it is enough to know
  the file exists and how it got there.

Run the seed config now, while the paths
are in front of you:

```bash
tealdeer --seed-config
```

Chapter 4 performs the update the first
run asked for, and reads the first page.
