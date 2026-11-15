# Workflow reference

## Node groups

### Input and control

- `When clicking ‘Execute workflow’`: manual entry point in the supplied export
- `Raw Notes`: retrieves the incoming submission payload
- `Split Out`: expands the submissions array
- `Limit`: controls the number of items entering the loop
- `Loop Over Items`: processes submissions one at a time

### Planning and clarification

- `Plan Input`: prepares the note and any clarification state
- `Information Extractor`: extracts a structured plan with Gemini
- `Map Plan`: normalizes the extracted result
- `Needs User Input?`: routes either to clarification or similarity analysis
- `Ask Creator`: sends a clarification request through Gmail
- `Read Reply`: normalizes the creator response

### Similarity and family management

- `Lookup Existing Families`: reads existing family records
- `Group Existing Families`: groups stored rows by family ID
- `Prepare Incoming Idea`: builds comparison fields from the new plan
- `Combine Similarity Inputs`: joins the incoming idea and existing families
- `Evaluate Idea Similarity`: validates the comparison input and creator scope
- `Prepare Similarity Candidates`: calculates supporting keyword-overlap scores
- `Gemini Semantic Similarity`: evaluates conceptual similarity
- `Structured Output Parser`: constrains the model response shape
- `Validate Semantic Matches`: rejects unknown IDs, invalid scores, duplicate IDs, missing reasons, or insufficient suggested angles
- `Determine Family Decision`: applies duplicate and similarity rules
- `Assign New Family ID`: proposes the next family identifier
- `Allow New Family Creation`: gates persistence
- `Prepare Family Record`: validates the record before writing
- `Check Existing Records Before Write`: re-reads the target store
- `Validate Pre-Write Uniqueness`: blocks ID and submission collisions
- `Authorize Family Write`: gates the final write
- `Finalize Sheet Columns`: prepares the stored columns
- `Record Write Rejection`: records a blocked write
- `Persist New Family to Similarity Dev`: appends the family record to the configured similarity sheet

### Scheduling and delivery

- `Restore Content Plan`: combines the persisted family record with the original plan
- `Build Pieces`: creates the production pieces and deterministic dates
- `Create an event`: creates a Calendar production event
- `Row For Sheet`: verifies event count and event title before mapping the row
- `Save to Sheet`: writes the content-piece record
- `Pass Rows`: returns saved rows to the loop
- `Build Digest`: creates the email digest body
- `Send a message`: sends the digest
- `Similarity Done`: terminal no-op node

## Data concepts

### Submission

The incoming creator note and its identity fields, including submission ID and creator identity.

### Content plan

The extracted anchor title, core angle, platform, format, audience, theme, priority, next action, and clarification state.

### Content family

A group of related content ideas represented by a stable family identifier such as `FAM-0001`.

### Content piece

A platform-specific deliverable derived from a family plan, with production metadata and scheduling fields.

### Similarity decision

A validated relationship containing the closest family, semantic score, explanation, suggested differentiated angles, and the resulting decision.

## Current decision rules

- Compare only against families belonging to the same creator.
- Treat missing identity or invalid model output as a manual-review condition.
- Treat a score of `0.80` or higher as similar.
- Preserve the new idea as a new family proposal instead of overwriting an existing family.
- Block duplicate family IDs and repeated creator submissions before writing.
- Require at least two suggested angles from the similarity evaluator.

## Similarity acceptance checks

A representative similar-idea test should demonstrate that:

- a new `family_id` is created;
- the suspected match is stored in `similar_family_id`;
- `match_confidence` is visible;
- `similarity_status` indicates that similarity was flagged;
- the original family content and schedule remain unchanged;
- new angle suggestions belong only to the new family; and
- the workflow does not auto-merge the two families.

## Important implementation caveats

These are documented as engineering limitations, not hidden from the portfolio audience:

- The supplied export is inactive and starts with a manual trigger.
- The clarification path has a known input-handoff issue that requires testing and repair before production claims.
- Gmail destinations are configured as fixed recipients rather than being derived from each creator record.
- Publish-day reminders are stored as metadata; the current workflow creates production events rather than a separate publish event.
- Partial-write recovery and concurrent family-ID allocation are not demonstrated.
- The similarity score is an estimate, not a calibrated probability.
