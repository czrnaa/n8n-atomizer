# Evidence, scope, and limitations

## Evidence reviewed

The local project package contains:

- Two matching n8n workflow JSON exports
- Four PNG screenshots/log captures
- One Atomizer demo video
- One XLSX snapshot of content-planning data
- The n8n buildathon qualifying-round brief
- An Atomizer engineering handoff document
- A non-destructive idea-similarity feature brief

The two workflow JSON files describe the same 43-node workflow and appear to be duplicate exports.

## What is supported by the artifacts

- The workflow contains the required integration categories: HTTP ingestion, AI processing, Google Sheets, Google Calendar, and Gmail.
- The workflow contains explicit validation and guarded-write logic around semantic matching and family creation.
- The workflow includes extraction, clarification, similarity, persistence, scheduling, and digest stages.
- The feature brief defines the intended non-destructive result fields and acceptance checks, including a new family ID, linked suspected family, visible confidence, similarity status, and creator-controlled merge deferral.
- The spreadsheet snapshot contains persisted family/content records and calendar metadata.
- The screenshots and video provide presentation evidence of the workflow and its outputs.

## What is not proven

- A complete end-to-end run of the exact supplied export in the live n8n instance.
- Current credential validity or service availability.
- Production reliability, throughput, or measured time savings.
- Similarity-score accuracy or probability calibration.
- Recovery from a failed write between Sheets, Calendar, and Gmail.
- Safe concurrent family-ID allocation.
- A creator-facing merge or update workflow after similarity is flagged.
