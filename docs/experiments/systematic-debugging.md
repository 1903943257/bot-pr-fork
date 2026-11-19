# systematic-debugging：接入与实验结果

先复现故障，再沿组件边界验证根因并复测。 Skill 正文沿用实验中的简短适配版，附来源与 MIT 许可。

## 接入方式

1. 在项目角色设置中创建控制台文件 Skill bundle，加入 `test-driven-development/SKILL.md` 和 `systematic-debugging/SKILL.md`，并绑定给 Dev。也可将文件放入目标项目的 `.agents/skills/<名称>/SKILL.md`，刷新项目规则、固定提交和路径，再绑定。见[角色配置](../role-pool.md)。
2. 常规使用可让 Dev 按需读取。要复现实验，在 Dev 的 `persona_prompt` 末尾追加：「每次开发委派开始时，在调查或编辑前，用 `read_skill` 按路径读取绑定的 `SKILL.md` 正文并遵循其指引。」双 Skill 配置要指定两条路径；按包里实际显示的路径填写。
3. 启动新任务，检查 Dev 的 `skill_read` 日志是否记录了相应文件。只看到文件列表表示技能可用。合入本 PR 只提供技能文件，现有 Bot 运行时代码无需修改。

## Navidrome 双 Skill 复跑（2026-11-18）

| 设置 | 内容 |
| --- | ---: |
| 任务 | SWE-Milestone v1.0.2，Navidrome `milestone_006`，五项 UI 改进 |
| 共用基线 | Navidrome `adbd68b`；Bot `753cef62`；Native 后端；同一 `DeepSeek-V4.1-Flash-1017` API；同一验收门槛 |
| 分组 | Base 无额外 Dev Skill；双 Skill 绑定 TDD 和系统化调试，并要求 Dev 开工先读两份正文 |

按 Dev 各轮的实际起止时间累计开发用时。双 Skill 组前三轮各读取两份正文，首轮后续模型请求中核验到完整正文。

| 指标 | Base | 双 Skill |
| --- | ---: | ---: |
| 独立 QA | pass | pass |
| 官方功能 / 回归 | 7/7 / 1063/1063 | 7/7 / 1063/1063 |
| Dev 累计耗时 | 34 分 07 秒 | 27 分 14 秒（−20.2%） |
| Dev 模型请求 | 98 | 94 |
| Dev 输入 token（含缓存） | 8,709,794 | 7,647,349（−12.2%） |
| Dev 输出 token | 155,436 | 100,992（−35.0%） |
| 任务创建到开 PR | 1 小时 52 分 03 秒 | 2 小时 36 分 50 秒 |

**双 Skill 组功能和回归同分，Dev 少用 6 分 53 秒（20.2%），输出 token 少 35.0%。** 发布恢复延长了整轮交付。本轮只验证组合，无法分离单项贡献。 双 Skill 组在候选提名后重试了发布标签和测试依赖恢复，最终发布时未改动候选 Git 树。将两轮恢复也计入，双 Skill 所有 Dev 运行合计 30 分 39 秒、105 次请求。功能与回归是固定评分分类，评分范围不覆盖全仓测试。上一次仅绑定技能未确认读到正文，不计为有效双 Skill 对照。

本实验没有单独运行 `systematic-debugging`，两份 Skill 可以各自安装。
