# Test-driven development：接入与实验结果

增加修改实现前观察预期断言失败、最小实现后用同一测试验证通过的文本技能；行为保持的重构使用 characterization test。

## 接入方式

沿用仓库 `skills/roadmap-decomposition/` 的普通文本 Skill 打包方式。将本目录的 `SKILL.md` 作为控制台文件 Skill bundle 导入并绑定到 Dev；配置和固定版本机制见 [角色池](../role-pool.md)。如使用 repository 来源，文件必须先进入目标项目规则缓存支持的 `.agents/skills/<名称>/SKILL.md`，刷新规则后以明确 commit 和 paths 固定并绑定。仅把文件放入 Bot 自身的 `skills/` 目录不会自动注入运行角色。

正文与实验使用的适配版一致；不是完整原版 Superpowers。来源和 MIT 许可随技能保留，历史实验未记录上游原版 revision，`SOURCES.json` 明确记为 null。

## 结果来源与范围

以下结果转述自 2026-11-18 交付包 v2 的《Bot Skill 三组实验总结》（`00-实验总结.md`），本 PR 未重新运行模型实验。只提供汇总，不包含私仓源码、凭据或完整实验归档。

## Navidrome 单 TDD 对照

使用 SWE-Milestone v1.0.2 的 Navidrome `milestone_006`，两组从相同官方起点 `adbd68b` 启动，模型均为 `deepseek-flash`。实验组只增加 TDD，目标为菜单事件、ReplayGain、年份显示、错误图标和歌单删除符号五项 UI 改进。

| 指标 | Base | 单 TDD |
|---|---:|---:|
| 首次自主运行 | needs_replan | 完成交付 PR |
| 首次累计运行时间 | 121.5 分钟 | 80.6 分钟 |
| 模型请求 | 820 次 | 606 次 |
| 后续完成条件 | 人工介入后完成并补齐评分 | 首次自主运行已交付 |
| 后续功能／回归评分 | 7/7、1063/1063 | 7/7、1063/1063 |

本轮 TDD 组自主交付，Base 需要人工恢复；首次快照中 TDD 少用 26.1% 请求、33.7% 运行时间，并保留旧实现失败、修复后通过的回归证据。

时间比较止于 Base 的待重规划停点，不是最终完成总成本。两组 QA 对额外代码的判定存在差异，不能把全部差距归因于 TDD；人工恢复后的同分也不等于自主完成能力相同。

两组评分都有 `partial_test_universe` 和 Go 插件编译问题，7/7、1063/1063 只代表固定分类内的功能与回归要求通过，不代表全仓测试全绿。样本不足以证明稳定收益。

## 其他组合实验的边界

TDD＋systematic-debugging 的 Navidrome 006 实验达到功能 7/7、回归 1063/1063；历史 Base 已开 PR、QA pass，但评分为 infra_invalid、实际执行 0 项，不能由此计算功能胜率提升或分离两项技能的贡献。

完整 Roadmap＋Bot＋DigitalMate 实验中，两组均为独立 QA `pass_with_issues`、固定回归 44/44。Base 父任务至 PR 约 5 小时 1 分，三 Skill 配置组约 9 小时 56 分，本轮未观察到整体效率优势。模型、并发和人工恢复有变更；仅确认 Manager 读取拆分 Skill，未找到 Dev 读取另外两项的记录，因此配置不等于实际生效。
