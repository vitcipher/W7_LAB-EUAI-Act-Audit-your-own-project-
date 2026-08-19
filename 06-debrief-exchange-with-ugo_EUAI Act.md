# Peer audit exchange — Whizbiz, EU AI Act lens

**Between:** Ugo Ahukannah (auditor) and Vittal Navale (builder) · **Sent:** 19 August 2026 · **Returned:** 19 August 2026

One file, one round trip. My parts are filled in below and returned. Ugo's full report travels with
this file: [`from-ugo/From_Ugo-eu-ai-act-peer-audit-whizbiz.md`](./from-ugo/From_Ugo-eu-ai-act-peer-audit-whizbiz.md).

**A process note, for honesty's sake:** Ugo's report and this exchange file arrived in the same
batch, alongside my own in-progress self-audit. That means Part 2 below isn't the product of a truly
blind window the way the lab intends — I had already seen his conclusions by the time I wrote my own
tier down. What I can say is that Part 2 was reasoned from the system's own facts and the regulation,
not copied from his findings, and the areas where we converge are because the facts are genuinely
clean (a transactional bot, not a person-scoring one), not because I deferred to him. Full reasoning
in [`02-risk-tier-classification_EU AI Act.md`](02-risk-tier-classification_EU%20AI%20Act.md).

---

## Part 1 — Five clarifying questions

**Q1. Is the bot's AI nature disclosed inside the product, or only in the marketing?**
> Only the product name. There is no explicit "you are talking to an AI" statement in any of the
> message nodes — I checked the exported workflow to confirm this rather than answering from memory.
> Your provisional assumption was correct.

**Q2. Who will place Whizbiz on the market, and under whose name?**
> Undecided. Currently me, individually — no company or other legal entity has been formed. The
> subscription model in the pitch is a plan, not yet a release decision.

**Q3. Where does the n8n instance run in production — is it the shared cohort instance?**
> Currently the bootcamp/course development instance. No separate production hosting has been
> decided. Your assumption was correct.

**Q4. Are `Kunde` and `Addresse` required for a legally valid German invoice, or convenience?**
> Required. German invoices need the customer's name and address as mandatory invoice content
> (§14 UStG-style requirements), so this isn't a convenience field that could simply be dropped —
> it narrows the fix to a minimisation/notice question rather than a "just remove it" one.

**Q5. Is the web-searched news headline in the daily digest presented as fact — labelled, and is the source URL checked before sending?**
> Presented as fact, unlabelled. There's no verification step in the workflow that confirms the
> headline exists or that the URL supports it before the digest sends. Your assumption was correct,
> and I'd already flagged this independently in my own gap analysis (Gap 3) before reading yours.

---

## Part 2 — My position, before reading the full report in detail

**My risk tier for Whizbiz, and the article behind it:**
> Limited risk / transparency, Article 50(1) — the bot converses directly with a natural person, which
> triggers the disclosure duty, while nothing it does assesses or scores a person, which keeps it out
> of Article 5 and every Annex III area.

**My top three findings from my own self-audit:**
> 1. No in-product AI disclosure (Article 50(1) gap) — the one obligation this tier actually imposes,
>    currently unmet.
> 2. No AI-literacy/limitations material for users (Article 4) — nothing tells a user that extraction
>    can be wrong or that they're responsible for checking figures before filing.
> 3. Provider entity undecided while a subscription model is described (Article 3(3)) — a paperwork
>    gap now, an accountability gap at launch.

---

## Part 3 — After reading your report in full

**My response:**
> The tier and the top findings match closely, which I take as a good sign for both audits rather
> than a coincidence — the underlying facts really are this clean. Two things from your report I'd
> add context to as the builder: first, the "correct?" confirmation message pattern on receipt
> extraction (e.g. "€23.80, REWE, 19% USt, category: Wareneinkauf — correct?") is a real, working
> review point, not just incidental UX — it's the specific mechanism your Section 5 observation about
> "the human stays in the loop by construction" is describing, and I think it's worth naming
> explicitly as a partial mitigation on the Article 4 gap, not just a nice side effect. Second, on the
> rolled-back confirm/cancel flow — that was cut for a concrete engineering reason (n8n's
> callback_query vs. message trigger shapes don't unify cleanly under deadline pressure), not because
> review wasn't valued; worth knowing since it affects how quickly Gap 1/2 could be closed versus how
> quickly a true pre-commit gate could be rebuilt.

**Where our tiers differ, if they do — genuine disagreement or a communication gap?**
> They don't differ. Given the process note above, I'd flag that near-total agreement here is weaker
> evidence of independent convergence than it would be in a genuinely blind exchange — but I also
> don't think a blind version would have landed anywhere else, given how unambiguous the "transaction,
> not a person" fact is.

**What did my self-audit catch that you missed?**
> Nothing tier-relevant — my Gap 6 (production hosting undetermined) roughly matches your Finding 6.
> The one addition is the German-invoice legal basis for `Kunde`/`Addresse` (Q4 above), which sharpens
> your Finding 5 from "personal data with no clear necessity" to "necessary personal data with no
> notice path" — a narrower, more accurate gap.

**What did you catch that I hadn't seen, or hadn't weighted the same way?**
> Framing Article 4 as applying at *every* tier, not just high-risk, was sharper than how I'd
> initially been thinking about it — I'd been treating literacy as a "nice to have" alongside the
> Article 50(1) gap rather than as its own standing obligation. Also, naming the provider-status
> question (Finding 4) as a live accountability gap tied to a specific trigger ("the moment that
> ships") rather than an abstract future concern was a more useful framing than mine.

---

## Part 4 — Joint closing note

**Vittal's draft, for discussion:**
> This exercise showed that when a system's underlying facts are genuinely clean — a bot that handles
> transactions rather than people — independent audits converge on the same tier, and the real value
> of a peer audit isn't a different classification but catching the operational gaps a builder stops
> seeing because they're "obviously" true in his own head (that the bot is AI, that a review step
> exists, that no one has decided who the legal provider is yet). Auditing your own work means
> knowing the system too well to notice what it doesn't say out loud; auditing someone else's means
> noticing exactly that, and nothing else.

**Agreed final version:**
> _pending — for us to agree together._
