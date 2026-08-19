# Compliance Memo — Whizbiz

**To:** Head of Product, Whizbiz
**From:** Vittal Navale, Project Lead
**Date:** 2026-08-19
**Re:** First-pass EU AI Act compliance position for Whizbiz V1

---

**1. System classification.** Whizbiz is a limited-risk AI system under Article 50(1) of the EU AI
Act — it converses directly with users, which triggers a disclosure duty, but it makes no decision
about a person and falls outside the Act's high-risk regime entirely.

**2. Role map.** We are the likely **provider** once Whizbiz is placed on the market as a
subscription product, though the release entity itself hasn't yet been formally decided. Each
subscribing solopreneur is the **deployer**, using the tool in their own business. OpenAI, as the
underlying model provider, carries its own separate general-purpose-AI obligations that don't
transfer to us.

**3. Key findings.**
- We don't currently tell users, inside the product, that they're talking to an AI system — only the
  product name implies it. This is the one obligation this risk tier actually imposes, and it's
  currently unmet.
- We don't give users any limitations guidance — that receipt extraction can be wrong, that category
  assignment is a model's best guess, and that figures should be checked before they're relied on for
  a filing.
- The daily digest includes a web-searched "real" news headline with no verification step before it
  reaches the user, sitting in the same trusted message as their financial data.

**4. Recommended next steps.**
1. Add an in-product AI disclosure and a short limitations note to onboarding — both are text changes
   to existing workflow nodes, shippable this sprint.
2. Label or verify the daily digest's news headline before the next release.
3. Record who the provider entity actually is before we take a single paying subscriber, and have
   that reviewed by counsel alongside the role split.
4. Treat the customer name/address data on the income sheet as a GDPR question first — that's covered
   in the separate privacy audit, not repeated here.

**5. Caveats.** This memo is not a legal opinion, not a conformity assessment, and not a
certification. It reflects a first-pass self-review, not an external audit, and every conclusion
here should be verified with legal counsel before Whizbiz is placed on the EU market or takes on a
paying subscriber.
