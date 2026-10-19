---
name: to-prd
description: 在需求已经经过讨论和确认后，将当前对话与代码库事实整理为结构化 PRD。用户明确要求 PRD、产品需求文档或需求基线时使用；不要用它替代前置访谈、SOP 可行性评估或用户确认。
---

This skill takes already-confirmed conversation context and codebase understanding and produces a PRD. Do not reopen a full interview here; if the goal, users, scope, or success criteria are still unclear, route to brainstorm first.

## Process

1. Explore the repo to understand the current state of the codebase, if you haven't already.

2. Sketch out the major modules you will need to build or modify to complete the implementation. Actively look for opportunities to extract deep modules that can be tested in isolation, but do not invent modules unsupported by the codebase or confirmed requirements.

A deep module (as opposed to a shallow module) is one which encapsulates a lot of functionality in a simple, testable interface which rarely changes.

Before writing the final PRD, confirm that the proposed scope and modules match the user's confirmed intent. Do not silently turn optional ideas into requirements.

3. Write the PRD using the template below.

<prd-template>

## Problem Statement

The problem that the user is facing, from the user's perspective.

## Solution

The solution to the problem, from the user's perspective.

## User Stories

A LONG, numbered list of user stories. Each user story should be in the format of:

1. As an <actor>, I want a <feature>, so that <benefit>

<user-story-example>
1. As a mobile bank customer, I want to see balance on my accounts, so that I can make better informed decisions about my spending
</user-story-example>

This list of user stories should be extremely extensive and cover all aspects of the feature.

## Implementation Decisions

A list of implementation decisions that were made. This can include:

- The modules that will be built/modified
- The interfaces of those modules that will be modified
- Technical clarifications from the developer
- Architectural decisions
- Schema changes
- API contracts
- Specific interactions

Do NOT include specific file paths or code snippets. They may end up being outdated very quickly.

## Testing Decisions

A list of testing decisions that were made. Include:

- A description of what makes a good test (only test external behavior, not implementation details)
- Which modules will be tested
- Prior art for the tests (i.e. similar types of tests in the codebase)

## Out of Scope

A description of the things that are out of scope for this PRD.

## Further Notes

Any further notes about the feature.

</prd-template>
