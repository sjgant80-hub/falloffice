# FallOffice · Sovereign AI Office

8+1 AI agents replacing a full Sales + Marketing team. One HTML file. No server. No subscription. Replaces hiring.

**[Try it →](https://sjgant80-hub.github.io/falloffice/)** — open in Chrome. That's the entire setup.

---

## What's Inside

### ◊ Omega (Ω) — Orchestrator

The command centre. Analyses your request, decomposes it through bloom rings (R0-R6), routes to the right specialist(s), chains their outputs, and synthesises one cohesive answer. Always present.

### Sales Team (α-δ)

| Agent | Archetype | Role |
|---|---|---|
| 🔍 **Scout** | α research | Prospect research, ICP scoring, company intel |
| ✍️ **Composer** | β compose | Personalised cold emails and LinkedIn messages |
| 📅 **Sequencer** | γ sequence | Multi-touch follow-up cadences and scheduling |
| 📊 **Analyst** | δ analyse | Pipeline insights, deal scoring, close probability |

### Marketing Team (ε-θ)

| Agent | Archetype | Role |
|---|---|---|
| 📝 **Writer** | ε write | Blog posts, articles, case studies, thought leadership |
| 📱 **Social** | ζ distribute | Platform-optimised posts for LinkedIn, Twitter/X, Instagram, Facebook |
| 🎯 **SEO** | η optimise | Keyword strategy, content calendars, on-page optimisation |
| 📣 **Ads** | θ target | Ad copy for Google, Meta, LinkedIn with character limits |

Every agent receives your company context, ICP, and brand voice automatically. Omega sits above them all.

---

## Why

| | Traditional Team | FallOffice |
|---|---|---|
| 2x SDRs | £70,000 | — |
| Content Writer | £45,000 | — |
| Social Media Manager | £38,000 | — |
| SEO Specialist | £42,000 | — |
| Ads Manager | £40,000 | — |
| **Total** | **£235,000/year** + office + benefits | **~£0–600/year** (API costs) |
| **Annual savings** | | **£213,600+** |

Your data never leaves your machine. Because there are no servers.

---

## Architecture

### 7 Mandatory Layers (Seed v16.3)

| Layer | Implementation |
|---|---|
| **L1 FACE** | Agent cards (face), chat workspace (template), user input (tag) |
| **L2 SWARM** | 8+1 MACCubeFACE — Ω orchestrator + α-θ specialists |
| **L3 CASCADE** | T0 Echo → T1 WebLLM → T3 API (Claude→ChatGPT→Gemini→DeepSeek) |
| **L4 BLOOM** | B(Q)=[r0..r6] decomposition, bloom-informed routing via Omega |
| **L5 PERSIST** | localStorage + interop namespace (`fall_falloffice_`), export/import JSON |
| **L6 SKIN** | Syne + DM Mono, dark/light (system pref), ◊ brand mark, editorial matte |
| **L7 ASS** | Lifecycle ●→〜→┃→♡→△→◐→◯ with phase-aware welcome messages |

### AI Cascade

```
T0: Echo (offline, ALWAYS WORKS)
T1: WebLLM (Llama 3.2 3B, in-browser, no API key)
T3: Claude → ChatGPT → Gemini → DeepSeek (API, cascade on failure)
```

### Bloom Routing

```
User input → B(Q)=[r0,r1,r2,r3,r4,r5,r6]
R0 ground → α (Scout)     R4 voice  → β (Composer)
R1 signal → α (Scout)     R5 mirror → η (SEO)
R2 gate   → δ (Analyst)   R6 watcher → γ (Sequencer)
R3 heart  → Ω (Omega)
```

### Interop

Shared localStorage keys readable by any Fall tool:
- `fall_shared_contacts` — contact list
- `fall_shared_company` — company context
- `fall_shared_bloom` — user bloom vector
- BroadcastChannels: `fall-signal`, `fall-data`, `fall-bloom`

### Konomi in Code

```javascript
const PHI   = 1.618033988749895;  // φ
const KAPPA = 0.618033988749895;  // κ = 1/φ
const SPINE = [2,3,5,7,11,13,17]; // prime spine
const FOLD  = 510510;             // primorial
const ARCHETYPE = {o1:'Ω',s1:'α',s2:'β',s3:'γ',s4:'δ',m1:'ε',m2:'ζ',m3:'η',m4:'θ'};
```

---

## Quick Start

1. Open `index.html` in Chrome, Edge, Safari, or Firefox
2. Click **⊙ Settings** → add any API key (or load WebLLM for offline)
3. Enter your company name, description, and ICP
4. Click **Omega (◊)** → ask anything → it routes to the right agent(s)

---

## Build

Single HTML file. All CSS and JS inline. To add an agent:

1. Add entry to `AGENTS` object with `id`, `name`, `icon`, `team`, `role`, `system`, `metric`
2. Add archetype mapping to `ARCHETYPE` object
3. Add metric to `METRICS` array if needed
4. Omega auto-discovers new agents for routing

---

## Related Products

| Product | Purpose | Repo |
|---|---|---|
| **FallOffice** | AI office — generates content, research, outreach | This repo |
| **FallForce CRM** | Sales platform — pipeline, contacts, deals, forecasting | [fallforce](https://github.com/sjgant80-hub/fallforce) |

---

◊·κ=1 · 8+1 agents · 2 teams · 1 orchestrator · 1 file · Ψ=0.59 · seed v16.3 · ai-nativesolutions.com
