# Gap Analysis and Remediation — Whizbiz

Whizbiz is not high-risk, so the Phase 4 obligation checklist (Articles 9–72) is skipped per the lab
instructions. What follows covers the transparency gap under Article 50, the Article 4 literacy gap
that applies regardless of tier, and the parallel legal issues (GDPR, consumer protection) that sit
outside the AI Act but are material to a real launch.

---

### Gap 1
**Obligation:** Article 50(1) — inform a natural person they are interacting with an AI system,
unless obvious from context.
**Current state:** None of the bot's message nodes state that the counterpart is an AI system. The
only signal is the product name ("bot accountant"), which is an argument for obviousness rather than
a designed control.
**Required state:** An explicit, low-friction disclosure — in the `/start` reply, the first message
of any new conversation, or a persistent footer — that the user is talking to an AI system.
**Remediation:** Add one line to the onboarding message and to the first response in a session. This
is a text change to existing n8n message nodes, not a redesign.
**Escalation needed?** No.

---

### Gap 2
**Obligation:** Article 4 — AI literacy, applicable to providers and deployers at every risk tier.
**Current state:** No in-product material explains that vision-based extraction can misread a
receipt, that category assignment is a model's inference rather than a certainty, or that the user
is responsible for checking figures before they're used in a tax filing. The confirm-style message
("€23.80, REWE, 19% USt, category: Wareneinkauf — correct?") is a genuine, working review point, but
it's a UX pattern, not a stated policy the user has been told to rely on.
**Required state:** A short, plain-language limitations note delivered during onboarding — what the
bot reads, where it can go wrong, and the user's duty to check figures before filing.
**Remediation:** One onboarding message plus a `/help` or `/about` command that restates it. Low
effort, meaningfully closes a real gap.
**Escalation needed?** No.

---

### Gap 3
**Obligation:** Not an AI Act obligation directly — an accuracy/credibility risk with consumer-facing
implications.
**Current state:** The daily digest's prompt asks GPT-4o with web search for "one recent, real news
headline … and the source URL." There is no step in the workflow that verifies the headline exists or
that the URL supports it before sending, and it arrives in the same trusted message as the user's own
financial figures.
**Required state:** Either the headline is dropped, or it is clearly labelled as AI-selected and
unverified, ideally with the source link rendered so the user can check it themselves.
**Remediation:** Add a labelling string to the digest-composition step, or add a verification call
before the message sends. The labelling fix is trivial; verification is a small additional node.
**Escalation needed?** No, unless the digest is later monetised as an editorial/content feature, which
would change its character.

---

### Gap 4
**Obligation:** Article 3(3) — provider status attaches to whoever places the system on the EU market
under their own name.
**Current state:** The pitch describes a per-solopreneur monthly subscription, which is a market-
placement plan, but no repository artefact records who the provider entity actually is — me
individually, or a company yet to be formed.
**Required state:** A recorded decision on the release model and the provider entity, reflected in
whatever terms a subscriber accepts.
**Remediation:** Document the intended release structure now, before any paying user, even if the
near-term answer is "individual, pending incorporation."
**Escalation needed?** Yes — a lawyer should confirm the role split at the point of commercialisation.

---

### Gap 5
**Obligation:** Not an AI Act obligation — a GDPR issue, flagged here because an AI Act-only audit
would otherwise miss it.
**Current state:** The income sheet stores the owner's customers' name and address (`Kunde`,
`Addresse`) — third parties who never interact with Whizbiz and have no visibility into it. This data
is required for a legally valid German invoice, not incidental convenience, which narrows the
minimisation question but doesn't remove the controller-duty question of how those individuals are
informed.
**Required state:** The owner's own controller obligations toward their customers need to be
addressed — this is the governing analysis for this specific data, not the AI Act.
**Remediation:** This is already the subject of a dedicated companion GDPR audit
(`W7_LAB-Same-product-privacy-lens/GDPR-Audit-Pack-VittalNavale.md` in a separate repo for that lab) —
referenced here rather than re-litigated, per the lab's own instruction to note parallel legal issues
without re-doing a different lab's work.
**Escalation needed?** Yes — DPO or privacy counsel, tracked in the GDPR audit.

---

### Gap 6
**Obligation:** Not an AI Act obligation — an operational/data-governance note.
**Current state:** The exported workflow doesn't record which n8n instance is intended for
production. If a real subscriber's data ever runs through the shared course instance, that
environment is neither controlled nor contractually covered for that purpose.
**Required state:** A recorded production-hosting decision before the first paying user.
**Remediation:** Decide and document hosting (self-hosted n8n, n8n Cloud, or similar) before launch.
**Escalation needed?** No — an engineering decision, not a legal one.
