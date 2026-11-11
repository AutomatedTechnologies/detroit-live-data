# detroit-live-data

Data plane for Live Transit Detroit (2026-11-10 split, Forge Line goal record).

The VM feed-publisher is the single writer. Every publish cycle it commits the
finished live-data payload set here (under `live-data/`, byte-identical to what it
writes to `AutomatedTechnologies/detroit-automation-academy-public`, which remains
the archive and the pages' fallback source) and GitHub Pages serves this repo on
its own: a few hundred kilobytes, so a data publish deploys in seconds instead of
queueing behind the full estate site build.

Consumers fetch `live-data/*` from this repo's Pages origin first and fall back to
the site origin, choosing the fresher copy by `generated_at`. The `watch/` subtree
is seeded from the site tip; its bundle producer is a separate pipeline and keeps
publishing to the site repo only.

No Cloudflare anywhere in this chain.
