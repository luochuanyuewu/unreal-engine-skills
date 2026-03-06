# Unreal Engine AI Agent 技能集

[English](README.md) | 简体中文

一个包含 27 个 Unreal Engine C++ 开发 AI agent 技能的集合。专为希望 AI 编程助手帮助编写正确、生产级 UE5 C++ 代码的游戏开发者构建。适用于 Claude Code、Cursor、Windsurf 以及任何支持 [Agent Skills 规范](https://agentskills.io) 的 agent。

每个技能都已根据 Unreal Engine 源代码进行审计，以确保 API 准确性 — 正确的函数签名、有效的类层次结构和真实的方法名称。没有幻觉生成的 API。

**欢迎贡献！** 发现了不准确的地方或想要改进某个技能？[提交 PR](#贡献)。



## 什么是技能？

技能是 markdown 文件，为 AI agent 提供特定任务的专业知识和工作流程。当你将这些技能添加到项目中时，你的 agent 能够识别你正在处理 Unreal Engine 任务，并应用正确的模式、API 和最佳实践。

## 技能如何协同工作

技能相互引用并构建在共享上下文之上。`ue-project-context` 技能是基础 — 它捕获你项目的模块、目标平台和约定，以便其他技能能够提供相关建议。

```
                          ┌──────────────────────────────────────┐
                          │          ue-project-context           │
                          │    (read by all other skills first)   │
                          └──────────────────┬───────────────────┘
                                             │
    ┌─────────────┬────────────┬─────────────┼────────────┬─────────────┬──────────────┐
    ▼             ▼            ▼             ▼            ▼             ▼              ▼
┌────────┐ ┌──────────┐ ┌──────────┐ ┌───────────┐ ┌──────────┐ ┌──────────┐ ┌───────────┐
│Core C++│ │Gameplay  │ │Rendering │ │  World &  │ │  AI &    │ │  UI &    │ │  Build &  │
│        │ │          │ │& VFX     │ │ Streaming │ │  Logic   │ │  Input   │ │  Tools    │
├────────┤ ├──────────┤ ├──────────┤ ├───────────┤ ├──────────┤ ├──────────┤ ├───────────┤
│cpp-    │ │gameplay- │ │materials │ │world-lvl  │ │ai-nav    │ │ui-umg    │ │module-    │
│ found  │ │ framework│ │niagara   │ │procedural │ │state-tree│ │input-sys │ │ build     │
│actor-  │ │abilities │ │audio     │ │physics    │ │mass-     │ │          │ │editor-    │
│ comp   │ │animation │ │sequencer │ │serial-    │ │ entity   │ │          │ │ tools     │
│        │ │char-move │ │          │ │ savegame  │ │          │ │          │ │testing    │
│        │ │game-feat │ │          │ │data-asset │ │          │ │          │ │async-     │
│        │ │net-repl  │ │          │ │           │ │          │ │          │ │ thread    │
└───┬────┘ └────┬─────┘ └────┬─────┘ └─────┬─────┘ └────┬─────┘ └────┬─────┘ └─────┬─────┘
    │           │            │             │            │             │              │
    └───────────┴─────┬──────┴─────────────┴────────────┴─────────────┴──────────────┘
                      │
       Skills cross-reference each other:
         cpp-foundations ↔ actor-component ↔ gameplay-framework
         gameplay-abilities ↔ animation ↔ character-movement
         ai-navigation ↔ state-trees ↔ mass-entity
```

查看每个技能的**相关技能**部分以获取完整的依赖关系图。

## 可用技能

<!-- SKILLS:START -->
| 技能 | 描述 |
|-------|-------------|
| [ue-actor-component-architecture](skills/ue-actor-component-architecture/) | Actor 和组件设计 — BeginPlay、Tick、组件附加、所有权、子 actor |
| [ue-ai-navigation](skills/ue-ai-navigation/) | AI 控制器、行为树、黑板、AI 感知、NavMesh、EQS |
| [ue-animation-system](skills/ue-animation-system/) | AnimInstance、蒙太奇、混合空间、状态机、动画通知、链接动画图 |
| [ue-async-threading](skills/ue-async-threading/) | 异步操作、线程、并行执行、任务、FRunnable、AsyncTask |
| [ue-audio-system](skills/ue-audio-system/) | UAudioComponent、SoundCue、MetaSound、衰减、并发、音频分析 |
| [ue-character-movement](skills/ue-character-movement/) | CharacterMovementComponent、移动模式、根运动、网络预测 |
| [ue-cpp-foundations](skills/ue-cpp-foundations/) | UPROPERTY、UFUNCTION、UCLASS、TArray、TMap、委托、FString、垃圾回收、智能指针 |
| [ue-data-assets-tables](skills/ue-data-assets-tables/) | DataAsset、DataTable、软引用、TSoftObjectPtr、异步加载、资产管理器 |
| [ue-editor-tools](skills/ue-editor-tools/) | 编辑器实用工具 widget、Blutility、详情自定义、属性编辑器、编辑器子系统 |
| [ue-game-features](skills/ue-game-features/) | Game Feature 插件、模块化游戏玩法、GameFeatureAction、GameFrameworkComponentManager |
| [ue-gameplay-abilities](skills/ue-gameplay-abilities/) | GAS、游戏玩法能力、游戏玩法效果、属性集、游戏玩法标签、游戏玩法提示 |
| [ue-gameplay-framework](skills/ue-gameplay-framework/) | GameMode、GameState、PlayerController、PlayerState、Pawn、HUD |
| [ue-input-system](skills/ue-input-system/) | 增强输入系统 — Input Actions、Input Mapping Contexts、修饰符、触发器 |
| [ue-mass-entity](skills/ue-mass-entity/) | Mass Entity 框架、MassProcessor、MassFragment、MassTag、MassObserver（UE 5.5+） |
| [ue-materials-rendering](skills/ue-materials-rendering/) | 材质、着色器、动态材质实例、后处理、渲染目标、Nanite、Lumen |
| [ue-module-build-system](skills/ue-module-build-system/) | Build.cs、Target.cs、模块创建、插件设置、构建配置 |
| [ue-networking-replication](skills/ue-networking-replication/) | 多人游戏网络、复制、RPC、网络角色、服务器/客户端权威 |
| [ue-niagara-effects](skills/ue-niagara-effects/) | Niagara 粒子系统、VFX、发射器、数据接口、GPU 模拟 |
| [ue-physics-collision](skills/ue-physics-collision/) | 碰撞检测、跟踪、物理模拟、物理交互、Chaos 物理 |
| [ue-procedural-generation](skills/ue-procedural-generation/) | PCG 框架、ProceduralMesh、实例化网格、运行时生成、噪声 |
| [ue-project-context](skills/ue-project-context/) | 项目上下文文档 — 模块、目标平台、约定、团队标准 |
| [ue-sequencer-cinematics](skills/ue-sequencer-cinematics/) | Sequencer、LevelSequence、过场动画、电影、相机轨道、Movie Render Queue |
| [ue-serialization-savegames](skills/ue-serialization-savegames/) | 保存/加载系统、玩家进度持久化、数据序列化、FArchive |
| [ue-state-trees](skills/ue-state-trees/) | State Tree、状态机、StateTreeTask、StateTreeCondition、StateTreeEvaluator |
| [ue-testing-debugging](skills/ue-testing-debugging/) | 自动化测试、功能测试、UE_LOG、可视化日志、调试绘制 |
| [ue-ui-umg-slate](skills/ue-ui-umg-slate/) | UMG、Slate、UserWidget、HUD、BindWidget、Common UI、MVVM |
| [ue-world-level-streaming](skills/ue-world-level-streaming/) | World Partition、关卡流送、关卡切换、数据层、世界子系统 |
<!-- SKILLS:END -->

## 安装

### 方式 1：CLI 安装（推荐）

使用 [npx skills](https://github.com/vercel-labs/skills) 直接安装技能：

```bash
# 安装所有技能
npx skills add quodsoler/unreal-engine-skills

# 安装特定技能
npx skills add quodsoler/unreal-engine-skills --skill ue-cpp-foundations ue-gameplay-abilities

# 列出可用技能
npx skills add quodsoler/unreal-engine-skills --list
```

这会自动安装到你的 `.agents/skills/` 目录（并为 Claude Code 兼容性创建符号链接到 `.claude/skills/`）。

### 方式 2：克隆并复制

克隆整个仓库并复制 skills 文件夹：

```bash
git clone https://github.com/quodsoler/unreal-engine-skills.git
cp -r unreal-engine-skills/skills/* .agents/skills/
```

### 方式 3：Git 子模块

添加为子模块以便于更新：

```bash
git submodule add https://github.com/quodsoler/unreal-engine-skills.git .agents/unreal-engine-skills
```

然后从 `.agents/unreal-engine-skills/skills/` 引用技能。

### 方式 4：Fork 并自定义

1. Fork 此仓库
2. 为你的特定项目自定义技能
3. 将你的 fork 克隆到你的项目中

### 方式 5：SkillKit（多 Agent）

使用 [SkillKit](https://github.com/rohitg00/skillkit) 在多个 AI agent（Claude Code、Cursor、Copilot 等）之间安装技能：

```bash
# 安装所有技能
npx skillkit install quodsoler/unreal-engine-skills

# 安装特定技能
npx skillkit install quodsoler/unreal-engine-skills --skill ue-cpp-foundations ue-gameplay-abilities

# 列出可用技能
npx skillkit install quodsoler/unreal-engine-skills --list
```

## 使用方法

安装完成后，只需让你的 agent 帮助处理 Unreal Engine 任务：

```
"使用 GAS 添加一个复制的生命值属性"
→ 使用 ue-gameplay-abilities 技能

"为我的开放世界设置 World Partition 流送"
→ 使用 ue-world-level-streaming 技能

"创建一个由 C++ 参数驱动的 Niagara 系统"
→ 使用 ue-niagara-effects 技能

"为我的库存系统编写自动化测试"
→ 使用 ue-testing-debugging 技能
```

你也可以直接调用技能：

```
/ue-cpp-foundations
/ue-gameplay-abilities
/ue-networking-replication
```

## 技能分类

### 核心 C++
- `ue-cpp-foundations` — UPROPERTY、UFUNCTION、容器、委托、GC、智能指针
- `ue-actor-component-architecture` — Actor 生命周期、组件设计、附加、生成
- `ue-module-build-system` — Build.cs、Target.cs、模块、插件、构建配置

### 游戏玩法系统
- `ue-gameplay-framework` — GameMode、GameState、PlayerController、PlayerState、Pawn
- `ue-gameplay-abilities` — GAS：能力、效果、属性、标签、提示
- `ue-animation-system` — AnimInstance、蒙太奇、混合空间、动画通知
- `ue-character-movement` — CMC、移动模式、根运动、网络预测
- `ue-game-features` — Game Feature 插件、模块化游戏玩法
- `ue-networking-replication` — 复制、RPC、网络角色、预测

### 渲染与 VFX
- `ue-materials-rendering` — 材质、着色器、MID、后处理、Nanite、Lumen
- `ue-niagara-effects` — Niagara 粒子、发射器、数据接口、GPU 模拟
- `ue-audio-system` — 音频组件、SoundCue、MetaSound、空间音频
- `ue-sequencer-cinematics` — Sequencer、过场动画、相机、Movie Render Queue

### 世界与数据
- `ue-world-level-streaming` — World Partition、关卡流送、数据层
- `ue-procedural-generation` — PCG 框架、程序化网格、运行时生成
- `ue-physics-collision` — 跟踪、碰撞、Chaos 物理、物理交互
- `ue-serialization-savegames` — 保存系统、FArchive、序列化
- `ue-data-assets-tables` — DataAsset、DataTable、软引用、异步加载

### AI 与逻辑
- `ue-ai-navigation` — AI 控制器、行为树、EQS、NavMesh、感知
- `ue-state-trees` — State Tree、任务、条件、评估器
- `ue-mass-entity` — Mass Entity 框架、处理器、片段、观察器

### UI 与输入
- `ue-ui-umg-slate` — UMG、Slate、Common UI、MVVM、widget 绑定
- `ue-input-system` — 增强输入、动作、映射上下文、修饰符

### 构建与工具
- `ue-editor-tools` — 编辑器实用工具 widget、详情自定义、编辑器子系统
- `ue-testing-debugging` — 自动化测试、功能测试、日志、调试工具
- `ue-async-threading` — 异步任务、线程、并行执行、并发

### 项目设置
- `ue-project-context` — 项目上下文文档，捕获你的特定设置和约定

## API 准确性

这些技能已经过多轮针对 Unreal Engine 头文件的源码级审计，以修复错误或幻觉生成的 API 调用。已识别并纠正了超过 160 处不准确之处，包括：

- 错误的函数签名和返回类型
- 不存在的方法（在 LLM 生成的 UE 代码中常见）
- 已弃用的 API 被当前替代品替换
- 错误的类层次结构和继承链

如果你发现与引擎源代码不匹配的 API 调用，请[提交 issue](https://github.com/quodsoler/unreal-engine-skills/issues)。

## 贡献

发现了改进技能的方法？有新技能建议？欢迎提交 PR 和 issue！

### 指南

- `name` 必须与目录名完全匹配（小写、仅使用连字符）
- `description` 应包含触发短语以便技能发现
- `SKILL.md` 必须少于 500 行（将详细信息移至 `references/`）
- 提交前根据 Unreal Engine 源代码验证 API 调用

## 许可证

[MIT](LICENSE) — 随意使用。
