# Contributing to borrowed-brain

This is a single instruction file (`SKILL.md`) plus a folder of example output (`profiles/`). There's no build step, no tests to run, no dependencies to install — contributing means editing Markdown thoughtfully.

## Ways to contribute

**Add a test profile.** The most valuable contribution right now is a new profile in `profiles/` built by actually running Distill mode on a real person — ideally someone in a domain not yet covered (science, writing, sports, politics, etc.). Follow `SKILL.md`'s process for real: do the research, don't fabricate sources, and be honest in the Confidence note if material was thin.

**Improve the research/extraction process.** If you run Distill mode and notice the output is generic, under-sourced, or the guardrails leaked (an invented-sounding quote, a claim with no traceable source), open an issue or PR describing exactly what went wrong and where in `SKILL.md` the instruction should be tightened.

**Translate.** `README.zh-CN.md` is the first translation. Additional language READMEs are welcome — keep `README.md` (English) as the canonical source and translate from it, not from another translation.

**Report guardrail violations.** If any profile in `profiles/` (including the existing ones) contains a quote over 15 words, an unsourced claim, or speculation about someone's private motives, that's a bug — please open an issue.

## Ground rules (non-negotiable)

These come directly from `SKILL.md`'s Core principle and won't be relaxed for any contribution, including to make output sound more impressive:

- No fabricated quotes. Direct quotes stay under 15 words, one per source, everything else paraphrased.
- Every claim in a profile must trace to an actual source you found — not an assumption or something that "sounds right."
- No profiles of private individuals — only people with a substantial public record.
- No speculation about a living/contested figure's private motives — describe documented reasoning and positions only.

## Submitting a PR

1. Fork, branch, make your change.
2. If you're adding a profile, include the actual sources you used (real URLs, not placeholders).
3. Open a PR describing what you tested and what you found — "I ran Distill mode on X and here's the output" is more useful than "improved profile quality."

## Questions

Open an issue — there's no separate mailing list or chat for this yet.
