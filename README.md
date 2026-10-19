# 项目 Skill 目录

本项目是一个可通过 Codex Plugin 机制安装的 AI 开发 SOP 工具包。运行时 skill 位于正式插件目录，维护工具保留在仓库顶层。

## 设计判断

这套工具包的核心不是让 AI 一次生成完整系统，而是让非技术用户能在对话中完成一条可回溯的闭环：

需求澄清 → SOP 可行性 → 项目规则 → 需求基线 → 变更实现 → 验收回归 → 问题修复 → 再次迭代。

原目录已经覆盖了不少专项能力，但缺少两个流程控制点：

- project-workflow：判断当前阶段、选择下一个 skill、阻止越过前置条件。
- acceptance-check：按用户目标验证核心路径、失败路径和回归，不把能编译当成完成。

## 目录结构

    项目根目录/
    ├── .agents/plugins/marketplace.json
    ├── plugins/ai-development-sop/
    │   ├── .codex-plugin/plugin.json
    │   └── skills/<skill-name>/SKILL.md
    ├── skill-creator/
    ├── AI开发SOP-新版.html
    └── README.md

## 安装

### Codex Plugin

在 Codex CLI 中添加本仓库的 marketplace：

    codex plugin marketplace add https://github.com/usertianziyang/ai-development-sop.git --ref main

然后安装插件：

    codex plugin add ai-development-sop --marketplace ai-development-sop-marketplace

桌面端也可以在 /plugins 中选择同名插件。

也可以直接使用下面的一句话让具备文件和终端权限的 AI 执行安装：

    请从 https://github.com/usertianziyang/ai-development-sop 安装 ai-development-sop 插件，固定使用 main 版本；先读取 plugin.json 和 README.md，安装到当前 Codex 项目，不要修改业务代码，安装后列出已发现的 SKILL.md。

### 单独打包某个 skill

    python3 skill-creator/scripts/package_skill.py plugins/ai-development-sop/skills/project-workflow dist

## 发布结构

- .codex-plugin/plugin.json：插件元数据和版本。
- plugins/ai-development-sop/skills/：面向用户运行的 skill。
- .agents/plugins/marketplace.json：公开 marketplace 清单。
- skill-creator/：维护和打包工具，不作为普通用户运行 skill 默认安装。

## Skill 功能清单

### 一、核心流程、需求与文档

| Skill | 功能作用 | 适用场景 |
|---|---|---|
| [project-workflow](./project-workflow/SKILL.md) | 总流程路由和阶段门 | 从 0 开发、继续迭代、新增功能、修复 bug、调整 UI、不知道下一步做什么 |
| [sop-feasibility-review](./sop-feasibility-review/SKILL.md) | 评估 SOP 是否适合系统化，划分自动化、人工和暂缓边界 | 流程评估、接口依赖、风险和替代方案 |
| [sop-organizer](./sop-organizer/SKILL.md) | 把通用 SOP 适配成当前项目可执行的流程 | 生成流程适配结论和 docs/流程适配.md |
| [agents-md-init](./agents-md-init/SKILL.md) | 根据项目事实初始化或更新 AGENTS.md | 建立项目规则、技术栈、命令和工作约定 |
| [brainstorm](./brainstorm/SKILL.md) | 通过结构化问答把想法整理成产品方案 | 新项目、需求模糊、开始写需求前 |
| [to-prd](./to-prd/SKILL.md) | 把已确认的范围整理成结构化 PRD | 用户明确需要需求基线或产品文档 |
| [database-model-docs](./database-model-docs/SKILL.md) | 将真实数据库结构整理成模型文档并同步 ER 图 | 使用数据库、schema、migration 或 ORM model 时 |

### 二、问题、开发纪律与验收

| Skill | 功能作用 | 适用场景 |
|---|---|---|
| [qa](./qa/SKILL.md) | 通过少量追问收集和拆分可复现问题 | 用户无法准确描述 bug 或验收问题时 |
| [app-diagnose](./app-diagnose/SKILL.md) | 在问题已复述后定位根因、修复并验证 | 页面异常、按钮无反应、数据不对或报错 |
| [acceptance-check](./acceptance-check/SKILL.md) | 按用户目标做功能验收和回归检查 | 功能开发、bug 修复、UI 调整完成后 |
| [karpathy-guidelines](./karpathy-guidelines/SKILL.md) | 降低 AI 过度修改、猜测和无关复杂度 | 写代码、改代码、重构和审查全过程 |

### 三、界面与技术栈专项

| Skill | 功能作用 | 适用场景 |
|---|---|---|
| [impeccable](./impeccable/SKILL.md) | 建立设计上下文并确定新页面视觉方向 | 从零设计页面或需要 teach/craft 流程 |
| [frontend-design](./frontend-design/SKILL.md) | 根据已确认的方向实现前端页面和组件 | 新建网页、组件、仪表盘或交互 |
| [design-polish](./design-polish/SKILL.md) | 精修已有页面的风格、排版、响应式和动效 | 页面太普通、太丑、拥挤或像 AI 生成 |
| [antd-table-guide](./antd-table-guide/SKILL.md) | 提供 Ant Design Table 的修改规范 | 表格列、分页、筛选、固定列和性能 |
| [i18n](./i18n/SKILL.md) | 提供 NestJS + React 多语言实现约定 | 国际化、翻译和语言切换 |
| [react-hook-best-practices](./react-hook-best-practices/SKILL.md) | 处理 React Hooks、Effect 和派生状态问题 | 编写或审查 React Hooks |
| [zoom-out](./zoom-out/SKILL.md) | 给出代码库高层地图和调用关系 | 不熟悉代码区域时 |
| [improve-codebase-architecture](./improve-codebase-architecture/SKILL.md) | 分析架构摩擦并寻找可测试的模块边界 | 架构改进、模块拆分和维护性问题 |
| [request-refactor-plan](./request-refactor-plan/SKILL.md) | 通过访谈制定小步重构计划 | 重构 RFC 和安全拆分提交 |

### 四、维护与表达

| Skill | 功能作用 | 适用场景 |
|---|---|---|
| [skill-creator](./skill-creator/SKILL.md) | 创建、修改、评估和打包 skill | 维护本仓库或设计新 skill |
| [caveman](./caveman/SKILL.md) | 压缩回复表达 | 用户明确要求极简回复 |

## 核心使用顺序

涉及新项目或新系统时，用 project-workflow 做入口，按实际情况走这些阶段：

1. 流程型系统先用 sop-feasibility-review；有通用 SOP 再用 sop-organizer。
2. 新想法用 brainstorm；需求确认后需要正式基线再用 to-prd。
3. 没有项目规则时用 agents-md-init。
4. 读取现有代码：简单任务直接查相关模块；复杂任务用 zoom-out，再按需要用架构或重构 skill。
5. 实现时只加载相关的数据库、React、表格、多语言或设计专项 skill。
6. 完成后必须用 acceptance-check；发现问题时 qa 负责收集，app-diagnose 负责定位和修复。

## 哪些是核心，哪些是可选

核心：project-workflow、brainstorm、sop-feasibility-review、to-prd、qa、app-diagnose、acceptance-check、karpathy-guidelines。

条件触发：sop-organizer、agents-md-init、database-model-docs、zoom-out、improve-codebase-architecture、request-refactor-plan、frontend-design、impeccable、design-polish。

技术专项：antd-table-guide、i18n、react-hook-best-practices。它们不是每个项目都需要，不应默认加载。

维护和表达：skill-creator 只用于维护本仓库；caveman 只改变回复长度，不参与业务开发流程。

已处理的重叠：

- impeccable 负责设计上下文和新页面方向；frontend-design 负责已有方向的前端实现；design-polish 负责已有页面的整体精修。
- qa 负责把问题说清楚；app-diagnose 负责在问题已确认后找根因和修复。
- sop-feasibility-review 负责能不能做；sop-organizer 负责如何适配当前项目。

因此没有删除技术专项，但它们不属于核心入口；真正不需要默认加载的是 caveman、技术专项和只在特定项目才触发的数据库/架构类 skill。

## 验证

使用 Python 3 运行所有 skill 的结构校验：

    for d in plugins/ai-development-sop/skills/*/; do python3 skill-creator/scripts/quick_validate.py "$d"; done

当前仓库没有具体业务应用，也没有统一测试命令；skill 的行为验证应在目标项目中执行，重点检查触发边界、阶段门和验收报告是否被遵守。

## 当前范围

本仓库是可安装的 AI 开发 SOP 插件，不包含一个具体的业务应用。各 skill 会读取使用它们的目标项目，以目标项目中的实际文件和配置为准。
