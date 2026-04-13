# Verifiable Timestamp Format

AI-based transcript summarization and minute writing can drift from the original intent. Include supporting timestamps in every sentence or bullet of the meeting minutes so the content can be verified.

## Basic Rules

- Include at least one timestamp for every sentence or bullet in the meeting minutes.
- Use one primary supporting utterance for each timestamp comment.
- Do not insert arbitrary times.
- Use the original transcript file's `record_start_time` for `@time`.
- Use the speaker at that same point, `participant_name`, for `@participant`.
- `@time` and `@participant` must come from the same speech block.
- If additional utterances support the same sentence or bullet, append them as `@see` entries.
- Use the most reliable supporting utterance as the primary `@time` and `@participant` pair.

## Basic Format

```markdown
<!--@time="08:00",@participant="participant_name"-->
```

- Use an HTML comment.
- Always wrap `@time` and `@participant` values in double quotes.
- Separate the two fields with a comma and no surrounding spaces.

## Format for Additional Supporting Sources

If one sentence or bullet is supported by multiple utterances, keep one primary source and append the remaining timestamps with `@see`.

```markdown
<!--@time="15:02",@participant="participant_name"&@see="12:56"&@see="16:28"&@see="16:37"&@see="16:44"-->
```

- Keep exactly one primary `@time` and `@participant` pair.
- Add every additional supporting timestamp as `@see`.
- Join `@see` entries with `&` and no surrounding spaces.
- Wrap every `@see` value in double quotes.
