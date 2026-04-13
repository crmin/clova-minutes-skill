---
name: clova-minutes
description: Write and save meeting minutes from Clova Note transcripts and markdown meeting-minute templates. Use for transcript-based meeting note requests.
---

# Clova Minutes

Write and save a meeting-minutes file from a Clova Note transcript and a markdown meeting-minutes template.

## Core Rules

- Resolve the transcript file, template, and output path before writing.
- Do not resolve ambiguous input by guesswork. Present candidates and let the user choose.
- Preserve the markdown structure of the template.
- Do not leave `{placeholder}` tokens in the final output.
- Do not invent facts that are not supported by the transcript.
- Include at least one supporting timestamp in every sentence or bullet of the meeting minutes.
- Write in Korean unless the user explicitly requests another language.

## Inputs

Work from these three inputs:

1. Transcript file
2. Meeting-minutes template
3. Output path (optional)

The request does not need to specify all three items explicitly, but resolve all three before writing.

## Find the Transcript File

Treat the transcript as a Clova Note plain-text file.

### When a transcript path is provided

- If a full path is provided, check that path first.
- If only a filename is provided, search the current directory, `$HOME/Downloads`, and on Windows `$HOME/Documents`.
- If the extension is omitted, check for a matching `.txt` file first.
- If a network URL is provided, obtain it as an accessible local file before processing it.

### When no transcript path is provided

- Check `.txt` files in the current directory.
- If there is exactly one `.txt` file, use it.
- If there are multiple candidates, present them as an ordered list and ask the user to choose by number or text.

### When the transcript path is ambiguous

Ask the user to choose when:

- Multiple files have the same or similar names.
- The user provides only part of a filename and the exact target cannot be identified.
- Both local-file and URL candidates exist and the intended source is unclear.

When presenting candidates, include both filename and path for each item.

## Find the Meeting-Minutes Template

Treat the template as a markdown file.

### When a template path is provided

- If a full path is provided, check that file.
- If only a filename is provided, search the current directory and `$HOME/.scribe`.
- If the extension is omitted, check for a matching `.md` file first.

### When no template path is provided

- List the templates under `$HOME/.scribe`.
- If there is exactly one template, use it.
- If there are multiple templates, show the list and descriptions and ask the user to choose.

### Template interpretation rules

- The template may contain markdown structures such as headings, lists, and tables.
- The template may contain placeholders in the form `{placeholder}`.
- Placeholder names may vary by template, so read the full template first and identify the values that must be filled.

## Resolve the Output Path

Interpret the output path using these rules:

- If no output path is provided, save to the current directory using the default filename.
- If the output path already exists and is a directory, save under that directory using the default filename.
- If the output path already exists and is a file, stop before writing and explain the error.
- If the output path does not exist and ends with a file extension, save to that exact file path. Create parent directories as needed.
- If the output path does not exist and does not end with a file extension, treat it as a directory, create it, and save the default filename inside it.
- If the output path is ambiguous, present the possible interpretations as an ordered list and ask the user to choose.

Use the default filename format `회의록_{meeting_date}_{source_transcript_filename}.md`.

- Use the date extracted from transcript metadata `record_date`, normalized as `YYYY-MM-DD`, for `meeting_date`.
- Use the original transcript filename without its extension for `source_transcript_filename`.

## Clova Note Transcript Format

- Read `references/clova-note-format.md` for the detailed structure and examples.
- Parse metadata, speech blocks, and footer separately.
- `record_content` may span multiple lines, so keep it in one block until the next speech header appears.
- Do not treat footers such as `clovanote.naver.com` as transcript content.

## Write the Meeting Minutes

### 1. Read the template first

- Identify the sections and placeholders first.
- Separate values that can be filled directly from metadata from values that require transcript-based summarization.

### 2. Structure the transcript content

Extract at least the following information:

- Meeting title
- Meeting date and time
- Participants
- Main agenda items
- Key discussion points
- Decisions made
- Follow-up action items
- Items requiring confirmation

Do not invent content that is not grounded in the transcript.

### 3. Write in a verifiable form

- Include at least one timestamp for every sentence or bullet in the meeting minutes.
- Use the supporting transcript utterance's `record_start_time` and `participant_name` for each timestamp.
- If a sentence or bullet is supported by multiple utterances, record one primary supporting timestamp and append the remaining references as `@see` entries.
- Follow the timestamp comment format and syntax in `references/verifiable-timestamps.md`.

### 4. Replace placeholders

- Replace each placeholder with an actual value.
- Do not leave raw `{placeholder}` text even when a section has no content.
- If a section should remain empty, clean it up naturally while preserving the template structure.

### 5. Preserve the markdown structure

- Do not arbitrarily change heading levels, list structure, or table structure.
- Prefer the format required by the template.
- Add new sections only when they are strictly necessary.

## Handle Ambiguous Input

When user confirmation is needed, present candidates as an ordered list.

Example:

1. `./infrastructure-study-kickoff-meeting.txt`
2. `$HOME/Downloads/infrastructure-study-kickoff-meeting.txt`

Ask the user to reply with either a number or text.

## Request Interpretation Examples

- Read `references/request-examples.md` when request-interpretation examples are needed.
- If the target cannot be resolved to a single candidate, do not proceed automatically. Ask the user to choose.
