<p align="center">
    <img width="400" alt="Technical Decision Record Skill Logo" src="https://github.com/user-attachments/assets/3af14b51-33a3-4944-936a-4748d2aaffd7" />
</p>

<h1 align="center" style="border-bottom: none;">
    <code>Technical Decision Record Skill</code>
</h1>

<p align="center">
  기술 의사결정을 재사용 가능한 Markdown 기록으로 정리하기 위한 Codex Skill입니다.
</p>

<p align="center">
  <a href="./README.md">English</a> |
  <a href="./README.ko.md">한국어</a> |
  <a href="./README.ja.md">日本語</a> |
  <a href="./README.zh-CN.md">简体中文</a>
</p>

## 개요

`technical-decision-record`는 기술적 선택을 재사용 가능한 의사결정 기록으로 바꾸는 데 도움을 줍니다.

다음과 같은 내용을 기록하고 싶을 때 사용할 수 있습니다.

- 왜 특정 구현 방식을 선택했는가
- 어떤 대안들을 고려했는가
- 왜 그 대안들을 선택하지 않았는가
- 어떤 trade-off를 받아들였는가
- 어떤 근거 또는 결과가 이 결정을 뒷받침하는가
- 다음에는 무엇을 개선할 수 있는가

이 Skill은 프로젝트 회고, 이슈 코멘트, Pull Request 설명, 아키텍처 노트, 포트폴리오 작성, 블로그 글, 기술 면접 준비에 활용할 수 있습니다.

## 설치

이 저장소를 Codex plugin marketplace로 추가합니다.

```bash
codex plugin marketplace add electrohyun/technical-decision-record --ref main
```

그다음 플러그인을 설치합니다.

```bash
codex plugin add technical-decision-record@technical-decision-record
```

Codex를 재시작한 뒤, Skill이 정상적으로 보이는지 확인합니다.

```txt
/skills
```

다음 Skill이 보이면 설치가 완료된 것입니다.

```txt
technical-decision-record
```

## 로컬 설치

이 저장소를 로컬에 clone한 경우, 로컬 경로를 marketplace로 추가할 수도 있습니다.

```bash
codex plugin marketplace add /path/to/technical-decision-record
```

그다음 플러그인을 설치합니다.

```bash
codex plugin add technical-decision-record@technical-decision-record
```

## 업데이트

저장소의 최신 변경사항을 가져온 뒤, 필요한 경우 플러그인을 다시 설치합니다.

```bash
git pull
codex plugin remove technical-decision-record
codex plugin add technical-decision-record@technical-decision-record
```

## 플러그인 구조

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

## 사용법

기술 의사결정을 기록하고 싶을 때 Codex에서 Skill을 명시적으로 호출합니다.

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

## 출력 예시

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

## 언제 사용하나요?

다음과 같은 상황에서 사용할 수 있습니다.

- 라이브러리나 프레임워크를 선택할 때
- 아키텍처를 변경할 때
- 의미 있는 구현 선택이 포함된 버그를 해결할 때
- 리팩터링을 진행할 때
- 이슈나 PR의 범위를 정할 때
- 구현 방향을 결정할 때
- PR 또는 이슈 설명을 준비할 때
- 회고, 포트폴리오, 블로그 글, 기술 면접 답변을 준비할 때

## 참고

이 Skill은 모든 작은 코드 변경을 기록하기 위한 도구가 아닙니다.

대안, trade-off, 제약 조건, 측정 가능한 결과처럼 의미 있는 판단 근거가 있는 결정에 사용할 때 가장 유용합니다.
