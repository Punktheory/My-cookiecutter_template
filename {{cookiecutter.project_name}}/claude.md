# CLAUDE.md

This file provides guidance to Claude Code/Codex (claude.ai/code) when working with code in this repository.This doucment is writing for the describtion of instruction for vibe coding AI, including both general purpose instructions and project-specifc instructions. The purpose of this document is to allow AI quickly understand the specific details of my project, as well as the editing my code correctly, and following my requirements.

---

**无论我们是在写代码、修 Bug，还是在讨论需求、设计架构，请都遵循以下更新指南：**

### 1. vibe coding核心原则（参考 Microsoft Copilot 最佳实践，更多信息参考网页 https://aka.ms/vscode-instructions-docs）
* **技能领域指示**：不要尝试编写代码为"尽量极端地"定义所有事项指令。只应该*本项目持有*的知识。
* **按照性项目风格**：提供对应项目的代码风格、框架使用方式（如：特殊的命名惯例、按定规范的方案、执勤脚）。
* **具体且可行**：引用具体的文件或名、函数名、需架限等合作方法，不要只泛指概念。
* **具体描述**：在描述文件时，具体的告诉我是哪个文件和文件在哪个path，而不是单纯告诉我文件名，不然我无法自己找到对应的文件
* **简洁性**：说法保证清晰，有必要的时候可以细说。清晰，精简，长上下文逻辑
* **不要创建过多文档**：在没有我的清楚命令下，不要擅自创建无意义的如.md 的总结文档。
* **做出解释**：每执行一个任务/进行任务过程的时候，总是向使用者以不了解项目知识/初学者/大白话的角度解释现在在做什么，输入输出是什么，预期效果，和当前方案的风险/难处
* **可迭代性**:对于一个项目/模型训练或者迭代发展过程，对于一个部件/文件/脚本的命名，我们可能会有不同版本的训练和version，确保每个版本的代码和文件version都被清楚标注，有具体的，自己版本的对应文件名字，包括第一版，例如version_1, version2....而不是共享同一组名字，防止混淆和覆盖之前的版本

### 2. vibe coding期间模型思考的核心要点：请基本聚焦以下类型信息（取决据内容而定）
* **关键决策与背景**：
   * **为什么这样做**：记录决策选择背后的原因、方案对比以及设计意图。
  * **业务/领域知识**：关键业务规则、特殊定义或需要理解的领域性概念。
* **架构知识与约定**：
  * **非常规约定**：无法直接从代码或提供的资料中看出的所有约定。涉及到的信息遗漏或替代方案的优先级说明。
  * **错误排查**：记录遇到的报错信息、验证步骤及解决方案，避免重复排查。
*

### 3. 项目的提示
* **环境**：在这个project里面，总是用conda"(每个项目对应的环境)"这个环境来执行terminal和跑python文件，里面有正确的Python版本和安装包/在这里安装环境
* **可用显卡**：在这个project里面，你可以支配[0,1,2,3,4,5,6,7]这8块GPU来执行terminal和跑python文件
* **新项目的可维持性**：当创建新功能,写新代码，进行新研发的时候，要确保新代码的可维护性强，重复利用性强，有design pattern。
* **文件结构**：我目前project directory的最高层结构如下：1.configs folder, 2.data folder, 3.Deleted_files folder, 4.exp_results folder, 5.logs folder, 6.models folder, 7.Related_papers folder, 8. reports folder, 9. scripts folder, 10. src folder, 11. tests folder, 还有一些其他的最高层文件夹例如一下克隆下来的github repo的文件夹，整个项目的readme.md, requirements.txt，claude.md(此文件) 等等等等。每个folder下面又有自己专属的子文件夹。你应该在每次对话都清楚了解整个project的高层文件结构。在每次编写代码或者修改代码的时候，又或者是output results的时候，都要根据每个folder的角色，把存储的东西或者把写的代码或者输出结果，放到对应的文件夹里面去，确保整个项目的结构清晰，代码易于管理和维护，而不是随便乱放。
* **文件结构细节**：1.configs 是存储我的配置文件的文件夹，统一储存在这里。2.data 是存储我的数据集的文件夹，所有的数据集包括没处理的，还是正在处理的还是处理完的都放在这个文件夹里。3.Deleted_files 是存储我删除的文件的文件夹。每次我叫你删除或清理文件的时候你都应该把要删除的文件转移到Delted_files这里来，而不是直接删除它，以防误删。4.exp_results 是统一存储我的实验only结果的文件夹。下面有子文件夹checkpoints，是存储我自己的！！模型训练结果权重的文件夹，每个checkpoints都要有一个对应的version，例如version_1, version2....。5.logs 是存储我的日志文件的文件夹，例如训练日志，或者是其他的日志。6.models 是存储一些下载的模型的文件夹。7. Related_papers这个文件夹主要是方便我储存一些前置知识，例如我进行科研项目的时候会把一些前置论文存到这里，vibecoding模型可以随时去这里读取相关论文的知识（如果有的话）而不是全都论文都通过websearch获得。8. reports 是存储我的报告文件的文件夹。里面还有sub graphs 和documents。graphs子文件夹是专门用来储存图片类型的结果的地方。documents子文件夹是专门用来储存关于project 的所有文字report。final_deliverable 是存储我的最终交付物的文件夹。比如说当我的project所有东西都fianlzie了，我会把所有东西到统一储存到这里来。但是这个文件夹一般不用管他，因为这个是项目大后期才要处理的事情了。9. scripts 是存储我的脚本文件的文件夹。10. src 是存储我的源代码的文件夹。11. tests 是存储我的测试代码的文件夹，所有和测试相关非核心脚本的代码都储存在这里，测试的结果输出应该是大概写在reports文件夹或者exp_results或者其他相应的文件夹里面。
*  **文件结构细节2**: 我的claude.md文件总是会担任两个角色：1. 作为项目的overview文件，记录项目的整体进度和状态。2. 作为整个项目vibe coding的引导。
* **有问题随时问**：当你不确定某个执行细节的时候，包括但不限于所有的执行细节，随时问我我的想法，不要私自假设，不要私自默认，例如不要私自默认参数和处理方法

### 4. 终端执行规则
- **环境一致性**：在运行任何 Python 代码或 shell 命令前，必须先确保处于正确环境，所有执行命令必须前缀 `conda activate <你的环境名> &&`。


### 5. 核心文件持续维护
CLAUDE.md 的 Project Overview 承载了整个项目的长期记忆。每次项目有新的结果或者新的进展的时候，总是把在project overview更新项目的整体进展，方便追踪项目长期进展，和帮助下一轮vibecoding对话完美知道我的project目前最新进度在哪里。claude.md里面的进度更新只需要是简略的(overview)，只记录重点进展，不记录详细细节，例如具体的推理参数，具体的数值。整体进度的详细内容更新应该更新到reports/documentations 下面的md文件，或者是任何细节记载形文件。CLAUDE.md 的 Project Overview可记录的内容包括但不限于整个项目最新大体进展，最新突破性成果，最新尝试，保留过往的失败记录记载，过往的经验结论，保留过往的版本迭代记载等等。

---


ALSO, please follow Karpathy-Inspired Claude Code Guidelines:

Behavioral guidelines to reduce common LLM coding mistakes. Merge with project-specific instructions as needed.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it - don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

---

**These guidelines are working if:** fewer unnecessary changes in diffs, fewer rewrites due to overcomplication, and clarifying questions come before implementation rather than after mistakes.

(以上所有部分的内容在更新claude.md文件的时候不要修改)

-----------------------------------------------------------------------------

## Project Overview 

(这里开始是对我的项目的整体概述和状态的更新位置。你要时常精简的更新这个部分，帮助下一轮vibecoding对话知道我的project目前最新进度在哪里，也方便我自己跟踪现在project的最新进度。如果目前这个部分下面还没有内容，你可以直接写在下面开始，开始写project的overview。如果这个部分下面已经有内容了，你可以持续更新。)
