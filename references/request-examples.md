# Request Interpretation Example

You may receive a request like this:

```text
The infrastructure study kickoff meeting file is in the Downloads directory. Write the minutes using the meeting-minutes template.
```

Interpret it like this:

- Transcript file: Find `.txt` candidates under `$HOME/Downloads` that match `infrastructure study kickoff meeting`.
- Template: The user did not specify one, so check `$HOME/.scribe`.
- Output path: The user did not specify one, so save to the current directory using the default filename.

If the target cannot be resolved to a single candidate, do not proceed automatically. Ask the user to choose.
