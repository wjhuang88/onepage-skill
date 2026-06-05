# Release Notes

Before pushing a `v*` tag, add `releases/<tag>.md` with an Agent-authored summary for that
version.

Keep each file concise:

```markdown
## Summary

- ...

## Notable Changes

- ...

## Upgrade Notes

- ...
```

The release workflow fails if the matching file is missing. It appends the commit list and install
instructions automatically.
