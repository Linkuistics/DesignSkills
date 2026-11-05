# DesignSkills provenance

The skills use independent prose, but several disciplines and examples were
adapted from public prior art. This file keeps the claim-level source keys used
inside `SKILL.md` files without retaining the large point-in-time survey that
originally discovered them.

The sections below come from `plugins/linkuistics/PROVENANCE.md` in Grove. Each
covers one craft skill of this pack. `cli-tool-design` had no section there and
has none here. The three kind skills are Grove's own text, and the repository's
README names their source.

## Individual skills

### `codebase-design`

The skill distinguishes Ousterhout's reduction of design complexity through
interfaces and information hiding, Hickey's separation of independent concerns,
and Feathers' mechanism for substituting behaviour. Sources below were inspected
on 2026-09-19. The book's public extracts and the author's teaching material
support the Ousterhout guidance; this is not a claim to reproduce the full book.

| Key | Primary source | Contribution |
|---|---|---|
| `O1` | John Ousterhout, [Complexity and Dependencies](https://web.stanford.edu/~ouster/cgi-bin/cs190-spring16/lecture.php?topic=complexity) | Change amplification, cognitive load, unknown dependencies, and the cost of tactical design. |
| `O2` | Ousterhout, [Modular Design](https://web.stanford.edu/~ouster/cgi-bin/cs190-spring16/lecture.php?topic=modularDesign) | Interfaces include informal obligations; module depth, information hiding, useful generality, downward complexity, and alternative designs. |
| `O3` | Ousterhout, [A Philosophy of Software Design, second-edition extract](https://web.stanford.edu/~ouster/cgi-bin/aposd2ndEdExtract.pdf), chapters 6 and 21; [book page](https://web.stanford.edu/~ouster/cgi-bin/aposd.php) | General-purpose interfaces serving present needs, separating special-purpose policy, and identifying what matters. |
| `O4` | Ousterhout, [CS190 wrap-up slides](https://web.stanford.edu/~ouster/cs190-winter24/slides/wrapup.pdf) | Design warnings, documentation, and reducing avoidable error cases rather than multiplying caller handling. |
| `O5` | Ousterhout, [A Philosophy of Software Design vs. Clean Code](https://github.com/johnousterhout/aposd-vs-clean-code/blob/main/README.md) | Method length is not a design objective; comments carry information that code alone cannot express. |
| `H1` | Rich Hickey, [Simple Made Easy](https://www.infoq.com/presentations/Simple-Made-Easy/), Strange Loop 2011 | Simplicity versus ease, entanglement, state and time dependencies, composition, and abstraction. Publisher notes are summaries, not a verbatim transcript. |
| `H2` | Hickey, [Values and Change](https://clojure.org/about/state) | Values, identities, state over time, and explicit coordination. This supporting essay is distinct from the talk. |
| `F1` | Michael Feathers, [Working Effectively with Legacy Code: Seams](https://www.informit.com/articles/article.aspx?p=359417&seqNum=2) | A seam permits behaviour substitution without editing at that point. |
| `F2` | Feathers, [Seam Types](https://www.informit.com/articles/article.aspx?p=359417&seqNum=3) | Enabling points and concrete substitution mechanisms. |

The workflow, evidence table, deletion test, dependency categories, review
checklist, tradeoff rules, adapter vocabulary, and worked examples are Linkuistics
synthesis. They are not a joint method proposed by the three authors. In
particular, neither interface depth nor an immutable representation establishes
independence by itself, and testability is not a proxy for either.

The earlier skill also credited [`mattpocock/skills`](https://github.com/mattpocock/skills)
for its design-it-twice exercise. That inherited attribution is retained here;
the exact upstream snapshot is **UNVERIFIED**. The revised skill cites Ousterhout
for comparing designs and does not retain a required number of design agents.

### `decision-records`

The minimal template, examples, and three-part when-to-write test were adapted
from [`mattpocock/skills`](https://github.com/mattpocock/skills) at `b8be62ff`
(MIT). The minimum-coherent-set framing, in-place rework, and slug identity are
original to Linkuistics.
`decision-records/LICENSES/mattpocock-skills.LICENSE` holds the MIT licence
text of that source.

### `model-led-development`

Original to Linkuistics, and unusual in this file for having **no external prior
art at all**. Every rule in it is distilled from
[`docs/formalism-findings.md`](https://github.com/Linkuistics/grove/blob/main/docs/formalism-findings.md) in
Grove's repository, across **two** modelling campaigns and in two passes.

- **Entries 001 – 025**, distilled by `formalism-skill-k38`: one workstream
  extracting a tree-on-disk library under two formalisms (Alloy 6.2 on its
  structure, Quint 0.32.0 on its operations), with the model written before each
  operation was implemented.
- **Entries 026 – 048 and the log's closing synthesis**, distilled by
  `model-led-development-k94`: Alloy 6 and Quint on the *same* behavioural
  questions about Grove's own protocols, 129 obligations across 258
  `(family, obligation)` cells, against an implementation already shipped and
  green. Its rules are cited to the adjudication in
  [`docs/candidate-lessons.md`](https://github.com/Linkuistics/grove/blob/main/docs/candidate-lessons.md)
  as well as to the log, because that document re-opened the model files and
  falsified or weakened three of the six claims the producing sessions believed —
  including one the skill had shipped as a caution.

The citation keys inside the skill are `[003]` for a log entry, `[synthesis]` for
the log's closing sections and `[c1]` – `[c5]` for the adjudicated candidates;
the log's two distillation notes record where each entry landed and what did not
survive. The named tools are third-party: [Alloy](https://alloytools.org/) and
[Quint](https://quint-lang.org/) are cited as instruments, not adapted from.
