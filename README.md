# Claude Code Files

A collection of Claude Code configurations, custom commands, and PRP (Product Requirement Proposal) templates for AI-driven feature development.

## Overview

This repository provides a structured workflow for using Claude Code to autonomously research, plan, and implement features. The system uses PRPs as comprehensive context documents that enable AI agents to implement features with high accuracy in a single pass.

## Structure

```
.
├── .claude/
│   ├── commands/
│   │   ├── generate-prp.md    # Command to create new PRPs
│   │   └── execute-prp.md     # Command to implement PRPs
│   ├── tasks/
│   │   ├── product_backlog.md # Feature backlog tracking
│   │   └── innovation_loop.md # Autonomous development workflow
│   └── settings.local.json    # Local Claude settings
├── .github/
│   └── workflows/
│       ├── claude.yml              # @claude mention handler
│       └── claude-code-review.yml  # Automatic PR review
└── PRPs/
    ├── templates/
    │   └── prp_base.md        # Base PRP template
    └── EXAMPLE_multi_agent_prp.md
```

## Custom Commands

### `/generate-prp <feature-file>`

Generates a comprehensive PRP for a feature by:
- Analyzing the codebase for existing patterns
- Researching external documentation and best practices
- Creating validation gates for self-verification
- Including all context needed for one-pass implementation

### `/execute-prp <prp-file>`

Executes a PRP by:
- Loading and understanding all context
- Creating a detailed implementation plan
- Implementing the code following existing patterns
- Running validation loops until all checks pass

## PRP Philosophy

PRPs are designed around these core principles:

1. **Context is King** - Include ALL necessary documentation, examples, and caveats
2. **Validation Loops** - Provide executable tests/lints the AI can run and fix
3. **Information Dense** - Use keywords and patterns from the codebase
4. **Progressive Success** - Start simple, validate, then enhance

## Innovation Loop

The `innovation_loop.md` task defines an autonomous workflow for continuous improvement:

1. **Research** - Discover features from competitors and market trends
2. **Ideation** - Check against backlog, propose new optimizations
3. **Spec Generation** - Create PRP via `/generate-prp`
4. **Implementation** - Execute via `/execute-prp`
5. **Verification** - Run tests and validation
6. **Fix Loop** - Iterate until tests pass (max 5 attempts)
7. **Quality Gate** - Every 3rd iteration, do critical review
8. **Deployment** - Commit and push changes
9. **Restart** - Begin next iteration

## GitHub Actions

### Claude Code Review (`claude-code-review.yml`)

Automatically reviews pull requests when opened or synchronized. Reviews include:
- Code quality and best practices
- Potential bugs or issues
- Performance considerations
- Security concerns
- Test coverage

**Setup**: Add `CLAUDE_CODE_OAUTH_TOKEN` to your repository secrets.

### Claude Mention Handler (`claude.yml`)

Responds to `@claude` mentions in:
- Issue comments
- PR review comments
- PR reviews
- New issues

This allows team members to ask Claude questions or request changes directly in GitHub.

**Setup**: Add `CLAUDE_CODE_OAUTH_TOKEN` to your repository secrets.

## Usage

1. Copy the `.claude/` directory to your project
2. Copy the `.github/` directory for GitHub Actions integration
3. Add `CLAUDE_CODE_OAUTH_TOKEN` to your repository secrets
4. Customize the PRP template for your tech stack
5. Use `/generate-prp` to create feature specifications
6. Use `/execute-prp` to implement features

## License

MIT
