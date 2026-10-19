---
name: transfer-domain
description: Transfer an existing internet domain into Fairverra and optionally point it at the current project. Use when the user wants to move a domain from another registrar, start a transfer, or attach a transferred domain to this project.
---

# Transfer a domain into Fairverra

Use the Fairverra MCP tools from this plugin.

## Money and legal

`create_quote` then `confirm_approval`. Show `presentment` and `total` first.
Call `confirm_approval` only after an explicit yes. Confirm debits `total`.
Never print an auth code.

On production, `whoami` first. Missing legal documents: show
https://fairverra.com/legal, then `accept_legal_documents` after an explicit yes.

## Transfer

1. Ask for the domain and the current registrar's auth/EPP code.
2. `whois_check` with that `auth_code` (syntax only; the registry validates
   at confirm). If locked, tell the human to unlock at the losing registrar.
3. `get_registration_requirements` for the TLD.
4. `list_handles` or `create_handle` for required roles.
5. `get_wallet`. If needed, `create_deposit_link` and wait for payment.
6. `create_quote` with `action: transfer` and
   `domains: [{ domain, auth_code }]`.
7. Show presentment and total. Wait for yes.
8. `confirm_approval`. Transfers can stay pending; say so if the result is
   not yet active.

Then offer `/fairverra:register-and-connect-domain` connect steps (DNS or
nameservers) if the human wants the domain on this project.
