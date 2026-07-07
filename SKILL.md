---
name: borrowed-brain
description: Distills any real person's public thinking (a business leader, scientist, writer, investor, teacher — anyone with a enough public track record) into a structured, reusable "thinking profile," then applies that profile as an extra lens on a problem the user is facing. Use this whenever the user names a specific person and asks to think, decide, or write "like" them, wants their "framework" or "mental model," asks "what would X think about this," or wants to build/update a saved profile for a person to reuse later. Also trigger when the user references an existing profile in profiles/ and wants it applied to a new question. Do NOT use this to impersonate a person's literal voice for creative writing/dialogue — that's a different task.
---

# Borrowed Brain

Turn a real person's public track record into a structured "thinking profile" — then use that profile to add a perspective to a decision, without pretending to speak for them.

This skill has two modes. Figure out which one the user needs before starting:

- **Distill mode**: no profile exists yet (or the user wants to refresh one) → research the person and produce `profiles/<name>.md`
- **Apply mode**: a profile already exists in `profiles/` → read it and use it to give the user another angle on their actual question

If unsure which mode, check whether `profiles/<name>.md` already exists first.

---

## Core principle (read this before anything else)

The output is **a speculative framework inferred from public material**, not the person's actual private views, and never a verbatim transcript of what they'd say. Every profile and every application of a profile must stay inside these lines:

- Never invent a quote or attribute words to someone they didn't say.
- Any direct quote must be under 15 words, and reuse at most one quote per source — everything else gets paraphrased in your own words.
- Every claim in the profile should be traceable to a source you actually found — if you can't find support for a "principle," don't include it.
- Frame outputs as "based on public material, X's approach seems to be..." — not "X believes..." stated as settled fact.
- For living/current public figures on contested topics (politics, active litigation, etc.), stick to describing their reasoning style and documented positions, not speculation about private motives or unstated views.
- If the person is a private individual (not a public figure) rather than someone with a substantial public record, decline — there isn't enough legitimate public material to responsibly build a profile, and it risks misrepresenting a real person who never put themselves forward for this.

---

## Distill Mode

### Step 1 — Scope the request

Confirm (ask only if genuinely ambiguous, otherwise infer and state your assumption):
- Full name of the person
- Any specific domain/angle the user cares about (e.g. "his product decisions" vs. general)
- Whether the user has specific source material to prioritize (articles, interview links, a book) — if so, use those as the anchor sources first

**Language**: write the profile file in the same language the user is using to talk to you (e.g. respond in Simplified Chinese if they've been writing in Simplified Chinese), unless they explicitly ask for a different output language. Source material found in other languages should still be paraphrased into the profile's output language — just keep any short direct quotes (under 15 words) in their original language with a brief translation alongside, so nothing gets misquoted through translation.

### Step 2 — Research (search in layers, don't do one generic search)

**Before searching, confirm you actually have working search/fetch tools in this environment.** If web search or web fetch isn't available here, say so plainly to the user — don't produce a profile from training-data memory and present it as researched. Offer two options instead: (a) write a profile explicitly labeled as "unverified — built from model memory, not live research, likely stale and unsourced," with that caveat repeated in the Confidence note, or (b) tell the user to run this skill in an environment with search access. Silently falling back to memory is the single worst failure mode for this skill — it produces exactly the kind of unsourced, unverifiable output the Core principle exists to prevent.

**Before searching, check for name collisions.** If the name is shared with something else — a common name, a programming language, a band, another public figure — note that ambiguity up front and filter every result for an actual match to the target person before using it. Search pollution from a namesake is a silent failure mode: it won't look wrong, it'll just quietly put the wrong person's material in the profile.

Run searches across these categories — not just one query. Adjust volume to how much public material exists (a global public figure needs more searches than a niche domain expert):

1. **Primary voice** — interviews, essays/letters they wrote themselves, talks, podcasts. These carry the most signal because they show real-time reasoning, not a summary of it.
2. **Documented decisions** — "why did X choose to..." / specific case studies where they made a call and the reasoning is on record.
3. **Third-party read** — how colleagues, biographers, or journalists describe how they think, to catch blind spots the person wouldn't self-report.
4. **Criticism and failure** — deliberately search for pushback, mistakes, and how they responded to failure. This is where real decision logic shows up — people are more candid about tradeoffs under pressure than in a polished profile piece. Skipping this step is the #1 reason profiles come out generic.

Use `web_fetch` on the actual articles/transcripts, not just search snippets — snippets are too thin to extract real reasoning patterns from. If a fetch fails (paywall, 403, dead link), don't just drop that angle — find a different source covering the same event or quote. A category should come up thin because the material genuinely doesn't exist, not because the first link you tried happened to fail.

Don't rely on one phrasing per category. Vary the query so you don't just get the same 2-3 puff pieces reworded. Examples (swap in the actual name/domain):

- Primary voice: `"<name>" interview transcript`, `"<name>" podcast full episode`, `"<name>" essay OR letter OR memo`
- Documented decisions: `"<name>" "why we" OR "why I decided"`, `"<name>" case study`, `"<name>" turning point`
- Third-party read: `"<name>" biography excerpt`, `"how <name> thinks"`, `colleagues describe "<name>"`
- Criticism/failure (never skip this category): `"<name>" criticism OR backlash OR controversy`, `"<name>" failed OR mistake OR wrong`, `"<name>" apologized OR admitted`

**Minimum bar before moving to Step 3**: at least 2 independent, non-overlapping sources (not two articles both quoting the same original interview), and at least one hit from the criticism/failure category specifically. If the criticism category comes up empty after a genuine attempt, say so explicitly in the profile's Confidence note rather than silently dropping that section.

If after a reasonable number of searches (roughly 8–15 for a well-documented person, fewer for a niche figure) the material is thin — fewer than 2 independent sources, or nothing beyond generic press-kit bios — say so plainly in the profile rather than padding it with generic filler. A short, honest profile that flags thin sourcing is a correct output, not a failure.

### Step 3 — Extract atomic facts first (don't jump straight to a summary)

Before writing any "principles," pull out raw, specific material:
- 3–5 concrete decisions or moments where their reasoning is visible on the record — note roughly when each happened
- 3–5 recurring phrases, analogies, or framings they actually use
- At least one documented failure/criticism and how they responded to it
- Where their own account and an outside account of the same thing differ, if that came up

Tag each fact with an approximate date. If the facts span years, check whether the person's stated position actually shifted over that time rather than assuming one moment represents a timeless view — if it did shift, that shift is itself worth carrying into the profile (e.g. "held X early on, moved toward Y after [event]") instead of flattening it into a single, undated stance.

This atomic layer is what keeps the final profile from sounding like every other profile — skipping it is why generic "thought leader" summaries all read the same.

**If you can't fill one of these with something specific** (e.g. you only found 1 concrete decision, or no real failure/criticism turned up despite searching), don't invent one to round out the set. Write down what you actually have, note the gap, and let Step 5's Confidence note reflect it. A thin-but-honest atomic layer produces a thin-but-honest profile — that's correct behavior, not a bug to paper over.

### Step 4 — Synthesize into the framework

Only now go from atomic facts up to the structured profile. Every principle you write here should trace back to something from Step 3 — don't introduce a "principle" that isn't grounded in a specific fact you found.

### Step 5 — Write the profile file

Save to `profiles/<name-slug>.md` using this template:

```markdown
# <Full Name>

*Profile generated <date>. Based on public material — a speculative framework, not verified personal views.*

## Sources
- [List the actual sources used, with links where available. Tag each as (self-published / company-controlled) or (independent third-party) — a company culture deck and an independent journalist's investigation are not equally strong evidence for a principle, and the tag lets the Confidence note discount accordingly.]

## Core stance
[2-3 sentences: how this person tends to approach problems in their domain, grounded in the atomic facts]

## Recurring principles
For each (aim for 3-5, only include ones with real support):
- **Principle**: [stated plainly]
- **Where it shows up**: [paraphrased case, 1-2 sentences, cite source]
- **Where it likely breaks down**: [a specific, concrete scenario — not a vague hedge like "under pressure" — ideally anchored to an actual moment from Step 3 (a documented case where they bent or abandoned it, or a plausible near-neighbor of one). If you can't tie it to anything concrete from the research, that's a sign the "principle" itself may be too generic to include — reconsider it rather than inventing a breaks-down clause to make it look rigorous.]

## Default reasoning order
When facing a new problem, what does the evidence suggest they check first, second, third? (Not invented — inferred from the documented decisions in Step 3.)

## Tradeoffs they lean toward
What do they consistently prioritize over what, when the two are in tension? (e.g. speed over polish, long-term relationships over short-term leverage)

## One documented failure or criticism
What happened, how they responded — this is often the most revealing material and shouldn't be dropped for flattery.

## Vocabulary / analogies they reach for
Short list of characteristic framings (paraphrased, not quoted verbatim beyond fragments under 15 words).

## Confidence note
Flag anywhere the material was thin, contested, or where you're inferring rather than finding direct evidence. Explicitly flag any principle above that leans mainly on self-published/company-controlled sources rather than independent third-party accounts — that's weaker evidence of a real, tested pattern than a principle backed by outside reporting.
```

Keep the whole file readable in one sitting — this isn't a biography, it's a working reference card.

### Step 6 — Differentiation self-check (do this before finishing)

Before treating the profile as done, reread the **Core stance**, **Recurring principles**, and **Default reasoning order** sections and ask: could these sentences be swapped onto a different person in this general field without anyone noticing? If yes, they're too generic — go back to Step 3's atomic facts and tighten the wording until it's specific to something only this person's record supports (a phrase they actually use, a decision only they made, a tradeoff visible in their specific history).

---

## Apply Mode

### Step 1 — Load the right profile(s)

Read `profiles/<name>.md`. If the user references more than one person, load each — multiple lenses on the same problem is often more useful than one, especially when the profiles pull in different directions.

**Check the profile's generation date before applying it.** People's public positions, roles, and circumstances change. If the profile is more than roughly a year old, or the person is someone whose situation moves fast (an active founder, a sitting politician, anyone mid-controversy), flag this to the user before applying it — e.g. "this profile is from [date] and may not reflect anything that's happened since; want me to refresh it first?" This is especially important for a profile like a "documented failure" that was current at generation time but may since have new developments (an admission, a reversal, a new incident) that change the picture.

### Step 2 — Apply it to their actual situation

Respond in the same language the user is using, even if the loaded profile file itself is written in a different language — translate the relevant principle/reasoning faithfully rather than quoting the profile file's language verbatim.

Don't answer as if you *are* the person. Structure the response as:

- "Running your situation through [Name]'s framework — particularly [the specific principle that's relevant] — a few things stand out: ..."
- Point out what this lens surfaces that might otherwise get missed, using the profile's specific principles and reasoning order, not generic advice
- If multiple profiles are loaded and they'd disagree, say so explicitly, and name it plainly rather than blending it into a compromise: "[Name A]'s [principle] points toward X; [Name B]'s [principle] points toward Y — these actually conflict here because [reason]." Don't resolve the disagreement for the user by picking a winner; the tension itself is the useful output.
- Always close by naming what this lens *doesn't* cover, or where the profile's "breaks down" condition might apply to their specific case

### Step 3 — Keep the epistemic boundary visible

This is a tool for surfacing an additional angle, not a verdict. Never present the output as "here's what you should do" in the profiled person's name — present it as "here's a angle worth weighing, and here's its limits." The user makes the actual call.

**In multi-turn conversations, this framing doesn't get a one-time pass.** If the user keeps asking follow-ups against the same profile, each response still needs the "running this through [Name]'s framework" framing and the closing limits — don't let it erode turn by turn into casually talking as if you were the person. The risk isn't in turn one, it's in turn five, after the framing feels repetitive.

---

## Notes for updating profiles

Profiles get stale or thin. If the user asks to refresh one, or if you're in Apply mode and the existing profile looks weak (few sources, vague principles, no failure case), offer to re-run Distill mode rather than silently working around a poor profile.
