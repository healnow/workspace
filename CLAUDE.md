  # HealNow Workspace
  Multi-project healthcare platform monorepo.

  ## Project Architecture
  api_service/          # Rails 7.2 API (primary backend)
  ├─ dashboard/         # Patient portal (Next.js, consumes api_service)
  ├─ healnow-admin/     # Admin dashboard (Next.js, consumes api_service)
  └─ payments-ui/       # Payment widget (standalone JS)

  ## Cross-Project Workflows

  **Starting development**:
  ```bash
  cd api_service && .claude/scripts/rails.sh s
  cd dashboard.healnow.co && npm run dev

Database changes affect:
- api_service (schema)
- dashboard + healnow-admin (API contracts)

## Shared Standards

All projects follow workspace standards:
- Coding: See `.claude/common-policies/coding.md`
- Git workflow: See `.claude/common-policies/git.md`
- Security: See `.claude/common-policies/security.md`
- HIPAA/PCI compliance required across all projects

## Agent Delegation Philosophy

**Before responding to EVERY prompt**, review agent descriptions to check if any trigger criteria match the task:
1. Check `.claude/agents/` (workspace-level), `~/.claude/agents/` (user-level), and project `.claude/agents/`
2. Read agent descriptions for specific triggers and capabilities
3. Delegate proactively when trigger criteria match - trust the agent's self-description
4. Consider whether specialized expertise would improve the outcome

**Delegation triggers** - Check agents before proceeding if the task involves:
- Domain-specific expertise (security, testing, documentation, DevOps)
- Multi-step workflows with established patterns
- Cross-cutting concerns (HIPAA compliance, performance optimization)
- Tasks mentioned in agent frontmatter descriptions

**Philosophy**: Delegation is preferred over generalist approaches when specialized agents exist. Check agent capabilities early, not as a fallback.

## Domain-Specific Workflows

**Security/Compliance**: For HIPAA or PCI-related work, consult security agents before implementation
**Testing**: For test suite setup or mutation testing, check testing agents
**Documentation**: For API docs or runbooks, review documentation agents
**Performance**: For optimization work, consider performance analysis agents