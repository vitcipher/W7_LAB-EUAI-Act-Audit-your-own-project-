# Role Map — Whizbiz

| Role | Entity | Key AI Act obligations |
|---|---|---|
| **Provider** | Vittal Navale, individually — no separate legal entity formed yet, though the pitch describes market placement as a monthly subscription product | **Article 50(1)** — design the AI-interaction disclosure into the product itself, not just the marketing. **Article 4** — ensure users have a sufficient level of AI literacy to understand what the system does and its limitations (this obligation applies at every risk tier, including minimal/limited risk). Accurate, non-misleading product claims. No conformity assessment, CE marking, registration, or post-market monitoring duties — those attach only to high-risk systems, which Whizbiz is not. |
| **Deployer** | Each subscribing solopreneur, using Whizbiz in a professional context for their own business | **Article 4** literacy in their own use of the tool; using it within its stated scope (bookkeeping records, not tax advice). No Article 26 high-risk deployer duties and no FRIA (Article 27) — that obligation reaches public bodies, private entities providing public services, and credit/insurance-risk deployers, none of which describes a home baker running her own books. |
| **Vendor — OpenAI** | GPT-4o Vision (receipt extraction), GPT-4o-mini (intent classification), GPT-4o with web search (daily digest) | OpenAI is itself a **GPAI (general-purpose AI) provider** under Articles 51–56 — technical documentation, information to downstream integrators, EU copyright-compliance summary, and systemic-risk duties above the FLOPs threshold. These obligations sit with OpenAI, not Whizbiz — but they also don't shield Whizbiz from its own Article 50/Article 4 duties as the system built on top. |
| **Vendor — Telegram** | Messaging/file-transport channel | No AI Act role — pure transport layer. |
| **Vendor — Google (Sheets, Drive, Calendar)** | Bookkeeping storage, receipt archival, delivery scheduling | No AI Act role — standard storage/productivity services, not AI systems in this context. |
| **Platform — n8n** | Orchestration host running all 52 workflow nodes | No AI Act role in itself. Its regulatory relevance is about *where it runs* (a shared course instance vs. a controlled production environment) rather than what it is — this affects data-protection posture, not AI Act classification. |

**Note on confidence:** this is a first-pass map, consistent with the lab's own caveat that role
mapping in a real engagement would need legal confirmation — particularly the provider question,
since no release entity has actually been decided (see Gap 4).
