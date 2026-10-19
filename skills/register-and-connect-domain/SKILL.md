---
name: register-and-connect-domain
description: Register an internet domain through Fairverra and point it at the current project (Vercel, Netlify, Cloudflare, VPS, or custom DNS). Use when the user wants to buy or register a domain, connect a domain to this project, or set the domain as the project's hostname.
---

# Register a domain and connect it to this project

Use the Fairverra MCP tools from this plugin. Do not invent REST calls when
those tools exist.

## Money and legal

Paid work is two tools: `create_quote` then `confirm_approval`.
Show the human the quote `presentment` (if present) and `total` first.
Call `confirm_approval` only after an explicit yes. Confirm debits `total`
(EUR wallet). Never convert FX yourself.

On production, call `whoami` first. If legal documents are missing, show
https://fairverra.com/legal and call `accept_legal_documents` only after an
explicit yes.

Never print API keys or auth codes.

## If the connector is not signed in

Ask the human to connect the Fairverra MCP server (OAuth: email + one-time
code). New accounts: send them to https://fairverra.com/get-started.
Sandbox only (no real registration): https://sandbox.api.fairverra.com/mcp.

## Register

1. Ask for the domain if missing. One name per `check_domain`.
2. `check_domain`. If taken, stop or offer `/fairverra:transfer-domain`.
3. `get_registration_requirements` for the TLD.
4. `list_handles`. Reuse a `registrar_synced` handle, or `create_handle`.
   NL phone: `area_code` without a leading 0 (6 for mobile).
5. `get_wallet`. If the balance cannot cover the quote, `create_deposit_link`
   and give the human `deposit_url`. Wait until they paid.
6. `create_quote` with `action: register`, the domain and required handles.
7. Show presentment and total. Wait for yes.
8. `confirm_approval`. Report per-domain results. Failures are refunded.

## Connect to this project

After a successful register, or when the domain is already on the account:

1. `list_domains` for `domain_id`.
2. `list_nameserver_groups`. The default group is Fairverra DNS: use
   `add_dns_record`. A custom group you create is delegation; DNS-record
   tools then do not apply.
3. Detect the host from the repo (`vercel.json`, `.vercel`, `netlify.toml`,
   `wrangler.toml`, a `CNAME` file) or ask. Do not hardcode provider IPs;
   read the host's current docs or use values the human gives.
4. Stay on Fairverra DNS when possible: `add_dns_record` for A, AAAA, CNAME,
   TXT (including ACME) or MX. Ask before changing live A or MX.
5. Only `create_nameserver_group` then `set_domain_nameservers` when the
   human wants to delegate (Cloudflare, host nameservers). Confirm first:
   wrong nameservers take the site and mail offline.
6. Reply with the domain, what you set, and that DNS can take minutes.

Do not register a second domain unless asked. Do not enable auto-renew
without asking.
