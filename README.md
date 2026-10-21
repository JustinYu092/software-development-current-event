# Software Development Current Event Project

## Project Overview

**Topic:** AI Coding Agents Gone Wrong: Data Loss, Sandbox Escapes, and Security Risks

**Topic Summary:**
AI coding agents now run terminal commands, edit files, and interact with Git and databases, which gives them real power over developers' systems. Recent reports and security advisories show agents deleting live data and crossing the sandbox boundaries meant to contain them, through bugs in path handling, symlink resolution, and configuration files. This project compares these failures across three tools (Gemini, Claude Code, and Cursor) and explains what developers can do to limit an agent's blast radius.

## Team Members

| Name | Student Number | Role / Research Focus |
|------|----------------|-----------------------|
| Kyeongjun Yu | 120742267 | Research: Claude Code sandbox escapes / Slides |
| Ryan Klusacek | 117598268 | Research: Gemini sandbox escape / Script / Content |
| ByeongHak Lee | 134807221 | Research: OpenAI / Slides / Visuals |

Roles may overlap. Every member contributes through GitHub Issues, branches, commits, Pull Requests, reviews, and Discussions.

## Video Presentation

YouTube Video: https://www.youtube.com/watch?v=ayvV9KyTVA8

Desired Duration: 2:30–3:00 minutes

Actual Durtion: 3:03 minutes

## Repository Structure

```
.
├── README.md
├── research/
│   ├── research-notes.md
│   └── sources.md
├── script/
│   └── presentation-script.md
├── slides/
│   └── presentation-slides.*
└── media/
    └── presentation-assets/
```

- `research/`: individual research notes and verified sources
- `script/`: presentation script drafts and the final version
- `slides/`: presentation slides
- `media/`: images, screenshots, and other media assets

## GitHub Collaboration Workflow

- **Issues**: one issue per research case, script draft, slide design, video edit, and review
- **Branches**: one branch per task (for example `research-claude-code`, `research-gemini`, `research-cursor`, `script-draft`, `slide-design`, `video-edit`); `main` is not edited directly
- **Pull Requests**: each change goes through a PR, which teammates review before merging into `main`
- **Discussions**: topic decisions, case selection, script feedback, and progress updates

## Sources

Verified sources for each case are listed in `research/sources.md`.

## Project Deliverables

- [x] Individual research notes (`research/research-notes.md`)
- [x] Sources documented (`research/sources.md`)
- [x] Presentation script (`script/presentation-script.md`)
- [x] Presentation slides (`slides/`)
- [x] Video recorded and edited
- [x] Video uploaded publicly to YouTube
- [x] YouTube link added to README
- [ ] Issues created and completed
- [x] Branches created and merged
- [x] Pull Requests reviewed
- [x] GitHub Discussions used
- [ ] Final repository reviewed
