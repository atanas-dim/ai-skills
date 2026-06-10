---
name: compact-communication
description: Communicate coding work in concise, easy-to-follow updates that prioritize decisions, changes, verification, and next steps. Use when the user asks for compact, brief, concise, low-noise, or easier-to-follow communication.
disable-model-invocation: true
argument-hint: "What task should be communicated compactly?"
---

# Compact Communication

Use this skill when the user wants coding-agent communication to be easier to follow, less verbose, and focused on the information needed to make progress.

## Core Rule

Lead with the answer or current state, then add only the context needed to understand it.

Prefer compact, useful messages over comprehensive explanations. Do not hide important risks, blockers, decisions, verification results, or user action needed.

## Response Style

- Keep paragraphs short.
- Use bullets only when listing distinct items.
- Prefer concrete outcomes over broad explanations.
- Avoid teaching library background unless the user asks.
- Avoid long alternative comparisons unless a decision is needed.
- Skip implementation trivia that does not affect review, usage, or next steps.
- Use progressive disclosure: give the short version first, then offer deeper detail only when useful.

## Working Updates

When reporting progress, include only:

- What changed or what was found.
- Why it matters.
- What is blocked, risky, or still undecided.
- What happens next.

## Final Answers

Default to one or two short paragraphs. Use a small list only when the result is naturally list-shaped, such as checks run, changed files, or next steps.

For implementation work, include:

- The user-visible outcome.
- Verification performed.
- Any remaining risk or follow-up.

## Examples

Verbose:

```text
I investigated the implementation and found that the reason this is happening is related to how the library handles the internal state of the component. In many frameworks there are multiple ways to solve this, including using callbacks, state reducers, or a wrapper component...
```

Compact:

```text
The issue is stale component state. I fixed it by resetting the selected value when the source data changes.

Checked with `pnpm lint`; no new errors.
```

Verbose:

```text
There are several things to consider before making this change. First, we should think about whether the API should support this behavior. Second, there may be edge cases around loading states. Third, accessibility could be affected...
```

Compact:

```text
This needs one decision before implementation: should the empty state appear while loading, or only after loading succeeds with no results?
```
