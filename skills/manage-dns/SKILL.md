---
name: manage-dns
description: Manage Fairverra DNS records, nameservers and DNSSEC for a domain on the account. Use when the user wants to add or change A, AAAA, CNAME, MX, TXT, SRV or CAA records, point nameservers at a host, set glue, or enable or disable DNSSEC.
---

# Manage DNS, nameservers and DNSSEC

Use the Fairverra MCP tools from this plugin.

## Before you write

`list_domains` and `list_nameserver_groups`.

- Default / Fairverra DNS group: `list_dns_records`, `add_dns_record`,
  `update_dns_record`, `delete_dns_record` apply.
- A custom nameserver group: the platform does not serve the zone.
  Change records at that DNS host, not here.

Show the change. Ask before you edit or delete a live A, AAAA, MX or
nameserver set. Wrong values take the site or mail offline.

Never print API keys.

## Records

`add_dns_record` / `update_dns_record` / `delete_dns_record` match on
type, name and value. Types: A, AAAA, CNAME, MX, TXT, SRV, CAA.
Do not invent provider IPs; read current host docs or use values the
human gives. ACME: TXT on `_acme-challenge`.

## Nameservers

To delegate: `create_nameserver_group` (2-4 hostnames; `{hostname, ip, ip6}`
for in-bailiwick glue) then `set_domain_nameservers`. Confirm first.

## DNSSEC

`get_dnssec`. `set_dnssec` takes DNSKEYs, not DS digests. `disable_dnssec`
removes protection. Confirm both writes.

Reply with what changed and that DNS can take minutes.
