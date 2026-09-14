# Legal rewrite: supporting research

Source review dated 15 September 2026. This is background evidence, not an
action list or a legal opinion. Current remaining work is in
[review-notes.md](review-notes.md).

## Implementation evidence

Paths are relative to this repository. This was a source review, not a
production configuration audit or a live test using customer information.

| Source | Finding |
|---|---|
| `../evercom-landing/src/legalDocuments.ts` | Website's current embedded legal wording; not changed in this pass. Separate from the public Markdown files in this repository. |
| `../evercom/apps/backend/internal/workflow/ai_openai_contract.go` | Answer/search request builders append current message, history and knowledge content. |
| `../evercom/apps/backend/internal/workflow/ai_history.go` | History uses generic role labels but retains message text; this is not content anonymisation. |
| `../evercom/apps/backend/internal/workflow/ai_openai_transport.go` | Sends request JSON to configured chat-completions endpoint; also records request/response through the trace hook. Trace persistence/retention needs its own audit. |
| `../evercom/apps/backend/internal/assistant/runtime_openai.go` | Playground forwards user-message and knowledge content to an OpenAI-compatible endpoint. |
| `../evercom/apps/backend/internal/auth/repository.go` | Account/workspace deletion paths set `deleted_at`; this does not establish erasure of personal data. |
| `../evercom/apps/backend/internal/workspace/repository.go` | Additional workspace deletion path also performs soft deletion. |
| `../evercom-landing/server/booking.go` | Stores name, email, optional company/context and appointment information; successful daily cleanup removes bookings whose scheduled end has passed. |
| `../evercom-landing/server/telegram.go` | Sends booking details and status to Telegram; owner is instructed to email the visitor manually. |
| `../evercom/apps/backend/internal/observability/sentry.go` | Monitoring integration exists. Actual production enablement and provider data scope remain unverified. |

## Sources checked

- [Postmypost's own website](https://postmypost.ru/twitter/) displays BIN 260140021721, matching the number supplied by the operator. This is corroboration, not a certified registry extract. Public English renderings vary between LLC and LLP; the draft retains the operator-supplied name and exact BIN rather than asserting a certified English legal translation.
- [Kazakhstan: On Personal Data and their Protection, Articles 12 and 16](https://www.adilet.zan.kz/eng/docs/Z1300000094): domestic storage and cross-border processing. Search excerpts were retrievable; direct page fetches timed out. The [Russian text](https://www.adilet.zan.kz/rus/docs/Z1300000094) search excerpt flagged a 2026 amendment; its present effect needs verification, not assumption.
- [Kazakhstan government explanation of personal-data protection](https://www.gov.kz/memleket/entities/zhetysu-eskeldy-kokzhazyk/press/article/details/218955): reiterates domestic database storage. The existence of a cross-border transfer rule does not by itself establish an exception to domestic storage. Do not advise that user consent, German hosting, a Kazakhstan backup alone or excluding local customers is a verified solution for this deployment. Ask local counsel what data and arrangements the current rules cover.
- [Kazakhstan: On Protection of Consumer Rights, Article 26](https://adilet.zan.kz/eng/docs/Z100000274_): trader identity/address and related disclosures.
- [ICO: What privacy information should we provide?](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/individual-rights/the-right-to-be-informed/what-privacy-information-should-we-provide/): disclosure checklist for processing within UK GDPR scope. The ICO flags this guidance as under review following the Data (Use and Access) Act.
- [ICO: Contracts and liabilities between controllers and processors](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/accountability-and-governance/contracts-and-liabilities-between-controllers-and-processors-multi/): processing agreements, instructions, confidentiality, assistance and end-of-contract obligations where applicable. Guidance is also flagged as under review.
- [Your Europe: B2C distance selling](https://europa.eu/youreurope/business/selling-in-eu/selling-goods-services/ecommerce-distance-selling/index_en.htm): consumer pre-contract information and cancellation requirements. These must be assessed separately from a voluntary first-payment guarantee.
- [Lemon Squeezy: Payments](https://docs.lemonsqueezy.com/help/payments): provider name and merchant-of-record role; [refund documentation](https://docs.lemonsqueezy.com/help/payments/refunds-chargebacks) allows seller policies while reserving additional refund discretion. [Customer portal documentation](https://docs.lemonsqueezy.com/help/online-store/customer-portal) describes subscription management capabilities; verify Evercom's actual customer route before promising it.
- [Lemon Squeezy: Privacy Policy](https://www.lemonsqueezy.com/privacy): its processing purposes, roles and international processing; these are provider statements, not an audit of Evercom's integration.
