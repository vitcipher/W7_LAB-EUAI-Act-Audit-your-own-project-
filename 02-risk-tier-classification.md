# Risk Tier Classification — Whizbiz

**A note on process, honestly stated:** the lab asks you to classify your own system before
cross-checking against the official Compliance Checker, and before reading any peer audit. In
practice, my teammate Ugo sent his completed external audit of Whizbiz in the same batch as the
exchange document requesting my independent position, so I did not have a clean "blind" window. The
classification below is reasoned from the regulation and the system's own facts, not copied from his
conclusions — and where it agrees with his, that is because the facts are fairly unambiguous, not
because I deferred to him. Where I later found his framing sharper than mine, I've flagged it in the
gap analysis rather than silently absorbing it.

---

## Classification table

| Question | Answer |
|---|---|
| Does this system fall under any prohibited category (Article 5)? | **No.** No social scoring, no biometric categorisation or identification, no emotion inference, no subliminal manipulation, no exploitation of vulnerabilities. Receipt OCR and expense categorisation are not among Article 5's practices. |
| Does this system operate in any of the eight Annex III areas? | **No.** The closest candidate is Annex III(5)(b), creditworthiness assessment — but Whizbiz records income and expenses the owner already incurred; it does not assess anyone's ability to pay, extend or deny credit, or price risk. It has no presence in employment, education, essential services, law enforcement, migration, biometrics, or justice/democratic processes either. |
| If Annex III: does it "significantly influence" decisions in that area, or is it narrow/preparatory? | Not applicable — Annex III is not engaged. |
| Does this system interact with end users or generate content requiring disclosure (Article 50)? | **Yes.** The bot converses directly with a natural person over Telegram, which engages **Article 50(1)**: a person must be informed they are interacting with an AI system unless that is obvious from context. Separately, the daily digest's web-searched "real news headline" is a generative, fact-presenting output with no stated verification step — an accuracy/labelling question worth tracking even though it does not itself trigger Article 50(4) (that provision targets synthetic media intended to inform the public, not a private one-to-one message). |

## First-pass risk tier

**Limited risk / transparency, under Article 50(1).**

**One-sentence justification:** Whizbiz is a conversational AI system that interacts directly with a
natural person and therefore engages Article 50(1)'s disclosure duty, while every decision it
produces is about a transaction rather than an assessment of a person — which is what keeps it out of
Article 5 and every Annex III category, and out of the Chapter III high-risk regime entirely.

## Where I'm unsure, and what would resolve it

The tier itself I hold with reasonable confidence — the facts are clean (no profiling, no scoring,
no Annex III domain). The genuine uncertainty is at the edges of scope, not the tier:

- **If a future version ever used transaction history to decide whether to accept a customer, offer
  different terms, or flag a customer as a credit risk**, that would move meaningfully closer to
  Annex III(5)(b) territory, even if still short of "significant influence." Nothing in the current
  build does this — it is a scope-creep risk, not a present gap.
- **If the product is ever marketed as producing "tax-authority-compliant" filings** rather than
  "compliance-formatted" records, that is a claim the AI Act doesn't regulate but consumer-protection
  and professional-liability law would — worth a legal read before that language ships externally.

I would use the European Commission's Compliance Checker to cross-check this tier next, per the
lab's instruction to form my own view first — noted as a follow-up rather than done here, since the
lab explicitly asks not to front-load it.
