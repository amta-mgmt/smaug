# CLAUDE.md

This file provides guidance to Claude Code when working with code in this repository.

## Repository Purpose

Archive Twitter/X bookmarks (and optionally likes) to markdown. Automatically fetches bookmarks, expands links, extracts content, and uses Claude Code for AI-powered categorization and filing.

## Key Commands

```bash
# Install dependencies
npm install

# Run the setup wizard
npx smaug setup

# Full job (fetch + process with Claude)
npx smaug run

# Fetch bookmarks (default: 50)
npx smaug fetch 20

# Fetch ALL bookmarks (paginated)
npx smaug fetch --all

# Fetch from likes instead
npx smaug fetch --source likes

# Process already-fetched tweets
npx smaug process

# Force re-process (ignore duplicates)
npx smaug process --force

# Run tests
npm test
```

## Architecture Overview

```
1. Fetch bookmarks (bird CLI) → Twitter/X API
2. Expand t.co links → Reveal actual URLs
3. Extract content → GitHub READMEs, articles, quote tweets
4. Invoke Claude Code → Analyze and categorize
5. Save to markdown → bookmarks.md + knowledge library
```

### Project Structure

```
src/
├── cli.js        # CLI entry point
├── index.js      # Main processor logic
├── processor.js  # Bookmark processing
├── config.js     # Config loading and validation
└── job.js        # Bree job scheduler integration
knowledge/
├── tools/        # GitHub repos filed here
└── articles/     # Articles/blogs filed here
.claude/commands/ # Claude Code custom commands
test/             # Test files and fixtures
```

### Key Files

| File | Purpose |
|------|---------|
| `src/cli.js` | Commander-based CLI |
| `src/processor.js` | Core bookmark processing logic |
| `smaug.config.json` | User configuration (gitignored) |
| `.claude/commands/process-bookmarks.md` | Claude Code processing instructions |

## Configuration

Copy `smaug.config.example.json` to `smaug.config.json` and add:
- `twitter.authToken` - Twitter auth_token cookie
- `twitter.ct0` - Twitter ct0 cookie
- `claudeModel` - AI model (`sonnet`, `haiku`, `opus`)
- `source` - What to fetch (`bookmarks`, `likes`, `both`)

## Important Patterns

- Uses bird CLI for Twitter API access (requires manual cookie auth)
- Parallel processing kicks in for 8+ bookmarks (uses Haiku subagents for cost optimization)
- Categories are extensible via `smaug.config.json`
- Default actions: `file` (create separate .md) or `capture` (bookmarks.md only)

## Output Format

- `bookmarks.md` - Main archive organized by date
- `knowledge/tools/*.md` - Filed GitHub repos with frontmatter
- `knowledge/articles/*.md` - Filed articles with frontmatter

## Security Notes

- `smaug.config.json` is gitignored - never commit credentials
- Twitter cookies expire; refresh from browser DevTools as needed
- Token tracking available with `-t` flag to monitor API costs
