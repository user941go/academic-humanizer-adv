<div align="center">

<img src="assets/banner.svg" alt="Academic Humanizer: personalized editing for AI-assisted academic drafts, keeping your voice and every claim, number, and citation intact" width="860">

[![license](https://img.shields.io/badge/license-MIT-2f8f57?style=flat-square)](LICENSE)
&nbsp;![version](https://img.shields.io/badge/version-0.4.0-2f8f57?style=flat-square)
&nbsp;![skill](https://img.shields.io/badge/skill-papers_and_grant_proposals-1c1a15?style=flat-square)
&nbsp;![built by](https://img.shields.io/badge/built_by-NSF,_CAREER,_NIH_R01-555?style=flat-square)

</div>

## Why we built this

Some of us write a lot of papers and grant proposals, and our team started using AI to help with
drafts. The problem is that AI-assisted drafts come out generic and verbose, with "In recent years..."
openers, inflated phrasing, and over-long sentences. They also drift from the author's own voice and
lose the precision scholarship depends on.

There are tools called "humanizers," but they are built for blogs and marketing. Run one on a paper or
an NSF proposal and it flattens the precision along with everything else. The careful wording academic
writing depends on is the first thing to go.

So we put together our own. To calibrate it, we had the AI compare its own drafts with our team's
accepted papers and funded proposals, and we went through the differences by hand. It is nothing fancy,
and it is not about gaming review, defeating detectors, or adding fake novelty. We wanted AI-assisted
drafts to read clearly and in the author's own voice, with the numbers, citations, and claims left
exactly as written.

## Ethics and disclosure

This is an editing aid for clarity and voice, calibrated to an author's own prior accepted work. It does
not generate findings, invent data, or change citations, and it is not designed to evade AI-use
detection. Using it does not remove your obligation to disclose AI assistance: always follow the
disclosure policy of the venue you submit to.

## See it work

> [!CAUTION]
> **Before** (a generic AI draft):
>
> In recent years, continual learning has attracted increasing attention. Existing methods remain
> empirical, and their unclear principles limit reliability and progress. In this proposal, we propose a
> novel framework spanning adaptation, soft supervision, and cross-domain knowledge. We will evaluate it
> in autonomous driving and network management, paving the way for a transformative paradigm.

> [!TIP]
> **After** (clear, in the author's voice, with claims tied to evidence):
>
> Existing continual-learning methods remain empirical, and their unclear principles limit reliability
> and progress. This proposal develops a framework spanning adaptation, soft supervision, and cross-domain
> knowledge and evaluates it in autonomous driving and network management.

**More before/after passes** are in [`examples/before-after.md`](examples/before-after.md): a general
example, an NIH Specific Aims page, and a funded NSF CAREER summary.

---

## What it does

- **Sharpens clarity and voice:** trims generic AI phrasing, redundant hedging, unsupported rhetorical
  contrasts, repeated openings, and unclear or choppy sentence structure while retaining legitimate
  scientific usage and the author's punctuation and perspective.
- **Keeps claims tied to evidence:** no verb stronger than the supplied evidence. Missing support is
  flagged, never replaced with an invented number, statistic, citation, result, or evidence pointer.
- **Leaves real scholarship alone:** claims, uncertainty, perspective, terminology, numbers, statistics,
  units, equations, citations, headings, tables, figures, and cross-references stay intact.
- **Has a separate mode for grant proposals (NSF, NIH):** it keeps the vision a paper would trim, and
  spends most of the effort on the first pages, since that's what reviewers score.

## Install

```bash
git clone https://github.com/user941go/academic-humanizer-adv ~/.claude/skills/academic-humanizer
```

It is a plain `SKILL.md` plus examples, so it also runs as a skill or system prompt for **Codex** and
**MorphMind**. Point your agent at `SKILL.md`.

## Use

```
/academic-humanizer
[paste a section, or point at main.tex]
# optionally: "match my voice from prior_paper.pdf; target venue: ICLR"
```

Ask for **audit only**, a **conservative rewrite** (default), a **voice-matched rewrite**, or an
**invariant check**. For voice matching, an explicitly named file takes precedence; otherwise the skill
uses suitable files in `voice_sources/`. Voice samples influence style only, never content, evidence,
citations, results, arguments, or distinctive wording.

Place compatible papers or writing samples directly in `voice_sources/` (PDF, DOCX, TXT, or Markdown).
Name particular files in the request to select only those files; if none are named, the skill compares all
suitable files in that directory. It analyzes files separately, cross-validates recurring patterns, and
turns only well-supported or consistently chapter/section-matched findings into drafting process gates.
Single-source patterns remain provisional and are not applied as general voice rules.

## Make it yours

The rules here reflect one group's voice. Fork the repo and adapt them to your own: point it at a few of
your past papers, keep the checks that fit your field, and adjust the rest. It is meant to be
personalized, not a one-size-fits-all filter.

## How it works

Six layers: guarded general AI-tell catalog → academic-specific tells → preserve scholarly conventions →
claim↔evidence matching → evidence-backed voice/venue process gates → funding-proposal mode (NSF/NIH structure,
first-page primacy, claim↔feasibility). The audit→rewrite loop is defined in [`SKILL.md`](SKILL.md).

Version 0.4.0 aligns file, pasted-text, and embedded invocation behavior with that loop, adds a whole-draft
preservation recheck, and restores guarded checks for staged objections, fake alternatives, and staccato
fragments without weakening the academic exceptions.

## References

Layer 6 distills the *stable* structure of NSF and NIH proposals. For current, binding requirements
(page limits, formatting, deadlines), consult the source:

- NSF: [Proposal & Award Policies & Procedures Guide (PAPPG)](https://www.nsf.gov/policies/pappg)
- NSF: [CAREER program](https://new.nsf.gov/funding/opportunities/career-faculty-early-career-development-program)
- NIH: [Write Your Application](https://grants.nih.gov/grants/how-to-apply-application-guide/format-and-write/write-your-application.htm) (Specific Aims, Significance, Innovation, Approach)

## Acknowledgments

- **[blader/humanizer](https://github.com/blader/humanizer)** (MIT). *Focus:* removing general
  AI-writing patterns for blog, casual, and encyclopedic text. This skill reuses its general AI-tell
  catalog (Layer 1) and extends it for academic prose.
- **[koaeraser/ARMS](https://github.com/koaeraser/ARMS)**. *Focus:* an autonomous pipeline for
  statistics/methodology research papers (idea → validated, revised manuscript). A complementary,
  broader-scope project that informed the claim-evidence and numerical-precision emphasis here.
- **[WeMakeGood/extracting-voice-profiles](https://github.com/WeMakeGood/extracting-voice-profiles)**
  (MIT). *Focus:* source-grounded, cross-sample voice analysis and conversion of supported observations
  into generative process gates. This skill adapts that methodology to scientific and academic prose.

This skill is the narrower piece: a single-purpose **editing pass** that sharpens clarity and matches
claims to evidence while preserving the author's scholarly voice.

## License

MIT.
