---
name: technical-decision-record
description: Use when making, explaining, reviewing, or documenting meaningful technical decisions, including choosing libraries or frameworks, changing architecture, fixing bugs, refactoring code, defining issue scope, deciding implementation direction, confirming a chosen direction after discussing alternatives, choosing what to include or exclude from an issue or PR, introducing or replacing implementation patterns, preparing PR or issue explanations, writing retrospectives, portfolio notes, blog posts, or technical interview answers about why a specific implementation was chosen.
---

# Technical Decision Record

## Purpose

Use this skill to turn a technical choice into a reusable decision record.

Focus on why the implementation was chosen, what alternatives were considered, and what trade-offs were accepted. Do not simply describe what was implemented or praise the solution.

The output should be reusable in:

- Project retrospectives
- Blog posts
- Portfolio descriptions
- Technical interviews
- Issue comments
- Pull request descriptions
- Architecture notes
- Decision boards

## Core Rule

Do not just explain what was built. Record why it was built that way.

Do not turn every technical conversation into a final document.

If the user is still exploring, comparing, debugging, or deciding, help them think first.

If the user confirms a direction, scope, or implementation boundary after a technical decision discussion, treat that confirmation as the chosen decision and write the decision record.

## Workflow

1. Identify the decision being documented.
2. Gather enough context to explain the problem, chosen solution, alternatives, trade-offs, and result.
3. Before writing the final record, identify the key decision questions. Ask up to 3 focused questions that would help the user choose or clarify the direction. Prefer questions that reveal scope, trade-offs, evidence, or implementation boundaries.
4. If meaningful context is missing, ask only the questions that would materially improve the record.
5. If the user confirms a direction, scope, or implementation boundary after a decision discussion, treat it as the chosen solution and write the decision record.
6. Write a concise markdown decision record.
7. Mark uncertain inferences clearly when the user has not provided enough evidence.

## Context To Gather

When documenting a decision, focus on:

- What problem was being solved?
- What solution was chosen?
- What alternatives were considered?
- Why were the alternatives rejected?
- What trade-offs were accepted?
- What improved after the change?
- Is there evidence, a metric, or a concrete result?
- What would be changed next time?

## Missing Context

If important context is missing, ask before writing a final record.

Ask about:

- The original problem
- The previous implementation
- The chosen solution
- Rejected alternatives
- Constraints such as time, team size, performance, maintainability, or project scope
- Concrete results after the change
- Metrics, logs, screenshots, user feedback, or test results if available

When asking questions, do not ask a long checklist.
Ask at most 3 questions at a time.

Prioritize questions that help the user make a decision, such as:

- What scope should this issue or PR include?
- Which trade-off is acceptable for this project?
- What evidence will be used to verify the result?

Do not force the user to answer every question. Ask only for the missing information that would meaningfully improve the record.

## Trigger Examples

Use this skill when the user says things like:

- "이 결정 기록으로 남기자."
- "이 방향으로 기술 의사결정 문서 작성해줘."
- "Decision Board에 올릴 수 있게 정리해줘."
- "PR 설명으로 남기자."
- "왜 이렇게 했는지 기록하자."
- "대안과 trade-off를 정리하자."
- "나중에 회고나 면접에서 설명할 수 있게 정리하자."

Also use this skill when the user confirms a direction after a technical decision discussion, such as:

- "이 방향으로 가자."
- "이번 이슈 범위는 여기까지로 하자."
- "서버 구조는 이번에 안 건드리고, 클라이언트 번들부터 줄이자."
- "우선 이 방법으로 가고, 결과는 Lighthouse로 확인하자."
- "이렇게 결정하자."

In these cases, treat the user's message as the chosen decision and write the decision record, as long as there is enough prior context.

Do not use this skill merely because the user mentions an issue, pull request, blog post, portfolio, or architecture note.
Use it when the conversation is about a meaningful technical decision or when the user asks to document the reasoning behind a choice.

## Decision Record Format

Use this structure when preparing a technical decision record:

## Decision summary

Briefly summarize the decision in one or two sentences.

## Problem

Explain what problem, limitation, bug, or uncertainty existed before the decision.

## Chosen solution

Describe the solution that was selected. Focus on what changed and how it solves the problem.

## Alternatives considered

List the realistic alternatives that were considered, including options that were rejected, postponed, or intentionally avoided.

## Why alternatives were rejected

Explain why each alternative was not chosen.

## Trade-offs accepted

Explain what was gained and what was sacrificed. Do not pretend the chosen solution is perfect.

## Result

Explain what improved after the decision.

## Evidence

Include metrics, examples, logs, screenshots, test results, or before-and-after comparisons if available. If there is no concrete evidence yet, say whether the result is based on implementation reasoning or qualitative observation.

## What I would change next time

Mention future improvements, remaining risks, or follow-up tasks.

## Alternative Rejection Reasons

Use concrete reasons when explaining rejected options:

- Too complex for the current scope
- Poor maintainability
- Unnecessary dependency
- Performance concern
- Weak type safety
- Difficult testing
- Poor user experience
- Mismatch with project architecture
- Too much migration cost

## Result Examples

Prefer specific outcomes such as:

- Reduced duplicated validation logic by moving responsibility into a shared schema
- Made dependency direction clearer by preventing feature modules from importing each other directly
- Avoided adding a new library because the required behavior could be implemented with the existing platform API
- Reduced code duplication
- Simplified the API
- Reduced bugs
- Improved rendering speed
- Improved readability
- Made testing easier
- Clarified responsibility boundaries
- Improved a user flow

## Writing Style

Write concise, reusable markdown.

Use the user's language by default.

If the user writes in Korean, write the decision record in Korean unless the user explicitly asks for English.

For Korean output, keep technical terms readable.
Use common English technical terms such as `LCP`, `FCP`, `bundle`, `hydration`, `lazy loading`, `priority`, and `trade-off` when translating them would make the record less clear.

Avoid vague praise such as:

- This is a good implementation.
- This was a clean solution.
- It improved the code a lot.

Prefer concrete explanations such as:

- This reduced duplicated validation logic by moving the responsibility into a shared schema.
- This made the dependency direction clearer by preventing feature modules from importing each other directly.
- This avoided adding a new library because the required behavior could be implemented with the existing platform API.

## Output Behavior

When the user asks for a technical decision record, output a clean markdown record.

When the user asks to prepare content for a decision board, issue, pull request, retrospective, portfolio, blog post, or architecture note, prepare the output as a standalone markdown document that can be copied directly.

When the user confirms a direction, scope, or implementation boundary after a technical decision discussion, write the decision record directly.

Do not create a standalone markdown document merely because the user mentions an issue, pull request, blog post, portfolio, or architecture note.

Only write the final decision record when one of these is true:

- The user explicitly asks to document, record, write, summarize, prepare, or save the decision.
- The user confirms a direction after alternatives, trade-offs, issue scope, or implementation boundaries have already been discussed.
- The user provides a chosen solution and asks to proceed with that direction.
- The user asks for content that can be reused in a decision board, issue comment, pull request description, retrospective, portfolio, blog post, technical interview, or architecture note.

If the user asks to save the record as a file, create or update a markdown file instead of only replying in chat.

When a file path is not provided, suggest a concise filename such as:

- docs/decisions/issue-45-rendering-performance.md
- docs/decisions/lobby-initial-rendering-performance.md
- decisions/technical-decision-record-issue-45.md

When the user is still thinking through a decision, help compare options first.

When the user only provides code or a short explanation, infer what is reasonable, clearly mark uncertain parts, and ask for missing context if needed.
