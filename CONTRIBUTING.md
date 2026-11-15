# Contributing

Contributions should improve the workflow without weakening validation, privacy, or traceability.

## Before opening a change

1. Explain the user problem or workflow behavior being changed.
2. Use synthetic data and redacted credentials.
3. Describe affected nodes and external services.
4. Add or update documentation for behavior and limitations.
5. Include the verification performed and any remaining gaps.

## Review expectations

- Do not commit credentials, private URLs, real personal data, or live service identifiers.
- Do not silently change the similarity threshold or duplicate-handling policy.
- Do not replace guarded writes with unchecked AI output.
- Keep Atomizer changes separate from FixLoop work.
- Label prototype behavior and production-validated behavior accurately.
