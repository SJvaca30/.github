---
title: Use structured GitHub issue forms for AI-readable default templates
date: "2026-07-02"
category: docs/solutions/conventions
module: GitHub default community files
problem_type: convention
component: development_workflow
severity: low
applies_when:
  - Updating account-level default issue and pull request templates
  - Designing templates that AI assistants and humans both need to follow
  - Replacing project-specific Markdown issue templates with reusable defaults
tags: [github, issue-forms, pull-requests, ai-tracking, templates]
---

# Use structured GitHub issue forms for AI-readable default templates

## Context

The default templates in `SJvaca30/.github` originally worked as account-level community health files, but they were lightweight Markdown templates with project-specific residue such as Python, PDF upload, and medical guardrail wording. That made them usable for humans, but weak as reusable personal defaults and weak for AI agents that need stable fields for scope, evidence, verification, risk, rollback, and follow-up tracking.

## Guidance

Use GitHub Issue Forms for issue intake and keep pull request templates in Markdown. GitHub supports structured issue forms under `.github/ISSUE_TEMPLATE/*.yml`, while pull requests still use Markdown templates such as `.github/PULL_REQUEST_TEMPLATE.md`.

For personal default templates, prefer a small set of broad forms:

- Bug report
- Feature request
- Engineering task
- Technical decision

Keep the headings and field labels stable across repositories. The important fields for AI-readable work tracking are:

- Source context or truth source
- Scope and non-goals
- Acceptance criteria
- Verification plan or verification evidence
- Risk and rollback
- Related issues, pull requests, commits, and follow-ups
- Secret and privacy redaction acknowledgement

Use only labels that exist in the default `.github` repository and are likely to exist in target repositories. For this repo, that means conservative defaults such as `bug`, `enhancement`, and `question`. Custom labels such as `agent:ready` or `status:needs-triage` should wait until there is a label sync policy for target repositories.

## Why This Matters

Account-level default templates are inherited by repositories that do not define their own templates. A bad default propagates widely. Structured issue forms reduce missing context, help GitHub and Copilot collect required fields, and make later agents less dependent on free-form interpretation.

Markdown remains the right format for pull requests because GitHub does not support Issue Forms for PRs. The PR template should therefore make verification, risk, rollback, and AI tracking explicit in stable Markdown sections.

## When to Apply

- Updating `SJvaca30/.github` default community health files
- Creating a new personal or organization `.github` defaults repo
- Generalizing templates copied from a project-specific repository
- Designing issue intake for AI-assisted implementation or review workflows

## Examples

Issue form path:

```text
.github/ISSUE_TEMPLATE/engineering_task.yml
```

Pull request template path:

```text
.github/PULL_REQUEST_TEMPLATE.md
```

Conservative template labels:

```yaml
labels: ["enhancement"]
```

AI tracking section for pull requests:

```markdown
## AI tracking

Source issue/thread:
Base branch:
Head branch:
Key commits:
Follow-up issues:
Known limitations:
```

## Related

- Commit `cf9643c`: `feat: add AI-friendly issue and PR templates`
- GitHub default community health files documentation
- GitHub Issue Forms documentation
