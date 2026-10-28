# Glossary

**cache** — the client's local copy of
the whole page collection, downloaded
once as an archive and unpacked into a
folder (`~/.cache/tealdeer/` by default).
All lookups read the cache; nothing about
a lookup needs the network.

**client** — the program you run to fetch
and render pages. Many exist, written to
a shared specification; this guide's is
Tealdeer. Clients are interchangeable in
a way pages are not: the pages are the
shared asset.

**common** — the platform folder for
pages whose commands work the same on
every system; also usable as a
`--platform` value. Most pages live here.

**custom page** — a page you write
yourself, in the custom pages directory,
for a command the collection does not
cover (usually your own script). In
Tealdeer 1.9.1 its file is named
`<command>.page.md`. A custom page with a
community page's name replaces that page.

**custom pages directory** — the folder
holding your custom pages and patches,
never touched by cache updates
(`~/.local/share/tealdeer/pages/` by
default; `--show-paths` names yours).

**man page** — the built-in manual page
for a command, read with the `man`
command: the complete, version-matched
reference that tldr relieves of reminder
duty. Chapter 6 is their comparison.

**Markdown** — the plain-text format the
pages are written in: `#` titles, `>`
quoted descriptions, backticked commands.
Chosen so a page can be read raw, edited
anywhere, and reviewed like code.

**page** — one command's cheat sheet:
a description, a link to the real
documentation, and a handful of examples.
The unit of the whole project.

**patch** — a file named
`<command>.patch.md` in the custom pages
directory, holding extra examples that
the client appends to the community page
of the same name at render time.

**placeholder** — the part of an example
command you replace with your own value,
written `{{like this}}` in a page's
source. Placeholders offering two
spellings, `{{[-C|--directory]}}`, render
as one or the other depending on the
short/long option setting.

**platform** — the operating-system
family a page variant is written for:
linux, macos, windows, the BSDs, and
others, plus common. The client serves
your platform by default; `--platform`
asks for another's page.

**render** — what the client does to a
page: turn the Markdown source into the
tidy terminal layout, with colour on a
terminal and plain text in a pipe.
`--raw` skips it; `--render` applies it
to any file.

**Tealdeer** — the client this guide
installs: a single static binary written
in Rust, named for the letters TLDR,
whose selling points are speed and a
small footprint. Its messages usually
call it `tldr`, after the project.

**tldr** — *too long; didn't read*,
recycled as a compliment: the project
(tldr-pages) of community cheat-sheet
pages, the idea of answering with
examples only, and, in many
installations, the command name itself.

**tldr-pages** — the volunteer project
and repository that holds the pages,
reviews contributions, and publishes the
archives clients download.
