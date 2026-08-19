# System Brief — Whizbiz (Messenger Accountant)

**Author:** Vittal Navale
**System audited:** Whizbiz — a Telegram-based bookkeeping assistant, built as Project 3 (Week 6)

---

**What it does.** Whizbiz is a chat-based back-office assistant for German sole proprietors
(Einzelunternehmer) — home bakers, freelancers, and makers legally required to keep EÜR-compliant
bookkeeping and VAT-correct invoices, who currently do this after hours in notebooks and
spreadsheets. It lives inside Telegram, the app the owner already has open all day, and runs as a
52-node n8n workflow with no standing conversation memory — every message is handled as a
self-contained request.

**Inputs.** Three trigger types: (1) a photographed receipt (image data); (2) a free-text order or
report request (e.g. "invoice Anna, €45, delivery Friday"); (3) a scheduled daily trigger for the
digest. Receipt photos and order text routinely contain **personal data belonging to third
parties who never interact with the bot** — a customer's name and delivery address, captured onto
the income sheet so an invoice can be generated. The bot owner's own Telegram account is the only
first-party personal data the system holds about a user of the product itself.

**What it outputs.** A structured expense-sheet row (vendor, VAT breakdown, category) from receipt
OCR; a generated invoice PDF plus a Calendar event from an order message; a revenue-vs-profit report
on request; and a scheduled daily digest combining business data with an AI-generated encouragement
line and a web-searched news headline. Nothing is a score, ranking, or decision about a person —
every output describes a transaction.

**Who is affected.** Primarily the bot owner (the solopreneur), who reads and acts on every output.
Secondarily, the owner's own customers, whose name and address are recorded on the income sheet
without their own visibility into or relationship with Whizbiz.

**Human review.** Every extraction is echoed back in the same chat before it becomes the system of
record — a receipt is confirmed with a message like "€23.80, REWE, 19% USt, category: Wareneinkauf —
correct?" — and figures land in a sheet the owner reads and controls, not a black box. There is no
dedicated confirm/cancel gate (a build-and-roll-back attempt is documented separately); review
currently happens because the owner is reading the chat, not because a step blocks on it.

**Who built it.** I built it solo, using n8n as the orchestration layer and OpenAI (GPT-4o Vision,
GPT-4o-mini, GPT-4o with web search) as the AI provider, integrated with Telegram, Google
Sheets/Drive/Calendar, and QuickChart.io.

**Who would use it in production.** The pitch describes a monthly subscription per solopreneur — so
the intended production user is any subscribing sole proprietor, not a single client. No production
hosting, release entity, or legal/business structure has been decided yet; it currently runs on the
course's development n8n instance.

*(≈390 words)*
