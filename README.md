# ASA-Translation

《方舟：生存飞升》(ARK: Survival Ascended) 社区中文翻译数据仓库。

本仓库以 `.jsonc` 格式存放游戏文本翻译数据，由配套的方舟翻译工具读取并注入游戏本地化。仓库只维护翻译数据本身，不包含工具代码。

## 目录结构

```
ASA-Translation/
├── 000-OBT.jsonc              # OBT 测试分支文本
├── 001-Official.jsonc         # 正式服文本
├── Gen1-SpokenText/           # 创世纪 Part 1 语音台词（源文为德语/日语）
│   ├── HLN-A_DE.jsonc         #   HLN-A 向导语音（德语源）
│   ├── HLN-A_JA.jsonc         #   HLN-A 向导语音（日语源）
│   ├── VRBoss_DE.jsonc        #   VR Boss 台词（德语源）
│   └── VRBoss_JA.jsonc        #   VR Boss 台词（日语源）
└── Mods/                      # 第三方模组翻译（按编号-名称命名）
```

## 条目格式

所有翻译条目遵循统一结构：

```jsonc
{
  "NamespaceHash": "Content::602683638",   // 游戏内字符串的哈希定位，不可修改
  "Source": "英文/德文/日文原文",            // 游戏原文，不可修改
  "Trans": {
    "SC": "简体中文译文",                     // 简体中文（主要维护列）
    "JA": ""                                 // 日文（预留列）
  },
  "Config": {
    "Item": false,        // 是否为物品名（用于物品名覆盖）
    "Dino": false,        // 是否为恐龙名（用于恐龙名覆盖）
    "Default_Hash": ""    // 默认哈希（特殊用途）
  }
}
```

注意事项：

- **不要修改** `NamespaceHash` 和 `Source`，只编辑 `Trans` 中的译文。
- 译文中的换行请使用 `\n` 表示。
- 文件支持注释（`//`），可用于记录翻译依据、修订说明等，但请勿注释掉有效条目残留造成混淆。

## 主要文件分节说明

### 000-OBT.jsonc（OBT 测试分支）

| 节名 | 说明 |
|---|---|
| `OBT` | OBT 分支主体文本 |
| `Revise` | 术语修订条目 |
| `TC` | 繁体中文转换条目（SC 为繁中写法） |

### 001-Official.jsonc（正式服）

| 节名 | 说明 |
|---|---|
| `Official` | 正式服主体文本 |
| `Revise` | 生物名称修订（如 牛龙 → 肉食牛龙，附考据注释） |
| `CreatureDossier` | 生物图鉴长文本 |
| `LostColonyVoice` | 失落殖民地语音（待填充） |
| `DT_Milestones_LC` / `TidesOfFortune` / `Dragontopia` / `Bounties` | 各活动里程碑与任务文本 |
| `TC_A2B` | 简→繁字符替换字典（非翻译条目，勿增删普通条目） |
| `TC_A2B_2` | 繁中转换例外/强制结果（避免与 `TC_A2B` 冲突，最后执行） |
| `Version` | 版本显示文本 |

### Gen1-SpokenText

HLN-A 向导与 VR Boss 的语音台词。源文分别为德语（`_DE`）与日语（`_JA`），`Trans.SC` 为对应的简体中文翻译。节名（如 `Functional`、`Glitches`、`Missions`、`Cinematics`、`Store`）须与游戏字符串表严格一致，**请勿改动节名**。

## 贡献流程

1. Fork 本仓库并创建分支。
2. 编辑对应 `.jsonc` 文件，补齐或改进译文。
3. 提交前自查：
   - 文件可正常解析为 JSONC（注意逗号、引号、括号配对）；
   - 节名与条目结构未被改动；
   - 同一文件内 `NamespaceHash` 无重复。
4. 发起 Pull Request，简要说明改动内容（如：新增翻译 / 修订译文 / 修复错误）。

## 翻译约定

- 游戏专有名词请参考 `Revise` 节中的既有译名，保持一致。
- 生物译名建议在注释中附简要考据（学名词根含义等），便于后续审校。
- 无法确定译法的条目可保留 `SC` 为空并在条目旁添加注释说明原因。
