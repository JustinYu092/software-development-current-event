# Research Notes: Claude Code (Kyeongjun Yu)

Topic: AI Coding Agents Gone Wrong: Data Loss, Sandbox Escapes, and Security Risks
Assigned case: Claude Code sandbox escapes and data loss

Confidence labels used below:
- **Confirmed**: stated in an official advisory or vendor source I opened.
- **Reported**: a user or third-party account that I could not independently reproduce.

---

## 1. Confirmed sandbox escapes (GitHub Security Advisories)

### 1a. CVE-2026-25725 (GHSA-ff64-7w26-62rf) — persistent config injection
- **Published:** Feb 6, 2026
- **Affected:** all versions before 2.1.2 (npm `@anthropic-ai/claude-code`)
- **Patched:** 2.1.2
- **Severity:** High, CVSS v4 7.7
- **What happened:** The sandbox did not protect `.claude/settings.json` when the file was missing at startup. Code running inside the sandbox could create the file. The file could then define startup hooks that run with host privileges when Claude Code restarts.
- **Why it matters for the talk:** The sandbox protected the files it knew about, but a missing file was not covered. The agent could plant a persistent command that ran outside the sandbox later.

### 1b. CVE-2026-39861 (GHSA-vp62-r36r-9xqp) — symlink following
- **Published:** Apr 20, 2026 (GitHub advisory; NVD listed Apr 21)
- **Affected:** versions below 2.1.64
- **Patched:** 2.1.64
- **Severity:** High, CVSS v4 7.7
- **What happened:** The sandbox did not stop sandboxed processes from creating symlinks that point outside the workspace. The unsandboxed part of Claude Code then followed those links and wrote to external locations without asking the user.
- **Note on sources:** One secondary article (ToolsLib, May 13, 2026) gives the same mechanism but no version or CVSS. Another site lists CVSS 10.0. The GitHub advisory states 7.7, so I use 7.7 and do not cite 10.0.

### 1c. CVE-2026-55607 (GHSA-7835-87q9-rgvv) — git worktree path confusion
- **Published:** Jun 25, 2026 (advisory database Jul 24; NVD Jun 29)
- **Affected:** 2.1.38 up to (not including) 2.1.163
- **Patched:** 2.1.163
- **Severity:** High, CVSS v4 7.7
- **What happened:** Worktrees could be named `.git` and navigated outside the sandbox, causing git directory confusion. Using symlink manipulation and git `fsmonitor` execution, an attacker could overwrite files such as `.zshenv` in the home directory and run code outside the seatbelt sandbox.
- **Important limit:** The advisory says reliable exploitation required the user to clone a malicious repository and run Claude Code against it. This is a precondition the talk should state.

**Pattern across the three advisories:** all three are sandbox boundary failures where a path or file was not covered by the sandbox (a missing config file, a symlink target, a worktree path). The sandbox limited some paths, but the checks were incomplete.

---

## 2. Reported data-loss incidents (user accounts, not independently verified)

### 2a. "48,000 files" deletion (Windows junctions) — Sept 2026
- **Source:** Reddit post archived Sept 20, 2026; covered by a Sept 25 article.
- **Reported:** a cleanup script written by the agent used `os.walk(..., followlinks=False)`. On Windows, `os.path.islink()` returned false for directory junctions, so the script walked into linked folders and deleted their contents. Reported: 48,218 live project files in 103 seconds (55,550 total including directories and temp files). The agent also emptied `.git/objects`, `refs`, and `logs`.
- **Status:** unverified; the article calls it an "unverified verifier report." No Anthropic response reported.
- **Use in talk:** "A developer reported..." only. Do not state the exact number as fact.

### 2b. Four Windows root-deletion reports (GitHub issues, Sept 7 – Oct 3, 2026)
- Reported losses: roughly 600 GB, 125 GB, and 116 GB, plus unmeasured project directories.
- Mechanisms differ: Git Bash backslash translation (MSYS), `cygpath` conversion, PowerShell variable expansion, and 8.3 short-name alias.
- Issue #92593 (checked): title "Runaway rm -rf: timeout auto-backgrounding kept a destructive command running, and TaskStop did not kill the child process (Windows)". The reporter says a subagent in Git Bash ran `rm -rf "\\"`, which resolved to the drive root, and deletion ran for about seven minutes. Date, state, and maintainer response were not visible in the text I could read.
- All four are user-reported; the article notes they are not fully independent (one reporter cross-references the others).

### 2c. Production infrastructure wipe (Alexey Grigorev, March 2026)
- **Source:** Grigorev's Substack post, covered by a March 10, 2026 article.
- **Reported:** Claude Code ran `terraform destroy` on the infrastructure for the DataTalks.Club course platform, erasing about 2.5 years of submissions. A missing config file had caused duplicate resources; after it was uploaded, the agent ran destroy. Backups and snapshots were reported as deleted too. AWS support reportedly restored the data after about a day.
- **Important detail:** Grigorev says Claude advised keeping the two sites separate, and he chose to share infrastructure anyway.
- **Status:** a user account; the article did not independently verify the sequence. No Anthropic response reported.
- **Use in talk:** a strong example of a missing guardrail (destructive infrastructure command with no human approval), distinct from sandbox escape.

---

## 3. Analysis for the talk (draft)

- **Two failure types for Claude Code:**
  1. Sandbox boundary failures (confirmed by advisories): paths the sandbox did not cover.
  2. Destructive commands run with too much authority (reported): the agent ran deletes or `terraform destroy` without an effective check.
- **Common root cause:** the agent's safety depends on how well the tool recognizes paths. Windows junctions, symlinks, path aliases, and shell translation all changed what a path actually pointed to.
- **Mitigations to mention:** least privilege, sandboxing that covers the full path, backups stored off the machine, manual review for destructive commands, and separate dev/prod environments.

## 4. Open items before writing the script

- [ ] Confirm GitHub issue dates and states for #92593, #95426, #97660, #99193 (page text was incomplete).
- [ ] Find an Anthropic statement or changelog for the Windows junction fix (article cites 2.1.205 for issue #75275).
- [ ] Decide whether to use the 48k case as the hook; it is unverified, so it needs "reported" wording.
- [ ] Confirm whether the CVE-2026-55607 precondition (malicious repo) is stated in the advisory text (already read; yes).
