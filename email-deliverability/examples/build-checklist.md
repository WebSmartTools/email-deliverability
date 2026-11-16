# Build Checklist

Run through this list every time a domain's SPF or DMARC record is built or changed. Tick each item only after a live lookup confirms it.

## Before publishing

- [ ] Every service that sends as the domain is listed: mailbox provider, marketing tool, transactional sender, shop, helpdesk.
- [ ] Each sender has an include from the provider table, or from the provider's own documentation.
- [ ] The SPF lookup total is counted, including nested includes, and is 10 or under.
- [ ] The SPF record ends with `~all` for a new record, or `-all` only when the sender list is certain and the record has run clean.
- [ ] The record does not contain `+all`.
- [ ] The DMARC record starts at `p=none` with a `rua` address set.
- [ ] The DMARC record contains no `pct`, `rf`, or `ri` tags.
- [ ] DKIM selectors are known for every provider that needs one.

## After publishing

- [ ] A live lookup returns exactly one SPF record for the domain.
- [ ] A live lookup returns the DMARC record at `_dmarc.<domain>`.
- [ ] A live lookup returns a DKIM key record for each selector.
- [ ] The SPF lookup total from the live records is 10 or under.
- [ ] The check was repeated after the TTL passed, so the change has spread.

## Before moving the DMARC policy up

- [ ] Aggregate reports have been read for at least two weeks at the current policy.
- [ ] Every legitimate sender passes in the reports.
- [ ] Every failing sender is identified and fixed, not ignored.
- [ ] Only then move `none` to `quarantine`, and later `quarantine` to `reject`.

## Never

- [ ] Never publish a second SPF record. Merge into the one that exists.
- [ ] Never jump straight to `p=reject`.
- [ ] Never trust a pasted record without a live lookup.
- [ ] Never claim a record is safe to enforce until the reports say so.
