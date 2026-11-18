# Systematic debugging：接入与实验结果

增加最小复现、边界追踪、单一因果假设和针对性验证的文本技能，区分起点已有失败与本次回归。

## 接入方式

沿用仓库 `skills/roadmap-decomposition/` 的普通文本 Skill 打包方式。将本目录的 `SKILL.md` 作为控制台文件 Skill bundle 导入并绑定到 Dev；配置和固定版本机制见 [角色池](../role-pool.md)。如使用 repository 来源，文件必须先进入目标项目规则缓存支持的 `.agents/skills/<名称>/SKILL.md`，刷新规则后以明确 commit 和 paths 固定并绑定。仅把文件放入 Bot 自身的 `skills/` 目录不会自动注入运行角色。

正文与实验使用的适配版一致；不是完整原版 Superpowers。来源和 MIT 许可随技能保留，历史实验未记录上游原版 revision，`SOURCES.json` 明确记为 null。

## 结果来源与范围

以下结果转述自 2026-11-18 交付包 v2 的《Bot Skill 三组实验总结》（`00-实验总结.md`），本 PR 未重新运行模型实验。只提供汇总，不包含私仓源码、凭据或完整实验归档。

## 双 Skill 的 SWE-Milestone 006 验证

Navidrome `milestone_006` 使用 `deepseek-flash`，Dev 加入 TDD 和 systematic-debugging。历史 Base 与双 Skill 的源文件清单排除 Skill 文件后，路径和 blob SHA 无差异；运行时间和环境未完全同步锁定。

| 指标 | 历史 Base | 双 Skill |
|---|---|---|
| 开发交付 | 已开 PR，QA pass | 已开 PR，开发阶段约 29 分 28 秒 |
| 评分结果 | infra_invalid，实际执行 0 项 | 功能 7/7、回归 1063/1063 |
| 有效功能成绩 | 未取得 | resolved=true，计分范围内零回归失败 |

双 Skill 配置完成需求→实现→PR→有效评分链路，目标功能与固定回归全部达标。Base 的停点是评分基础设施／候选应用链路无效，不是开发未交付，也不是执行功能测试后失败；不能将 0 项执行写成 0/7 或据此计算功能胜率提升。

评分有 `partial_test_universe` 和 Go 插件编译问题，“通过”仅指固定分类内的功能和回归要求，不代表全仓测试全绿。该实验同时配置两项 Skill，不能单独归因于 systematic-debugging，也不足以证明稳定收益。本 PR 可独立合入；复现组合实验仍需另外配置 TDD。

## 完整 Roadmap 组合实验的边界

完整 Roadmap＋Bot＋DigitalMate 对比中，Base 与三 Skill 配置组均为独立 QA `pass_with_issues`、固定回归 44/44；Base 父任务至 PR 约 5 小时 1 分，Skill 组约 9 小时 56 分，本轮未观察到整体效率优势。

期间模型、并发和人工恢复影响耗时。日志仅确认 Manager 读取 roadmap-decomposition，未找到 Dev 读取 TDD／systematic-debugging 的记录。配置三项不等于三项都实际生效；这些是适配版本，也不能直接代表完整原版 Superpowers。
