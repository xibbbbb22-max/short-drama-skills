# short-drama-skills

用于 AI 短剧和漫剧制作的一组 skill：从选题、剧本、分镜到审片和作品介绍。

| Skill | 用途 |
|---|---|
| `short-drama-producer` | 统筹制作路径、排期、生成预算、素材进度和返工交付 |
| `short-drama-writer` | 选题、素材改编、剧本写作和局部改稿 |
| `short-drama-director` | 角色与场景规范、分镜表、逐镜头提示词和时长核对 |
| `short-drama-review` | 审查剧本、分镜和成片，给出定位明确的最小返工方案 |
| `short-drama-pitch` | 片名、作品简介和路演讲稿 |

每个 skill 目录下的 `agents/openai.yaml` 是 Codex 的界面信息（显示名、简介、默认提示词）；在 Codex 中可用 `$short-drama-producer` 等名称调用。

## 安装

五个目录一起放进所用 Agent 的同一个 skills 目录，保持同级：

```sh
cp -r short-drama-* <skills 目录>/
```

writer、director、review、pitch 通过 `../short-drama-producer/references/` 读取比赛参考，director 还读取平台核实记录。单独安装其中某个 skill 时这些链接会失效，需要在对话中直接提供相应内容。

## 参考文件

| 文件 | 内容 |
|---|---|
| `short-drama-producer/references/maimai-13-competition.md` | 脉脉 13 周年 AI 漫剧大赛规则快照及现场排期建议；仅在用户指向该比赛时读取 |
| `short-drama-producer/references/platform-verification.md` | 制作平台能力的核实结果、来源和日期；赛前填写，现场复核 |
| `short-drama-writer/references/script-example.md` | 完整剧本的格式与估时示例 |
| `short-drama-director/references/storyboard-example.md` | 角色与场景固定描述块、镜头表和逐镜头提示词示例 |

## 外部依赖

以下 skill 不在本仓库中，只在环境中可用且任务需要时调用：

| 依赖 | 使用位置 | 不可用时 |
|---|---|---|
| `lark-doc` | producer、review 读取飞书文档；更新比赛规则快照 | 请用户粘贴文档内容或提供导出文件 |
| `imagegen` | producer、director 生成角色图、场景图或封面 | 只交付文字规范和提示词 |
| `presentations` | pitch 在用户要求时制作幻灯片 | 只交付讲稿文字，并说明未制作幻灯片 |

本仓库不包含视频生成、配音或剪辑能力；这些步骤需要实际可用的平台或工具。
