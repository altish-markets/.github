# Cross-Repository Coordination Guide

This document outlines the strategy for coordinating work across the Altworth Markets repository ecosystem.

## Repository Structure

The Altworth Markets project is organized as a **polyrepo** with four independent repositories:

- **`backend`** - API server (.NET/C#)
- **`contracts`** - Solana smart contracts (Rust)
- **`sdk`** - TypeScript SDK monorepo (published to GitHub Packages)
- **`front-end`** - Next.js web application (consumes SDK)

Each repository:
- Has its own git history, issues, and pull requests
- Maintains independent versioning and releases
- Has dedicated CI/CD workflows
- Can be worked on separately by different team members

## Workflow Principle

**Work in separate repositories, coordinate via GitHub Issues.**

### Why Separate Repos?

✅ **Clear boundaries** - No accidental cross-repo commits
✅ **Independent CI/CD** - Each repo has its own build, test, and deploy pipeline
✅ **Better focus** - Claude Code and other tools work on one codebase at a time
✅ **Team collaboration** - Different developers can own different repos
✅ **Flexible versioning** - Each component can version independently

## Cross-Repo Coordination Patterns

### 1. Issue Linking

When work spans multiple repos, create issues in each affected repo and link them:

```markdown
## Related Issues

- Backend API: altworth-markets/backend#123
- SDK Implementation: altworth-markets/sdk#45
- Front-end Integration: altworth-markets/front-end#67
```

### 2. Pull Request References

In PR descriptions, reference related PRs from other repos:

```markdown
## Related PRs

- Depends on: altworth-markets/sdk#45
- Blocks: altworth-markets/front-end#67
- Related: altworth-markets/contracts#12
```

### 3. GitHub Projects for Epic Tracking

Use [GitHub Projects](https://github.com/orgs/altworth-markets/projects) to track multi-repo features:

1. Create a project for the feature/epic
2. Add issues from all affected repos to the project
3. Use project views to track progress across repos

### 4. Commit Message Conventions

Reference related issues across repos in commit messages:

```
feat: add market data endpoint (altworth-markets/front-end#67)
```

### 5. Release Coordination

For features spanning multiple repos:

1. **Plan the release** - Document which repos need updates
2. **Version dependencies** - Update SDK version in front-end `package.json`
3. **Deploy in order**:
   - Contracts → SDK → Backend → Front-end
4. **Tag releases** - Create git tags in each repo
5. **Document** - Update changelogs in each repo

## Common Coordination Scenarios

### Scenario 1: New API Endpoint

**Affected repos**: `backend`, `sdk`, `front-end`

**Workflow**:
1. Create issue in `backend`: "Add `/api/packs/purchase` endpoint"
2. Create issue in `sdk`: "Add `purchasePack()` method"
3. Create issue in `front-end`: "Implement pack purchase UI"
4. Link all three issues to each other
5. Create GitHub Project to track the feature
6. Work on each repo separately:
   - Backend: Implement endpoint → Test → Merge → Deploy
   - SDK: Add client method → Publish new version
   - Front-end: Update `package.json` → Implement UI → Deploy

### Scenario 2: Contract Update

**Affected repos**: `contracts`, `sdk`, `front-end`

**Workflow**:
1. Update Solana program in `contracts`
2. Deploy new program to devnet/mainnet
3. Update SDK in `sdk` to use new program IDL
4. Publish new SDK version
5. Update front-end to use new SDK version
6. Test end-to-end
7. Link all PRs and issues

### Scenario 3: Bug Fix

**Single repo**: Fix in the affected repo only

**Multiple repos**:
- Create issue in each affected repo
- Fix independently
- Link issues for context

## Issue Templates

Each repository has these issue templates:

- **Bug Report** - Standard bug reporting
- **Feature Request** - New feature proposals
- **Cross-Repo Coordination** - Features/bugs spanning multiple repos

## Best Practices

### ✅ DO

- Work in one repository at a time with Claude Code
- Create separate issues in each affected repo
- Link issues and PRs explicitly
- Use GitHub Projects for tracking epics
- Document cross-repo dependencies in README files
- Version SDK packages semantically
- Test integration points thoroughly

### ❌ DON'T

- Try to work on multiple repos in a single Claude Code session
- Make cross-repo commits (there are no cross-repo commits in a polyrepo!)
- Assume changes in one repo are automatically available in others
- Skip linking related issues
- Deploy without updating dependency versions

## Tools for Coordination

### GitHub Features

- **Issue references**: `altworth-markets/repo#123`
- **Projects**: Track work across repos
- **Milestones**: Set in each repo for releases
- **Labels**: Use consistent labels across repos (e.g., `type: bug`, `type: feature`, `priority: high`)

### Claude Code

When working with Claude Code:

1. Open one repository at a time
2. Add other repos as additional working directories only when doing cross-repo debugging
3. Use GitHub Issues for coordination context
4. Reference issue numbers in conversations

### Development Tools

- **GitHub CLI** (`gh`): Manage issues and PRs from command line
- **VS Code Multi-root Workspaces**: View multiple repos side-by-side
- **Git worktrees**: Work on multiple branches simultaneously

## Dependency Flow

```
contracts (Solana Programs)
    ↓ (IDL, program IDs)
sdk (TypeScript packages)
    ↓ (npm packages)
front-end (Next.js app) ← backend (API server)
```

**Key dependency**: Front-end depends on SDK, which depends on contracts

## Questions?

For questions about cross-repo coordination, create an issue in the relevant repository or ask in the team chat.
