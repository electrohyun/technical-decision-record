<p align="center">
    <img width="400" alt="Technical Decision Record Skill Logo" src="https://github.com/user-attachments/assets/3af14b51-33a3-4944-936a-4748d2aaffd7" />
</p>

<h1 align="center" style="border-bottom: none;">
    <code>Technical Decision Record Skill</code>
</h1>

<p align="center">
  A Codex Skill for recording technical decisions as reusable Markdown decision records.
</p>

<p align="center">
  <a href="./README.md">English</a> |
  <a href="./README.ko.md">한국어</a> |
  <a href="./README.ja.md">日本語</a> |
  <a href="./README.zh-CN.md">简体中文</a>
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

## Installation

Add this repository as a Codex plugin marketplace.

```bash
codex plugin marketplace add electrohyun/technical-decision-record --ref main
```

Then install the plugin.

```bash
codex plugin add technical-decision-record@technical-decision-record
```

Restart Codex, then check that the skill is available.

```txt
/skills
```

You should see:

```txt
technical-decision-record
```

## Local installation

If you cloned this repository locally, you can add it as a local marketplace instead.

```bash
codex plugin marketplace add /path/to/technical-decision-record
```

Then install the plugin.

```bash
codex plugin add technical-decision-record@technical-decision-record
```

## Updating

Pull the latest changes from the repository, then reinstall the plugin if needed.

```bash
git pull
codex plugin remove technical-decision-record
codex plugin add technical-decision-record@technical-decision-record
```

## Plugin structure

```txt
technical-decision-record/
├─ .codex-plugin/
│  └─ plugin.json
├─ .agents/
│  └─ plugins/
│     └─ marketplace.json
├─ skills/
│  └─ technical-decision-record/
│     └─ SKILL.md
├─ README.md
├─ README.ko.md
├─ README.ja.md
└─ README.zh-CN.md
```

## Usage

Mention the skill in Codex when you want to record a technical decision.

```txt
$technical-decision-record

For issue #45, let's keep the server data loading structure mostly unchanged for now,
and first move the sound and modal-related code to lazy loading.

For image priority and sizes, let's verify the actual LCP element first,
then apply them only to the critical images.

We should verify the improvement using the Lighthouse Mobile Navigation LCP breakdown
and the unused JavaScript section.

Please write a technical decision record in Markdown based on this direction.
```

## Example output

```md
## Decision summary

For `/lobby` initial rendering performance, we decided not to significantly change the server data loading structure in this issue. Instead, we will first lazy load the sound and modal-related code.

Image `priority` and `sizes` will be applied only to critical images after verifying the actual LCP element.

## Problem

The `/lobby` initial rendering path had several potential performance bottlenecks, including the client bundle size, image loading priority, and the timing of modal code loading.

## Chosen solution

- Move sound-related code out of the initial bundle.
- Load modal-related code only when the modal is actually opened.
- Apply image `priority` and `sizes` only after verifying the actual LCP element.
- Avoid major changes to the server data loading structure in this issue.

## Trade-offs accepted

This can reduce the initial rendering cost, but it may introduce a small delay the first time the user opens a modal or uses a sound-related feature.

## Evidence

Compare Lighthouse Mobile Navigation results before and after the change.

Focus on the following items:

- LCP breakdown
- unused JavaScript
- actual LCP element
- client bundle changes
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
