<p align="center">
    <img width="400" alt="Technical Decision Record Skill Logo" src="https://github.com/user-attachments/assets/3af14b51-33a3-4944-936a-4748d2aaffd7" />
</p>

<h1 align="center" style="border-bottom: none;">
    <code>Technical Decision Record Skill</code>
</h1>

<p align="center">
  一个用于将技术决策记录为可复用 Markdown 文档的 Codex Skill。
</p>

<p align="center">
  <a href="./README.md">English</a> |
  <a href="./README.ko.md">한국어</a> |
  <a href="./README.ja.md">日本語</a> |
  <a href="./README.zh-CN.md">简体中文</a>
</p>

## 概览

`technical-decision-record` 可以帮助你把技术选择整理成可复用的决策记录。

当你想记录以下内容时，它会很有用：

- 为什么选择某个具体实现
- 考虑过哪些替代方案
- 为什么没有选择这些替代方案
- 接受了哪些 trade-off
- 哪些证据或结果支持这个决策
- 下次可以改进什么

这个 Skill 适用于项目复盘、Issue 评论、Pull Request 描述、架构笔记、作品集写作、博客文章以及技术面试准备。

## 安装

将此仓库添加为 Codex plugin marketplace。

```bash
codex plugin marketplace add electrohyun/technical-decision-record --ref main
```

然后安装 plugin。

```bash
codex plugin add technical-decision-record@technical-decision-record
```

重启 Codex，然后确认 Skill 是否可用。

```txt
/skills
```

如果看到下面的 Skill，说明安装成功。

```txt
technical-decision-record
```

## 本地安装

如果你已经在本地 clone 了这个仓库，也可以将本地路径添加为 marketplace。

```bash
codex plugin marketplace add /path/to/technical-decision-record
```

然后安装 plugin。

```bash
codex plugin add technical-decision-record@technical-decision-record
```

## 更新

从仓库拉取最新改动后，如有需要可以重新安装 plugin。

```bash
git pull
codex plugin remove technical-decision-record
codex plugin add technical-decision-record@technical-decision-record
```

## Plugin 结构

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

## 使用方法

当你想记录技术决策时，可以在 Codex 中显式调用这个 Skill。

```txt
$technical-decision-record

这次 #45 issue 不大幅修改服务器数据加载结构，
先将声音和弹窗相关代码改为 lazy loading。

图片的 priority/sizes 在确认实际 LCP element 之后，
只应用到关键图片上。

改进效果通过 Lighthouse Mobile Navigation 的 LCP breakdown
以及 unused JavaScript 项目来确认。

请按照这个方向编写技术决策文档。
```

## 输出示例

```md
## Decision summary

为了改善 `/lobby` 的初始渲染性能，本次 issue 决定不大幅修改服务器数据加载结构，而是先将声音和弹窗代码改为 lazy loading。

图片的 `priority` 和 `sizes` 会在确认实际 LCP element 之后，只应用到关键图片上。

## Problem

在 `/lobby` 的初始渲染中，client bundle、图片加载优先级以及弹窗代码的加载时机被确认是可能影响性能的因素。

## Chosen solution

- 将声音相关代码从初始 bundle 中分离出来。
- 弹窗内部代码只在实际打开弹窗时加载。
- 图片的 `priority` 和 `sizes` 在确认实际 LCP element 后再应用。
- 本次 issue 不大幅修改服务器数据加载结构。

## Trade-offs accepted

这样可以减少初始渲染成本，但用户第一次打开弹窗或使用声音功能时，可能会出现轻微延迟。

## Evidence

对比修改前后的 Lighthouse Mobile Navigation 结果。

重点确认以下项目：

- LCP breakdown
- unused JavaScript
- actual LCP element
- client bundle changes
```

## 什么时候使用

你可以在以下场景中使用这个 Skill：

- 选择库或框架时
- 修改架构时
- 修复包含重要实现选择的 bug 时
- 进行重构时
- 定义 Issue 或 PR 的范围时
- 决定实现方向时
- 准备 PR 或 Issue 说明时
- 编写复盘、作品集、博客文章或技术面试回答时

## Notes

这个 Skill 不是用来记录每一个小的代码改动的。

当一个决策背后包含有意义的理由，例如替代方案、trade-off、约束条件或可衡量结果时，它最有用。
