# Git Policy

Git workflow standards for commits, pull requests, and repository operations.

## Commit Policy

**NEVER automatically**:
- Create commits unless explicitly instructed
- Push commits unless explicitly instructed
- Include Claude attribution or Co-Authored-By tags
- Add verbose explanations of changes that simply reiterate what we can see in the diff

**Commit message format**:
- Follow standard git format (subject line ≤50 chars, body wrapped at 72 chars)
- Imperative mood, present tense
- Focus on WHY the change happened (the diff shows WHAT)
- Add body/details only to explain potentially surprising things in the diff
- Intended for context sharing with future developers and agents

**Examples:**
```
Fix rounding errors in tax calculation
Support filtering in patient search
Prevent unauthorized API access
```

## Pull Request Policy

**Format**: Draft mode, short descriptive title

**Description template**:
```
[One sentence on problem, one on solution direction]

## Manual Testing
- [ ] Test step 1
- [ ] Test step 2 (include gem install/bundle steps if needed)
- [ ] Test step 3 (include migration run steps if needed)

## Deployment Notes
- Migration for [feature name] added: [github link to migration file]
- New gem added: [gem name] - requires bundle install
- Rails credentials changes: [list any new credentials keys added] - requires update in production
- Config changes: [list any config files modified]
- [Other deployment considerations]

## Post-Deployment Notes
_(Include only if applicable)_
- Backfill job for [feature]: Scheduled in [scheduler file] to run every [interval]
- Manual verification: Check [specific metric/dashboard] after 24 hours
- Cleanup PR needed: [Details about when/what to remove]
- Follow-up: [Any manual checks needed before merging dependent PRs]
```

**Post-deployment workflow**:

**Backfill jobs**: Check scheduler file. If scheduled → suggest cleanup PR after automatic completion. If not scheduled → suggest manual run, then cleanup PR.

**Other temporary code**: Identify temporary code (feature flags, migration helpers), track removal conditions, offer cleanup PRs when safe.

## Repository Operations

**Auto-approved**: Read operations (status, diff, log, show)
**Require confirmation**: Destructive operations (force push, hard reset, rebase)
**NEVER**: Push to main/master with --force without explicit user request
