# ◊ FallOffice · sovereign office suite

> v2 · seven apps + one orchestrator · single HTML · sovereign · MIT · prime 7

**Live:** [sjgant80-hub.github.io/falloffice](https://sjgant80-hub.github.io/falloffice/)

A full office suite that runs from `file://`. Your data stays in IndexedDB on your device. No accounts, no subscriptions, no telemetry. One HTML file replaces seven Microsoft 365 apps.

## What's inside

| | App | Replaces | Engine |
|---|---|---|---|
| ¶ | **Words** | Word | rich-text editor · markdown / HTML / TXT export · auto-save |
| ⊞ | **Sheets** | Excel | spreadsheet with formula engine · SUM AVG MIN MAX COUNT IF ROUND ABS SQRT CONCAT NOW TODAY LEN UPPER LOWER · range syntax `A1:A10` · CSV / JSON export |
| ❏ | **Slides** | PowerPoint | deck builder · markdown body · standalone HTML deck export with arrow-key navigation |
| ✉ | **Mail** | Outlook compose | draft compose · cc / subject / body · mailto send · `.eml` export |
| ☐ | **Calendar** | Outlook calendar | month grid · click-to-add · ICS export |
| ≡ | **Notes** | OneNote | markdown editor · tag search · per-note export |
| ✓ | **Tasks** | To Do | priorities · projects · due dates · markdown checklist export |

And one thing Microsoft doesn't ship:

| | App | Power |
|---|---|---|
| **Ω** | **Autopilot** (Ctrl+K) | type plain English ("draft a quote for Acme £2,400") · the Ω orchestrator routes to the right app and auto-fills via your model (T3) or by built-in rules (T0) |

## How autopilot works

Press **Ctrl+K** (or click ◊ autopilot in the toolbar). Type what you want in plain English:

- *"draft a quote for Acme — £2,400 for the discovery sprint"* → opens Words with the document pre-filled
- *"spreadsheet for monthly expenses"* → opens Sheets with a template
- *"three-slide deck on why our pricing changed"* → opens Slides with three slides drafted
- *"email Mansoor about Friday's review"* → opens Mail with subject + body
- *"meeting with Ivan Thursday 2pm"* → opens calendar event form
- *"jot · the audit shim needs SRI hashes"* → opens Notes with the captured thought
- *"todo · ship the brand pack by Friday"* → adds the task with the due date

**T0** (offline) routes by keyword. **T3** (any LLM key in settings) routes intelligently *and* generates the body. Same operation, different depth.

## Cascade

| Tier | Source | Fires when |
|------|--------|-----------|
| **T0** | built-in keyword router | always · works offline |
| **T2** | local Ollama at `127.0.0.1:11434` | if running |
| **T3** | Anthropic / Gemini (free) / OpenAI / OpenRouter | any key set in Settings |

Keys stay in your browser. Sent direct to the provider, never relayed.

## Sovereignty stack

Per the estate doctrine, sovereign at all four layers:

| Layer | Status |
|---|---|
| **UI** | runs from `file://` · no server required |
| **Compute** | T0 in-browser · T2 your local Ollama · T3 your direct API call |
| **Storage** | IndexedDB · JSON export covers everything |
| **Mesh** | `BroadcastChannel('fall-signal')` · prime 7 · responds to ping · `postMessage` API for `ping` and `create` |

## Use it

1. Open `index.html` from `file://` or visit the live URL
2. Press **Ctrl+K** to summon Ω · or click any app tab
3. (Optional) Open Settings → drop in a Gemini key (free) to unlock T3
4. Use it the way you'd use Office

Auto-saves continuously to IndexedDB. Export everything at any moment via Settings → ↓ export everything. Import to restore.

## Keyboard

- **Ctrl+K** / **Cmd+K** — open autopilot palette
- **Esc** — close any modal
- **↵** — execute the autopilot intent

## For developers

```
index.html               one file · ~70KB · vanilla JS · no deps
README.md                this
LICENSE                  MIT
.nojekyll                Pages legacy deploy
archive/agents.html      previous FallOffice (sales+marketing agents) — preserved
```

### Architecture

- **Shell:** 48px header (brand + tab nav + tools) + one `<main id="view">` that swaps in app HTML
- **State:** one top-level `state` object · persisted to IndexedDB under key `state`
- **Apps:** each app has `viewX()` (mount), `renderXSide()` (left panel), `renderXPane()` (right panel). All seven follow the same shape.
- **Cascade:** generic `Cascade.generate(system, user)` returns `{tier, text}`. Falls through Anthropic → Gemini → OpenAI → OpenRouter → local Ollama → null.
- **Orchestrator:** `omegaRoute(intent)` tries T0 keyword match first, then sharpens with T3 if available. Returns `{app, title, body}`. Each app's `newX(title, body)` accepts these params.
- **Formula engine:** `evalFormula(expr, cells, seen)` expands cell references and ranges, then runs the expression in a sandboxed `new Function()` with the function library injected as args. Cycles detected via `seen` set.

### Adding an app

1. Add to `APPS` array (id, name, icon, hint)
2. Write `viewX()` setting `#view` innerHTML and calling render helpers
3. Add a route to `ROUTES` for autopilot keyword matching
4. Add the app's switch case in `executeIntent()` for autopilot prefill
5. Add a default for it in `getDefaults()` so old state migrations work

### What this does NOT do

By design — the speed comes from saying no:
- **Real-time collaboration** — no server, no presence, no CRDT
- **Track changes / comments** — single-author tools
- **Image embed in Words** — paste plain text, link to assets
- **Pivot tables / charts in Sheets** — small enough that CSV → external chart is fine
- **Send mail directly** — `mailto:` + `.eml` export · your mail app sends
- **Real IMAP / Exchange** — would require a backend

If you need those, you need Microsoft 365. If you don't, you need this.

## Credit

- The fall* estate doctrine — every build-gate point honoured
- Previous FallOffice (sales/marketing agents) preserved at [`archive/agents.html`](archive/agents.html)
- Cascade pattern shared with [FallMap](https://github.com/sjgant80-hub/fallmap), [ACG Mapper](https://github.com/sjgant80-hub/acg-mapper), [FallForensics](https://github.com/sjgant80-hub/fallforensics)

◊·κ=1 · prime 7 · MIT
