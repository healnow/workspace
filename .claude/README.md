# HealNow Workspace - Claude Code Configuration

Team-shareable Claude Code configuration for the entire HealNow multi-project workspace.

## Workspace Structure

This workspace contains 4 projects:
- **api_service** - Rails 7.2 API (HIPAA + PCI compliance)
- **dashboard.healnow.co** - Next.js 14 patient portal (HIPAA compliance)
- **healnow-admin** - Next.js 14 admin dashboard (HIPAA compliance)
- **payments-ui** - Webpack 5 embeddable payment widget (PCI compliance)

## Shared Configuration

### `common-policies/`
Universal coding standards shared across all projects. Agents in each project reference these via @ includes.

Available common policies:
- **coding.md** - Self-documenting code over comments, project organization
- **git.md** - Commit format, PR templates, backfill job workflow
- **code-review.md** - Review priority hierarchy, feedback standards
- **security.md** - HIPAA and PCI compliance standards

### `hooks/`
Shared hooks that can be referenced by project-level settings.json files.

Example: `delete-confirmation` - Prompts before file deletion operations

**Note**: Each project should copy hooks locally to `.claude/hooks/` for better portability and team sharing. Projects reference hooks with relative paths (`.claude/hooks/delete-confirmation`).

## How @ Includes Work

Projects and agents use @ includes to reference shared policies:

```markdown
@../.claude/common-policies/coding.md
@../.claude/common-policies/git.md
```

This allows common standards to be defined once and automatically loaded by all agents.

## Project-Level Configuration

Each project has its own `.claude/` directory with:
- **agents/** - Project-specific specialized agents
- **policies/** - Project-specific coding standards (e.g., Rails patterns, Next.js conventions)
- **hooks/** - Project-specific or copied shared hooks
- **settings.json** - Team-shared settings (tracked in git)
- **settings.local.json** - Personal overrides (gitignored)

## Personal Files Convention

Any file or directory with `local` in the name is automatically gitignored. Use this for personal scripts, experiments, or work-in-progress that shouldn't be shared with the team.

Examples:
- `.claude/scripts_local/` - Personal automation scripts
- `.claude/local_scripts/` - Alternative naming
- `.claude/agents_local/` - Experimental agents
- `.claude/branches.local/` - Local branch work
- `.claude/config.local.json` - Personal config overrides
- `.claude/tmp_local/` - Temporary work files

Pattern: `*local*` in filename or directory name → automatically ignored

## Precedence

1. Project-level policies override workspace policies (if same name)
2. settings.local.json overrides settings.json
3. Project agents override user-level agents (if same name)

## Git Repository Structure

This workspace is designed to be a shareable team repository:
- Common policies, hooks, and workspace README are tracked in git
- Each project subdirectory contains its own git repository
- Projects can be managed as git submodules

## Learn More

- [Claude Code Documentation](https://docs.anthropic.com/claude-code)
- [Agent SDK Documentation](https://docs.anthropic.com/claude-code/agent-sdk)
