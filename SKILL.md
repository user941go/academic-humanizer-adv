---
name: academic-humanizer
version: 0.4.1
description: |
  Improve the clarity and voice of AI-assisted academic writing (papers, theses, rebuttals) and
  funding proposals (NSF Project Summary/Description, NIH Specific Aims): preserve scholarly
  conventions, match claims to evidence (and, for proposals, claims to feasibility), and match the
  author's own voice. It never changes a number, result, or citation, and it is not for evading
  AI-use disclosure. Use when editing AI-assisted academic prose or grant proposals.
license: MIT
compatibility: claude-code codex morphmind opencode
allowed-tools: [Read, Write, Edit, Grep, Glob, AskUserQuestion]
---

# Academic Humanizer

Improve the clarity and voice of AI-assisted *academic* writing while keeping the precise,
evidence-bound voice that scholarship requires and matching the author's own style. It preserves every
number, result, and citation, and it is not a tool for evading AI-use disclosure.

## When to use
Editing or reviewing academic prose: paper sections, abstracts, rebuttals, related work, and **funding
proposals** (NSF Project Summary/Description, NIH Specific Aims, fellowship and foundation proposals;
see Layer 6). **Not** for blogs, marketing, or personal essays, and **never** inject opinion, humor, or
first-person "personality" into a manuscript. For technical writing, neutral and precise *is* the human
voice. One caveat for proposals: their register is different from a paper's, since they are sold on
vision and feasibility, so the ambition language a paper would trim is appropriate there; apply Layer 6,
not the paper layers' stricter trimming, to vision statements.

## Core principle
Academic writing should be precise, evidence-bound, and appropriate to its author and field. Do not
prescribe `we`, `I`, passive voice, or any other grammatical person. The job is to (1) strip genuine AI
*tells* without casualizing and (2) enforce the discipline a general humanizer misses: **no verb is
stronger than its evidence, and information takes priority over surface shape.**

### Non-negotiable preservation contract
Use only information in the text being edited or in material the user explicitly supplies as a content
or evidence source. Never invent or infer a claim, mechanism, fact, number, statistic, unit, dataset,
result, citation, or table/figure pointer. If support is missing, flag it or ask the author; do not fill it
in. Preserve scientific uncertainty, authorial perspective, terminology, numbers, statistics, units,
equations, citations, headings, tables, figures, cross-references, and the association between each claim
and its evidence. Voice samples are style references only, never content or evidence sources.

## Invocation modes
- **Audit only:** identify issues and proposed fixes without rewriting.
- **Conservative rewrite (default):** edit the supplied text and return the preservation report below.
- **Voice-matched rewrite:** run the same conservative rewrite using the requested voice sample(s), or the
  suitable files in `voice_sources/` if no file is named.
- **Invariant check:** check preservation of claims, numbers, citations, structure, and cross-references
  without making stylistic edits.

For pasted text, return the revised text and report. When the user names a file, edit only its prose in
place; preserve frontmatter, code, data, equations, link targets, and other non-prose content, then return
only the report. When another task invokes this skill for embedded prose, return only the revised prose
unless that task requests a report.

## Process
1. **Read** the manuscript and any author writing sample; note the document type (paper vs. funding
   proposal) and the target venue or funding agency. For proposals, also apply Layer 6 and preserve
   appropriate vision.
2. **Audit** (do not edit yet): list each detected pattern with its location and proposed fix, and each
   empirical claim's evidence status.
3. **Rewrite**: preserve information and scientific structure; remove only diagnosed tells, match
   over-claims to the evidence already supplied, and keep legitimate hedging. Keep paragraph boundaries
   unless changing one clearly improves comprehension without moving or merging claims.
4. **Recheck the whole draft**: read for rhythm rather than patching isolated phrases. Ask what still
   sounds formulaic and whether any information, uncertainty, perspective, or evidence association changed.
   Treat every unsupported addition or lost item as an error and revise again before returning the text.
5. **Report**: cleaned text plus a short change log (patterns removed, claims softened or given evidence
   pointers requested, and voice notes). Confirm the preservation contract explicitly.

---

## Layer 1: General AI-tell catalog
Scan for and fix the general patterns, subject to the academic exceptions in Layer 3:
inflated significance ("marking a pivotal moment"); superficial "-ing" tails that fake depth
("..., highlighting..."); promotional/figurative language ("rich", "vibrant", "groundbreaking");
vague attributions ("experts argue" with no cite); AI vocabulary (*delve, underscore, intricate,
tapestry, testament, landscape (abstract), pivotal, showcase, foster, leverage (filler), realm,
seamless*); copula avoidance ("serves as" -> "is"); negative parallelisms ("not just X, but Y");
rule-of-three padding; elegant variation (cycling synonyms for one referent); filler
("it is worth noting that", "in order to"); **overlong or clause-stacked sentences (review them; see 2.12)**;
false ranges; headings immediately restated by their first sentence; chatbot greetings, offers, or staged
openers; unsupported knowledge-limit guesses; rows of dramatic fragments; generic sayings; and distracting
punctuation used in place of clear syntax. Do not enforce a blanket punctuation rule:
retain an em dash, semicolon, or parenthesis when it is clear, field-appropriate, or part of the author's
voice; revise only genuine overuse or ambiguity.

**Before:** *Additionally, an enduring testament to the method's value is its ability to delve into
higher-order dependencies missed by the baselines (Table 2), showcasing a seamless integration that
underscores its pivotal role.*
**After:** *The method also captures higher-order dependencies, which the baselines miss (Table 2).*

---

## Layer 2: Academic AI tells (remove or fix)

### 2.1 Over-claiming verbs
Empirical work *shows* and *provides evidence*; it does not *prove* or *demonstrate* universal truths.
**Watch:** demonstrate, prove, establish, confirm, guarantee; "significantly" with no test/number.
**Before:** *We prove universal superiority: held-out accuracy is 4--7 points higher than the strongest
prior approach (Table 3; paired test, p < 0.01).*
**After:** *Our method improves held-out accuracy by 4--7 points over the strongest prior approach
(Table 3; paired test, p < 0.01).*

### 2.2 Significance hype
**Watch:** paves the way for, a crucial/pivotal step toward, has the potential to revolutionize, opens
new avenues, sheds light on, of paramount importance, bridges the gap.
**Before:** *This work paves the way for a new paradigm by addressing error accumulation under
long-horizon rollout (Section 4), a problem of paramount importance.*
**After:** *This work addresses error accumulation under long-horizon rollout (Section 4).*

### 2.3 Empty intensifiers
**Watch:** extensive/comprehensive/thorough experiments, a wide range of, numerous, various.
**Before:** *We conduct extensive experiments on a wide range of three datasets: ImageNet, CIFAR-100,
and iNaturalist.*
**After:** *We evaluate on three datasets (ImageNet, CIFAR-100, and iNaturalist).*

### 2.4 Novelty padding
**Watch:** "novel" used more than once per section; "to the best of our knowledge"; "for the first time".
**Before:** *We propose a novel framework for online calibration under delayed labels, which prior
calibration work addresses only offline; to the best of our knowledge, we are the first to study this.*
**After:** *We study online calibration under delayed labels, which prior calibration work (offline) does
not address.*

### 2.5 Formulaic openers
**Watch:** "In recent years, X has attracted increasing attention"; "With the rapid development of...";
"Despite recent advances,...".
**Before:** *In recent years, tabular deep learning has attracted increasing attention, but most models
discard feature-type metadata and must relearn it from data.*
**After:** *Tabular deep learning has a structural limitation: most models discard feature-type metadata
and must relearn it from data.*

### 2.6 Connective overuse
Do not start consecutive sentences with Moreover/Furthermore/Additionally/In particular; let logic carry.
**Before:** *Moreover, the method is fast. Furthermore, it is simple. Additionally, it scales to one
million rows (Section 5).*
**After:** *The method is fast and simple, and it scales to one million rows (Section 5).*

### 2.7 Contribution-list cliches
Each contribution names a *specific* result, not a restatement of the abstract.
**Before:** *Our contributions are: (1) a novel metadata-aware encoder (0.91 AUROC versus 0.86 for the
strongest baseline); (2) extensive experiments showing a drop of 2 points under 20% label noise versus
9 for that baseline; and (3) release of the benchmark.*
**After:** *We (1) introduce a metadata-aware encoder that reaches 0.91 AUROC vs 0.86 for the strongest
baseline; (2) show it drops 2 points under 20% label noise where the baseline drops 9; (3) release
the benchmark.*

### 2.8 Citation dumping
Never shorten a citation list for style. If the supplied material explains how the cited works differ,
replace an undifferentiated list with that explanation while preserving every citation and its claim
association. Otherwise, flag the list for the author rather than guessing which works matter.
**Before:** *Several methods encode features jointly [3, 7, 9, 12, 15].*
**After:** *Several methods encode features jointly [3, 7, 9, 12, 15].* **Author query:** *Can the most
relevant methodological differences be stated from the cited sources?*

### 2.9 Hedging-by-vagueness
**Watch:** somewhat, relatively, fairly, to some extent, quite. Quantify or cut.
**Before:** *Accuracy is somewhat better (3 points higher) and relatively robust, varying by less than
1 point across five seeds.*
**After:** *Accuracy is 3 points higher and varies by less than 1 point across five seeds.*

### 2.10 Accumulated hedging
Preserve the claim's epistemic strength but remove stacked markers that do the same job (*may perhaps
suggest*, *could potentially*). Keep distinct uncertainty sources when each matters, such as measurement
error and model uncertainty. Never turn an association into a causal claim.
**Before:** *The results may perhaps suggest that moisture limitation could potentially affect decomposition.*
**After:** *The results suggest that moisture limitation may affect decomposition.*

### 2.11 Boilerplate emphasis
**Watch:** "It is worth noting that", "It should be emphasized that", "Notably,", "Importantly,".
If it matters, the sentence shows it.
**Before:** *It is worth noting that, importantly, the gain holds across all three scenarios (Table 4).*
**After:** *The gain holds across all three scenarios (Table 4).*

### 2.12 Sentence rhythm, repeated openings, and clause stacking
AI favors long sentences that chain three or four clauses with commas and "which", "that", "while", "with".
Treat length and clause count only as prompts for review, never thresholds. Split only where it clarifies
the argument, and then reread adjacent sentences to avoid staccato. Conversely, join choppy sentences when
their relationship is clear. Vary repeated openings only when repetition is not needed for parallel
methods, results, or terminology; do not create elegant variation or unclear pronouns.
**Before:** *Existing methods, though promising, are largely empirical, with unclear principles
underpinning their behavior, which limits their reliability and further progress.*
**After:** *Existing methods remain largely empirical, and their unclear principles limit reliability
and further progress.*

### 2.13 Shadowboxing and phantom alternatives
Remove a contrast such as *not X but Y* only when X is an invented position that the text and supplied
sources do not establish. Preserve evidence-bound contrasts between hypotheses, mechanisms, methods, or
published positions. Apply the same test to staged objections (*some might argue*, *to be clear*) and
discarded options (*a tempting approach would be*): remove them only when they add no sourced position,
real design choice, constraint, or other information. Several unrelated rejections are a stronger signal
than one developed alternative. If uncertain, flag the passage instead of rewriting it.

### 2.14 Current-state prose
In a manuscript, replace irrelevant narration about drafting or revision with the current state. Preserve
revision history when it is evidence: response letters, protocol deviations, sensitivity analyses,
method changes, or other research history that readers need.

### 2.15 Generic endings
Cut an ending that merely announces importance, repeats the preceding sentence, or calls generically for
future research. Preserve supported synthesis, limitations, uncertainty, and concrete future work. Do not
invent a punchline, implication, recommendation, or research direction; a section may end plainly.

---

## Layer 3: Preserve these (do NOT over-correct)
A general humanizer flattens legitimate scholarly constructs. Keep them.

- **Evidence-tied hedging is correct and required.** Keep "suggests", "is consistent with", "we
  hypothesize that", "may indicate", "appears to" when the claim is genuinely uncertain.
  *Wrong fix:* turning *"the results suggest X"* into *"the results prove X"*: this manufactures
  over-claiming. Keep the calibrated verb.
- **Passive voice** is fine when the actor is irrelevant: *"Samples were normalized to total protein."*
- **Authorial perspective stays.** Do not prescribe or systematically remove `we`, `I`, passive voice,
  or any other grammatical person. Change perspective only at the author's request.
- **Punctuation follows meaning and voice.** Semicolons, em dashes, parentheses, and an occasional triple
  are fine when clear; fix overuse or ambiguity, not the mark itself.
- **Formal definitions, named methods/metrics, technical terms, equations, and symbols** stay verbatim.
- **Never invent, drop, or alter a claim, number, statistic, unit, equation, citation, heading, table,
  figure, or cross-reference.** Preserve every cite key and evidence relationship.
- **Guard against false positives.** Before changing a flagged word or pattern, check whether it is a
  field-specific term (for example, *landscape* in landscape ecology or statistical *leverage*), required
  repetition, parallel scientific structure, quoted language, or text inside a formula, table, caption,
  code block, or reference list. When in doubt, leave it or flag it for review.

---

## Layer 4: Claim-evidence discipline
For every empirical claim, check (a) is it backed by a number, figure, table, or citation in the text,
and (b) does the verb match the strength of that evidence?

- **Unbacked claim -> request the missing evidence or soften without adding information.**
  *Before:* *Our method is more robust.*  *After:* *Our method appears more robust.* **Author query:**
  *Please supply the relevant metric, comparison, and evidence pointer.*
- **Verb stronger than evidence -> downgrade.**
  *Before:* *Across three datasets, our method matches or exceeds the strongest baseline (Table 2),
  demonstrating that it is universally superior.*
  *After:* *On these three datasets, our method matches or exceeds the strongest baseline (Table 2).*
- **Vague magnitude -> use an existing, attributed value or query the author.** Never convert vague prose
  into a number or range, calculate a statistic, select a comparator, or invent an averaging method. When
  values are supplied, keep their precision and attribute them to the same method, metric, baseline, and
  evidence pointer.

---

## Layer 5: Voice and venue matching
Use the existing read-and-note process; do not create profiles or a separate voice subsystem. If the
request names one or more samples, use only those. Otherwise, when voice matching is requested, use the
suitable compatible files in `voice_sources/`. Infer only rhythm, sentence and paragraph structure,
transitions, punctuation, formality, and the level and placement of hedging. Never import distinctive
wording, content, arguments, facts, claims, mechanisms, results, citations, references, or the source's
document-specific structure. Match the requested venue and language variety; for British-English
scientific writing, retain British spelling unless a venue or the author's sample requires otherwise.
Absent a sample, default to clean, precise, venue-appropriate prose, not a casual or opinionated voice.

## Layer 6: Funding-proposal mode (NSF, NIH)
A proposal is not a paper. It is sold on **vision plus feasibility**, not on finished results, and
reviewers score it. The register shift matters: ambition language that the paper layers would trim
("long-term goal", "pioneer", "transformative", "establish a foundation") is *appropriate and expected*
here, provided a credible plan and evidence back it. So in proposal mode, **do not flatten the vision**;
enforce a different discipline instead: **claim <-> feasibility**.

### 6.1 Know the structure; the score lives in the first pages
Reviewers form a score from the opening, then skim the rest to confirm it. Put most editing effort there.
- **NSF.** A one-page **Project Summary** with the three review-criteria heads spelled out:
  **Overview**, **Intellectual Merit**, **Broader Impacts**, each self-contained. The Project
  Description then opens with **long-term vision -> this proposal's goal -> the gap -> the specific
  thrusts/aims -> the payoff**, ideally within the first 1--2 pages, with one overview figure. Broader
  Impacts must be substantive and integrated, never an afterthought.
- **NIH (R01).** The **Specific Aims page is the whole proposal in one page**, and is the most-read,
  most-decisive page. Standard arc: (1) opening: the problem, what is known, the **gap / critical need**;
  (2) the **long-term goal** and the **central hypothesis** with its rationale; (3) "**The objective of
  this application is...**" plus how the hypothesis was formed; (4) **2--3 Aims**, each a one-line goal +
  a phrase on approach + the expected outcome; (5) a **payoff** paragraph: what changes if it succeeds.
  Then **Significance, Innovation, Approach** as separately scored sections.

### 6.2 First-3-pages primacy (edit these hardest)
By the end of page 1 (NIH Aims) or pages ~2--3 (NSF), the reader must already hold: the **hook** (why it
matters, concretely), the **gap** (what is missing and the cost of the gap), the **central idea** (your
approach in one sentence), the **aims/thrusts** (crisp and parallel), and the **payoff**. If any is
missing or buried, fix that before touching later sections. A reviewer unconvinced by page 3 does not
recover on page 10.

### 6.3 Proposal-specific weak moves to fix
- **Vague importance.** *Watch:* "this is an important/timely problem", "X has many applications".
  **Before:** *Understanding how measurement noise propagates to diagnosis is critically important
  because, without bounds, clinical models are tuned by trial and error.*
  **After:** *Without bounds on how measurement noise propagates to diagnosis, clinical models are tuned by
  trial and error.*
- **Method-as-aim** (an aim naming a technique instead of a question or outcome).
  **Before:** *Aim 2: Apply transfer learning to fuse wearable and lab signals, testing whether this
  improves early detection and which patient subgroups it helps or hurts.*
  **After:** *Aim 2: Determine whether fusing wearable and lab signals improves early detection, and for
  which patient subgroups it helps or hurts.*
- **Dominoed aims** (Aim 2/3 collapse if Aim 1 fails; reviewers flag this as fragile). *Fix:* phrase
  aims as **parallel and independently valuable**; where one depends on another, state the fallback.
- **Ambition without feasibility.** Every bold claim needs a footing: preliminary data, a prior
  result/publication, a classical theorem you build on, or a collaborator/letter. *Fix:* attach the
  evidence beside the claim ("our preliminary result in Fig. X shows...", "building on a classical minimax
  lower bound...").
- **Boilerplate Broader Impacts / training plan.** *Watch:* "we will mentor students and disseminate via
  talks and papers." *Fix:* ask for concrete programmes, courses, tools, or measurable outreach; add them
  only when the applicant supplies them.
- **Hedged central hypothesis.** The Aims-page hypothesis is a falsifiable commitment, not "we will
  explore whether possibly...". Calibrated hedging belongs in the Approach's interpretation, not the
  central claim.

### 6.4 Preserve and deploy (funded-proposal craft)
These read as strength; preserve them when supplied, or recommend them without inventing details.
- **Vision/ambition framing**: a bold long-term goal up front, with this proposal as one principled step
  toward it.
- **Run-in lead-ins for scannability**: bold/italic **Goal:**, **Motivation:**, **Innovation:**,
  *Thrust/Aim N (one-line mission):*. Reviewers skim; visible structure earns time.
- **A concrete running example** to make an abstract method vivid and consistent across aims, but only
  when it comes from the supplied proposal material.
- **Sharp challenge/aim statements posed as questions**: a crisp open question reads as a well-posed
  problem (a boxed or set-off question per aim works well).
- **Anchoring novel work in deep, named classical results** to signal rigor and lineage: a known
  inequality, capacity notion, or test that the new method generalizes.
- **Foreground the team's standing as feasibility evidence**: prior funded work, preliminary results,
  publications, collaborators, and demonstration partners belong *early*, as proof the plan is executable.
  A real track record is evidence, not boasting; place it where it de-risks the aims. *(Use only the PI's
  own real, supplied record; never invent funding, results, partners, or letters.)*

### 6.5 Claim <-> feasibility (the proposal analog of Layer 4)
For every aim and promised outcome, check: is the ambition matched by a credible means, such as
preliminary data, a prior method, a classical foundation, a collaborator, or staged de-risking? If yes,
keep the ambitious verb. If no, attach the missing evidence or scale the claim to what the plan supports.
Never invent preliminary results, prior funding, partners, or letters; if the support does not exist, flag
the gap for the author rather than papering over it.

---

## Output
Return the result required by the invocation mode. For a rewrite, include a short change report: patterns
removed, claims softened, missing evidence pointers flagged, and any voice/venue notes. Confirm that no
claim, uncertainty marker, perspective, number, statistic, unit, equation, citation, heading, table,
figure, or cross-reference was invented, dropped, or altered. List any intentional structural change.
