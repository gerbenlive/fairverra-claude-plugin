# Fairverra

Register a domain from Claude Code or Cursor and point it at the project you have open.

Ask Claude to register a name and connect it. The plugin opens the Fairverra
connector, checks availability, shows the priced quote, and only confirms after
you approve. It then sets DNS records or nameservers so the domain reaches your
host: Vercel, a VPS, Cloudflare, or records you give.

## Use it

After install, ask: "Register example.com and point it at this Vercel project."
Or run `/fairverra:register-and-connect-domain`. Transfer and DNS skills are
`/fairverra:transfer-domain` and `/fairverra:manage-dns`.

## Data

The plugin stores nothing on your machine. It talks only to the Fairverra
MCP server at https://api.fairverra.com/mcp. That server receives the
domain name, contact fields (name, address, phone, email), wallet and
quote actions, and DNS or nameserver changes you approve. You sign in
with email and a one-time code (OAuth). Paid confirms debit the prepaid
EUR wallet. Fairverra keeps account data under the privacy policy at
https://fairverra.com/privacy. Terms: https://fairverra.com/terms.
Legal index: https://fairverra.com/legal. Support: info@fairverra.com
or https://fairverra.com/docs. The plugin does not send data anywhere
else and does not collect conversation text.

## Install

Once listed, add Fairverra from Plugins in Claude or from the Cursor Marketplace.

From this plugin repository:

```
claude --plugin-dir .
```

From the Fairverra portal checkout:

```
claude --plugin-dir ./plugins/fairverra
```

New account: https://fairverra.com/get-started. Sandbox (no real
registration): https://sandbox.api.fairverra.com/mcp as a custom
connector.
