# Security

The public version of Atomizer must use sanitized workflow exports and synthetic data.

## Never commit

- API keys, OAuth tokens, passwords, private keys, or n8n credential exports
- Live webhook URLs
- Google Sheet, Calendar, or Drive identifiers that expose private resources
- Email addresses, inbox contents, or creator records
- Calendar event links or private screenshots

## Reporting a concern

For a private repository, report suspected exposure directly to the repository owner through the project’s approved private channel. Do not open a public issue containing the secret or sensitive data.

## If exposure is suspected

Revoke or rotate the affected credential at the provider, remove the value from the working tree and Git history, and review access logs. Removing a value from the latest file alone is not sufficient if it was previously committed.
