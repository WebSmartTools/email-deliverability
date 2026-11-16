# Provider Includes

The 11 providers measured against live DNS, with what each include covers and the alignment note for each. Lookup costs are live-measured estimates; a provider can change its own record, and the checker in the premium pack is the authority after a record is published.

## Google Workspace

- Include: `include:_spf.google.com`
- Lookups: 1
- Covers: mail sent from Google Workspace mailboxes and Google's sending servers.
- Alignment: Google Workspace sends with the customer's domain as the return-path when the domain is set up in Workspace, so SPF aligns. DKIM is set up in the Workspace admin console with the selector `google` by default.

## Microsoft 365

- Include: `include:spf.protection.outlook.com`
- Lookups: 1
- Covers: mail sent from Microsoft 365 (Exchange Online) mailboxes.
- Alignment: Microsoft 365 sends with the customer's domain as the return-path when the domain is added to the tenant, so SPF aligns. DKIM uses two selectors, `selector1` and `selector2`, set up in the Microsoft 365 Defender portal.

## SendGrid

- Include: `include:sendgrid.net`
- Lookups: 2
- Covers: transactional and marketing mail sent through SendGrid.
- Alignment: SendGrid's default return-path uses SendGrid's own domain, so SPF does not align unless the domain is authenticated in SendGrid with a custom return-path subdomain. Set up domain authentication in SendGrid and use its DKIM selectors; DKIM then carries DMARC.

## Mailchimp

- Include: `include:servers.mcsv.net`
- Lookups: 1
- Covers: campaign mail sent through Mailchimp.
- Alignment: Mailchimp's default return-path uses Mailchimp's domain, so SPF does not align without domain authentication. Authenticate the domain in Mailchimp and add its DKIM records; DKIM then carries DMARC.

## Mailgun

- Include: `include:mailgun.org`
- Lookups: 5
- Covers: transactional mail sent through Mailgun.
- Alignment: Mailgun's default return-path uses Mailgun's domain, so SPF does not align unless a custom tracking and return-path subdomain is set up. Mailgun's include is the most expensive in this table at 5 lookups, so count the total carefully when Mailgun shares a record with other providers.
- Note: Mailgun documents a dedicated sending subdomain (for example `mg.example.com`) as its normal setup. When the domain uses one, the SPF record usually lives on that subdomain, not on the domain root.

## Amazon SES

- Include: `include:amazonses.com`
- Lookups: 1
- Covers: mail sent through Amazon Simple Email Service.
- Alignment: SES supports a custom MAIL FROM subdomain, which makes SPF align. Without it, SPF does not align and DKIM (Easy DKIM, set up in the SES console) carries DMARC.

## Postmark

- Include: `include:spf.mtasv.net`
- Lookups: 1
- Covers: transactional mail sent through Postmark.
- Alignment: Postmark supports a custom return-path subdomain, which makes SPF align. Postmark also publishes DKIM records for the domain; set them up from the Postmark sender signature page.

## Zoho Mail

- Include: `include:zohomail.com`
- Lookups: 2
- Covers: mail sent from Zoho Mail mailboxes.
- Alignment: Zoho Mail sends with the customer's domain as the return-path when the domain is added to Zoho, so SPF aligns. DKIM uses the selector `zoho` by default, set up in the Zoho Mail admin console.

## HubSpot

- Include: `include:_spf.hubspotemail.net`
- Lookups: 1
- Covers: marketing mail sent through HubSpot.
- Alignment: HubSpot's default return-path uses HubSpot's domain, so SPF does not align without connecting the sending domain in HubSpot. Connect the domain and add HubSpot's DKIM records; DKIM then carries DMARC.

## Shopify

- Include: `include:shops.shopify.com`
- Lookups: 1
- Covers: order, shipping, and account mail sent by Shopify for the store.
- Alignment: Shopify usually needs a sending subdomain for DMARC alignment, because its default return-path uses Shopify's domain. Set up the sender email and domain in Shopify's notification settings and follow its Sender Policy Framework guidance before relying on this include for alignment.

## Brevo

- Include: `include:spf.brevo.com`
- Lookups: 1
- Covers: transactional and marketing mail sent through Brevo (formerly Sendinblue).
- Alignment: Brevo usually needs a sending subdomain for DMARC alignment, because its default return-path uses Brevo's domain. Authenticate the domain in Brevo and add its DKIM records; DKIM then carries DMARC.

## How to Read the Costs

Add the costs of every include in the record, then add 1 for each `a`, `mx`, `ptr`, or `exists` mechanism and 1 for a `redirect`. The total must stay at or under 10. At 8 or 9, warn the user that one more provider may push it over. The checker in the premium pack counts the total from live DNS, including nested includes, so it catches a provider whose own record has grown since this table was written.
