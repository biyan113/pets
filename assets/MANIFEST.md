# Character Asset Manifest — Chibi Sailor Girl

## 主对齐基准（后续所有状态行强制对齐）

| 项 | 值 |
|---|---|
| **MASTER 文件** | `character/chibi_sailor/MASTER_REF.jpg` |
| 用途 | 后续每一行状态/变体生成时的 **唯一身份参考** |
| 生产 | 由 `char_front_full` edit-chain，纯白底干净主参考图 |
| 姿态 | 正面全身站立，双臂微张便于读轮廓 |

### 冻结识别点（每一行不得改变）

| 识别点 | 冻结内容 |
|--------|----------|
| 发型 | 齐肩深棕短发 + 齐刘海 + 头顶 ahoge（画面偏右） |
| 服装 | 蓝白水手服：白上衣 / 海军蓝领与袖口条纹 / 红蝶结金扣 / 海军蓝百褶短裙 |
| 袜 | 黑色过膝袜 |
| 脸 | 圆脸、大眼（深棕虹膜）、粉腮红 |
| 气质 | 元气活泼（默认开朗微笑基调；状态行可改表情，不可改脸型与五官结构） |
| 比例 | Chibi：头大身短 |
| 风格 | 2D cel-shaded、黑描边、软分层 |
| 底 | 纯白/可抠纯色，无场景无投影 |

> 后续状态行：一律 `image_edit`，输入 **MASTER_REF**，prompt 写  
> `Keep this exact character — same hair, face, sailor uniform, black over-knee socks, chibi proportions, style — change only <状态>`。

## Style Contract

| 项 | 约定 |
|---|---|
| 介质 | 2D 动画风 cel-shaded 游戏角色立绘 |
| 比例 | Chibi：头约占身高 2/5，短肢圆手 |
| 描边 | 干净黑色轮廓线 |
| 着色 | 软 cel 分层，腮红粉润 |
| 背景 | **主基准纯白**；其他行默认可抠纯色，无地面影/无场景 |
| 光向 | 正面柔光，轻微体积阴影 |
| 身份锚点 | 见上方「冻结识别点」；以 `MASTER_REF.jpg` 为唯一真源 |

## 角色设定（原创）

- **气质**：元气活泼、圆脸大眼
- **发型**：齐肩深棕色，齐刘海，头顶小 ahoge
- **服装**：蓝白水手服（白上衣 / 海军蓝领与蓝袖口条纹 / 红领结 / 海军蓝百褶短裙）
- **袜鞋**：黑色过膝袜 + 深蓝便鞋
- **禁止**：不参考任何既有动漫/游戏角色

## 交付清单

| 文件 | 内容 | 画幅 |
|------|------|------|
| `character/chibi_sailor/MASTER_REF.jpg` | **主对齐基准**（纯白底正面全身） | 3:4 |
| `character/chibi_sailor/char_front_full.jpg` | 正面全身站立（灰底初稿） | 3:4 |
| `character/chibi_sailor/char_side_half.jpg` | 侧面半身（严格 profile） | 3:4 |
| `character/chibi_sailor/expr_smile.jpg` | 表情：微笑 | 1:1 半身特写 |
| `character/chibi_sailor/expr_focus.jpg` | 表情：专注 | 1:1 半身特写 |
| `character/chibi_sailor/expr_dejected.jpg` | 表情：沮丧 | 1:1 半身特写 |
| `character/chibi_sailor/pose_wave.jpg` | 挥手姿态全身 | 3:4 |
| `character/chibi_sailor/char_side_full_bonus.jpg` | 侧面全身（附加参考） | 3:4 |

### 状态行（对齐 MASTER_REF）

目录：`character/chibi_sailor/states/`  
全部由 `MASTER_REF.jpg` edit-chain，只改动作/表情。

| 文件 | 状态 | 动作要点 |
|------|------|----------|
| `state_idle.jpg` | 待机 | 正面站立，闭口轻笑，双臂自然下垂 |
| `state_move_right.jpg` | 向右移动 | 右侧面行走中步态 |
| `state_move_left.jpg` | 向左移动 | 左侧面行走中步态 |
| `state_wave.jpg` | 挥手 | 正面，右手高举挥手，开朗笑容 |
| `state_jump.jpg` | 跳跃 | 腾空双腿收起，双臂上扬 |
| `state_fail.jpg` | 失败沮丧 | 正面，垂肩，泪珠，瘪嘴 |
| `state_wait_confirm.jpg` | 等待确认 | 双手合十胸前，期待微笑 |
| `state_processing.jpg` | 运行中 | **非奔跑**；站立专注打字处理任务（含迷你键盘道具） |
| `state_check_results.jpg` | 检查结果 | 托腮思考 + 另一手托举展示，评估神情 |

### 方向行（头部/眼神一整圈）

目录：`character/chibi_sailor/looks/`  
只动头颈与眼睛；身体/水手服/过膝袜姿态冻结。  
**screen-left / screen-right = 画面左右边缘，不是角色自身左右手。**

| 文件 | 朝向 |
|------|------|
| `look_front.jpg` | 正面（= MASTER_REF） |
| `look_up.jpg` | 向上 |
| `look_up_screen_right.jpg` | 上 + 画面右 |
| `look_screen_right.jpg` | 画面右 |
| `look_down_screen_right.jpg` | 下 + 画面右 |
| `look_down.jpg` | 向下 |
| `look_down_screen_left.jpg` | 下 + 画面左 |
| `look_screen_left.jpg` | 画面左 |
| `look_up_screen_left.jpg` | 上 + 画面左 |

### Spritesheet + 配置

| 文件 | 说明 |
|------|------|
| `character/chibi_sailor/sheet/chibi_sailor_spritesheet_v2.webp` | **Codex v2 正式图集** 8×11 / 192×208 / 1536×2288 |
| `character/chibi_sailor/sheet/chibi_sailor_spritesheet_v2.png` | PNG 中间件 |
| `character/chibi_sailor/sheet/chibi_sailor_spritesheet.webp` | 旧草稿（9×2，勿装进 Codex） |
| `character/chibi_sailor/character.json` | 项目内角色配置（草稿用） |

### Codex 安装路径

```
/Users/pan/.codex/pets/xiaoqing/
├── pet.json              # spriteVersionNumber: 2
└── spritesheet.webp      # 1536×2288，validate_atlas --require-v2 通过
```

- 单元格：192×208  
- 网格：8 列 × 11 行  
- 行 0–8：状态（当前为 hold 帧，非完整动画序列）  
- 行 9–10：16 方向（由 9 张 look 最近邻填充）  
- 行 0 列 6：v2 neutral look（正面）

## 生产链路

1. `image_gen` 出正面全身 base  
2. edit-chain 得 `MASTER_REF`  
3. 设定图变体（侧/表情/挥手）edit-chain  
4. 九状态行全部 `image_edit` 自 MASTER_REF  

## 已知缺陷 / 有意偏离

| 项 | 说明 |
|----|------|
| 侧面半身闭眼 | `char_side_half` 为闭眼柔和 profile，非睁眼参考；侧面全身 bonus 为睁眼 |
| 鞋色 | 深蓝便鞋（非纯黑），与裙子同色系 |
| 文件格式 | 生成器输出 JPEG，扩展名 `.jpg` |
| 专注表情 | 略偏「认真凝视」而非「看书皱眉」，避免怒气误读 |
| 运行中道具 | `state_processing` 增加迷你键盘以表达「处理任务」；非奔跑 |
| 挥手脚位 | `state_wave` 双脚略开，带元气弹跳感 |

## 引擎接入建议

- 纯白底可用色键或抠图；轮廓已干净  
- 全身立绘适合 UI 角色卡 / 对话立绘缩放  
- 表情特写适合对话框头像或状态反馈  
- 状态行可直接映射 agent/任务 UI：idle / move / wave / jump / fail / wait / processing / check  
- 挥手姿态适合问候 / 引导交互  
