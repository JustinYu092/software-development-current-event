# Sources: Claude Code (Kyeongjun Yu)

## Primary (verified by opening the page)
- GHSA-ff64-7w26-62rf (CVE-2026-25725): https://github.com/advisories/GHSA-ff64-7w26-62rf
- GHSA-vp62-r36r-9xqp (CVE-2026-39861): https://github.com/advisories/GHSA-vp62-r36r-9xqp
- GHSA-7835-87q9-rgvv (CVE-2026-55607): https://github.com/advisories/GHSA-7835-87q9-rgvv
- anthropics/claude-code issue #92593 (Windows rm -rf, text partially readable): https://github.com/anthropics/claude-code/issues/92593

## Secondary: reported incidents (user accounts, not independently verified)
- Android Headlines, "claude code ai agent deletes 48000 files in 103 seconds" (Sept 2026): https://androidheadlines.com/2026/09/claude-code-ai-agent-deletes-48000-files-in-103-seconds.html
- Vibe Graveyard, four Windows root-deletion reports (Sept–Oct 2026): https://vibegraveyard.ai/story/claude-code-windows-path-alias-recursive-deletions/
- Storyboard18, Grigorev production wipe (Mar 2026): https://www.storyboard18.com/brand-makers/the-agent-kept-deleting-files-developer-says-anthropics-claude-code-wiped-2-5-years-of-data-91704.htm

## Secondary: vulnerability write-ups (for context only, not used for severity)
- ToolsLib blog, CVE-2026-39861 (May 13, 2026): https://blog.toolslib.net/2026/05/13/claude-code-cve-2026-39861-symlink-sandbox-escape/
- SentinelOne vulnerability database, CVE-2026-25725: https://www.sentinelone.com/vulnerability-database/cve-2026-25725/

## Notes on source quality
- The ToolsLib article's byline describes an AI-assisted writer; use only for mechanism, not severity.
- Vibe Graveyard and Android Headlines rely on user reports and state that they are unverified; cite them as "reported".
- Do not cite CVSS 10.0 (seen on one aggregator); the GitHub advisory states 7.7.
