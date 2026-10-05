# CLAUDE.md — Set Theory

Guidance for working in this repo. Set Theory (formerly Volleyball Tactic) is an ad-free web app for planning volleyball rotations, built for Ryden's team: a full court with draggable player circles (name + role), a clockwise Rotate button per team, run/ball-path arrows, and a 5-1 lineup generator (squad roles → every valid player group, with filters and OH/MB swap buttons). People share their squad and court with a `#s=` share link or a saved `.json` file. Hosted on Netlify at https://silver-blini-3cca1e.netlify.app/ (the link the team uses), linked to this GitHub repo: every push to `main` redeploys (settings in `netlify.toml`). GitHub Pages was turned off so the team only uses the Netlify link. The repo is public, so keep real teammates' names out of the code; real squads travel by share link.

Scenario buttons above the court (Base, Serve receive, Attack, Defend: OH/MB/RS) move the home team to spots computed from each player's role and rotation zone; while one is showing, the rotation spots live in `state.scen.base`, and Rotate rotates those and recomputes the scenario. The Settings tab sets the team system, kept in `state.settings` (defaults in `DEFAULT_SETTINGS`): defense system (perimeter / rotational / middle-up, spot tables in `DEFENSE_SYSTEMS`), libero left back or middle back, whether their hitter steps up in the Defend scenarios (their real spot is kept in `state.scen.oppBase`), and whether drags inside a scenario are saved. Saved spots live in `state.custom`, keyed by scenario plus the roles in zones 1-6, so they apply to any lineup with that shape. Share links carry settings (`set`) and saved spots (`c`).

Everything is one self-contained file, `index.html` (HTML + CSS + vanilla JS, no build step, no dependencies besides Google Fonts). Each viewer's board is saved in their own browser's `localStorage`. There is no server or shared database.

## Commands

```bash
python3 -m http.server 8777   # then open http://localhost:8777
```

## Invariants — do not break these

<!--
  Starts empty ON PURPOSE. Each entry should be a rule that cost a real bug once, stated
  with the bug that earned it. Add one the moment a bug is fixed — that is the only time
  the reason is still known. An invariant with no incident behind it is a guess.
-->

## Conventions

<!--
  How this codebase does things, where a newcomer would reasonably do it differently.
  Not style rules a linter already enforces.
-->

## Things that would trip you up

- The `localStorage` key is still `volleyball-tactic-board-v1` after the rename to Set Theory. Changing it would silently wipe every board people have saved on the live site.

<!--
  The non-obvious traps: a file that isn't where you'd look, a script that is deliberately
  NOT a script, a metric whose name lies, a standing false positive. Earned over time —
  leave this empty until something actually trips you.
-->

## Context

Design history and decisions live on the Notion project page (below). The app started as a claude.ai Artifact (https://claude.ai/artifact/A7KaLD96KcJXR5shJVAAo7), which briefly had a shared team board. That was dropped so people without Claude can use it.

## Session start

Before starting work, fetch the Set Theory Notion project page
(https://app.notion.com/p/3f05b79e681281608504ce0b52ff295b — cached in `.claude/notion-project.json`) and read its latest
`## 📓 Session Logs` entry plus current `Status`/`Next Step`. That's the last session's
state — use it instead of assuming a fresh start. Log this session's own work there with
the `log-session` skill before ending.
