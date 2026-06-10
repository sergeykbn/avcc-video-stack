# Contributing

Thanks for thinking about contributing. This stack is opinionated — it codifies what works in production AI video. Contributions that sharpen that focus are very welcome.

## What we accept

### New skills
Drop a folder under `skill/<your-skill-name>/` containing a `SKILL.md` with proper frontmatter. Skills should solve a recurring video-production problem (e.g., VO scripts, B-roll planning, thumbnail generation). Include hard rules where appropriate.

### New demos
Drop a clean, finished project under `projects/demo-<short-name>/` showing a full workflow end-to-end. Keep total size under 100MB. Include a `README.md` walking through the folders.

### Workflow improvements
Edits to `docs/`, `templates/`, or `tools/` that make the process clearer or faster.

### Bug reports
Open an issue with: what you tried, what happened, what you expected.

## What we don't accept

- Promotional material disguised as demos
- Skills that bypass safety rules (real-person hallucination, brand IP impersonation, etc.)
- Massive binary uploads without trimming
- Tool-specific lock-in when a tool-agnostic alternative exists

## How to submit

1. Fork the repo
2. Create a branch (`git checkout -b skill/my-thing` or `demo/my-thing`)
3. Make your changes
4. Open a pull request describing what it does and why

Keep PR descriptions concrete: what problem does this solve, and what does the user experience look like?

## Quality bar for skills

A good skill:

- Has a clear, narrow trigger (don't claim every video task)
- Enforces rules learned from production, not theoretical best practices
- Asks before assuming when the user's intent is ambiguous
- Produces structured, parseable output

## License

By contributing you agree your contributions are released under the same MIT License as the rest of the project.
