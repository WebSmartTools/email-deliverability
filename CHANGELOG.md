# Changelog

## v1.0.1 - 2026-11-16

- `check.py`: `--wait <seconds>` and `--retries <n>` flags that re-check DNS when a record is missing, so a record published moments ago does not false-fail; the report says when a record appears on a retry.
- `check.py`: DKIM key-strength check, parsed from the `p=` tag; warns when the key is under 2048 bits (1024-bit keys are being phased out).
- `check.py`: DKIM `d=` tag check; warns when the key record's domain does not match the checked domain.
- `check.py`: `rua` and `ruf` addresses are now validated as `mailto:` URIs, not just checked for the `mailto:` prefix.
- Premium: Google Postmaster Tools guide (`google-postmaster-guide.md`), setup plus what to watch (domain reputation, spam rate, feedback loop).
- Skill: a bulk sender rules section (the 2024 Gmail/Yahoo rules: one-click unsubscribe, spam rate under 0.3%), with the honest limit stated plainly: the script cannot verify message headers or complaint rates from DNS; those are checked from a sent message and from Postmaster Tools.
- Deliberately not added: a BIMI kit. BIMI needs a Verified Mark Certificate, which costs far more than the skill; a logo SVG template alone would mislead buyers into thinking BIMI is just a logo file. The skill carries a one-paragraph BIMI note stating the certificate requirement instead.

## v1.0.0 - 2026-11-16

First release.

- Free skill: the email-deliverability skill for Claude Code, with the hard rules (live DNS only, the 10-lookup limit, alignment, the none to quarantine to reject rollout, never `+all`, never the retired tags `pct`, `rf`, `ri`), the 11 measured provider includes with their lookup costs, how to build SPF and DMARC records, a worked example, and a troubleshooting table. Includes the provider reference (`references/provider-includes.md`), install steps for Claude Code, Codex, Cursor, and Claude.ai, the worked example records, and a build checklist.
- Premium pack: the free skill plus the live-check script (`check.py`, DNS-over-HTTPS, standard library only), record templates for all 11 providers (`references/record-templates.md`), and the DMARC enforcement rollout checklist (`dmarc-rollout-checklist.md`).
- Price: $15, one-time payment, single-user licence.
