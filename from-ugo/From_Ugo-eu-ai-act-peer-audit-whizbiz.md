# EU AI Act peer audit — Whizbiz: Messenger Accountant

**System audited:** Whizbiz — Messenger Accountant (V1) · **Built by:** Vittal Navale
**Auditor:** Ugo Ahukannah · **Date of audit:** 19 August 2026
**Basis:** Regulation (EU) 2024/1689 as amended by Regulation (EU) 2026/1744 (in force 27 July 2026)

**Materials received:** the project repository
`vitcipher/W6_Project3-Whizbiz-Messenger-Accountant` — pitch assets, planning checklist, build
learnings, and the exported n8n workflow (52 nodes). **A written system brief was not received**;
this audit is built from the repository, which the lab permits as technical documentation. Where the
absence of a brief left something unresolved it is logged in Phase 3 rather than assumed silently.

**Ground rules observed.** I have not seen Vittal's self-audit, his risk-tier classification, his gap
analysis or his compliance memo, and I have not discussed findings with him. Clarifying questions
were logged in writing rather than resolved in conversation.

---

## Phase 1: Read and annotate

What the system does, from the evidence rather than the pitch. A solopreneur — the pitch targets
German *Einzelunternehmer*, home bakers and freelancers — messages a Telegram bot. Three paths run
off one trigger:

| Path | Trigger | What happens |
|---|---|---|
| **Receipt capture** | User sends a photo | Telegram file fetched → **gpt-4o vision** extracts vendor, date, gross, VAT rate, VAT amount, net and category as JSON → image uploaded to **Google Drive** → row appended to a German-format expense sheet (`Datum`, `Lieferant`, `Kategorie`, `Netto-/Brutto-Betrag`, `USt-Betrag`, `Beleg-Link`) |
| **Order / invoice / calendar** | Text message | **gpt-4o-mini** classifies intent into `order_invoice_calendar`, `profit_report` or `unclear` → invoice row appended to the income sheet (`Kunde`, `Addresse`, `Betrag`, `Leistungsdatum`, `Rechnungsnummer`) → invoice document generated and returned → **Google Calendar** event created |
| **Reporting / daily digest** | User asks, or a schedule trigger fires | Income and expense sheets read back → profit report composed → separately, **gpt-4o with web search** produces a motivational line and a real news headline for the daily message |

**Annotations that shaped the audit:**

1. **Three distinct LLM uses, not one.** Vision extraction, intent classification, and open-ended
   generation with live web search. They carry different failure modes and the third is the only one
   that can put unverified external claims in front of the user.
2. **The system holds data about people who never touch it.** `Kunde` and `Addresse` on the income
   sheet are the *owner's customers*. They are not users of Whizbiz and have no relationship with it.
3. **The subject of every decision is a transaction, not a person.** Nothing scores, ranks or
   profiles an individual. This is what settles the risk tier.
4. **It is a product, not a one-off.** The pitch describes a monthly subscription per solopreneur,
   so this is intended for market placement — which makes the provider/deployer split live rather
   than hypothetical.

---

## Phase 2: First-pass classification

| Question | Answer |
|---|---|
| Does this system fall under any prohibited category (Article 5)? | **No.** No social scoring, no biometric categorisation, no emotion inference, no manipulation of behaviour causing harm. Receipt OCR and expense categorisation touch none of Article 5's practices. |
| Does this system operate in any of the eight Annex III areas? | **No.** The nearest candidates fail on their facts: this is not creditworthiness assessment or credit scoring (Annex III 5(b)) — it records income and expenses the owner already incurred and makes no assessment of anyone's ability to pay; it is not employment, education, essential services, law enforcement, migration or justice. |
| If Annex III: does it significantly influence decisions in that area, or is it narrow/preparatory? | **Not applicable** — Annex III is not engaged. |
| Does this system interact with end users or generate content requiring disclosure (Article 50)? | **Yes — this is the tier-setting answer.** It is a conversational agent that a natural person talks to in a messaging app, so **Article 50(1)** applies: the user must be informed they are interacting with an AI system unless it is obvious from context. Product naming ("bot accountant") arguably makes it obvious, but that is an argument rather than a control. The daily digest additionally generates text presented as a real news headline, which raises an accuracy duty rather than an Article 50(4) labelling duty, since it is a private message and not synthetic media. |
| **First-pass risk tier** | **Limited risk / transparency (Article 50)** |
| One-sentence justification | The system is an AI-driven conversational assistant that interacts directly with a natural person, engaging **Article 50(1)**, while making no decision about any person that would bring it within Article 5 or any Annex III area — so its obligations are disclosure obligations, not the Chapter III high-risk regime. |

**Areas of uncertainty.** Two, both logged as questions in Phase 3. First, whether the invoicing path
is ever used to decide whether to *accept* a customer or set their terms — that would move the
analysis toward assessment of a person, though still short of Annex III. Second, whether the product
is ever positioned as producing tax-compliant filings; the pitch says "tax-authority-compliant
expense sheet", and a claim of compliance output is a consumer-protection and professional-liability
exposure even where the AI Act stays silent.

---

## Phase 3: Clarifying questions log

Sent to Vittal as [`exchange-with-vittal-ai-act.md`](./exchange-with-vittal-ai-act.md) on 19 August 2026, before this report was finalised — we work by
document exchange, so the log is the artefact rather than a record of a conversation. **The
provisional assumptions below were deliberately withheld from the version he received**, so they
could not lead his answers. No answers at the time of writing.

**Q1 — Is the bot's AI nature disclosed to the user in-product, or only in the marketing?**
*Why it matters:* Article 50(1) is the only obligation that attaches at this tier, so this single
fact determines whether the system's principal duty is met.
*Provisionally assuming:* no in-product disclosure exists beyond the bot's name.

**Q2 — Who will place Whizbiz on the market, and under whose name?**
*Why it matters:* it decides who is the provider under Article 3(3), and therefore who owes the
Article 50 and Article 4 duties. The pitch describes a subscription product, which implies market
placement rather than a private build.
*Provisionally assuming:* Vittal (or a Whizbiz entity) would be the provider; each subscribing
solopreneur would be the deployer.

**Q3 — Where does the n8n instance run in production, and is it the shared cohort instance?**
*Why it matters:* it is the processing environment for every customer record the system holds, and a
shared teaching instance is not a production environment.
*Provisionally assuming:* currently the bootcamp-hosted n8n instance, with no production hosting
decision taken.

**Q4 — Are the customer name and address fields (`Kunde`, `Addresse`) required, or convenience?**
*Why it matters:* it is the difference between processing third-party personal data because the
invoice needs it and processing it because the sheet has a column for it. It drives minimisation
under GDPR and shapes what the AI Act's Article 4 literacy material must warn a user about.
*Provisionally assuming:* required for a legally valid German invoice, therefore necessary.

**Q5 — Is the web-search-generated news headline in the daily digest shown to the user as fact?**
*Why it matters:* the prompt asks for "one recent, real news headline … and the source URL", which is
a retrieval task presented as a factual claim. Wrong output here is a credibility and accuracy
problem for a product whose whole value proposition is bookkeeping reliability.
*Provisionally assuming:* it is presented as fact, unlabelled and unverified.

---

## Phase 4: Audit report

### Section 1: System summary

Whizbiz is a chat-based bookkeeping assistant for solo business owners, built as a 52-node n8n
workflow around a Telegram bot. A user photographs a receipt and a vision model extracts the vendor,
date, VAT breakdown and category into a German-format expense sheet, with the image filed to Google
Drive. A typed instruction such as "invoice Anna, €45, delivery Friday" is classified by a second
model, written to an income sheet with the customer's name and address, turned into an invoice
document and booked into Google Calendar. The user can ask how the business is doing and receive a
revenue-versus-profit report, and a scheduled job sends a daily message combining that data with an
AI-generated encouragement line and a web-searched industry headline.

### Section 2: Risk classification

**Limited risk / transparency, under Article 50(1).** The system converses with a natural person, so
the disclosure duty applies; nothing it does falls within Article 5 or any Annex III area, because
every output describes a transaction rather than assessing a person. The uncertainty worth stating is
directional rather than doubtful: were the product to extend into deciding which customers to accept
or what terms to offer them, the analysis would need revisiting — and if it ever advises on tax
positions rather than recording figures, the exposure changes even though the tier may not.

### Section 3: Role map

| Role | Entity | Key obligations |
|---|---|---|
| **Provider** | Vittal / Whizbiz, on the stated subscription model — placing the system on the EU market under its own name | **Article 50(1)** disclosure designed into the product; **Article 4** support for user AI literacy, which survives the Digital Omnibus in softened form; accurate product claims. No conformity assessment, CE marking, registration or post-market monitoring — those attach to high-risk systems |
| **Deployer** | Each subscribing solopreneur | **Article 4** literacy in their own use; use within the stated limits. No Article 26 duties and **no FRIA** — Article 27 reaches public bodies, private entities providing public services, and credit or life/health insurance deployers, none of which a home baker is |
| **Vendor — OpenAI** | gpt-4o vision, gpt-4o-mini classification, gpt-4o with web search | **GPAI provider**, Articles 51–56: technical documentation, information to downstream providers, EU copyright compliance, training-data summary; systemic-risk duties if above 10²⁵ FLOPs. These do not transfer to Whizbiz, and do not shield it either |
| **Vendor — Telegram** | Messaging channel and file transport | No AI Act role. It is the transport layer, and an independent actor for the messaging itself |
| **Vendor — Google** | Drive (receipt images), Sheets (books), Calendar (deliveries) | No AI Act role; storage and productivity services |
| **Platform — n8n** | Orchestration host | No AI Act role. Its significance is where it runs, not what it is |

### Section 4: Compliance findings

> **Finding 1 — Article 50(1) disclosure is not evidenced in the product**
> **Severity:** Significant
> **Description:** Article 50(1) requires that a natural person be informed they are interacting with an AI system unless that is obvious from the context. The workflow contains four `Send a text message` nodes and a photo message node; none of the message content in the export states that the counterpart is an AI system. The product name is the only signal, and "obvious from context" is a defence to be argued rather than a control to rely on. This is the principal obligation at this tier, so a gap here is the one finding that goes to the heart of the classification.
> **Recommended action:** add a one-line AI disclosure to the bot's first response in any conversation and to the daily digest, and state it in the onboarding message. This is a text change to existing nodes.
> **Escalation needed?** No.

> **Finding 2 — No AI literacy or limitations material for the user (Article 4)**
> **Severity:** Significant
> **Description:** Article 4 applies to providers and deployers of **all** AI systems at every tier. A user handing over VAT categorisation to a vision model needs to know that extraction can be wrong, that categories are a model's guess, and that the figures require review before they reach a tax filing. Nothing in the repository performs that function: the pitch materials describe capability, and the learnings file is developer-facing.
> **Recommended action:** a short in-product limitations note plus a line in the onboarding flow — what the bot reads, what it can get wrong, and the user's duty to check figures before filing.
> **Escalation needed?** No.

> **Finding 3 — Unverified web-search output presented as fact in the daily digest**
> **Severity:** Significant
> **Description:** The scheduled digest asks a model with web search for "one recent, real news headline … and the source URL". Nothing verifies the headline exists or that the URL supports it, and the user receives it inside the same trusted message as their own financial figures. This is not an Article 50 labelling breach — it is a private message, not synthetic media published to inform the public — but it is an accuracy and credibility risk in a product whose entire proposition is reliability, and a misleading-claims exposure if a fabricated headline is ever attributed to a real outlet.
> **Recommended action:** either drop the news element, or render it as a link-out with the source named and an explicit "AI-selected, unverified" label. Verification of the URL before sending would be better still.
> **Escalation needed?** No — unless the digest is ever monetised as a content feature, which would make it a publishing decision.

> **Finding 4 — Provider status is undecided while the product is described as a subscription**
> **Severity:** Significant
> **Description:** The pitch sets out a per-solopreneur monthly subscription. The moment that ships, someone places an AI system on the EU market under their own name and becomes the provider under Article 3(3), acquiring the Article 50 and Article 4 duties above. Nothing in the repository records who that entity is. This is a paperwork gap now and an accountability gap at launch.
> **Recommended action:** record the release model and the provider entity in the repository before any paying user, and reflect it in the terms the subscriber accepts.
> **Escalation needed?** Yes — a lawyer should confirm the role split at the point of commercialisation.

> **Finding 5 — Third-party personal data is processed with no notice path to those people**
> **Severity:** Significant *(and Blocking under GDPR — see the companion privacy audit)*
> **Description:** The income sheet records `Kunde` and `Addresse` — the owner's customers, who never interact with Whizbiz and have no visibility of it. The AI Act is largely silent here, and I am flagging it because an auditor who confines himself to one regime will hand a client a clean report on the wrong question. Under the AI Act this is only a literacy and transparency matter; under GDPR it is the central issue.
> **Recommended action:** treat the privacy audit as the governing analysis for this data, and make the subscriber-facing material explain the owner's own controller duties toward their customers.
> **Escalation needed?** Yes — DPO or privacy counsel.

> **Finding 6 — Production environment undetermined**
> **Severity:** Minor *(AI Act) — Significant operationally*
> **Description:** The workflow is an export from an n8n instance whose production identity is not recorded. If the shared cohort instance is used with real customer data, the environment is neither controlled nor contractually covered. Under the AI Act this touches nothing at this tier; it is logged because it conditions several answers in the privacy audit.
> **Recommended action:** record the production hosting decision before the first paying user.
> **Escalation needed?** No.

### Section 5: Overall recommendation

**Proceed with conditions.** There are no blocking findings under the AI Act: the system is correctly
outside the high-risk regime, and its tier brings a small, tractable set of duties. The conditions
are that **Article 50(1) disclosure be added in-product before any external user**, that **Article 4
limitations material accompany it**, and that the **provider entity be recorded** before the
subscription launches. The unverified news headline should be labelled or dropped in the same pass.
None of this requires redesign — all four are text and configuration changes on top of a workflow
that is, on the regulatory question that matters, correctly scoped: it automates bookkeeping about
transactions rather than making decisions about people, and that choice is what keeps it out of the
high-risk regime.

I would add one observation a peer audit is well placed to make. The strongest compliance property of
this system is one its documentation never claims: **the human stays in the loop by construction**,
because every output lands in a chat the owner reads and in a sheet the owner owns. Nothing is
decided while they are not looking.

### Section 6: What this report is not

This report is not a legal opinion, not a conformity assessment, and not a certification. It is a
first-pass external review conducted from a repository without a written system brief and without
answers to the questions in Phase 3. Conclusions should be verified with legal counsel before any EU
market placement, and the classification should be revisited if the product's scope changes.

---

## Phase 5: Debrief conversation

_Runs as a single document exchange rather than a meeting — [`exchange-with-vittal-ai-act.md`](./exchange-with-vittal-ai-act.md)
carries the questions out, his tier and findings recorded before he reads this report, his response
after, and the joint closing note. Pending his return of that file._
