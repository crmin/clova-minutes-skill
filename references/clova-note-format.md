# Clova Note Transcript Format

Transcript files usually have this structure:

1. metadata
2. two blank lines
3. record contents
4. two blank lines
5. footer(optional)

## metadata

Read the following values from the top of the file:

- `title`
- `record_date`
- `record_duration`
- `participants`

Example:

```text
{title}
{record_date} ・ {record_duration}
{participants}
```

## record contents

Each speech block usually has this structure:

```text
{participant_name} {record_start_time}
{record_content}
```

- Assume speech blocks are separated by a single blank line.
- Split the speech header into speaker name and start time.
- `record_content` may span multiple lines.

## footer

- The footer is usually `clovanote.naver.com`.
- The footer is a marker from the transcription tool and is not part of the transcript content.
- The footer may be missing depending on user preprocessing.
