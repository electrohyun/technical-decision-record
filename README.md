<p align="center">
    <img width="1027" height="1027" alt="Technical Decision Record Skill Logo" src="https://github.com/user-attachments/assets/3af14b51-33a3-4944-936a-4748d2aaffd7" />
</p>

<h1 align="center" style="border-bottom: none;">
    <code>Technical Decision Record Skill</code>
</h1>

<p align="center">
  A Codex Skill for recording technical decisions as reusable Markdown decision records.
</p>

## Overview

`technical-decision-record` helps turn technical choices into reusable decision records.

It is useful when you want to document:

- why a specific implementation was chosen
- what alternatives were considered
- why those alternatives were rejected
- what trade-offs were accepted
- what evidence or result supports the decision
- what should be improved next time

This skill is designed for project retrospectives, issue comments, pull request descriptions, architecture notes, portfolio writing, blog posts, and technical interview preparation.

## Plugin structure

```txt
technical-decision-record-plugin/
├─ .codex-plugin/
│  └─ plugin.json
├─ skills/
│  └─ technical-decision-record/
│     └─ SKILL.md
└─ README.md
```

## Usage

Mention the skill in Codex when you want to record a technical decision.

```txt
$technical-decision-record

이번 #45 이슈는 서버 데이터 로딩 구조는 이번 범위에서 크게 바꾸지 않고,
먼저 사운드와 모달 코드를 lazy loading하는 방향으로 가자.

이미지 priority/sizes는 실제 LCP element를 확인한 뒤,
핵심 이미지에만 적용하자.

개선 여부는 Lighthouse Mobile Navigation의 LCP breakdown과
unused JavaScript 항목으로 확인하는 게 좋겠어.

이 방향으로 기술 의사결정 문서 작성해줘.
```

## Example output

```md
## Decision summary

`/lobby` 초기 렌더링 성능 개선을 위해 서버 데이터 로딩 구조는 이번 이슈 범위에서 제외하고, 사운드와 모달 코드를 lazy loading하는 방향으로 결정했다.

이미지 `priority`와 `sizes`는 실제 LCP element를 확인한 뒤 핵심 이미지에만 적용한다.

## Problem

`/lobby` 초기 렌더링에서 client bundle, 이미지 로딩 우선순위, 모달 코드 로딩 시점이 성능 저하 후보로 확인되었다.

## Chosen solution

- 사운드 관련 코드는 초기 bundle에서 분리한다.
- 모달 내부 코드는 실제로 모달이 열릴 때 로드한다.
- 이미지 `priority`와 `sizes`는 실제 LCP element를 확인한 뒤 적용한다.
- 서버 데이터 로딩 구조는 이번 이슈에서 크게 변경하지 않는다.

## Trade-offs accepted

초기 렌더링 비용은 줄일 수 있지만, 사용자가 모달이나 사운드 기능을 처음 사용할 때 약간의 지연이 생길 수 있다.

## Evidence

변경 전후 Lighthouse Mobile Navigation 결과를 비교한다.

특히 다음 항목을 확인한다.

- LCP breakdown
- unused JavaScript
- 실제 LCP element
- client bundle 변화
```

## When to use

Use this skill when you are:

- choosing a library or framework
- changing architecture
- fixing a bug with a meaningful implementation choice
- refactoring code
- defining issue or PR scope
- deciding implementation direction
- preparing PR or issue explanations
- writing retrospectives, portfolio notes, blog posts, or technical interview answers

## Notes

This skill is not intended to document every small code change.

It is most useful when a decision has meaningful reasoning behind it, such as alternatives, trade-offs, constraints, or measurable results.
