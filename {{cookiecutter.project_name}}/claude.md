# CLAUDE.md

This file provides guidance to Claude Code/Codex (claude.ai/code) when working with code in this repository.This doucment is writing for the describtion of instruction for vibe coding AI, including both general purpose instructions and project-specifc instructions. The purpose of this document is to allow AI quickly understand the specific details of my project, as well as the editing my code correctly, and following my requirements.

---

**无论我们是在写代码、修 Bug，还是在讨论需求、设计架构，请都遵循以下更新指南：**

### 1. vibe coding核心原则（参考 Microsoft Copilot 最佳实践）
* **指引词**：在这个project里面，每一轮对话的结尾都要加上“已经严格按照CLAUDE.md的指引执行”，这几个字。这几个字是为了让我确认在当轮对话你是否还记得CLAUDE.md的指引，防止因为上下文过长忘记CLAUDE.md的指引，导致没有根据我的范式要求。
* **时常复习CLAUDE.md**：你要经常回来看和复习CLAUDE.md的内容，防止上下文过长导致遗忘项目进展或者引导内容。

* **技能领域指示**：不要尝试编写代码为"尽量极端地"定义所有事项指令。只应该*本项目持有*的知识。
* **按照性项目风格**：提供对应项目的代码风格、框架使用方式（如：特殊的命名惯例、按定规范的方案、执勤脚）。
* **具体且可行**：引用具体的文件或名、函数名、需架限等合作方法，不要只泛指概念。
* **具体描述**：在描述文件时，具体的告诉我是哪个文件和文件在哪个path，而不是单纯告诉我文件名，不然我无法自己找到对应的文件
* **简洁性**：说法保证清晰，有必要的时候可以细说。清晰，精简，长上下文逻辑
* **不要创建过多文档**：在没有我的清楚命令下，不要擅自创建无意义的如.md 的总结文档。
* **做出解释**：每执行一个任务/进行任务过程的时候，总是向使用者以不了解项目知识/初学者/大白话的角度解释现在在做什么，输入输出是什么，预期效果，和当前方案的风险/难处
* **可迭代性**:对于一个项目/模型训练或者迭代发展过程，对于一个部件/文件/脚本的命名，很自然会有不同版本的训练和version，确保每个版本的代码和文件version都被清楚标注，有具体的，自己版本的对应文件名字，包括第一版，例如version_1, version2....等等而不是共享同一组名字，以防止混淆和覆盖之前的版本文件/权重。总之谨记要防止新版本的文件覆盖旧版本的文件。这些version可以称为内部版本号。
* **有问题随时问**：当你不确定某个执行细节的时候，包括但不限于所有的执行细节，随时问我我的想法，不要私自假设，不要私自默认，例如不要私自默认参数和处理方法。遇到任何不确定的事情或者没有预先plan好的情况下（例如怎么预处理数据），一定不要想当然，而是先plan好，或者跟我确认好，或者必须告知我你做了什么我们根本没explicit商量过的假设。
* **不要用奇怪的词语或者造词语或者乱造算法**：当一个模型/事物存在标准的词语形容的时候，用标准方法形容，不要造词语。当一个算法存在标准实现的时候，优先使用标准实现，不要造实现，除非是跟我商量好的。


### 2. vibe coding期间模型思考的核心要点：请基本聚焦以下类型信息（取决据内容而定）
* **关键决策与背景**：
   * **为什么这样做**：记录决策选择背后的原因、方案对比以及设计意图。
  * **业务/领域知识**：关键业务规则、特殊定义或需要理解的领域性概念。
* **架构知识与约定**：
  * **非常规约定**：无法直接从代码或提供的资料中看出的所有约定。涉及到的信息遗漏或替代方案的优先级说明。
  * **错误排查**：记录遇到的报错信息、验证步骤及解决方案，避免重复排查。


### 3. 项目的提示
* **环境**：在这个project里面，总是用conda"(这个项目对应的环境)"这个环境来执行terminal和跑python文件，里面有正确的Python版本和安装包/在这里安装环境，在运行任何 Python 代码或 shell 命令前，必须先确保处于正确环境，所有执行命令必须前缀 `conda activate <这个项目对应的环境> &&`。同时如果有需要安装的包就都安装到这个环境就好。安装新包或者删除不需要的包的时候都记得更新requirements.txt。
* **可用显卡**：在这个项目里面，你可以支配[0,1,2,3,4,5,6,7]这8块GPU来执行terminal和跑python文件，请最大利用化这些卡。比如说当进行模型训练的时候，当多于1块卡空闲的时候，可以进行DDP训练加快训练速度。又或者可以使用8块卡同步进行不同的实验，加快实验效率，最大化利用卡资源和时间。
* **新项目的可维持性**：当创建新功能,写新代码，进行新研发的时候，要确保新代码的可维护性强，重复利用性强，功能拓展性强，有design pattern。
* **挂在后台运行命令**：当codex/claude code运行一个命令/进行一个训练/跑一个脚本的时候，一定要总是默认挂在tmux/nonhup运行，确保了命令在后台长期稳定持续运行，不要只在当前terminal/当前codex/claudecode会话运行，避免因为关闭terminal而停止运行，和其他不稳定
* **文件结构**：我目前project directory的最高层结构如下：1.`checkpoints` folder, 2.`competitor_experiments` folder, 3.`configs` folder, 4.`data` folder, 5.`Deleted_files` folder, 6.`exp_results` folder, 7.`external_repos` folder, 8.`final_deliverable` folder, 9.`logs` folder, 10.`models` folder, 11.`Related_papers` folder, 12.`reports` folder, 13.`scripts` folder, 14.`src` folder, 15.`tests` folder，还有整个项目的 `README.md`, `requirements.txt`, `CLAUDE.md`(此文件), `AGENTS.md`, `.gitignore` 等等。每个folder下面又有自己专属的子文件夹。你应该在每次对话都清楚了解整个project的高层文件结构。在每次编写代码，或修改代码的时候，又或是output results的时候，都要根据每个folder的角色，把要存储的东西，或把写的代码，或输出结果，放到对应的文件夹里面去。这样可以确保整个项目的结构清晰，代码易于管理和维护，代码不会随便摆放。
* **文件结构细节**：1.`checkpoints` 是存储我自己的模型训练结果权重的文件夹，每个checkpoint都要有一个对应的version，例如version_1, version2....，不要覆盖之前版本。注意这里主要放我自己训练出来的权重，和下面 `models` 里下载来的预训练模型区分开。2.`competitor_experiments` 是存储竞品方法、baseline方法、对比实验相关代码或结果的文件夹。如果外部repo被克隆到 `external_repos`，那么基于这些外部repo做的实验配置、运行脚本、结果记录，可以放在这里，不要和原始第三方代码混在一起。3.`configs` 是存储我的配置文件的文件夹，统一储存在这里。4.`data` 是存储我的数据集的文件夹，里面按照 `raw`, `interim`, `processed`, `external` 区分原始数据、处理中间数据、处理完成数据和外部数据。5.`Deleted_files` 是存储我删除的文件的文件夹。每次我叫你删除或清理文件的时候你都应该把要删除的文件转移到 `Deleted_files` 这里来，而不是直接删除它，以防误删。6.`exp_results` 是统一存储我的实验结果的文件夹，主要放实验输出，例如指标表、实验中间结果、临时分析结果等，不要放源代码、外部repo或正式报告。里面的 `visualizations` 用来存储实验过程中产生的可视化结果。7.`external_repos` 是存储外部克隆下来的github repo或第三方代码库的文件夹，尽量保持外部repo本身的原始结构，不要和本项目自己写的核心代码混在一起。8.`final_deliverable` 是存储我的最终交付物的文件夹，比如最终报告、最终图表、最终模型、最终整理好的代码或文档等经过筛选的交付内容。但是这个文件夹一般不用管它，因为这个是项目大后期才要处理的事情。9.`logs` 是存储我的日志文件的文件夹，例如训练日志、运行日志、报错日志等。10.`models` 是存储下载的模型、预训练模型或外部模型资源的文件夹，和 `checkpoints` 里面我自己训练出来的权重区分开。11.`Related_papers` 这个文件夹主要是方便我储存一些前置知识，例如我进行科研项目的时候会把一些前置论文存到这里，vibecoding模型可以随时去这里读取相关论文的知识（如果有的话）而不是全都论文都通过websearch获得。12.`reports` 是存储我的报告文件的文件夹，里面的 `figures` 子文件夹是专门用来储存图片类型结果的地方，`documentations` 子文件夹是专门用来储存关于project的所有文字report、实验说明、阶段总结和细节记录。如果有很详细的plan或者实验记录需要记录下来，可以在documentations下面建立文件夹及文件进行记录。13.`scripts` 是存储我的脚本文件的文件夹，主要放一次性执行脚本、pipeline入口脚本、数据处理/训练/评估的启动脚本。14.`src` 是存储我的源代码的文件夹，主要放可以被重复调用、长期维护的核心代码、模块和函数。15.`tests` 是存储我的测试代码的文件夹，所有和测试相关的非核心脚本代码都储存在这里，测试结果按类型写入 `reports` 文件夹、`exp_results` 文件夹或者其他相应的文件夹里面。
*  **文件结构细节2**: 我的claude.md文件会一直担任两个角色：1. 作为项目的overview文件，记录项目的整体进度和状态。2. 作为整个项目vibe coding的引导，请记住。
*  **文件整理范式**: 当开启新模块或者架构研究的时候，总是开更多的文件夹来存储相关的代码、数据、结果等，而不是直接在比如说\exp_results\visualizations下面直接加入裸文件，这便于管理和整理。
*  **不可误删文件**:请记住`Deleted_files` 是存储我删除的文件的文件夹。每次我叫你删除或清理文件的时候你都应该把要删除的文件转移到 `Deleted_files` 这里来，而不是直接删除它，以防误删。也就是说在我的项目下面你不可以直接删除文件，而是把`Deleted_files`当初一个垃圾桶，废弃文件可以转移到这里面，权当删除了。我会亲自审批再决定是否真正删除这个文件。请记住，在这个项目你不可以直接删除我的任何文件，同时转移任何文件到`Deleted_files`也要经过我的同意，防止误删。你只有一个情况可以直接删除文件：经过我的explicit 同意，同时删除的规模并不大比如说只是删除一个很小的空文件或者删除一个很小的error版本。


### 4. 我的工作模式
*  **smoke test**:在启动长期训练或者大体积训练之前，总是先尝试小型的smoke test，保证一切能跑通和初期loss是正常的情况下，再进行正式训练。
*  **multi vibe coding 工作模式**:通常我在一个项目工作的时候，会同时进行多个vibe coding对话，每个对话都有自己的任务和目标。你要明白这一点。所以在一个vibe coding工作的期间，如果你发现文件发生了什么变更，但是不是你的窗口做的事情，又或者发现GPU被其他不是你启动的进程占用了，不要感到奇怪，这是正常的情况，这可能是另一个窗口的vibe coding 在工作。（除非你感觉到有很大，很异常的项目改动，那这可能是发生了什么意外，而不是另一个窗口的vibe coding的操作，通知我就好）
*  **branch 和 ablation 工作模式**:通常我在一个项目工作的时候，会以不同branch的形式进行实验，比如说一个模块的研发可能会有很多不同的实验和尝试，因为我不能总是确保某一条尝试是正确的，所以我要做多条线路的尝试，最后选出一条最好的线路你要明白这一点，我的科研模式是这样。另外就是我的习惯来说每当我研发完一个模块我都要立即进行一个消融实验，来观察这个模块是否真正work，而不是因为一些confounding 因素，这可以为整个架构打好基础和为下一个模块提供稳定的地基。
*  **数据集处理**：我通常有一个很好的习惯，所有数据集都会拆分成train, val, test 三个部分，分别用于训练，验证和测试。默认按照70:15:15的比例拆分就好，但是这一点是case by case。
*  **每次跑完实验或者提出新idea都给我用大白话从头到尾解释和分析结果**：由vibecoding的做事速度很快和思维很高，人类的思维时常跟不上你，我需要你每一次跑完实验/提出新想法/做出一次分析，自动每次都要完完全全由背景，到结果，到你的分析，向我用大白话解释一次现在发生了什么，你在做什么，保证我能够跟上vibe coding你的进度。
*  **Workspace文件瘦身**：在项目开始了一段时间时候，一般会经历大量的研发或者版本积累，由于实验总是会有很多失败的版本，和会有积累很多中途的测试文件，一般整个workspace都会开始积累成比较臃肿的样子（有很多臃肿沉淀的文件和未整理的文件夹），我会定期命令你帮workspace瘦身并且会给你明确指引我想瘦身，以精简和整理整个workspace的文件管理。workspace文件瘦身这件事情我会明确告诉你触发和具体怎么做，不需要你自动触发，我在这里只是想告诉你：可能会有瘦身这件事情出现。

### 5. 核心文件持续维护
CLAUDE.md 的 Project Overview 承载了整个项目的长期记忆。每次项目有新的结果或者新的进展的时候，总是在project overview更新项目的整体最新进展，方便我们追踪项目的长期进度，和帮助下一轮vibecoding对话完美知道我的project目前最新进度在哪里。claude.md里面的进度更新只需要是简略的(overview)，只记录重点进展，不记录详细细节，例如具体的推理参数，具体的数值等等。CLAUDE.md 的 Project Overview“记录重点进展”的内容包括但不限于整个项目最新大体进展，最新突破性成果，最新尝试，保留过往的失败记录记载，过往的经验结论，保留过往的版本迭代记载等等。如果是整体进度的具体详细内容更新应该更新到reports/documentations 下面的md记录文件（如有），或者是任何细节记载形文件。

CLAUDE.md是重要文件，记得不要乱删里面的内容（除非是错误的资料），否则会导致项目进度丢失。过去，对现在已经没用的信息，可以标志为[history]。但是记住过去，对现在已经没用的信息不代表是没有价值，过去，失败的信息同样可以为未来的研究提供宝贵的经验。有时候CLAUDE.md可能会过长，所以我可能会**主动**（记住不是你自动触发）叫你稍微精简和整理一下CLAUDE.md，记住这种情况下也是要秉持“最大程度上保留信息量,只是让CLAUDE.md更整齐，只是去掉**确定**为无用，赘余的信息”的原则进行精简，而不是乱删，乱总结，直接删掉旧版本的资料等等。

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

(这里开始是对我的项目的整体概述和状态的更新位置。你要时常精简的更新这个部分，更新最新进展，帮助下一轮vibecoding对话知道我的project目前最新进度在哪里，也方便我自己跟踪现在project的最新进度。如果目前这个部分下面还没有内容，你可以直接写在下面开始，开始写project的overview。如果这个部分下面已经有内容了，你可以持续更新。)
