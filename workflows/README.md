# Workflow exports

`atomizer-sanitized.json` is a public-safe n8n export for portfolio review and local reconstruction.

Before importing it into n8n:

1. Replace the example webhook with your own endpoint.
2. Configure Google Gemini credentials.
3. Configure Gmail, Google Sheets, and Google Calendar credentials.
4. Replace the placeholder spreadsheet and calendar references.
5. Review all recipients and write destinations.
6. Test with synthetic data before connecting real creator records.

The export intentionally removes credential bindings, workflow instance identifiers, live service URLs, real email addresses, and pinned runtime data. The original exports remain outside the public repository.
