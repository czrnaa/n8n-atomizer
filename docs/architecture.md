# Architecture and design

## Problem

Creator ideas arrive as loosely formatted notes. A useful system must extract a consistent plan, recognize repeated or closely related ideas, preserve meaningful differences, and move approved work into a production schedule.

## System boundary

Atomizer covers the creator-note-to-content-planning workflow described here. FixLoop is out of scope and is not part of this architecture, evidence set, or repository documentation.

## Main stages

### 1. Ingestion

The `Raw Notes` HTTP Request node reads a payload containing submissions. `Split Out` converts the batch into individual items for processing.

### 2. Duplicate filtering

Existing content-log rows are read before processing. `Filter New Notes` checks submission identity and creator identity to avoid processing the same submission repeatedly.

### 3. Plan extraction

The workflow passes the note through an information-extraction chain backed by Google Gemini. The resulting plan includes fields such as an anchor title, core angle, format, audience, platform, priority, next action, and clarification state.

### 4. Human clarification

If the plan needs clarification, the workflow sends a Gmail message and reads the reply before returning to the planning stage. The configured planning logic supports capped clarification rounds.

### 5. Similarity analysis

The workflow reads existing families from Sheets and first prepares candidate comparisons using token overlap. Gemini then evaluates conceptual similarity using the core idea, audience, purpose, and angle. The AI response is constrained by a structured output schema and validated before it can affect persistence.

### 6. Non-destructive family decision

The decision logic uses a semantic similarity threshold of `0.80`. A high-scoring related idea is marked as similar, linked to the closest family, and proposed as a new family. It is not written over an existing family.

The workflow also validates family identifiers, required fields, duplicate submissions, family-ID collisions, and self-references before writing.

The result is inspectable through `similar_family_id`, `match_confidence`, `similarity_status`, `decision`, and `angle_update`. New angle suggestions apply to the new family only. A later creator-controlled merge or update is intended behavior, but no merge workflow is implemented in the supplied export.

### 7. Scheduling and logging

The workflow creates production events in Google Calendar, verifies the returned event identity, and writes content-piece rows to Google Sheets with the calendar event ID and link.

### 8. Digest delivery

The workflow builds an HTML digest and sends it through Gmail after the loop completes.

## Design principles

- Preserve distinct ideas instead of auto-merging them.
- Use AI for interpretation, not unchecked writes.
- Validate model output before persistence.
- Keep family identity and content-piece identity separate.
- Make scheduling and logging traceable through returned event identifiers.
- Keep a human decision point for unclear input.

## External services

The workflow is configured around:

- n8n as the orchestration layer
- Google Gemini for extraction and semantic comparison
- Google Sheets for family and content-log persistence
- Google Calendar for production scheduling
- Gmail for clarification and digest delivery

The public repository should document these integrations without including real endpoints, IDs, email addresses, or credential names.
