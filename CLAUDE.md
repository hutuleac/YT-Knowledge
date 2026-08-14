# YT Knowledge — Project Notes

Library of structured research briefs generated from YouTube videos (investing/AI-news podcasts,
crypto/market interviews, and dev/career/workflow content). Static HTML, no build step, no deps.

## Repo
- **Remote:** https://github.com/hutuleac/YT-Knowledge.git (`main` branch, no other branches used)
- **Live site:** https://hutuleac.github.io/YT-Knowledge/ — GitHub Pages serving `main` branch root
- Working directory root should only ever gain the finished `.html` brief + the refreshed
  `index.html`/`library.json`. Everything else (transcripts, JSON, archived data files) lives in
  `research-data/<slug>/`.

## Generating a brief
Use the **youtube-research-brief** skill (`~/.claude/skills/youtube-research-brief/SKILL.md`) for
every new video. It fetches the transcript via `yt-dlp`, cleans it, and drives `generate.py` off a
per-video Python data file (never edit `generate.py` itself per video). Read the skill file fresh
each time — it gets tuned periodically and this doc is not a substitute for it.

Key things baked into the current skill that aren't obvious from a first read:
- **`META["category"]`** is `"market"` (default — investing/AI-news mix) or `"dev"` (dev/systems/
  knowledge/AI-workflow content, no market angle). This drives which `index.html` tab a brief
  lands under, and which color/badge vocabulary applies (stock-conviction language for `market`;
  descriptive "character of the claim" language for anything else — never force ticker/stance
  vocabulary onto non-market content).
- **Sponsor content is always excluded.** No sponsor segment, plug, discount code, or "this video
  is sponsored by" read ever goes into a brief — not as a theme, OTHER_NEWS item, RISKS caveat, or
  glossary term. This was an explicit standing instruction, not a default of the skill template.
- `index.html` has four tabs: All Briefs, By Channel, By Company/Ticker, and Dev & Workflows
  (filtered to `category: "dev"`). Rebuilt automatically on every `generate.py` run, or standalone
  via `python3 <skill-folder>/generate.py --reindex`.

## Git conventions for this repo
- **Never add a `Co-Authored-By: Claude...` trailer to commits** in this repo — removed once
  already by explicit request, don't reintroduce it.
- Commit and push after generating each new brief (or batch of briefs) unless told otherwise.
- Local tool directories (`.claude/`, `.gstack/`, `.opencode/`, `.DS_Store`) are gitignored —
  they're editor/agent tooling, not project content, and don't belong in this repo.
