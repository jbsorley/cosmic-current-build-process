# Cosmic Current — AI-Assisted Build Process

> How a non-engineer founder built a production AI product — audit-first, verify everything, never let AI hold the judgment.

**Live product:** [cosmiccurrent.co](https://cosmiccurrent.co)  
**Builder:** [Jessica Sorley](https://github.com/jbsorley/Jessica-Sorley) — Senior Brand Director, AI Founder, Systems Thinker

---

## What it is

Cosmic Current delivers daily readings personalized to each user's birth chart. The product positions itself as "perspective, not prediction" — self-understanding infrastructure rather than astrology content.

**Technical stack:**
- Frontend / template implementation: Lovable
- Backend: Supabase (Postgres + edge functions)
- Astrology engine: astronomy-engine library + custom helpers in `generate-cosmic-calendar`
- Email: transactional via Supabase edge functions with per-user dispatch caching
- AI development partner: Claude

---

## How it was built

I'm a senior brand strategist, not an engineer. I built this product by treating AI as a thinking partner first, an implementation tool second, and never as a decision-maker.

The pattern that emerged across the build:

### 1. Audit before build

Every meaningful change to the codebase starts with a read-only inspection prompt that asks Lovable to report what's actually there — not what should be there, not what's planned, what *is*. Before fixing the email personalization pipeline, I ran a four-part audit that revealed every user was receiving identical "Moon in Libra → weigh and meet" copy regardless of their actual chart. The fix prompt that followed was surgical because the audit had removed all ambiguity.

### 2. Verify, don't trust

Lovable will claim success while leaving underlying data unchanged. Every build prompt ends with explicit grep checks that prove specific strings appear (or don't) in specific files. "Looks done" is not done.

### 3. Strategic decisions before implementation prompts

When evaluating new features (chapter arrivals, Human Design infrastructure), I worked through brand-strategic tradeoffs before writing a single line of spec. The implementation prompts are short because the strategic work already collapsed the option space.

### 4. Brand voice as a non-negotiable constraint

Every copy string in this product follows a documented voice framework: declarative not advisory, recognition not instruction, lowercase greetings, em-dash rhythm, first-person present-tense affirmation closes. AI doesn't invent voice — it encodes mine.

### 5. Portable context over session memory

A build context document holds the brand voice rules, Lovable prompting patterns, card structure spec, and Tier 1 arrival copy. Any new AI conversation about this product starts by loading the relevant section. Memory is owned by me, not by any AI.

---

## What's shipped

- **Core product** — live at cosmiccurrent.co with daily personalized readings, birth chart calculation, Supabase backend with per-user dispatch caching, transactional email infrastructure, and a working cron pipeline
- **Brand voice framework** — declarative, recognition-not-instruction, lowercase, em-dash rhythm, first-person present-tense affirmation closes — developed iteratively and codified
- **Rebuilt daily email template** — TypeScript interface, card-based structure (Transit, Focus, Today, Move, Prompt, Anchor, Affirmation), passing grep-verification
- **End-to-end email personalization** — audited the existing pipeline, identified Transit and Focus cards rendering hardcoded defaults for every user, designed and shipped a fix exposing five new astrology fields plus aspect-to-verb translation logic plus an abort-on-dispatch-failure path
- **Chapter arrivals architecture** — Tier 1 takeover screens, Tier 2 season frames, Tier 3 inline weather — with canonical copy for nine arrival types and a 3-stage Lovable prompt sequence
- **Custom operational agents** — inbox-to-calendar agent, signal-filtering agent

---

## The build loop (from conversation evidence)

```
Strategic question
       ↓
Audit existing code (read-only inspection)
       ↓
Architecture / tradeoff decision
       ↓
Spec writing
       ↓
Implementation prompt (encoding decisions already made)
       ↓
Grep-based verification
       ↓
Ship
```

One concrete example: the email personalization fix.

1. **Strategic question** — why are all emails reading the same?
2. **Audit** — four-part read-only inspection revealed hardcoded fallback copy in Transit and Focus cards
3. **Decision** — expose five new astrology fields, add aspect-to-verb translation, add abort-on-failure path
4. **Spec** — written in plain language before any prompt to Lovable
5. **Fix prompt** — surgical, single-purpose, encoding the spec
6. **Verification** — grep checks confirming specific field names appear in specific files
7. **Shipped** — production email personalization, no developer in the loop

---

## Artifacts *(coming soon)*

The following documents are being pulled from the active build and will be added here:

| File | Description |
|---|---|
| `voice-framework.md` | The declarative voice rules governing every user-facing string |
| `audit-prompts/` | Read-only inspection prompts used before every codebase change |
| `lovable-prompts/` | Build prompts written to prevent Lovable's known failure modes |
| `chapter-arrivals-spec.md` | Architecture and canonical copy for Tier 1 / 2 / 3 arrival moments |
| `email-personalization-fix.md` | The full audit → decision → fix → verify loop, documented |

---

## What this is not

This isn't a tutorial on AI-assisted coding. It's documentation of one specific working pattern: a non-engineer founder holding voice, strategy, and sequencing, while delegating implementation to AI under strict verification protocols.

The distinction that matters: I keep judgment in my seat. AI handles translation-to-implementation.

---

## Status

Production. Daily readings shipping to users. Iterating on chapter arrivals and Human Design infrastructure at time of writing.

---

*Part of [Jessica Sorley's GitHub profile](https://github.com/jbsorley/Jessica-Sorley)*
