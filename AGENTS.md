# AGENTS.md

> Agent instructions for this repository.

## Commands

| Action | Command |
|--------|---------|
| Install | `npm install` |
| Setup wizard | `npx smaug setup` |
| Full job | `npx smaug run` |
| Fetch bookmarks | `npx smaug fetch 20` |
| Fetch all | `npx smaug fetch --all` |
| Fetch likes | `npx smaug fetch --source likes` |
| Process | `npx smaug process` |
| Force reprocess | `npx smaug process --force` |
| Test | `npm test` |

## Conventions

- Follow existing patterns in codebase
- Study similar files before creating new ones
- Categories are extensible via `smaug.config.json`
- Default actions: `file` (create separate .md) or `capture` (bookmarks.md only)
- Parallel processing kicks in for 8+ bookmarks

## Git Protocol

- Commit after completing logical units of work
- Use descriptive commit messages
- Never force push or amend published commits

## Quality Gates

- All tests must pass before marking task complete
- No lint errors
- Build must succeed

## Tech Stack

- **Runtime:** Node.js
- **Language:** JavaScript
- **Twitter API:** bird CLI (cookie auth)
- **AI:** Claude Code

## Configuration

Copy `smaug.config.example.json` to `smaug.config.json` and add:
- `twitter.authToken` - Twitter auth_token cookie
- `twitter.ct0` - Twitter ct0 cookie
- `claudeModel` - AI model

## Security Notes

- `smaug.config.json` is gitignored - never commit credentials
- Twitter cookies expire; refresh from browser DevTools as needed
