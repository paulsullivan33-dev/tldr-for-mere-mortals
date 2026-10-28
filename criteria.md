# Writing criteria for this guide

Every "for Mere Mortals" guide is written to the same nine-point
standard, so a reader who trusts one can trust the rest. Here it
is, with the verification notes for this particular guide below.

1. **Fix it first.** Reader outcomes lead, not action items: each
   chapter opens by naming the outcome it delivers, shows a check
   the reader can run to confirm they got it, and a reasonable
   reader finishes able to state what was done, what it means,
   and what to try next.
2. **Plain language.** Short sentences, everyday vocabulary,
   technical terms defined on first use. No slang, and no
   idioms that only make sense in one country — the reader may
   be translating as they go.
3. **No dead ends.** A guide never tells the reader to do
   something it cannot show them how to verify. Every claim a
   reader relies on — an install, a command, an output — is
   something this guide demonstrates or clearly labels
   documented-only below.
4. **Live-verified where it matters.** Procedures are run for
   real in the guide's lab wherever the build machine allows it,
   and the transcripts kept in the repository are the evidence.
   What could not be run is listed honestly below, never
   presented as if it had been.
5. **General audiences.** Nothing in this guide — examples,
   fixtures, names, addresses — is modelled on any particular
   reader or author's real life, network, or organisations.
   The lab's traffic is the lab talking to itself.
6. **Standalone.** A reader needs this guide, its lab, and
   nothing else. Where another guide would genuinely help, it
   is pointed to once, by name, and the chapter still completes
   without it.
7. **Honest about limits.** Chapter 13 names what the tool
   cannot do: uneven coverage that is only discovered by asking,
   pages that can lag the tool they describe, examples without
   explanations or safety warnings, lookup by exact name only,
   the network needed for the first download, translations that
   trail the English collection, and the format's one-depth cap.
8. **The standing caution is in the text, early.** Chapter 1
   and chapter 6 state the guide's one safety-relevant rule —
   a cheat sheet is a reminder, not an authority, and commands
   that delete, overwrite or rewrite deserve the real
   documentation — before any procedure depends on it, and
   chapter 13 repeats the point where a page's silence could
   hurt.
9. **Builds clean.** The site builds with MkDocs in strict mode
   with no warnings, and a fresh reader following the chapters
   in order reaches the stated outcome of each.

## Verification notes for this guide

The build machine is a small Ubuntu 24.04 sandbox. The client
was **Tealdeer 1.9.1**, the official static binary
(`tealdeer-linux-x86_64-musl` from the project's GitHub
releases), verified against the project's published SHA-256
before first run, and exercised with a deliberately empty home
folder so first-run behaviour is a new user's behaviour. All
transcripts live in `tldr-lab/transcripts/`; the lab's personal
page and patch are `tldr-lab/pages/`.

Run for real, with transcripts as evidence:

- Install and version; `--help`, `--show-paths`, and a seeded
  config file read back in full (t00, t01, t02).
- The fresh-install refusal ("Page cache not found") and its
  return after `--clear-cache`, including the finding that
  custom pages also refuse while no cache exists (t01, t20).
- The cache update, twice over: first failing against this
  sandbox's TLS-intercepting proxy with
  `InvalidCertificate(UnknownIssuer)`, then succeeding after
  the config change the client's own error text suggests,
  `tls_backend = "rustls-with-native-roots"` (t03, t04).
- The downloaded cache measured: about 30 MB unpacked, 7,602
  English page files, 4,740 in `common`, 2,070 in `linux`,
  and a page count of 7,391 in this platform's `--list` view
  (t05, t10).
- Rendered pages for tar, curl, jq, sed, git-checkout and
  tldr itself, including a subcommand page asked for with a
  space (`tealdeer git checkout`) (t06, t07, t08, t10, t12,
  t19).
- A page's Markdown source read from the cache, and `--raw`
  producing the same source through the client (t09, t13).
- The short/long placeholder rendering of the same example
  (`--directory` versus `-C`) via `--short-options` (t13).
- Platform variants: the GNU (linux) and BSD (macos) sed
  pages side by side, including the `sed -i bak` spelling in
  the macOS page's source (t12).
- The three shapes of "no page": an invented name and a typo
  (both flat refusals, no suggestions), a real installed
  command with no page (`start-stop-daemon`, with `run-parts`
  and `savelog` probed the same way), and a language variant
  absent from the cache (`--language de tar`) — plus a page
  served for a tool that is not installed (`mkdocs`) (t11,
  t11b, t14).
- A personal page for an invented household script,
  `photo-backup`: invisible while named `photo-backup.md`,
  rendered once renamed `photo-backup.page.md`, the suffix
  discovered via `--edit-page` (t15).
- A patch (`tar.patch.md`) whose extra example appears at the
  end of the community tar page, and the precedence rules: a
  same-named custom page replaces the community page
  entirely, patch not appended, and removing it restores the
  community page with the patch still applied (t16, t16b,
  t16c).
- Configuration changes with visible effect: `compact = true`
  and `show_title = true` on a rendered page (t17), and the
  stale-cache nudge after the cache was artificially aged
  forty days against the 720-hour interval (t18).
- The broken-pipe complaint left when a page is piped into
  `head` (visible at the end of t10), kept in the transcript
  rather than cleaned away.

Documented only — described from the project's documentation
or characterised from evidence above, not run, and the text
does not claim otherwise:

- The man page comparison in chapter 6: the lab machine has
  no man-db installed, so the Ubuntu 24.04 tar(1) page was
  rendered with groff (man's own formatter, run from packages
  downloaded and unpacked into the lab's scratch area, never
  installed) and measured there — 1,164 lines, its examples
  reference found at line 46 pointing to the texinfo manual.
  The `start-stop-daemon` man page was measured the same way
  at 308 lines (t06b, t11). The chapter states this where the
  number is used; on a normal machine the equivalent is
  `man tar | wc -l`.
- Colour rendering and the `[style]` settings: transcripts are
  piped output, where the client prints plain text, so styles
  are described from the seeded config and the `--color`
  options, not demonstrated in colour.
- The interactive pager, editor integration beyond the
  filenames `--edit-page`/`--edit-patch` create, and behaviour
  on Windows and macOS machines (the macOS *page* was rendered
  on Linux; no Mac was involved).
- Other clients (the Node.js and Python clients, and others)
  and the neighbours of chapter 12 (cheat, cheat.sh, navi) are
  characterised from the project's own pages and
  documentation, not installed or benchmarked.
- Contributing a page upstream: the file format and the local
  result were run for real in chapter 9; the project's GitHub
  review process was not exercised.

Fixtures are this guide's own and deliberately generic: one
invented household backup script (`photo-backup`) with an
example.com address, one house rule about listing archives
before extracting them, and throwaway names
(`frobnicate-9000`) for commands that do not exist. No example
is modelled on any real person, network, service or
organisation.
