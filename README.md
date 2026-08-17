# n8n-enterprise-ai-agents

n8n workflow JSONs for finance, GTM, and loan origination AI agents, with per-agent design docs.

![Type](https://img.shields.io/badge/type-n8n%20workflows-orange?style=flat-square)
![Workflows](https://img.shields.io/badge/workflows-9-informational?style=flat-square)
![Last Commit](https://img.shields.io/github/last-commit/vinaygangidi/n8n-enterprise-ai-agents?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)

## What This Does

Nine exported n8n workflow definitions covering finance operations, go-to-market analysis,
and loan origination, plus seven detailed design documents explaining how the larger ones
work.

These are JSON exports, not running services. Import them into an n8n instance and
reconnect credentials to use them.

## How It Works

Each workflow follows a similar shape: a trigger, document or record retrieval, an
extraction step, an LLM-backed agent node, and output shaping in JavaScript.

### Finance — `agents/finance/`

| Workflow | Nodes | Purpose |
|---|---|---|
| `cash_reconciliation_agent.json` | 9 | Match transactions across sources |
| `tax_agent.json` | 10 | OCR plus expense categorization |
| `erp_copilot_agent.json` | 5 | Conversational customer intelligence |
| `erp_customer_orders_agent.json` | 6 | Batch order and revenue pattern analysis |

### Go-to-Market — `agents/gtm/`

| Workflow | Nodes | Purpose |
|---|---|---|
| `gtm-account-360-copilot.json` | 14 | Unified account view with health and risk signals |
| `gtm-win-loss-analysis.json` | 10 | Patterns across closed deals |
| `gtm-icp-segmentation-analysis.json` | 10 | ICP derived from closed-won data |

### Loan Origination — `agents/loan-origination/`

| Workflow | Nodes | Purpose |
|---|---|---|
| `loan_underwriting_agent.json` | 13 | Application analysis against policy criteria |
| `loan_fraud_detection_agent.json` | 12 | Pattern detection on application data |

### Design documents — `docs/`

Seven walkthroughs cover node-by-node logic for the four finance workflows and the three GTM
workflows: `CashReconciliation_DETAILED.md`, `Tax_Agent_DETAILED.md`,
`ERP_Copilot_Agent_DETAILED.md`, `ERP_Customer_Orders_Tool_DETAILED.md`, and one per GTM
workflow. The two loan-origination workflows have no design document.

## Quickstart

1. Open your n8n instance (Cloud or self-hosted).
2. Choose **Workflows → Import from File** and select a JSON file from `agents/`.
3. Reconnect credentials on every node that needs them. Depending on the workflow this
   includes OpenAI, Anthropic, Mistral AI, Microsoft OneDrive, Microsoft Excel, and any CRM
   or ERP connector the workflow references.
4. Update file paths, folder IDs, and record references to point at your own data.
5. Read the matching document in `docs/` before running — several workflows expect a specific
   input file layout.

## Configuration

Credentials live in n8n's credential store, not in these files. No environment variables are
involved.

| Credential type | Used by | Purpose |
|---|---|---|
| OpenAI API key | Most workflows | Agent reasoning |
| Mistral AI API key | Workflows with OCR steps | Document text extraction |
| Microsoft OneDrive OAuth2 | Document-driven workflows | Source file retrieval |
| Microsoft Excel OAuth2 | Finance workflows | Tabular input |

Trigger types, folder paths, and record identifiers are embedded in each workflow's nodes and
must be edited after import.

## Limitations

- **Not runnable as-is.** These are workflow exports. Without an n8n instance and reconnected
  credentials they do nothing.
- **Nine workflows, not "21+".** An earlier version of this README claimed 21+ agents with 9
  live and 12 "in development (Q2 2026)". Only the 9 exist; the other 12 were never built and
  are not represented by any file here.
- **Previously published ROI and accuracy figures were not measured.** Earlier revisions
  quoted per-agent annual savings ($46,720 for GTM, $84,960 for Finance), time-saved
  percentages (97%, 95%, 88%), and a "96-99% auto-match" rate for cash reconciliation. None
  came from instrumented runs on real data; they were illustrative estimates and have been
  removed rather than restated.
- **"Production" status was aspirational.** Workflows previously marked ✅ Production are
  exports from a personal n8n workspace, not systems running under an SLA in a company
  environment.
- **Credentials are stripped from exports.** Node credential references point at IDs from the
  original workspace and will not resolve elsewhere.
- **Paths and record IDs are hardcoded** to the original author's storage and will fail until
  edited.
- **No error handling.** No error branches, retries, or failure notifications in any workflow.
- **No n8n version pinned.** Node parameters shift between n8n releases; imports into a much
  newer instance may need adjustment.
- **Financial and lending output is unverified model output.** Reconciliation matching,
  underwriting analysis, and fraud signals are produced by an LLM with no deterministic
  verification step. Loan underwriting and fraud detection are regulated decisions — these
  workflows are not suitable for adverse-action determinations without a documented,
  auditable rules layer and human review.
- **Document contents go to third parties.** Files processed by these workflows are sent to
  OpenAI, Anthropic, or Mistral. Do not run them against confidential financial, customer, or
  applicant data without checking your agreements.
- **The two loan-origination workflows are undocumented.** No design document explains their
  node logic or expected inputs.
- **`LICENSE` was missing** despite the README asserting MIT. Added.

## License

MIT — see [LICENSE](LICENSE).
