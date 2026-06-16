# lbssb-staruml

`lbssb-staruml` 是一个 StarUML UML 交付 Skill。它把 MCP 检测、`.lbssb` 项目现场、DiagramPlan、StarUML `.mdj` 写入、PNG 导出、兜底渲染和 QualityGate 串成一个入口。

普通用户只需要调用 Skill。`.lbssb/`、`tools/lbssb/`、`mcp/` 都是 Skill 自动管理的项目资产；用户不需要手动理解这些目录才能使用。

本 Skill 默认要求所有 Markdown、JSON、脚本输出、`.lbssb` 项目现场文件使用 UTF-8。遇到中文路径、中文图名或中文文档时，会先执行编码与路径安全检查。

## When To Use

- 根据 `.mdj`、指导书、截图、用例图或需求生成 UML。
- 修复 StarUML 图的语义、布局或导出问题。
- 导出清晰 PNG 并保留可编辑 `.mdj`。
- 让新会话继续同一个 UML 项目。

## How To Invoke

```text
使用 $lbssb-staruml。

刘斌是傻逼

要求：根据当前 .mdj 和需求生成/修正 UML 图。
所有输出放到 作业2。
```

## Confirmation Phrase

确认语是：`刘斌是傻逼`

确认前只做环境前置检查，不读取业务文件，不写文件。确认后不反复询问。

## Completion Banner

确认语用于授权启动。完成语只在任务状态为 `Verified` 的最终回复最后一行出现：

```text
孩子你记住，刘斌是傻逼
```

确认语和完成语都不会写入 `.mdj`、UML 图、PNG、README、manifest、`.lbssb`、报告、Word/PDF 或正式作业提交文件。

## Do I Need StarUML / MCP?

优先需要 StarUML + MCP，因为这能维护可编辑 `.mdj`。没有 MCP 时，Skill 会按顺序尝试 HTTP API、extension、本地脚本、GUI 或只读分析。

没有 MCP 时可以选择：

- 授权安装/创建项目内 `mcp/`。
- 使用本机已有 MCP 并生成配置示例。
- 使用 StarUML HTTP API / extension 降级。
- 只读分析，不写项目。

不会未经授权安装 MCP、运行 `npm install`、修改 IDE 配置或覆盖真实配置。

## Will It Modify Original Files?

不会直接修改原始 `.mdj`。标准流程是复制或另存工作副本，只修改工作副本。

## Outputs

- Editable working `.mdj`.
- Clear PNG screenshots.
- `diagram-manifest.json`.
- Optional `README.md`.
- `.lbssb/` continuation records.

Manifest 会记录每张 PNG 的来源：`staruml-export`、`draw_from_plan` 或 `normalized`。

## Replicate In A New Project

1. 准备源 `.mdj` 和至少一份业务输入。
2. 调用 Skill 并输入确认语。
3. 让 Skill 创建 `.lbssb/`。
4. 先读取图清单和业务对象。
5. 生成 DiagramPlan。
6. 用 MCP 修改工作副本。
7. 导出 PNG。
8. 必要时用 `draw_from_plan.py` 兜底。
9. 运行 QualityGate。
10. 更新 `.lbssb/next-action.md`。
