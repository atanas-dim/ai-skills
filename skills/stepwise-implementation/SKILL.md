---
name: stepwise-implementation
description: Implement an approved coding plan across multiple turns, completing exactly one meaningful step per turn with review, verification, and user confirmation before continuing.
argument-hint: "What plan or next step should be implemented?"
---

# Stepwise Implementation

Use this skill when the user wants a coding plan implemented gradually, in the same logical order a thoughtful human developer would use. Each step should be easy to review, understand, and continue from. This is a multi-turn workflow: do not collapse the plan into one implementation pass unless the user explicitly opts out.

## Activation

Stepwise mode is active when the user references this skill or asks for stepwise, step-by-step, staged, incremental, or confirmation-based implementation.

When stepwise mode is active, broad requests such as "start work", "implement the plan", or "continue" mean: implement only the next single logical step.

Only implement more than one meaningful step in a turn if the user explicitly opts out with instructions such as "implement all steps", "continue through the full plan without stopping", or "stepwise mode off".

## Core Rule

Implement exactly one meaningful step per turn.

If an approved plan, task list, or todo list exists:

- Choose the next logical incomplete step.
- Mark only that step as in progress or complete.
- Leave later steps pending.
- Do not start the next meaningful step until the user confirms.

Small corrections inside the current step are allowed, such as fixing a lint error or test failure introduced by that step.

## Human Reasoning Order

Implement in the order a careful human developer would use, not in file order.

Choose each step because it reduces uncertainty, establishes a needed foundation, or proves one part of the approach before expanding it.

Prefer this rhythm:

1. Clarify the immediate goal of the current step.
2. Identify the smallest useful foundation for later work.
3. Implement that foundation or focused behavior.
4. Verify it locally where practical.
5. Explain the result in plain engineering language.
6. Stop for confirmation.

Common ordering patterns:

- Shared contracts, types, constants, or helpers before feature-specific usage.
- Data access or state shape before UI that depends on it.
- One representative integration before applying the same pattern broadly.
- Validation and error handling before expanding the behavior's surface area.
- Tests or checks after each meaningful behavior layer.
- Documentation or polish after the behavior is working.

## Step Format

At the start of each step, state:

- The step number and name. If the total is known, use `Step [current]/[total]: Step Name`.
- The reasoning goal for this step.
- The files or code areas likely to be touched.
- What will intentionally remain unfinished.

After implementing the step, state:

- What changed.
- Why it matters.
- How it was checked.
- Any assumptions, tradeoffs, blockers, or follow-up risks.
- The next logical step.
- One suggested commit message in short, specific, imperative present tense.

When the step is complete and no blocker remains, end with:

> Ready for the next step?

Do not implement the next step in the same turn after asking.

## Review Boundaries

Keep each step reviewable on its own.

Good step boundaries include:

- Add shared helpers, contracts, or configuration.
- Wire the new behavior into one representative flow.
- Extend a proven pattern to additional flows.
- Add validation, error handling, or persistence.
- Add or update focused tests.
- Update documentation, accessibility, performance, or polish as a final focused pass.

It is acceptable to revisit the same file in multiple steps when that matches the natural implementation order. Do not optimize for touching each file only once.

## Autonomy Boundaries

The agent may inspect files, prepare the next step, and run checks needed to verify the current step.

Stop and ask for clarification if a decision would affect public behavior, data contracts, security, accessibility, analytics, external integrations, or user-facing content and the correct choice is not clear from context.

Do not refactor unrelated code while implementing a step. If unrelated issues are discovered, mention them as follow-up work.

## Handoff Between Sessions

Use a handoff when the session may pause, another agent may continue, context is getting long, or the user asks for one.

By default, save handoff documents to the operating system's temporary directory, not the repository. Save a handoff inside the workspace only if the user explicitly asks for a durable project artifact.

A handoff should include:

- The current goal and active stepwise status.
- Completed steps and the current step state.
- Relevant files, branches, commits, issues, plans, or other artifacts by path or URL.
- Checks run and their results.
- Open decisions, assumptions, blockers, and risks.
- The next logical step.
- Suggested skills or workflows for the next agent.

Do not duplicate content already captured in plans, PRDs, ADRs, issues, commits, diffs, or other artifacts. Reference those artifacts instead. Redact secrets, credentials, personal data, and sensitive implementation details.

## Avoid

- Implementing the full plan in one pass.
- Implementing multiple meaningful steps in one turn.
- Completing all todos before asking for confirmation.
- Presenting work file-by-file when the logic spans files.
- Making all edits first and explaining only at the end.
- Hiding assumptions until the final summary.
- Saying "Ready for the next step?" and then continuing anyway.
