# Sourcing Agent Skills

Markdown-only prompt assets that turn a general-purpose LLM into a **procurement lead for
cross-border sourcing** — the person who finds factories in China, quotes, negotiates, seals
samples, follows up production, inspects, and answers when something goes wrong.

No code. No framework. Just structured operating knowledge, written by someone who actually
runs a sourcing agency.

---

## The problem this solves

Sourcing agents in China mostly run on tacit knowledge: supplier contacts live in one
salesperson's WeChat, quotes are produced from memory, sampling has no confirmation gate, and
when a senior person leaves, the company forgets how to work.

The failures are predictable and expensive:

- The same product gets quoted at two different prices by two people, and the buyer concludes
  the agency is either unprofessional or dishonest.
- A sample passes, bulk fails, and nobody can prove what was approved — because there was no
  sealed sample, no signed confirmation, no retained reference.
- A new hire takes three months to become independent, because nobody wrote down what happens
  at each step or what document should exist when it's done.

This repository is an attempt to convert that tacit knowledge into something a machine can
execute and a new hire can follow.

## What's inside

| Skill | Size | What it is |
|---|---|---|
| [`sourcing-agent`](skills/sourcing-agent/) | ~24k words (references) | The full methodology: 8-stage flow, 14-section asset library, 5 case studies |
| [`sourcing-agent-lite`](skills/sourcing-agent-lite/) | ~1.5k words | A drop-in persona prompt, small enough to paste into any chat |
| [`sourcing-zero-to-one`](skills/sourcing-zero-to-one/) | ~2k words + 30-day plan | The first-month execution plan for a new agency |

They are three views of one system, not three separate tools: **the playbook** (how it works),
**the persona** (how the AI behaves), **the plan** (what to do on day one).

## Design decisions worth your attention

**1. The 17-module template was rejected, not extended.**

The starting point was a conventional "prompt generator" template with 17 flat modules — role,
background, writing principles, tone, audience, industry keywords, prohibited words, trending
topics, founder IP, and so on. That structure comes from content marketing. For procurement,
eight of those modules are empty calories: there is no such thing as a "banned advertising
word" in supplier vetting.

It was restructured into four layers instead: **identity → judgement → scenarios → assets**.
The word count went into the asset layer, because that is the only part anyone can execute.

**2. Uncertainty is engineered in, not wished away.**

A procurement advisor that invents a tax rate is worse than no advisor. So the persona carries
three mechanisms:

- **Gap protocol** — when information is missing, ask at most 3 questions, each with "why I'm
  asking", and always ship a provisional answer based on stated assumptions. Never hide behind
  questions.
- **Confidence tagging** — every conclusion is marked `[usable as-is]`, `[verify]`, or
  `[assumption]`. An answer where everything is `[usable as-is]` is treated as laziness.
- **Banned phrasing** — no "guarantee", "100%", "lowest price". Absolute promises to a buyer are
  how agencies create liabilities they cannot honour.

**3. The structural tension is the spine of the document.**

A sourcing agent does not own the goods but answers for the outcome, and earns on spread while
the buyer assumes it earns a commission. Almost every complaint and every trust crisis traces
back to that gap. So every rule in the playbook is checked against one question: *does this
narrow the gap or widen it?*

That is why the repository contains a "packaged price vs. cost-plus" quoting option, a
4-layer trust diagnosis (authenticity → competence → process → interest alignment), and an
explicit rule that **no balance payment means no telex release**.

**4. It was cross-checked against a second, independently written SOP.**

A separate 15-stage agency SOP was compared line by line. Only the deltas were merged: the
spread-vs-commission comparison table, the RFQ six-column quote format, supplier entry red
lines, sampling numbering, DUPRO mid-inspection, AQL accept/reject values, change-order
discipline, the ten contract clauses, carton mark verification, telex-release control, and
five case studies. Everything already covered was not duplicated.

## Repository structure

```
sourcing-agent-skills/
├── README.md
├── README.zh-CN.md
├── LICENSE
└── skills/
    ├── sourcing-agent/
    │   ├── SKILL.md                        # index and operating rules
    │   └── references/
    │       └── procurement-playbook.md     # full methodology (~24k words)
    ├── sourcing-agent-lite/
    │   └── SKILL.md                        # drop-in persona (~1.5k words)
    └── sourcing-zero-to-one/
        ├── SKILL.md                        # execution essentials
        └── references/
            └── 30-day-plan.md              # day-by-day first month
```

## How to use

**With Claude Code / Claude Skills**: drop a skill folder into your skills directory and
invoke it by name.

**With any chat model**: paste `skills/sourcing-agent-lite/SKILL.md` (strip the YAML
frontmatter) as the system prompt. For deeper work, load the relevant section of
`procurement-playbook.md` as additional context.

**As a human playbook**: `procurement-playbook.md` is written to be printed. The 10-item wall
checklist near the end is designed to be taped up next to a desk.

## What this deliberately does not cover

- Freight booking, customs declaration, foreign-exchange settlement, taxation — these are
  handed off. The only exception is **release-of-goods decisions**, because under a spread
  model the title documents are the sole leverage, and that decision belongs to the principal,
  not the documentation clerk.
- Legal opinions. The ten contract clauses are drafting starting points, not advice.
- Recruitment and compensation design.

## A note on the numbers

Figures such as a 10% margin floor, a 3–5% after-sales provision, a 30% deposit cap, and AQL
accept/reject values are **reference values from one operator's context**. Category, order size
and destination market change them substantially. Treat them as a starting point to calibrate,
not as standards to adopt. Items depending on live data (tariffs, freight rates, certification
costs) are explicitly tagged for verification rather than given as facts.

## Contributing

If your market, category or business model behaves differently, open an issue describing the
case. Divergent experience is more useful here than agreement.

## License

MIT — see [LICENSE](LICENSE). Use it, adapt it, sell with it. Attribution appreciated.

## Author

Feng — sourcing agency operator, writing down what the job actually taught.
