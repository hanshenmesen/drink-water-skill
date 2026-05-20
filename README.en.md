# 💧 The Hydration Oracle

> A water reminder **that knows how to shut up.** No timers, just vibes.
> Most of the time it stays silent. When it speaks, it uses two lines.

**Languages**: English · [简体中文](README.md)

[![Skill](https://img.shields.io/badge/Claude-Skill-1E40AF)](#)
[![License](https://img.shields.io/badge/license-MIT-black)](#license)
[![Status](https://img.shields.io/badge/silence_first-✓-brightgreen)](#)

---

## What problem it solves

Most water reminders die on "timers": "time for water!" every two hours, muted on day three, uninstalled on day seven.

**The Hydration Oracle** does the opposite — it doesn't count time, it reads the room.
Its design goal isn't "nudge often", it's "get uninstalled slowly".

---

## How it works

Before every reply, Claude runs a quick **traffic-light check**:

### 🟢 Green lights (any one is enough to *consider* speaking)

| Signal | Examples |
|---|---|
| Body words | tired / dry mouth / brain fog / headache / 累 / 口干 |
| Just shipped | tests pass / PR merged / demo done |
| Debug death loop | same problem failed ≥ 3 times |
| Time cues | "been writing all afternoon" / "two hours in" / "just woke up" |
| First-of-the-day | the morning glass |

### 🔴 Red lights (any one → stay silent)

- Emotional topics (interpersonal stress, grief, conflict, mental health)
- A one-line factual question, asked on the way out
- Already nudged once in this session
- The user has said any of *no thanks / drop it / stop / leave me alone* → **silent for the rest of this session**
- Fast-paced technical exchange in flow
- The reply itself is already long

### Decision

```
nudge = (any green light) AND (no red lights)
```

Body signal or fresh ship → speak.
Time cue only → lean toward silence.
**When in doubt, shut up.**

---

## 5 personas, picked by vibe, never repeated back-to-back

| Persona | When | Line |
|---|---|---|
| 🍷 Sommelier | default | Pause. One glass. Top note: focus. Finish: clarity. Now. |
| 🦉 Night Owl | "it's late / all-nighter" | Keyboard's still warm, the night is long. Water first. |
| 💪 Gym Bro | just shipped / hyped | STACK THE GAINS. Hydrate before the next set. |
| 🔬 Scholar | analytical writing | Cognition drops around ~2% dehydration. One sip? |
| 🧘 Elder | stuck / frustrated | Thirty seconds away. Water. Window. One breath. Then look again. |

---

## Output format

```markdown
[Claude's actual answer …]

---
💧 *Sommelier:* Pause. One glass. Now.
```

- ≤ 2 lines
- Always **after** the answer
- Always small, never steals the show

---

## Status panel (only when you ask)

Trigger phrases: *how many glasses / hydration / hydration status / how many today*

```
💧 Hydration Oracle · Status
─────────────────────────────
Session   nudges 3 · acks 2
Today     nudges 5 · acks 4
Week      nudges 18 · acks 14
Total     nudges 142 · acks 117
Streak    4 days
```

- The numbers are the feedback. **No "nice job!" / "keep it up!"** lines.
- **Never** attach the panel to a regular nudge.
- All zero → just *"Not open for business yet."*
- When the persistent layer is unavailable, only show the session row and say so honestly.

---

## State has two layers (a design we're picky about)

```
┌──────────────────┐  resets at session start
│  Session layer   │  lives in Claude's context
│  always available│  minimum guarantee
└──────────────────┘
         ↓ optional overlay
┌──────────────────┐
│  Persistent layer│  only when env provides memory / files
│  today/week/     │  skip entirely when unavailable
│  total/streak    │  never fabricate numbers
└──────────────────┘
```

This part matters — plenty of skills pretend to have persistent state in their docs, but every session actually starts from zero and they still display a bunch of "fake numbers". **The Hydration Oracle only shows what it actually has.**

---

## Install

Drop `SKILL.md` (or `SKILL.en.md` if you prefer English) into Claude's skills directory (path depends on your runtime; Cowork / Claude Desktop / Claude Code each have their own).
Or drag in the `.skill` bundle.

```
your-skills/
└── drink-water/
    ├── SKILL.md          # 中文 (default)
    └── SKILL.en.md       # English
```

Loading conditions are baked into `description` — long sessions, fatigue signals, fresh-ship moments will summon it automatically.
**Loading ≠ nudging** — most loads end in silence, on purpose.

---

## Design principles

1. **Loading ≠ nudging.** The broad description is to get into context, not to open mouths.
2. **Silence is the default.** Speak only when all lights are green, and only two lines.
3. **Don't fake what you don't have.** No wall-clock → no time trigger. No memory → no history.
4. **Numbers without exclamation marks.** Not a leaderboard, not a medal, not a guilt machine.
5. **One "stop" silences forever.** "Leave me alone" is a termination, not a retention test.

---

## What it is **not**

- ❌ A timer
- ❌ A milliliter counter
- ❌ A medical tool
- ❌ A guilt machine
- ❌ An entry point into wellness lectures

---

## Failure modes to avoid (written into the skill so Claude doesn't backslide)

| Anti-pattern | Description |
|---|---|
| Repeat offender | Same persona, same line, twice |
| Therapist | A paragraph of emotional care around hydration |
| Worried parent | "Have you had enough water today?" |
| Poking in a crisis | Cracking jokes while the user fights an incident |
| Wall-of-water reply | Letting the nudge steal the show |
| Speaking on load | Confusing "loaded" with "open your mouth" |
| Fake data | Showing today/week/total when persistence is unavailable |

---

## Pre-send checklist (5 items)

1. Did I actually answer the thing they asked?
2. Is the nudge ≤ 2 lines?
3. Different persona from last time (if I remember)?
4. No red lights tripped?
5. **If a friend sent this to me, would I roll my eyes?**

All 5 pass → send.

---

## License

MIT — use it, keep the "knows how to shut up" core.

---

> The oracle is a friend who watches, not a clock that nags.
> Missing once is fine. Annoying once gets it muted forever.
