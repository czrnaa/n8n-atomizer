# Public repository checklist

Complete this checklist before changing repository visibility from private to public.

The repository keeps raw evidence under `private/`. That directory is ignored by Git and should remain local. Only sanitized, manually reviewed copies belong under `assets/`.

## Remove or sanitize

- [ ] Real webhook URLs
- [ ] Google spreadsheet IDs and links
- [ ] Google Calendar IDs and event links
- [ ] Email addresses and creator records
- [ ] Credential names or credential IDs that reveal operational setup
- [ ] Raw spreadsheet snapshots containing personal or business data
- [ ] Private screenshots or video frames containing inboxes, URLs, names, IDs, or tokens
- [ ] n8n exports containing live endpoints or environment-specific identifiers

## Replace with safe examples

- [ ] Placeholder URLs such as `https://example.invalid/webhook/creator-notes`
- [ ] Placeholder spreadsheet and calendar references
- [ ] Synthetic sample submissions
- [ ] Redacted screenshots or diagrams
- [ ] A sanitized workflow export with credentials removed

## Repository quality

- [ ] Add a license
- [ ] Add a short project description and topics
- [ ] Add a sanitized import/setup guide
- [ ] Document the required n8n and community-node versions
- [ ] Add a sample payload
- [ ] Add a sample output
- [ ] Add a troubleshooting section
- [ ] Add a changelog or version history
- [ ] Confirm the README does not claim unverified production behavior

## Final safety checks

- [ ] Run a secret scanner over the complete repository
- [ ] Search for `http`, `@`, `calendar`, `spreadsheet`, `credential`, `token`, and `key`
- [ ] Inspect Git history, not only the current working tree
- [ ] Confirm ignored files are not already tracked
- [ ] Review all media manually before publication
