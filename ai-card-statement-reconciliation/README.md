# AI Credit Card Statement Reconciliation

> 🇧🇷 [Versão em português abaixo](#-português)

An LLM reads every line of a credit card statement PDF and reconciles it against the payables in the client's ERP, flagging missing, duplicated or mismatched entries. **Read-only by default**: a human reviews the diff report before anything is posted.

```
Upload portal (PDF) ──► Gemini extracts lines (date, description, installments, amount, fees, refunds)
                    ──► ERP API (Conta Azul / Omie, OAuth 2.0) ──► diff report + alerts
```

## Impact

~9 statements/month. **20–60 min → a few minutes of review per statement.**

## Highlights

- Structured extraction with explicit rules for installments, refunds, annual fees and international purchases
- Two ERPs with different APIs behind the same flow
- OAuth 2.0 redirect fix (`06`) for a provider that expects parameters after `#`
- Assisted spreadsheet mode for clients without API access

| File | What it does |
|---|---|
| `01-upload-portal` | Form where the analyst uploads the PDF |
| `02-reconcile-erp-a` | Reconciliation against ERP A |
| `03`/`04` | Reconciliation against ERP B (card and bank statement) |
| `05-assisted-spreadsheet-mode` | Extraction to a spreadsheet when there is no API |
| `06-oauth-redirect-fix` | OAuth redirect helper |

**Stack:** n8n, Gemini, REST APIs, OAuth 2.0, n8n Forms. Client data, IDs and credentials were removed.

---

## 🇧🇷 Português

O LLM lê cada linha do PDF da fatura do cartão e confere com as contas a pagar do ERP (Conta Azul ou Omie), apontando o que falta, o que está duplicado ou diferente. Só leitura por padrão, com revisão humana. ~9 faturas/mês; de 20–60 min para poucos minutos cada. Workflows sanitizados.
